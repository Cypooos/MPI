
## Algorithme de Stressen

On cherche dans ce sujet à calculer un produit de matrices de manière efficace.
1. Donnez en C le code de `int** (int** mat1, int** mat2, int n)` qui calcule le produit de deux matrices de $\mathcal{M}_n(\R)$. Quelle est sa complexité ?

Soit $\Gamma,\Delta \in \mathcal{M}_n$ des matrices, on effectue la décomposition par bloc :
$$
\Gamma = \begin{pmatrix}
A & B \\
C & D 
\end{pmatrix},\ \Delta = \begin{pmatrix}
W & X  \\
Y & Z
\end{pmatrix}
$$
On défini le type en OCaml :
```ocaml
type mat = int array array;;
```
3. Donnez en OCaml `val mul: mat -> mat -> mat`  une fonction en $O(n^3)$ qui calcule récursivement $\Gamma\times \Delta$ quand c'est possible, et qui `failwith` sinon.
4. Quels sont les 8 sous-produits que l'on a effectué ?

On pose les produits suivant :
$$
\begin{align*}
&M_1 = (A+D)(W+Z) \\
&M_2 = (C+D)W \\
&M_3 = A(X-Z) \\
&M_4 = D(Y-W)\\
&M_5 = (A+B)Z \\
&M_6 = (C-A)(W+X) \\
&M_7 = (B-D)(Y+Z) \\
\end{align*}
$$

4. Donnez $\Gamma \times \Delta$ en fonction des $(M_i)_i$
5. Modifier l'algorithme pour qu'il n'effectue que 7 sous-produits. Quelle est la nouvelle complexité ?

## Liste doublement chainée
>  *INFO-C 2023 X-ENS MPI*

On ce donne le type d'une liste doublement chainée suivant :
```c
typedef struct chainon_s chainon;
struct chainon_s
{
	int val;
	chainon *prec;
	chainon *suiv;
};

struct liste_s
{
	chainon *premier;
	chainon *dernier;
};
typedef struct liste_s liste;
```
1. A quoi servent les `typedef` ?
2. Définir et initialiser une variable globale `lg` représentant une liste chainé initialement vide.
3. Programmez `bool est_vide()` renvoyant `true` si `lg` est vide et `false` sinon.
4. Programmez `void push(int v)` ajoutant `v` au début de la liste `lg`. On utilisera une assertion pour vérifier que l'allocation dynamique de mémoire est bien réalisée.
5. Programmez `int pop()` retirant de la liste `lg` son dernier élément, et le retournant. On utilisera une assertion pour s'assurer que la liste n'est pas vide.
6. Quelle structure de donnée avons-nous implémentée ?

## Détection de liste cyclique
On ce donne le type suivant en C:
```c
struct liste {
	liste* next;
	int value;
};
typedef struct liste liste;
```

1. Définissez deux variables représentant une liste cyclique et une liste acyclique.
2. Donnez `void add(liste* li, int v)` qui à une liste `li` ajoute en tête le chainon contenant la valeur `v`. On utilisera une assertion pour vérifier que l’allocation dynamique de mémoire est bien réalisée.
3. Donnez `void remove(liste* li, int v)` qui retire tous les maillons ayant `v` comme valeur à `li`.
4. Donnez `bool is_cyclique(liste* li)` qui détecte si un cycle est présent ou non dans la liste, en $O(n)$ avec $n$ la longueur de la liste.
5. Transformer la fonction pour qu'elle transforme la liste en une liste acyclique sans perdre aucun maillon. On cherchera la meilleur complexité.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4NDk5NzI3NCwxMDE0OTM0MDY2XX0=
-->