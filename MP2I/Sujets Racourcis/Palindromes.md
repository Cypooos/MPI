
Source : oral A3 tomé à l'ens ulm en 2019 https://diplome.di.ens.fr/informatique-ens/annales/2019_InfoU-exercices.pdf

# Palindromes
Un mot est ici un `string`

On dit que $\omega$ est un sous-mot (ou facteur) d'un mot $u$ s'il existe deux mots potentiellement vide $a$, $b$ tel que $u=a.\omega.b$ (l'opération $.$ est ici la concaténation)
Un palindrome est un mot dont la lecture de gauche à droite et de droite à gauche des lettres donne la même chose.

Le but de ce sujet est de calculer le nombre de facteurs palindromes d'un mot $\omega$.
## Question 1

Donnez une version naïve pour donner la liste des couples $(i,j)$ tel que le facteur de $\omega$ commençant en $i$ et terminant en $j$ soit un palindrome. 

## Question 2
Optimisez votre algorithme pour qu'il ai une complexité de $O(n^2)$. On pourra réfléchir sur la parité de la longueur du mot.
## Question 3

<!--stackedit_data:
eyJoaXN0b3J5IjpbODg1MjczOTRdfQ==
-->