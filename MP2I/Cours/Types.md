## Types?
Donnez la signature des fonctions suivante :
```ocaml
let a b c d = match b c [||] with
  | e when !e = d -> c+.c
  | _ -> d
``` 

```ocaml
let a b c d = b.(!c.(d)).[!c.(d)]
``` 


SOLUTIONS

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIyMTIyMzg3NiwtMTAwMzQwOTQ2Ml19
-->