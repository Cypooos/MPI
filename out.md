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
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjUxNzk3NTgyXX0=
-->