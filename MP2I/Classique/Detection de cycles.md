
## Detection de liste cyclique
On ce donne le type suivant en C:
```c
struct liste {
	liste* next;
	int value;
};
typedef struct liste liste;
```
Donnez le code de la fonction suivante qui détecte si un cycle 
```c
bool is_cyclique(liste* tete)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjEwNzA5NTQxXX0=
-->