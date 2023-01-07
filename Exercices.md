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
\*\*\*\* = Question ouverte

## AL-001***
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

## T-003*** /!\ TODO
On appelle fonctions de base les fonctions suivantes :
1. la fonction constante 0, notée $Z : \N → \N$, et définie par Z(x) = 0
2. la fonction successeur S : N → N , définie par S(x) = x + 1
3. les fonctions de projection π n i : N n → N définies pour 0 ≤ i < n ∈ N par π n i (x0, . . . , xn−1) = x
Soit $\mathcal{C}_0$ la classe des fonctions de base, et étant donné Cs, soit Cs+1 la classe qui contient les fonctions de Cs, et telle que pour tous n, k ∈ N, pour toutes fonctions g0, . . . , gn−1 ∈ Cs de type N k → N et toute fonction f ∈ Cs de type N n → N, la fonction h : N k → N définie par h(x0, . . . , xk−1) = f(g0(x0, . . . , xk−1), . . . , gn−1(x0, . . . , xk−1)) appartient à Cs+1. Soit C∞ = S s Cs la plus petite classe de fonctions contenant les fonctions de base, et close par l’opération de composition définie ci-dessus.

## M-003**
On essaye de coder un serveur pour un jeu vidéo de combat.
Nous avons besoin du comportement suivant : 
 - Les joueurs se connecte à un lobby commun.
 - Quand une des $k$ arènes se libère, les $n$ joueurs prioritaires y sont envoyés.
 - Les joueurs quand ils perdent se déconnectent un à un de leur arène et retourne au lobby.

Chaque joueur sera représenté par un fil d’exécution.
Proposer une architecture utilisant des sémaphores pour implémenter.

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
eyJoaXN0b3J5IjpbLTExNDA3OTU5MjZdfQ==
-->