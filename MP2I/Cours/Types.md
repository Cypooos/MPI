## Types?
Donnez la signature des fonctions suivante :
```ocaml
let a1 b c d = match b c [||] with
  | e when !e = d -> c+.c
  | _ -> d;;
``` 

```ocaml
let a2 b c d = b.(!c.(d)).[!c.(d)];;
``` 

```ocaml
let a3 b c = (b c) c (!c);;
```
```ocaml
let a4 b c d e = 1+match b c d with
 | 
 | f -> f e
 |
```


SOLUTIONS
```ocaml
val a1 : (float -> 'a array -> float ref) -> float -> float -> float = <fun>  
val a2 : string array -> int array ref -> int -> char = <fun>  
val a3 : ('a ref -> 'a ref -> 'a -> 'b) -> 'a ref -> 'b = <fun>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ4NjY1MTAxMywtMjExOTIzNTQ1NCwxMj
IxMjIzODc2LC0xMDAzNDA5NDYyXX0=
-->