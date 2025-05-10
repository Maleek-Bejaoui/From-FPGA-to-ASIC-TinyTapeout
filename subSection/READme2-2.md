## 2.2.  Résultats du CPU

### Obtention des résultats

De la même manière que pour le compteur 8 bits précédemment détaillé, nous avons pu observer les résultats dans la partie GDS de "Actions" sur Github.

### Résultats obtenus

GitHub nous fournit des informations essentielles pour la réalisation d'un ASIC, telles que les cellules utilisées, la taille de notre projet sur l'ASIC choisi, ainsi que des vues en 2D et 3D de notre projet sur la puce.

Nous avons fait varier la taille de la RAM ainsi que celle de la puce. Nous sommes parti d'une puce de taille maximale: 8*2 ce qui vaut 1336*216 µm(taille modifiable dans info.yaml).
Ainsi on a obtenu les résultats suivants pour 
  
  
  - En ce qui concerne l'occupation de notre compteur sur la carte, elle est de 2.633 %. On voit bien que le compteur était un projet simple pour concevoir notre premier ASIC et "se faire la main" sur le sujet.
  - Les cellules utilisées sont :
      - Cellules logiques (NAND, OR, AND...) : 23
      - Cellules combinatoires (flip-flops) : 8
      - Buffers : 5
      - Cellules diverses (constantes, delays) : 18
      - Cellules de remplissage (fill cells) et cellules de connexion (tap cells)
  - La vue 2D du compteur sur la carte est affichée ci-dessous : 
![Compteur8bits](../images/Compteur8bits2D.png)
