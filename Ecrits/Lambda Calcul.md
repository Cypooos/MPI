# Etude du Lambda Calcul

Ce sujet est difficile et long, et balaye les chapitres de Grammaire, Logique, Langages, Automates.

Ce sujet introduit la théorie derrière les langages fonctionnel : le lambda calcul.

La partie I propose une implémentation d'objets de base.
La partie II propose une implémentation de la soustraction.
La partie III s'intéresse à l'opérateur point fixe et au expressions récursives.
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

L'on se permettra l'utilisation de parenthèses pour indiquer de l'ordre des opérations. On note $E$ l'ensemble des expressions.

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
On appelle *dérivation* $A\to A'$si il existe dans $A$ une expression $a$ évaluable, avec $A'$ qui est $A$ ou l'on a remplacé $a$ par son évaluation. On dit que $A$ est sous forme normale si $A$ n'est pas dérivable.

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
 - $C_n = [f,x\mapsto f(f(...(f(x))...))]$ avec $n$ répétitions de $f$ imbriqué

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

11. Montrez que $D(e,e')(\top) \to^* e$ et  $D(e,e')(\bot) \to^* e'$
12. Définir $A$ une expression telle que $A(D(e,C_n)) \to^* D(C_n,C_{n+1}))$
13. (*) Définir $\text{decr}$ telle que $\text{decr}(C_n) \to^* C_{\max\{n-1;0\}}$
14. Définir $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$ 

# Partie III
Le but de cette partie est de pouvoir faire des fonctions récursives.
## L'opérateur Point-fixe

On dit que $\text{fix}$ est un opérateur point-fixe si, pour tout $f\in E$, on a :
$$\text{fix}(f) \to f(\text{fix}(f))$$

17. Montrez que $\text{fix}(f)$ n'est pas unitaire.
19. Montrez que si $\text{fix}(f)\to^* e$, alors $\exist a\in E,\ f\to^* K(a)$ (TODO: bien revérifier)

On appellera donc ce $a$ une valeur d'initialisation.
On appellera $e$ un point fixe de $f$ si $e=f(e)$

20. Montrez que si $\exist!e\in E,\ \text{fix}(f)\to^* e$, alors $f$ admet un point fixe.
20. Donnez une valeur d'initialisation de 
21. (*) Donnez une expression $\Theta$ point-fixe.

## La fonction récursive factorielle
On définie :
$$
\text{fact\_rec} = (f,x\mapsto \text{if0}(x)(C_1)(\text{mul}(x)(f(\text{sub}(x,1)))))
$$
Et on pose $\text{fact} = \Theta(\text{fact\_rect})$

18. Montrez que $\text{fact}(C_n) \to^* C_{n!}$

## Généralisation
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3OTgxNTU2NSwxMjY2OTM0MzYsLTI3Mz
Y0ODQ5NywtMTMxMjM2MTgyOCwxMTU3MTQ2NTYyLDE2NDQ1OTg1
NTgsLTE5MjU4MTE3NiwtMTc1Njc3MDAxNSwtMTYyNjA1ODA1My
wtMTk0OTc0NjQzNiwtOTI1NDgyMDY2LC0xNDc3ODIxMzQ5LC0y
MTM3Mjc1MDQ1LDEwMzA4MTM5NTAsNjYxNDExNDQ0LC0xOTkxMz
U4MDU1LC0xODE1MTU3NzY2LC0xMzg3MTc1NzgyLC0xNTgyODk2
NjU5LC0xNjg3NTQyOTkyXX0=
-->