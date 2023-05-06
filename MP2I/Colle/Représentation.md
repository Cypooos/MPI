## Représentation gauche
> *INFO-1 MINES MPI 2023*

## Représentation des entiers négatifs

## Entiers non bornée
> Inspiré d'une erreur dans le sujet *INFO-2 MINES MPI 2023*

On ce donne les types suivants :
```ocaml
type binaire = Zero | One;;
type mot = binaire list;;
```
On note $L$ l'ensemble des objets de type `mot`.

1. Rappelez l'encodage de nombre signé. Quelle est la plage (l'intervalle) des nombres signé représentable avec $n$ bits ?
2. Donnez en C `void affiche_binaire(int n)` qui pour une entré $n$ non signé, affiche (`print`) sa représentation binaire. On n'utilisera que `%d`.
3. Donnez en OCaml la fonction `val to_bit : int -> binaire list` qui à $n$ associe sa représentation binaire. Est-elle bijective ?
4. Montrez que $\phi : n,m\mapsto 2^n()$ Donnez en OCaml `val get_couple : int -> int*int`
5. Donnez `val phi : int -> binaire liste` bijective.
## Ensemble d'entiers
> *A3 (Q5) Oral Ulm 2021*, *J3 (Q2) Oral Ulm 2019*

Proposer une structure de données pour stocker des sous-ensembles d’entiers $S$ compris entre $0$ et $M$ qui supporte les opérations suivantes :
  — Créer cette structure (prend $M$ en argument) en $O(M)$
  — Ajouter un entier dans $S$, en $O(1)$;
  — Retirer un entier de $S$, en $O(1)$;
  — Parcourir les entiers actuellement stockés dans $S$, en $O(M)$.

La complexité en espace sera de $O(M)$
Écrire le pseudocode pour ces opérations.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU3NDI2MzM4OSwtMTc0OTU4MTE2LC0xOT
UyNDE4NzE2LDE3MzQ1MTEzODJdfQ==
-->