## Types ?
Donnez la signature des fonctions suivante :
```ocaml
let a1 b c d = b.(!c.(d)).[!c.(d)];;
``` 
```ocaml
let a2 b c = (b c) c (!c);;
```
```ocaml
let a3 a b c = a [|[b.[c]]|];;
```
```ocaml
let a4 a b c = c.(a c) (a !b);;
```
```ocaml
let b1 b c d = match b c [||] with
  | e when !e = d -> c+.c
  | _ -> d;;
``` 
```ocaml
let b2 b c d e = 1<match b c d with
  | f when !(d f) -> c
  | f -> f e;;
```

SOLUTIONS
```ocaml
val a1 : string array -> int array ref -> int -> char = <fun>  
val a2 : ('a ref -> 'a ref -> 'a -> 'b) -> 'a ref -> 'b = <fun>
val a3 : (char list array -> 'a) -> string -> int -> 'a = <fun>
val a4 :
  ((int -> 'a) array -> int) ->
  (int -> 'a) array ref -> (int -> 'a) array -> 'a = <fun>
val b1 : (float -> 'a array -> float ref) -> float -> float -> float = <fun>  
val b2 :
  (int -> (('a -> int) -> bool ref) -> 'a -> int) ->
  int -> (('a -> int) -> bool ref) -> 'a -> bool = <fun>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMzkyOTI4NjUsLTcxMjU3NDA5XX0=
-->