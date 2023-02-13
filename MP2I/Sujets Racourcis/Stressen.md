
## Multiplication de matrices
 Donnez en Ocaml le code de
```ocaml
val mul: int array array -> int array array -> int array array
```
qui calcule le produit de deux matrices de manière naïve si c'est possible, et qui `failwith` sinon.
Quelle est sa complexité ?

## Récursivement
Soit $\Gamma,\Delta \in \mathcal{M}_n$ des matrices, on effectue la décomposition par bloc :
$$
\Gamma = \begin{pmatrix}
A & B \\
C & D 
\end{pmatrix},\ \Delta = \begin{pmatrix}
W & X  \\
Y & Z
\end{pmatrix}
$$

Donnez en pseudo-code une fonction récursive en $O(n^3)$ qui calcule $\Gamma\times \Delta$
Quels sont les 8 sous-produits que l'on a effectué ?

## Algorithme de Stressen

On pose les produits suivant :
$$
\begin{align*}
&M_1 = (A+D)(W+Z) \\
&M_2 = (C+D)W \\
&M_3 = A(X-Z) \\
&M_4 = D(Y-W)\\
&M_5 = (A+B)Z \\
&M_6 = (C-A)(W+X) \\
&M_7 = (B-D)(Y+Z) \\
\end{align*}
$$
Donnez $\Gamma \times \Delta$ en fonction des $(M_i)_i$
Modifier l'algorithme pour qu'il n'effectue que 7 sous-produits. Quelle est la nouvelle complexité ?



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMwNDI2OTE5XX0=
-->