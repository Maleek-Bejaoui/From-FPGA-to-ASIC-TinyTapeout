# From-FPGA-to-ASIC-TinyTapeout

Ce projet a pour but de concevoir un processeur simple en utilisant la plateforme open source [TinyTapeout](https://tinytapeout.com/). Il s’inscrit dans une démarche pédagogique visant à explorer les limites de la synthèse ASIC à partir de designs initialement conçus pour FPGA.

---

## Objectifs du projet

- Implémenter un compteur 8 bits simple comme premier test.
- Migrer un CPU 16 bits depuis une version VHDL utilisée sur FPGA vers ASIC sur TinyTapeout.
- Étudier les contraintes liées à la synthèse ASIC (cellules, RAM, etc.).

---

## Plan du rapport

### Partie 1 : Développement et Implémentation

#### [1.1. Outils et environnement](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme1-1.md)
- Vivado (simulation, test FPGA)
- Yosys (synthèse)
- GitHub (gestion de projet)
- TinyTapeout (flow de fabrication ASIC)

#### [1.2. Premiers essais – Compteur 8 bits](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme1-2.md)
- Implémentation en VHDL et Verilog
- Simulation et synthèse TinyTapeout

#### [1.3. Tentative échouée – CPU 16 bits en VHDL](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme1-3.md)
- Architecture initiale pour FPGA
- Problèmes avec la traduction automatique VHDL → Verilog (Yosys)

#### [1.4. Passage au Verilog manuel](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme1-4.md)
- Ce qu’il faut éviter lors de la réécriture
- Débogage par test croisé VHDL ↔ Verilog

#### [1.5. Comparaison VHDL vs Verilog](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme1-5.md)
- Retour d’expérience sur les deux langages
- Problèmes rencontrés et solutions adoptées

---

### Partie 2 : Résultats et Interprétations

#### [2.1. Résultats du compteur 8 bits](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme2-1.md)
  - Taille
  - Place occupée
  - Cellules utilisées

#### [2.2. Résultats et analyse du CPU 16 bit](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme2-2.md)
- Cellules utilisées
- Optimisation mémoire

#### [2.3. Résultats et analyse du CPU RISC_V](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/blob/main/subSection/READme2-3.md)
- Cellules utilisées
- Optimisation mémoire


---

> Projet réalisé par Malek Bejaoui et Cossec Célian, encadré par M. Mathieu Escouteloup.
