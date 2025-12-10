# TP 5 - Intégration

**Consignes :**





- Le TP doit être réalisé **individuellement**.


- **Il n'est pas à rendre** : vous travaillez le TP pour vous ! Cependant, utilisez les bonnes pratiques de la programmation : ajoutez des commentaires ou des explications dans votre code.





**Objectifs du TP**





Etes-vous capable :


- d'utiliser la commande `integral` ou `integrate` ?


- d'expliquer le principe de l’intégration numérique ?


- de lister quelques méthodes de quadrature ? de les implementer ?


- d'expliquer la différence entre les méthodes simples et les méthodes composites ?

# Intégrales

Supposons que l'on souhaite calculer les primitives de :  $$ \int \frac{1}{2x+1} \mathrm{ d}x  $$

```python
x = var('x')
f = 1/(2*x+1)
integral(f,x)
```

```python
integrate(f,x)
```

Remarques : 





- La machine renvoie une primitive. Pour avoir l'ensemble des primitives, il faut bien entendu ajouter une constante. 


- La fonction log est la fonction logarithme népérien usuel, habituellement notée ln.


- Sage omet les valeurs absolues, ce qui ne l'empêche pas de faire des calculs exacts même pour les valeurs négatives. (Il travaille avec le logarithme complexe).

ou évaluer la même intégrale sur un intervalle donné $[0,1]$ :


```python
integral(f,x,0,1)
```

ou avoir une approximation de l'intégrale :

```python
N(integral(f,x,0,1))
```

# EXERCICE 1

Calculer les primitives suivantes et vérifier que vous avez trouvé le bon résultat en utilisant la commande `bool`.


  \begin{equation*}


    a) \quad \int \tan t \text{ d} t \quad


    b) \quad \int \dfrac{e^{kt}-e^{-kt}}{e^{kt}+e^{-kt}} \text{ d} t \quad


    c) \quad \int \dfrac{1}{1+e^{3u}} \text{ d} u


  \end{equation*}

```python
var('t')
f_a= tan(t)
primitive_a=integrate(f_a,t)

check_a = bool(diff(primitive_a,t)== f_a)
show(check_a)
show(primitive_a)
```

```python
var('t')
var('k')

f_b= (exp(k*t)-exp(-k*t)) / (exp(k*t)+exp(-k*t))

primitive_b=integrate(f_b,t)

check_b = bool(diff(primitive_b,t)== f_b)
show(check_b)
show(primitive_b)
```

```python
var('u')

f_c= 1/(1+exp(3*u))

primitive_c=integrate(f_c,u)

check_c = bool(diff(primitive_c,u)== f_c)
show(check_c)
show(primitive_c)
```

# EXERCICE 2

a) Calculer l'intégrale $ \displaystyle \int_0^{1} \sqrt{1-x^2} \text{ d} x  $.





```python
var('x')

f= sqrt(1-(x**2))

integral2=integrate(f,x,0,1)

show("L'intégrale est : ",integral2)
```

b) Représenter le graphe de la fonction intégrande en utilisant "aspect_ratio=1". Qu'est-ce que vous remarquez ?

```python
graph = plot(f,(x,0,1), aspect_ratio=1, color='red')
show(graph)

```

# Rappels : boucles et fonctions

La syntaxe de Sage est basée sur celle du langage Python.


L'indentation du code joue un rôle important dans cette syntaxe : le nombre d'espaces au début de chaque ligne a une influence sur la manière dont le code sera interprété.





Les boucles sont implémentées avec les constructuers `while`





C’est par l’indentation que l’on délimite le bloc exécuté dans la boucle while.

```python
i=0
while i<= 2:
    i=i+1
i

```

et `for`





Pour la boucle  `for`  on peut utiliser l'instruction  `range(n)`  qui renvoit la liste des  $n$  premiers entiers (indexé à partir de  0 ). On a donc  `range(n)=[0..n−1]`.


```python
n = 3
show(range(n))
for i in range(n):
    print(i)
```

Pour l'instruction  `range`  on peut spécifier un autre indice de départ, un autre indice de fin ainsi que le pas. De même, pour l'instruction  .. .

```python
show(range(0,11,2))
show(range(5,1,-1))
show([0..11,step=2])
show([5..1,step=-1])
```

Cependant on peut faire parcourir à l'indice n'importe quelle liste donnée dans l'instruction (sans que cette liste soit spécifiquement à valeurs entières ni même tous du même type).

```python
TableauTest = ['t','e','s','t', 2+2]
for i in TableauTest:
    print(i)
```

L'utilisation de boucles  `for`  est très utile pour travailler avec les listes.

```python
# Création d'une liste de 0 de taille 5
L = [0 for j in range(5)]
show(L)
# Parcours d'une liste de couples et récupération de la liste des premières composantes de chaque couple
L2 = [(0,1),(2,3),(4,5),(6,7)]
show('Liste complète ' , L2)
L2extrait = [l[0] for l in L2]
show('Liste extraite ' , L2extrait)

```




Pour définir la fonction $f(x)=0$ si $x<0$ et $f(x)=x^2$ si $x\geq0$ , on peut faire par exemple :

```python
def f(x):
    if x<0:
        return 0
    else:
        return x^2
```

```python
f(5)
```

```python
f(-5)
```

Une fonction est récursive si elle s’appelle elle-même.

```python
def puissance(x,n) :
    if n>0 :
        return x * puissance(x, n-1)
    else : return 1
```

```python
puissance(2,5)
```

# Intégration numérique

Le but est d’aborder le calcul général de l’intégrale d’une fonction $f(x)$ sur un domaine


fini délimité par des bornes finies $a$ et $b$  : $$ I = \int_a^b f(x) \mathrm{ d}x  $$





Dans certains cas très limités, une telle intégrale peut être calculée analytiquement (à la main). Cependant,


ce n’est que très rarement possible, et le plus souvent un des cas suivants se présente :


    


 – Le calcul analytique est long, compliqué et rébarbatif.


    


 – Le résultat de l’intégrale est une fonction compliquée qui fait appel à d’autres fonctions elles-même


longues à évaluer.





 – Cette intégrale n’a pas d’expression analytique (par exemple la fonction erreur : $Erf(x) = \frac{2}{ \pi} \int_0^x e^{-x^{'2}} \mathrm{ d}x'$.


 


Dans tous ces cas, on préfèrera calculer numériquement la valeur de l’intégrale $I$.





L’idée principale est de trouver des méthodes qui permettent de calculer rapidement une valeur approchée de l’intégrale à calculer : $$\tilde{I} \approx I$$





Une méthode bien connue consiste par exemple à diviser l’aire


sous la courbe en un grand nombre de petits rectangles d’aire $\tilde{I_k}$ et de les sommer. 





Le résultat $$\tilde{I}=\sum_k \tilde{I_k} $$ est alors une approximation de l’intégrale $I$. Cette approximation est d’autant meilleure que la largeur $h$ des


rectangles tend vers 0, c’est à dire : $\lim_{h \rightarrow 0}  \tilde{I_k} = I$.





Pour toutes les méthodes que l'on considère, l’intégrale numérique est calculée à


partir de l’évaluation de la fonction $f(x)$ en un nombre de points $n+1$ distincts : $f_k = f(x_k)$, $k\in [0, n]$.





Exemple graphique :





<img src=integration_rectangle.png></img>

# Méthodes de quadrature numérique simples:

- Rectangle : $\tilde{I} = (b-a)f(a) \quad $ ou Point au milieu : $\tilde{I} = (b-a)f\bigg(\dfrac{a+b}{2}\bigg)$ 


- Trapèze : $\tilde{I} = (b-a)\dfrac{f(a)+f(b)}{2}$


- Simpson : $\tilde{I} = \dfrac{b-a}{6}[f(a)+4f\bigg(\dfrac{a+b}{2}\bigg)+f(b)]$


# Méthodes de quadrature numérique composites 

L’idée est donc de découper le domaine total d’intégration $[a, b]$ en $n$ intervalles. On approxime alors


l’aire $\tilde{I}_k$, $k \in [0,n−1]$ de chaque intervalle par des méthodes de quadrature numérique simples, et on en déduit une approximation de l’aire totale par une simple somme :





$$\tilde{I}=\sum_k^{n-1} \tilde{I_k} $$





Lorsque $n$ est suffisamment grand, la largeur $h=(b − a)/n$ des intervalles devient aussi petite que l’on veut.





- Rectangles : $$\tilde{I} = \dfrac{b-a}{n} \sum_{i=0}^{n-1}f(x_i)$$





- Trapèzes : $$\tilde{I} = \dfrac{b-a}{n}\bigg(\dfrac{f(a)+f(b)}{2} + \sum_{i=1}^{n-1}f(x_i)\bigg)$$





- Simpson : $$\tilde{I} = \dfrac{b-a}{6n}\bigg(f(a)+2\sum_{i=1}^{n-1}f(x_{i})+4\sum_{i=0}^{n-1}f(m_{i})+f(b)\bigg)$$


avec $m_i = a + (i + \frac 1 2) h$ les milieux des segments $[x_i, x_{i+1}]$.








# EXERCICE 3

On veut estimer $\displaystyle \int_0^\frac{5}{2} f(x) \mathrm{ d}x  $ à partir des données suivantes :





<img src=tab.JPG></img>

a) En utilisant la méthode des rectangles. 

```python
valeurX = [0,1/2,1,3/2,2,5/2]
valeurF = [3/2,2,2,1.6364,1.25,0.9565]

h = valeurX[1] - valeurX[0]

I_rectangle_gauche = sum(valeurF[:-1]) * h 
I_rectangle_droite = sum(valeurF[1:]) * h 

show(I_rectangle_gauche,' et ', I_rectangle_droite)
```

b) En utilisant la méthode des trapèzes.

```python
valeurX = [0,1/2,1,3/2,2,5/2]
valeurF = [3/2,2,2,1.6364,1.25,0.9565]


h = valeurX[1] - valeurX[0]

I_trapeze = (h/2) * (valeurF[0] + valeurF[-1] + 2 * sum(valeurF[1:-1]))
show(I_trapeze)
```

c) Répresenter graphiquement la méthode des rectangles.

Suggestion :


1) Définir un graphique avec la commande `g = Graphics();`


2) Utiliser `line` et ajouter chaque ligne au graphique : `g += line([(1,0) , (1,2)]) `


```python
valeurX = [0,1/2,1,3/2,2,5/2]
valeurF = [3/2,2,2,1.6364,1.25,0.9565]


g = Graphics()


for i in range(len(valeurX) - 1):
    g += line([(valeurX[i], 0), (valeurX[i], valeurF[i])],color='red')  
    g += line([(valeurX[i], valeurF[i]), (valeurX[i+1], valeurF[i])], color='blue')  
    g += line([(valeurX[i+1], 0), (valeurX[i+1], valeurF[i])],color='green')

g += line([(valeurX[i], valeurF[i]) for i in range(len(valeurX))])

g.show(aspect_ratio=1)
```

# EXERCICE 4

a) Définir une fonction `trapezes(f,a,b,n)` qui prend en entrée la fonction, les bornes de l'intégrale et le nombre de subdivisions. Elle renvoie en sortie la valeur approchée de l'intégrale selon la <i>méthode des trapèzes</i> et la <i>repésentation graphique de la méthode et de la fonction si $n<15$</i> (Voir l'"exemple graphique" dans l'introduction Intégration numérique)





```python
def trapezes(f, a, b, n):
    h = (b - a)/n
    X = [a + i*h for i in range(n+1)]
    F = [f(x) for x in X]

    # Formule des trapèzes
    I = h*(0.5*F[0] + sum(F[1:-1]) + 0.5*F[-1])

    # Petit graphique si n < 15
    if n < 15:
        g1 = Graphics()
        for i in range(n):
            g1 += line([(X[i],0),(X[i],F[i])])       # bord gauche
            g1 += line([(X[i],F[i]),(X[i+1],F[i+1])]) # bord oblique
            g1 += line([(X[i+1],0),(X[i+1],F[i+1])]) # bord droit
        g1

    return I


```

b) En utilisant votre fonction `trapezes(f,a,b,n)`, calculer $\displaystyle \int_1^2 \dfrac{1}{\sin(x)} e^{x^{2}} \mathrm{ d}x  $


et vérifier que ce résultat s'approche de sa valeur exacte.

```python
f(x) = exp(x^2)/sin(x)
trapezes(f, 1, 2, 10)

```

# Curiosité : Performances

La performance d’une méthode se juge en comparant :





- Précision du résultat 





  Celle-ci se caractérise en estimant l’erreur $\varepsilon$ entre l’approximation et la valeur réelle de l’intégrale :





$$\varepsilon = I - \tilde{I}$$ 


  La valeur de l’erreur ne peut pas être calculée exactement puisqu’en général, on ne connaît pas l’intégrale $I$ que l’on cherche à calculer.   Cependant, une majoration peut souvent être estimée en étudiant le développement en série de Taylor de la fonction $f(x)$ (prochain chapitre du cours).








- Rapidité d’exécution nécessaire pour atteindre ce résultat. 





   De manière générale, toutes les méthodes peuvent atteindre de très grandes précisions. Cependant, le temps de calcul augmente avec la précision.


   Ce temps n’augmente pas de la même manière pour toutes les méthodes si bien que certaines


   s’avèrent plus efficaces que d’autres. En particulier, le temps de calcul des méthodes de quadrature est


   proportionnel au nombre de points où la fonction $f(x)$ est évaluée.





```python

```