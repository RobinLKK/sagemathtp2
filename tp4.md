# TP4 – Sagemath : Équations Différentielles  
**Auteur : Robin GAWLAS**

---

## 🧭 Résumé rapide (pour GitHub)

### 🎯 Objectif  
Manipuler et résoudre des **équations différentielles ordinaires (EDO)** avec SageMath :
- Résolution symbolique (`desolve`)
- Résolution numérique (`desolve_rk4`)
- Tracer les solutions
- Visualiser des champs de directions
- Gérer les conditions initiales
- Étudier des équations d’ordre 1 et 2

---

## 🧩 Notions essentielles

| Notion | Exemple |
|--------|---------|
| EDO 1er ordre | y' = f(x, y) |
| Linéaire | y' + a y = b |
| Second ordre | y'' + a y' + b y = g(x) |
| Condition initiale | y(x₀) = y₀ |
| Solution générale | y = y_h + y_p |
| Résolution symbolique | `desolve(...)` |
| Résolution numérique | `desolve_rk4(...)` |
| Visualisation | `plot_slope_field`, `plot` |

---

# 📘 Version complète et pédagogique

---

# 1️⃣ EDO du premier ordre  

### Exemple  
y' = x - y

### SageMath
```python
var('x y')
eq = diff(y, x) == x - y
sol = desolve(eq, y)
show(sol)
