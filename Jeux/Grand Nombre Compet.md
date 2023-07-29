## La compétition du plus grand nombre

Le but de cette compétition est de créer un programme C de moins de 500 caractères renvoyant le plus grand entier possible. On suppose que l'on dispose d'une mémoire infinie, et que les entiers soient bornée.

Exemple de programme :
```c
int ipow(int a, int b) {
	return b ? a*ipow(a,b-1) : 1;
}
int ipowstack(int a, int b) {
	if (b == 0) {
		return 1
	} else {
		return b ? ipow(a,ipowstack(a,b-1));
	} 
}
int main(void) {
	return ipowstack(999,999);
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ1NTIxMjkxNF19
-->