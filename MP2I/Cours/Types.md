## Types ?
Donnez la signature des fonctions suivante :
```ocaml
let a1 b c d = b.(!c.(d)).[!c.(d)];;
``` 
```ocaml
let a2 b c = (b c) c (!c);;
```
```ocaml
let a3 b c d = match b c [||] with
  | e when !e = d -> c+.c
  | _ -> d;;
``` 
```ocaml
let a4 b c d e = 1<match b c d with
  | f when !(d f) -> c
  | f -> f e;;
```

SOLUTIONS
```ocaml
val a1 : string array -> int array ref -> int -> char = <fun>  
val a2 : ('a ref -> 'a ref -> 'a -> 'b) -> 'a ref -> 'b = <fun>
val a3 : (float -> 'a array -> float ref) -> float -> float -> float = <fun>  
val a4 :
  (int -> (('a -> int) -> bool ref) -> 'a -> int) ->
  int -> (('a -> int) -> bool ref) -> 'a -> bool = <fun>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxMjU3NDA5LC0xMDk0NDQ0MTYyLC0yMT
E5MjM1NDU0LDEyMjEyMjM4NzYsLTEwMDM0MDk0NjJdfQ==
-->