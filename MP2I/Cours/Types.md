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


SOLUTIONS

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2MDEyMjQ4OCwxMjIxMjIzODc2LC0xMD
AzNDA5NDYyXX0=
-->