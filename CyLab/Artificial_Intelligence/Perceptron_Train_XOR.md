# Write-Up : Perceptron Train XOR

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Train XOR
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 15]

---

### 📝 Description

> _"Watch a perceptron learn in real time on XOR data using the classic update rule: only misclassified points trigger updates, with no weight decay. Because XOR is not linearly separable, a single perceptron cannot hit 100% accuracy. Reach 75% accuracy to prove you understand the limitation and reveal the flag. Visit the service in your browser: `http://chatelaine.cylabacademy.net:11221/`"_[cite: 15]

Les indices précisent :
1. Vous disposez de **16** mises à jour par exécution, et les points correctement classés ne modifient pas le modèle selon la règle classique.
2. La plage de taux d'apprentissage (*learning rate*) est large (`0.02` à `20.0`), ce qui fait que des valeurs très élevées peuvent déplacer agressivement la frontière de décision.
3. Le problème XOR ne peut pas être parfaitement séparé par une seule droite ; **75 %** est le meilleur score atteignable pour ce modèle.[cite: 15]

---

### 🔍 Étape 1 : Comprendre le problème XOR et les limites du Perceptron

Un perceptron simple est un classifieur linéaire : il cherche à tracer une unique droite (une frontière de décision linéaire) pour séparer deux classes de points.

Or, la table de vérité de la porte logique **XOR** (OU exclusif) possède 4 points :
- `(0, 0) -> 0` et `(1, 1) -> 0`
- `(0, 1) -> 1` et `(1, 0) -> 1`

Ces points ne sont **pas linéairement séparables** : il est géométriquement impossible de tracer une seule ligne droite séparant les `0` des `1`. Au mieux, une droite peut isoler l'un des quatre points des trois autres, ce qui correspond exactement à **3 points bien classés sur 4**, soit une précision maximale de **75 %**[cite: 15].

---

### 🛠️ Étape 2 : Ajustement des paramètres d'entraînement

En ouvrant l'interface web du challenge (`http://chatelaine.cylabacademy.net:11221/`), on accède à un simulateur permettant d'entraîner un perceptron sur les 4 points du jeu de données XOR sur un budget limité à **16 mises à jour**[cite: 15].

Avec un taux d'apprentissage (*learning rate*) trop élevé, les poids du modèle oscillent brutalement à chaque erreur et la droite de décision saute d'un extrême à l'autre sans jamais se stabiliser. En réglant le *learning rate* sur une valeur modérée (par exemple autour de `0.1` à `0.5`) et en lançant l'entraînement (ou en sélectionnant judicieusement l'ordre des points mal classés), la droite se positionne de manière à isoler un point d'une classe des trois autres, stabilisant ainsi la précision à **75 %**.

---

### 🚩 Étape 3 : Validation et obtention du Flag

Dès que le perceptron atteint l'objectif de **75 %** de précision sur l'ensemble des données XOR, le serveur valide la compréhension de cette limite fondamentale et affiche le flag sur la page.

**Flag :** `academy{...}` *(remplacez par le flag exact affiché sur votre instance)*

---

### 💡 Key Takeaways / Notions retenues

- **Séparabilité linéaire :** Un perceptron monocouche ne peut résoudre que des problèmes linéairement séparables (comme `AND` ou `OR`). Il est mathématiquement incapable d'atteindre 100 % de précision sur des fonctions non linéaires comme `XOR`.
- **Rôle du taux d'apprentissage (*Learning Rate*) :** Un *learning rate* trop grand provoque une instabilité et empêche la convergence du modèle, tandis qu'une valeur adaptée permet d'ajuster progressivement la frontière de décision.
- **Vers les réseaux profonds (MLP) :** Historiquement, cette limitation du perceptron simple (mise en évidence par Minsky et Papert en 1969) a motivé le développement des perceptrons multicouches (MLP) avec des fonctions d'activation non linéaires pour résoudre des problèmes complexes.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Train XOR
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 15]

---

### 📝 Description

> _"Watch a perceptron learn in real time on XOR data using the classic update rule: only misclassified points trigger updates, with no weight decay. Because XOR is not linearly separable, a single perceptron cannot hit 100% accuracy. Reach 75% accuracy to prove you understand the limitation and reveal the flag. Visit the service in your browser: `http://chatelaine.cylabacademy.net:11221/`"_[cite: 15]

The hints highlight:
1. You get **16** updates per run, and correctly classified points do not change the model in the classic rule.
2. The learning-rate sweep is wide (`0.02` through `20.0`), so very high values can swing the boundary aggressively.
3. XOR cannot be perfectly separated by one line; **75%** is the best achievable target for this model.[cite: 15]

---

### 🔍 Step 1: Understanding the XOR Problem & Perceptron Limitations

A single-layer perceptron is a linear classifier: it attempts to draw a single straight line (a linear decision boundary) to separate two classes of data points.

However, the **XOR** (exclusive OR) truth table consists of 4 points:
- `(0, 0) -> 0` and `(1, 1) -> 0`
- `(0, 1) -> 1` and `(1, 0) -> 1`

These points are **not linearly separable**—it is geometrically impossible to separate the `0`s from the `1`s with a single straight line. At best, a linear boundary can isolate one point from the remaining three, resulting in **3 out of 4 points classified correctly**, or a maximum accuracy of **75%**[cite: 15].

---

### 🛠️ Step 2: Tuning the Training Parameters

Navigating to the web service (`http://chatelaine.cylabacademy.net:11221/`) opens an interactive simulator where we train a perceptron on the XOR dataset within a strict budget of **16 updates**[cite: 15].

If the learning rate is set too high, weight updates overshoot and the decision boundary swings wildly back and forth without settling. By choosing a moderate learning rate (e.g., around `0.1` to `0.5`) and running the training updates, the boundary settles into a position that isolates one corner from the rest, achieving the target **75%** accuracy.

---

### 🚩 Step 3: Reaching the Target & Retrieving the Flag

Once the perceptron reaches **75%** accuracy across the XOR points, the application confirms that the theoretical limit has been demonstrated and reveals the flag.

**Flag:** `academy{...}` *(replace with the exact flag displayed on your instance)*

---

### 💡 Key Takeaways

- **Linear Separability:** A single perceptron can only solve linearly separable problems (such as `AND` or `OR`). It is mathematically incapable of reaching 100% accuracy on non-linear functions like `XOR`.
- **Impact of Learning Rate:** Excessively large learning rates cause severe oscillations that prevent convergence, whereas properly tuned values allow the decision boundary to stabilize effectively.
- **Need for Multi-Layer Perceptrons (MLPs):** Historically, the inability of single perceptrons to solve XOR (highlighted by Minsky and Papert in 1969) drove the adoption of multi-layer neural networks with non-linear activation functions.