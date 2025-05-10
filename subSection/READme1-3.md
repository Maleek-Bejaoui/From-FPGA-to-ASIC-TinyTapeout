##  1.3 – Passage au Verilog manuel

Face aux limitations rencontrées avec les traductions automatiques VHDL → Verilog, nous avons fait le choix de **réécrire manuellement notre CPU 16 bits** en Verilog.  
Cette étape a demandé plus de temps, mais elle nous a permis d’avoir **un contrôle total sur la structure, la lisibilité et la synthétisabilité** du design dans le flot TinyTapeout.

---

### Ce qu’il faut éviter lors de la réécriture

Afin d’assurer une bonne compatibilité avec la synthèse ASIC, plusieurs pratiques doivent être évitées :

-  L’utilisation de constructions complexes ou ambiguës (ex. : `initial`, `for generate`, types non signés...).
-  Déclarations implicites ou signal sans typage clair.
-  Noms de signaux non normalisés ou trop longs.
-  Utilisation de noms qui **entrent en conflit avec des mots-clés Verilog** (ex : `byte`, `input`, `case`, etc.).
-  Écriture non cohérente à la casse (Verilog étant **sensible à la casse**, contrairement à VHDL).
-  Machines d'états sans `localparam` → les états doivent être **clairement définis** avec `localparam` pour être synthétisables proprement dans OpenLane.

---

### Débogage par test croisé VHDL ↔ Verilog

Pour **accélérer le débogage** de chaque composant recodé en Verilog, nous avons utilisé une approche pragmatique dans **Vivado** :

- Nous avons pris notre design **fonctionnel en VHDL** comme référence stable.
- Puis, **bloc par bloc**, nous avons remplacé les composants VHDL par leurs équivalents Verilog nouvellement écrits.
- Vivado permet le **mélange des langages VHDL et Verilog dans un même projet**, ce qui nous a permis de :
  - isoler rapidement les erreurs,
  - valider chaque module indépendamment,
  - avancer plus efficacement et en toute confiance.

La méthode de validation est simple, basée sur **trois étapes répétées pour chaque bloc** :

1. **Traduction manuelle** d’un composant du CPU depuis VHDL vers Verilog.
2. **Simulation RTL** dans Vivado pour vérifier que le module fonctionne comme prévu.
3. **Implémentation sur carte FPGA (Artix-7)** pour tester le comportement réel du composant dans un environnement physique.

⚠️ Ce processus est essentiel car **la simulation seule ne suffit pas toujours** : certains modules peuvent fonctionner parfaitement en simulation, mais présenter des dysfonctionnements lors de l’implémentation réelle sur FPGA (ex : problèmes de timing, d’initialisation ou de synchronisation).

Grâce à cette approche hybride, nous avons pu corriger les incompatibilités **au fur et à mesure**, avant d'intégrer chaque bloc dans le design final Verilog destiné à TinyTapeout.
