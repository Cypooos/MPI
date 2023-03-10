EN COURS
Source : Exercice oral A3 de l'ens Ulm 2021 https://a3nm.net/work/exams/ens/exercices_info_ulm_2021.pdf

# Maintenance incrémentale de langages réguliers  

## Question 0
Si l’on fixe un langage régulier  $L \sube \Sigma^*$, le problème d’appartenance à $L$ est de déterminer, étant donné en entrée un mot $\omega \in\Sigma^*$, si $\omega \in L$. Quelle est la complexité du problème d’appartenance à $L$ en fonction de la longueur du mot d’entrée ?

## Question 1
Ce sujet s’intéresse à la *complexité incrémentale* du problème d’appartenance à un langage régulier $L$.
Dans ce problème, on reçoit en entrée un mot $\omega \in\Sigma^*$ de longueur $n$. On effectue d’abord un pré-traitement pour déterminer si $\omega\inL$ et pour construire si on le souhaite une structure de données auxiliaire : cette phase de pré-traitement doit s’exécuter en $O(n)$. Ensuite, on reçoit des *mises à jour*, c’est-à-dire des paires $(i, a)$ pour $1\le i\le n$ et $a\in\Sigma$, données l’une après l’autre. À chaque mise à jour, on modifie le mot $\omega$ pour que sa $i$-ème lettre devienne $a$, et on doit déterminer si $\omega \in L$ après cette modification. La longueur $n$ du mot ne change jamais. La *complexité incrémentale* d’un langage est la complexité dans le pire cas pour prendre en compte une mise à jour, exprimée en fonction de $n$.

Montrer que tout langage régulier a une complexité incrémentale en $O(n)$.

## Question 2
Montrer que le langage régulier $a^*$ sur l’alphabet $\Sigma = \{a, b\}$ a une complexité incrémentale en $O(1)$.
## Question 3
Soit  $L_3$  le langage des mots sur l’alphabet $\Sigma = \{a, b\}$ : 
- Comportant au moins deux $a$,
- Un nombre pair de $a$,
- Un nombre de $b$ qui n’est pas divisible par 3.

Ce langage est-il régulier ? Quelle est sa complexité incrémentale ?
## Question 4
On dénote par $\omega_1, ... , \omega_n$ les lettres d’un mot $\omega\in\Sigma^*$ de longueur $n$. Pour toute permutation  σ  :  {1, . . . , n} → {1, . . . , n}, on écrit par abus de notation  σ(w)  pour désigner le mot  
wσ(1)  · · ·  wσ(n). Un langage  L  est  commutatif  si pour tout  w  ∈  Σ∗, pour  n  la longueur de  w, pour toute  
permutation  σ  :  {1, . . . , n} → {1, . . . , n}, on a  w  ∈  L  si et seulement si  σ(w)  ∈  L.  
Montrer que tout langage régulier commutatif a une complexité incrémentale en  O(1).  
Question 5.  Proposer une structure de données pour stocker un ensemble d’entiers  S  qui supporte  
les opérations suivantes :  
— Ajouter un entier dans  S, en  O(1)  ;  
— Retirer un entier de  S, en  O(1)  ;  
— Parcourir les entiers actuellement stockés dans  S, en  O(|S|).  
Écrire le pseudocode pour ces opérations.  
Question 6.  On considère le langage  L6  sur l’alphabet  Σ =  {a, b, c}  dénoté par l’expression rationnelle  
c∗ac∗bc∗. Montrer que sa complexité incrémentale est  O(1)  en utilisant la structure de données de la  
question précédente.

Suite des questions  
Question 7.  À quelle classe de langages peut-on généraliser cette technique ?  
Question 8.  Soient deux langages  L1  et  L2  de complexité incrémentale en  O(1). Quelle est la com-  
plexité incrémentale des langages  L1  ∩  L2  et  L1  ∪  L2  ?  
Question 9.  On s’intéresse aux langages réguliers admettant au moins une “lettre neutre” (notion  
que le candidat ou la candidate aura dû identifier à la question 7). Proposer une classe aussi générale  
que possible de langages de complexité incrémentale en  O(1).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NTIxMTQ0NjUsLTE1MDM1MzAxMDgsND
YxOTAxMjU2XX0=
-->