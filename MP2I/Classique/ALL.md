


## Ensemble d'entiers, version 1

Proposer une structure de données pour stocker des sous-ensembles d’entiers S compris entre 0 et M qui supporte les opérations suivantes :
  — Créer cette structure (prend M en argument) en $O(M)$
  — Ajouter un entier dans S, en $O(1)$;
  — Retirer un entier de S, en $O(1)$;
  — Parcourir les entiers actuellement stockés dans S, en $O(M)$.

La complexité en espace sera de $O(M)$
Écrire le pseudocode pour ces opérations.
## Ensemble d'entiers, version 2
On suppose maintenant la présence d'une fonction `pow b` calculant $2^b$ en $O(1)$, et que nos entiers ne sont pas bornés.

Proposer une structure de données pour stocker des sous-ensembles d’entiers S compris entre 0 et M qui supporte les opérations suivantes :
  — Créer cette structure (prend M en argument) en $O(1)$
  — Ajouter un entier dans S, en  $O(1)$;
  — Retirer un entier de S, en $O(1)$;
  — Parcourir les entiers actuellement stockés dans S, en $O(M)$.

La complexité en espace sera de $O(1)$
Écrire le pseudocode pour ces opérations.

## Nombre de nombres premiers

On note $\pi(n)$ le nombre de nombres premiers inférieurs ou égaux à $n$.
Donnez une manière de calculer la fonction. Quelles sont ses complexités en temps et en espace ?

## Est-il premier ?
Donnez le code de `val premier: int -> bool` qui à un entier retourne `true` si il est premier. Quelles sont ses complexités en temps et en espace ?

## Nombre sans carré
> Source : Sujet Ulm 2019 J3 https://a3nm.net/work/exams/ens/exercices_info_ulm_2019.pdf

On dit qu’un entier naturel est sans carré s’il n’est pas divisible par le carré d’un entier supérieur ou égal à $2$.

Donner le pseudo-code d’un algorithme permettant de calculer le nombre d’entiers naturels sans carré inférieurs ou égaux à $n$. Quelles sont ses complexités en temps et en espace ?

## Tout les Palindromes
On dit que $\omega$ est un sous-mots (ou facteur) de $u$ s'il existe deux mots potentiellement vide $a$, $b$ tel que $u=a.\omega.b$ (l'opération $.$ est ici la concaténation)

Donnez le code d'une fonction qui à un string associe la liste de tout ses facteurs qui sont des palindromes en $O(N^2)$

## Le plus long Palindrome
On dit que $\omega$ est un sous-mots (ou facteur) de $u$ s'il existe deux mots potentiellement vide $a$, $b$ tel que $u=a.\omega.b$ (l'opération $.$ est ici la concaténation)
Donnez le code d'une fonction qui à un string associe son plus long palindrome. Quel est la complexité ? 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAzOTQyMzUzMl19
-->