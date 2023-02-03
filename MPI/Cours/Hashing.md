## Hashing
> Oraux P3 Ulm 2021

On considère $n$ objets décrits par des suites finies de bits, c.-à-d., par des mots de $\{0, 1\}^*$ . On fixe $k ∈ \N^*$. Une fonction de hachage est une fonction $h : \{0, 1\}^* \to [\![0;2^{k-1}]\!]$ associant à chaque suite finie de bits un entier entre $0$ et $2^{k-1}$.

Donner le pseudo-code des opérations de base sur les tables de hachage : rechercher si un élément est dans l’ensemble, ajouter un élément, en supprimer un.

Donner la complexité de ces fonctions en fonction de $n$ et de $k$ dans le pire des cas. Donner la complexité en moyenne de ces fonctions si on suppose que $h$ répartie équitablement les éléments dans $[\![0;2^{k-1}]\!]$
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MzA4NTI4MjldfQ==
-->