> Fonction, Récursivité, Équivalents, Analyse de programme

Sujet P1 d'INFO théorique d'Ulm en 2021
Il me semble d'une importance cruciale de par à quel point il est général
Source : https://a3nm.net/work/exams/ens/exercices_info_ulm_2021.pdf
# Théorème général de l’analyse des programmes récursifs
Étant données deux fonctions $f, g  :  \R+ \to \R+$, on note  f  (n) = Θ(g(n))  si  f  (n) =  O(g(n))  et  
g(n) =  O(f  (n)).  
On considère dans ce problème un algorithme récursif  A  prenant une entrée de taille  n  ∈  N∗. On  
suppose que :  
— si  n  = 1,  A  met un temps borné par une constante ;  
— pour  n >  1,  A  fait un nombre  a  ∈  N∗  d’appels récursifs à  A  sur une entrée de taille  n  
b  (b  est un  
rationnel strictement plus grand que  1), ainsi qu’un certain nombre d’autres opérations dont le  
temps est  f  (n).  
Ainsi, le temps  T  (n)  pris pour résoudre le problème au rang  n  est :  
T  (n) =  a  ×  T  
(  n  
b  
)  
+  f  (n).  
Par simplicité, on supposera dans tout le problème qu’on applique toujours l’algorithme à un  n  pour  
lequel  n  
b  est un entier, y compris lors des appels récursifs.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0MzgxOTk3MSwtMTM2MDY5NjExNF19
-->