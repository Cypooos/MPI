# Méthodes de programmations

## Algo et Programmes
1.  Qu'est-ce qu'un paradigme ? Expliquez les paradigmes suivant : paradigme logique, paradigme impératif structuré, paradigme fonctionnel, **paradigme orienté objet ?**
2. Qu'est ce-qu'un langage de programmation compilé ? Interprété ? **Compilé à la volé ?**
3. Quelle est la différence entre un `signed` et un `unsigned` ? Comment sont encodé les nombre négatifs ?
4. Comment sont encodé les flottants ? En sachant que un `int` (sur 2bits à 8 bits d'exposants, Combien de chiffre significatifs en base 10 peuvent t-il stoqués ? 
5. Déterminez que la fonction `getter` suivante termine :
```ocaml
let rec get m l = match l with
 | [] -> m
 | e::q with e>=m -> get e l
 | e::q -> get m l ;;
let getter = get min_int;;
```
Que fait-il ? Démontrer sa correction.

6. Qu'est-ce que une correction partielle ? Parallèles avec problème décidable et semi-décidable ?
7. Définition de la complexité ?
8. Quel est le type de la fonction suivante :
```ocaml
let a b c d = match b c [||] with
 | e with !e = d -> c+.1
 | _ -> d
```
9. Qu'est ce ce que la programmation défensive ? Pourquoi est-elle plus simple en ocaml que e
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAxNjIxMDczOCwtODgwMzE0Nzk4LDgwNT
E0ODY4NSwtMTg3NzEyMDEyOF19
-->