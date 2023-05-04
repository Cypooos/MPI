> Sources :
> *A3 ORAL-ULM MPI*
> *INFO 2023 CCP MPI*

# Palindromes
Un mot est ici un `string`

On dit que $\omega$ est un sous-mot (ou facteur) d'un mot $u$ s'il existe deux mots potentiellement vide $a$, $b$ tel que $u=a.\omega.b$ (l'opération $.$ est ici la concaténation)
Un palindrome est un mot dont la lecture de gauche à droite et de droite à gauche des lettres donne la même chose.

Le but de ce sujet est de calculer le nombre de facteurs palindromes d'un mot $\omega$ (constitué seulement de lettres) de longueur $n$.
## Question 1

Donnez une version naïve de l'algorithme pour donner la liste des couples $(i,j)$ tel que le facteur de $\omega$ commençant à la lettre d'indice $i$ et terminant en la lettre d'indice $j$ soit un palindrome. 

## Question 2
Expliquer comment on peut transformer ce problème en la recherche de palindrome de longueur impaire. Donner le code d'une fonction effectuant cette transformation.

En ne considérant que les palindromes de longueur impaire, donnez une version de l'algorithme recherché en $O(n^2)$ 

## Question 3
On note $\rho_i$ la longueur du plus grand palindrome centré en $i$
Donnez une inégalité sur $\rho_{i+d}$ qui fasse intervenir $\rho_{i-d}$
Donnez une condition suffisante pour qu'il y ait égalité.

## Question 4

Sur la base de cette observation, améliorer l’algorithme pour qu’il fonctionne en temps linéaire.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUwODI4Nzk5NCwtMTMxNzI3NzQ0OSwtNj
k2ODEzNDAxLC0zMzU5NDUxMDQsMTA4MjQxMTUwNl19
-->