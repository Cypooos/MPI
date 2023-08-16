# Résultats de la Compétition du Plus Grand Nombre

Merci à tous d'avoir participé !

Du fait du grand nombre d'entrée ne respectant les règles, deux listes ont été crée: 
- La première, prends les propositions tel quel, applique les règles du concours, et n'hésite pas à disqualifier des entrées.
- Dans la deuxième, je me suis permis d'interprété les différentes erreurs pour corriger les programmes et donner un classement ou personne n'a été disqualifié.

Les entrée sont listé avec des explications, de la plus petite (sur la liste principale) à la plus grande.
Ensuite, vous avez à la fin du document mon entrée (TREE(3)), ainsi que des ressources dans le domaine de la *gogologie*, la branche de l'informatique théorique / des mathématiques étudiant les grands nombres. Vous aurez aussi des conseils sur comment réduire le nombre de caractères pour un programme donné.

Dans ce document, les $\hat f$ représentent les fonctions de la [Fast-Growing Hierarchy](https://en.wikipedia.org/wiki/Fast-growing_hierarchy), une méthode utilisé pour comparer des fonctions grandissant vite et définies par récurrence.
Les fonctions des codes sont dans l'analyse mathématique appelée par le même nom ($f$, $g$, $\text{main}$ etc...)

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
**Calcul d'une borne max :**
On a, dans ce code $f(a,n,x) = a^{\hat f_{x}(n)} \le \hat f_{x+2}(n)$
On a donc, en posant $f'(n)=f(n,n,n)$, le fait que $f'(n)\le \hat f_{n+2}(n+2)$
Cela donne $g(d) = f'^d(d)\le \hat f_{\omega+1}(d+2)$
Si l'on pose $h'(n) = h(n,n)$, on a $h'(n) \le \hat f_{\omega+n+2}(n+2) = \hat f_{2\omega}(n+2)$
Pareillement, si l'on pose $c'(n) = c(n,n)$, on retrouve $c'(n) \le \hat f_{2\omega+n+1}(n+1) = \hat f_{3\omega}(n+1)$ *ici le n+1 viens du fait que la boucle est réalisée $c(x,i-1)$ fois*
On a donc $\text{main}() = c'(99999999999) \le \hat f_{3\omega}(100000000000)\boxed{\le \hat f_{3\omega+1}(1)}$



<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyMDU5ODI1NiwxNjc5MTY5MzEwLC0xNj
YxMTA5MzY3LDE4ODA1MDI0MjldfQ==
-->