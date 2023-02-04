> File, récursivité, liste, types, ocaml++ 

Cet exercice est difficile, et pousse la création de type récursif assez loin
Source : Sujet Ulm 2019 J3 https://a3nm.net/work/exams/ens/exercices_info_ulm_2019.pdf
## Paresse et file persistante
Question 0.
(a) Qu’est-ce qu’une file ?
(b) Rappeler la distinction entre structure de donnée persistante et impérative.
(c) Donner une implémentation persistante d’une file.
(d) En déduire une implémentation impérative d’une file.
(e) Dans le pire cas, quelle est la complexité de chacune des opérations des ces deux implémentations ?
Lorsque l’on analyse la complexité amortie d’une bibliothèque, on s’intéresse à la complexité d’une
séquence d’opérations dans son ensemble plutôt qu’à la complexité de chaque opération fournie par
la bibliothèque. Ainsi, même si une opération A est très coûteuse, son coût peut être compensé par
l’exécution préalable d’un grand nombre d’opérations B, de façon à ce que la complexité globale de la
séquence d’opérations soit asymptotiquement le même que si A était peu coûteuse.
Question 1.
(a) Faire l’analyse de complexité amortie de l’implémentation impérative de la question 0.
(b) Ce raisonnement peut-il s’appliquer pour l’implémentation persistante ?
On se propose d’implémenter, en OCaml, une bibliothèque de calcul paresseux. Celle-ci expose un
type paramétré de suspensions ’a susp et des fonctions de types suivants :
susp : (unit -> ’a) -> ’a susp
force : ’a susp -> ’a
Une suspension (de type ’a susp) contient une fonction permettant de calculer une valeur de type ’a.
Elle peut être construite facilement grâce à la fonction susp. Le calcul n’est effectué que lorsque
l’utilisateur de la bibliothèque le demande via la fonction force. Cette dernière fonction vérifie si le
calcul a déjà été effectué : si tel est le cas, elle en renvoie le résultat pré-calculé. Sinon, elle lance le
calcul, stocke le résultat pour de futurs appels, et elle le renvoie.
Question 2. Donner une implémentation possible de cette bibliothèque, dans le langage OCaml.
On définit le type des listes paresseuses en OCaml :
type ’a slist_cell =
| SNil
| SCons of ’a * ’a slist
and ’a slist = ’a slist_cell susp
Question 3.
(a) Comparer la notion de liste paresseuse avec la notion habituelle de liste.
(b) Écrire une fonction scons : ’a -> ’a slist -> ’a slist qui ajoute un élément en tête d’une
liste paresseuse, ainsi qu’une valeur snil de liste paresseuse vide.
(c) Écrire deux fonctions shd : ’a slist -> ’a et stl : ’a slist -> ’a slist qui prennent
une liste paresseuse non vide en paramètre, et qui renvoient respectivement son premier élément
et la liste paresseuse des autres éléments.
(d) Écrire une fonction sappend : ’a slist -> ’a slist -> ’a slist qui concatène de manière
paresseuse deux listes paresseuses. Cette fonction devra s’exécuter en temps constant.
(e) Écrire une fonction srev : ’a slist -> ’a slist qui renverse une liste paresseuse de manière
efficace. Quelle est la complexité des accès aux différents éléments de la liste renversée ?
Grâce aux listes paresseuses, on propose ici une variante de la file proposée dans la question 0.c, qui
évite le problème de complexité expliqué dans la question 0.e. Dans cette nouvelle implémentation, une
file sera représenté en OCaml par le type enregistrement suivant :
type ’a queue = {
rear : ’a slist;
len_rear : int;
front : ’a slist;
len_front : int;
}
Le plus souvent, on enfilera les éléments au début de la liste rear et on les défilera au début de la liste
front. De plus, on maintiendra les invariants suivants :
— les champs len_front et len_rear contiennent les longueurs des listes front et rear ;
— on a toujours len_rear ≤ len_front.
Question 4.
(a) Définir les fonctions d’enfilage et de défilage pour cette variante d’implémentation de file.
(b) Prouver que le temps d’exécution amorti de chacune de ces deux opérations est O(1).
Suite des questions
Question 5. Une liste paresseuse est-elle toujours de longueur finie ? Définir en OCaml une liste
paresseuse qui énumère les carrés parfaits
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNDAwMzUxMTBdfQ==
-->