
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
5. Transformer la fonction pour qu'elle transforme la liste en une liste acyclique sans perdre aucun maillon. On veillera à toujours le faire en $O(n)$ en complexité temporelle et $O(1)$ en complexité spatiale. 

## Liste générée

On ce donne le type suivant en OCaml :
```ocaml
```

1. Rapellez 
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzUwOTY5Njk5LC0xODU0OTMyMjUzXX0=
-->