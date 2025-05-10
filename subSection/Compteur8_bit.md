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
- 🔗 **Compteur VHDL** : [github.com/MalekBejaoui/tto-counter-vhdl](https://github.com/Maleek-Bejaoui/tto-counter-vhdl/actions/runs/13231193350)
- 🔗 **Compteur Verilog** : [github.com/Malek-Bejaoui/tto-counter-verilog](https://github.com/Maleek-Bejaoui/tto-counter-verilog/actions/runs/14938384629)
- 🔗 **Template TinyTapeout de base** :[github.com/TinyTapeout/tt-template](https://github.com/TinyTapeout/tt10-verilog-template)

---

#### Instructions d’intégration dans le template TinyTapeout

Pour intégrer un projet Verilog dans la plateforme TinyTapeout, voici les étapes à suivre (traduction officielle des consignes TinyTapeout) :

1. Ajoutez vos fichiers Verilog dans le dossier `src`.

2. Modifiez le fichier `info.yaml` et mettez à jour les informations concernant votre projet, en prêtant une attention particulière aux champs :
   - `source_files` (liste des fichiers source),
   - `top_module` (nom du module principal).

3. Modifiez `docs/info.md` pour ajouter une **description textuelle** de votre projet.

4. Adaptez le fichier de **testbench** à votre design. Pour cela, consultez le fichier `test/README.md`.

5. Pour publier les résultats, allez dans *Settings → Pages* du dépôt et sélectionnez **GitHub Actions** comme source.

L'action GitHub fournie avec le template exécutera automatiquement la synthèse ASIC à l'aide d'[OpenLane](https://www.zerotoasiccourse.com/terminology/openlane/).

#### Chaîne de synthèse automatique via GitHub Actions

Une fois le projet correctement structuré dans le template TinyTapeout, **aucune installation locale des outils de synthèse n’est nécessaire**.  
L’action GitHub intégrée au dépôt exécute automatiquement la **chaîne complète de conception ASIC à l’aide d’OpenLane**, dès qu’un `push` est effectué.

 *Le flot de conception suit ces étapes fondamentales* :

1. **Synthesis** – Transformation du code HDL (Verilog) en netlist logique.
2. **Floorplanning** – Définition de l'organisation physique des blocs sur la puce.
3. **Placement & Routing** – Placement des cellules logiques et génération du routage des connexions.
4. **Sign-off** :
   - **LVS (Layout vs Schematic)** – Vérification que le layout correspond au schéma logique.
   - **DRC (Design Rule Check)** – Vérification du respect des règles technologiques.
   - **STA (Static Timing Analysis)** – Analyse temporelle pour garantir les performances.

À l’entrée, on fournit un fichier Verilog ; à la sortie, on obtient un **fichier GDSII**, standard pour l’envoi en fabrication.

📚 Pour plus de détails sur les fichiers générés par OpenLane :  
🔗 [OpenLane Output Files](https://www.zerotoasiccourse.com/post/openlane_output_files/)


