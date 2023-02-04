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

Créez une liste cyclique. Une liste acyclique.

Donnez le code de la fonction suivante qui détecte si un cycle est présent ou non dans la liste, en O(N) avec N la taille de la liste
```c
bool is_cyclique(liste* tete)
```
**DIFFICILE** : Transformer la fonction pour quelle rende la liste acyclique sans perdre aucun maillon. On veillera à toujours le faire en O(N) en complexité temporelle et O(1) en complexité spatial. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg0ODA4NDA5XX0=
-->