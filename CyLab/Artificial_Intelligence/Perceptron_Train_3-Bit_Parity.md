# Write-Up : Perceptron Train 3-Bit Parity

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Train 3-Bit Parity
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 15]

---

### 📝 Description

> _"Watch a perceptron learn in real time on 3-bit parity data using the classic update rule: only misclassified points trigger updates, with no weight decay. This challenge extends the same idea into 3 dimensions, and the frontend renders the points in 3D space. Because parity is not linearly separable by one plane, a single perceptron cannot hit 100% accuracy. Reach 75% accuracy to reveal the flag. Visit the service in your browser: `http://xebec.cylabacademy.net:14650/`"_[cite: 15]

---

### 🔍 Étape 1 : Comprendre le problème de parité à 3 bits en 3D

Ce challenge généralise le problème XOR à **3 dimensions** (la fonction de parité sur 3 bits)[cite: 15]. Les 8 combinaisons binaires possibles ($2^3 = 8$) forment les 8 sommets d'un cube unité dans l'espace 3D :

- **Parité paire (classe `0` — nombre pair de bits à `1`) :** `(0,0,0)`, `(0,1,1)`, `(1,0,1)`, `(1,1,0)` (4 sommets).
- **Parité impaire (classe `1` — nombre impair de bits à `1`) :** `(0,0,1)`, `(0,1,0)`, `(1,0,0)`, `(1,1,1)` (4 sommets).

Géométriquement, les sommets de chaque classe alternent sur le cube de telle sorte qu'aucune arête ne relie deux points de même parité. Un perceptron simple en 3D apprend une **unique frontière de décision planaire** (un plan 2D coupant l'espace 3D)[cite: 15]. Il est mathématiquement impossible de trancher un cube avec un seul plan de manière à séparer parfaitement les deux groupes de 4 sommets alternés. Au mieux, un plan peut correctement classer **6 sommets sur 8**, soit une précision maximale de $6 / 8 = \mathbf{75 \%}$[cite: 15].

---

### 🛠️ Étape 2 : Entraînement du Perceptron et réglage du taux d'apprentissage

En accédant à l'interface web (`http://xebec.cylabacademy.net:14650/`), on visualise en 3D les 8 sommets du cube ainsi que l'évolution du plan de décision en temps réel[cite: 15].

Comme pour les défis XOR et XNOR, le choix du taux d'apprentissage (*learning rate*) est crucial :
- Une valeur trop élevée fait basculer agressivement l'orientation du plan à chaque point mal classé, empêchant toute stabilisation.
- En sélectionnant un *learning rate* modéré (par exemple entre `0.1` et `0.5`) et en lançant l'entraînement selon la règle classique (mise à jour uniquement sur erreur, sans *weight decay*), le plan se stabilise de manière à isoler un sommet ou une arête d'un côté et regrouper 6 points bien classés, atteignant ainsi la cible de **75 %** de précision[cite: 15].

---

### 🚩 Étape 3 : Validation et obtention du Flag

Dès que le modèle atteint et maintient l'objectif théorique maximal de **75 %** de précision sur le cube de parité à 3 bits, l'application valide l'étape et affiche le flag[cite: 15].

**Flag :** `academy{...}` *(remplacez par le flag exact affiché sur votre instance)*

---

### 💡 Key Takeaways / Notions retenues

- **Généralisation de XOR en dimension $N$ (Parité) :** La fonction de parité à $n$ bits est l'extension multidimensionnelle de XOR ; ses points alternent aux sommets d'un hypercube de dimension $n$ et ne sont jamais linéairement séparables par un seul hyperplan.
- **Plafond théorique de précision :** Sur un cube à 3 bits (8 sommets), un hyperplan unique ne peut classer correctement au maximum que $6 / 8$ points (**75 %**), démontrant que l'ajout de dimensions d'entrée ne résout pas la non-linéarité sans neurones cachés[cite: 15].
- **Visualisation géométrique des hyperplans :** En 2D un perceptron trace une droite, en 3D un plan, et en dimension $d$ un hyperplan de dimension $d-1$ — mais sa capacité de séparation reste fondamentalement limitée aux frontières plates.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Train 3-Bit Parity
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 15]

---

### 📝 Description

> _"Watch a perceptron learn in real time on 3-bit parity data using the classic update rule: only misclassified points trigger updates, with no weight decay. This challenge extends the same idea into 3 dimensions, and the frontend renders the points in 3D space. Because parity is not linearly separable by one plane, a single perceptron cannot hit 100% accuracy. Reach 75% accuracy to reveal the flag. Visit the service in your browser: `http://xebec.cylabacademy.net:14650/`"_[cite: 15]

---

### 🔍 Step 1: Understanding the 3-Bit Parity Problem in 3D

This challenge generalizes the XOR problem into **3 dimensions** via the 3-bit parity function[cite: 15]. The $2^3 = 8$ binary input combinations correspond to the 8 corners of a unit cube in 3D space:

- **Even parity (class `0` — even number of `1`s):** `(0,0,0)`, `(0,1,1)`, `(1,0,1)`, `(1,1,0)` (4 vertices).
- **Odd parity (class `1` — odd number of `1`s):** `(0,0,1)`, `(0,1,0)`, `(1,0,0)`, `(1,1,1)` (4 vertices).

Geometrically, the two classes alternate across every edge of the cube so that no two adjacent vertices share the same label. A single 3D perceptron learns a **single planar decision boundary** (a flat 2D plane slicing through 3D space)[cite: 15]. It is mathematically impossible to slice a cube with one flat plane to separate all four alternating vertices of one class from the other four. At best, a single plane can correctly classify **6 out of 8 vertices**, capping theoretical accuracy at $6 / 8 = \mathbf{75\%}$[cite: 15].

---

### 🛠️ Step 2: Training the Perceptron & Tuning the Learning Rate

Navigating to the web service (`http://xebec.cylabacademy.net:14650/`) opens an interactive 3D visualization rendering the 8 cube vertices and the evolving decision plane in real time[cite: 15].

Just like in the 2D XOR and XNOR challenges, choosing an appropriate learning rate is key:
- Very high learning rates violently tilt the plane on every misclassified point, preventing convergence.
- Selecting a moderate learning rate (e.g., around `0.1` to `0.5`) and running the classic perceptron updates (updating solely on misclassifications with no weight decay) allows the plane to settle cleanly into a position that classifies 6 out of 8 corners accurately, hitting the **75%** target[cite: 15].

---

### 🚩 Step 3: Reaching the Target & Retrieving the Flag

Once the perceptron reaches **75%** classification accuracy across the 3D parity cube, the web application confirms the theoretical limit has been achieved and reveals the flag[cite: 15].

**Flag:** `academy{...}` *(replace with the exact flag displayed on your instance)*

---

### 💡 Key Takeaways

- **Generalizing XOR to $N$ Dimensions (Parity):** The $n$-bit parity function extends XOR to higher dimensions; its classes alternate across the vertices of an $n$-dimensional hypercube and can never be separated by a single hyperplane.
- **Theoretical Accuracy Ceiling:** On a 3-bit hypercube (8 vertices), a single flat plane can classify at most $6 / 8$ points (**75%**), showing that increasing input dimensionality alone does not overcome non-linearity without hidden layers[cite: 15].
- **Geometric Intuition of Hyperplanes:** A single perceptron learns a line in 2D, a plane in 3D, and a $(d-1)$-dimensional hyperplane in $d$-dimensional space—remaining strictly limited to flat decision boundaries.