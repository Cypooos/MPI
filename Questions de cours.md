Par Cyprien (@Cypooos) en MPI* à Fénelon Sainte Marie. Droit à toute sorte de publication et modification, mais gardez les crédits !
En **gras** sont les questions non officiellement au programme (parfois explicitement hors programme), mais qu'il est bon de connaitre.

Il manque encore à ce document:
 - Bien refaire "base de donnée"
 - Extras (hors programme) plus théorique : Classes de fonctions, récursivité, machine de turing....

## Machines et implémentation
1.  Qu'est-ce qu'un paradigme ? Expliquez les paradigmes suivant : paradigme logique, paradigme impératif structuré, paradigme fonctionnel, **paradigme orienté objet ?**
2. Qu'est ce-qu'un langage de programmation compilé ? Interprété ? **Compilé à la volé ?**
3. Quelle est la différence entre un `signed` et un `unsigned` ? Comment sont encodé les nombre négatifs ?
4. Comment sont encodé les flottants ? Qu'est-ce que la mantisse ? En sachant que un `float` (encodé sur 32a 8 bits d'exposants, combien de chiffre significatifs en base 10 peuvent-ils stoker ?
5. Démontrez que la fonction `getter` suivante termine :
```ocaml
let rec get m l = match l with
 | [] -> m
 | e::q when e>=m -> get e q
 | e::q -> get m q;;
let getter = get min_int;;
```
Que fait-il ? Démontrer sa correction.

6. Qu'est-ce que une correction partielle ? **Parallèles avec problème décidable et semi-décidable.**
7. Définition de la complexité ? Donnez l'équation de récurrence des appels récursif du tri fusion et en déduire sa complexité.
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
56. Si $a,b\in\Sigma^*$ tel que $ab=ba$, alors $\exist\ \omega\in\Sigma^* \mid a,b\in\{\omega^n;n\in\N\}$
57. Définition inductive d'un langage régulier.
58. Définition inductive d'une expression régulière.
59. Définition d'un automate déterministe. Automate émondé. État accessible et co-accessible. $L(A)$ le langage reconnu par l'automate.
60. Différences avec un automate non déterministe ? $\varepsilon$-transition et 
61. **Qu'est-ce qu'une fonction de transition généralisé ?**
62. Donnez des automates déterministes sur $\Sigma=\{a,b\}$ reconnaissant
$L_1 = \{a^{2n} \mid n\in\N\}$
$L_2 = \{\omega\in\Sigma^* : |\omega|_a \in2\N\ \land\ |\omega|_b \in 3\N \}$ où $|\omega|_a$ est le nombre de $a$ dans $\omega$
**DIFFICILE : $L_3$, les mots binaires qui sont des multiples de 3 écrit en base 2**
63. Notion de langage local, d'expression régulière linéaire.
64. Donnez la méthode de Glush-kov (ou algorithme de Berry-Sethi) pour obtenir l'automate reconnaissant le langage associé à un regexp.
65. Donnez l'automate de Glush-kov associé à $((a|b).(bb|ca))^*.a$
66. **Expliquez la méthode de Thompson permettant de faire la même chose.**
67. Donnez une méthode pour déterminiser un automate non déterministe.
68. Déterminisez l'automate de la question 64.
69. Donnez un automate déterministe reconnaissant le langage associé à $(a|b)^*c$
70. Théorème de Kleene.
71. Lemme de l'étoile. L’utiliser pour démontrer que $L_4=\{a^nb^n : n\in\N\}$ n'est pas régulier.
72. **Opération quotient gauche. Si $L$ régulier, $K^{-1}L$ aussi.**
73. **Mots de Dyck. Les mots de Dyck ne sont pas rationnel. Nombre de mots de Dyck de $2n$ lettres**
74. Définir une grammaire. Une grammaire non contextuelle. **Une grammaire contextuelle. Une grammaire régulière.**
75. Définir une dérivation. Dérivation immédiate.
76. **Donnez la transformation pour obtenir un automate à partir d'une grammaire régulière à droite.**
77. Donnez des grammaires qui engendre $L_1$ et $L_2$.
78. Définir l’ambiguïté d'une grammaire. **Un langage inhéremment ambigüe.**
79. Démontrez que $L_5=\{a^{\ell }b^mc^n\mid m=\ell \ {\text{ou}}\ m=n\}$ est algébrique et **inhéremment ambigüe.**
80. Donnez une grammaire non ambigüe représentant les formules logiques. Pareillement pour les mots de Dyck.
81. Rappelez le problème du *sinon pendant*.
82. **Faire le diagramme de la hiérarchie de Chomsky**
83. Démontrez que $x \rArr^* uv$ ssi $\exist a.\exist b.\ (x=ab\land a\rArr^* u \land b\rArr^* v)$

## Logique
84. Pour chaque opérateur $\lnot, \land, \lor, \rarr, \lrarr$, donner son arité et sa table de vérité.
85. Écrire sous la forme d'arbre les formules logique $A \lrarr \lnot B$ et $A \land (B\lor \lnot C)$
86. Donnez une bijection entre $\{V, F \}$ et $\N/2\N$. A quoi correspondent les opérateurs $\lnot$ et $\land$ ? En déduire $\lor$
87. Exprimez $\lor$, $\rarr$ et $\lrarr$ avec $\lnot$ et $\land$
88. Lois de Morgan.
89. Pour chaque variable soulignée, indiquer si elle est libre et/ou liée. Quelle est la porté du $\forall y$ ?
$$\forall x([\forall y.\exist z.\underline f(x,u)] \land [\exist f.\ \underline f(\underline y,u)])$$
90. Qu'est-ce qu'une valuation ? Un modèle ?
91. Définition de l'équivalence entre deux formule ?
92. Mettre sous forme normale conjonctive de taille 3 $C\lor B\lor A\lor (B \land \lnot C)$
93. Mettre sous forme normale disjonctive de taille 3 $C\land B\land A\land (B \lor \lnot C)$
94. Algorithme de Quine-Mc Cluskey pour réduire une formule logique
95. Déduction naturelle. Arbre de preuve.
96. Règle d'introduction et d'élimination de $\lor$, $\land$, $\rarr$ et $\lnot$, définition de $\lrarr$
97. Règle d'introduction et d'élimination de $\forall$, $\exist$
98. Qu'est-ce qu'un axiome ?
99. Le syllogisme barbara, le modus ponen.
100. Quelle règle faut-il ajouter à la logique minimale pour avoir la logique intuitionniste ?
101. Citez 3 règles possible à ajouter à la logique intuitionniste pour obtenir la logique classique. Prouvez qu'elles sont équivalentes.
102. Faire l'arbre de preuve de $(\lnot A\land \lnot B)\lrarr \lnot (A\lor B)$ en logique minimale.
103. Faire l'arbre de preuve de $\lnot(A\lrarr \lnot A)$ en logique intuitionniste.
104. Faire l'arbre de preuve de $\exist y.\forall x.P(x,y)\implies \forall x.\exist y.P(x,y)$ en logique classique où $P$ est une proposition d’arité 2.
105. **Axiomes de l'égalité.**
106. **Axiomes de Peano.** 

## Algorithmique
107. Qu'est-ce qu'un algorithme déterministe ? Un algorithme probabiliste ?
108. Différence entre un algorithme de Las Vegas et de Monte Carlos ?
109. Qu'est-ce qu'un algorithme glouton ? Diviser pour régner ?
110. Qu'est-ce que la mémoïsation ? Donnez une implémentation de la suite de Fibonacci mémoïsé. Quelle est la nouvelle complexité ?
111. **Fonction d'Ackermann**
112. Algorithme de Boyer-Moore
113. Algorithme de Rabin-Karp
114. Algorithme de Huffman
115. Algorithme Lempel-Ziv-Welch
116. Algorithme de Kosaraju de recherche de composante fortement connexe à l'aide de parcours du graphe.
117. Algorithme de Dijkstra avec une file de priorité. Prononciation du nom.
118. Algorithme de Floyd-Warshall.
119. Recherche d’un arbre couvrant de poids minimum par l’algorithme de Kruskal.
120. Tri à bulle. Tri par insertion. Tris fusion. Tri par tas. Tri rapide *(quicksort)*. 

## Apprentissage automatique et jeux
121. Différences entre IA, Apprentissage supervisé, Apprentissage non supervisé.
122. Définition d'un arbre de décision
123. Notion de distance. De pseudo-distance. **Distance de Levenshtein sur les chaines de charactères**
124. Algorithmes des k plus proches voisins avec une distance.
125. Arbre k-dimensionnel. Insertion, et recherche des k plus proches voisins dans un arbre k-dimensionnel.
126. Définissez l'entropie de Shannon. Donnez le pseudo code de ID3.
127. Matrice de confusion. Que représente la trace d'une matrice de confusion ?
128. Graphe biparti d'un jeu à deux joueurs. 
129. Preuve de l'existence d'une stratégie gagnante pour un jeu sans état finaux de match nul. Algorithme min-max.
130. Élagage alpha-bêta. Déterminez si il existe une stratégie gagnante pour le morpion.
131. Qu'est-ce qu’une heuristique ? Une heuristique admissible ?
132. Algorithme A*

## Classe de complexité
133. Qu'est-ce qu'un problème de décision ? **Un problème semi-décidable ?**
134. Prouvez la non décidabilité du problème de l’arrêt.
135. Donnez l'énoncé des problèmes suivants : $\text{SAT}$, $\text{n-SAT}$, $\text{MAX2SAT}$, $\text{k-COLOR}$
136. **Donnez l'énoncé des problèmes suivants : $\text{CLIQUE}$, $\text{VERTEX-COVER}$, $\text{HAMILOTINAN}$, $\text{CIBLE-SAC-A-DOS}$**
137. Classe $\text{P}$, Classe $\text{NP}$, **Classe $\text{EXPTIME}$**, **Classe $\text{EXPSPACE}$**
138. Réduction de problèmes en temps polynomial.
139. Montrez que $\text{SAT}\le_P\text{3-SAT}$
140. **Démontrez que les problèmes si-dessus sont tous $\text{NP}$ et même $\text{NP-complet}$ (en supposant $\text{SAT}$ $\text{NP-complet}$ )**
141. Montrez que $\text{2-SAT}\le_P\text{2-COLOR}$. En déduire que $\text{2-SAT}$ est de classe $\text{P}$

## Base de données
> Cette partie est fébrile.

On pose pour cette partie le schéma suivant :
- USERS : `nom:char[20]` `prenom:char[20]` `email:char[40]` `est_admin:binary`
- COMMANDES : `date:int` `article_id:int` `adresse:varchar[100]`
- ARTICLES : `id:int` `nom:char[50]` `contact_email:char[50]`
142. Démontrez que une association $*-*$ peut être transformer en deux associations $1-*$ 
143. Donnez le type d'association entre USERS et COMMANDES. Entre COMMANDES et ARTICLES.
144. Donnez des clefs primaire possible pour USERS. Il y a t'il des clefs étrangères ?
145. Affichez tout les utilisateurs qui ont mis en vente un article.
146. Affichez le nombre de fois que un utilisateur à acheter le produit d'un administrateur.
147. Différence entre `WHERE` et `HAVING` ? Donnez un exemple de requêtes qui donne des résultats différents, l'une utilisant `WHERE` et l'autre `HAVING`

> *Version 0.3 (beta), par @Cypooos*
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MjQxMDA4MTIsNDQzODk3NjcxLDQyMT
U0NTgwLC0yMTM2MTY4OTksLTYwMDI1NzUxNSwtMTc0NDcxNTQw
Niw1MTA2Njc3MTUsNDE4MTAyNjk3LDE4MTk5NjA4MzcsLTEzNz
kxNTYwNTgsLTE0NDIwOTcxMzMsNDY4NzM2Mjk3LDIxMDE0MTk3
MTcsMTc0NDkzNDA0MCwxMDcxNDAxOTQ5LC0xNjY1MzQ4Njc4LD
E4Njc5MTM3MSwtMTAwNTQ4ODA4NSwtMjM2NjY3OTQwLC04OTQ0
NjM1OTVdfQ==
-->