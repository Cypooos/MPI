## La compétition du plus grand nombre

Le but de cette compétition est de créer un programme C de moins de 500 caractères renvoyant le plus grand entier possible en valeur absolue. On suppose que l'on dispose d'une mémoire infinie, et que les entiers ne soient pas bornée.

Exemple de programme de 174 caractères :
```c
int pow(int a, int b) {
	return b ? a*ipow(a,b-1) : 1;
}
int power_stack(int a, int b) {
	return b ? pow(a,power_stack(a,b-1)) : 1;
}
int main(void) {
	return power_stack(999,999);
}
```
Ceci calcule $999^{999^{999^{...}}}$ une tour 999 de haut d'exponentiels imbriqué de $999$.

## Règles 
Le programme DOIT retourner à la fin l’entier (et donc finir son exécution en un temps fini).

L'algorithme doit être déterministe; tout comportement indéterminé ( comme les valeurs pointé après un `malloc` ) doit être déterminité ( initialisation d'une structure )

Liste d’opérations utilisable : 
 - `+` `*` `/` `%` `||` `&&` `!` `==` `!=` `<` `>` `<=` `>=` **seulement sur les entiers**
 - L'opérateur ternaire `a ? b : c`
 - Les `#define`
 - la création de structure, les opérations `free` `malloc` `calloc` `sizeof`
 - La gestion de pointeur, opérations `*` `&`,  (attention à rester dans un cadre déterministe)
 
Liste 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEwODUzOTMwNiwtNTkwNzM1NzQzLDE1OD
ExMDcyMjddfQ==
-->