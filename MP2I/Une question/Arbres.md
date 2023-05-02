
## Arbre canonique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si pour toute feuille A plus proche de la racine qu'une feuille B, alors A sera plus à gauche que B.

Un arbre canonique peut-être uniquement représenté par un tableau qui à chaque hauteur associe son nombre de sommets.

1. Donnez les arbres canonique des tableaux $[\![0;2]\!]$, $[\![0;0;3;2]\!]$, $[\![0;1;1;1;1;2]\!]$
2. Donnez une fonction `val canonical : int array -> tree` qui à un tableau associe son arbre canonique
3. Démontrez que le tableau d'un arbre canonique non trivial doit se terminer avec un 2

## Arbre canonique, suite
On souhaite rajouter sur chaque sommet un entier positifs.

3. Modifier la définition de `tree` pour effectuer ce changement.

Si deux sommets `F(x)` et `F(y)` ont la même hauteur, alors `F(x)` est à gauche de `F(y)` si et seulement si x<y.
On rajoute donc au tableau représentant l'arbre canonique le tableau $[\![x_1,\_,x_n]\!]$ obtenue par parcours gauche-droite de l'arbre.

5.  Proposez un TODO


## Arbre binaire parfaits
> *INFO 1 2023 MINES MPI*

On ce donne le type d'arbre suivant :
```c
typedef strcut Noeud *arb;
struct Noeud {
  int valeur;
  arb fils_g;
  arb fils_d;
};
```

On dit que la hauteur de l'arbre nul (sans nœud) est -1.
1. Rappelez la définition d'un arbre binaire parfait. Donnez en un type en Ocaml.
2. Démontrez que tout arbre parfait de hauteur $n$ possède $2^{n+1}-1$ nœuds.
3. Donnez `int hauteur(arb a)` renvoyant la hauteur de l'arbre `a`
4. Donnez `arb arb_trouve(arb a, int n, int k)`
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAzMjA2MTM2NywtMTAwNzQ4ODA5MSwxOT
cwODYzMzc1XX0=
-->