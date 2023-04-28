# Etude du Lambda Calcul

Ce sujet est difficile et long, et balaye les chapitres de Logique, Grammaire, Graphes.

Ce sujet introduit la théorie derrière les langages fonctionnel : le lambda calcul.

La partie I propose une implémentation d'objets classique en lambda calcul.
La partie II propose une implémentation de la soustraction.
La partie III s'intéresse à la récursivité, elle est plus théorique.
La partie IV porte sur des expressions typées (logique).
>La partie V s'intéresse à la création de grammaires générant des expressions.
La partie VI à pour but de démontrer le _Théorème de Church-Rosser_ en utilisant des graphes.
Elles sont en cours d'écriture.

Toutes les parties sont dépendante de la partie 1, mais sont indépendantes entre elles.

Seul la question 31 est tiroir à la question 32.

Les questions plus difficile sont préambulées d'une étoile (*).
On pourra admettre une question pour passer à la suivante.
Il n'est pas fait pour être réalisé en 4h ; il sera difficile même en le faisant en 6 heures.

# Définitions

> Soit $\Sigma$ un ensemble de *lettres*. On dis que $\omega=\omega_1...\omega_n$ est un *mot* s'il est une suite finie de lettre. On note $\varepsilon$ le mot vide.
 Pour $\omega$ un mot, on note $|\omega|$ sa longueur et pour $\alpha\in\Sigma$, on note $|\omega|_\alpha$ le nombre d'occurrences de $\alpha$ dans $\omega$.
 Soit $n\in\N$, on note $\Sigma^n$ l'ensemble des mots de $\Sigma$ à $n$ lettres. On note $\Sigma^* = \cup_{n\in\N}\Sigma^n$
On appelle *langage* un ensemble de mots.

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
On appelle *dérivation* $A\to A'$si il existe $a\in A$ évaluable, avec $A'$ qui est $A$ ou l'on a remplacé $a$ par son évaluation. On dit que $A$ est sous forme normale si $A$ n'est pas dérivable.

On appelle un calcul de $A$ une série de dérivations finie $A\to A_1 \to ... \to A_n$. On note cela $A\to^n A_n$ ou $A\to^* A_n$. Si $A_n$ est sous forme normale, on appelle cela un calcul normalisant.
On admet le _Théorème de Church-Rosser_ dans toute les parties sauf la VI: si $A$ est normalisable, alors sa forme normale est unique.
Si il existe un $e\in E$ sous forme normale tel que $A\to^n e$ avec $n$ borné, on dit que $A$ est unitaire. *(Rem: Dans la littérature, le terme de "fortement normalisable" est plutôt employé.)*

On définit les expressions suivantes :
 - $I = (x\mapsto x)$
 - $K =  (y\mapsto (x\mapsto y)) = (y,x\mapsto y)$
 - $\Delta = (x\mapsto x(x))$

# Partie I: Objets classiques

## Préliminaires
1. Donnez un calcul normalisant de $K(K,I)$, de $I(I)$, de $K(I,\Delta)$

> On a $K(K,I)=K(K)(I)=(y\mapsto (x\mapsto y))(K)(I)\to (x\mapsto K)(I)\to K$, et $K$ est bien sous forme normale.
> On a $I(I)=(x\mapsto x)(I)\to I$, et $I$ est bien sous forme normale.
> On a $K(I,\Delta)=K(I)(\Delta)=(y\mapsto (x\mapsto y))(I)(\Delta)\to(x\mapsto I)(\Delta)\to I$, et $I$ est bien sous forme normale.

3. Montrez que l'expression $\Delta(\Delta)$ ne possède aucun calcul normalisant.

> On a que $\Delta(\Delta)\to\Delta(\Delta)$, qui est la seule dérivation possible.
> On suppose par l'absurde que $\Delta(\Delta)\to^ne_n$ avec e sous forme normale. Alors on a $\Delta(\Delta)\to e_1\to e_2\to ...\to e_n$, et par récurrence, on a $e_i = \Delta(\Delta)$, donc $e_n =\Delta(\Delta)$ est sous forme normale, or $\Delta(\Delta)\to\Delta(\Delta)$, donc il existe une dérivation, c'est absurde.

On s'intéresse maintenant à la création de différents objets de base.
## Booléens
On pose $\top = (x,y\mapsto x)$ et $\bot = (x,y\mapsto y)$. On pose $B=\{\top,\bot\}$
On pose $\text{if} = (b,f_1,f_2\mapsto b(f_1,f_2))$

3. Montrez que, soit $e,e'\in E$, on a $\text{if}(\top,e,e') \to^* e$ et $\text{if}(\bot,e,e') \to^* e'$

>On a:
$$\begin{align*}\text{if}(\top,e,e')&=\text{if}(\top)(e)(e') \\
&= (b,f_1,f_2\mapsto b(f_1,f_2))(\top)(e)(e')\\
&\to (f_1,f_2\mapsto \top(f_1,f_2))(e)(e')\\
&\to (f_2\mapsto \top(e,f_2))(e')\\
&\to\top(e,e')\\
&= (x,y\mapsto x)(e,e')\\
&\to (y\mapsto e)(e')\\
&\to e\\
\end{align*}$$
> De même :
$$\begin{align*}\text{if}(\bot,e,e')&=(b,f_1,f_2\mapsto b(f_1,f_2))(\bot)(e)(e')\\
&\to^3\bot(e,e')\\
&= (x,y\mapsto y)(e,e')\\
&\to (y\mapsto y)(e')\\
&\to e'\\
\end{align*}$$


4. Définir une expression $\text{not}$ tel que $\text{not}(\top) \to^* \bot$ et $\text{not}(\bot) \to^* \top$

> On pose $\text{not} = x\mapsto \text{if}(x,\bot,\top)$, et on a bien d'après la question précédente :
>  - $\text{not}(\top) = (x\mapsto \text{if}(x,\bot,\top))(\top)\to \text{if}(\top,\bot,\top) \to^*\bot$
>  - $\text{not}(\bot) = (x\mapsto \text{if}(x,\bot,\top))(\top)\to \text{if}(\bot,\bot,\top) \to^*\top$
> 
> NB: $\text{not} = (x\mapsto x(\bot,\top))$ fonctionne aussi

6. Définir une expression $\text{and}$ tel que, soit $b,b'\in B$, on ai:
   * $\text{and}(b,b') \to^* \top$  si $b=b'=\top$
   * $\text{and}(b,b') \to^* \bot$  sinon

> On pose $\text{and} = (x,y\mapsto \text{if}(x,\text{if}(y,\top,\bot),\bot)$, et on a :
$$\begin{align*}
\text{and}(\top,\top) &= (x,y\mapsto \text{if}(x,\text{if}(y,\top,\bot),\bot)(\top,\top) \\
&\to^2 \text{if}(\top,\text{if}(\top,\top,\bot),\bot) \\
&\to^* \text{if}(\top,\top,\bot) \\
&\to^* \top
\end{align*}$$Si $b=\bot$ :
$$\begin{align*}
\text{and}(\bot,b') &= (x,y\mapsto \text{if}(x,\text{if}(y,\top,\bot),\bot)(\bot,\top) \\
&\to^2 \text{if}(\bot,\text{if}(b',\top,\bot),\bot) \\
&\to^* \bot
\end{align*}
$$Sinon si $b'=\bot$ et $b=\top$ (ce qui conclu tout les cas) :
$$\begin{align*}
\text{and}(\top,\bot) &= (x,y\mapsto \text{if}(x,\text{if}(y,\top,\bot),\bot)(\top,\bot) \\
&\to^2 \text{if}(\top,\text{if}(\bot,\top,\bot),\bot) \\
&\to^* \text{if}(\top,\bot,\bot) \\
&\to^* \bot
\end{align*}$$
>  
> NB: $\text{and} = (x,y\mapsto x(y(\top,\bot),\bot))$ fonctionne aussi. directement évaluer un booléen par $e,e'$ est ce que fais $\text{if}$

## Entiers de Church

Pour tout $n\in\N$, on pose :
 - $C_0 = [f,x\mapsto x]$
 - $C_1 = [f,x\mapsto f(x)]$
 - $C_2 = [f,x\mapsto f(f(x))]$
 - $C_n = [f,x\mapsto f^n(x)]$ avec $f^n$ représentant $n$ répétitions de $f$ imbriqué

On appelle $C_n$ l'*entier de Church* associé à $n$.

6. Définir une expression $\text{succ}$ tel que $\text{succ}(C_n)\to^* C_{n+1}$

> On pose $\text{succ} = (C_n,f,x\mapsto C_n(f,f(x)))$. On a ainsi:
> $$
> NB: $\text{succ} = (C_n,f,x\mapsto f(C_n(f,x)))$ marche aussi: On aurai $\text{succ}(C_n) = (f,x\mapsto f(C_n(f,x))) \to (f,x\mapsto f(f^n(x))) = C_{n+1}$

7. Définir une expression $\text{add}$ tel que $\text{add}(C_n,C_m) \to^* C_{n+m}$
9. Définir une expression $\text{mul}$ tel que $\text{mul}(C_n,C_m) \to^* C_{n\times m}$

On utilisera les opérations $\text{add}$ et $\text{mul}$ pour représenter l'addition et la multiplication entre entiers que l'on représentera sous la forme d'entiers de Church.
On suppose l'opération $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m\ ;\ 0\}}$ a été écrite ; l'écrire est l'objet de la partie II.

## Condition sur les entiers de Church
9. Définir $\text{eq\_0}$ une expression tel que $\text{eq\_0}(C_0)\to^* \top$ et $\forall n>0,\ \text{eq\_0}(C_n)\to^* \bot$ 
10. Définir $\text{eq}$ une expression tel que :
    * $\text{eq}(C_n,C_m) \to^* \top$ si $n=m$
    * $\text{eq}(C_n,C_m) \to^* \bot$ si $n\neq m$

# Partie II: Soustraction
L'objectif de cette partie est d'implémenter $\text{sub}$ définie plus haut.
On définit :
$$D = (x,y,z \mapsto z(x,y))$$

qui représente un couple $(x,y)$

11. Montrez que $D(e,e')(\top) \to^* e$ et  $D(e,e')(\bot) \to^* e'$.
12. Définir $A$ une expression telle que $A(D(e,C_n)) \to^* D(C_n,C_{n+1}))$
13. (*) Définir $\text{decr}$ telle que $\text{decr}(C_n) \to^* C_{\max\{n-1;0\}}$. On expliquera le raisonnement.
14. Définir $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$ 

# Partie III: Récursivité
Le but de cette partie est de pouvoir faire des fonctions récursives.
## L'opérateur Point-fixe

On dit que $\text{fix}$ est un opérateur point-fixe si, pour tout $f\in E$, on a :
$$\text{fix}(f) \to f(\text{fix}(f))$$

15. Montrez que $\text{fix}(f)$ n'est pas unitaire.

On appellera $e$ un point fixe de $f$ si $e=f(e)$

16. Montrez que si $\exist!e\in E,\ \text{fix}(f)\to^* e$, alors $f$ admet un point fixe.
17. Donnez une expression $f$ telle que $\exist!e\in E,\ \text{fix}(f)\to^* e$. Quel est son point fixe ?
18. (*) Donnez une expression $\Theta$ qui est un opérateur point-fixe.

## Récursivité
On considère ici $F$ de la forme $F=(f,x\mapsto e)$ une fonction récursive, c'est à dire que $F$ sera appelé constamment avec $F$ comme premier argument.

19. Montrez que, $\forall x\in E$,
$$\text{fix}(F)(x) \to^* \alpha \implies\exist n_r,\ \underbrace{F(F(...(F)...))}_{n_r\text{ fois}}(x)\to^*\alpha$$

Si $\alpha$ est sous forme normale, on appellera le plus petit $n_r$ le *nombre d'appels récursif* de $F$.

## Quelques exemples
On définit :
$$
\text{fact\_rec} = (f,x\mapsto \text{if0}(x)(C_1)(\text{mul}(x,f(\text{sub}(x,1)))))
$$
Et on pose $\text{fact} = \Theta(\text{fact\_rect})$

20. Montrez que $\text{fact}(C_n) \to^* C_{n!}$
21. Donnez une expression $\text{pow}$ tel que, soit $n,m\in\N$, on ai $\text{pow}(C_n,C_m) \to^* C_{n^m}$ avec $n_r = O(\log_2(m))$

# Partie IV: Types
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

26. Montrez que si $e:t$ est typé, alors pour tout $a\in e$, $a:t'$ est typé et $t'\in t$.
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

REM: Le compromis pris par ocaml est de forcer l'existence d'un opérateur point-fixe, dont on ne vérifiera jamais le type. Quand une fonction est définie avec le mot clef `rec`, alors sa "vraie" signature est `val fct : fix -> RESTE`, mais ce premier argument n'est ni affiché, ni vérifié. Ocaml ajoute aussi des types par défaut tel que `int`, `string`, `bool` etc...

# Partie V
Ici, l'on suppose $V = \{v_1,...,v_n\}$ fini, comme cela on peut créer le nombre fini de règles $\hat{V}\to v_1|...|v_n$

35. Définir une grammaire hors contexte engendrant $E$
36. Définir une grammaire hors contexte engendrant les expressions sous forme normale. Expliquez votre raisonnement
> To continue. Cette partie sera peut-être dépendante des 2 dernières.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjA2NjA3NDQ1XX0=
-->