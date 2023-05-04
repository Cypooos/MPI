
# Etude du Lambda Calcul (corrigé)

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
> On suppose par l'absurde que $\Delta(\Delta)\to^ne_n$ avec $e_n$ sous forme normale. Alors on a $\Delta(\Delta)\to e_1\to e_2\to ...\to e_n$, et par récurrence, on a $e_i = \Delta(\Delta)$, donc $e_n =\Delta(\Delta)$ est sous forme normale, or $\Delta(\Delta)\to\Delta(\Delta)$, donc il existe une dérivation, c'est absurde.

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
> NB: $\text{not} = (x\mapsto x(\bot,\top))$ fonctionne aussi.

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
$$Sinon si $b'=\bot$ et $b=\top$ (ce qui conclut tous les cas) :
$$\begin{align*}
\text{and}(\top,\bot) &= (x,y\mapsto \text{if}(x,\text{if}(y,\top,\bot),\bot)(\top,\bot) \\
&\to^2 \text{if}(\top,\text{if}(\bot,\top,\bot),\bot) \\
&\to^* \text{if}(\top,\bot,\bot) \\
&\to^* \bot
\end{align*}$$
>  
> NB: $\text{and} = (x,y\mapsto x(y(\top,\bot),\bot))$ fonctionne aussi. Directement évaluer un booléen par $e,e'$ est ce que fais $\text{if}$, ici on l'a juste directement simplifié.

## Entiers de Church

Pour tout $n\in\N$, on pose :
 - $C_0 = [f,x\mapsto x]$
 - $C_1 = [f,x\mapsto f(x)]$
 - $C_2 = [f,x\mapsto f(f(x))]$
 - $C_n = [f,x\mapsto f^n(x)]$ avec $f^n$ représentant $n$ répétitions de $f$ imbriqué

On appelle $C_n$ l'*entier de Church* associé à $n$.

6. Définir une expression $\text{succ}$ tel que $\text{succ}(C_n)\to^* C_{n+1}$

> On pose $\text{succ} = (C,f,x\mapsto C(f,f(x)))$. On a ainsi:
> $\text{succ}(C_n) \to (f,x\mapsto C_n(f,f(x)))\to^2(f,x\mapsto f^n(f(x))) = (f,x\mapsto f^{n+1}(x)) = C_{n+1}$
> 
> NB: $\text{succ} = (C_n,f,x\mapsto f(C_n(f,x)))$ marche aussi: On aurai
> $\text{succ}(C_n) \to (f,x\mapsto f(C_n(f,x))) \to^2 (f,x\mapsto f(f^n(x))) =  (f,x\mapsto f^{n+1}(x)) = C_{n+1}$

7. Définir une expression $\text{add}$ tel que $\text{add}(C_n,C_m) \to^* C_{n+m}$

> On pose $\text{add} = (C,C' \mapsto C(\text{succ},C'))$
> On a : $\text{add}(C_n,C_m) \to^2 C_n(\text{succ},C_m)\to^2 \text{succ}^n(C_m) \to^* C_{m+n}$
> 
> NB: $\text{add} = (C,C',f,x\mapsto C(f,C'(f,x)))$ marche aussi.

8. Définir une expression $\text{mul}$ tel que $\text{mul}(C_n,C_m) \to^* C_{n\times m}$

> On pose $\text{mul} = (C,C'\mapsto C(\text{add}(C'),C_0))$ 
> On a : $\text{mul}(C_n,C_m) \to^2 C_n(\text{add}(C_m),C_0)\to^2 (\text{add}(C_m))^n(C_0) \to ^* C_{n\times m}$
> Ou l'on peut montrer par récurrence sur $n$ que $(\text{add}(C_m))^n(C_0) \to ^* C_{n\times m}$ :
>  - Initialisation: On a $(\text{add}(C_m))^0(C_0) = C_0= C_{n\times m}$
>  - Hérédité: On a $(\text{add}(C_m))^{n+1}(C_0)=\text{add}(C_m)((\text{add}(C_m))^n(C_0)) \to^*\text{add}(C_m)(C_{n\times m}) \to ^* C_{m+n\times m} = C_{(n+1)\times m}$

On utilisera les opérations $\text{add}$ et $\text{mul}$ pour représenter l'addition et la multiplication entre entiers que l'on représentera sous la forme d'entiers de Church.
On suppose l'opération $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m\ ;\ 0\}}$ a été écrite ; l'écrire est l'objet de la partie II.

## Condition sur les entiers de Church
9. Définir $\text{eq\_0}$ une expression tel que $\text{eq\_0}(C_0)\to^* \top$ et $\forall n>0,\ \text{eq\_0}(C_n)\to^* \bot$ 
 > On pose $\text{eq\_0} = (C\mapsto C(K(\bot),\top))$, et on a :
 >  - pour $C_0$ : $\text{eq\_0}(C_0) \to C_0(K(\bot),\top)\to \top$
 >  - soit $n>0$ : $\text{eq\_0}(C_n) \to C_n(K(\bot),\top)\to (K(\bot))^n(\top)\to^*K(\top)((K(\bot))^{n-1}(\top)) \to \bot$
 
10. Définir $\text{eq}$ une expression tel que :
    * $\text{eq}(C_n,C_m) \to^* \top$ si $n=m$
    * $\text{eq}(C_n,C_m) \to^* \bot$ si $n\neq m$

> On pose $\text{eq} = (C,C'\mapsto \text{and}\Big(\text{eq\_0}(\text{sub}(C,C')),\text{eq\_0}(\text{sub}(C',C))\Big))$
> Soit $n\in\N$, on a
> $$\begin{align*}\text{eq}(C_n,C_n)&\to^* \text{and}\Big(\text{eq\_0}(\text{sub}(C_n,C_n)),\text{eq\_0}(\text{sub}(C_n,C_n))\Big)
\\&\to^*\text{and}\Big(\text{eq\_0}(C_0),\text{eq\_0}(C_0)\Big)
\\&\to^* \text{and}(\top,\top) \\&\to \top\end{align*}$$
> Soit $n<m$, on a :
> $$\begin{align*}\text{eq}(C_n,C_m)&\to^* \text{and}\Big(\text{eq\_0}(\text{sub}(C_n,C_m)),\text{eq\_0}(\text{sub}(C_n,C_m))\Big)
\\&\to^*\text{and}\Big(\text{eq\_0}(C_0),\text{eq\_0}(C_{m-n})\Big)
\\&\to^* \text{and}(\top,\bot) \\&\to \bot\end{align*}$$
> Et pareillement si $m<n$
> NB: Il ne faut pas oublier le $\text{and}$ ! Il est important, car $\text{sub}(C_n,C_m)$ ne marche que pour des $n>m$
 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNzQzMzgwOTldfQ==
-->