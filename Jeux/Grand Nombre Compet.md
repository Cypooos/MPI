## La compétition du plus grand nombre

Le but de cette compétition est de créer un programme C de moins de 500 caractères renvoyant le plus grand entier possible en valeur absolue. On suppose que l'on dispose d'une mémoire infinie, et que les entiers ne soient pas bornée.

Exemple de programme de 151caractères :
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
 - la création de structure, les opérations `free` `malloc` `calloc` `sizeof` `typedef`
 - La gestion de pointeur, opérations `*` `&` (attention à rester dans un cadre déterministe), la constante `NULL`
 
Seuls les types `char` et `int` sont utilisable.
Aucune bibliothèque sera importé, on n'utilisera pas la librairie standard sauf pour les opérations déjà indiquée.

On suppose que le programme tourne sur un ordinateur ayant une mémoire infinie, et ayant des entiers non bornée. Plus concrètement, même si `sizeof(int)` renverra la même chose que dans le cas d'une exécution de C classique, il n'y a pas de Stack Overflow possible ou de dépassement d'entiers. Une allocation est toujours possible et ne causera jamais d'erreur.

Seul les entiers ne sont pas bornée, le type `char` fonctionne comme habituellement (bornée par $255$ dans le cas non signé et allant de $-128$ à $127$ dans le cas signé).

Un programme doit faire moins de 500 charactères, sans compter les espaces, les tabulations, les commentaires, les retours à la ligne et les retours chariots (sauf s'ils sont dans un string)

N'hésitez pas à donner avec votre programme une courte description de ses effets / de pourquoi il retourne / et approximation de la taille de son entrée.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzg2MDI2ODQ3LC01OTA3MzU3NDMsMTU4MT
EwNzIyN119
-->