Cet exercice simple est souvent utillisé

## Détection de liste cyclique
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
**DIFFICILE** : transformer la fonction pour quelle rende la liste acyclique sans perdre aucun maillon. On veillera à toujours le faire en O(N) en et O(1)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2NjA5MDcyM119
-->