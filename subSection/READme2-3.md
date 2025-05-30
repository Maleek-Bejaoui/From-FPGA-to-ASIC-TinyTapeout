## 2.3.  Résultats et Analyse du CPU RISC_V

### Travail réalisé
Ici des codes en Systme Verilog nous ont été fournis. Il s'agissait d'un CPU RISC V. Pour l’adapter au flux de conception TinyTapeout, nous n’avons pas modifié directement le code SystemVerilog généré, mais ajusté les options de compilation de **chisel3** afin d’obtenir un Verilog propre, synthétisable, et compatible avec les contraintes d’OpenLane. Nous avons notamment désactivé l’ajout automatique du mot-clé automatic, qui posait problème lors de la synthèse ASIC, puis nous avons complété le fichier top.v pour bien associé les signaux et permettre l'utilisation de TinyTapeout.

Voici la commande utilisée :

```Markdown
object TT extends App {
  _root_.circt.stage.ChiselStage.emitSystemVerilog(
    new TT(),
    firtoolOpts = Array.concat(
      Array(
        "--disable-all-randomization",          // Supprime l'insertion de valeurs aléatoires pour l'initialisation des registres (utile uniquement pour la simulation)
        "--strip-debug-info",                   // Supprime les informations de debug inutiles dans le fichier Verilog final
        "--split-verilog",                      // Génère un fichier Verilog par module, au lieu d’un seul fichier global
        "--lowering-options=noAlwaysCombNoSyncReg" // Évite d’utiliser les blocs always_comb ou always_ff avec `automatic`, ce qui améliore la compatibilité avec la synthèse ASIC
      ),
      args
    )
  )
}
```

Design fourni par **M. Mathieu Escouteloup** sur GitLab.  
© Tous droits réservés à M. Mathieu Escouteloup.

🔗 [riscv-chisel-design](https://gitlab.com/escou64/riscv-design).

### Obtention des résultats

De la même manière que pour le compteur 8 bits et le CPU précédemment détaillé, nous avons pu observer les résultats dans la partie GDS de "Actions" sur Github.

### Résultats obtenus

GitHub nous fournit des informations clés pour la conception d'un ASIC, notamment les cellules utilisées, l'empreinte de notre projet sur l'ASIC sélectionné, ainsi que des visualisations 2D et 3D de notre projet sur la puce.

Nous avons fait varier la taille de la RAM.
Ainsi on a obtenu les résultats suivants pour notre CPU


| RAM (octets) | Cellules utilisées |
|--------------|--------------------|
| 16           | 6931               |
| 32           | 7465               |
| 64           | 8530               |
| 96           | 9750               |
| 128          | 10778              |


Grâce à ces valeurs nous pouvons effectuer une régression linéaire du nombre totale de cellules utilisées en fonction de la taille de la RAM en octets:

![Graphique RAM vs Cellules](../images/RISCVvsRAM.png)

Avec cette régression nous en tirons une équation liant taille de la RAM et cellules utilisées:
```
Nombre de cellules utilisées = 34.68 x Taille_de_RAM(en octets) + 6360.54
```
Donc on peut estimer la taille de **notre CPU RISC V sans RAM: environ 6 360 cellules.**

🔗 Le projet complet est disponible ici : [Implémentation d’un processeur RISC-V sur le template TinyTapeout](https://github.com/Maleek-Bejaoui/RISC_V_ASIC).


Ce petit  travail finam nous a permis de maîtriser la conception d'un CPU RISC-V et d'appréhender l'impact des ressources mémoire sur la taille du circuit intégré. Grâce à l'utilisation de TinyTapeout et GitHub, nous avons observé un gain de temps à la génération des résultats et des visualisations. La régression linéaire nous a permis de prédire le nombre de cellules nécessaires en fonction de la taille de la RAM, offrant ainsi une méthode efficace pour anticiper les besoins en ressources. En somme, cette expérience nous a préparés à concevoir et analyser rapidement des ASICs pour des projets futurs.


### 🚨 Remarque très importante : Comportement inattendu des Flip-Flops synthétisés

Nous avons analysé l’évolution du nombre de flip-flops utilisés dans la synthèse en fonction de la taille de la RAM interne :

| Taille RAM (octets) | Flip-Flops synthétisés | Cellules totales (`NbrCells`) |
|---------------------|------------------------|-------------------------------|
| 128                 | 1942                   | 10778                         |
| 256                 | 1942                   | 10777                         |
| 272                 | 1046 (**diminue**)     | 6874 (**diminue fortement**)  |

Selon la [documentation officielle de TinyTapeOut sur la mémoire](https://tinytapeout.com/specs/memory/), la mémoire est implémentée à l’aide de bascules (DFF) synthétisées à partir de cellules logiques standards. Aucune macro SRAM n’est utilisée.

À partir de la taille **128 octets**, nous observons une **baisse soudaine** du nombre de flip-flops, ce qui est **contre-intuitif**. En effet, on s’attendrait à ce que **le nombre de flip-flops augmente proportionnellement** avec la taille de la RAM. De plus, le **nombre total de cellules logiques** utilisées dans la synthèse diminue également, alors qu’il devrait logiquement croître avec l’augmentation de la mémoire.


---
