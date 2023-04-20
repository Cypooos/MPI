
## Arbre alphabétique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F of int | N of tree * tree;;
``` 
On définie la relation $\prec_t$ par, soit $a,b\in \mathcu{S}$
Un arbre _t_ est dit *canonique* si pour toute feuille 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExNjgwMzg1N119
-->