## Représentation gauche
> *INFO-1 MINES MPI 2023*


On appelle *représentation binaire gauche* de $n$ sur $N$ chiffres une suite finie $g= (g_n)_{0\le n<N}$ tel que :
 - Chaque $g_i\in\{0,1,2\}$
 - $n=\sum_{k=0}^{N-1} g_k(2^{k+1}-1)$
 - Si $g = g_0,g_1,...,2,g_i,..,g_{N-1}$ alors $(g_i,...,g_{N-1}) = (0, ..., 0)$

1. Donnez la représentation binaire et binaire gauche des nombres de $0$ à $7$.
2. Donnez le plus grand $M_N$ qui admet une représentation binaire gauche sur $N$ chiffres.

On définie la structure 
```c
const int N = 8;
struct RepGauche {
	int position;
	bool chiffres[N];
};
typedef struct RepGauche rg;
```

## Représentation des entiers négatifs


## Bijection de $\N$ aux mots binaire
> Inspiré d'une erreur dans le sujet *INFO-2 MINES MPI 2023*

On ce donne les types suivants :
```ocaml
type binaire = Zero | One;;
type mot = binaire list;;
```
On note $L$ l'ensemble des objets de type `mot`.

1. Rappelez l'encodage de nombre signé. Quelle est la plage (l'intervalle) des nombres signé représentable avec $n$ bits ?
2. Donnez en C `void affiche_binaire(int n)` qui pour une entré $n$ non signé, affiche (`print`) sa représentation binaire. On n'utilisera que `%d`.
3. Donnez en OCaml la fonction `val to_bit : int -> binaire list` qui à $n$ associe sa représentation binaire. Est-elle bijective de $\N$ à $L$ ?
4. Montrez que $\psi : n,m\mapsto 2^n(2m+1)$ est bijectif de $(\N^*)^2\to\N^*$.
6. Donnez en OCaml `val psi : int -> int*int` qui à $n$ associe $\psi^{-1}(n)$.
7. Donnez `val phi : int -> binaire liste` bijective de $\N\to L$.
## Représentation d'ensembles
> *A3 (Q5) Oral Ulm 2021*, *J3 (Q2) Oral Ulm 2019*

On s'intéresse ici à implémenté une structure représentant des ensembles, et différentes opérations dessus.

1. Donnez 
1. Proposer une structure de données pour stocker des sous-ensembles d’entiers $S$ compris entre $0$ et $M$ qui supporte les opérations suivantes :
  — Créer cette structure (prend $M$ en argument) en $O(M)$
  — Ajouter un entier dans $S$, en $O(1)$;
  — Retirer un entier de $S$, en $O(1)$;
  — Parcourir les entiers actuellement stockés dans $S$, en $O(M)$.

La complexité en espace sera de $O(M)$
Écrire le code  pour ces opérations.
<!--stackedit_data:
eyJoaXN0b3J5IjpbODYwNzEzMTEwLC05MzIyNzM0MTQsLTE3ND
k1ODExNiwtMTk1MjQxODcxNiwxNzM0NTExMzgyXX0=
-->