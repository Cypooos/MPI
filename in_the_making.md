# Exercices

Exercices extrait d'oraux et autre.

A : Automates
L : Logique
S : Structure de donnée
P : Programmation
M : Multi-threading / Mutex / Sémaphore
T : Théorique
C : Cours
! = à savoir, mais pas du cours 

\* = Exercice facile
\*\* = Exercice moyen
\*\*\* = Exercice difficile
\*\*\*\* = Question ouverte / Exercice hardcore

## A-001***
> Oraux A2 - Ulm 2021

La densité de $L$ un langage est la fonction $δ_L: \N \to \N$ où $δ_L(n) := |L \cap Σ^n |$ pour $n ∈ \N$. On dit que $L$ est épars si on a $δ_L = O(P(n))$ pour un polynôme $P$.

### Question 1
Donner un exemple d’un langage régulier épars, et d’un langage régulier non-épars.
### Question 2
Proposer une condition suffisante et nécessaire sur un automate fini pour que le langage accepté par l’automate ne soit pas épars.
### Question 3
Écrire le pseudocode d’un algorithme naïf pour tester le critère de la question 2 sur un automate fourni en entrée, et discuter de sa complexité.

## S!-002**
On prend un groupe de n amis.
Montrez que 2 personnes ont au moins autant d'amis en commun dans ce groupe.




## M-003**



## M-004*
Dans une école, on essaye de concevoir des classes.
Il y a $p$ classes d'informatiques.
Chaque classe contiens $n$ élèves.

On représentera chaque élève par un fil numéroté par $i$. La fonction `niveau(i:int)` prend un temps proportionnel au niveau de l'élève $i$ à exécuter.

Formez des classes de niveaux à l'aide de sémaphore.

## M-005*
On fixe un tableau d'entier global $T$ de taille `n`
On ce donne deux fonctions `f: int -> int` et `g: int -> int`.
On cherche à calculer $T$ tel que $T[i] = g(f(i))$ ou la fonction $f$ n'est évalué que par un fil et la fonction $g$ par un autre.
Proposer une méthode avec des mutex et sémaphore. 

## 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU0Nzk1NjMzNl19
-->