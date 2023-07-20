

## Petites info

- Différence en OCaml entre `type C of int * int` et `type C of (int * int)`
- [On ne sait pas bien faire des parcours en profondeur](https://11011110.github.io/blog/2013/12/17/stack-based-graph-traversal.html)
- Sujet d'oral ? https://11011110.github.io/blog/2022/12/13/randomly-traceable-graphs.html
- Exact Matrix Cover est NP-complet
- Utiliser les Dancing Links pour faire du back-tracking efficace sur des listes triée
- Calcul de hauteur d'un ABR dans le cas d'un stackoverflow ? -> Stack + hauteur ou continuation
- [la conjecture de Robbins est vraie](https://en.wikipedia.org/wiki/Robbins_algebra), preuve par un prouveur automatique
- Théorème des 4 couleurs à eu 300+ cas vérifier par odinateur, puis elle a été refait en Coq
- Thomas Hales à fait une preuve demandant aussi bcp de cas que les mathématicien n'ont pas pu vérifier entièrement. Le projet Flyspeck à abouti à une preuve Coq.
- [On peut dérécursifier n'importe quel programme par la continuation](https://media.devenirenseignant.gouv.fr/file/agregation_externe/32/6/sujet0_agregation_externe_informatique_epreuve1_1422326.pdf) (qui donne une fonction récursif terminale) puis par simulation de la version en continuation par des types somme (appellé défonctionalisation) CF
## Fonctionnement d'un prouveur automatique
### Etape 1 : Un solveur SAT
Naif: Retour sur Trace
### Etape 2 : Egalité et fonction
Toujours décidable !
But :
 - Montrer $x_1 =x_2 \land x_3 = x_4 \land ... \implies x_i = x_j$
 - Montrer $f^3(x)=x \land f^5(x) = x \implies x=f(x)$ (avec $f^n$ la composition $n$-ième)

On crée une structure Union-Find pour chaque sous terme apparaissant dans nos éléments, représentant les classes d'équivalence de l'égalité.
L'Union-find nous assure la fermeture par transitivité, réflexivité, symétrie.
Il faut ajouter l'axiome de Leibniz.
A chaque itération, on va retrouver dans une formule une autre sous formule de la classe d'équivalence, et va pouvoir la remplacer pour trouver une nouvelle formule.
Par exemple, les étapes d’exécution donne :
$$
\begin{aligned}
\{x,f^3(x),f^5(x)\};\{f(x)\};\{f^2(x)\};\{f^4(x)\}&&\text{init}&\\
\{x,f^3(x),f^5(x);\};\{f(x)\};\{f^2(x)\};\{f^4(x)\}&&f^5(x)[f^³(x)\larr x]&\\
\{x,f^3(x),f^5(x);\};\{f(x)\};\{f^2(x)\};\{f^4(x)\}&&f^5(x)[f^³(x)\larr x]&\\
\end{aligned}
$$


### Etape 3 : Logique du premier ordre
Semi-décidable


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
(* ?? *)
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
eyJoaXN0b3J5IjpbLTEwOTAxMzc0MDEsLTE3MDEwNTczMDAsMT
k2NDM3MTk0XX0=
-->