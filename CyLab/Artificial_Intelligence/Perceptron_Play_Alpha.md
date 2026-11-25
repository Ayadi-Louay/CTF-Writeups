# Write-Up : Perceptron Play Alpha

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Play Alpha
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy

---

### 📝 Description

> _"Play with the weights and bias of a 2D perceptron while watching an ASCII plot update in real time. Tune the parameters so that the decision boundary separates all of the labeled points and you will earn the flag."_

---

### 🔍 Étape 1 : Connexion et analyse de la distribution 2D

Après avoir lancé l'instance et rejoint le service interactif en ligne de commande, on accède à un simulateur ASCII d'un perceptron monocouche en 2 dimensions. La fonction d'activation est définie par $z = w_1 \cdot x + w_2 \cdot y + b$, classant le point en classe `1` si $z \ge 0$ et en classe `0` si $z < 0$.

Avec les poids initiaux (`w1 = 1`, `w2 = -1`, `b = 0`), la frontière de décision ($x - y = 0$) traverse mal les données et laisse deux points mal classés (`x`). En affichant la liste des points via la commande `POINTS`, on observe leur répartition dans le plan :

- **Classe `0` (quadrant inférieur gauche) :** $(-3, -2)$, $(-1, -1)$, $(-4, -2)$
- **Classe `1` (quadrant supérieur droit) :** $(+3, +1)$, $(+2, +2)$, $(+1, +3)$

On remarque immédiatement que tous les points de classe `0` ont des coordonnées strictement négatives ($x + y < 0$), tandis que tous les points de classe `1` ont des coordonnées strictement positives ($x + y > 0$).

---

### 🛠️ Étape 2 : Ajustement des poids et orientation de la frontière

Pour tracer une droite séparatrice passant par l'origine avec une pente négative ($x + y = 0$), il suffit de fixer les deux poids à $+1$ et le biais à $0$ à l'aide de la commande `SET` :

```text
> set 1 1 0
```

L'équation devient alors $z = 1 \cdot x + 1 \cdot y + 0 = x + y$ :

- **Pour la classe `0`:** $(-3, -2) \rightarrow z = -5 < 0$, $(-1, -1) \rightarrow z = -2 < 0$, $(-4, -2) \rightarrow z = -6 < 0$ (tous classés `0`).
- **Pour la classe `1`:** $(+3, +1) \rightarrow z = +4 \ge 0$, $(+2, +2) \rightarrow z = +4 \ge 0$, $(+1, +3) \rightarrow z = +4 \ge 0$ (tous classés `1`).

Le graphique ASCII se met à jour en temps réel et affiche une séparation parfaite entre les `0` et les `1`.

### 🚩 Étape 3 : Validation et obtention du Flag

Une fois tous les points correctement classés, on exécute la commande CHECK pour valider le modèle et récupérer le flag.

```Plaintext
> check
Perfect! All points are classified correctly.
academy{11n34r1y_53p4r4813_9938a80d}
```

**Flag :** `academy{11n34r1y_53p4r4813_9938a80d}`

### 💡 Key Takeaways / Notions retenues

- **Vecteur de poids normal à la frontière :** Dans un perceptron 2D d'équation $w_1 x + w_2 y + b = 0$, le vecteur $\vec{w} = (w_1, w_2)$ est perpendiculaire à la droite de décision et pointe toujours vers la zone positive (classe 1).
- **Passage de la 1D à la 2D :** En ajoutant une deuxième dimension d'entrée, le seuil ponctuel de la droite numérique devient une droite séparatrice dans le plan, permettant de classifier des ensembles de points linéairement séparables en 2D.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Play Alpha
- **Platform / Event:** AI Foundations IAuthor: LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy

### 📝 Description

> "Play with the weights and bias of a 2D perceptron while watching an ASCII plot update in real time. Tune the parameters so that the decision boundary separates all of the labeled points and you will earn the flag."

### 🔍 Step 1: Connecting and Analyzing the 2D Point Distribution

Launching the challenge instance and connecting to the interactive CLI playground presents a real-time ASCII visualization of a 2D single-layer perceptron. The activation function computes $z = w_1 \cdot x + w_2 \cdot y + b$, predicting class `1` when $z \ge 0$ and class `0` when $z < 0$.

With the default parameters (`w1 = 1`, `w2 = -1`, `b = 0`), the decision boundary ($x - y = 0$) cuts poorly across the data, leaving two misclassified points (`x`). Running `POINTS` lists the training dataset:

- **Class `0` (bottom-left quadrant):** $(-3, -2)$, $(-1, -1)$, $(-4, -2)$
- **Class `1` (top-right quadrant):** $(+3, +1)$, $(+2, +2)$, $(+1, +3)$

Notice that every class 0 point lies strictly in the negative region ($x + y < 0$), whereas every class 1 point lies strictly in the positive region ($x + y > 0$).

### 🛠️ Step 2: Tuning the Weights to Rotate the Boundary

To draw a separating line passing through the origin along $x + y = 0$, we set both weights to $+1$ and keep the bias at $0$ using the `SET` command:

```Plaintext
> set 1 1 0
```

The activation equation becomes $z = 1 \cdot x + 1 \cdot y + 0 = x + y$:

- **For Class `0`:** $(-3, -2) \rightarrow z = -5 < 0$, $(-1, -1) \rightarrow z = -2 < 0$, $(-4, -2) \rightarrow z = -6 < 0$ (all classified as `0`).
- **For Class `1`:** $(+3, +1) \rightarrow z = +4 \ge 0$, $(+2, +2) \rightarrow z = +4 \ge 0$, $(+1, +3) \rightarrow z = +4 \ge 0$ (all classified as `1`).

The ASCII plot updates immediately, showing a clean separation between all `0` and `1` labels.

### 🚩 Step 3: Verification and Flag Retrieval

With every point classified properly, we run `CHECK` to verify the solution and reveal the flag.

```Plaintext
> check
Perfect! All points are classified correctly.
academy{11n34r1y_53p4r4813_9938a80d}
```

**Flag:** `academy{11n34r1y_53p4r4813_9938a80d}`

### 💡 Key Takeaways

- **Weight Vector Orientation:** In a 2D perceptron defined by $w_1 x + w_2 y + b = 0$, the weight vector $\vec{w} = (w_1, w_2)$ is orthogonal (perpendicular) to the decision line and always points toward the positive half-plane (class 1).
- **Scaling from 1D to 2D:** Adding a second input feature generalizes the decision boundary from a single threshold point on a number line to a full dividing line across a 2D plane, enabling linear separation of 2D datasets.
