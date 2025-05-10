## 1.5. Comparaison VHDL vs Verilog

### Retour d’expérience sur les deux langages

En tant qu’étudiants en électronique, nous avons utilisé à la fois **VHDL** et **Verilog** tout au long du projet. Voici nos observations :

| Aspect                          | VHDL                                                 | Verilog                                              |
|----------------------------------|-------------------------------------------------------|-------------------------------------------------------|
| Lisibilité                      | Plus verbeux, mais plus structuré                     | Plus concis, syntaxe plus proche du C                |
| Portabilité FPGA ↔ ASIC         | Bon pour FPGA, mais plus difficile à synthétiser ASIC| Plus adapté à la synthèse ASIC (TinyTapeout)        |
| Types de données                | Très typé, rigide (ex : `std_logic_vector`)          | Plus souple, mais moins strict                       |
| Simulations (Vivado)           | Très stable                                           | Stable également                                     |


### Problèmes rencontrés et solutions adoptées

- Le design **VHDL du CPU** fonctionnait parfaitement en simulation et sur FPGA, mais a échoué lors de la **traduction automatique vers Verilog via Yosys** (code non synthétisable).
- L’outil Yosys ne gère pas toujours correctement certains aspects spécifiques au VHDL : **types complexes, concaténations implicites, structures internes imbriquées**.
- Pour répondre aux contraintes de **synthèse stricte imposées par TinyTapeout**, nous avons finalement opté pour une **réécriture manuelle bloc par bloc** du design en **Verilog synthétisable**.

Pour mieux comprendre les erreurs et avertissements générés, nous nous sommes appuyés sur la documentation officielle de Verilator :  
🔗 [documentation officielle des warnings Verilator](https://verilator.org/guide/latest/warnings.html#)


💡 *Conclusion : même si VHDL est robuste pour les projets FPGA académiques, Verilog s’est imposé comme la meilleure option pour l’intégration dans un flot ASIC open source tel que TinyTapeout.*

