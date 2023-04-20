
## Arbre alphabétique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F of int | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si :
 - Tout les sommets à la même hauteur sont trié de gauche à droite dans l'ordre croissant 
 - Si un sommet 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk2MzQxNTkyNl19
-->