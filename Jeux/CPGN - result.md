# Résultats de la Compétition du Plus Grand Nombre

Merci à tous d'avoir participé !

Du fait du grand nombre d'entrée ne respectant les règles, deux listes ont été crées: 
- La première, prends les propositions tel quel, applique les règles du concours, et n'hésite pas à disqualifier des entrées.
- Dans la deuxième, je me suis permis d'interprété les différentes erreurs pour corriger les programmes et donner un classement ou personne n'a été disqualifié.

Ce document commence par une introduction de la [Fast-Growing Hierarchy](https://en.wikipedia.org/wiki/Fast-growing_hierarchy), une méthode utilisé pour comparer des fonctions grandissant vite et définies par récurrence.
Les entrée sont listé avec des explications des bornes obtenues et leur code, de la plus petite (sur la liste principale) à la plus grande.
Ensuite, vous avez à la fin du document mon entrée (TREE(3)), ainsi que des ressources dans le domaine de la *gogologie*, la branche de l'informatique théorique / des mathématiques étudiant les grands nombres. Vous aurez aussi des conseils sur comment réduire le nombre de caractères pour un programme donné.

Dans ce document, les $\hat f_{...}$ représentent les fonctions de la [Fast-Growing Hierarchy](https://en.wikipedia.org/wiki/Fast-growing_hierarchy).
Les fonctions des programmes sont dans l'analyse mathématique représentée par le même nom ($f$, $g$, $\text{main}$ etc...)
De plus, $f^n$ représente $n$ évaluations emboitée de $f$ : $f^n(x) = f(f(f(...(x)...)))$ répété $n$ fois

Liste principale :
- Quentin *disqualifié*
- Igor *disqualifié*
- 

Liste secondaire :
- Quentin $\le \frac{1}{\sqrt{5}}\times2^{1495000001}$
- Igor $\le$

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
Si l'on a $F_n$ le n-ème terme de la suite de Fibonacci, alors on a 
$$F_n = \frac{1}{\sqrt5}(\varphi^n-\varphi'^n)\le \frac{1}{\sqrt{5}}\times2^n$$
Avec $\varphi$ le nombre d'or et $\varphi' = -\varphi^{-1}$
Donc l'entier retournée est inférieur à $\frac{1}{\sqrt{5}}\times2^{1495000001}$.
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
On pose $f' = f(0,n,n)=f(0,n,n)$
On a ainsi
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
Le code analysé pour la liste secondaire (à 365 caractères), transformé par ChatGPT:
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

Donc comme $\text{bc}(x) = \text{rec}'^x(1)\le \hat f_{\omega^2}^{x}(2) = \hat f_{\omega^2}^{x+1}(1)$
Et on a aussi $\text{bc}(x) \ge \hat f_{\omega^2}^{x}(1)$
Comme $\hat f_{\omega^2}(2) \gg 999^2$, on a alors $\text{bc}(x) \le \hat f_{\omega^2+2}(2)$

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0MjY1NDU5NywtNTE0MTE1NjQ4LC0xNT
M2Mjc1MTc1LDMzODQ2MzY0MCwxODY0NTM5MTY1LC02NzkxMzky
NzEsMTY3OTE2OTMxMCwtMTY2MTEwOTM2NywxODgwNTAyNDI5XX
0=
-->