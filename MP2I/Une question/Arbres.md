
## Arbre alphabétique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si un sommet A est plus proche de la racine qu'un sommet B, alors A sera plus à gauche que B.

Un arbre canonique peut-etre uniquement dénoté par deux tableaux :
 - Le premier associé à la hauteur sont nombre de sommets
 - Le second associe

Exemple :
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTI0MDg4NTVdfQ==
-->