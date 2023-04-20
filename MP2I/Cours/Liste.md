
## Listes
1. Définissez en C et Ocaml un type correspondant à une liste simple
2. Donnez une fonction calculant la liste inversé en $O(n)$ en Ocaml
3. Donnez une fonction donnant la longueur de la liste en C
## Liste doublement chainée
> Tiré de X-ENS INFO C 2023

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
3. Programmez `bool est_vide()` renvoyant `true` is `lg` est vide et `false` sinon.
4. Programmez `void push(int v)` ajoutant `v` au début (à gauche) de la liste `lg`. On utilisera une assertion pour vérifier que l'allocation dynamique de mémoire est bien réalisée.
5. Programmez `int pop()` retirant de la liste `lg` son premier élément, et le retournant. On utilisera une assertion pour s'assurer que la liste n'est pas vide.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNzMxNDc1NjhdfQ==
-->