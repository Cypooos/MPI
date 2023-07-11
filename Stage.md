

## Petites info

- Différence en OCaml entre `type C of int * int` et `type C of (int * int)`
- [On ne sait pas bien faire des parcours en profondeur](https://11011110.github.io/blog/2013/12/17/stack-based-graph-traversal.html)

## Retirer le cycle à une liste cyclique en O(n) et O(1)

On décompose la liste en la partie $A = x_0 , ... , x_\lambda$ avant le cycle, et la partie $x_{\lambda+1}, ... x_{\lambda+\mu} = B$ cyclique de longueur $\mu$
1. Après avoir trouvé un $x\in B$ (lièvre et la tortue, ou alors exponentiation), on 
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
eyJoaXN0b3J5IjpbMTA4MzM4NDU2MiwxOTY0MzcxOTRdfQ==
-->