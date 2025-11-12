# TP3 - SageMath : Nombres Complexes et Géométrie du Plan  
**Auteur : Robin GAWLAS**  

---

## 🧭 Résumé rapide (pour GitHub)

### 🎯 Objectif du TP
Découvrir et manipuler les **nombres complexes** dans SageMath, ainsi que leur interprétation **géométrique dans le plan complexe**.  
Ce TP introduit les liens entre **calculs algébriques**, **représentation graphique**, et **transformations géométriques** (rotations, homothéties, similitudes).

---

### 🧩 Notions principales

| Concept | Description |
|:--|:--|
| Nombre complexe | z = x + i y avec i² = -1 |
| Module et argument | |z| = √(x² + y²), arg(z) = angle avec l’axe réel |
| Forme exponentielle | z = r·e^{iθ} avec r = |z| et θ = arg(z) |
| Conjugué | conj(z) = x − i y |
| Multiplication / Division | Addition ou soustraction des arguments |
| Puissance | zⁿ = |z|ⁿ·e^{i·n·θ} |
| Racines n-ièmes | ζₖ = e^{2iπk/n}, k = 0…n-1 → points d’un polygone régulier |
| Transformation | z ↦ a·z + b → similitude directe (rotation + homothétie + translation) |

---

### 🔢 Commandes clés SageMath

| Commande | Effet |
|:--|:--|
| `I` | unité imaginaire (i) |
| `real(z)` / `imag(z)` | partie réelle / imaginaire |
| `abs(z)` | module |
| `arg(z)` | argument (radians) |
| `conj(z)` | conjugué |
| `exp(I*θ)` | e^{iθ} |
| `solve(expr == 0, z)` | résolution d’équation complexe |
| `list_plot([...], plotjoined=True, aspect_ratio=1)` | tracé de points complexes |
| `parametric_plot((cos(t), sin(t)), (t,0,2*pi))` | cercle unité |

---

## 📘 Version complète et pédagogique

### 1️⃣ Représentation des nombres complexes

#### 💻 Exemple
```python
z = 1 + 2*I
show(z)
show(abs(z))     # module
show(arg(z))     # argument
show(conj(z))    # conjugué
```

#### 🧠 Interprétation
- `abs(z)` → distance à l’origine.  
- `arg(z)` → angle avec l’axe réel (en radians).  
- `conj(z)` → symétrie par rapport à l’axe réel.

---

### 2️⃣ Opérations fondamentales

#### 💻 Exemple
```python
z = 1 + 2*I
w = 2 - 3*I
show(z + w)
show(z * w)
show(z / w)
```

#### 🧠 Remarques
- La **somme** correspond à la somme des coordonnées (translation).  
- Le **produit** combine rotation et changement d’échelle.  
- La **division** inverse la transformation.

---

### 3️⃣ Puissances et racines n-ièmes

#### 💻 Exemple
```python
z = 1 + 2*I
for n in range(6):
    show(z^n)
```

#### 💡 Remarque
Les points (Re(zⁿ), Im(zⁿ)) forment une **spirale** si |z| ≠ 1.  

#### Racines n-ièmes de l’unité
```python
def racines_n_eme_unite(n):
    return [exp(I*2*pi*k/n) for k in range(n)]

show(racines_n_eme_unite(6))
list_plot(racines_n_eme_unite(6), plotjoined=True, aspect_ratio=1)
```

Chaque racine représente un sommet d’un **polygone régulier** inscrit dans le cercle unité.

---

### 4️⃣ Résolution d’équations complexes

#### 💻 Exemple
```python
var('z')
solve(z^2 + 2*z + 6 == 0, z)
```

#### 🔍 Explication
Les solutions sont :  
z = −1 ± i√5  
Elles peuvent être affichées sous forme approchée avec `N(...)`.

---

### 5️⃣ Géométrie par affixes

#### 💻 Exemple
```python
A = -1 + I
B = -1 - I
C = 2*I
D = 2 - 2*I

# Vérification orthogonalité : angle entre AC et AD
arg((C - A)/(D - A))
```

#### 🧠 Interprétation
- Si arg((C−A)/(D−A)) = π/2, alors les vecteurs AC et AD sont perpendiculaires.  
- |z−z₀| = R représente le cercle de centre z₀ et de rayon R.

---

### 6️⃣ Transformations et similitudes

#### 💻 Exemples
```python
f1(z) = z + I             # Translation de vecteur (0,1)
f2(z) = 3*z               # Homothétie de centre O, rapport 3
f3(z) = I*z               # Rotation d’angle π/2
f4(z) = 5*exp(I*pi/4)*z + 6  # Similitude directe (rapport 5, rotation π/4, translation 6)
```

#### 🧭 Lecture géométrique
- Multiplication par un complexe de module > 1 → **agrandissement**.  
- Multiplication par `exp(Iθ)` → **rotation d’angle θ**.  
- Addition d’un complexe → **translation**.

---

### 7️⃣ Tracés et visualisations

#### 💻 Exemple complet
```python
# Puissances successives
z = 1 + 2*I
pts = [z^n for n in range(10)]
list_plot(pts, plotjoined=True, aspect_ratio=1)
```

#### 💡 Astuce
Toujours fixer `aspect_ratio=1` pour éviter les déformations des figures.  

---

### 8️⃣ Fiche récapitulative

| Fonction | Rôle |
|:--|:--|
| `real(z)` / `imag(z)` | Parties réelle et imaginaire |
| `abs(z)` / `arg(z)` | Module et argument |
| `conj(z)` | Conjugué |
| `exp(I*θ)` | Représentation exponentielle |
| `solve(expr==0,z)` | Résolution symbolique |
| `list_plot([...])` | Tracé de points complexes |
| `parametric_plot((cos(t), sin(t)))` | Cercle unité |
| `exp(I*2*pi*k/n)` | Racine n-ième de l’unité |

---

## 🎓 Conclusion

- Les nombres complexes unifient les **calculs algébriques** et la **géométrie plane**.  
- SageMath permet de manipuler et visualiser facilement ces objets.  
- Les transformations (translation, rotation, homothétie, similitude) s’expriment élégamment sous forme complexe.  

---

**Fin du TP3 — Nombres Complexes et Géométrie du Plan.**  
*Bonne révision pour l’évaluation !* 🧮
