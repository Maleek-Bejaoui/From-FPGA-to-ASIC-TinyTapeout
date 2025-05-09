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
- 🔗 **Compteur Verilog** : [github.com/Malek-Bejaoui/tto-counter-verilog](https://github.com/Maleek-Bejaoui/tto-counter-verilog/actions/runs/14937893261)
- 🔗 **Template TinyTapeout de base** :[github.com/TinyTapeout/tt-template](https://github.com/TinyTapeout/tt10-verilog-template)

---

## 📎 Annexe – Instructions d’intégration dans le template TinyTapeout

Pour intégrer un projet Verilog dans la plateforme TinyTapeout, voici les étapes à suivre (traduction officielle des consignes TinyTapeout) :

### 🔧 Configuration de votre projet Verilog

1. Ajoutez vos fichiers Verilog dans le dossier `src`.

2. Modifiez le fichier `info.yaml` et mettez à jour les informations concernant votre projet, en prêtant une attention particulière aux champs :
   - `source_files` (liste des fichiers source),
   - `top_module` (nom du module principal).

   👉 Si vous partez d’un ancien projet TinyTapeout, utilisez l’outil de migration en ligne :  
   https://tinytapeout.com/docs/porting/

3. Modifiez `docs/info.md` pour ajouter une **description textuelle** de votre projet.

4. Adaptez le fichier de **testbench** à votre design. Pour cela, consultez le fichier `test/README.md`.

> 🔁 L'action GitHub fournie avec le template exécutera automatiquement la synthèse ASIC à l'aide d'OpenLane.

---

### 🌐 Activer GitHub Pages pour publier les résultats

Pour générer une page de résultats accessible via GitHub Pages :

- Suivez la documentation officielle :  
  https://tinytapeout.com/docs/porting/#enabling-github-pages
