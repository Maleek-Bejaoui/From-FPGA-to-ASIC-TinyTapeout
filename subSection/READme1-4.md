##  1.4 – Outils et Environnement

Face aux limitations rencontrées avec les traductions automatiques VHDL → Verilog, nous avons fait le choix de **réécrire manuellement notre CPU 16 bits** en Verilog.  
Cette étape a demandé plus de temps, mais elle nous a permis d’avoir **un contrôle total sur la structure, la lisibilité et la synthétisabilité** du design dans le flot TinyTapeout.

---

### Vivado

Nous avons utilisé Vivado pour simuler et tester le compteur en Verilog afin de valider son fonctionnement avant de l'intégrer dans le flow de conception ASIC. Pour l'implémentation sur FPGA nous avons utilisé une carte Artix 7, fournit par le magasin. 


---

### Yosys

Nous avons utilisé Yosys pour affiner le code Verilog après notre transcription manuelle depuis le VHDL, puis pour synthétiser ce dernier en vue de générer la netlist nécessaire à la fabrication de l'ASIC avec TinyTapeout.



---

### Github

Nous avons utilisé GitHub pour héberger et partager le projet TinyTapeout, en facilitant le suivi des versions et la collaboration sur le code source.

---

### TinyTapeout

Nous avons utilisé TinyTapeout pour intégrer notre design dans le flow de fabrication ASIC, en suivant un processus simplifié et accessible pour la réalisation du circuit.

