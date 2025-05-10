##  1.3 – Outils et Environnement

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
-  Machines d'états sans `localparam` → les états doivent être **clairement définis** avec `localparam` pour être synthétisables proprement dans OpenLane par exemple :
 ```bash
  // State encoding
    localparam [3:0] 
        INIT = 4'd0,
        FETCH_INS = 4'd1,
        FETCH_INS_DLY = 4'd2,
        DECODE = 4'd3,
        FETCH_OP = 4'd4,
        FETCH_OP_DLY = 4'd5,
        EXE_NOR_ADD = 4'd6,
        EXE_JCC = 4'd7,
        STORE = 4'd8,
        STORE_DLY = 4'd9; 
---

### Débogage par test croisé VHDL ↔ Verilog
