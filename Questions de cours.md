## S-001
> Oraux J1 Ulm 2021

1) Rappeler ce qu’est un arbre binaire de recherche.
2) Quelle en est l’utilité ? 
3) Donner le pseudo-code de la fonction d’insertion dans un arbre binaire de recherche. 
4) Discuter de sa complexité en temps.

## S-002
> Oraux J2 Ulm 2021
1) Différence entre structure de donnée persistante et impérative
2) Définition d'une file
3) Implémentation d'une file persistante en ocaml 
4) Déduire implémentation impérative

## S-003*
> Oraux A3 - Q5 Ulm 2021

Proposer une structure de données pour stocker un ensemble d’entiers S qui supporte les opérations suivantes :
  — Ajouter un entier dans S, en O(1);
  — Retirer un entier de S, en O(1);
  — Parcourir les entiers actuellement stockés dans S, en O(|S|).

On suppose que les entiers en question sont tous entre 0 et M.

Écrire le pseudocode pour ces opérations.

## S-004
> Oraux P2 - Ulm 2021

Donner le pseudo-code de l’algorithme de Dijkstra pour calculer la plus courte distance d’un nœud source à un nœud destination dans un graphe avec des poids positifs ou nuls.
Le pseudo-code devra utiliser une file de priorité.
Quelle est la complexité en terme du nombre $n$ de nœuds et $m$ d’arêtes du graphe, ainsi que de la complexité des opérations de la file de priorité utilisée ?

Quelle est la complexité de l’algorithme de Dijkstra si on utilise un tas binaire ?

## S-005
> Oraux P3 Ulm 2021

On considère $n$ objets décrits par des suites finies de bits, c.-à-d., par des mots de $\{0, 1\}^*$ . On fixe $k ∈ \N^*$. Une fonction de hachage est une fonction $h : \{0, 1\}^* \to [\![0;2^{k-1}]\!]$ associant à chaque suite finie de bits un entier entre $0$ et $2^{k-1}$.

Donner le pseudo-code des opérations de base sur les tables de hachage : rechercher si un élément est dans l’ensemble, ajouter un élément, en supprimer un.

Donner la complexité de ces fonctions en fonction de $n$ et de $k$ dans le pire des cas. Donner la complexité en moyenne de ces fonctions si on suppose que h répartie équitablement les éléments dans $[\![0;2^{k-1}]\!]$

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg4MDMxNDc5OCw4MDUxNDg2ODUsLTE4Nz
cxMjAxMjhdfQ==
-->