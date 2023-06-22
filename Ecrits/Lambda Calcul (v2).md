# Etude du Lambda Calcul

Ce sujet est difficile, et balaye les chapitres de Logique, Grammaire, et programmation fonctionnelle.

Ce sujet introduit la théorie derrière les langages fonctionnel : le lambda calcul.

Les questions plus difficile sont préambulées d'une étoile (*).
On pourra admettre une question pour passer à la suivante.
Il n'est pas fait pour être réalisé en 4h.

# Définitions


Soit $V=\{x,y,z,t,u,v,...\}$ un ensemble dénombrable infinie de *variables*.
On définit une *expression* inductivement :
 - "$x$" est une expression pour tout $x\in V$
 - "$e_1(e_2)$" est une expression pour tout $e_1,e_2$ deux expressions
 - "$x\mapsto e$" est une expression pour tout $x\in V$ et $e$ une expression

On utilisera des parenthèses pour indiquer de l'ordre des opérations. On note $E$ l'ensemble des expressions. Si $a$ est une expression présente dans $A$, une autre expression, on note cela $a\in A$.

On pourra noter $x_1,x_2,...,x_n\mapsto e$ pour dénoter $x_1\mapsto (x_2\mapsto(...(x_n\mapsto e)...))$
On pourra noter $e(x_1,x_2,...,x_n)$ pour dénoter $e(x_1)(x_2)...(x_n)$
 
Soient $e\in E$ et $x,y\in V\times E$, on définit l'opération de substitution $e[x\larr y]$ inductivement :
 - $x[x\larr y] := y$
  - $u[x\larr y] := u$ pour $u\in V\setminus \{x\}$
  - $e(e')[x\larr y] := e[x\larr y]\Big(e'[x\larr y]\Big)$
  - $(x\mapsto e)[x\larr y] := x\mapsto e$
  - $(u\mapsto e)[x\larr y] := u\mapsto e[x\larr y]$ pour $u\in V\setminus \{x\}$

Informellement, $e[x\larr y]$ est $e$ dans laquelle on a remplacé toute les occurrences libre de $x$ par $y$.
Dans ce sujet, pour $x,y\in V$, si $y\not\in e$ on identifiera $e$ et $e[x \larr y]$ : un renommage d'une variable ne change pas fondamentalement l'expression.

On dit que $x$ est libre dans $e$ si $e \neq e[x\larr x']$ avec $x' \ne x$

On appelle *évaluation* de l'expression $a =(x\mapsto e)(e')$ l'expression $â=e[x\larr e']$.
On appelle *dérivation* $A\to A'$si il existe $a\in A$ évaluable, avec $A'$ qui est $A$ ou l'on a remplacé $a$ par son évaluation $\hat a$. On dit que $A$ est sous forme normale si $A$ n'est pas dérivable.

On appelle un calcul de $A$ une série de dérivations finie $A\to A_1 \to ... \to A_n$. On note cela $A\to^n A_n$ ou $A\to^* A_n$. Si $A_n$ est sous forme normale, on appelle cela un calcul normalisant.

Si tout les calculs à partir de $A$ sont de longueurs inférieur à un $n$ fixé, on dit que $A$ est unitaire. *(Rem: Dans la littérature, le terme de "fortement normalisable" est plutôt employé.)*

On définit les expressions suivantes :
 - $I = (x\mapsto x)$
 - $K =  (y\mapsto (x\mapsto y)) = (y,x\mapsto y)$
 - $\Delta = (x\mapsto x(x))$

# Partie I: _Church-Rosser_ et l'unicité de la forme normale

## Préliminaires
1. Donnez un calcul normalisant de $K(K,I)$, de $I(I)$, de $K(I,\Delta)$
2. Montrez que l'expression $\Delta(\Delta)$ ne possède aucun calcul normalisant.

On s'intéresse maintenant à démontrer le théorème de _Church-Rosser_.

## le théorème de _Church-Rosser_

Pour tout $e\in E$, on pose $G_e=(S_e,V_e)$ un graphe avec $S_e=\{x\in\E\}$

3.

# Partie II: objet de base

On s'intéresse maintenant à la création de différents objets de base.
## Booléens
On pose $\top = (x,y\mapsto x)$ et $\bot = (x,y\mapsto y)$. On pose $B=\{\top,\bot\}$
On pose $\text{if} = (b,f_1,f_2\mapsto b(f_1,f_2))$

3. Montrez que, soit $e,e'\in E$, on a $\text{if}(\top,e,e') \to^* e$ et $\text{if}(\bot,e,e') \to^* e'$ 
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
On suppose l'opération $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m\ ;\ 0\}}$ a été écrite ; l'écrire est l'objet de la partie II.

## Condition sur les entiers de Church
9. Définir $\text{eq\_0}$ une expression tel que $\text{eq\_0}(C_0)\to^* \top$ et $\forall n>0,\ \text{eq\_0}(C_n)\to^* \bot$ 
10. Définir $\text{eq}$ une expression tel que :
    * $\text{eq}(C_n,C_m) \to^* \top$ si $n=m$
    * $\text{eq}(C_n,C_m) \to^* \bot$ si $n\neq m$

# Partie III: Soustraction
L'objectif de cette partie est d'implémenter $\text{sub}$ définie plus haut.
On définit :
$$D = (x,y,z \mapsto z(x,y))$$

qui représente un couple $(x,y)$

11. Montrez que $D(e,e')(\top) \to^* e$ et  $D(e,e')(\bot) \to^* e'$.
12. Définir $A$ une expression telle que $A(D(e,C_n)) \to^* D(C_n,C_{n+1})$
13. (*) Définir $\text{decr}$ telle que $\text{decr}(C_n) \to^* C_{\max\{n-1;0\}}$. On expliquera le raisonnement.
14. Définir $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$ 

# Partie IV: Récursivité
Le but de cette partie est de pouvoir faire des fonctions récursives.
## L'opérateur Point-fixe

On dit que $\text{fix}$ est un opérateur point-fixe  si il est sous forme normale et que, pour tout $f\in E$, on a :
$$\text{fix}(f) \to^* f(\text{fix}(f))$$

15. Montrez que $\text{fix}(f)$ n'est pas unitaire.

On appellera $e$ un point fixe de $f$ si $f(e)\to^* e$

16. Montrez que si $\text{fix}(f)$ et $\forall e \in E, f(e)$ admettent des formes normales, alors $f$ admet un point fixe.
17. Soit $e$ sous forme normale. Donnez une expression $f$ respectant les hypothèses de la question précédente qui admet $e$ comme point fixe.
18. (*) Donnez une expression $\Theta = (x\mapsto e)$ tel que $\Theta(f) \to^* f(e[x\larr \Theta(f)])$

*Rem: Dans la littérature, ce n'est pas la définition exacte d'un opérateur point-fixe. Voire remarque partie IV.*

## Récursivité
On considère ici $F$ de la forme $F=(f,x\mapsto e)$ une fonction récursive, c'est à dire que $F$ sera appelé constamment avec $F$ comme premier argument. 

19. Montrez que, pour tout $\alpha$ sous forme normale, $\forall x\in E$,
$$\text{fix}(F)(x) \to^* \alpha \implies\exist n_r,\ \underbrace{F(F(...(F)...))}_{n_r\text{ fois}}(x)\to^*\alpha$$


Si $\alpha$ est sous forme normale, on appellera le plus petit $n_r$ le *nombre d'appels récursif* de $F(x)$.

*J'ai mal écrit ce sujet. Pour prouver cette question, il aurai été judicieux d’utiliser le graphe introduit partie IV*

## Un exemple
On définit :
$$
\text{fact\_rec} = (f,x\mapsto \text{if}(\text{eq\_0}(x))(C_1)(\text{mul}(x,f(\text{sub}(x,1)))))
$$
Et on pose $\text{fact} = \Theta(\text{fact\_rect})$

20. Montrez que $\text{fact}(C_n) \to^* C_{n!}$
21. (*) Donnez une expression $\text{pow\_rec}$ tel que, soit $n,m\in\N$, on ai $\Theta(\text{pow\_rec})(C_n,C_m) \to^* C_{n^m}$ avec $n_r = O(\log_2(m))$. On n’utilisera pas d'opérateur point fixe. *(On posera ici que $0^0 = 1$)*

# Partie V: Types
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

22. Donnez un arbre de dérivation donnant un typage de $\top$, $K$ et $C_0$

Soit $A\sube E$. Si $t$ est un type tel que $\forall a\in A, \empty \vdash a:t$, on dira que $t$ est le type généralisé de $A$

24. Donnez $t$ un type généralisé de $\{\top, \bot\}$
25. Donnez $t$ un type généralisé de $\{C_n\ |\ n\in\N\}$

## Caractérisation des expressions unitaire
On essaye de montrer que toute les expressions unitaire sont tel que $\Gamma \vdash e:t$.

26. Montrez que si $e:t$ est typé, alors pour tout $a\in e$, $a:t'$ est typé.
27. Montrez que le type d'une expression est invariant par dérivation.
28. Montrez que si $f$ est sous forme normale, alors il existe $\Gamma,t$ tel que toute variable libre de $f$  est une variable dans un couple de $\Gamma$ et $\Gamma \vdash f:t$
29. Montrez que si $e$ est unitaire, alors il existe $\Gamma,t$ tel que $\Gamma \vdash e:t$.
30. Montrez que si $e$ unitaire n'as pas de variable libre, alors $e$ est bien typé.

## Réciproque
On pose $\phi$ injective de $\{\tau,\tau_1,...\}$ dans $V$

31. En étendant $\phi$, donnez $\varphi : T\to E$ injective 
32. Soit $\Gamma\vdash e:t$. Montrez que $e\to^* \phi(t)$ et $e$ unitaire.
> Je pense avoir fait une erreur quand j'ai écrit la correction, mais je ne sais pas d'où elle viens. Je regarderai avec vos propositions. Ne passez pas trop de temps dessus si elle vous semble impossible.
33. En déduire que si $e$ est typé, alors $e$ est unitaire et n'as pas de variable libre.
34. En déduire que $\Delta$ ne possède pas de typage.

REM: En pratique, le lambda calcul typé est assez faible, il ne permet pas de faire de fonctions récursive, de boucle, ou même la fonction $\text{pow}$ comme on a pu le voir dans la partie III.

REM: Le compromis pris par OCaml est de forcer l'existence d'un opérateur point-fixe, dont on ne vérifiera jamais le type. Quand une fonction est définie avec le mot clef `rec`, alors sa "vraie" signature est `val fct : fix -> RESTE`, mais ce premier argument n'est ni affiché, ni vérifié. OCaml ajoute aussi des types par défaut tel que `int`, `string`, `bool` etc...

# Partie V
Ici, l'on suppose $V = \{v_1,...,v_n\}$ fini, comme cela on peut créer le nombre fini de règles $\hat{V}\to v_1|...|v_n$

35. Définir une grammaire hors contexte engendrant $E$
36. Définir une grammaire hors contexte engendrant les expressions sous forme normale. Expliquez votre raisonnement

> To continue. Cette partie sera peut-être dépendante des 2 dernières.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTEzMjM1MzUsLTEyOTk3ODQ5NDldfQ
==
-->