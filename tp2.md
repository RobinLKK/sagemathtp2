# TP2 - Introduction à SageMath  
**Auteur : Robin GAWLAS**  

---

## 🧭 Résumé rapide (pour GitHub)

### 🎯 Objectif du TP
Découvrir les bases du langage **SageMath**, en manipulant :
- Les **nombres**, **factorielles**, et **valeurs numériques approchées**  
- Les **expressions symboliques** et les **fonctions**  
- Les **graphiques** 2D  
- Les **résolutions d’équations** et la **représentation graphique**  

Ce TP introduit les fonctions essentielles pour aborder les TPs suivants (espaces vectoriels, interpolation, etc.).

---

### 🔢 Principales notions vues

| Notion | Exemple |
|:--|:--|
| Factorielle et calcul numérique | `factorial(42)`, `N(pi)` |
| Expressions symboliques | `var('x')`, `f(x) = x^2 - 2*x + 1` |
| Évaluation d’une fonction | `f(3)` ou `f(3.5)` |
| Résolution d’équation | `solve(f(x)==0, x)` |
| Tracé d’une courbe | `plot(f(x), (x, -5, 5))` |
| Approximation numérique | `n(exp(1))` ou `N(sqrt(2))` |

---

### 📊 Résultats observés

- SageMath distingue les **calculs exacts (symboliques)** des **approximations numériques**.  
- Le langage est très proche de Python mais spécialisé pour les mathématiques.  
- Les commandes `show()` et `plot()` permettent d’afficher facilement des résultats et graphes.  

---

## 📘 Version complète et pédagogique

---

### 🧩 1. Calculs exacts et numériques

#### 📍 Objectif  
Comprendre la différence entre un calcul exact et son approximation.

#### 💻 Exemple de code
```python
factorial(42)
N(factorial(42))
```

#### 🧠 Explication  
- `factorial(42)` donne le résultat exact sous forme entière.  
- `N(...)` ou `n(...)` convertit ce résultat en valeur décimale approchée.  

---

### 🧮 2. Nombres et constantes

```python
pi
N(pi)
sqrt(2)
N(sqrt(2))
```

#### 💡 Remarque  
- `pi` et `sqrt(2)` sont symboliques.  
- `N()` permet d’obtenir leur valeur numérique.  

---

### 🔣 3. Expressions symboliques

#### Déclaration de variable symbolique
```python
var('x')
f(x) = x^2 - 2*x + 1
```

#### Évaluation
```python
f(0)
f(3)
```

#### 🔍 Dérivée et simplification
```python
diff(f, x)
simplify((x^2 - 1)/(x - 1))
```

#### 🧠 Explication  
- `var('x')` déclare une variable mathématique.  
- `diff(f, x)` calcule la dérivée de la fonction.  
- `simplify()` simplifie une expression algébrique.  

---

### 🧾 4. Résolution d’équations

#### Exemple simple
```python
solve(f(x) == 0, x)
```

#### Autre exemple
```python
solve(x^2 - 5*x + 6 == 0, x)
```

#### 🧠 Explication  
- `solve(expression == 0, variable)` cherche les solutions symboliques.  
- SageMath renvoie une liste d’équations du type `[x == 2, x == 3]`.  

---

### 📈 5. Tracés de fonctions

#### Exemple basique
```python
plot(f(x), (x, -5, 5))
```

#### Superposition de plusieurs fonctions
```python
plot(x^2, (x, -3, 3), color='blue') + plot(x^3, (x, -3, 3), color='red')
```

#### Options utiles
- `color='red'` : couleur de la courbe  
- `thickness=2` : épaisseur du trait  
- `gridlines=True` : affiche une grille  

---

### 📐 6. Calculs avancés

#### Définition et dérivée d’une fonction
```python
g(x) = sin(x) * exp(-x)
diff(g, x)
plot(g, (x, 0, 10))
```

#### Dérivée seconde
```python
diff(g, x, 2)
```

#### Intégrale
```python
integrate(g, x, 0, 10)
```

---

### 📊 7. Résumé des commandes importantes

| Commande | Description |
|:--|:--|
| `factorial(n)` | Calcule n! |
| `N(expr)` ou `n(expr)` | Valeur numérique approchée |
| `var('x')` | Déclare une variable symbolique |
| `diff(f, x)` | Dérivée de f par rapport à x |
| `simplify(expr)` | Simplifie une expression |
| `solve(eq, x)` | Résout une équation |
| `plot(expr, (x, a, b))` | Trace une fonction |
| `integrate(f, x, a, b)` | Intègre une fonction |
| `show(objet)` | Affiche un résultat formaté (graphiques, matrices, etc.) |

---

## 🎓 Conclusion

- SageMath est un environnement puissant pour le **calcul symbolique et numérique**.  
- Il combine la **rigueur des mathématiques** et la **souplesse de Python**.  
- Ce TP a permis de manipuler les opérations de base : factorielles, dérivées, intégrales, et tracés.  

---

**Bonnes révisions pour l’éval SageMath ! 🧮**  
