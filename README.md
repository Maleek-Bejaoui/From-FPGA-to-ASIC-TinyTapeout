# From-FPGA-to-ASIC-TinyTapeout

Ce projet a pour but de concevoir un processeur simple en utilisant la plateforme open source [TinyTapeout](https://tinytapeout.com/). Il s’inscrit dans une démarche pédagogique visant à explorer les limites de la synthèse ASIC à partir de designs initialement conçus pour FPGA.

---

## 🛠 Objectifs du projet

- Implémenter un compteur 8 bits simple comme premier test.
- Migrer un CPU 16 bits depuis une version VHDL utilisée sur FPGA vers ASIC sur TinyTapeout.
- Étudier les contraintes liées à la synthèse ASIC (cellules, RAM, etc.).

---

## Plan du rapport

### Partie 1 : Développement et Implémentation

#### [1.1. Premiers essais – Compteur 8 bits](https://github.com/Maleek-Bejaoui/From-FPGA-to-ASIC-TinyTapeout/edit/main/Compteur8_bit.md)
- Implémentation en VHDL et Verilog
- Test via FPGA et synthèse TinyTapeout

#### 1.2. Tentative échouée – CPU 16 bits en VHDL
- Architecture initiale pour FPGA
- Problèmes avec la traduction automatique VHDL → Verilog (Yosys)
- Incompatibilités avec la synthèse ASIC

#### 1.3. Passage au Verilog manuel
- Abandon de la traduction automatique
- Réécriture bloc par bloc du CPU en Verilog
- Ajustements pour la synthèse : RAM, interfaces, etc.

#### 1.4. Outils et environnement
- Vivado (simulation, test FPGA)
- Yosys (synthèse)
- GitHub (gestion de projet)
- TinyTapeout (flow de fabrication ASIC)

#### 1.5. Comparaison VHDL vs Verilog
- Retour d’expérience sur les deux langages
- Problèmes rencontrés et solutions adoptées

---

### Partie 2 : Résultats et Interprétations

#### 2.1. Résultats de synthèse TinyTapeout
- Cellules utilisées
- Optimisation mémoire
- Densité et limites physiques

#### 2.2. Analyse et interprétation
- Courbes et équations RAM vs Cellules
- Analyse des performances
- Observations sur la scalabilité

#### 2.3. Enseignements
- Bonnes pratiques pour TinyTapeout
- Ce qu’il faut éviter
- Améliorations futures possibles

---

> Projet réalisé par Malek Bejaoui et Cossec Célian, encadré par Mathieu Escouteloup.
