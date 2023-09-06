# Résultats de la Compétition du Plus Grand Nombre

Merci à tous d'avoir participé !

Du fait du grand nombre d'entrée ne respectant les règles, deux listes ont été crées: 
- La première, prends les propositions tel quel, applique les règles du concours, et n'hésite pas à disqualifier des entrées.
- Dans la deuxième, je me suis permis d'interpréter les différentes erreurs pour corriger les programmes et donner un classement ou personne n'a été disqualifié.

Cette compétition à été une version plus simple d'une compétition qui a déjà été réalisée, le [BIGNUM BAKEOFF](http://djm.cc/bignum-rules-posted.txt).

Ce document utilise pour comparer les différentes fonctions la [Fast-Growing Hierarchy](https://en.wikipedia.org/wiki/Fast-growing_hierarchy).
Les entrées sont listées avec des explications des bornes obtenues et leur code, de la plus petite (sur la liste secondaire) à la plus grande.
Ensuite, vous avez à la fin du document mon entrée (TREE(n)), ainsi que des ressources dans le domaine de la *gogologie*, la branche de l'informatique théorique / des mathématiques étudiant les grands nombres. Vous aurez aussi des conseils sur comment réduire le nombre de caractères pour un programme donné.

Dans ce document, les $\hat f_{...}$ représentent les fonctions de la [Fast-Growing Hierarchy](https://en.wikipedia.org/wiki/Fast-growing_hierarchy).
Les fonctions des programmes sont dans l'analyse mathématique représentée par le même nom ($f$, $g$, $\text{main}$ etc...)
De plus, $f^n$ représente $n$ évaluations emboitée de $f$ : $f^n(x) = f(f(f(...(x)...)))$ répété $n$ fois.
Je n'ai pas forcément essayée d'avoir les plus belles bornes, juste des bornes suffisantes pour obtenir un classement

Liste principale :
| Entrée  |Borne Inf                      |Borne sup                    |
|---------|-------------------------------|-----------------------------|
|Quentin  |*Disqualifié*                  |*Disqualifié*                |
|Igor     |*Disqualifié*                  |*Disqualifié*                |
|Julien   |*Disqualifié*                  |*Disqualifié*                |
|Carfaure |*Ne termine pas*               |*Ne termine pas*             |
|Thomas   | 0                             |0                            |
|Cornich' | 9                             |9                            |


Liste secondaire:
| Entrée  |Borne Inf                      |Borne sup                    |
|---------|-------------------------------|-----------------------------|
|Thomas   |0                              |0                            |
|Cornich' |9|9                            |
|Quentin  |1495000000  |$\frac{1}{\sqrt{5}}\times2^{1495000001}$|
|Igor     |$\hat f_{3\omega}(2)$|$\hat f_{3\omega+1}(2)$|
|Thomas-2 |$\hat f_{2^{101}\omega}(2)$|$\hat f_{2^{101}\omega^2+1}(2)$  *borne temporaire et large* |
|Julien   |$\hat f_{\omega^2+1}(2)$|$\hat f_{\omega^2+2}(2)$|
|Carfaure |$\sout{\hat f_{\omega^\omega}(2)}$ A REVOIR     |$\sout{\hat f_{\omega^{\omega^\omega}+1}(9)}$ A REVOIR   |

TODO: Il me reste le code de Chloé à juger.
## Cornich (493 caractères)
(code une fois formaté) :
```c
int f(int n, int m, int g) {
  if (n < m) {
    return (f(g * g, n + 1, m));
  } else {
    return (g);
  }
}

int main() {
  return f(
      0,
      f(0,
        f(0, f(0, f(0, f(0, f(0, 9, 9), 9), 9), f(0, f(0, f(0, 9, 9), 9), 9)),
          f(0, f(0, f(0, f(0, 9, 9), 9), 9), f(0, f(0, f(0, 9, 9), 9), 9))),
        f(0, f(0, f(0, f(0, f(0, 9, 9), 9), 9), f(0, f(0, f(0, 9, 9), 9), 9)),
          f(0, f(0, f(0, f(0, 9, 9), 9), 9), f(0, f(0, f(0, 9, 9), 9), 9)))),
      f(0,
        f(0, f(0, f(0, f(0, f(0, 9, 9), 9), 9), f(0, f(0, f(0, 9, 9), 9), 9)),
          f(0, f(0, f(0, f(0, 9, 9), 9), 9), f(0, f(0, 9, 9), 9))),
        f(0, f(0, f(0, f(0, 9, 9), 9), f(0, f(0, 9, 9), 9)),
          f(0, f(0, f(0, 9, 9), 9), f(0, f(0, 9, 9), 9)))));
}
```
On remarque que $f(0,9,9)=f(81,1,9) = 9$
En remplaçant dans le code toutes les occurrences de la chaine de texte `f(0, 9, 9)` par `9` et ceci sept fois, on ce rend compte que ce programme renvoie $9$.
D'ailleurs, en compilant et exécutant ce code, il renvoie le code d'erreur 9.

Il m'est difficile de comprendre les intentions derrière le code, donc je ne l'ai pas modifié pour la liste secondaire, ce qui donne aussi 9 pour la liste secondaire.

## Quentin (163 caractères)
```c
#include <stdio.h>
int main() {

  int i;
  int n = 1495000000;
  int t1 = 0, t2 = 1;
  int nextTerm = t1 + t2;

  for (i = 3; i <= n; ++i) {
    t1 = t2;
    t2 = nextTerm;
    nextTerm = t1 + t2;
  }
  printf("%d, ", nextTerm);
  return 0;
}
```

Cette entré est disqualifié pour l'utillisation d'une librairie.
De plus, même si `printf` - qui ne sert à rien - aurait été utilisable, le code retourne 0.

Le code corrigé de `main` pour la liste secondaire est  :
```c
int main() {
  int i;
  int n = 1495000000;
  int t1 = 0, t2 = 1;
  int nextTerm = t1 + t2;
  for (i = 3; i <= n; ++i) {
    t1 = t2;
    t2 = nextTerm;
    nextTerm = t1 + t2;
  }
  return nextTerm;
}
```
Ce code calcul le `1495000001`ème terme de la suite de Fibonacci.
Si l'on note $F_n$ le n-ème terme de la suite de Fibonacci, alors on a 
$$F_n = \frac{1}{\sqrt5}(\varphi^n-\varphi'^n)\le \frac{1}{\sqrt{5}}\times2^n$$
Avec $\varphi$ le nombre d'or et $\varphi' = -\varphi^{-1}$
Donc on a les bornes $\boxed{1495000000 \le n \le \frac{1}{\sqrt{5}}\times2^{1495000001}}$.

## Thomas (427 caractères)
```c
int max = 0;

int lo(int l,int r){
	int s=r;
	if(l==0)for(int i=0;i<s;i++)r<<=r;
	else for(int i=0;i<s;i++)r=lo(l-1,r);
	return r;
}

int loy(int n){
	return lo(n,n);
}

int fks(int k,int i,int n){
	if(k==0){
		max = loy(max);
		return loy(max);
	}
	if(i==0){
		for(int j=0;j<k;j++) max = fks(j,max,max);
		return max;
	} else if(n==0){
		max = loy(max);
		for(int j=0;j<i;j++) max=fks(k,i-j-1,max);
		return max;
	}
	return fks(k,i-1,fks(k-1,i,n-1));
}

int main(){
	fks(loy(2<<100),loy(2<<100),loy(2<<100));
	return 0;
}
```
Le code renvoie 0.

Le code corrigé de la fonction `main` pour la liste secondaire est  :
```c
int main(){
	return fks(loy(2<<100),loy(2<<100),loy(2<<100));
}
```
**Calcul des bornes:**
On remarque que effectuer l'opération `r<<=r`, c'est exactement faire $r \larr r2^r = \hat f_2(r)$
On a ainsi que $\text{lo}(0,x) = \hat f_2^r(r)=\hat f_3(r)$
On a donc que $\text{lo}(i,x) = \hat f_{3+i}(x)$
Donc $\text{loy}(n) = \hat f_{3+n}(n)\le \hat f_{\omega}(n+3)$ et $\text{loy}(n) \ge \hat f_{\omega}(n)$

L'algorithme est bien parti !
Malheureusement, `max` étant initialisé à 0, et comme `loy(0) = 0`, max est constamment égal à 0.
Si le programme termine, alors il renvoie 0, car les seuls appels non récursifs de `fks` possible sont ceux qui renvoient `max`. Le programme termine car les appels récursif de `fks` sont descendant strict pour la relation d'ordre lexicographique.
Donc le programme renvoie $0$.

Il y a donc eu une deuxième correction (appelée `thomas-2` dans le classement), ou l'on remplace la première ligne par :
```c
int max = 2;
```
**Calcul des bornes:**
On a toujours $\text{loy}(n) = \hat f_{3+n}(n)\le \hat f_{\omega}(n+3)$ et $\text{loy}(n) \ge \hat f_{\omega}(n)$

On pose deux autres fonctions qui encadre la fonction `fks` :
```c
int fks_sup(int k, int i, int n, int max){
	if(k==0){
		return loy(loy(max));
	} else if (i==0) {
		// répéter k fois 
		for(int j=0;j<k;j++) max = fks_sup(k-1, max, max, max);
		return max;
	} else if (n==0) {
		max = loy(max);
		// répéter i fois 
		for(int j=0;j<i;j++) max = fks_sup(k, i-1, max, max);
		return max;
	}
	max = fks_sup(k, i, n-1, max);
	return fks_sup(k, i, n-1, max);
	// supérieur à fks_sup(k, i-1, max, max); car appelle cette
	// fonction dans les sous-appels récursif
}
```
Pour le triplet $(k,i,n)$ on associe l'ordinal $k\omega^2+i\omega+n$
On remarque alors que :
 - si $(k,i,n) \ne (0,0,0)$ alors $\text{fks-sup}_{k\omega^2+i\omega+n}(\text{max}) \le \text{fks-sup}^{\text{max}}_{k\omega^2+i\omega+n-1}(\text{max})$ pour $\text{max}\ge 2$
 - sinon si $(k,i) \ne (0,0)$ alors $\text{fks-sup}_{k\omega^2+i\omega}(\text{max}) \le \text{fks-sup}^{\text{max}}_{k\omega^2+(i-1)\omega+\text{max}}(\text{max})$
 - sinon si $k \ne 0$ alors $\text{fks-sup}_{k\omega^2}(\text{max}) \le \text{fks-sup}^{\text{max}}_{(k-1)\omega^2+\text{max}\omega+\text{max}}(\text{max})$

Donc $\text{fks-sup}$ est inférieur à $\hat f_{k\omega^2+i\omega+n}(\text{max})$ compositions de $\text{loy}^2$.
Précisément, à cause de la façon dont sont faite les conditions, on estimera que (si $\text{max} >1$ et $i,n \ll f_{k\omega^2}(\text{max})$ )
$$
\text{fks-sup}(k,i,n,\text{max}) \le \hat f_{2(\omega+3)+(k-1)\omega^2+(i-1)\omega+n}(\max) = \hat f_{(k-1)\omega^2 + (i+1)\omega+n+6}(\max) \le \hat f_{k\omega^2+1}(\max)
$$

Cette borne est **TRÈS** avantageuse, notamment à cause de la sur-évaluation effectué lors du cas $(k,i,n) \ne (0,0,0)$. La réalité est plutôt de l'ordre de $4\omega(k-1)$ intuitivement.

On encadrera donc $\text{fks}(x,x,x,n)$ par 
$$
\hat f_{x\omega}(n) \le \text{fks-sup}(x,x,x,n) \le  \hat f_{k\omega^2+1}(n)
$$
On a donc notre encadrement *temporaire*:
$$
\boxed{\hat f_{2^{101}\omega}(2) \le \text{main}() \le \hat f_{2^{101}\omega^2+1}(2)}
$$


```c
int fks_inf(int k, int i, int n, int max){
	if(k==0){
		return loy(loy(max));
	} else if (i==0) {
		return loy(loy(max));
	} else if (n==0) {
		max = loy(max);
		for(int j=0;j<i;j++) max = fks_sup(k, i-1, max, max);
		return max;
	}
	max = fks_sup(k-1,i,n-1);
	return fks_sup(k, i-1, max, max);
}
```


## Igor (349 caractères)
```c
typedef int I;

I f(I a,I b,I i){
    if(i==0){return a*b;}
    I r = a;
    for(I j=0;j<b;++j){
        r=f(a,r,i-1);
    }
    return r;
}

I g(I d){
    I c=d;
    for(I j=0;j<d;++j){
        c=f(c,c,c);
    }
    return c;
}

I h(I x,I i){
    if(i==0){return g(x);}
    I y=x;
    for(I j=0;j<x;++j){
        y=h(y,i-1);
    }
    return y;
}

I c(I x,I i){
    if(i==0){return h(x,x);}
    I y=x;
    for(I j=0;j<c(x,i-1);++j){
        y=c(y,i-1);
    }
    return y;
}

I main(void) {
    c(__INT_MAX__,__INT_MAX__);
    return 0;
}
```
Cette entré est disqualifié pour l'utillisation de `__INT_MAX__`.
De plus, même si `__INT_MAX__` aurait été utilisable, le code retourne 0.

Le code corrigé de la fonction `main` pour la liste secondaire est  :
```c
I main(void) {
    return c(99999999999,99999999999);
}
```
**Calcul des bornes :**
On a, dans ce code $f(a,n,x) = a^{\hat f_{x}(n)} \le \hat f_{x+2}(n)$
On a donc, en posant $f'(n)=f(n,n,n)$, le fait que $f'(n)\le \hat f_{n+2}(n+2)$
Cela donne $g(d) = f'^d(d)\le \hat f_{\omega+1}(d+2)$
Si l'on pose $h'(n) = h(n,n)$, on a $h'(n) \le \hat f_{\omega+n+2}(n+2) = \hat f_{2\omega}(n+2)$
Pareillement, si l'on pose $c'(n) = c(n,n)$, on retrouve $c'(n) \le \hat f_{2\omega+n+1}(n+1) = \hat f_{3\omega}(n+1)$ *ici le n+1 viens du fait que la boucle est réalisée $c(x,i-1)$ fois*
On a donc $\text{main}() = c'(99999999999) \le \hat f_{3\omega}(100000000000)\boxed{\le \hat f_{3\omega+1}(2)}$

Par un raisonnement similaire, on estimera donc que $\boxed{\hat f_{3\omega}(2) \le \text{main}()  \le \hat f_{3\omega+1}(2)}$
## Julien
Code (python):
```py
def compound(x,a,b,n):
    if n==1:
        return rec(x,a,b)
    else:
        return compound(rec(x,a,b),a,b,n-1)

def rec(x,a,b):
    if b==0:
        if a==0:
            return x+1
        else:
            return compound(x,a-1,b,x)
    else:
        if a==0:
            return rec(x,x,b-1)
        else:
            return compound(x,a-1,b,x)
            
def bc(x):
    if x==1:
        return rec(x,x,x)
    else:
        return rec(bc(x-1),bc(x-1),bc(x-1))
        
print(bc(pow(999,999)))
```
Par l'utillisation du python (il ne connaissait pas le C), l'entrée est disqualifié.
Le code analysé pour la liste secondaire (à 365 caractères), transformé par ChatGPT (pour éviter d'introduire un biais personnel quelconque):
```c
int compound(int x, int a, int b, int n) {
    if (n == 1) {
        return rec(x, a, b);
    } else {
        return compound(rec(x, a, b), a, b, n - 1);
    }
}

int rec(int x, int a, int b) {
    if (b == 0) {
        if (a == 0) {
            return x + 1;
        } else {
            return compound(x, a - 1, b, x);
        }
    } else {
        if (a == 0) {
            return rec(x, x, b - 1);
        } else {
            return compound(x, a - 1, b, x);
        }
    }
}

int bc(int x) {
    if (x == 1) {
        return rec(x, x, x);
    } else {
        return rec(bc(x - 1), bc(x - 1), bc(x - 1));
    }
}

int main() {
    return bc(999*999);
}
```

**Calcul des bornes :**
Ici, on remarque que $\text{compound}(x,a,b,n)$ calcule $\text{rec}(\text{rec}(...(x)...,a,b),a,b)$, ou autrement dit, $\text{rec}^n_{a,b}(x)$
Dans le cas de $b=0$, on a $\text{rec}(x,a,b) = \hat f_a(x)$ *exactement*
On a donc $\text{rec}(x,a,b)=\hat f_{b.\omega+a}(x)$ *exactement*
On pose $\text{rec}'(n) = \text{rec}(n,n,n)$
On a ainsi $\hat f_{n.\omega}(n)\le \text{rec}'(n) =\hat f_{n.\omega+n}(n) \le \hat f_{(n+1).\omega}(n+1)=\hat f_{\omega^2}(n+1)$

Donc on a $\text{bc}(x) = \text{rec}'^x(1)\le \hat f_{\omega^2}^{x}(2)= \hat f_{\omega^2}^{x+1}(1) \le \hat f_{\omega^2+1}(x+1)$
Et l'on a aussi $\text{bc}(x) \ge \hat f_{\omega^2}^{x}(1) \ge f_{\omega^2+1}(2)$ (pour $x>2)$

Finalement, comme $\text{main()} = \text{bc}(999^2)$, cela nous donne les bornes :
$$\boxed{f_{\omega^2+1}(2) \le\text{main()} \le \hat f_{\omega^2+1}(1000000)\le \hat f_{\omega^2+2}(2)}$$
## Carfaure (500 caractères)
```c
#define w int
#define g return
w *z(w *t, w n, w p, w k) {
  w *j = malloc(n * 4);
  for (w i = 0; i < n; i++) {
    j[i] = i == p ? k : t[i];
  }
  g j;
}

w e(w *t, w n, w i) {
  g i ? t[i] ? e(z(z(t, n, i - 1, e(z(t, n, i - 1, t[i - 1] - 1), n, n - 1)), n,
                   i, t[i] - 1),
                 n, n - 1)
             : e(t, n, i - 1)
  : t[0] ? t[0] * e(z(t, n, 0, t[0] - 1), n, n - 1)
         : 9;
}

w y(w n) {
  w *j = calloc(n, 4);
  j[n - 1] = n;
  g e(j, n, n - 1);
}

w f(w *t, w n, w i) {
  g i ? t[i] ? f(z(z(t, n, i - 1, f(z(t, n, i - 1, t[i - 1] - 1), n, n - 1)), n,
                   i, t[i] - 1),
                 n, n - 1)
             : f(t, n, i - 1)
      : y(t[i]);
}

w v(w n) {
  w *j = calloc(n, 4);
  j[n - 1] = n;
  g f(j, n, n - 1);
}

w u(w z, w y) { g y ? z ? u(u(z - 1, y), y - 1) : u(9, y - 1) : v(z); }

w main(void) { g u(9, u(9, 9)); }
```
Le code d'explication est celui-ci :
```c
#include <stdio.h>
#include <stdlib.h>

int a(int n) { // n!
  return n ? n * a(n - 1) : 1;
}

int b(int n) { // 9 puis n fois !
  return n ? a(b(n - 1)) : a(9);
}

int c(int n) { // b(b(b(b(b(b(b(...))))))) avec n fois b
  return n ? b(c(n - 1)) : b(9);
}
//...

// apres generalisation :
int d(int z, int y) { // si y=0 alors a(z) si y=1 alors b(z) si y=2 alors c(z)
                      // etc... meme principe que ackermann
  return y   ? (z ? d(d(z - 1, y), y - 1) : d(9, y - 1))
         : z ? z * d(z - 1, 0)
             : 9;
}

// apres generalisation :
int *copy_modif(int *t, int n, int p, int k) { // copy t et fait copie[p]=k
  int *j = malloc(n * sizeof(int));
  for (int i = 0; i < n; i++) {
    j[i] = i == p ? k : t[i];
  }
  return t;
}

int e2(int *t, int n) { // t[0] est z et t[1] est y dans d
  for (int i = n - 1; i > 0; i--) {
    if (i == 0) {
      return t[0]; // mis en factorielle
    } else {
      if (t[i] != 0) {
        return e2(
            copy_modif(copy_modif(t, n, i - 1,
                                  e2(copy_modif(t, n, i - 1, t[i - 1] - 1), n)),
                       n, i, t[i] - 1),
            n);
      }
    }
  }
}
// z est copymodif et e est e2 réecrit
```
Dans le code d'explication :
- $a(n) =n!<n^n\le \hat f_3(n)$
- $b(n) = a^n(9) \le f_3^n(9) \le f_3^n(n) \le f_4(n)$
- $c(n) = c^n(9) \le f_4^n(9) \le f_4^n(n) \le f_5(n)$
- $d(n,0) = n!$ et $d(n,e) = d_{k=e-1}^n(9) \le d_{k=e-1}^n(n) \le \hat f_{k+3}(n)$
- `copy_modif` n'est pas bon dans le code d'explication, mais est bon dans le code soumis et est la fonction `z`
- si $n=1$, `e2` ne retourne rien. Le cas `i==0` n'arrive jamais. Cette erreur est corrigé dans le code soumis.

Analyse du code soumis :
- `e` cherche le dernier `i` tel que `t[i] != 0`
- `e([n,0,...,0],_,_)` $= n!$
- Ce programme ne s’arrête pas : on a que `e([x,1], 2, 1)` appelle `e(z([x,1], 2, 0, t[0]-1 ), 2, 1)` qui donne `e([x-1,1], 2, 1)` qui appelle `e([x-2,1], 2, 1)` etc...

Or `e` est appelé avec un tableau non trivial. Donc il ne termine pas. 

On corrige pour la liste secondaire la ligne
```c
  g i ? t[i] ? e(z(z(t, n, i - 1, e(z(t, n, i - 1, t[i - 1] - 1),
  n, n - 1)), n,
```
en 
```c
  g i ? t[i] ? e(z(z(t, n, i - 1, e(z(t, n, i, t[i] - 1),
  n, n - 1)), n,
```
On corrige aussi cette ligne dans `f`.
> Dans ce cas, on a que, si on appelle $x$ le dernier élément de $t$ (et qu'il est non nul): 
$$
\hat f _ {\omega^{|t|}} (9) \le e(t,|t|,|t|-1) \le \hat f _ {(x+1)\omega^{|t|}+3} (9)
$$
>
> On a donc $\hat f_{\omega^\omega}(n-1)=\hat f _ {\omega^{n-1}} (n-1) \le \hat f _ {\omega^{n}} (9) \le y(n) \le \hat f _ {(n+1)\omega^{n}+3} (9) \le \hat f _ {\omega^{n+1}} (n+1) = \hat f_{\omega^\omega}(n+1)$ (pour $n>1$)
>$y$ diagonalise donc les $\hat f_{\omega^i}$, donc est une implémentation de $\hat f_{\omega^\omega}$ !
>
>On a donc que $\hat f_{\omega^\omega}(k-1) \le$ `f([k,0,...,0],_,_)` $\le \hat f _ {\omega^\omega} (k+1)$
>
>Dans ce cas, on a que, si on appelle $x$ le dernier élément de $t$ (et qu'il est non nul): 
>$$
f(t,|t|,|t|-1) \le v(\hat f _ {x\omega^{|t|}} (9)) \le \hat f_{\omega^\omega}(\hat f_{\omega^\omega} (n+1)+1) \le \hat f_{\omega^\omega+1}(n)
$$
et 
$$
f(t,|t|,|t|-1) \ge y(\hat f _ {(x+1)\omega^{|t|}+3} (9)) \le \hat f_{\omega^\omega}(\hat f _ {(x+1)\omega^{|t|}+3} (9))
$$

Problème dans le calcul de la borne supérieure fait au dessus : 
Le problème dans ce code est que, quelquesoit les calculs précédemment effectué, (A continuer, mais ce code est au final de l'ordre de $\hat f_\omega(n)$ ) TODO

## Chloé (500 caractères)
```c
int Z(int a, int *t, int n, int k, int *s, int l) {
  int *u = malloc(4 * n);
  for (int i = 0; i < n; i++)
    u[i] = n - k       ? k - i ? t[i] : t[i] - 1
           : n - 1 - i ? E(a, Z(a, t, n, n - 2, s, l), n, s, l)
                       : t[i] - 1;
  return u;
}

int E(int a, int *t, int n, int *s, int l) {
  return n - 1 ? t[n - 1] ? t[n - 2] ? E(a, Z(a, t, n, n, s, l), n, s, l) : a
                          : E(a, t, n - 1, s, l)
               : N(a, t[0], Z(a, s, l, 0, s, l), l, l);
}

int N(int a, int b, int *s, int l, int k) {
  int *t = malloc(4 * b);
  for (int i = 0; i < b; i++)
    t[i] = a;
  return l ? k ? s[k - 1] ? N(a, b, s, l, k - 1)
                 : l - k  ? N(a, b, Z(a, s, l, k, s, l), l, k)
                          : N(a, b, s, l - 1, k)
               : E(a, t, b, s, l)
           : a * b;
}

int main() {
  int s[999] = {9};
  return N(9, 99, s, 999, 999);
}
```
Le code d'explication peut être trouvé [ici](https://raw.githubusercontent.com/Cypooos/CPGN-2023/main/2023/Chlo%C3%A9/chall_cyp2.c?token=GHSAT0AAAAAACFXSPRTKWK4H447HHV6GBSYZG443XQ) (trop long pour ce pdf)
 TODO
 
 ## Tree(n)
 
 Version explicative :
 ```c
#define bool int
#define true 1
#define false 0

// bijective pairing
int pair(int a, int b) { return ((a << 1) | 1) << b; }
int get_b(int couple) { return couple & 1 ? 0 : 1 + get_b(couple >> 1); }
int get_a(int couple) { return couple >> (1 + get_b(couple)); }

// a node is the couple (X, (N, (A,(B,(C,...(D,E)...)) with X the color (!= 1)
// and N the number of sons. A,B,...,E are the sons
//
// an end is 0, aka not a couple (a couple must contain a 1 in the binary
// notation)
int get_color(int tree) { return get_a(tree); }
int get_nb(int tree) { return get_a(get_b(tree)); }
int get_son(int tree, int n) {
  return n == 0 ? get_a(get_b(get_b(tree))) : get_son(get_b(tree), n - 1);
}
int remove_son_inner(int tree_inner /* without the X and N pairs */, int n) {
  if (n == 0) {
    return get_b(tree_inner);
  }
  int recu = remove_son_inner(get_b(tree_inner), n - 1);
  return pair(get_a(tree_inner), recu);
}
int remove_son(int tree, int n) { // inline ?
  return pair(get_color(tree),
              pair(get_nb(tree) - 1, remove_son_inner(get_b(get_b(tree)), n)));
}
int add_son(int tree, int son) {
  return pair(get_color(tree),
              pair(get_nb(tree) + 1, pair(son, get_b(get_b(tree)))));
}
int is_empty(int tree) { return !tree; }
int get_size(int tree) {
  return is_empty(tree) || !get_nb(tree)
             ? 0
             : get_size(get_son(tree, 0)) + 1 + get_size(remove_son(tree, 0));
}

void print_bin(int x) {
  if (x > 1) {
    print_bin(x >> 1);
  }
  printf("%d", x & 1);
}

// search for tree_to_find as a subtree of main_tree starting at a height of
// at_height. return true if found - false if not -
// if at_height is negative it means we need to test all sons of tree_to_find
// from the same node at the heigh -at_height
// h(main_tree) <= height_borne_max
bool is_in(int main_tree, int tree_to_find, int at_height,
           int height_borne_max) {
  if (is_empty(tree_to_find) || (get_nb(tree_to_find) == 0 && at_height < 0)) {
    return true;
  }
  if (is_empty(main_tree)) {
    return false;
  }

  // if height > 0 test if we found one at a certain bigger height sup
  if (at_height > 0) {
    for (int i = 0; i < get_nb(main_tree); i++) { // test all sons
      if (is_in(get_son(main_tree, i), tree_to_find, at_height - 1,
                height_borne_max - 1)) {
        return true;
      }
    }
  }

  // if height < 0 we need to test sons at -height (we have at least one)
  if (at_height < 0) {
    int son_to_test = get_son(tree_to_find, 0);
    int new_tree = remove_son(tree_to_find, 0);
    for (int son_i = 0; son_i < get_nb(main_tree); son_i++) {
      if (is_in(get_son(main_tree, son_i), son_to_test, -at_height,
                height_borne_max) &&
          is_in(remove_son(main_tree, son_i), new_tree, at_height,
                height_borne_max)) {
        return true;
      }
    }
    return false;
  }

  // need for color to be good
  if (get_color(main_tree) != get_color(tree_to_find)) {
    return false;
  }

  // test all sons at all possible heights recursively (we have at least one to
  // do)
  for (int h = 1; h < height_borne_max; h++) {
    if (is_in(main_tree, tree_to_find, -h, height_borne_max)) {
      return true;
    }
  }
  return false;
}

int iterate(int *table, int *trees, int n, int nb_trees, int colors) {
  // will be transformed to malloc(n*8) bc n*4*2 >= (n+1)*4 (for n>0)
  int *table2 = malloc(n * 4 + 4);
  int *trees2 = malloc(nb_trees * nb_trees);
  for (int i = 0; i < n; i++) {
    table2[i] = table[i];
    trees2[i] = trees[i];
  }
  
  // get all k-colored tree with <=n vertices
  for (int i = 0; i < nb_trees; i++) {
    for (int j = 0; j < nb_trees; j++) {
      int to_add = add_son(trees[i], trees[j]);
      trees2[(i + 1) * nb_trees + j] = get_size(to_add) > n ? 1 : to_add;
    }
  }

  // recursive call
  int c = 1;
  for (int i = 0; i < nb_trees * nb_trees; i++) {
    int call_recur = true;
    for (int j = 0; j < n; j++) {
      for (int h = 0; h < n; h++) {
        call_recur &= !is_in(table[j], table[n], h, n);
      }
    }
    if (call_recur) {
      c += iterate(table, trees2, n + 1, nb_trees * nb_trees, colors);
    }
  }
  return c;
}
int TREE(int k) {
  int *init_trees = malloc((k + 1) * 4);
  for (int i = 1; i <= k; i++) {
    init_trees[i] = pair(i, pair(0, 1));
  }
  init_trees[0] = 1;
  return iterate(0, init_trees, 0, k + 1, k);
}

int main(void) {
  return TREE(3);
}
```

version optimisé (malheureusement, + de 500 caractères) :
TODO: petite problème de transpileur, une variable `c` est redéfinie...
TODO: utiliser ternaire + récursion pour optimiser les boucles
```c
#define I int
#define T if
#define O for
#define H malloc
#define R return
I P(I a, I b) { R ((a << 1) | 1) << b; }I B(I c) { R c & 1 ? 0 : 1 + B(c >> 1);
}I A(I c) { R c >> (1 + B(c)); }I C(I t) { R A(t); }I N(I t) { R A(B(t)); }I G(I
t, I n) {R n ? G(B(t), n - 1) : A(B(B(t)));}I _(I t, I n) {R n ? P(A(t), _(B(t),
n - 1)): B(t);}I M(I t, I n) {R P(C(t),P(N(t) - 1, _(B(B(t)), n)));}I S(I t) {R t
&& N(t)? S(G(t, 0)) + 1 + S(M(t, 0)): 0;}I E(I t, I f, I h,I b) {T (!f || (N(f)
== 0 && h < 0)) {R 1;}T (!t) {R 0;}T (h > 0) {O (I i = 0; i < N(t); i++) {T(E(G(
t, i), f, h - 1,b - 1)) {R 1;}}}T (h < 0) {I s = G(f, 0);I a = M(f, 0);O (I s =
0; s < N(t); s++) {T (E(G(t, s), s, -h,b) &&E(M(t, s), a, h,b)) {R 1;}}R 0;}T
(C(t) != C(f)) {R 0;}O (I h = 1; h < b; h++) {T (E(t, f, -h, b)) {R 1;}}R 0;}I
F(I *l, I *t, I n, I m, I c) {I *q = H(n * 8);I *u = H(m * m);O (I i = 0; i < n;
i++) {q[i] = l[i];u[i] = t[i];}O (I i = 0; i < m; i++) {O (I j = 0; j < m; j++)
{I p = P(C(t[i]),P(N(t[i]) + 1, P(t[j], B(B(t[i])))));u[(i + 1) * m + j] = S(p) >
n ? 1 : p;}}I c = 1;O (I i = 0; i < m * m; i++) {I b = 1;O (I j = 0; j < n; j++)
{O (I h = 0; h < n; h++) {b &= !E(l[j], l[n], h, n);}}T (b) {c += F(l, u, n + 1,
m * m, c);}}R c;}I Y(I k) {I *l = H(k * 8);O (I i = 1; i <= k; i++) {l[i] = P(i,
P(0, 1));}l[0] = 1;R F(0, l, 0, k + 1, k);}I main(void) { R Y(3); }
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4NzQyNDg3MywxNTI3ODgyMzgzLC0yMD
QzMDI3OTY3LDc0ODY5NzgxMSwtNTkzMDIyMDIzLDU2MzA1NTc3
MSwzODc3Mjk1MzcsNTk0NjQwNDAsMjE0MDg5MTQ4NCwxNDgxOT
YzOTgsLTE3NzcxOTUwMTUsLTUxNDA1MTU5MCw1NzAwMjI1MjIs
NzA4Mzg5MzExLC0yNjQxMTAzMSwtNDgwNDA5MjgyLC0xNzQyMj
g1MTMzLC04NDY1MDQ1MTYsLTIwMDE4MzUwNzgsMTQxNzM5ODQ4
MV19
-->