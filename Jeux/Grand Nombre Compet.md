# La compétition du plus grand nombre

Le but de cette compétition est de créer un programme C de moins de 500 caractères renvoyant le plus grand entier possible en valeur absolu. On suppose que l'on dispose d'une mémoire infinie, et que les entiers ne soient pas bornée.

Exemple de programme de 151 caractères :
```c
int pow(int a, int b) {
	return b ? a*pow(a,b-1) : 1;
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
Le programme DOIT retourner à la fin un entier (et donc finir son exécution en un temps fini).

L'algorithme doit être déterministe; tout comportement indéterministe ( comme les valeurs pointées après un `malloc` ) doit être déterminisé ( par l'initialisation de ces valeurs par exemple )

Liste d’opérations utilisable : 
 - `+` `*` `/` `%` `||` `&&` `!` `==` `!=` `<` `>` `<=` `>=` **seulement sur les entiers**
 - L'opérateur ternaire `a ? b : c`
 - Les `#define`
 - la création de structure, les opérations `free` `malloc` `calloc` `sizeof` `typedef`
 - La gestion de pointeur, opérations `*` `&` (attention à rester dans un cadre déterministe), la constante `NULL`
 - Toute les structures de contrôle usuelle : création de fonction, `while` `if` `else` et `for`
 
Seuls les types `char` et `int` sont utilisable.
Aucune bibliothèque sera importé, on n'utilisera pas la librairie standard sauf pour les opérations déjà indiquée.

On suppose que le programme tourne sur un ordinateur ayant une mémoire infinie, et ayant des entiers non bornée. Plus concrètement, même si `sizeof(int)` renverra la même chose que dans le cas d'une exécution de C classique, il n'y a pas de Stack Overflow possible ou de dépassement d'entiers. Une allocation est toujours possible et ne causera jamais d'erreur.

Seul les entiers ne sont pas borné, le type `char` fonctionne comme habituellement (borné par $255$ dans le cas non signé et allant de $-128$ à $127$ dans le cas signé).

Un programme doit faire moins de 500 charactères, sans compter les espaces, les tabulations, les commentaires, les retours à la ligne et les retours chariots (sauf s'ils sont dans un string)

N'hésitez pas à donner avec votre programme une courte description de ses effets / de pourquoi il retourne / et approximation de la taille de son entrée.

Le programme vainqueur sera le programme renvoyant le plus grand entier e. Vous pouvez proposer autant de programmes que vous voulez.

La date limite pour envoyer vos programmes par discord à @cypooos ou par mail à cyprien.bourotte@gmail.com ou par whatsapp est le lundi 14 août à 14h.
N'hésitez pas à m'envoyer des questions / demande de précisions concernant les règles si besoin ! 
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTk1OTc4OTYxLC01OTA3MzU3NDMsMTU4MT
EwNzIyN119
-->