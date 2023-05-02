
## Détection de liste cyclique
On ce donne le type suivant en C:
```c
struct liste {
	liste* next;
	int value;
};
typedef struct liste liste;
```

1. Créez une liste cyclique. Une liste acyclique.

2. Donnez le code de la fonction suivante qui détecte si un cycle est présent ou non dans la liste, en $O(n)$ avec $n$ la taille de la liste
```c
bool is_cyclique(liste* tete)
```
3. **DIFFICILE** : Transformer la fonction pour quelle rende la liste acyclique sans perdre aucun maillon. On veillera à toujours le faire en O(N) en complexité temporelle et O(1) en complexité spatial. 


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
3. Programmez `bool est_vide()` renvoyant `true` is `lg` est vide et `false` sinon.
4. Programmez `void push(int v)` ajoutant `v` au début (à gauche) de la liste `lg`. On utilisera une assertion pour vérifier que l'allocation dynamique de mémoire est bien réalisée.
5. Programmez `int pop()` retirant de la liste `lg` son dernier élément, et le retournant. On utilisera une assertion pour s'assurer que la liste n'est pas vide.
6. Quelle structure de donnée avons-nous implémenté ?
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NTQ5MzIyNTNdfQ==
-->