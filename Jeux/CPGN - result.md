# Résultats de la Compétition du Plus Grand Nombre

Merci à tous d'avoir participé !

Du fait du grand nombre d'entrée ne respectant les règles, deux listes ont été crée: 
- La première, prends les propositions tel quel, applique les règles du concours, et n'hésite pas à disqualifier des entrées.
- Dans la deuxième, je me suis permis d'interprété les différentes erreurs pour corriger les programmes et donner un classement ou personne n'a été disqualifié.

Les entrée sont listé avec des explications, de la plus petite (sur la liste principale) à la plus grande.
Ensuite, vous avez à la fin du document mon entrée (TREE(3)), ainsi que des ressources dans le domaine de la *gogologie*, la branche de l'informatique théorique / des mathématiques étudiant les grands nombres. Vous aurez aussi des conseils sur comment réduire le nombre de caractères pour un programme donné.

Liste principale :
- Quentin *disqualifié*
- ?
- 

## Igor
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

Le code corrigé de `main` pour la liste secondaire est  :
```c
I main(void) {
    return c(99999999999,99999999999);
}
```
Dans ce code :
- $f(n,n,x) \le f_{x+1}(n)$


## Quentin
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwNDQ5ODE4MCwtMTY2MTEwOTM2NywxOD
gwNTAyNDI5XX0=
-->