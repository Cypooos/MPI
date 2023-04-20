
## Listes
1. Définissez en C et Ocaml un type correspondant à une liste simple
2. Donnez une fonction calculant la liste inversé en $O(n)$ en Ocaml
3. Donnez une fonction donnant la longueur de la liste en C
## Liste doublement chainée
> Tiré de X-ENS INFO C 2023

On ce donne le type d'une liste doublement chainée suivant :
```c
typedef struct chainon_s chainon;
struct chainon_s
{
	int val;
	chainon *prec;
	chainon *suiv;
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NzQ2MzQ3ODldfQ==
-->