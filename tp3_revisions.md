FICHE MÉMO — RÉVISION TP3 : NOMBRES COMPLEXES (détaillé)

Objectif

Cette fiche résume les notions et commandes utiles pour travailler avec les nombres complexes et la géométrie du plan complexe (TP3). Elle contient : définitions, opérations, commandes Sage/Python utiles, exemples liés aux exercices (puissances, équations, transformations, polygones réguliers) et astuces pratiques pour tracer et manipuler les objets.

1. Notions de base

- Un nombre complexe s'écrit z = x + i y, avec i^2 = -1. Dans Sage l'unité imaginaire est I (ou i selon le contexte).
- Partie réelle : Re(z) = x. Partie imaginaire : Im(z) = y.
- Module : |z| = sqrt(x^2 + y^2). Argument : arg(z) (angle en radians, branch principal usuel (-π, π] en Sage).
- Formes : cartésienne z = x + i y, exponentielle z = r e^{i θ} avec r = |z| et θ = arg(z).

2. Opérations et propriétés utiles

- Conjugué : conj(z) = x − i y. Propriétés : z * conj(z) = |z|^2.
- Module et argument : |z w| = |z| |w| ; arg(z w) = arg(z) + arg(w) (mod 2π).
- Puissances : z^n = |z|^n e^{i n arg(z)}.
- Racines n-ièmes : solutions de w^n = 1 sont ζ_k = exp(2 i π k / n), k = 0..n-1 (répartition régulière sur le cercle unité).

3. Commandes Sage/Python repérées (avec comportement attendu)

- I ou i : unité imaginaire (I dans Sage). Exemple : I^2 == -1.
- real(z) ou z.real() : partie réelle. imag(z) ou z.imag() : partie imaginaire.
- abs(z) : module |z| (retourne sqrt(...) s'il est exact).
- arg(z) : argument principal de z (en radians). Attention à la branche.
- exp(I*theta) : e^{i θ}.
- var('z') et solve(expression == 0, z) : résoudre symboliquement (solve renvoie une liste d'égalités ; utiliser N(...) pour des approximations numériques).
- list_plot(list_of_complexes, plotjoined=True, aspect_ratio=1) : tracer points (Re,Im) et les relier.
- parametric_plot((cos(t), sin(t)), (t, 0, 2*pi)) : tracer un cercle.
- Graphics primitives : point(), text("A", coord), line([a, b], thickness=...), show() pour afficher.

4. Exemples tirés du TP (avec interprétations)

Exemple A — puissances
- z = 1 + 2 i. |z| = sqrt(5). Les puissances z^n donnent une suite de complexes dont les modules sont |z|^n et dont les arguments sont n * arg(z) (mod 2π). Tracé : les points (Re(z^n), Im(z^n)) forment une spirale (si |z| ≠ 1).

Exemple B — équations complexes
- Résoudre z^2 + 2 z + 6 = 0 → solutions z = -1 ± i sqrt(5).
- Sage renvoie des expressions exactes ; pour les valeurs approximatives utiliser N(solutions) ou float(...).
- Pour polynômes de degré ≥ 3, solve peut renvoyer des expressions algébriques compliquées (formules de Cardan). On peut utiliser factor() ou roots() pour approcher numériquement.

Exemple C — géométrie par affixes
Points : A = -1 + i, B = -1 − i, C = 2 i, D = 2 − 2 i.
- Calcul d'angle : arg((c − a)/(d − a)) = arg(c−a) − arg(d−a). Si résultat = π/2 alors vecteurs AC et AD sont orthogonaux.
- Distance : |z − z0| correspond à la distance euclidienne entre le point d'affixe z et z0. Si plusieurs points ont même valeur |z − z0| = R, ils sont concycliques sur le cercle de centre z0 et rayon R.

Exemple D — similitudes et transformations
- f1(z) = z + i : translation de vecteur i (0,1).
- f2(z) = 3 z : homothétie de centre O et rapport 3.
- f3(z) = i z : rotation directe d'angle π/2 (90°) autour de O.
- f(z) = 5 exp(I*pi/4) * z + 6 : similitude directe (rapport 5, rotation π/4) suivie d'une translation de 6.

5. Fonctions utiles à coder (exemples)

- Racines n-ièmes de l'unité :

```python
def racines_n_eme_unite(n):
    return [exp(I*2*k*pi/n) for k in range(n)]
```

- Tracer un polygone régulier centré en 0 (Sage / matplotlib) : construire la liste de racines et tracer list_plot(..., plotjoined=True, aspect_ratio=1).

6. Astuces et pièges

- arg renvoie l'argument principal : normaliser modulo 2π si besoin.
- solve fournit des expressions exactes : convertir en numérique pour interprétation (N(...)).
- Toujours fixer aspect_ratio=1 pour les tracés géométriques afin d'éviter les déformations.
- Multiplication par exp(I*theta) → rotation; par réel r positif → homothétie; combinaison r*exp(I theta) → similitude directe.

7. Fiches de commandes rapides

- Partie réelle / imaginaire : real(z), imag(z)
- Module / argument : abs(z), arg(z)
- Conjugué : conj(z)
- Racines : [exp(I*2*k*pi/n) for k in range(n)]
- Résolution : solve(poly == 0, z) ; approximations : [N(s) for s in solutions]
- Tracés : list_plot(points, plotjoined=True, aspect_ratio=1), parametric_plot(...)

8. Exemple complet (mini-script Sage)

```python
# Définition
z = 1 + 2*I
# Puissances
for n in range(11):
    w = z**n
    print(n, w, "Re=", real(w), "Im=", imag(w), "|w|=", abs(w), "arg=", arg(w))
# Tracé
pts = [z**n for n in range(11)]
list_plot(pts, plotjoined=True, aspect_ratio=1)
```

9. Références rapides

- Formule d'Euler : e^{iθ} = cos θ + i sin θ.
- Racines de l'unité et polygones réguliers (sommets = racines).

Fin de la fiche. Bonne révision !
