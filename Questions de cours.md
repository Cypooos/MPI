# Méthodes de programmations

## Algo et Programmes
1.  Qu'est-ce qu'un paradigme ? Expliquez les paradigmes suivant : paradigme logique, paradigme impératif structuré, paradigme fonctionnel, **paradigme orienté objet ?**
2. Qu'est ce-qu'un langage de programmation compilé ? Interprété ? **Compilé à la volé ?**
3. Quelle est la différence entre un `signed` et un `unsigned` ? Comment sont encodé les nombre négatifs ?
4. Comment sont encodé les flottants ? En sachant que un `int` (sur 2bits à 8 bits d'exposants, Combien de chiffre significatifs en base 10 peuvent t-il stoqués ? 
5. Déterminez que l'algorithme suivant termine :
```ocaml
let rec get l m = match l with
 | [] -> m
 | e::q with e>=m -> get l e
 | e::q -> get l m 
```
Que fait-il ? Le démontrez.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM0NzU2MDU4NywtODgwMzE0Nzk4LDgwNT
E0ODY4NSwtMTg3NzEyMDEyOF19
-->