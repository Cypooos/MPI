On fixe un ensemble $X = \{x_1, ... , x_n\}$ de variables booléennes.

Un *diagramme de décision* $D$ sur $X$ est la donnée d’un graphe orienté $(V, E)$, supposé sans cycle, d’un nœud initial $v_i \in V$, d’une partition de $V$ en $V =  V_0 \sqcup V_1 \sqcup V'$, d’une partition de $E$ en $E = E_0 \sqcup E_1$, et d’une fonction $μ : V' \to X$, de sorte que:
1) Aucun nœud  $v \in V_0$ ou $v \in V_1$ n’a d’arête sortante, i.e., il n’existe aucun $w \in V$ tel que $(v, w) \in E$ ;
2) Tout nœud $v \in V'$ a exactement une arête sortante dans $E_0$ et une arête sortante dans $E_1$, i.e., il existe exactement un $w_0 \in V$ et exactement un $w_1 \in V$ tels que $(v, w_0) \in E_0$ et $(v, w_1) \in E_1$.

Si on se donne une *valuation* $\nu :  X \to \{0, 1\}$, le diagramme de décision $D$ associe $\nu$ à une valeur $b \in \{0, 1\}$ obtenue comme suit :
1) On initialise le nœud courant par $v := v_i$
2) Tant que le nœud courant $v$ est dans $V'$ alors on remplace $v$ par $v := w_0$ ou $v := w_1$ comme défini ci-dessus selon la valeur de $\nu(μ(v))$
2) Une fois que $v\in V_0$ ou $v \in V_1$ alors on renvoie $0$ ou $1$ suivant le cas.

## Question 0
On considère $X = \{x_1, x_2, x_3, x_4\}$ et le diagramme $D0  suivant, où on indique dans  
chaque nœud la valeur de  μ  ou l’appartenance à  V0  ou  V1, et on indique le nœud initial par une flèche :  
x1  
x3  
x2  
0  
1  
0  
1  
0  
1  
1  
0  
À quelle valeur est associée la valuation qui envoie  x1, x2, x3, x4  respectivement vers  1,  1,  0,  1  ? vers  
0,  1,  0,  0  ?  
Question 1.  Donner une formule logique décrivant la fonction booléenne représentée par  D0.  
Question 2.  Si on se donne une formule logique  φ, on dit que  D  représente  φ  si  φ  est la fonction  
booléenne qu’il décrit. Donner un diagramme de décision  D2  représentant la fonction  ¬(x1  ∧  x2)  ∨  x3  
Question 3.  La  profondeur  d’un diagramme de décision est la plus grande longueur possible d’un che-  
min orienté à partir du nœud initial, en comptant le nombre de nœuds de  V  ′  traversés (y compris  vinit).  
Décrire la profondeur du diagramme  D0  et celle du diagramme  D2.  
Question 4.  Peut-on avoir deux diagrammes de décision de profondeurs différentes qui représentent  
une même formule logique ?  
Question 5.  On appelle  profondeur minimale  d’une fonction booléenne  φ  la plus petite profondeur  
possible pour un diagramme de décision représentant  φ.  
Quelle est la profondeur minimale de la fonction identifiée en question 1 ?  
Question 6.  Une fonction booléenne  φ  sur  n  variables est dite  évasive  si sa profondeur minimale est  
de  n. Donner un exemple d’une famille infinie de fonctions évasives, et justifier.  
Question 7.  On considère, pour tout  n  ≥  1, la fonction booléenne  ψn  définie par la formule  (x0  ∧  
x1)  ∨  (x1  ∧  x2)  ∨  (x2  ∧  x3)  ∨ · · · ∨  (xn−1  ∧  xn). Ces fonctions sont-elles évasives ? Justifier.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwNDAwMDgxNl19
-->