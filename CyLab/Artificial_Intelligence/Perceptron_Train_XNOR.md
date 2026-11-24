# Write-Up : Perceptron Train XNOR

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Train XNOR
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 16]

---

### 📝 Description

> _"Watch a perceptron learn in real time on XNOR data using the classic update rule: only misclassified points trigger updates, with no weight decay. Because XNOR is not linearly separable, a single perceptron cannot hit 100% accuracy. Reach 75% accuracy to prove you understand the limitation and reveal the flag."_[cite: 16]

Les indices précisent :
1. Vous disposez de **16** mises à jour par exécution, et les points correctement classés ne modifient pas le modèle selon la règle classique.
2. La plage de taux d'apprentissage (*learning rate*) est large (`0.02` à `20.0`), ce qui fait que des valeurs très élevées peuvent déplacer agressivement la frontière de décision.
3. Le problème XNOR ne peut pas être parfaitement séparé par une seule droite ; **75 %** est le meilleur score atteignable pour cette configuration.[cite: 16]

---

### 🔍 Étape 1 : Comprendre le problème XNOR et la non-séparabilité linéaire

Tout comme la fonction XOR, la porte logique **XNOR** (NON-OU exclusif) est la négation exacte de XOR et possède 4 points dans sa table de vérité :
- `(0, 0) -> 1` et `(1, 1) -> 1`
- `(0, 1) -> 0` et `(1, 0) -> 0`

Un perceptron monocouche ne pouvant tracer qu'une **seule frontière de décision linéaire** (une droite), il lui est mathématiquement impossible de regrouper les deux coins opposés `(0, 0)` et `(1, 1)` d'un même côté tout en laissant `(0, 1)` et `(1, 0)` de l'autre côté. Au maximum, une droite peut correctement séparer **3 points sur 4**, plafonnant ainsi la précision théorique à **75 %**[cite: 16].

---

### 🛠️ Étape 2 : Entraînement et réglage du taux d'apprentissage

Après avoir lancé l'instance du challenge et ouvert l'interface web, on accède au simulateur d'entraînement du perceptron sur les données XNOR avec un budget maximal de **16 mises à jour**[cite: 16].

Si l'on choisit un *learning rate* trop élevé, chaque erreur entraîne une correction brutale des poids et fait osciller la droite de décision sans jamais stabiliser la classification. En sélectionnant un taux d'apprentissage modéré (par exemple entre `0.1` et `0.5`) et en exécutant les étapes d'entraînement, la frontière linéaire se stabilise de manière à isoler un point des trois autres, permettant d'atteindre et de maintenir **75 %** de précision[cite: 16].

---

### 🚩 Étape 3 : Validation et obtention du Flag

Dès que l'objectif de **75 %** de précision est atteint sur l'ensemble des données XNOR, l'interface valide la démonstration de cette limite fondamentale et affiche le flag[cite: 16].

**Flag :** `academy{...}` *(remplacez par le flag exact affiché sur votre instance)*

---

### 💡 Key Takeaways / Notions retenues

- **Symétrie XOR / XNOR :** XNOR est le complément logique de XOR ; ces deux fonctions partagent exactement la même propriété géométrique de non-séparabilité linéaire pour un classifieur linéaire simple.
- **Limitation d'un neurone unique :** Un seul neurone (perceptron) ne peut partitionner l'espace d'entrée qu'en deux demi-plans séparés par un hyperplan (une droite en 2D).
- **Importance de l'architecture et des hyperparamètres :** Résoudre XNOR à 100 % nécessite au moins une couche cachée (un perceptron multicouche / MLP) combinant plusieurs frontières linéaires, tandis que le réglage fin du *learning rate* garantit une convergence stable.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Train XNOR
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 16]

---

### 📝 Description

> _"Watch a perceptron learn in real time on XNOR data using the classic update rule: only misclassified points trigger updates, with no weight decay. Because XNOR is not linearly separable, a single perceptron cannot hit 100% accuracy. Reach 75% accuracy to prove you understand the limitation and reveal the flag."_[cite: 16]

The hints highlight:
1. You get **16** updates per run, and correctly classified points do not change the model in the classic rule.
2. The learning-rate sweep is wide (`0.02` through `20.0`), so very high values can swing the boundary aggressively.
3. XNOR cannot be perfectly separated by one line; **75%** is the best achievable target for this setup.[cite: 16]

---

### 🔍 Step 1: Understanding the XNOR Problem & Linear Non-Separability

Just like XOR, the **XNOR** (exclusive NOR) logic gate is the exact logical complement of XOR and defines 4 points in its truth table:
- `(0, 0) -> 1` and `(1, 1) -> 1`
- `(0, 1) -> 0` and `(1, 0) -> 0`

Because a single-layer perceptron can only learn a **single linear decision boundary** (a straight line), it is geometrically impossible to group the diagonally opposite corners `(0, 0)` and `(1, 1)` on one side while keeping `(0, 1)` and `(1, 0)` on the other. At best, one line can classify **3 out of 4 points** correctly, capping maximum accuracy at **75%**[cite: 16].

---

### 🛠️ Step 2: Training & Tuning the Learning Rate

After launching the challenge instance and opening the web interface, we interact with the real-time perceptron trainer on the XNOR dataset within a strict budget of **16 updates**[cite: 16].

Setting the learning rate too high causes aggressive weight updates that swing the decision boundary erratically on every misclassified point. By selecting a moderate learning rate (e.g., around `0.1` to `0.5`) and running the updates, the linear boundary settles into a stable position that isolates one corner from the remaining three, reaching the **75%** accuracy target[cite: 16].

---

### 🚩 Step 3: Reaching the Target & Retrieving the Flag

Once the perceptron achieves **75%** accuracy on the XNOR dataset, the service confirms that this fundamental limitation has been demonstrated and reveals the flag[cite: 16].

**Flag:** `academy{...}` *(replace with the exact flag displayed on your instance)*

---

### 💡 Key Takeaways

- **XOR / XNOR Symmetry:** XNOR is the logical inverse of XOR; both share the exact same geometric non-linear separability limitation for a single linear classifier.
- **Single-Neuron Constraint:** A single perceptron can only divide an input space into two half-spaces separated by a single hyperplane (a line in 2D).
- **Architecture & Hyperparameter Tuning:** Achieving 100% accuracy on XNOR requires a multi-layer perceptron (MLP) with non-linear activations to combine multiple decision boundaries, while a properly tuned learning rate ensures stable convergence.