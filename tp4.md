# TP4 – SageMath : Équations Différentielles  
# Auteur : Robin GAWLAS

## 🧭 Résumé rapide (pour GitHub)

### 🎯 Objectif  
Manipuler et résoudre des équations différentielles ordinaires (EDO) avec SageMath :
- Résolution symbolique (desolve)
- Résolution numérique (desolve_rk4)
- Tracer les solutions
- Visualiser des champs de directions
- Gérer les conditions initiales
- Étudier des équations d’ordre 1 et 2

## 🧩 Notions essentielles

| Notion | Exemple |
|--------|---------|
| EDO 1er ordre | y' = f(x, y) |
| Linéaire | y' + a y = b |
| Second ordre | y'' + a y' + b y = g(x) |
| Condition initiale | y(x₀) = y₀ |
| Solution générale | y = y_h + y_p |
| Résolution symbolique | desolve(...) |
| Résolution numérique | desolve_rk4(...) |
| Visualisation | plot_slope_field, plot |

# 📘 Version complète et pédagogique

# 1️⃣ EDO du premier ordre  

### Exemple  
y' = x - y

### SageMath
var('x y')
eq = diff(y, x) == x - y
sol = desolve(eq, y)
show(sol)

### Résultat attendu  
y(x) = x - 1 + C e^{-x}

### Condition initiale
desolve(eq, y, ics=[0, 2])

# 2️⃣ Équations différentielles linéaires  

### Exemple  
y' - y = x

eq = diff(y, x) - y == x
sol = desolve(eq, y)
show(sol)

### Résultat :  
y(x) = x - 1 + C e^{x}

# 3️⃣ Second ordre  

### Exemple  
y'' + 3y' + 2y = e^x

var('x')
y = function('y')(x)

eq = diff(y, x, 2) + 3*diff(y, x) + 2*y == exp(x)
sol = desolve(eq, y)
show(sol)

# 4️⃣ Résolution numérique — Runge–Kutta (RK4)

### Exemple  
y' = y - x^2

f(x, y) = y - x^2
sol = desolve_rk4(f, y, 0, 1, step=0.1, end_points=[0, 5])
list_plot(sol)

# 5️⃣ Champ de directions

eq = diff(y, x) == x - y
sol = desolve(eq, y, ics=[0, 1])

p1 = plot_slope_field(x - y, (x, -3, 3), (y, -3, 3))
p2 = plot(sol, (x, -3, 3), color='red', thickness=2)

show(p1 + p2)

# 6️⃣ Tracés multiples

p = plot_slope_field(x-y, (x,-3,3), (y,-3,3))

for c in [-2, -1, 0, 1, 2]:
    sol = desolve(diff(y, x) == x - y, y, ics=[0, c])
    p += plot(sol, (x,-3,3))

show(p)

# 📊 FICHE RÉCAP — Commandes SageMath

# Déclarations
var('x y')
y = function('y')(x)

# Résolution symbolique
desolve(diff(y, x) == f(x), y)

# Avec CI
desolve(diff(y, x) == f(x), y, ics=[x0, y0])

# Équation linéaire
desolve(diff(y, x) + a*y == b, y)

# Second ordre
desolve(diff(y,x,2) + a*diff(y,x) + b*y == g(x), y)

# Résolution numérique RK4
f(x,y) = y - x^2
desolve_rk4(f, y, x0, y0, step=0.1, end_points=[xmin, xmax])

# Tracé solution
plot(sol, (x, xmin, xmax))

# Champ de directions
plot_slope_field(f(x,y), (x,xmin,xmax), (y,ymin,ymax))

# Superposition champ + solution
plot_slope_field(...) + plot(sol, ...)

# 🎓 Conclusion

# Le TP4 enseigne toutes les bases nécessaires pour manipuler et comprendre
# les équations différentielles ordinaires dans SageMath :
# - Résolution symbolique
# - Résolution numérique
# - Visualisation graphique
# Il prépare aux méthodes avancées (systèmes différentiels, stabilité, etc.).
