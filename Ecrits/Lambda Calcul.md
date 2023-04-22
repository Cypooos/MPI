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

Soit $V=\{x,$ un ensemble de *variables*.
On définie une *expression* inductivement :
 - "$x$" est une expression pour tout $x\in V$
 - "$e_1(e_2)$" est une expression pour tout $e_1,e_2$ deux expressions
 - "$\lambda x.e$" est une expression pour tout $x\in V$ et $e$ une expression


## Préliminaire


Soit $V$ un ensemble de variables. 
On définie une instruction de lambda cal
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNjY5NDY0NTcsNDgyODAyNzM5LC0yMD
g4NzQ2NjEyXX0=
-->