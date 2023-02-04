
## Detection de liste cyclique
On ce donne le type suivant en C:
```c
struct liste {
	liste* next;
	int value;
};
typedef struct liste liste;
```

Créé une liste cyclique. Une liste acyclique.

Donnez le code de la fonction suivante qui détecte si un cycle est présent ou non dans la liste, en O(N) avec N la taille de la liste
```c
bool is_cyclique(liste* tete)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjYzNDE0MDcwXX0=
-->