

## Petites info

- Différence en OCaml entre `type C of int * int` et `type C of (int * int)`
- [On ne sait pas bien faire des parcours en profondeur](https://11011110.github.io/blog/2013/12/17/stack-based-graph-traversal.html)

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
```
3. Avec une ref :
```ocaml
let a = ref (fun () -> ()) in
!a := (fun () -> !a ()) in
!a ();;
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk2NDM3MTk0XX0=
-->