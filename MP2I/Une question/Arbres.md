
## Arbre alphabétique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si pour tout sommet A plus proche de la racine qu'un sommet B, alors A sera plus à gauche que B.

Un arbre canonique peut-être uniquement dénoté par un tableau qui à chaque hauteur associe son nombre de sommets.

1. Donnez les arbres canonique des tableaux $[\![0;0$
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NTA0NjkyMTldfQ==
-->