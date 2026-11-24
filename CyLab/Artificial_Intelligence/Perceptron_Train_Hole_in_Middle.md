# Write-Up : Perceptron Train Hole in Middle

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Train Hole in Middle
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 17]

---

### 📝 Description

> _"Watch a perceptron learn in real time on a 'hole in the middle' pattern: positive points surround one negative center point. The classic perceptron update rule still applies (only misclassified points trigger updates, with no weight decay), but this shape is not linearly separable by a single line. Reach 88.9% accuracy to reveal the flag."_[cite: 17]

Les indices précisent :
1. Vous disposez de **16** mises à jour par exécution, et les points correctement classés ne modifient pas le modèle selon la règle classique.
2. La plage de taux d'apprentissage (*learning rate*) est large (`0.02` à `20.0`), ce qui fait que des valeurs très élevées peuvent déplacer agressivement la frontière de décision[cite: 17].

---

### 🔍 Étape 1 : Comprendre le motif « Hole in the Middle » et sa non-séparabilité

Dans ce scénario, le jeu de données est composé d'une grille de **9 points** (3×3) : **8 points positifs** forment un anneau autour d'**1 point négatif** situé exactement au centre.

Un perceptron simple ne pouvant apprendre qu'une **seule frontière de décision linéaire** (une droite unique), il est géométriquement impossible d'encercler le point central pour l'isoler des 8 points qui l'entourent. Toute droite traversant le nuage de points laissera nécessairement le point central du même côté qu'au moins plusieurs points positifs.

La stratégie optimale pour un classifieur linéaire consiste donc à déplacer la droite complètement à l'extérieur de la grille de points afin de classer **tous les 9 points comme positifs** : on obtient ainsi **8 points bien classés sur 9**, soit $8 / 9 \approx \mathbf{88,9 \%}$ de précision[cite: 17].

---

### 🛠️ Étape 2 : Entraînement et réglage du taux d'apprentissage

Après avoir lancé l'instance et ouvert l'interface web, on accède au simulateur permettant d'entraîner le perceptron sur ces 9 points avec un budget limité à **16 mises à jour**[cite: 17].

En sélectionnant un taux d'apprentissage (*learning rate*) adapté (ni trop faible pour pouvoir repousser la droite hors de la grille en moins de 16 étapes, ni trop élevé pour éviter les oscillations excessives), les mises à jour déclenchées par les points positifs mal classés repoussent progressivement la frontière de décision jusqu'à englober l'intégralité de la grille dans la zone positive. Une fois la droite sortie de la grille, les 8 points positifs sont correctement classés et seul le point négatif central reste en erreur, stabilisant la précision à **88,9 %**[cite: 17].

---

### 🚩 Étape 3 : Validation et obtention du Flag

Dès que le perceptron atteint l'objectif théorique maximal de **88,9 %** de précision, l'interface valide la résolution du challenge et révèle le flag[cite: 17].

**Flag :** `academy{...}` *(remplacez par le flag exact affiché sur votre instance)*

---

### 💡 Key Takeaways / Notions retenues

- **Topologies concentriques et non-séparabilité :** Une distribution où une classe est enfermée à l'intérieur d'une autre (« hole in the middle ») ne peut pas être séparée par un hyperplan unique. Un perceptron simple finit par ignorer la classe minoritaire enclavée pour maximiser sa précision globale.
- **Équilibre du taux d'apprentissage (*Learning Rate*) :** Avec un nombre limité d'itérations (ici 16 mises à jour), le *learning rate* doit être suffisamment grand pour déplacer rapidement la frontière hors du nuage de points, tout en restant assez contrôlé pour ne pas provoquer de divergence[cite: 17].
- **Rôle des couches cachées et des noyaux :** Pour isoler une région fermée dans l'espace (comme un cercle ou un carré au centre), il faut combiner plusieurs frontières linéaires via un réseau multicouche (MLP) ou projeter les données dans un espace de dimension supérieure (astuce du noyau / *Kernel Trick*).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Train Hole in Middle
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 17]

---

### 📝 Description

> _"Watch a perceptron learn in real time on a 'hole in the middle' pattern: positive points surround one negative center point. The classic perceptron update rule still applies (only misclassified points trigger updates, with no weight decay), but this shape is not linearly separable by a single line. Reach 88.9% accuracy to reveal the flag."_[cite: 17]

The hints highlight:
1. You get **16** updates per run, and correctly classified points do not change the model in the classic rule.
2. The learning-rate sweep is wide (`0.02` through `20.0`), so very high values can swing the boundary aggressively[cite: 17].

---

### 🔍 Step 1: Understanding the "Hole in the Middle" Pattern & Non-Separability

In this setup, the dataset forms a 3×3 grid of **9 points**: **8 positive points** surround **1 negative point** located right in the center[cite: 17].

Because a single-layer perceptron can only learn a **single linear decision boundary** (one straight line), it is geometrically impossible to enclose the center point and separate it from the surrounding ring. Any straight line cutting through the grid will inevitably group the negative center together with several positive points.

Therefore, the optimal strategy for a linear classifier is to push the decision boundary completely outside the grid so that it predicts **all 9 points as positive**. This correctly classifies **8 out of 9 points**, yielding $8 / 9 \approx \mathbf{88.9\%}$ accuracy[cite: 17].

---

### 🛠️ Step 2: Training & Tuning the Learning Rate

After launching the challenge instance and opening the web interface, we use the real-time simulator to train the perceptron within a budget of **16 updates**[cite: 17].

By choosing an appropriate learning rate (large enough to push the boundary outside the grid within 16 steps, yet controlled enough to avoid wild oscillations), updates from misclassified positive points steadily push the decision line past the outer edge of the grid. Once the boundary clears all positive points, only the center negative point remains misclassified, locking accuracy at **88.9%**[cite: 17].

---

### 🚩 Step 3: Reaching the Target & Retrieving the Flag

As soon as the perceptron reaches the maximum achievable accuracy of **88.9%**, the application confirms the solution and reveals the flag[cite: 17].

**Flag:** `academy{...}` *(replace with the exact flag displayed on your instance)*

---

### 💡 Key Takeaways

- **Concentric Distributions & Non-Separability:** Datasets where one class is completely enclosed inside another ("hole in the middle") cannot be separated by a single hyperplane. A single perceptron maximizes accuracy by sacrificing the enclosed minority class.
- **Balancing Learning Rate & Step Budget:** Under a tight update budget (16 steps), the learning rate must be tuned carefully—high enough to shift the boundary across the feature space quickly, without overshooting into instability[cite: 17].
- **Need for Hidden Layers or Kernels:** Enclosing a bounded region in feature space requires combining multiple linear boundaries using a Multi-Layer Perceptron (MLP) or mapping inputs into a higher-dimensional space (such as with kernel methods).