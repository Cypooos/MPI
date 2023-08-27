# Etude du Lambda Calcul

Ce sujet introduit la théorie derrière les langages fonctionnels : le lambda calcul.

La partie I introduit le lambda calcul et les booléens.
La partie II étudie la $\beta$-équivalence et la propriété de *Church-Rosser*.
La partie III implémente les entiers de Church et les opérations classiques dessus.
La partie IV introduit le principe d'opérateur point-fixe et la récursivité.
La partie V définie des types aux expressions du lambda calcul. Elle est en cours d'écriture.
La partie VI, pour aller plus loin.

Dépendances des différentes parties :
$$
\begin{array}{ccccc} 
&&\text{I}&\\
&\swarrow&&\searrow\\
\text{II}&&&&\text{III}\\
\downarrow&&\swarrow&&\downarrow\\
\text{IV}&&&&\text{V}\\
\end{array}
$$
(la partie IV est dépendante de la II et de la III) 

Les questions les plus difficile sont préambules d'une étoile (*).
On pourra admettre une question pour passer à la suivante.
Ce sujet n'est pas fait pour être réalisé en 4h.

# Définitions


Soit $V$ un ensemble dénombrable infini de *variables*.
On définit une *expression* inductivement :
 - "$x$" est une expression pour tout $x\in V$
 - "$e_1(e_2)$" est une expression pour tout $e_1,e_2$ deux expressions
 - "$x\mapsto e$" est une expression pour tout $x\in V$ et $e$ une expression

On utilisera des parenthèses pour lever les ambiguïtés de cette grammaire. On note $E$ l'ensemble des expressions. Si $a$ est une expression présente dans $A$, une autre expression, on note cela $a\in A$.

On pourra noter $x_1,x_2,...,x_n\mapsto e$ pour dénoter $x_1\mapsto (x_2\mapsto(...(x_n\mapsto e)...))$
On pourra noter $e(x_1,x_2,...,x_n)$ pour dénoter $e(x_1)(x_2)...(x_n)$
 
Soient $e\in E$ et $x,a\in V\times E$, on définit l'opération de *substitution* $e[x\larr a]$ inductivement :
 - $x[x\larr a] := y$
  - $u[x\larr a] := u$ pour $u\in V\setminus \{x\}$
  - $e(e')[x\larr a] := e[x\larr a]\Big(e'[x\larr a]\Big)$
  - $(x\mapsto e)[x\larr a] := x\mapsto e$
  - $(u\mapsto e)[x\larr a] := u\mapsto e[x\larr a]$ pour $u\in V\setminus \{x\}$

Informellement, $e[x\larr a]$ est $e$ dans laquelle on a remplacé toutes les occurrences libres de $x$ par $a$.

On dit que $x$ est *libre* dans $e$ si $e \neq e[x\larr x']$ avec $x' \ne x$. Une variable *liée* de $A$ est une variable $x$ non libre dans $A$ avec $x\in A$.

Dans ce sujet, un renommage d'une variable liée ne change pas fondamentalement l'expression. On identifiera donc deux expressions à renommage d'une variable liée près. Par exemple, les expressions $x\mapsto x$ et $y\mapsto y$ seront identifiée, même si $x\neq y$.

On appelle *évaluation* de l'expression $a =(x\mapsto e)(e')$ l'expression $â=e[x\larr e']$.
On appelle *dérivation* $A\to A'$si il existe $a\in A$ évaluable, avec $A'$ qui est $A$ ou l'on a remplacé une occurrence de $a$ par son évaluation $\hat a$. On dit que $A$ est sous forme normale si $A$ n'est pas dérivable.

On appelle un calcul de $A$ une série de dérivations finie $A\to A_1 \to ... \to A_n$. On note cela $A\to^n A_n$ ou $A\to^* A_n$. Si $A_n$ est sous forme normale, on appelle cela un calcul normalisant.

Si tout les calculs à partir de $A$ sont de longueurs inférieur à un certain $n$, on dit que $A$ est unitaire. *(Rem: Dans la littérature, le terme de "fortement normalisable" est plutôt employé.)*

On définit les expressions suivantes :
 - $I = (x\mapsto x)$
 - $K =  (y\mapsto (x\mapsto y)) = (y,x\mapsto y)$
 - $\Delta = (x\mapsto x(x))$

# Partie I: Introduction

## Préliminaires
1. Donner un calcul normalisant de $K(K,I)$, de $I(I)$, de $K(I,\Delta)$
2. Montrer que l'expression $\Delta(\Delta)$ ne possède aucun calcul normalisant.

## Graphe des réductions
Soit $e\in E$, on pose $G_e = (S_e,A_e)$ le *graphe orienté des réductions de $e$* avec $S_e = \{x\in E : e \to^* x\}$ et $A_e = \{(x,y)\in S_e^2 : x\to y \}$

3. Donner le graphe des réductions de $K(I,\Delta(\Delta))$, et de $\Delta((x\mapsto\Delta)(I))$.
4. Donner une expression donnant un graphe des réductions infini.
5. Montrer que si le graphe des réductions de $e$ est acyclique fini, alors $e$ est unitaire. 

## Booléens
On pose $\top = (x,y\mapsto x)$ et $\bot = (x,y\mapsto y)$. On pose $B=\{\top,\bot\}$
On pose $\text{if} = (b,f_1,f_2\mapsto b(f_1,f_2))$

6. Montrer que, soit $e,e'\in E$, on a $\text{if}(\top,e,e') \to^* e$ et $\text{if}(\bot,e,e') \to^* e'$ 
7. Définir une expression $\text{not}$ tel que $\text{not}(\top) \to^* \bot$ et $\text{not}(\bot) \to^* \top$
8. Définir une expression $\text{and}$ tel que, soit $b,b'\in B$, on ai:
   * $\text{and}(b,b') \to^* \top$  si $b=b'=\top$
   * $\text{and}(b,b') \to^* \bot$  sinon

# Partie II: résultats généralistes


## $\beta$-équivalence

On pose $\lrarr$ la fermeture symétrique de $\to$ : on a $x\lrarr y$ si et seulement si $x\to y$ ou $y\to x$

On pose $G = (E,A)$ un graphe orienté infini avec $A = \{(x,y)\in E^2 : x\to^* y \}$
On définie $=_\beta$ une relation d'équivalence telle que $x=_\beta y$ si $x$ et $y$ appartiennent à la même composante faiblement connexe dans $G$

9. Montrer que $a=_\beta b$, si et seulement si il existe $n\in\N$ et $M_1,...,M_n \in E$ tel que $a\lrarr M_1\lrarr...\lrarr M_n\lrarr b$
10. Montrer que $=_\beta$ est une relation d'équivalence sur $E$. 

## Le théorème de _Church-Rosser_

On dit que une relation $\mathcal{R}$ sur $E$ respecte la propriété du diamant si :
> Soit $t,u,v\in E$, si $t\mathcal{R}u$ et $t\mathcal{R}v$, alors il existe $\omega\in E$ tel que $u\mathcal{R}\omega$ et $v\mathcal{R}\omega$

Le théorème de *Church-Rosser* assure que la relation $\to^*$ respecte la propriété du diamant.

Pour démontrer cela, on pose $\triangleright$ la réduction parallèle tel que :
- $x\triangleright x$
- $x\mapsto t \triangleright x\mapsto t'$ si $t \triangleright t'$
- $t(x)\triangleright t'(x')$ si $t\triangleright t'$ et $x\triangleright x'$
- $(x\mapsto e)(u) \triangleright t'[x\larr u']$ si $t \triangleright t'$ et $u \triangleright u'$

11. Montrer que si $a\to b$, alors $a\triangleright b$.
12. Montrer que si $a\triangleright b$, alors $a\to^* b$
13. Montrer les règles d'interversion de la substitution, à savoir : soient $t,t',e \in E$ et $x,y\in V$,
Si $x\neq y$, on a $t[x\larr t'][y\larr e] = t[y\larr e][x\larr t'[y\larr e]]$
Si $x=y$, on a $t[x\larr t'][y\larr e] = t[x\larr t'[y\larr e]]$
14. Donner un $e\in E$ ayant $x$ comme variable libre tel que, si $t\to t'$, on a n'a pas $e[x\larr t] \to e[x\larr t']$ 
15. Montrer que, soit $t,t',v,v' \in E$ et $x\in V$, si $t\triangleright  t'$ et $v\triangleright v'$, alors $t[x \larr v] \triangleright t'[x \larr v']$
> Indication : On peut procéder par induction selon la règle obtenue pour avoir $t\triangleright t'$.
16. (\*) Montrez le théorème de *Church-Rosser*.

## Autour de Church-Rosser
17. Montrez que si $a\in E$ possède une forme normale, alors celle-ci est unique.

> Remarque : On a ici prouvé que quelque-soit notre manière d'évaluer une expression $e$ bien écrite, on tombera toujours sur le même résultat. Autrement dit, le lambda calcul est fondamentalement "déterministe" par rapport à son implémentation.
> Attention, cela suppose que l'on arrive à atteindre la forme normale après un nombre fini d'étapes. Dans le cas de $\text{if}(\top,I,\Delta(\Delta)) \to^* I$, si l'on calcule constamment $\Delta(\Delta)$, on n'atteindra jamais la forme normale $I$, alors qu'elle existe et est unique.

18. Montrez que si $a=_\beta b$, alors il existe $e\in E$ tel que $a\to^* e$ et $b\to^* e$
19. Soit $f\in E$. Donnez une expression $g$ tel que pour tout $e\in E$ on ai $f(e) =_\beta g(e)$ mais $f \neq_\beta g$

# Partie III: Entiers et opérations

## Entiers de Church

Pour tout $n\in\N$, on pose :
 - $C_0 = [f,x\mapsto x]$
 - $C_1 = [f,x\mapsto f(x)]$
 - $C_2 = [f,x\mapsto f(f(x))]$
 - $C_n = [f,x\mapsto f^n(x)]$ avec $f^n$ représentant $n$ répétitions de $f$ imbriqué

On appelle $C_n$ l'*entier de Church* associé à $n$.

20. Définir une expression $\text{succ}$ tel que $\text{succ}(C_n)\to^* C_{n+1}$
21. Définir une expression $\text{add}$ tel que $\text{add}(C_n,C_m) \to^* C_{n+m}$
22. Définir une expression $\text{mul}$ tel que $\text{mul}(C_n,C_m) \to^* C_{n\times m}$ 



## Soustraction

L'objectif de cette partie est d'implémenter $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m\ ;\ 0\}}$
On définit :
$$D = (x,y,z \mapsto z(x,y))$$

qui représente un couple $(x,y)$

23. Montrez que $D(e,e')(\top) \to^* e$ et  $D(e,e')(\bot) \to^* e'$.
24. Définir $A$ une expression telle que $A(D(e,C_n)) \to^* D(C_n,C_{n+1})$
25. (*) Définir $\text{decr}$ telle que $\text{decr}(C_n) \to^* C_{\max\{n-1;0\}}$. On expliquera le raisonnement.
26. Définir $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$

## Conditions sur les entiers de Church
27. Définir $\text{eq\_0}$ une expression tel que $\text{eq\_0}(C_0)\to^* \top$ et $\forall n>0,\ \text{eq\_0}(C_n)\to^* \bot$ 
28. Définir $\text{eq}$ une expression tel que :
    * $\text{eq}(C_n,C_m) \to^* \top$ si $n=m$
    * $\text{eq}(C_n,C_m) \to^* \bot$ si $n\neq m$

# Partie IV: Point-fixe et Récursivité
Le but de cette partie est de pouvoir faire des fonctions récursives.
## L'opérateur Point-fixe


On ce donne $\text{fix}$ un opérateur point-fixe, c'est-à dire une expression sous forme normale et telle que, pour tout $f\in E$, on a :
$$\text{fix}(f) =_\beta f(\text{fix}(f))$$

29. Montrer que si $\text{fix}(f) \to^* f(\text{fix}(f))$, alors $\text{fix}(f)$ n'est pas unitaire.

On appellera $e$ un *point fixe* de $f$ si $f(e) =_\beta e$, et un *point fixe fort* de $f$ si $f(e)\to^* e$

30. Montrer que tout $f\in E$ admet un point fixe.

31. Montrez que si pour tout $e\in E$, on a que $f(e)$ admet une forme normale, alors $f$ admet un point fixe fort.

32. (*) Donner une expression point-fixe.

> Voir *Pour aller plus loin*, question 1, 2 et 3
## Récursivité
On considère ici $F$ de la forme $F=(f,x\mapsto e)$ une fonction récursive, c'est à dire que $F$ sera appelé constamment avec $F$ comme premier argument. 

33. Justifier sans démonstration que, pour tout $\alpha$ sous forme normale, $\forall e\in E$,
$$\text{fix}(F)(e) \to^* \alpha \implies\exist n_r,\ \underbrace{F(F(...(F)...))}_{n_r\text{ fois}}(e)\to^*\alpha$$


Si $\alpha$ est sous forme normale, on appellera le plus petit $n_r$ le *nombre d'appels récursif* de $F(x)$.

> Voir *Pour aller plus loin*, question 4
## Un exemple
On définit :
$$
\text{fact\_rec} = (f,x\mapsto \text{if}(\text{eq\_0}(x))(C_1)(\text{mul}(x,f(\text{sub}(x,1)))))
$$
Et on pose $\text{fact} = \text{fix}(\text{fact\_rect})$

34. Montrer que $\text{fact}(C_n) \to^* C_{n!}$
35. (*) Donner une expression $\text{pow\_rec}$ tel que, soit $n,m\in\N$, on ai $\text{fix}(\text{pow\_rec})(C_n,C_m) \to^* C_{n^m}$ avec $n_r = O(\log_2(m))$. On n’utilisera pas d'opérateur point fixe dans la définition de $\text{pow\_rec}$. *(On posera ici que $0^0 = 1$)*

# Partie V: Types (en cours)
Cette partie s'intéresse au lambda calcul typé, elle cherche à imposer des règles telle que on obtienne un caractérisation des expressions unitaire.

On pose $T$ tel que $\{\tau,\tau_1,\tau_2,...\} \sub T$ et pour tout $t,t'\in T$, on a $(t\to t')\in T$. On appelle $\tau,\tau_1,\tau_2,...$ les *types par défault*.

Un *contexte de type*, dénoté par $\Gamma$, est un sous-ensemble de $X\times T$.
Un *jugement de type* est un triplet $\Gamma \vdash x: t$ tel que on ai les règles d'inférences suivantes :

Axiome, pour $(x,t) \in \Gamma$ :
$$
\frac{}{\Gamma \vdash x: t}\tiny\text{(ax)}\\
$$
Généralisation :
$$
\frac{\Gamma \vdash x: t}{\Gamma\cup\Gamma' \vdash x: t}\tiny\text{(gen)}\\
$$
Evaluation :
$$
\frac{\Gamma \vdash f: t\to t',\qquad \Gamma \vdash x: t}{\Gamma \vdash f(x): t'}\tiny\text{(ev)}
$$
Abstraction :
$$
\frac{\Gamma\ \cup \{(x,t)\} \vdash x': t'}{\Gamma\ \vdash x\mapsto x': t\to t'}\tiny\text{(ab)}
$$

On dit que $t$ est un *typage* de $x$ si $\empty \vdash x:t$.
Par exemple, ce qui suit est un arbre de dérivation montrant que $\tau\to\tau$ est un typage de $I$ :
$$
\cfrac{}{\cfrac{(x,\tau) \vdash x: \tau}{\empty \vdash x\mapsto x : \tau\to \tau}\tiny\text{(ab)}}\tiny\text{(ax)}\\
$$

 On n'hésitera pas a ajouter des parenthèses pour ce faire comprendre : par défaut, les flèches sont une opération de droite à gauche, ainsi, $\tau\to\tau\to\tau = \tau\to(\tau\to\tau)$
On notera $e:t$ pour dire qu'une expression $e$ à un typage $t$.
Si $t$ un type est présent dans $t'$ un autre type, on notera cela $t\in t'$.
## Typage de groupe d'expressions

36. Donner un arbre de dérivation donnant un typage de $\top$ et $C_1$

Soit $A\sube E$. Si $t$ est un type tel que $\forall a\in A, \empty \vdash a:t$, on dira que $t$ est le type généralisé de $A$

37. Donner $t$ un type généralisé de $\{\top, \bot\}$
38. Donner $t$ un type généralisé de $\{C_n\ |\ n\in\N\}$

## Caractérisation des expressions unitaire
Le but de cette partie est de montrer que tout les expressions unitaire sans variable libre sont typé.
> Les questions arriveront....

## Réciproque

> Les questions arriveront....



# VI Pour aller plus loin
Toutes les questions ici sont difficiles.

1. Donner un opérateur point fixe $\Theta$ tel que $\Theta(f) \to^* f(\Theta(f))$
2. Montrer que si pour tout $e\in E$, on a que $f(e)$ normalisable, alors $f$ est constante, c'est à dire que il existe $\omega \in E$ tel que $x\not \in \omega$ et $f =_\beta (x\mapsto \omega)$

3. On cherche à calculer la forme normale de $f(e)$, pour cela on met d'abord l'argument $e$ sous forme normale inductivement avant de faire l'évaluation. Comment changer $Y$ tel que le calcul de $\text{fact}(C_1)$ termine ? 


4. Faire la preuve de la question 33 avec l’opérateur point fixe $\Theta$
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MzIxNzQ4MTMsLTEzODY3MzEwMTAsMT
gyNDQyMTEwMiwtMjEwODI0NzkwMiwtMTYxMDY3MzUxNSwtODQ1
MzUxNDY1XX0=
-->