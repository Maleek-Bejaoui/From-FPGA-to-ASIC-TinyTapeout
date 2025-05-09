# Projet ASIC – Conception d’un compteur 8 bits avec TinyTapeout

Ce projet a pour objectif de concevoir un composant simple (compteur 8 bits) en VHDL et Verilog, de le tester sur FPGA (Artix-7), puis de l’implémenter dans un flot de fabrication ASIC via la plateforme open source [TinyTapeout](https://tinytapeout.com/).

Il s'agit d'une première étape dans notre démarche de développement d'un processeur 16 bits compatible avec TinyTapeout.

---

## 1.1.  Premiers essais : Compteur 8 bits

###  Implémentation en VHDL

Nous avons conçu un compteur 8 bits synchrone en VHDL avec remise à zéro asynchrone. Ce module a été :

- simulé sous **Vivado**.
- testé sur **carte FPGA Artix-7**.
- et retenu comme point de comparaison pour la version Verilog.

### Implémentation en Verilog

Nous avons également développé une version équivalente du compteur en Verilog. Les étapes suivantes ont été réalisées :

1. **Écriture manuelle** du code Verilog, équivalent fonctionnel au design VHDL.
2. **Simulation** du module sous **Vivado** pour valider le comportement RTL.
3. **Implémentation sur carte FPGA Artix-7**.

Cette double implémentation (VHDL et Verilog) nous a permis de mieux comprendre les contraintes de portabilité et les exigences de la plateforme TinyTapeout.

---

###  Synthèse via TinyTapeout

Nous avons intégré les deux versions du compteur dans le flot de fabrication de TinyTapeout.

####  Liens des projets
- 🔗 **Compteur VHDL** : [github.com/MalekBejaoui/tto-counter-vhdl](https://github.com/Maleek-Bejaoui/tto-counter-vhdl)
- 🔗 **Compteur Verilog** : [github.com/Malek-Bejaoui/tto-counter-verilog](https://github.com/Maleek-Bejaoui/tto-counter-verilog/actions/runs/14937893261)
- 🔗 **Template TinyTapeout de base** : [github.com/TinyTapeout/tt-template](https://github.com/TinyTapeout/tt-template)

#### ⚙️ Étapes d’intégration du design dans le template TinyTapeout

Pour chaque version :

1. Création d’un dépôt GitHub à partir du template `tt-template`.
2. Ajout du fichier source (`counter.vhdl` ou `counter.v`) dans `/src`.
3. Création d’un fichier `tt_um_<nom>.v` pour lier les ports au standard TinyTapeout.
4. Instanciation du compteur dans ce top module :
   ```verilog
   counter my_counter (
       .clk(clk),
       .rst(io_in[0]),
       .out(io_out)
   );
