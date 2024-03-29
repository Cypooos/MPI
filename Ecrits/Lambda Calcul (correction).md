
# Etude du Lambda Calcul (correction)

Ce sujet introduit la théorie derrière les langages fonctionnels : le lambda calcul.

La partie I introduit le lambda calcul et les booléens.
La partie II étudie la $\beta$-équivalence et la propriété de *Church-Rosser*.
La partie III implémente les entiers de Church et les opérations classiques dessus.
La partie IV introduit le principe d'opérateur point-fixe et la récursivité.
La partie V définie des types aux expressions du lambda calcul.
La partie VI, pour aller plus loin. Certaines parties en font référence.

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


Soit $V$ un ensemble dénombrable infinie de *variables*.
On définit une *expression* inductivement :
 - "$x$" est une expression pour tout $x\in V$
 - "$e_1(e_2)$" est une expression pour tout $e_1,e_2$ deux expressions
 - "$x\mapsto e$" est une expression pour tout $x\in V$ et $e$ une expression

On utilisera des parenthèses pour lever les ambiguïtés de cette grammaire. On note $E$ l'ensemble des expressions. Si $a$ est une expression présente dans $A$, une autre expression, on note cela $a\in A$.

On pourra noter $x_1,x_2,...,x_n\mapsto e$ pour dénoter $x_1\mapsto (x_2\mapsto(...(x_n\mapsto e)...))$
On pourra noter $e(x_1,x_2,...,x_n)$ pour dénoter $e(x_1)(x_2)...(x_n)$
 
Soient $e\in E$ et $x,a\in V\times E$, on définit l'opération de *substitution* $e[x\larr a]$ inductivement :
 - $x[x\larr a] :=a$
  - $u[x\larr a] := u$ pour $u\in V\setminus \{x\}$
  - $e(e')[x\larr a] := e[x\larr a]\Big(e'[x\larr a]\Big)$
  - $(x\mapsto e)[x\larr a] := x\mapsto e$
  - $(u\mapsto e)[x\larr a] := u\mapsto e[x\larr a]$ pour $u\in V\setminus \{x\}$

Informellement, $e[x\larr a]$ est $e$ dans laquelle on a remplacé toutes les occurrences libre de $x$ par $a$.

On dit que $x$ est *libre* dans $e$ si $e \neq e[x\larr x']$ avec $x' \ne x$. Un variable *liée* de $A$ est une variable $x$ non libre avec $x\in A$.

Dans ce sujet, un renommage d'une variable liée ne change pas fondamentalement l'expression. On identifiera donc deux expressions à renommage d'une variable non libre près. 

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
> On a $K(K,I)=K(K)(I)=(y\mapsto (x\mapsto y))(K)(I)\to (x\mapsto K)(I)\to K$, et $K$ est bien sous forme normale.
> On a $I(I)=(x\mapsto x)(I)\to I$, et $I$ est bien sous forme normale.
> On a $K(I,\Delta)=K(I)(\Delta)=(y\mapsto (x\mapsto y))(I)(\Delta)\to(x\mapsto I)(\Delta)\to I$, et $I$ est bien sous forme normale.


2. Montrez que l'expression $\Delta(\Delta)$ ne possède aucun calcul normalisant.

> On a que $\Delta(\Delta)\to\Delta(\Delta)$, qui est la seule dérivation possible.
> On suppose par l'absurde que $\Delta(\Delta)\to^ne_n$ avec $e_n$ sous forme normale. Alors on a $\Delta(\Delta)\to e_1\to e_2\to ...\to e_n$, et par récurrence, on a $e_i = \Delta(\Delta)$, donc $e_n =\Delta(\Delta)$ est sous forme normale, or $\Delta(\Delta)\to\Delta(\Delta)$, donc il existe une dérivation, c'est absurde.

## Graphe des réductions
Soit $e\in E$, on pose $G_e = (S_e,A_e)$ le *graphe orienté des réductions de $e$* avec $S_e = \{x\in E : e \to^* x\}$ et $A_e = \{(x,y)\in S_e^2 : x\to y \}$

3. Donnez le graphe des réductions de $K(I,\Delta(\Delta))$, et de $\Delta((x\mapsto\Delta)(I))$.

> On a le graphe des réductions de $K(I,\Delta(\Delta))$ :
> $$
\begin{CD}
\overbrace{K(I,\Delta(\Delta))}^{\text{Etat bouclant}} @>>> \overbrace{(x\ \mapsto\ I\ )(\Delta(\Delta))}^{\text{Etat bouclant}} @>>> I\\
\end{CD}
$$
> On a le graphe des réductions de $\Delta((x\mapsto\Delta)(I))$ :
> $$
\begin{array}{ccc} 
&\Delta((x\mapsto\Delta)(I))&\lrarr&(x\mapsto\Delta)(I)((x\mapsto\Delta)(I))&\\
&\downarrow&&\downarrow&\\
&\underbrace{\Delta(\Delta)}_{\text{Etat bouclant}}&\larr&(x\mapsto\Delta)(I)(\Delta)&\\
\end{array}
$$

4. Donnez une expression donnant un graphe des réductions infini.

> On pose $\Delta'=(x\mapsto x(x)(x))$.
> On a alors $\Delta'(\Delta') \to \Delta'(\Delta')(\Delta') \to \Delta'(\Delta')(\Delta')(\Delta') \to ...$
> Qui donne donc un $S_{\Delta'(\Delta')}$ infinie, donc un graphe infini (qui est le même graphe que la série de dérivation donnée plus haut)

6. Montrez que si le graphe des réductions de $e$ est acyclique fini, alors $e$ est unitaire.

> Supposons par l'absurde que $e$ n'est pas unitaire. On a alors $(A_n)_n$ un calcul infini. Donc on a un chemin dans le graphe des réductions de longueur infinie. Or les états sur le chemin sont tous deux à deux différents car le graphe est acyclique, donc il y a une infinité d'états, donc le graphe est infini, absurde.

## Booléens
On pose $\top = (x,y\mapsto x)$ et $\bot = (x,y\mapsto y)$. On pose $B=\{\top,\bot\}$
On pose $\text{if} = (b,f_1,f_2\mapsto b(f_1,f_2))$

6. Montrez que, soit $e,e'\in E$, on a $\text{if}(\top,e,e') \to^* e$ et $\text{if}(\bot,e,e') \to^* e'$ 

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

7. Définir une expression $\text{not}$ tel que $\text{not}(\top) \to^* \bot$ et $\text{not}(\bot) \to^* \top$

> On pose $\text{not} = x\mapsto \text{if}(x,\bot,\top)$, et on a bien d'après la question précédente :
>  - $\text{not}(\top) = (x\mapsto \text{if}(x,\bot,\top))(\top)\to \text{if}(\top,\bot,\top) \to^*\bot$
>  - $\text{not}(\bot) = (x\mapsto \text{if}(x,\bot,\top))(\top)\to \text{if}(\bot,\bot,\top) \to^*\top$
> 
> NB: $\text{not} = (x\mapsto x(\bot,\top))$ fonctionne aussi.


8. Définir une expression $\text{and}$ tel que, soit $b,b'\in B$, on ai:
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
> NB: $\text{and} = (x,y\mapsto x(y(\top,\bot),\bot))$ ou $\text{and} = (x,y\mapsto x(y,x))$ fonctionne aussi. Directement évaluer un booléen par $e,e'$ est ce que fais $\text{if}$, ici on l'a juste directement simplifié.
# Partie II: résultats généralistes


## $\beta$-équivalence

On pose $\lrarr$ la fermeture symétrique de $\to$ : on a $x\lrarr y$ si et seulement si $x\to y$ ou $y\to x$

On pose $G = (E,A)$ un graphe orienté infini avec $A = \{(x,y)\in E^2 : x\to^* y \}$
On définie $=_\beta$ une relation d'équivalence telle que $x=_\beta y$ si $x$ et $y$ appartiennent à la même composante faiblement connexe dans $G$

9. Montrez que $a=_\beta b$, si et seulement si il existe $n\in\N$ et $M_1,...,M_n \in E$ tel que $a\lrarr M_1\lrarr...\lrarr M_n\lrarr b$

> Soit $a,b\in E$ tel que $a=_\beta b$.
> Par définition d'une composante faiblement connexe, on a des $a = e_1,...,e_n=b$ tel que pour tout $i\in [\![1;n-1]\!], e_i \to^* e_{i+1}$ ou $e_{i+1} \to^* e_i$.
> Or si $e_i\to^* e_{i+1}$ alors il existe $e_i=e_i^{1},...,e_i^{n_i}=e_{i+1}$ tel que $e_i^{1}\to ... \to e_i^{n_i}$, donc tel que $e_i^{1}\lrarr ... \lrarr e_i^{n_i}$
> Réciproquement, si $e_{i+1}\to^* e_{i}$, on a bien les $e_i^{k}$ qui existe et vérifient la même propriété.
> Finalement, on a $a=e_1^{1}\lrarr e_1^{2}\lrarr ... \lrarr e_1^{n_1}\lrarr e_2^{1} \lrarr ... \lrarr e_n^{n_n}=b$
> La réciproque est beaucoup plus simple : Le chemin nous ai donné par les $M_i$. En effet, pour $i\in [\![1;n-1]\!]$, on a $M_i \lrarr M_{i+1}$ donc soit $M_i \to M_{i+1}$ soit $M_{i+1} \to M_i$, et donc soit $M_i \to^* M_{i+1}$ soit $M_{i+1} \to^* M_i$.
> Donc $M_i$ et $M_{i+1}$ sont bien relié faiblement dans $G$


10. Montrez que $=_\beta$ est une relation d'équivalence sur $E$. 

> On vérifie les différentes propriétés, qui découle immédiatement du chemin dans G ( "$a,b$ sont dans les mêmes composantes faiblement connexe" est bien une relation d'équivalence) :
>  - Symétrie : si $a=_\beta b$, alors on a un chemin $(M_{i\le n})_i$ de $a$ vers $b$. En prenant le chemin $(M_{n-i+1})_i$, on a bien une chemin de $b$ vers $a$
>  - Réflexivité : On a $(a)$ qui est un chemin qui conviens à montrer que $a =_\beta a$.
>   - Transitivité : On suppose que l'on ai $a =_\beta b$ et $b =_\beta c$. Alors on a $a = e_1 \lrarr ... \lrarr e_n = b$ et $b = e'_1 \lrarr ... \lrarr e'_m = c$, donc en concaténant les chemins, on a $a=e_1 \lrarr ... \lrarr e_{n-1} \lrarr e'_1 \lrarr ... \lrarr e'_m = c$ un chemin de $a$ à $c$, donc $a=_\beta c$

 > On peut aussi dire que comme les composantes faiblement connexe de $G$ forme une partition de $E$, on a que $=_\beta$ est la relation d'équivalence qui est associé à cette partition.

## Le théorème de _Church-Rosser_

On dit que une relation $\mathcal{R}$ sur $E$ respecte la propriété du diamant si :
> Soit $t,u,v\in E$, si $t\mathcal{R}u$ et $t\mathcal{R}v$, alors il existe $\omega\in E$ tel que $u\mathcal{R}\omega$ et $v\mathcal{R}\omega$

Le théorème de Church-Rosser assure que la relation $\to^*$ respecte la propriété du diamant.

Pour démontrer cela, on pose $\triangleright$ la réduction parallèle tel que :
- $x\triangleright x$
- $x\mapsto t \triangleright x\mapsto t'$si $t \triangleright t'$
- $t(x)\triangleright t'(x')$ si $t\triangleright t'$ et $x\triangleright x'$
- $(x\mapsto t)(u) \triangleright t'[x\larr u']$ si $t \triangleright t'$ et $u \triangleright u'$


11. Montrez que si $a\to b$, alors $a\triangleright b$.

> Supposons $A\to B$. On choisi $a\in A$ qui soit évalué avec  $\hat a\in B$.
> On a alors $a=(x\mapsto e)(e') \to e[x\larr e']$. On montre $a\triangleright \hat a$ par la quatrième formule :
>  - On a bien $e\triangleright e$ par la première formule
>  - On a bien $e' \triangleright e'$ par la première formule
> 
> Par induction rapide sur les sous-formules de $A$, on aura maintenant $A \triangleright B$: 
> Soit $X$ une sous formule de $A$, avec $X'$ celle qui correspond dans $B$ :
>  - Si $a\not \in X \to X'$, alors $X=X'$ et donc $X\triangleright X'$.
>  - Si $X=a$, alors $X=a\triangleright \hat a= X'$ comme vu précédemment.
>  - Sinon, si $a\in X$, on décompose $X$ et raisonne par induction.
>    - Si $X=u(v)\to u'(v')=X'$, comme $u'\triangleright u'$ et $v' \triangleright v'$, on a $X\triangleright X'$.
>    - Si $X=(x\mapsto e)\to(x\mapsto e')=X'$, comme $e\triangleright e'$, on a $X\triangleright X'$.
> 
> Cela conclu la preuve.
12. Montrez que si $a\triangleright b$, alors $a\to^* b$

> On montre par induction sur les 4 règles de la dérivation parallèle que si $a\triangleright b$ alors $a\to^* b$ :
> - Règle 1, case de base, si $a\triangleright a$ :
>  On a trivialement $a\to^* a$ (calcul vide)
> 
> - Règle 2, si $x\mapsto t \triangleright x\mapsto t'$ avec $t \triangleright t'$:
> Par induction, on a $t\to^* t'$. Donc on a par le même calcul qui passe de $t$ à $t'$:  $(x\mapsto t) \to^* (x'\mapsto t')$
> 
> - Règle 3: si $t(x)\triangleright t'(x')$ avec $t\triangleright t'$ et $x\triangleright x'$ :
> Par induction, on a $t\to^* t'$ et $x\to^* x'$. On a donc le calcul $t(x) \to^* t(x') \to^* t'(x')$
> 
> - Règle 4: si $(x\mapsto t)(u) \triangleright t'[x\larr u']$ avec $t \triangleright t'$ et $u \triangleright u'$.
>  Par induction, on a $t\to^* t'$ et $u\to^* u'$. On pose donc le calcul constitué du calcul de $u$, puis de $t$, puis de l’évaluation :
>  $(x\mapsto t)(u) \to^* (x\mapsto t)(u') \to^* (x\mapsto t')(u') \to t'[x\larr u']$

13. Montrer les règles d'interversion de la substitution, à savoir : soient $t,t',e \in E$ et $x,y\in V$,
Si $x\neq y$, on a $t[x\larr t'][y\larr e] = t[y\larr e][x\larr t'[y\larr e]]$
Si $x=y$, on a $t[x\larr t'][y\larr e] = t[x\larr t'[y\larr e]]$

> Pour le cas $x=y$: on procède par induction sur $t$:
>  - Si $t\in V \setminus\{x\}$, alors on a $t[x\larr t'][y\larr e] = t = t[x\larr t'[y\larr e]]$
>  - Si $t=x$, alors on a $t[x\larr t'][y\larr e] = t'[y\larr e] = t[x\larr t'[y\larr e]]$
>  - Si $t=(x\mapsto e)$, alors $t[x\larr t'][y\larr e] = t = t[x\larr t'[y\larr e]]$
>  - Si $t=(z\mapsto e)$ avec $z\in V \setminus \{ x\}$, on a $t[x\larr t'][y\larr e] = (z\mapsto e[x\larr t'][y\larr e]) = (z\mapsto e[x\larr t'[y\larr e]])) = t[x\larr t'[y\larr e]]$ par induction
>  - Si $t=e_1(e_2)$, alors par induction $t[x\larr t'][y\larr e] = e_1[x\larr t'][y\larr e](e_2[x\larr t'][y\larr e]) = e_1[x\larr t'[y\larr e]](e_1[x\larr t'[y\larr e]]) = t[x\larr t'[y\larr e]]$
> 
> Pour le cas $x\neq y$: on procède aussi par induction sur $t$:
>  - Si $t=x$, alors $t[x\larr t'][y\larr e] = t'[y\larr e] = x[x\larr t'[y\larr e]] = t[y\larr e][x\larr t'[y\larr e]]$
>  - Sinon si $t=y$, alors $t[x\larr t'][y\larr e] = t[y\larr e] = e = t[y\larr e][x\larr t'[y\larr e]]$
>  - Sinon, $t=v\in V\setminus\{x,y\}$, et on a $t[x\larr t'][y\larr e] = t = t[y\larr e][x\larr t'[y\larr e]]$
>  - Sinon, si $t=x\mapsto e$
>  - Sinon, si $t=y\mapsto e$
>  - Sinon, si $t=v\mapsto e$ avec $v\in V\setminus\{x,y\}$
>  - Sinon, si $t=e(e')$
>  TODO : finir cette preuve


14. Donner un $e\in E$ ayant $x$ comme variable libre tel que, si $t\to t'$, on a n'a pas $e[x\larr t] \to e[x\larr t']$ 

> On peut donner $x(x)$ et par exemple $I(I) \to I$ pour $t\to t'$ :
> $(x(x))[x\larr I(I)] = I(I)(I(I))$ et $x(x)[x\larr I] = I(I)$.
> Hors $I(I)(I(I))$ ne se réduit que en 2 étapes à $I(I)$

15. Montrer que, soit $t,t',v,v' \in E$ et $x\in V$, si $t\triangleright  t'$ et $v\triangleright v'$, alors $t[x \larr v] \triangleright t'[x \larr v']$
> Indication : On peut procéder par induction selon la règle obtenue pour avoir $t\triangleright t'$.

> On procède par induction selon la règle obtenue pour avoir $t\triangleright t'$ : 
> - Règle 1, si $t = t'$, alors on procède par induction sur $t$:
>    - Si $t=x$, alors $t[x \larr v] = v \triangleright v' = t'[x \larr v']$
>    - Si $t= (x\mapsto e)$, alors $t[x \larr v] = t\ \triangleright t' = t'[x \larr v']$
>    - Si $t=(y\mapsto e)$ (avec $y\neq x$), alors par induction on a $e[x \larr v] \triangleright (y\mapsto e[x \larr v'])$ on a $t[x \larr v] = (y\mapsto e[x \larr v])\ \triangleright (y\mapsto e[x \larr v']) = t'[x \larr v]$ car 
>    - Si $t=(e_1)(e_2)$, alors $t[x \larr v] = (e_1[x \larr v])(e_2[x \larr v])$ et par hypothèse d'induction, $e_1[x \larr v] \ \triangleright e_1[x \larr v']$ et $e_2[x \larr v] \ \triangleright e_2[x \larr v']$ ce qui montre par la règle 3 que $t[x \larr v]  \ \triangleright t'[x \larr v']$
> - Règle 2, si on a $t = y\mapsto e \triangleright y\mapsto e' = t'$ avec $e \triangleright e'$.
> Dans ce cas, on a par induction que $e[x\larr v] \triangleright e'[x\larr v']$, donc que $t[x \larr v] \triangleright t'[x \larr v']$ par la Règle 2.
> - Règle 3, si on a que $t = e(y)\triangleright e'(y')$ avec  $e\triangleright e'$ et $y\triangleright y'$.
> Dans ce cas, par induction, $e[x \larr v] \triangleright e'[x \larr v']$ et $y[x \larr v] \triangleright y'[x \larr v']$.
> Donc, par la Règle 3, on a que $t[x \larr v] \triangleright t'[x \larr v']$
> - Règle 4, si on a $t = (y\mapsto e)(u) \triangleright e'[y\larr u'] = t'$ avec $e \triangleright e'$ et $u \triangleright u'$.
> Dans ce cas, on a par induction que $e[x\larr v] \triangleright e'[x\larr v']$ et $u[x\larr v] \triangleright u'[x\larr v']$.
> On a donc par la règle 4 que $(y\mapsto e[x\larr v])(u[x\larr v]) \triangleright e'[x\larr v'][y\larr u'[x\larr v']]$.
>   - Si $x \neq y$, alors $t[x\larr v] = (y\mapsto e[x\larr v])(u[x\larr v]) \triangleright e'[x\larr v'][y\larr u'[x\larr v']]=e'[y\larr u'][x\larr v'] = t'[x\larr v']$ (Question 13)
>   - Si $x=y$, alors $t[x\larr v] = (x\mapsto e)(u[x\larr v]) \triangleright e'[x\larr u'[x\larr v']] = e'[y\larr u'][x\larr v'] = t'[x\larr v']$ par la règle 4 et le (Question 13)
> 

16. (*) Montrez le théorème de _Church-Rosser_.

## Autour de Church-Rosser
17. Montrez que si $a\in E$ possède une forme normale, alors celle-ci est unique.

> Soit $a\in E$ tel que $a\to^* \alpha_1$ et $a\to^* \alpha_2$, avec $\alpha_1$ et $\alpha_2$ sous forme normale.
> On a par la propriété du diamant qu'il existe $w$ tel que $\alpha_1 \to^* w$ et $\alpha_2 \to^* w$. 
> Or comme ils sont sous forme normale (pas de dérivation), on a $\alpha_1 = w = \alpha_2$, ce qui conclu la preuve.

> Remarque : On a ici prouvé que quelque-soit notre manière d'évaluer une expression $e$ bien écrite, on tombera toujours sur le même résultat. Autrement dit, le lambda calcul est fondamentalement "déterministe" par rapport à son implémentation.
> Attention, cela suppose que l'on arrive à atteindre la forme normale après un nombre fini d'étapes. Dans le cas de $\text{if}(\top,I,\Delta(\Delta)) \to^* I$, si l'on calcule constamment $\Delta(\Delta)$, on n'atteindra jamais la forme normale $I$, alors qu'elle existe et est unique.

18. Montrez que si $a=_\beta b$, alors il existe $e\in E$  tel que $a\to^* e$ et $b\to^* e$

> On pose $(M_i)_i$ la suite finie dans $E$ tel que $a= M_0 \lrarr M_1 \lrarr ... \lrarr M_n = b$.
> On montre, par récurrence sur $i$ que il existe $e_i\in E$ tel que $a \to^* e_i$ et $M_i\to^* e_i$ :
> Pour $i=0$, $e_i = a$ conviens.
> On suppose que $M_i \to^* e_i$ et que $M_0 \to^* e_i$ :
> - Si $M_{i} \larr M_{i+1}$, alors on a $M_{i+1} \to M_i \to^* e_i$ et donc $e_{i+1}=e_i$ conviens
> - Si $M_i \rarr M_{i+1}$, alors on sait par la propriété du diamant sur $e_i$ et $M_{i+1}$, tout deux généré par $M_i$ qu'il existe $\alpha$ tel que $e_i \to^* \alpha$ et $M_{i+1}\to^* \alpha$.
> On pose $e_{i+1} = \alpha$, et on a bien $M_0 \to^* e_i \to^* e_{i+1}$ et $M_{i+1}\to^* e_{i+1}$ 

19. Soit $f\in E$. Donnez une expression $g$ tel que pour tout $e\in E$ on ai $f(e) =_\beta g(e)$ mais $f \neq_\beta g$
> On peut prendre $g = y \mapsto f(y)$
> On a bien, soit $e\in E$, $g(e) = f(e) =_\beta f(e)$, mais $f \not=_\beta g$ (les deux sont sous forme normale, or s'ils étaient dans la même classe dans $=_\beta$, ils auraient eu la même forme normale)
# Partie III: Entiers et opérations

## Entiers de Church

Pour tout $n\in\N$, on pose :
 - $C_0 = [f,x\mapsto x]$
 - $C_1 = [f,x\mapsto f(x)]$
 - $C_2 = [f,x\mapsto f(f(x))]$
 - $C_n = [f,x\mapsto f^n(x)]$ avec $f^n$ représentant $n$ répétitions de $f$ imbriqué

On appelle $C_n$ l'*entier de Church* associé à $n$.

20. Définir une expression $\text{succ}$ tel que $\text{succ}(C_n)\to^* C_{n+1}$

> On pose $\text{succ} = (C,f,x\mapsto C(f,f(x)))$. On a ainsi:
> $\text{succ}(C_n) \to (f,x\mapsto C_n(f,f(x)))\to^2(f,x\mapsto f^n(f(x))) = (f,x\mapsto f^{n+1}(x)) = C_{n+1}$
> 
> NB: $\text{succ} = (C_n,f,x\mapsto f(C_n(f,x)))$ marche aussi: On aurai
> $\text{succ}(C_n) \to (f,x\mapsto f(C_n(f,x))) \to^2 (f,x\mapsto f(f^n(x))) =  (f,x\mapsto f^{n+1}(x)) = C_{n+1}$

21. Définir une expression $\text{add}$ tel que $\text{add}(C_n,C_m) \to^* C_{n+m}$

> On pose $\text{add} = (C,C' \mapsto C(\text{succ},C'))$
> On a : $\text{add}(C_n,C_m) \to^2 C_n(\text{succ},C_m)\to^2 \text{succ}^n(C_m) \to^* C_{m+n}$
> 
> NB: $\text{add} = (C,C',f,x\mapsto C(f,C'(f,x)))$ marche aussi.

22. Définir une expression $\text{mul}$ tel que $\text{mul}(C_n,C_m) \to^* C_{n\times m}$ 

> On pose $\text{mul} = (C,C'\mapsto C(\text{add}(C'),C_0))$ 
> On a : $\text{mul}(C_n,C_m) \to^2 C_n(\text{add}(C_m),C_0)\to^2 (\text{add}(C_m))^n(C_0) \to ^* C_{n\times m}$
> Ou l'on peut montrer par récurrence sur $n$ que $(\text{add}(C_m))^n(C_0) \to ^* C_{n\times m}$ :
>  - Initialisation: On a $(\text{add}(C_m))^0(C_0) = C_0= C_{n\times m}$
>  - Hérédité: On a $(\text{add}(C_m))^{n+1}(C_0)=\text{add}(C_m)((\text{add}(C_m))^n(C_0)) \to^*\text{add}(C_m)(C_{n\times m}) \to ^* C_{m+n\times m} = C_{(n+1)\times m}$


## Soustraction

L'objectif de cette partie est d'implémenter $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m\ ;\ 0\}}$
On définit :
$$D = (x,y,z \mapsto z(x,y))$$

qui représente un couple $(x,y)$

25. Montrez que $D(e,e')(\top) \to^* e$ et  $D(e,e')(\bot) \to^* e'$.

> On a : $D(e,e')(\top)\to \top(e,e')= (x,y\mapsto x)(e,e') \to^2 e$
> Et aussi : $D(e,e')(\bot)\to \bot(e,e')= (x,y\mapsto y)(e,e') \to^2 e'$

26. Définir $A$ une expression telle que $A(D(e,C_n)) \to^* D(C_n,C_{n+1})$

> On pose $A = (d\mapsto D\Big(d(\bot),\text{succ}(d(\bot))\Big))$
> On a alors : $A(D(e,C_n))\to D\Big(D(e,C_n)(\bot),\text{succ}(D(e,C_n)(\bot))\Big)\to^* D\Big(C_n,\text{succ}(C_n)\Big)\to^* D(C_n,C_{n+1})$

27. (*) Définir $\text{decr}$ telle que $\text{decr}(C_n) \to^* C_{\max\{n-1;0\}}$. On expliquera le raisonnement.

> On $\text{decr} = (C\mapsto C(A,D(C_0,C_0))(\top))$
> L'idée que comme A passe de (x,n) à (n,n+1), en répétant n fois A, on a une fonction qui à (0,0) associe (n-1,n). En récupérant la première composante, on pourra avoir n-1.
> 
> On a ainsi $\text{decr}(C_n) \to C_n(A,D(C_0,C_0))(\top)\to^2 A^n(D(C_0,C_0))(\top)$
> 
> Et on montre que $A^n(D(C_0,C_0)) \to^* D(C_{\max(n-1;0)},C_n)$ par récurrence (pour n>0) :
> - initialisation : pour n=0, on a $D(C_0,C_0) =  D(C_{\max(n-1;0)},C_n)$
> - hérédité : on a $A^{n+1}(D(C_0,C_0)) \to^* A(A^n(D(C_0,C_0))) \to^*A(D(C_{\max(n-1;0)},C_n))\to^* D(C_{\max(n;0)},C_{n+1})$
> 
> Donc $\text{decr}(C_n) \to^* D(C_{\max(n-1;0)},C_n)(\top)\to^*C_{\max(n-1;0)}$


28. Définir $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$

> On pose $\text{sub} = (C,C'\mapsto C(\text{decr},C'))$
> Et on a bien $\text{sub}(C_n,C_m) \to^2C_n(\text{decr},C_m)\to^2\text{decr}^n(C_m)\to^*C_{\max\{n-m;0\}}$
## Conditions sur les entiers de Church
23. Définir $\text{eq\_0}$ une expression tel que $\text{eq\_0}(C_0)\to^* \top$ et $\forall n>0,\ \text{eq\_0}(C_n)\to^* \bot$ 

 > On pose $\text{eq\_0} = (C\mapsto C(K(\bot),\top))$, et on a :
 >  - pour $C_0$ : $\text{eq\_0}(C_0) \to C_0(K(\bot),\top)\to \top$
 >  - soit $n>0$ : $\text{eq\_0}(C_n) \to C_n(K(\bot),\top)\to (K(\bot))^n(\top)\to^*K(\top)((K(\bot))^{n-1}(\top)) \to \bot$
 
24. Définir $\text{eq}$ une expression tel que :
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

# Partie IV: Point-fixe et Récursivité
Le but de cette partie est de pouvoir faire des fonctions récursives.
## L'opérateur Point-fixe

On dit que $\text{fix}$ est un opérateur point-fixe  si il est sous forme normale et que, pour tout $f\in E$, on a :
$$\text{fix}(f) =_\beta f(\text{fix}(f))$$

On admet qu'il en existe (sauf à la question 32).

29. Montrez que si $\text{fix}(f) \to^* f(\text{fix}(f))$, alors $\text{fix}(f)$ n'est pas unitaire.

> On suppose $\text{fix}(f)$ unitaire par l'absurde. On note alors $\text{fix}(f)\to^n e$ avec le plus grand $n$ possible (ils sont bornées). On a alors $\text{fix}(f)\to^p f(\text{fix}(f))\to^n f(e)$ qui est aussi un calcul normalisant de longueur $n+p$ ($p\neq 0$ car $\text{fix}(f)\neq f(\text{fix}(f))$), absurde.


On appellera $e$ un *point fixe* de $f$ si $f(e) =_\beta e$, et un *point fixe fort* de $f$ si $f(e)\to^* e$

30. Montrez que tout $f\in E$ admet un point fixe.

> On pose $e=\text{fix}(f)$ et on a $f(e) = f(\text{fix}(f)) = _\beta \text{fix}(f) = e$

31. Montrez que si pour tout $e\in E$, on a que $f(e)$ admet une forme normale, alors $f$ admet un point fixe fort.

> Par la question 18, on a que $f(\text{fix}(f)) \to^* e$ et $\text{fix}(f) \to^* e$. Or on peut trouver une forme normale $e'$ de $f(\text{fix}(f))$ par hypothèse, donc on a $e\to^* e'$.
> On a donc $f(\text{fix}(f))\to^* f(e) \to^* f(e')$ mais aussi $f(\text{fix}(f))\to^* e \to^* e'$.
> En appliquant la propriété du diamant sur $f(e')$ et $e'$ généré par $f(\text{fix}(f))$, on a que $f(e') \to^* p$ et $e' \to^* p$.
> Comme $e'$ sous forme normale, on a $p=e'$. Donc $f(e') \to^* e'$.

32. (*) Donnez une expression $Y$ point-fixe.

> Bravo si vous l'avez réussie ! Vraiment pas facile.
> On peut donner $Y = (f\mapsto\Big((x\mapsto f(x(x)))(x\mapsto f(x(x)))\Big))$

## Récursivité
On considère ici $F$ de la forme $F=(f,x\mapsto e)$ une fonction.

33. Justifiez sans démonstration que, pour tout $\alpha$ sous forme normale, $\forall e\in E$,
$$\text{fix}(F)(e) \to^* \alpha \implies\exist n_r,\ \underbrace{F(F(...(F)...))}_{n_r\text{ fois}}(e)\to^*\alpha$$


Si $\alpha$ est sous forme normale, on appellera le plus petit $n_r$ le *nombre d'appels récursif* de $F(x)$.

> TODO
## Un exemple
On définit :
$$
\text{fact\_rec} = (f,x\mapsto \text{if}(\text{eq\_0}(x))(C_1)(\text{mul}(x,f(\text{sub}(x,1)))))
$$
Et on pose $\text{fact} = \Theta(\text{fact\_rect})$

34. Montrez que $\text{fact}(C_n) \to^* C_{n!}$

> On le montre par récurrence: 
> Initialisation: On a $\text{fact}(C_0)\to \text{if}((\text{eq\_0}(C_0))(C_1)(\text{mul}(C_0,\text{fact}(\text{sub}(C_0,1)))) \to^*C_1$
> heredité : On suppose que $\text{fact}(C_n) \to^* C_{n!}$. On a alors
>  $$
\begin{align*}
\text{fact}(C_{n+1}) &\to^*  \text{if\_0}(C_{n+1})(C_1)(\text{mul}(C_{n+1},\text{fact}(\text{sub}(C_{n+1},1)))) \\
&\to^* \text{mul}(C_{n+1},\text{fact}(\text{sub}(C_{n+1},1))) \\
&\to^* \text{mul}(C_{n+1},\text{fact}(C_{n})) \\
&\to^* \text{mul}(C_{n+1},C_{n!}) \\
&\to^* C_{(n+1)!} \\
\end{align*}
$$

35. (*) Donnez une expression $\text{pow\_rec}$ tel que, soit $n,m\in\N$, on ai $\Theta(\text{pow\_rec})(C_n,C_m) \to^* C_{n^m}$ avec $n_r = O(\log_2(m))$. On n’utilisera pas d'opérateur point fixe. *(On posera ici que $0^0 = 1$)*
> On fait de l'exponentiation rapide :
> On pose $\text{is\_even} = (C\mapsto C(\text{not},\top))$
> On pose $\text{div\_2} = (C\mapsto C(x\mapsto \text{if\_eq}(\text{mul}(x,C_2),C)(x)(\text{sub}(x,1) )(C))$
> On pose $\text{div\_2\_i} = (C\mapsto C(x\mapsto \text{if\_eq}(\text{mul}(x,C_2),C)(x)(\text{sub}(x,1) )(\text{sub}(C,1)))$ (qui fait la division entière d'un nombre impaire)
> On pose $$\text{pow\_rec} = (f,x,y\mapsto \text{if}(\text{eq\_0}(y))(C_1)\Big(\text{if}(\text{is\_even}(y))\\(\text{mul}(f(x,\text{div\_2}(y)),f(x,\text{div\_2}(y))))\\(\text{mul}(x,\text{mul}(f(x,\text{div\_2\_i}(y)),f(x,\text{div\_2\_i}(y)))))\Big))$$
> On montre que $\text{is\_even}(C_{2n}) \to^* \top$ et $\text{is\_even}(C_{2n+1 }) \to^* \bot$, que
> $\text{div\_2}(C_{2n})\to^*C_n$ et $\text{div\_2\_i}(C_{2n+1})\to C_n$

# Partie V: Types (partie fausse)
Cette partie s'intéresse au lambda calcul typé, elle cherche à imposer des règles telle que on obtienne un caractérisation des expressions unitaire.

On pose $T$ tel que $\{\tau,\tau_1,\tau_2,...\} \sub T$ et pour tout $t,t'\in T$, on a $(t\to t')\in T$. On appelle $\tau,\tau_1,\tau_2,...$ les *types par défault*.

Un *contexte de type*, dénoté par $\Gamma$, est un sous-ensemble de $X\times T$.
Un *jugement de type* est un triplet $\Gamma \vdash x: t$ tel que on ai les règles d'inférences suivantes :

Axiome, pour $(x,t) \in \Gamma$ :
$$
\frac{}{\Gamma \vdash x: t}\tiny\text{(ax)}\\
$$
Evaluation :
$$
\frac{\Gamma_0 \vdash f: t\to t',\qquad \Gamma_1 \vdash x: t}{\Gamma_0\cup\Gamma_1 \vdash f(x): t'}\tiny\text{(ev)}
$$
Abstraction :
$$
\frac{\Gamma\ \vdash x': t'}{\Gamma\ \setminus \{(x,t)\} \vdash x\mapsto x': t\to t'}\tiny\text{(ab)}
$$

On dit que $t$ est un *typage* de $x$ si $\empty \vdash x:t$.
Par exemple, ce qui suit est un arbre de dérivation montrant que $\tau\to\tau$ est un typage de $I$ :
$$
\cfrac
{}
{\cfrac{
	\{(x,\tau)\} \vdash x: \tau}{
		\empty \vdash x\mapsto x : \tau\to \tau
	}\tiny\text{(ab)}
}\tiny\text{(ax)}\\
$$

 On n'hésitera pas a ajouter des parenthèses pour ce faire comprendre : par défaut, les flèches sont une opération de droite à gauche, ainsi, $\tau\to\tau\to\tau = \tau\to(\tau\to\tau)$
On notera $e:t$ pour dire qu'une expression $e$ à un typage $t$.
Si $t$ un type est présent dans $t'$ un autre type, on notera cela $t\in t'$.

## Typage de groupe d'expressions

36. Donner un arbre de dérivation donnant un typage de $\top$ et $C_1$
> Pour $\top$ :
$$
\cfrac {}{\cfrac{
	\{(x,\tau)\} \vdash x: \tau}{\cfrac{
	\{(x,\tau)\} \vdash y\mapsto x : \tau' \to \tau}{
	\empty \vdash x,y\mapsto x : \tau \to \tau' \to \tau
}\tiny\text{(ab)}
}\tiny\text{(ab)}
}\tiny\text{(ax)}\\
$$
> Pour $C_1$ :
$$
\cfrac {
	\cfrac {
		\cfrac {
			\cfrac {}{\{(x:\tau)\}\vdash x : \tau} 
			\qquad 
			\normalsize\cfrac {}{\{(f:\tau\to \tau')\}\vdash f : \tau\to\tau'} \tiny\text{(ax)}
		}
		{\{(x,\tau),(f,\tau\to\tau')\} \vdash f(x) :\tau'}   \tiny\text{(ev)}
	}
	{\{(f:\tau\to\tau')\} \vdash x\mapsto f(x) :\tau \to \tau'}   \tiny\text{(ab)}
}
{\empty \vdash f,x\mapsto f(x) : (\tau \to \tau') \to\tau \to \tau'}   \tiny\text{(ab)}
$$

Soit $A\sube E$. Si $t$ est un type tel que $\forall a\in A, \empty \vdash a:t$, on dira que $t$ est le type généralisé de $A$.

37. Donner $t$ un type généralisé de $\{\top, \bot\}$

> On a $\tau \to \tau \to \tau$

38. Donner $t$ un type généralisé de $\{C_n\ |\ n\in\N\}$

> On a $(\tau\to\tau) \to \tau \to \tau$

## Caractérisation des expressions unitaire sans variable libre

Le but de cette partie est de montrer que tout les expressions unitaire sans variable libre sont typé.

> Les questions arriveront....

## Réciproque

> Les questions arriveront....

# VI Pour aller plus loin

1. Donner un opérateur point fixe $\Theta$ tel que $\text{fix}(f) \to^* f(\text{fix}(f))$

> On a $\Theta = (f,x\mapsto (x (f(f,x))))(f,x\mapsto (x (f(f,x))))$, l'opérateur de point fixe de Turing.


2. Montrer que si pour tout $e\in E$, on a que $f(e)$ admet une forme normale, alors $f$ est constante, c'est à dire que il existe $\omega \in E$ tel que $x\not \in \omega$ et $f =_\beta (x\mapsto \omega)$

> $f$ admet une forme normale $f'$
> Si $f' \neq x\mapsto e$, alors $e$ est sous forme normale et $f(\Delta(\Delta))$ n'est pas normalisable (le seul calcul est $f(\Delta(\Delta))\to f(\Delta(\Delta)) \to ...$), donc $f(e)$ n'admet pas de forme normal pour tout $e$, absurde
> Sinon, on montre que $x\not\in e$ par l'absurde, mais je ne sais pas le finir.

2. On cherche à calculer la forme normale de $f(e)$, pour cela on met d'abord l'argument $e$ sous forme normale inductivement avant de faire l'évaluation. Comment changer $Y$ tel que $\text{fact}(C_1)$ termine ? 

> On peut utiliser $Y = (f\mapsto\Big((x\mapsto f(\mu \mapsto x(x)(\mu)))(x\mapsto f(\mu \mapsto x(x)(\mu)))\Big))$
> 
3. Faire la preuve de la question 33 avec l’opérateur point fixe $\Theta$

> Aucune idée
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg4MTY0MDc3LDI0ODA5ODUsMjA5MDcxMz
EzNiwtMTA5MjYwOTY5NCwyMDg0NDk1NDQwLC03NDI4MTY4NDQs
MjA1MTU0NDk3NCwxMDc3MTAwODY4LDE5NTE0NjY0NjYsLTg3OT
EwMTM5MCwtMTI2NDY1MDc4OSwtMTgxMDAyMjI2MSw2NDI0Njkw
NywzNDYzMTc0NDEsMTgxNjIyODg0NiwtMTM1ODQ5NDIwNiwtMT
E1NzU0NDM1MCwxNDYzMDE3ODE2LC03NDE1ODQxNTIsLTE1MTQx
NjI2OTFdfQ==
-->