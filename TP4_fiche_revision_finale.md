# Fiche de révision – TP4 Équations différentielles (SageMath)

## 1. Définition  
Une **équation différentielle (ED)** relie une fonction inconnue \( y(x) \) à ses dérivées.

---

## 2. Résolution d’une ED du 1er ordre

### a) Cas homogène  
\[
y'_h + a(x) y_h = 0
\]

→ Solution :  
\[
y_h = C \, e^{-\int a(x) dx}
\]

### b) Cas particulier  
On cherche \( y_p \) qui vérifie l’équation complète.

### c) Solution générale  
\[
y(x) = y_h + y_p
\]

### d) Condition initiale  
Pour déterminer C :  
\[
y(x_0)=y_0
\]

---

## 3. Exemple central du TP  
Équation :
\[
y' + y = e^{-x}
\]

- Solution homogène : \( y_h = C e^{-x} \)  
- Solution particulière : \( y_p = \frac{x}{2} e^{-x} \)  
- Solution générale :  
\[
y(x)=C e^{-x} + \frac{x}{2} e^{-x}
\]

Avec \( y(0)=1 \) :  
\[
y(x) = e^{-x} + \frac{x}{2} e^{-x}
\]

---

## 4. SageMath – Comment faire ?

### 💻 Exemple de code — Déclarer les variables
```python
var('x')
y = function('y')(x)
```

### 💻 Exemple de code — Définir l’équation différentielle
```python
eq = diff(y, x) + y == exp(-x)
```

### 💻 Exemple de code — Résolution symbolique
```python
desolve(eq, y)
```

### 💻 Exemple de code — Résolution avec condition initiale
```python
desolve(eq, y, ics=[0, 1])
```

### 💻 Exemple de code — Tracer la solution
```python
sol = desolve(eq, y, ics=[0, 1])
plot(sol, (x, -2, 4))
```

### 💻 Exemple de code — Exemple générique (comme dans l’énoncé)
```python
factorial(42)
N(factorial(42))
```

---

# 📘 Fiche récapitulative finale

## ✔ Ce que tu dois retenir absolument

### 🎯 1. Structure d’une ED du 1er ordre
- **Forme générale** : \( y' + a(x) y = b(x) \)  
- **Toujours résoudre** : homogène + particulière

### 🎯 2. Méthodes
- **Homogène** : exponentielle  
- **Particulière** : essayer une forme adaptée à b(x)  
- **Solution générale** = somme des deux  
- **Condition initiale** → unique solution

### 🎯 3. SageMath
- `desolve(eq, y)`  
- `desolve(eq, y, ics=[x0, y0])`  
- `plot(... )` pour visualiser
- Penser à déclarer `var('x')` et `function('y')(x)`

### 🎯 4. Interprétation
- Une ED décrit l’évolution d’un phénomène (physique, mécanique, population…)  
- On contrôle les solutions en vérifiant qu’elles satisfont l’ED.

---

Si tu veux une version encore plus esthétique (couleurs, emojis, encadrés), je peux t’en refaire une !