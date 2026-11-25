# Write-Up : Perceptron Play Naught

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Play Naught
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy

---

### 📝 Description

> _"The points would be inseparable in just the x-dimension, but each point now has a new y-value so the set becomes linearly separable in 2D. Watch the ASCII plot update in real time as you tweak the perceptron weights and bias. Separate the labeled points with a single line to earn the flag. Connect with netcat: `$ nc xebec.cylabacademy.net 37839`"_

---

### 🔍 Étape 1 : Connexion et élévation de dimension (Feature Engineering)

En se connectant au serveur via `netcat` (`nc xebec.cylabacademy.net 37839`), on retrouve l'interface interactive en ligne de commande du perceptron 2D.

Ce challenge illustre un concept fondamental du _Machine Learning_ : des données qui ne sont **pas linéairement séparables en 1 dimension** (sur le seul axe $x$) le deviennent dès qu'on leur ajoute une **deuxième dimension** ($y$). Dans ce nouvel espace en 2D, les points de classe `0` et de classe `1` peuvent désormais être séparés par une seule frontière de décision linéaire d'équation $w_1 \cdot x + w_2 \cdot y + b = 0$.

---

### 🛠️ Étape 2 : Réglage des poids et du biais (`SET 1 2 -2`)

Après avoir inspecté les points étiquetés sur le graphique ASCII (via `POINTS`), on ajuste simultanément les deux poids ($w_1, w_2$) et le biais ($b$) afin d'orienter et de décaler la droite séparatrice entre les deux groupes de points.

En exécutant la commande suivante dans le simulateur :

```text
> set 1 2 -2
```

On définit les paramètres 𝑤1=1, 𝑤=2 et 𝑏=−2. L'équation d'activation du perceptron devient alors :

z=1⋅x+2⋅y−2
La frontière de décision (x+2y−2=0, soit y=−0.5x+1) traverse le plan avec la pente et l'ordonnée à l'origine exactes pour placer tous les points de classe 0 dans la zone négative (z<0) et tous les points de classe 1 dans la zone positive (z≥0).

### 🚩 Étape 3 : Vérification et obtention du Flag

Une fois que le graphique ASCII affiche tous les points correctement classés (0 et 1 sans aucun x), on lance la commande CHECK pour valider la séparation et récupérer le flag.

```Plaintext
> check
Perfect! All points are classified correctly.
```

**Flag :** `academy{...}` (remplacez par le flag exact affiché dans votre terminal)

### 💡 Key Takeaways / Notions retenues

- **Projection dans un espace de dimension supérieure :** Un ensemble de points non linéairement séparable en dimension 𝑑 (ici 1D) peut devenir linéairement séparable en dimension d+1 (ici 2D) grâce à l'ajout d'une nouvelle caractéristique (feature 𝑦). C'est le principe fondamental derrière les couches cachées des réseaux de neurones et l'astuce du noyau (Kernel Trick).
- **Rôle conjoint des poids et du biais :** Les poids(w 1,w 2) fixent l'inclinaison de la droite séparatrice, tandis que le biais 𝑏 (ici −2) permet de décaler cette droite hors de l'origine pour épouser la marge exacte entre les deux classes.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Play Naught
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy

### 📝 Description

> "The points would be inseparable in just the x-dimension, but each point now has a new y-value so the set becomes linearly separable in 2D. Watch the ASCII plot update in real time as you tweak the perceptron weights and bias. Separate the labeled points with a single line to earn the flag."

### 🔍 Step 1: Connecting and Dimensionality Lifting (Feature Engineering)

Connecting to the instance via netcat (nc xebec.cylabacademy.net 37839)[cite: 12] opens the interactive 2D perceptron CLI playground.

This challenge demonstrates a foundational machine learning concept: data points that are not linearly separable in 1D (along the x-axis alone) become linearly separable when projected into 2D via a second feature (𝑦). In this 2D plane, class 0 and class 1 points can be cleanly divided by a single linear decision boundary defined by
𝑤1⋅𝑥+𝑤2⋅𝑦

- 𝑏=0w1⋅x+w2⋅y+b=0.

🛠️ Step 2: Tuning the Weights and Bias (SET 1 2 -2)

After inspecting the labeled dataset on the ASCII graph (using POINTS), we adjust both weights (w 1,w 2) and the bias (b) to tilt and shift the dividing line cleanly between the two classes.

Running the following command in the playground:

```Plaintext
> set 1 2 -2
```

Sets the parameters to w1=1, 𝑤=2, and b=−2, yielding the activation equation:

z=1⋅x+2⋅y−2

The resulting decision boundary (x+2y−2=0, or y=−0.5x+1) slices across the 2D plane with the exact slope and intercept required to place all class 0 points in the negative half-plane (z<0) and all class 1 points in the positive half-plane (z≥0).

### 🚩 Step 3: Verification and Flag Retrieval

Once the real-time ASCII plot confirms that every point is classified properly (displaying 0 and 1 with no x markers), running CHECK validates the model and reveals the flag.

```Plaintext
> check
Perfect! All points are classified correctly.
```

**Flag:** `academy{...}` (replace with the exact flag printed in your terminal)

### 💡 Key Takeaways

- **Higher-Dimensional Feature Mapping:** Data that is inseparable in 𝑑 dimensions (1D here) can become linearly separable in 𝑑+1 dimensions (2D here) by introducing an informative new feature (𝑦). This principle underpins hidden layers in neural networks as well as kernel methods (the Kernel Trick).
- **Combined Effect of Weights and Bias:** The weights (w 1,w 2) control the angle/slope of the decision line, while the bias 𝑏 (here −2) translates the line away from the origin so it fits neatly into the separating margin.
