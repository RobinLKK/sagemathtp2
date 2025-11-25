# Fiche de révision – TP4 Équations différentielles (SageMath)

## 1. Définition
Une **équation différentielle (ED)** relie une fonction inconnue \( y(x) \) à ses dérivées.  
Exemples :
- \( y' + y = e^{-x} \)
- \( y' - y = x \)
- \( y'' + y = 0 \)

## 2. Résolution d’ED du 1er ordre – Méthode générale
Pour une ED linéaire :
\[
y'(x) + a(x) y(x) = b(x)
\]

### a) Cas homogène
\[
y'_h + a(x) y_h = 0
\]
→ Solution :
\[
y_h = C \, e^{-\int a(x) dx}
\]

### b) Cas particulier
Méthode classique :  
On cherche \( y_p \) vérifiant l'équation complète.  
Exemples courants :
- Si \( b(x)=k e^{mx} \), on teste \( y_p = lpha e^{mx} \)
- Si \( b(x)=P_n(x) \), on teste un polynôme du même degré

### c) Solution générale
\[
y = y_h + y_p
\]

### d) Application d’une condition initiale
On utilise :
\[
y(x_0) = y_0
\]
→ permet de déterminer la constante C.

---

## 3. Exemple traité dans le TP :  
### ### Équation :  
\[
y' + y = e^{-x}
\]

### a) Solution homogène :
\[
y_h = C e^{-x}
\]

### b) Solution particulière :
On teste \( y_p = lpha x e^{-x} \).  
On trouve finalement :
\[
y_p = rac{x}{2} e^{-x}
\]

### c) Solution générale :
\[
y = C e^{-x} + rac{x}{2} e^{-x}
\]

### d) Exemple avec condition initiale
Si \( y(0)=1 \) :
- On obtient \( C = 1 \)
- Solution :
\[
y(x) = e^{-x} + rac{x}{2} e^{-x}
\]

---

## 4. Résolution avec SageMath

### Définir variables et fonction
```python
var('x')
y = function('y')(x)
```

### Déclarer l’équation différentielle
```python
eq = diff(y, x) + y == exp(-x)
```

### Résoudre l’équation
```python
desolve(eq, y)
```

### Condition initiale
```python
desolve(eq, y, ics=[0, 1])
```

### Tracer la solution
```python
sol = desolve(eq, y, ics=[0,1])
plot(sol, (x, -2, 4))
```

---

## 5. Méthodes vues dans le TP
- Définir une ED dans SageMath  
- Résoudre symboliquement  
- Utiliser des conditions initiales (`ics=[x0, y0]`)  
- Tracer les solutions  
- Manipuler les solutions (simplification, substitution…)

---

## 6. Points clés à retenir
- Une ED se résout via *homogène + particulière*.  
- SageMath facilite énormément les calculs.  
- Toujours vérifier la solution en la réinjectant dans l’ED.  
- Les conditions initiales rendent la solution **unique**.
