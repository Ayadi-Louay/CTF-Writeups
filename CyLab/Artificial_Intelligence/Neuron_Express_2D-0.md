# Write-Up : Neuron Express 2D-0

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Neuron Express 2D-0
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy

---

### 📝 Description

> _"Probe the 2D perceptron, then submit its weights and bias. Send two integers (x, y) within the bounds to see if the perceptron fires (1) or stays quiet (0)."_

Contraintes et règles de l'environnement :
- **Domaine d'entrée :** Paires d'entiers $(x, y) \in [-10, 10]^2$
- **Règle d'activation :** $w_1 \cdot x + w_2 \cdot y + b \ge 0 \rightarrow \mathbf{1}$, sinon $\mathbf{0}$ (avec $w_1, w_2, b \in \mathbb{Z}$)
- **Validation :** La commande `TEST w1 w2 b` vérifie que le triplet $(w_1, w_2, b)$ reproduit exactement les sorties du perceptron cible sur l'ensemble de la grille $21 \times 21$ des points entiers.

---

### 🔍 Étape 1 : Sondage de la frontière de décision en 2D

En envoyant plusieurs coordonnées entières pour observer où le perceptron bascule de `0` (*stays quiet*) à `1` (*fires!*) :
1. Sur la diagonale : `(0, 0) -> 0`, `(1, 1) -> 0`, `(2, 2) -> 0`, puis `(3, 3) -> 1`.
2. Autour du point de bascule : `(3, 2) -> 1` alors que `(2, 3) -> 0`.
3. Après de premiers essais (`test 1 -1 0` et `test 1 -1 -1`) montrant une grille d'erreur structurée verticalement, deux sondages supplémentaires confirment l'indépendance vis-à-vis de l'axe $y$ : `(2, 1) -> 0` et `(3, 1) -> 1`.

---

### 🛠️ Étape 2 : Déduction des poids et du biais $(w_1, w_2, b)$

Les observations montrent que la sortie ne dépend que de la coordonnée $x$ :
- Dès que $x = 2$ (quel que soit $y$), le neurone reste silencieux (`0`).
- Dès que $x = 3$ (quel que soit $y$), le neurone s'active (`1`).

La frontière de décision est donc une **droite verticale** d'équation $x = 3$, ce qui implique :
- Un poids nul sur l'axe $y$ : $w_2 = 0$
- Un poids unitaire positif sur l'axe $x$ : $w_1 = 1$
- Un biais décalant le seuil en $x = 3$ : $b = -3$

L'équation d'activation s'écrit alors :
$$z = 1 \cdot x + 0 \cdot y - 3 = x - 3$$
- Pour $x = 2$ : $z = 2 - 3 = -1 < 0 \rightarrow \mathbf{0}$
- Pour $x = 3$ : $z = 3 - 3 = 0 \ge 0 \rightarrow \mathbf{1}$

---

### 🚩 Étape 3 : Soumission et obtention du Flag

On soumet les paramètres entiers déduits via la commande `TEST` :

```text
[10/128] (x,y)> 2 1
Perceptron stays quiet.
[11/128] (x,y)> 3 1
Perceptron fires!
[12/128] (x,y)> test 1 0 -3
Perfect match! Here is your flag:
academy{n3ur0n_expr_2d_32e4b2b4}
```

**Flag :** `academy{n3ur0n_expr_2d_32e4b2b4}`

---

### 💡 Key Takeaways / Notions retenues

- **Frontières alignées sur les axes (*Axis-Aligned Boundaries*) :** Lorsqu'un poids est nul ($w_2 = 0$), le perceptron ignore complètement la variable correspondante ($y$) et trace une frontière strictement parallèle à cet axe ($x = -b/w_1$).
- **Extraction de modèle par grille de rétroaction :** L'analyse des motifs d'erreur sur l'espace d'entrée permet d'identifier rapidement l'orientation réelle de l'hyperplan séparateur et de corriger les poids en conséquence.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Neuron Express 2D-0
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy

---

### 📝 Description

> _"Probe the 2D perceptron, then submit its weights and bias. Send two integers (x, y) within the bounds to see if the perceptron fires (1) or stays quiet (0)."_

Environment rules and constraints:
- **Input bounds:** Integer pairs $(x, y) \in [-10, 10]^2$
- **Output rule:** $w_1 \cdot x + w_2 \cdot y + b \ge 0 \rightarrow \mathbf{1}$, else $\mathbf{0}$ (with integer parameters $w_1, w_2, b \in \mathbb{Z}$)
- **Submission:** The `TEST w1 w2 b` command checks whether $(w_1, w_2, b)$ reproduces the target perceptron's exact outputs across every integer pair on the $21 \times 21$ grid.

---

### 🔍 Step 1: Probing the 2D Decision Boundary

By sending integer coordinate pairs to observe where the output flips from `0` (*stays quiet*) to `1` (*fires!*):
1. Along the diagonal: `(0, 0) -> 0`, `(1, 1) -> 0`, `(2, 2) -> 0`, and `(3, 3) -> 1`.
2. Around the transition zone: `(3, 2) -> 1` whereas `(2, 3) -> 0`.
3. After initial guesses (`test 1 -1 0` and `test 1 -1 -1`) revealed a vertically structured mismatch grid, two additional probes confirmed invariance along the $y$-axis: `(2, 1) -> 0` and `(3, 1) -> 1`.

---

### 🛠️ Step 2: Deducing the Weights and Bias $(w_1, w_2, b)$

The probes demonstrate that the neuron's output depends solely on the $x$-coordinate:
- Whenever $x = 2$ (regardless of $y$), the perceptron stays quiet (`0`).
- Whenever $x = 3$ (regardless of $y$), the perceptron fires (`1`).

Thus, the decision boundary is a **vertical line** at $x = 3$, corresponding to:
- Zero weight on $y$: $w_2 = 0$
- Positive unit weight on $x$: $w_1 = 1$
- Bias shifting the threshold to $x = 3$: $b = -3$

The activation function evaluates to:
$$z = 1 \cdot x + 0 \cdot y - 3 = x - 3$$
- At $x = 2$: $z = 2 - 3 = -1 < 0 \rightarrow \mathbf{0}$
- At $x = 3$: $z = 3 - 3 = 0 \ge 0 \rightarrow \mathbf{1}$

---

### 🚩 Step 3: Submitting the Guess & Retrieving the Flag

We submit the integer parameters using the `TEST` command:

```text
[10/128] (x,y)> 2 1
Perceptron stays quiet.
[11/128] (x,y)> 3 1
Perceptron fires!
[12/128] (x,y)> test 1 0 -3
Perfect match! Here is your flag:
academy{n3ur0n_expr_2d_32e4b2b4}
```

**Flag:** `academy{n3ur0n_expr_2d_32e4b2b4}`

---

### 💡 Key Takeaways

- **Axis-Aligned Decision Boundaries:** When a weight equals zero ($w_2 = 0$), the perceptron completely ignores that input feature ($y$) and forms a boundary strictly parallel to that axis ($x = -b/w_1$).
- **Diagnostic Error Grids in Model Extraction:** Inspecting where candidate parameters fail across an input grid quickly reveals the true orientation of the target hyperplane and guides exact parameter recovery.