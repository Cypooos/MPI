
## Arbre alphabétique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si pour toute feuille A plus proche de la racine qu'une feuille B, alors A sera plus à gauche que B.

Un arbre canonique peut-être uniquement dénoté par un tableau qui à chaque hauteur associe son nombre de sommets.

1. Donnez les arbres canonique des tableaux $[\![0;0;3;2]\!]$, $[\![0;1;1;1;1;2]\!]$, $[\![]\!]$, 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1MTcxNzYyNl19
-->