

## Petites info

- Différence en OCaml entre `type C of int * int` et `type C of (int * int)`
- [On ne sait pas bien faire des parcours en profondeur](https://11011110.github.io/blog/2013/12/17/stack-based-graph-traversal.html)
- Exact Matrix Cover est NP-complet
- Utiliser les Dancing Links pour faire du back-tracking efficace sur des listes triée. Utillisé pour faire un algo très efficace sur le problème Exact Matrix Cover. Permet d'implémenté une struture d'ensemble d'entier bornée la plus efficace possible ( add et remove en O(1), parcours en O(|S|) ).
- Calcul de hauteur d'un ABR dans le cas d'un stackoverflow ? -> Stack avec (hauteur, arb) ou continuation
- [la conjecture de Robbins est vraie](https://en.wikipedia.org/wiki/Robbins_algebra), preuve par un prouveur automatique
- Théorème des 4 couleurs à eu 100+ cas vérifier par odinateur, puis elle a été refait en Coq
- Thomas Hales à fait une preuve demandant aussi bcp de cas que les mathématiciens n'ont pas pu vérifier entièrement. Le projet Flyspeck à abouti à une preuve Coq.
- [On peut dérécursifier n'importe quel programme par la continuation](https://media.devenirenseignant.gouv.fr/file/agregation_externe/32/6/sujet0_agregation_externe_informatique_epreuve1_1422326.pdf) (qui donne une fonction récursif terminale) puis par simulation de la version en continuation par des types somme (appellé défonctionalisation). 
- Liste doublement chainé en OCaml avec `type 'a lidb = | Null | E of {mutable before:lidb; mutable after:lidb; mutable val: 'a}`
- Pour calculer $AB$, transposer $B$ dans la ram pour utilliser le registre L1
- Jean Gallier fait des cours sur la logique qui sont bien
- [Projet Euler pour créer des exercices de colles](https://projecteuler.net/problem=215)
- Coder `val memo` une fonctionelle faisant de la mémoïsation automatiquement, aka
`let fib = memo (fun fib n -> if n <= 1 then 1 else fib (n-2) + fib (n-1))`

- `let rec li = 1::li;; li=li;;` ne termine pas, 
`type recl = {v:int; q:recl};;let rec b={v=0;q=a};;a=a;;` ne termine pas,
`type recl = {q:recl; v:int};;let rec b={q=a;v=0};;b=b;;` termine et indique une erreur.
En fait, les trois termine avec la même erreur, mais dans le cas 3 OCaml détecte immédiatement le cycle et renvoie l'erreur en avance.

- On peut créer ces propres opérateurs `let` et `and` en ocaml : https://v2.ocaml.org/manual/bindingops.html
- On peut créer des [fonctions polymorphique universellement quantifié](https://v2.ocaml.org/manual/polymorphism.html) pour éviter de dépasser les weaks ou préciser la généralisation d'un type.
- `golly` implémente l'algo du HashLife, utillisé pour faire des execution rapide du jeu de la vie / Rule 110, une sorte de mémoisation spaciale et temporelle
- En ocaml on a des modules du premier ordre, donc on peut faire des fonctions qui prend des modules `let fct (module A: ModuleType) = ... A.truc`, et l'on peut faire des foncteurs aussi (qui map des modules)
- Pour faire des fonctions polymorphe universellement quantifié, on peut faire `let f (type a) (x:a) = ...`
- Sujet d'oral ? https://11011110.github.io/blog/2022/12/13/randomly-traceable-graphs.html
- Comment faire un pretty-printer (qui met un nombre réduit de parenthèses) à l'aide de règle de priorité et de fonction mutuellement récursive / un compteur, en temps linéaire ?
- Comment faire un lexer en temps linéaire ? Un lexer match toujours la plus grande entré possible avant de passer à match la suivante. 
- En ocaml on peut utilliser Merlin pour faire un analyser syntaxique et ocamllex pour faire un lexer.

## Fonctionnement d'un prouver automatique
### Etape 1 : Un solveur SAT
Naif: Retour sur Trace
### Etape 2 : Egalité de Leibniz + fonction non évalué
Toujours décidable !
Exemples  :
 - Montrer $x_1 =x_2 \land x_3 = x_4 \land ... \implies x_i = x_j$
 - Montrer $(2)$ : $f^3(x)=x \land f^5(x) = x \implies x=f(x)$ (avec $f^n$ la composition $n$-ième)

On crée une structure Union-Find pour chaque sous terme apparaissant dans nos éléments, représentant les classes d'équivalence de l'égalité.
L'Union-find nous assure la fermeture par transitivité, réflexivité, symétrie.
Il faut ajouter l'axiome de Leibniz :
A chaque itération, on va retrouver dans une formule une autre sous formule de la classe d'équivalence, et va pouvoir la remplacer pour trouver une nouvelle formule.
Par exemple, les étapes d’exécutions de $(2)$ donne :
$$
\begin{align*}
&&\{&x&,&&f^3(x)&&,&&f^5(x)&&\};\{ &&f(x)&&\};\{&&f^2(x)&&\};\{&&f^4(x)&&\}&&\text{init}&\\
&&\{&x&,&&f^3(x)&&,&&f^5(x)&&,&&f^2(x)&&\};\{&&f(x)&&\};\{&&f^4(x)&&\}&&f^5(x)[f^3(x)\larr x]&\\
&&\{&x&,&&f^3(x)&&,&&f^5(x)&&,&&f^2(x)&&,&&f(x)&&\};\{&&f^4(x)&&\};&&f^3(x)[f^2(x)\larr x]&\\
&&\{&x&,&&f^3(x)&&,&&f^5(x)&&,&&f^2(x)&&,&&f(x)&&,&&f^4(x)&&\};&&f^5(x)[f(x)\larr x]&\\
\end{align*}
$$
On continue jusqu’à ce l'on ne peut plus crée de termes présent dans notre structure.
Dans ce cas, on laisse le SAT solver faire une supposition $P$ (qui corresponderai à un $f(x)=g(0,f(t))$ par exemple) et re-faire tourner notre union-find.
On continue ça jusqu’à soit que on ai plus de variables à supposer (on a donc une preuve), soit que on a supposer $x\neq y$ mais $x$ et $y$ sont dans la même classe, dans ce cas on fait un retour sur trace.

### Etape 3 : Logique du premier ordre
Semi-décidable.
But : montrer $\forall x.\exist y.y=x$, ou encore $\forall x.\forall y.( S(x)=S(y)\implies x=y)$ ($S$ le successeur de Peano) 

On exprime tout problème sous la forme $X,Y,Z \implies \bot$ (quitte à le faire par l'absurde)
On sépare les formules en formules commençant par un $\forall$ (on les met dans $H$), et les autres (dans $T$).
Pour chaque formule de la forme $\exist c.P$, on rajoute un terme $X_c$ et effectue $P := P[c\larr X_c]$ (remplacer seulement les variables libres par une constante).
> pas sur :
> Pour les formules commençant par $\lnot P$, on applique morgan pour faire tomber le not?

On effectue alors notre SAT + algo union-find sur toute les formules dans $T$.
Quand l'on a fini, c'est que l'on doit utilliser une des formules de $H$.
L'on va alors appliquer tout les $H$ à des termes qui apparaissent dans un $T$. Pour savoir lesquels, on peut analyser une hypothèse pour trouver un terme plus utile.
Par exemple, dans $\forall x(x\neq 0 \implies \exist y. x= S(y))$, le terme "trigger" serai un prédicat de la forme "$e\neq 0$"

L'on recommence jusqu’à (avec un peu de chance) trouver une preuve de notre solution.

> Ref: https://www.lri.fr/~conchon/FIIL/slides_conchon_ejcim2018.pdf
### Autre
On peut aussi faire une approche + naturelle, avec la théorie de la Résolution, montré par Robinson.
**Liste de prouveur automatique SMT :**
 - Z3
 - CVC5
 - Alt-Ergo
## Sujet d'oraux
- Addition Chains, KNUTH, volume II, Chapitre 4, "how fast can we multiply" - 465
- Calculer $M^n.V$ par $\exp(M,2n,V) = \exp(M^2,n,V)$ et $\exp(M,2n+1,V) = \exp(M^2,n,MV)$ car $MV$ en $O(n^2)$ (négligeable devant $M^2$)

## Retirer le cycle à une liste en temps O(n) et espace O(1)

On décompose la liste en la partie $A = x_0 , ... , x_\lambda$ avant le cycle, et la partie $x_{\lambda+1}, ... x_{\lambda+\mu} = B$ cyclique de longueur $\mu$
1. Sans arithmétique :
Après avoir trouvé un $x_i\in B$ (lièvre et la tortue, ou alors exponentiation), on calcule $\mu$ (juste on parcours jusqu’à retomber sur $x_i$).
Puis on inverse la liste de $x_0$ à $x_i$, et on fait un parcours partant de $x_i$ et un autre partant de $x_{i+1}$.
On sait que la somme des longueurs de deux parcours fait $2\lambda + \mu -1$.
Comme on a $\mu$, on peut trouver la longueur de $\lambda$.
Permet de poser des questions sur inverser une liste, le lièvre et la tortue, la définition d'une liste etc...

2. Avec arithmétique :
le lièvre et la tortue se termine en l'unique $x_i$ tel que $x_i = x_{2i}$ (unique dans le sens ou si $x_r = x_{2r}$, alors $x_r = x_i$)
A continuer.

## Récursivité sans `rec` ou boucle :
1. Méthode par des types :

```ocaml
type t = T of (t -> t);;
let app (T f) x = f x;;
let delta = (fun x -> app x x);;
let inf = delta (T delta);;

let y = (fun (T f) -> (fun x -> app (f (fun t -> app (app x x) t)))(fun x -> app (f (fun t -> app (app x x) t))))
```
2. Avec l'option `-rectype`, on peut définir l'opérateur point-fixe :
```ocaml
(* sans eta-réduction : *)
let fix f = (fun x -> f (x x))(fun x -> f (x x));;
(* avec eta-réduction : *)
let fix f = (fun x,u -> f (x x) u)(fun x,u -> f (x x) u);;

let rec_fact rec_me n = match n with | 0 -> 1 | _ -> n*(rec_me (n-1)) in
let factorial = fix rec_fact;;
```
3. Avec une ref :
```ocaml
let a = ref (fun () -> ()) in
!a := (fun () -> !a ()) in
!a ();;
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzNTUwNjUzMywxMzQ0NjY4MDcwLC05Mj
YxMjczNjcsLTIxMjA1MzY4ODYsLTIwNzMzMzc5OTQsLTg1MzI5
MjQxNywtMTQ4ODk2Mjc5MCwtMTA2ODk3OTcwMiwtOTE3NTM0ND
I2LC0xNTI4NDExMTM0LDM3ODM4MDQyNywxNzcyNDUwODQwLDk3
MjQzNDc3MCwxODkzNzMxMTU5LC0xNDQ3MDQzMjg0LDE2MzQ3Nj
QwNDgsLTExNDgxNzI0NTYsLTExNDYyNjU0OTEsLTIwOTgwNDM0
OTcsODk5Njk5NjUzXX0=
-->