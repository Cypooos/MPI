## La compétition du plus grand nombre

Le but de cette compétition est de créer un programme C de moins de 500 caractères renvoyant le plus grand entier possible. On suppose que l'on dispose d'une mémoire infinie, et que les entiers soient bornée.

Exemple de programme :
```c
int pow(int a, int b) {
	return b ? a*ipow(a,b-1) : 1;
}
int power_stack(int a, int b) {
	return b ? pow(a,power_stack(a,b-1)) : 1;
}
int main(void) {
	return ipowstack(999,999);
}
```
Ceci 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU4MTEwNzIyN119
-->