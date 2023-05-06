## Représentation gauche
> *INFO-1 MINES MPI 2023*

## Représentation des entiers négatifs

## Bijection de $\N$ à $L$
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
4. Montrez que $\psi : n,m\mapsto 2^n(2m+1)$ est bijectif de $\N^2\to\N$.
5. Donnez en OCaml `val psi : int -> int*int` qui à $n$ associe $\psi^{-1}(n)$
6. Donnez `val phi : int -> binaire liste` bijective de $\N\to L$.
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
eyJoaXN0b3J5IjpbMTM0NDY0NjU5LC0xNzQ5NTgxMTYsLTE5NT
I0MTg3MTYsMTczNDUxMTM4Ml19
-->