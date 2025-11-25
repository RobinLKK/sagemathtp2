# ============================================================
# TP4 – FICHE RÉVISION : ÉQUATIONS DIFFÉRENTIELLES EN SAGEMATH
# Auteur : Robin GAWLAS
# ============================================================

# ------------------------------------------------------------
# 📌 Objectifs
# ------------------------------------------------------------
# - Savoir reconnaître une équation différentielle (type, ordre)
# - Résoudre symboliquement avec desolve
# - Résoudre numériquement avec desolve_rk4
# - Utiliser des conditions initiales
# - Vérifier une solution
# - Tracer solutions et champs de pentes
# - Gérer les EDO linéaires, homogènes, non homogènes, et 2ème ordre

# ------------------------------------------------------------
# 📌 1. Déclarer variables et fonctions
# ------------------------------------------------------------

var('x')                  # variable réelle
y = function('y')(x)      # y(x) comme vraie fonction

# ------------------------------------------------------------
# 📌 2. Résolution symbolique (EDO 1er ordre)
# ------------------------------------------------------------
# Forme : y' = f(x,y)

eq = diff(y, x) == f(x)          # équation
sol = desolve(eq, y)             # solution générale

# Avec condition initiale (CI) :
sol_ci = desolve(eq, y, ics=[x0, y0])

# ------------------------------------------------------------
# 📌 3. Résolution d'une EDO LINÉAIRE
# ------------------------------------------------------------
# Forme : y' + a*y = b

eq = diff(y, x) + a*y == b
sol = desolve(eq, y)

# ------------------------------------------------------------
# 📌 4. Résolution d'une EDO du second ordre
# ------------------------------------------------------------
# Forme : y'' + a*y' + b*y = g(x)

eq2 = diff(y, x, 2) + a*diff(y, x) + b*y == g(x)

# CI : y(x0) = c1 et y’(x0) = c2
sol2 = desolve(eq2, y, ics=[x0, c1, c2])

# ------------------------------------------------------------
# 📌 5. Vérification qu'une fonction est solution
# ------------------------------------------------------------
# Résultat = 0 → c'est bien une solution

eq.substitute(y == sol).full_simplify()

# ------------------------------------------------------------
# 📌 6. Résolution numérique (méthode RK4)
# ------------------------------------------------------------
# Usage quand Sage ne peut pas résoudre symboliquement

f(x, y) = ...
sol_points = desolve_rk4(f, y, x0, y0, step=0.1, end_points=[xmin, xmax])

# sol_points = liste de points → list_plot pour tracer

# ------------------------------------------------------------
# 📌 7. Tracer une solution
# ------------------------------------------------------------
plot(sol, (x, xmin, xmax))

# Tracé pour solution numérique :
list_plot(sol_points)

# ------------------------------------------------------------
# 📌 8. Champ de pentes (direction field)
# ------------------------------------------------------------

var('x y')
f(x, y) = ...

plot_slope_field(f, (x, xmin, xmax), (y, ymin, ymax))

# ------------------------------------------------------------
# 📌 9. Superposer champ + solution
# ------------------------------------------------------------

p = plot_slope_field(f, (x,-3,3),(y,-3,3))
p += plot(sol, (x,-3,3), color='red')
show(p)

# ------------------------------------------------------------
# 📌 10. Tracer plusieurs solutions (multisolutions)
# ------------------------------------------------------------

var('x')
y = function('y')(x)
p = plot_slope_field(f, (x,-5,5), (y,-5,5))

for y0 in [-2,-1,0,1,2]:
    sol = desolve(diff(y,x)==f(x,y), y, ics=[0, y0])
    p += plot(sol, (x,-5,5))

show(p)

# ------------------------------------------------------------
# 📌 11. Reconnaître le type d’équation
# ------------------------------------------------------------

# 1er ordre générale :
#     y' = f(x,y)

# 1er ordre linéaire :
#     y' + a(x)*y = b(x)

# homogène :
#     y' + a(x)*y = 0 → solution = C*exp( - ∫ a(x) dx )

# 2ème ordre linéaire :
#     y'' + a y' + b y = g(x)

# autonome :
#     y' = f(y)

# séparables :
#     y' = f(x)*g(y) → dy/g(y) = f(x) dx → intégrer

# ------------------------------------------------------------
# 📌 12. Les commandes MINIMALES à connaître (pour l’éval)
# ------------------------------------------------------------

# Résolution symbolique :
desolve(diff(y,x)==f(x), y)

# CI 1er ordre :
desolve(diff(y,x)==f(x), y, ics=[x0,y0])

# CI 2ème ordre :
desolve(diff(y,x,2)+a*diff(y,x)+b*y == g(x), y, ics=[x0,y0,dy0])

# Vérification :
eq.substitute(y==sol).full_simplify()

# Champ de pentes :
plot_slope_field(f(x,y), (x,a,b), (y,c,d))

# Tracer une solution :
plot(sol, (x,a,b))

# Résolution numérique :
desolve_rk4(f, y, x0, y0, step=0.1, end_points=[a,b])

# ------------------------------------------------------------
# FIN DE LA FICHE RÉVISION
# ------------------------------------------------------------
