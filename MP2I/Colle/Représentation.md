## Représentation gauche
> *INFO-1 MINES MPI 2023*

## Entiers non bornée
On ce donne les types suivants :
```ocaml
type binaire = Zero | One;;
type mot = binaire list;;
```
On note $L$ l'ensemble des mots.

1. Rappelez l'encodage de nombre signé. Quelle est la page des nombre signé représentable avec $n$ bits ?
2. Donnez en C `void affiche_binaire(int n)` qui pour une entré $n$, affiche (`print)` 
3. 
4. Donnez une injection de $\N$ dans $L$
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
eyJoaXN0b3J5IjpbMTE1OTcyMzM4MywxNzM0NTExMzgyXX0=
-->