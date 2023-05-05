> *J2 ORAL-Ulm 2021*
# Paresse et file persistante

## Question 0
1) Qu’est-ce qu’une file ?
2) Rappeler la distinction entre structure de donnée persistante et impérative.
3) Donner une implémentation persistante d’une file.
4) En déduire une implémentation impérative d’une file.
5) Dans le pire cas, quelle est la complexité de chacune des opérations des ces deux implémentations ?

Lorsque l’on analyse la complexité amortie d’une bibliothèque, on s’intéresse à la complexité d’une séquence d’opérations dans son ensemble plutôt qu’à la complexité de chaque opération fournie par la bibliothèque.

Ainsi, même si une opération A est très coûteuse, son coût peut être compensé par l’exécution préalable d’un grand nombre d’opérations B, de façon à ce que la complexité globale de la séquence d’opérations soit asymptotiquement le même que si A était peu coûteuse.
## Question 1
1) Faire l’analyse de complexité amortie de l’implémentation impérative de la question 0.
2) Ce raisonnement peut-il s’appliquer pour l’implémentation persistante ?

## Question 2
On se propose d’implémenter, en OCaml, une bibliothèque de calcul paresseux. Celle-ci expose un type paramétré de suspensions `’a susp` et des fonctions de types suivants :
```ocaml
val susp : (unit -> ’a) -> ’a susp
val force : ’a susp -> ’a
```
Une suspension (de type `’a susp`) contient une fonction permettant de calculer une valeur de type `’a`.
Elle peut être construite facilement grâce à la fonction `susp`. Le calcul n’est effectué que lorsque l’utilisateur de la bibliothèque le demande via la fonction force. Cette dernière fonction vérifie si le calcul a déjà été effectué : si tel est le cas, elle en renvoie le résultat pré-calculé. Sinon, elle lance le calcul, stocke le résultat pour de futurs appels, et elle le renvoie.

Donner une implémentation possible de cette bibliothèque, dans le langage OCaml.
## Question 3
On définit le type des listes paresseuses en OCaml :
```ocaml
type ’a slist_cell =
| SNil
| SCons of ’a * ’a slist
and ’a slist = ’a slist_cell susp
```

1) Comparer la notion de liste paresseuse avec la notion habituelle de liste.
2) Écrire une fonction `scons : ’a -> ’a slist -> ’a slist` qui ajoute un élément en tête d’une liste paresseuse.
3) Définissez une valeur `snil` de liste paresseuse vide.
3) Écrire deux fonctions `shd : ’a slist -> ’a` et `stl : ’a slist -> ’a slist` qui prennent une liste paresseuse non vide en paramètre, et qui renvoient respectivement son premier élément et la liste paresseuse des autres éléments.
4) Écrire une fonction `sappend : ’a slist -> ’a slist -> ’a slist` qui concatène de manière paresseuse deux listes paresseuses. Cette fonction devra s’exécuter en temps constant.
5) Écrire une fonction `srev : ’a slist -> ’a slist` qui renverse une liste paresseuse de manière efficace. Quelle est la complexité des accès aux différents éléments de la liste renversée ?
## Questions 4
Grâce aux listes paresseuses, on propose ici une variante de la file proposée dans la question **0.3**, qui évite le problème de complexité expliqué dans la question **0.5**. Dans cette nouvelle implémentation, une file sera représenté en OCaml par le type enregistrement suivant :
```ocaml
type ’a queue = {
	rear : ’a slist;
	len_rear : int;
	front : ’a slist;
	len_front : int;
}
```
Le plus souvent, on enfilera les éléments au début de la liste `rear` et on les défilera au début de la liste `front`. De plus, on maintiendra les invariants suivants :
— les champs `len_front` et `len_rear` contiennent les longueurs des listes `front` et `rear` ;
— on a toujours `len_rear` $\le$ `len_front`.

1) Définir les fonctions d’enfilage et de défilage pour cette variante d’implémentation de file.
2) Prouver que le temps d’exécution amorti de chacune de ces deux opérations est O(1).

## Question 5
Une liste paresseuse est-elle toujours de longueur finie ? Définir en OCaml une liste paresseuse qui énumère les carrés parfaits.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNDA4NzY1MzAsLTEwNDIwNTUzMTAsLT
cxNTU3NTgyMCwtMTQ0Mjc3NjQxNiwtMTEzMDE2MzQ1NCwxMjE0
OTU3MzZdfQ==
-->