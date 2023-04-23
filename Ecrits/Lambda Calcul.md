# Etude du Lambda Calcul

Ce sujet est difficile et long, et balaye les chapitres de Grammaire, Logique, Langages, Automates.

Ce sujet introduit la théorie derrière les langages fonctionnel : le lambda calcul.

La partie I propose une implémentation d'objets de base.
La partie II propose une implémentation de la soustraction.
La partie III s'intéresse à l'opérateur point fixe et au expressions récursives. Elle est plus théorique.
La partie IV porte sur de la logique, des expressions typées.
La partie V s'intéresse au règles de grammaire et à la logique combinatoire.
La partie VI s'intéresse à la notion de confluence, et fait introduire des graphes.

Toutes les parties sont dépendante de la partie 1, mais sont indépendantes entre elles.

Les questions plus difficile sont préambulées d'une étoile (*).
On pourra admettre une question pour passer à la suivante.

# Définitions

Soit $\Sigma$ un ensemble de *lettres*. On dis que $\omega=\omega_1...\omega_n$ est un *mot* s'il est une suite finie de lettre. On note $\varepsilon$ le mot vide.
 Pour $\omega$ un mot, on note $|\omega|$ sa longueur et pour $\alpha\in\Sigma$, on note $|\omega|_\alpha$ le nombre d'occurrences de $\alpha$ dans $\omega$.
 Soit $n\in\N$, on note $\Sigma^n$ l'ensemble des mots de $\Sigma$ à $n$ lettres. On note $\Sigma^* = \cup_{n\in\N}\Sigma^n$
On appelle *langage* un sous-ensemble de mots.

Soit $V=\{x,y,z,t,u,v,...\}$ un ensemble dénombrable de *variables*.
On définie une *expression* inductivement :
 - "$x$" est une expression pour tout $x\in V$
 - "$e_1(e_2)$" est une expression pour tout $e_1,e_2$ deux expressions
 - "$x\mapsto e$" est une expression pour tout $x\in V$ et $e$ une expression

L'on se permettra l'utilisation de parenthèses pour indiquer de l'ordre des opérations. On note $E$ l'ensemble des expressions. Si $a$ est une expression présente dans $A$, une autre expression, on note cela $a\in A$.

On pourra noter $x_1,x_2,...,x_n\mapsto e$ pour dénoter $x_1\mapsto (x_2\mapsto(...(x_n\mapsto e)...))$
On pourra aussi noter $e(x_1)(x_2)...(x_n)$ comme $e(x_1,x_2,...,x_n)$

Soient $e\in E$ et $x,y\in V\times E$, on définie l'opération de substitution $e[x\larr y]$ inductivement :
 - $x[x\larr y] := y$
  - $u[x\larr y] := u$ pour $u\in V\setminus \{x\}$
  - $e(e')[x\larr y] := e[x\larr y]\Big(e'[x\larr y]\Big)$
  - $(x\mapsto e)[x\larr y] := x\mapsto e$
  - $(u\mapsto e)[x\larr y] := u\mapsto e[x\larr y]$ pour $u\in V\setminus \{x\}$

Informellement, $e[x\larr y]$ est $e$ dans laquelle on a remplacé toute les occurrences libre de $x$ par $y$.

On dit que $x$ est libre dans $e$ si $e \neq e[x\larr x']$ avec $x' \ne x$

On appelle *évaluation* de l'expression $a =$ "$(x\mapsto e)(e')$" l'expression $â=$ "$e[x\larr e']$".
On appelle *dérivation* $A\to A'$si il existe $a\in A$ évaluable, avec $A'$ qui est $A$ ou l'on a remplacé $a$ par son évaluation. On dit que $A$ est sous forme normale si $A$ n'est pas dérivable.

On appelle un calcul de $A$ une série de dérivations finie $A\to A_1 \to ... \to A_n$. On note cela $A\to^* A_n$. Si $A_n$ est sous forme normale, on appelle cela un calcul normalisant. 
Si il existe au plus qu'un seul calcul normalisant de $A$ possible, on dit que $A$ est unitaire.

On définie les expressions suivantes :
 - $I = (x\mapsto x)$
 - $K =  (y\mapsto (x\mapsto y)) = (y,x\mapsto y)$
 - $\Delta = (x\mapsto x(x))$

# Partie 1

## Préliminaires
1. Donnez un calcul normalisant de $K(K,I)$, de $I(I)$, de $K(I,\Delta)$
2. Montrez que l'expression $\Delta(\Delta)$ ne possède aucun calcul normalisant.

On s'intéresse maintenant à la création de différents objets de base.
## Booléens
On pose $\top = (x,y\mapsto x)$ et $\bot = (x,y\mapsto y)$. On pose $B=\{\top,\bot\}$
On pose $\text{if} = (b,f_1,f_2\mapsto b(f_1,f_2))$

3. Montrez que, soit $b\in B$ et $e,e'\in E$, on a $\text{if}(b,e,e') \to^* e \iff b = \top$
4. Définir une expression $\text{not}$ tel que $\text{not}(\top) \to^* \bot$ et $\text{not}(\bot) \to^* \top$
5. Définir une expression $\text{and}$ tel que, soit $b,b'\in B$, on ai:
   * $\text{and}(b,b') \to^* \top$  si $b=b'=\top$
   * $\text{and}(b,b') \to^* \bot$  sinon

## Entiers de Church

Pour tout $n\in\N$, on pose :
 - $C_0 = [f,x\mapsto x]$
 - $C_1 = [f,x\mapsto f(x)]$
 - $C_2 = [f,x\mapsto f(f(x))]$
 - $C_n = [f,x\mapsto f^n(x)]$ avec $f^n$ représentant $n$ répétitions de $f$ imbriqué

On appelle $C_n$ l'*entier de Church* associé à $n$.

6. Définir une expression $\text{succ}$ tel que $\text{succ}(C_n)\to^* C_{n+1}$
7. Définir une expression $\text{add}$ tel que $\text{add}(C_n,C_m) \to^* C_{n+m}$
8. Définir une expression $\text{mul}$ tel que $\text{mul}(C_n,C_m) \to^* C_{n\times m}$

On utilisera les opérations $\text{add}$ et $\text{mul}$ pour représenter l'addition et la multiplication entre entiers que l'on représentera sous la forme d'entiers de Church.
On suppose l'opération $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$ a été écrite ; l'écrire est l'objet de la partie II.

## Condition sur les entiers de Church
9. Définir $\text{eq\_0}$ une expression tel que $\text{eq\_0}(C_0)\to^* \top$ et $\forall n>0,\ \text{eq\_0}(C_n)\to^* \bot$ 
10. Définir $\text{eq}$ une expression tel que :
    * $\text{eq}(C_n,C_m) \to^* \top$ si $n=m$
    * $\text{eq}(C_n,C_m) \to^* \bot$ si $n\neq m$

# Partie II
L'objectif de cette partie est d'implémenter $\text{sub}$ définie plus haut.
On définie :
$$D = (x,y,z \mapsto z(x,y))$$

qui représente un couple $(x,y)$

11. Montrez que $D(e,e')(\top) \to^* e$ et  $D(e,e')(\bot) \to^* e'$.
12. Définir $A$ une expression telle que $A(D(e,C_n)) \to^* D(C_n,C_{n+1}))$
13. (*) Définir $\text{decr}$ telle que $\text{decr}(C_n) \to^* C_{\max\{n-1;0\}}$
14. Définir $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$ 

# Partie III
Le but de cette partie est de pouvoir faire des fonctions récursives.
## L'opérateur Point-fixe

On dit que $\text{fix}$ est un opérateur point-fixe si, pour tout $f\in E$, on a :
$$\text{fix}(f) \to f(\text{fix}(f))$$

15. Montrez que $\text{fix}(f)$ n'est pas unitaire.

On appellera $e$ un point fixe de $f$ si $e=f(e)$

16. Montrez que si $\exist!e\in E,\ \text{fix}(f)\to^* e$, alors $f$ admet un point fixe.
17. Donnez une expression $f$ telle que $\exist!e\in E,\ \text{fix}(f)\to^* e$. Quel est son point fixe ?
18. (*) Donnez une expression $\Theta$ point-fixe.

## Récursivité
On considère ici $F$ de la forme $F=(f,x\mapsto e)$ une fonction récursive, c'est à dire que F sera appelé constamment avec $F$ comme premier argument.

19. Montrez que, $\forall x\in E$,
$$\text{fix}(F)(x) \to^* \alpha \implies\exist n_r,\ \underbrace{F(F(...(F)...))}_{n_r\text{ fois}}(x)\to^*\alpha$$

On notera le plus petit $n_r$ le *nombre d'appels récursif* de $F$.

## Quelques exemples
On définie :
$$
\text{fact\_rec} = (f,x\mapsto \text{if0}(x)(C_1)(\text{mul}(x)(f(\text{sub}(x,1)))))
$$
Et on pose $\text{fact} = \Theta(\text{fact\_rect})$

20. Montrez que $\text{fact}(C_n) \to^* C_{n!}$
21. Donnez un expression $\text{pow}$ tel que, soit $n,m\in\N$, on ai $\text{pow}(C_n,C_m) \to^* C_{n^m}$ avec $n_r = O(\ln m)$

# Partie IV
Cette partie s'intéresse au lambda calcul typé, elle cherche à imposer des règles telle que chaque expression bien typé soit unitaire.
On pose $\hat{T}$ un ensemble non vide de types par défaut.
Pour chaque type $\tau\in\hat{T}$ par défaut, on pose $E_{\tau}$ un ensemble d'expressions par défaut.
Par exemple, si on ajoute le type $\text{Bool}$, on posera $E_{\text{Bool}} = \{ \text{true},\text{false}\}$
De même, si on ajoute le type $\text{Nat}$, on posera $E_{\text{Nat}} = \{ 0_E,1_E,2_E,3_E, ... \}$

On pose $T$ tel que $\hat{T} \sub T$ et pour tout $\tau,\tau'\in T$, on a $\tau\to\tau'\in \hat{T}$

Un contexte de type, dénoté par $\Gamma$, est un sous-ensemble de $X\times T$
Un jugement de type est un triplet $\Gamma \vdash x: t$ tel que on ai les règles d'inférences suivantes :

Défaut, pour $t\in \hat{T}$ et $x\in E_t$ :
$$
\frac{}{\Gamma \vdash x: t}\tiny\text{(def)}\\
$$
Axiome, pour $(x,t) \in \Gamma$ :
$$
\frac{}{\Gamma \vdash x: t}\tiny\text{(ax)}\\
$$
Evaluation :
$$
\frac{\Gamma \vdash f: \tau_1 \to \tau_2,\qquad \Gamma \vdash x: \tau_1}{\Gamma \vdash f(x): \tau_2}\tiny\text{(ev)}
$$
Abstraction :
$$
\frac{\Gamma\ \cup \{(x,t)\} \vdash x': t'}{\Gamma\ \vdash x\mapsto x': t\to t'}\tiny\text{(ab)}
$$

On dit que $t$ est un typage de $x$ si $\empty \vdash x:t$.
Par exemple, ce qui suit est un arbre de dérivation montrant que $\tau\to\tau$ est un typage de $I$ :
$$
\cfrac{}{\cfrac{(x,t) \vdash x: t}{\empty \vdash x\mapsto x : \tau\to \tau}\tiny\text{(ab)}}\tiny\text{(ax)}\\
$$
 On n'hésitera pas a ajouter des parenthèses pour ce faire comprendre : par défaut, les flèches sont une opération de droite à gauche, ainsi, $\tau\to\tau\to\tau = \tau\to(\tau\to\tau)$
On notera $e:t$ pour dire qu'une expression $e$ à un typage $t$.

## Introduction
On suppose dans cette sous-partie que $\hat{T} = \{\tau\}$ et $E_\tau = \empty$

22. Donnez un arbre de dérivation donnant un typage de $\top$, $K$ et $C_0$

Soit $A\sube E$. Si $t$ est un type tel que $\forall a\in A, \empty \vdash a:t$, on dira que $t$ est le type généralisé de $A$

24. Donnez $t$ un type généralisé de $\{\top, \bot\}$
25. Donnez $t$ un type généralisé de $\{C_n\ |\ n\in\N\}$
27. Montrez que $\Delta$ n'est pas typé.

## Forme normalisante des 
On essaye de montrer que toute les expressions bien typé sont unitaire.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwNjc4NjA2LDEwNTU2MTI3MjksMTM5OT
c3Njc3NiwzNDkwMzQzMzMsMTIwMTQxMTk0NiwyMDM0MjA1NjUz
LC00MjUyNzk5ODMsLTEzNTE4ODMwNjUsLTg5MjczNTAzOSwtMj
QzMzYwMDMzLDM3MDE2Mjg4NSwtNTgzMjM3NzcwLDE1OTk2MjE0
NDAsLTk1MzQ5NDAxNiwxNTc5ODE1NTY1LDEyNjY5MzQzNiwtMj
czNjQ4NDk3LC0xMzEyMzYxODI4LDExNTcxNDY1NjIsMTY0NDU5
ODU1OF19
-->