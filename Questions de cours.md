Par Cyprien (@Cypooos) en MPI* à Fénelon Sainte Marie. Droit à toute sorte de publication et modification, mais gardez les crédits !
En gras sont les questions non officiellement au programme (parfois explicitement hors programme), mais qu'il est bon de connaitre.

Il manque encore à ce document:
 - Bien refaire "base de donnée"
 - Extras plus théorique : Classes de fonctions, récursit

## Machines et implémentation
1.  Qu'est-ce qu'un paradigme ? Expliquez les paradigmes suivant : paradigme logique, paradigme impératif structuré, paradigme fonctionnel, **paradigme orienté objet ?**
2. Qu'est ce-qu'un langage de programmation compilé ? Interprété ? **Compilé à la volé ?**
3. Quelle est la différence entre un `signed` et un `unsigned` ? Comment sont encodé les nombre négatifs ?
4. Comment sont encodé les flottants ? En sachant que un `float` a 8 bits d'exposants, combien de chiffre significatifs en base 10 peuvent-ils stoker ? Qu'est-ce que la mantisse ?
5. Démontrez que la fonction `getter` suivante termine :
```ocaml
let rec get m l = match l with
 | [] -> m
 | e::q when e>=m -> get e q
 | e::q -> get m q;;
let getter = get min_int;;
```
Que fait-il ? Démontrer sa correction.

6. Qu'est-ce que une correction partielle ? Parallèles avec problème décidable et semi-décidable ?
7. Définition de la complexité ? Donnez l'équation de récurrence complexité sur la version naïve du calcul de Fibonacci et en déduire sa complexité.
8. Quel est le type de la fonction suivante :
```ocaml
let a b c d = match b c [||] with
 | e when !e = d -> c+.c
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
20. Donnez un exemple d'algorithme qui donnera une situation d'interblocage possiblement avec 2 threads.
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
35. **Nombre d'arbre possible avec $n$ sommets ?** 
36. **Nombre d'arbre binaire possible avec $n$ sommets ?** 
37. Définir un arbre binaire de recherche. Donnez une implémentation en C et en Ocaml. Complexité de la recherche d'élément ? Complexité de l'ajout d'un élément ? 
38. Opération de rotation gauche et rotation droite. A quoi servent-elles ?
39. Donnez une fonction de sérialisation pour un arbre binaire de recherche.
> *La sérialisation est au programme. Il s'agit de transformer une structure de données hiérarchique en une structure de données séquentielle pour après, par exemple, la sauvegarder dans un fichier texte. On pourra considérer des tableaux comme structure de données séquentielle. La fonction doit être bijective.*
40. Donnez une fonction de sérialisation pour un graphe non orienté.
41. "Arbre bicolore" lol
42. Définir un graphe. Un graphe orienté. Un graphe pondéré. Un graphe complet. Une clique. Un graphe biparti.
43. Qu'est-ce qu'une matrice d’adjacence ?
44. **Si $A$ est une matrice d'adjacence, que représente $(A^n)_{i j}$ ?**
45. Qu'est-ce qu'une composante fortement connexe ? Faiblement connexe ?
46. Soit $R$ une relation et $G=(S,A)$ le graphe associé. Traduire le fait que $R$ soit réflexive. Transitive. Totale. Une relation d'ordre. Que représente une composante fortement connexe dans G ?
47. Qu'est-ce qu'un graphe planaire ? **Démontrez la propriété d'Euler**
48. On note $\sim$ la relation d'existance d'un chemin entre deux sommets. Montrez que cela définie bien une relation d'équivalence. Que représente les classes d'équivalence ?
49. Montrez que $G=(S,A)$ est un arbre, ssi pour tout paires $a,b\in S$ il existe un unique chemin de $a$ à $b$ sans cycle
50. Montrez que $\sum_{s\in S} \deg (s) = |A|/2$
51. Quelle est la structure unir et retrouver ? Donnez les optimisations de compression de chemin et de réunir à la plus grande racine. **La complexité amortie est $O(\alpha(n))$ où $\alpha = \{x\mapsto A(x,x)\}^{-1}$ avec $A$ la fonction d'Ackermann**
52. Recherche d'un arbre couvrant de poids minimal (Algorithme de Kruskal). Preuve de sa correction et terminaison. **Complexité en $O(\log^*(n))$, en pratique O(1)**

## Langages formels
53. Définition d'un alphabet, mot, langage.
54. Définition de préfixe, suffixe, facteur. **Mot miroir.**
55. Opérations sur les langages. Concaténation, Union, étoile de Kleen.
56. Définition inductive d'un langage régulier.
57. Définition inductive d'une expression régulière.
58. Définition d'un automate déterministe. Automate émondé. État accessible et co-accessible. $L(A)$ le langage reconnu par l'automate.
59. Différences avec un automate non déterministe ? $\varepsilon$-transition et 
60. **Qu'est-ce qu'une fonction de transition généralisé ?**
61. Donnez des automates déterministes sur $\Sigma=\{a,b\}$ reconnaissant
$L_1 = \{a^{2n} \mid n\in\N\}$
$L_2 = \{\omega\in\Sigma^* : |\omega|_a \in2\N\ \land\ |\omega|_b \in 3\N \}$ où $|\omega|_a$ est le nombre de $a$ dans $\omega$
**DIFFICILE : $L_3$, les mots binaires qui sont des multiples de 3 écrit en base 2**
62. Notion de langage local, d'expression régulière linéaire.
63. Donnez la méthode de Glush-kov (ou algorithme de Berry-Sethi) pour obtenir l'automate reconnaissant le langage associé à un regexp.
64. Donnez l'automate de Glush-kov associé à $((a|b).(bb|ca))^*.a$
65. **Expliquez la méthode de Thompson permettant de faire la même chose.**
66. Donnez une méthode pour déterminiser un automate non déterministe.
67. Déterminisez l'automate de la question 64.
68. Donnez un automate déterministe reconnaissant le langage associé à $(a|b)^*c$
69. Théorème de Kleene.
70. Lemme de l'étoile. L’utiliser pour démontrer que $L_4=\{a^nb^n : n\in\N\}$ n'est pas régulier.
71. **Opération quotient gauche. Si $L$ régulier, $K^{-1}L$ aussi.**
72. **Mots de Dyck. Les mots de Dyck ne sont pas rationnel. Nombre de mots de Dyck de $2n$ lettres**
73. Définir une grammaire. Une grammaire non contextuelle. **Une grammaire contextuelle. Une grammaire régulière.**
74. Définir une dérivation. Dérivation immédiate.
75. **Donnez la transformation pour obtenir un automate à partir d'une grammaire régulière à droite.**
76. Donnez des grammaires qui engendre $L_1$ et $L_2$.
77. Définir l’ambiguïté d'une grammaire. **Un langage inhéremment ambigüe.**
78. Démontrez que $L_5=\{a^{\ell }b^mc^n\mid m=\ell \ {\text{ou}}\ m=n\}$ est algébrique et **inhéremment ambigüe.**
79. Donnez une grammaire non ambigüe représentant les formules logiques. Pareillement pour les mots de Dyck.
80. Rappelez le problème du *sinon pendant*.
81. **Faire le diagramme de la hiérarchie de Chomsky**
82. Démontrez que $x \rArr^* uv$ ssi $\exist a.\exist b.\ (x=ab\land a\rArr^* u \land b\rArr^* v)$

## Logique
83. Pour chaque opérateur $\lnot, \land, \lor, \rarr, \lrarr$, donner son arité et sa table de vérité.
84. Écrire sous la forme d'arbre les formules logique $A \lrarr \lnot B$ et $A \land (B\lor \lnot C)$
85. Donnez une bijection entre $\{V, F \}$ et $\N/2\N$. A quoi correspondent les opérateurs $\lnot$ et $\land$ ? En déduire $\lor$
86. Exprimez $\lor$, $\rarr$ et $\lrarr$ avec $\lnot$ et $\land$
87. Lois de Morgan.
88. Pour chaque variable soulignée, indiquer si elle est libre et/ou liée. Quelle est la porté du $\forall y$ ?
$$\forall x([\forall y.\exist z.\underline f(x,u)] \land [\exist f.\ \underline f(\underline y,u)])$$
89. Qu'est-ce qu'une valuation ? Un modèle ?
90. Définition de l'équivalence entre deux formule ?
91. Mettre sous forme normale conjonctive de taille 3 $C\lor B\lor A\lor (B \land \lnot C)$
92. Mettre sous forme normale disjonctive de taille 3 $C\land B\land A\land (B \lor \lnot C)$
93. Algorithme de Quine-Mc Cluskey pour réduire une formule logique
94. Déduction naturelle. Arbre de preuve.
95. Règle d'introduction et d'élimination de $\lor$, $\land$, $\rarr$ et $\lnot$, définition de $\lrarr$
96. Règle d'introduction et d'élimination de $\forall$, $\exist$
97. Qu'est-ce qu'un axiome ?
98. Le syllogisme barbara, le modus ponen.
99. **Quelle règle faut-il ajouter à la logique minimale pour avoir la logique intuitionniste ?**
100. **Citez 3 règles possible à ajouter à la logique intuitionniste pour obtenir la logique classique. Prouvez qu'elles sont équivalentes.**
101. **Faire l'arbre de preuve de $(\lnot A\land \lnot B)\lrarr \lnot (A\lor B)$ en logique minimale.**
102. **Faire l'arbre de preuve de $\lnot(A\lrarr \lnot A)$ en logique intuitionniste.**
103. Faire l'arbre de preuve de $\exist y.\forall x.P(x,y)\implies \forall x.\exist y.P(x,y)$ en logique classique où $P$ est une proposition d’arité 2.
104. **Axiomes de l'égalité.**
105. **Axiomes de Peano.** 

## Algorithmique
106. Qu'est-ce qu'un algorithme déterministe ? Un algorithme probabiliste ?
107. Différence entre un algorithme de Las Vegas et de Monte Carlos ?
108. Qu'est-ce qu'un algorithme glouton ? Diviser pour régner ?
109. Qu'est-ce que la mémoïsation ? Donnez une implémentation de la suite de Fibonacci mémoïsé. Quelle est la nouvelle complexité ?
110. **Fonction d'Ackermann**
111. Algorithme de Boyer-Moore
112. Algorithme de Rabin-Karp
113. Algorithme de Huffman
114. Algorithme Lempel-Ziv-Welch
115. Algorithme de Kosaraju de recherche de composante fortement connexe à l'aide de parcours du graphe.
116. Algorithme de Dijkstra avec une file de priorité. Prononciation du nom.
117. Algorithme de Floyd-Warshall.
118. Recherche d’un arbre couvrant de poids minimum par l’algorithme de Kruskal.
119. Tri à bulle. Tri par insertion. Tris fusion. Tri par tas. Tri rapide *(quicksort)*. 

## Apprentissage automatique et jeux
120. Différences entre IA, Apprentissage supervisé, Apprentissage non supervisé.
121. Définition d'un arbre de décision
122. Notion de distance. De pseudo-distance. **Distance de Levenshtein sur les chaines de charactères**
123. Algorithmes des k plus proches voisins avec une distance.
124. Arbre k-dimensionnel. Insertion, et recherche des k plus proches voisins dans un arbre k-dimensionnel.
125. Définissez l'entropie de Shannon. Donnez le pseudo code de ID3.
126. Matrice de confusion. Que représente la trace d'une matrice de confusion ?
127. Graphe biparti d'un jeu à deux joueurs. 
128. Preuve de l'existence d'une stratégie gagnante pour un jeu sans état finaux de match nul. Algorithme min-max.
129. Élagage alpha-bêta. Déterminez si il existe une stratégie gagnante pour le morpion.
130. Qu'est-ce qu’une heuristique ? Une heuristique admissible ?
131. Algorithme A*

## Classe de complexité
132. Qu'est-ce qu'un problème de décision ? **Un problème semi-décidable ?**
133. Prouvez la non décidabilité du problème de l’arrêt.
134. Donnez l'énoncé des problèmes suivants : $\text{SAT}$, $\text{n-SAT}$, $\text{MAX2SAT}$, $\text{k-COLOR}$
135. **Donnez l'énoncé des problèmes suivants : $\text{CLIQUE}$, $\text{VERTEX-COVER}$, $\text{HAMILOTINAN}$, $\text{CIBLE-SAC-A-DOS}$**
136. Classe $\text{P}$, Classe $\text{NP}$, **Classe $\text{EXPTIME}$**, **Classe $\text{EXPSPACE}$**
137. Réduction de problèmes en temps polynomial.
138. Montrez que $\text{SAT}\le_P\text{3-SAT}$
139. **Démontrez que les problèmes si-dessus sont tous $\text{NP}$ et même $\text{NP-complet}$ (en supposant $\text{SAT}$ $\text{NP-complet}$ )**
140. Montrez que $\text{2-SAT}\le_P\text{2-COLOR}$. En déduire que $\text{2-SAT}$ est de classe $\text{P}$

## Base de données
> Cette partie est fébrile.

On pose pour cette partie le schéma suivant :
- USERS : `nom:char[20]` `prenom:char[20]` `email:char[40]` `est_admin:binary`
- COMMANDES : `date:int` `article_id:int` `adresse:varchar[100]`
- ARTICLES : `id:int` `nom:char[50]` `contact_email:char[50]`
141. Démontrez que une association $*-*$ peut être transformer en deux associations $1-*$ 
142. Donnez le type d'association entre USERS et COMMANDES. Entre COMMANDES et ARTICLES.
143. Donnez des clefs primaire possible pour USERS. Il y a t'il des clefs étrangères ?
144. Affichez tout les utilisateurs qui ont mis en vente un article.
145. Affichez le nombre de fois que un utilisateur à acheter le produit d'un administrateur.
146. Différence entre `WHERE` et `HAVING` ? Donnez un exemple de requêtes qui donne des résultats différents, l'une utilisant `WHERE` et l'autre `HAVING`

> *Version 0.2 (beta), par @Cypooos*
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxMzQ5MzYwNyw0MjE1NDU4MCwtMjEzNj
E2ODk5LC02MDAyNTc1MTUsLTE3NDQ3MTU0MDYsNTEwNjY3NzE1
LDQxODEwMjY5NywxODE5OTYwODM3LC0xMzc5MTU2MDU4LC0xND
QyMDk3MTMzLDQ2ODczNjI5NywyMTAxNDE5NzE3LDE3NDQ5MzQw
NDAsMTA3MTQwMTk0OSwtMTY2NTM0ODY3OCwxODY3OTEzNzEsLT
EwMDU0ODgwODUsLTIzNjY2Nzk0MCwtODk0NDYzNTk1LC0xOTA1
NDYzMDA3XX0=
-->