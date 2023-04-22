# Etude du Lambda Calcul

Ce sujet introduit la théorie derrière les langages fonctionnel : le lambda calcul.
La partie I propose une introduction généralisé,
La partie II porte sur de la logique, et typé des expressions
La partie III s'intéresse au règles de grammaire de la logique combinatoire
La dernière partie s'intéresse à la notion de confluence, et fait introduire des graphes.

## Définitions

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

Soient $e\in E$ et $x,y\in V\times E$, on définie l'opération de substitution $e[x\larr y]$ inductivement :
 - $x[x\larr y] := y$
 
  - $u[x\larr y] := u$ pour $u\in V\setminus \{x\}$
  - $e(e')[x\larr y] := e[x\larr y]\Big(e'[x\larr y]\Big)$
  - $(x\mapsto e)[x\larr y] := x\mapsto e$
  - $(u\mapsto e)[x\larr y] := u\mapsto e[x\larr y]$ pour $u\in V\setminus \{x\}$

Informellement, l'on remplace toute les occurrences libre de $x$ par $y$ dans $e$. On dit que $x$ est libre dans $e$ si $e \neq e[x\larr x']$

On appelle *évaluation* de l'expression $a =$ "$(x\mapsto e)(e')$" l'expression $â=$ "$e[x\larr e']$". On note alors $a\to a'$.

On appelle *dérivation* $A\to A'$si il existe dans $A$ une expression $a$. $A'$ est $A$ ou l'on a remplacé $a$ par son évaluation.

On appelle un calcul de $A$ 

On définie les expressions suivantes :
 - $I = (x\mapsto x)$
 - $K =  (y\mapsto (x\mapsto y))$
 - $\Delta = (x\mapsto x(x))$

## Préliminaire

1. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU2ODI1MzQ5MSwyMDE5ODM3MDU5LDQ4Mj
gwMjczOSwtMjA4ODc0NjYxMl19
-->