## Méthodes de programmations
1.  Qu'est-ce qu'un paradigme ? Expliquez les paradigmes suivant : paradigme logique, paradigme impératif structuré, paradigme fonctionnel, **paradigme orienté objet ?**
2. Qu'est ce-qu'un langage de programmation compilé ? Interprété ? **Compilé à la volé ?**
3. Quelle est la différence entre un `signed` et un `unsigned` ? Comment sont encodé les nombre négatifs ?
4. Comment sont encodé les flottants ? En sachant que un `int` (sur 2bits à 8 bits d'exposants, Combien de chiffre significatifs en base 10 peuvent t-il stoqués ? 
5. Déterminez que la fonction `getter` suivante termine :
```ocaml
let rec get m l = match l with
 | [] -> m
 | e::q with e>=m -> get e l
 | e::q -> get m l;;
let getter = get min_int;;
```
Que fait-il ? Démontrer sa correction.

6. Qu'est-ce que une correction partielle ? Parallèles avec problème décidable et semi-décidable ?
7. Définition de la complexité ?
8. Quel est le type de la fonction suivante :
```ocaml
let a b c d = match b c [||] with
 | e with !e = d -> c+.1
 | _ -> d
```
9. Qu'est ce ce que la programmation défensive ? Pourquoi est-elle plus simple en ocaml que en python ?
10. Faite de graphe de flot de contrôle du code de la fonction `getter` si dessus.
11. Faite le graphe de flot de contrôle de la fonction suivante. Donnez un jeu de test couvrant les sommets. Donnez un autre jeu de test couvrant les arêtes. Donnez un dernier jeu de test donnant des test exhaustif des conditions.
```c
int q11(int* liste,int n,int k) {
	if (liste==NULL){return 0;}
	printf("Starting...\n");
	for (int i=0;i<n;i++) {
		printf("Doing i=%d\n",i);
		if (liste[i] >= k && i-k>0) {return i;}
	}
	return n;
}
```
12. **Qu'est-ce que l'assembleur ?**

## Récursivité et induction

## Structures de données
13. Qu’est ce que l'allocation ? Citez les 3 lieux ou la mémoire peut être stoqué dans un programme. Où sont stoqué `30`, `40` et `50` dans la mémoire au moment de l'appel à `fct` dans le programme suivant ? Ou est stoqué la *variable* `table` ? et son contenu ?
```c
int fct(int a){return a*a;};
const int set = 30;
int main() {
	int* table = (int*)malloc(sizeof(int)*4);
	for (int i=0;i<4;i++){
		table[i] = 40;
	}
	b[2] = fct(50);
}
```
14. **Comment sont implémenté `true` et `false` en C ?**
15. Distinction entre structure de données mutable et immuable.
16. Qu'est ce qu'un Constructeur ? Accesseur ? Transformateur ? **Destructeur ?**
17. Qu'est-ce qu'une structure de donnée abstraite ? Donnez une structure de donnée abstraite représentant une hashmap (un dictionnaire).
18. Qu'est-ce qu'une liste ? Une liste doublement chainé ? Donner une implémentation d'une liste doublement chainé en C stoquants des `int`. 
19. Donnez une implémentation possible des listes à l'aide de tableau grandissants.
20. Qu'est-ce qu'une file ? Une pile ? Implémentez une file en ocaml à l'aide de deux listes. Quelle est le cout amorti de `ajouter` et de `retirer` ?
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA2ODc3ODcxLC0yMzQzMDM3OTYsNjY4OD
cwNjUsMjAxMjI3NTg2MCwtODgwMzE0Nzk4LDgwNTE0ODY4NSwt
MTg3NzEyMDEyOF19
-->