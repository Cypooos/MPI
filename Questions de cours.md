Par Cyprien (@Cypooos) en MPI* à Fénelon Sainte Marie. Droit à toute sorte de publication et modification, mais gardez les crédits !
En gras sont les questions non officiellement au programme (parfois explicitement hors programme), mais qu'il est bon de connaitre.
## Machines et implémentation
1.  Qu'est-ce qu'un paradigme ? Expliquez les paradigmes suivant : paradigme logique, paradigme impératif structuré, paradigme fonctionnel, **paradigme orienté objet ?**
2. Qu'est ce-qu'un langage de programmation compilé ? Interprété ? **Compilé à la volé ?**
3. Quelle est la différence entre un `signed` et un `unsigned` ? Comment sont encodé les nombre négatifs ?
4. Comment sont encodé les flottants ? En sachant que un `float` a 8 bits d'exposants, combien de chiffre significatifs en base 10 peuvent-ils stoker ? 
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
9. Qu'est ce ce que la programmation défensive ? Pourquoi est-elle plus simple en Ocaml que en python ?
10. Faites le graphe de flot de contrôle du code de la fonction `getter` si dessus.
11. Faites le graphe de flot de contrôle de la fonction suivante. Donnez un jeu de test couvrant les sommets. Donnez un autre jeu de test couvrant les arêtes. Donnez un dernier jeu de test donnant des tests exhaustif des conditions.
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
13. Quels sont les différents droits modifiables sur un fichier / dossier ? (*`chmod`*)
14. Qu'est-ce qu'un pipe ?
15. A quoi correspondent les flux standard *stdin*, *stdout* et *sterr* ?
16. Qu'est-ce qu'un *inode* (nœuds d’index) dans un système de fichier ?
17. Différence entre un lien symbolique et physique ?
18. Qu'est-ce qu'une instruction atomique ?
19. Différence entre mutex et sémaphore. Notion de section critique.
20. Donnez un exemple d'algorithme qui donnera une situation d'interblocage possiblement avec 2 thread.
21. Quel est le problème du diner des philosophe ?
22. Algorithme de Peterson pour une implémentation des mutex avec 2 threads.
23. Algorithme de la Boulangerie de Lamport pour implémentation des mutex avec k threads.


## Structures de données
24. Qu’est ce que l'allocation ? Citez les 3 lieux ou la mémoire peut être stocké dans un programme. Où sont stocké `30`, `40` et `50` dans la mémoire au moment de l'appel à `fct` dans le programme suivant ? Ou est stocké la *variable* `table` ? et son contenu ?
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
25. **Comment sont implémenté `true` et `false` en C ? Que fais `if (n)` avec `n` un nombre ?** 
26. Distinction entre structure de données mutable et immuable.
27. Qu'est ce qu'un Constructeur ? Accesseur ? Transformateur ? **Destructeur ?**
28. Qu'est-ce qu'une structure de donnée abstraite ? Donnez une structure de donnée abstraite représentant une hashmap (un dictionnaire).
29. Qu'est-ce qu'une liste ? Une liste doublement chainé ? Donner une implémentation d'une liste doublement chainé en C stoquants des `int`. 
30. Qu'est-ce qu'une liste cyclique ? Algorithme du lièvre et de la tortue pour savoir si une liste est cyclique.
31. Donnez une implémentation possible de liste à l'aide de tableau grandissants en Ocaml.
32. Qu'est-ce qu'une file ? Une pile ? Implémentez une file en ocaml à l'aide de deux listes. Quelle est le cout amorti de `ajouter` et de `retirer` ?
33. **Donnez une structure de donnée permettant de stoquer des sous-ensembles de $[\![0;n]\!]$. Les opérations d'ajout et de retrait d'élément se feront en $O(1)$, l’initialisation en $O(n)$**
34. Définir un arbre. Un arbre binaire. Sa hauteur et sa largeur. La hauteur d'un nœud. Une foret. Donnez un type en C et en Ocaml. 
35. Nombre d'arbre possible avec $n$ sommets ?
36. Définir un arbre binaire de recherche. Donnez une implémentation en C et en Ocaml. Complexité de la recherche d'élément ? Complexité de l'ajout d'un élément ? 
37. Opération de rotation gauche et rotation droite. A quoi servent-elles ?
38. Donnez une fonction de sérialisation pour un arbre binaire de recherche.
> *La sérialisation est au programme. Il s'agit de transformer une structure de donné hiérarchique en une structure de donné séquentielle pour après, par exemple, la sauvegarder dans un fichier texte. On pourra considérer des tableaux comme structure de donné séquentielle. La fonction doit être bijective.*
39. Donnez une fonction de sérialisation pour un graphe non orienté.
40. "Arbre bicolore" lol
41. Définir un graphe. Un graphe orienté. Un graphe pondéré. Un graphe complet.
42. Qu'est-ce qu'une matrice d’adjacence ?
43. Qu'est-ce qu'une composante fortement connexe ? Faiblement connexe ?
44. Soit $R$ une relation et $G=(S,A)$ le graphe associé. Traduire le fait que $R$ soit réflexive. Transitive. Totale. Une relation d'ordre. Que représente une composante fortement connexe dans G ?
45. Qu'est-ce qu'un graphe planaire ? **Démontrez la propriété d'Euler**
46. On note $\sim$ la relation d'existance d'un chemin entre deux sommets. Montrez que cela définie bien une relation d'équivalence. Que représente les classes d'équivalence ?
47. Montrez que $G=(S,A)$ est un arbre, ssi pour tout paires $a,b\in S$ il existe un unique chemin de $a$ à $b$ sans cycle
48. Quelle est la structure unir et retrouver ? Donnez le pseudo-code avec des forets.

## Logique
1. Pour chaque opérateur $\lnot, \land, \lor, \rarr, \lrarr$, donner sa table de vérité et son arité.
2. Loi de morgans.
3. Ecrire sous la forme d'arbre les formules logique $A \land (B\lor \lnot C)$

## Algorithmique
1. Qu'est-ce qu'un algorithme déterministe ? Un algorithme probabiliste ?
2. Différence entre un algorithme de Las Vegas et de Monte Carlos ?
3. Qu'est-ce qu'un algorithme glouton ?
4. Qu'est-ce que la mémoïsation ? Donnez une implémentation de la suite de Fibonacci mémoïsé. Quelle est la nouvelle complexité ?
5. Algorithme de Boyer-Moore
6. Algorithme de Rabin-Karp
7. Algorithme de Huffman
8. Algorithme Lempel-Ziv-Welch
9. Algorithme de Kosaraju de recherche de composante fortement connexe à l'aide de parcours du graphe.
10. Algorithme de Dijkstra avec une file de priorité. Prononciation du nom.
11. Algorithme de Floyd-Warshall.
12. Recherche d’un arbre couvrant de poids minimum par l’algorithme de Kruskal.


## Classe de complexité
1. Qu'est-ce qu'un problème de décision ? 
2. Prouvez la non décidabilité du problème de l’arrêt.
3. Donnez l'énoncé des problèmes suivants : **SAT**, **3-SAT**, **2-SAT**, **MAX2SAT**, **k-COLOR**
4. Classe P, Classe NP, **Classe EXPTIME**, **Classe EXPSPACE**
5. Réduction de problèmes en temps polynomial. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MzAzMzY4NjQsLTM1NDI2MDAxNSwtMj
M0MzAzNzk2LDY2ODg3MDY1LDIwMTIyNzU4NjAsLTg4MDMxNDc5
OCw4MDUxNDg2ODUsLTE4NzcxMjAxMjhdfQ==
-->