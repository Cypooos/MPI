# Etude du Lambda Calcul

Ce sujet difficile introduit la théorie derrière les langages fonctionnel : le lambda calcul.

La partie I introduit le lambda calcul et les booléens.
La partie II étudie la $\beta$-équivalence et la propriété de Church Rosser.
La partie III implémente les entiers de church et les opérations classiques dessus.
La partie IV introduit le principe d'opérateur point-fixe et la récursivité.
La partie V définie des types aux expressions du lambda calcul.
La partie VI est en cours d'écriture, et portera sur des liens avec les grammaires.

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

# Partie I: Introduction

## Préliminaires
1. Donnez un calcul normalisant de $K(K,I)$, de $I(I)$, de $K(I,\Delta)$

> On a $K(K,I)=K(K)(I)=(y\mapsto (x\mapsto y))(K)(I)\to (x\mapsto K)(I)\to K$, et $K$ est bien sous forme normale.
> On a $I(I)=(x\mapsto x)(I)\to I$, et $I$ est bien sous forme normale.
> On a $K(I,\Delta)=K(I)(\Delta)=(y\mapsto (x\mapsto y))(I)(\Delta)\to(x\mapsto I)(\Delta)\to I$, et $I$ est bien sous forme normale.


2. Montrez que l'expression $\Delta(\Delta)$ ne possède aucun calcul normalisant.

> On a que $\Delta(\Delta)\to\Delta(\Delta)$, qui est la seule dérivation possible.
> On suppose par l'absurde que $\Delta(\Delta)\to^ne_n$ avec $e_n$ sous forme normale. Alors on a $\Delta(\Delta)\to e_1\to e_2\to ...\to e_n$, et par récurrence, on a $e_i = \Delta(\Delta)$, donc $e_n =\Delta(\Delta)$ est sous forme normale, or $\Delta(\Delta)\to\Delta(\Delta)$, donc il existe une dérivation, c'est absurde.

## Graphe des réductions
Soit $e\in E$, on pose $G_e = (S_e,A_e)$ le *graphe des réductions de $e$* avec $S_e = \{x\in E : e \to^* x\}$ et $A_e = \{(x,y)\in S_e^2 : x\to y \}$

3. Donnez le graphe des réductions de $I(I(I))$, et de $K(I,\Delta(\Delta))$.

> On a le graphe des réductions de $I(I(I))$ :
> $$
\begin{CD}
I(I(I)) @>>> I(I) @>>> I\\
\end{CD}
> $$
> On a le graphe des réductions de $K(I,\Delta(\Delta))$ :
> $$
\begin{CD}
\overbrace{K(I,\Delta(\Delta))}^{\text{Etat bouclant}} @>>> \overbrace{(x\ \mapsto\ I\ )(\Delta(\Delta))}^{\text{Etat bouclant}} @>>> I\\
\end{CD}
$$

4. Donnez une expression donnant un graphe des réductions infini.

> On pose $\Delta'=(x\mapsto x(x)(x))$.
> On a alors $\Delta'(\Delta') \to \Delta'(\Delta')(\Delta') \to \Delta'(\Delta')(\Delta')(\Delta') \to ...$
> Qui donne donc un $S_{\Delta'(\Delta')}$ infinie, donc un graphe fini (qui est le même graphe que la série de dérivation donnée plus haut)

6. Montrez que si le graphe des réductions de $e$ est acyclique fini, alors $e$ est unitaire.

> Tout les calculs partant de $e$ sont fini, et de longueur inférieur à la profondeur de l'arbre si on l'enracine en $e$.
> Supposons par l'absurde que $e$ n'est pas unitaire. On a alors $(A_n)_n$ un calcul infini. Donc on a un chemin dans le graphe des réduction de longueur infinie. Or les états sur le chemin sont tous deux à deux différents car le graphe est acyclique, donc il y a une infinité d'états, donc le graphe est infini, absurde.

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
> NB: $\text{and} = (x,y\mapsto x(y(\top,\bot),\bot))$ fonctionne aussi. Directement évaluer un booléen par $e,e'$ est ce que fais $\text{if}$, ici on l'a juste directement simplifié.
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


10. Montrez que $=_\beta$ est une relation d'équivalence sur E. 

> On vérifie les différentes propriétés, qui découle immédiatement du chemin dans G ( "$a,b$ sont dans les même composante faiblement connexe" est bien une relation d'équivalence) :
>  - Symétrie : si $a=_\beta b$, alors on a un chemin $(M_{i\le n})_i$ de $a$ vers $b$. En prenant le chemin $(M_{n-i+1})_i$, on a bien une chemin de $b$ vers $a$
>  - Réflexivité : le chemin vide conviens.
>   - Transitivité : On concatène les chemins.

 

## Le théorème de _Church-Rosser_

On dit que une relation $\mathcal{R}$ sur $E$ respecte la propriété du diamant si :
> Soit $t,u,v\in E$, si $t\mathcal{R}u$ et $t\mathcal{R}v$, alors il existe $\omega\in E$ tel que $u\mathcal{R}\omega$ et $v\mathcal{R}\omega$

Le théorème de Church-Rosser assure que la relation $\to^*$ respecte la propriété du diamant.

Pour démontrer cela, on pose $\triangleright$ la réduction parallèle tel que :
- $x\triangleright x$
- $x\mapsto t \triangleright x'\mapsto t'$ si $x \triangleright x'$ et $t \triangleright t'$
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

> TODO : le reste de cette section.

13. Montrez que, soit $t,t',v,v' \in E$ et $x\in V$, si $t\triangleright  t'$ et $v\triangleright v'$, alors $t[x \larr v] \triangleright t'[x \larr v']$
> Indication : Procédez par induction sur la forme de $t$
14. Montrez que $\triangleright$ respecte la *propriété du diamant*.
15. En déduire le théorème de *Church-Rosser*.

## Autour de Church-Rosser
16. Montrez que si $a\in E$ possède une forme normale, alors celle-ci est unique.

> Soit $a\in E$ tel que $a\to^* \alpha_1$ et $a\to^* \alpha_2$, avec $\alpha_1$ et $\alpha_2$ sous forme normale.
> On a par la propriété du diamant qu'il existe $w$ tel que $\alpha_1 \to^* w$ et $\alpha_2 \to^* w$. 
> Or comme ils sont sous forme normale (pas de dérivation), on a $\alpha_1 = w = \alpha_2$, ce qui conclu la preuve.

> Remarque : On a ici prouvé que quelque-soit notre manière d'évaluer une expression $e$ bien écrite, on tombera toujours sur le même résultat. Autrement dit, le lambda calcul est fondamentalement "déterministe" par rapport à son implémentation.
> Attention, cela suppose que l'on arrive à atteindre la forme normale après un nombre fini d'étapes. Dans le cas de $\text{if}(\top,I,\Delta(\Delta)) \to^* I$, si l'on calcule constamment $\Delta(\Delta)$, on n'atteindra jamais la forme normale $I$, alors qu'elle existe et est unique.

17. En déduire que tout graphe des réductions de $e$ possède un plus petit et un plus grand élément pour la relation $\to^*$. 

> Le plus petit sera l'unique forme normale $\alpha$, le plus grand sera $e$ : Soit $x \in S_e$ :
>  - On a par définition de $S_e$ que $e \to^* x$ (maximalité de $e$)
>  - On a que $x\to^* \alpha$ par la propriété du diamant appliqué à $\alpha,x$ : On a un $w$ tel que  

18. Montrez que si $a=_\beta b$, alors il existe $e\in E$ sous forme normale tel que $a\to^* e$ et $b\to^* e$


# Partie III: Entiers et opérations

## Entiers de Church

Pour tout $n\in\N$, on pose :
 - $C_0 = [f,x\mapsto x]$
 - $C_1 = [f,x\mapsto f(x)]$
 - $C_2 = [f,x\mapsto f(f(x))]$
 - $C_n = [f,x\mapsto f^n(x)]$ avec $f^n$ représentant $n$ répétitions de $f$ imbriqué

On appelle $C_n$ l'*entier de Church* associé à $n$.

19. Définir une expression $\text{succ}$ tel que $\text{succ}(C_n)\to^* C_{n+1}$
20. Définir une expression $\text{add}$ tel que $\text{add}(C_n,C_m) \to^* C_{n+m}$
21. Définir une expression $\text{mul}$ tel que $\text{mul}(C_n,C_m) \to^* C_{n\times m}$ 


## Conditions sur les entiers de Church
22. Définir $\text{eq\_0}$ une expression tel que $\text{eq\_0}(C_0)\to^* \top$ et $\forall n>0,\ \text{eq\_0}(C_n)\to^* \bot$ 
23. Définir $\text{eq}$ une expression tel que :
    * $\text{eq}(C_n,C_m) \to^* \top$ si $n=m$
    * $\text{eq}(C_n,C_m) \to^* \bot$ si $n\neq m$

## Soustraction

L'objectif de cette partie est d'implémenter $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m\ ;\ 0\}}$
On définit :
$$D = (x,y,z \mapsto z(x,y))$$

qui représente un couple $(x,y)$

24. Montrez que $D(e,e')(\top) \to^* e$ et  $D(e,e')(\bot) \to^* e'$.
25. Définir $A$ une expression telle que $A(D(e,C_n)) \to^* D(C_n,C_{n+1})$
26. (*) Définir $\text{decr}$ telle que $\text{decr}(C_n) \to^* C_{\max\{n-1;0\}}$. On expliquera le raisonnement.
27. Définir $\text{sub}$ telle que $\text{sub}(C_n,C_m) \to^* C_{\max\{n-m;0\}}$

# Partie IV: Point-fixe et Récursivité
Le but de cette partie est de pouvoir faire des fonctions récursives.
## L'opérateur Point-fixe

On dit que $\text{fix}$ est un opérateur point-fixe  si il est sous forme normale et que, pour tout $f\in E$, on a :
$$\text{fix}(f) =_\beta f(\text{fix}(f))$$

28. Montrez que $\text{fix}(f)$ n'est pas unitaire.

On appellera $e$ un point fixe de $f$ si $f(e)\to^* e$

29. Montrez que si $\text{fix}(f)$ et $\forall e \in E, f(e)$ admettent des formes normales, alors $f$ admet un point fixe.
30. Soit $e$ sous forme normale. Donnez une expression $f$ respectant les hypothèses de la question précédente qui admet $e$ comme point fixe.
31. (*) Donnez une expression $\Theta$ point-fixe.

## Récursivité
On considère ici $F$ de la forme $F=(f,x\mapsto e)$ une fonction récursive, c'est à dire que $F$ sera appelé constamment avec $F$ comme premier argument. 

32. Montrez que, pour tout $\alpha$ sous forme normale, $\forall e\in E$,
$$\text{fix}(F)(e) \to^* \alpha \implies\exist n_r,\ \underbrace{F(F(...(F)...))}_{n_r\text{ fois}}(e)\to^*\alpha$$


Si $\alpha$ est sous forme normale, on appellera le plus petit $n_r$ le *nombre d'appels récursif* de $F(x)$.

> Indication : On pourra utiliser le graphes des réductions de $\text{fix}(F)(e)$
## Un exemple
On définit :
$$
\text{fact\_rec} = (f,x\mapsto \text{if}(\text{eq\_0}(x))(C_1)(\text{mul}(x,f(\text{sub}(x,1)))))
$$
Et on pose $\text{fact} = \Theta(\text{fact\_rect})$

33. Montrez que $\text{fact}(C_n) \to^* C_{n!}$
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
> A revoir: Je pense avoir fait une erreur quand j'ai écrit la correction, mais je ne sais pas d'où elle viens. Je regarderai avec vos propositions. Ne passez pas trop de temps dessus si elle vous semble impossible.
33. En déduire que si $e$ est typé, alors $e$ est unitaire et n'as pas de variable libre.
34. En déduire que $\Delta$ ne possède pas de typage.

> Remarque : En pratique, le lambda calcul typé est assez faible, il ne permet pas de faire de fonctions récursive, de boucle, ou même la fonction $\text{pow}$ comme on a pu le voir dans la partie III.

> Remarque : Le compromis pris par OCaml est de forcer l'existence d'un opérateur point-fixe, dont on ne vérifiera jamais le type. Quand une fonction est définie avec le mot clef `rec`, alors sa "vraie" signature est `val fct : fix -> RESTE`, mais ce premier argument n'est ni affiché, ni vérifié. OCaml ajoute aussi des types par défaut tel que `int`, `string`, `bool` etc...


<!--stackedit_data:
eyJoaXN0b3J5IjpbNTkxNDQ0NTQ3LDE1NzcxMjkyOTAsLTU4Nz
UyOTkwMSwtNjk2MDgxNzEzLC0xNTk1MjQ3NDA3LDEyODI1Nzg4
MzEsLTc2NDYzMzQ1MiwzOTMwNzk1MTcsMTEyMDYxNzI1MCw3OD
M1NzE4OSw2OTIxNjM0MywtMTc3ODY2OTM3MCwzMTQzODQ2MTYs
MjAzOTM5OTc3Myw3NzM0ODgwNzgsLTc4OTMwOTQxOCw3MzIwOT
UyNjEsLTEwNzM0MTYwMTksNDg5OTU5Mzc5LDEzMjgyMzg0NzBd
fQ==
-->