## Arbre binaire parfaits
> *INFO-1 MINES MPI 2023*

On ce donne le type d'un arbre suivant :
```c
typedef struct Noeud *arb;
struct Noeud {
  int valeur;
  arb fils_g;
  arb fils_d;
};
```

On définie un arbre binaire **parfait** tel que toute les feuilles sont à la même distance de la racine.
On dit que la hauteur de l'arbre nul (sans nœud) est -1.
1. Donnez une définition équivalente de ce type en OCaml. Toujours en OCaml, donnez la fonction `val hauteur : arbre -> int` donnant pour un arbre quelconque sa hauteur.
2. Dessinez un arbre parfait à 7 nœuds. Tout les arbres complets sont-ils parfaits ?
3. Démontrez que tout arbre parfait de hauteur $h$ possède $2^{h+1}-1$ nœuds.
4. Donnez `bool est_parfait(arb a)` renvoyant vrai si l'arbre `a` est parfait.
5. Donnez `arb arb_trouve(arb a, int k)` renvoyant le `k`ème élément dans l'ordre préfixe de l'arbre. On suppose ici que `a` est parfait et que $0\le k<n$ avec $n$ le nombre de sommets.
6. Discutez de la complexité de `arb_trouve` et de potentiel moyens de l'améliorer.

## Arbres d'intervalles
> Source : https://info-llg.fr/option-mp/pdf/TP_intervalles.pdf

Un arbre d'intervalles est un arbre binaire de recherche dont tous les nœuds contiennent un intervalle de la forme $[\![ a; b]\!]$, dont les clefs sont $(a,b)$ dans l'ordre alphabétique.

On ce donne le type suivant en ocaml :
```ocaml
type intervalle = int * int;;
type arbre_int = F | N of intervalle * arbre_int * arbre_int;;
```

1. Qu'est-ce qu'un arbre binaire de recherche ? Proposez une structure en C similaire à celle proposé pour représenter un arbre d'intervalles.
2. Donnez en C la fonction `int hauteur(arbre* a)` donnant la hauteur d'un arbre d'intervalle.
3. Dessinez puis donnez en OCaml arbre équilibré contenant les intervalles $\{[0;2]; [0;1]; [1;3]; [4;5]; [3;5]; [3;3]\}$
4. Donnez `val trouver : arbre_int -> intervalle -> intervalle` tel que `trouver a i`  retourne un intervalle de l'arbre `a` intersectant `i` en $O(h)$ avec $h$ la hauteur de `a`.
5. Définissez les opérations de rotations sur les arbres binaire de recherche. Donnez la fonction `val rotg : arbre_int -> arbre_int` effectuant l'opération de rotation gauche. 

On supposera écrite la fonction `val rotd : arbre_int -> arbre_int` qui effectue l'opération de rotation droite.

6. Donnez `val ajouter : arbre_int -> intervalle -> arbre_int` tel que `ajouter a i` ajoute à un arbre équilibré `a` l'intervalle `i`. On veillera à ce que `a` reste équilibré.
## Arbre canonique
> *INFO-A X-ENS MPI 2023*

On définie une structure d'arbre :
```ocaml
type tree = F of int | N of tree * tree;;
``` 
Un arbre binaire strict (ou localement complet) est dit *canonique* si pour $A$ et $B$ deux feuilles, on a $A$ plus proche de la racine que $B$ ssi $A$ arrive avant $B$ dans un parcours préfixe.

Un arbre canonique peut-être représenté par un tableau qui à chaque hauteur associe son nombre de feuilles.

1. Donnez une définition équivalente de ce type en C. Toujours en C, donnez la fonction `void parcours(arbre* arb)` qui affiche le parcours préfixe de `arb`.
2. Donnez les arbres canonique des tableaux $[\![0;2]\!]$, $[\![0;0;3;2]\!]$, $[\![0;1;1;1;1;2]\!]$.
3. Démontrez que le tableau d'un arbre canonique non trivial doit se terminer avec un nombre pair.
4. Donnez une fonction OCaml `val to_array : tree -> int array` qui à un arbre canonique associe son tableau d'entiers le représentant.
5. Donnez une fonction OCaml `val canonical : int array -> tree` qui à un tableau associe son arbre canonique. On mettra sur chaque feuille son indice d'apparition dans le parcours préfixe. 


## Arbre d'ensembles de mots
On ce donne le type suivant d'arbre en C :
```c
typedef struct arbre_mot arbre_mot;
struct arbre_mot {
  bool est_un_mot;
	arbre_mot[255] next;
}
```
On modélise une lettre par un entier positif entre $0$ et $255$.
On dit qu'un mot $(a_n)_{n\le p}$ appartient à un `arbre_mot` si il existe un chemin étiqueté par les lettres $a_0,...,a_p$ de la racine à un nœud ayant `est_un_mot` à `true`.

1. Donnez en OCaml une structure équivalente représentant le type `arbre_mots`. Toujours en OCaml, donnez `val hauteur : arbre_mots -> int` qui à un arbre associe sa hauteur.
2. Dessinez l'arbre représentant $\{ [ \! [0,1,0]\!]; [ \! [0,1,1]\!]; [ \! [1]\!]; [ \! [1,2]\!]\}$. Crée une variable `arbre_mot* example` le représentant.
3. Donnez `bool is_in(arbre_mot* a, int* mot, int n)` qui test si un `mot` de longueur `n` appartient à `a`
4. Montrez que si deux mots sont dans le même sous-arbre enraciné à une distance $n$ de la racine, alors leur $n$ premières lettres sont les mêmes.
5. Donnez `void add(arbre_mot* a, int* mot, int n)` qui ajoute à `a` le mot `mot` de longueur `n`. On utilisera une assertion pour vérifier que l'allocation dynamique de mémoire est bien réalisée.
6. Donnez `void remove(arbre_mot* a, int* mot, int n)` qui retire à `a` le mot `mot` de longueur `n`. On retirera aussi tout les maillons de l'arbre qui ne sont plus utilisés.
7. Donnez `int distance(arbre_mot* a, int* mot, int n)` qui à un mot associe le nombre minimal de lettres à modifier pour qu'il appartienne à `a`. On retournera $-1$ si il n'y a pas de mot de longueur `n` dans `a`

## Tas binaires

On ce donne en OCaml le type d'arbre suivant :
```ocaml
type tas = F | N of float * int * tas * tas
```
ou si l'on a un nœud `k = N(f,a,g,d)`, alors `a` représente le nombre de nœuds dans l'arbre `k`.
On note $n$ la taille d'un arbre.

1. Rappelez la définition d'un tas binaire. Donnez en C une structure représentant un arbre, et `int hauteur(arbre* arb)` qui à un arbre `arb` lui associe sa hauteur.
2. Donnez en OCaml `val rotg : arbre -> arbre` qui effectue l'opération de rotation gauche.
3. Montrez que si on a un arbre binaire de recherche, il est possible de le convertir en un arbre complet contenant les mêmes entrées. Cela fonctionne-t'il avec les tas ?
4. Donnez en OCaml `val add : arbre -> int -> arbre` qui ajoute à un arbre complet un nœud tel que l'arbre reste complet. On veillera à avoir une complexité de $O(\ln n)$.
5. Donnez en OCaml `val add_tas : arbre -> int -> arbre` qui ajoute à un tas binaire un nœud tel que l'arbre de retour reste un tas. On fera en sorte que la fonction soit en $O(\ln n)$
6. Donnez en OCaml `val rem_tas : arbre -> int -> arbre` qui ajoute à un tas binaire un nœud tel que l'arbre de retour reste un tas. On fera en sorte que la fonction soit en $O(\ln n)$
7. En déduire un algorithme de tri de liste en $O(n\ln n)$.

## Arbres via des tableaux (TODO)

On s'intéresse ici en la représentation d'arbre sous la forme d'un tableau.
On pose la structure suivante :
```c
struct liste {
  int length;
  int* array;
  int hauteur;
};
typedef struct liste liste;
```

1. Donnez en OCaml une définition d'une fonction 
2. Donnez en Ocaml une fonction `val pow : int -> int -> int` qui 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYzMzY1MzgzOSwyODQzNTMxOTcsLTE4MD
Q1OTAwMjcsMjAwMzA5MDYyMSwtMjE3ODcyODcwLDEzNjIxMDMz
NDIsNjcyODU0OTk1LDEyMDg2MzMyMDAsOTEzMjI1Njc1LC0yMT
gxNzYzMDIsLTEwMjQ1ODcyMTQsLTE0OTM3NzIwOSwtMTI4ODQ1
ODEwMSwtMTM2MTgwNTE1NSwtMTE2NTc3MTI2OSwtODExMDc2Nz
I3LC03MzEwMzMxMiw4NjkxMDY5NTcsLTE0OTE0Njk2NTMsMjkz
MDI5M119
-->