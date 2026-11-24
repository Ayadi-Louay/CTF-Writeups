# Write-Up : Perceptron Train Classic 0

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Train Classic 0
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 18]

---

### 📝 Description

> _"Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. This dataset is intentionally gentle, so many learning rates still converge quickly. Dial in a rate, trigger a run, and the interface will animate each step until every point is classified correctly. Visit the service in your browser: `http://xebec.cylabacademy.net:40103/`"_[cite: 18]

---

### 🔍 Étape 1 : Comprendre la règle classique de mise à jour du Perceptron

Contrairement aux problèmes non linéaires comme XOR ou XNOR, le jeu de données proposé dans ce challenge est **linéairement séparable** et volontairement simple (« intentionally gentle »)[cite: 18].

L'algorithme d'entraînement suit la **règle d'apprentissage classique du perceptron** :
- Le modèle évalue les points un par un à l'aide de sa frontière de décision linéaire (une droite).
- Si un point est **correctement classé**, aucune modification n'est apportée aux poids ni au biais.
- Si un point est **mal classé**, les poids ($w$) et le biais ($b$) sont ajustés proportionnellement au taux d'apprentissage (*learning rate* $\eta$) afin de rapprocher la frontière de décision du bon côté de ce point[cite: 18].

D'après le théorème de convergence du perceptron, dès lors qu'un jeu de données est linéairement séparable, cet algorithme est mathématiquement garanti de converger en un nombre fini d'étapes.

---

### 🛠️ Étape 2 : Configuration et exécution de l'entraînement

En accédant au service web (`http://xebec.cylabacademy.net:40103/`)[cite: 18], on accède au simulateur interactif.

1. On choisit un taux d'apprentissage (*learning rate*) standard (par exemple `0.1`, `0.5` ou `1.0`). Le jeu de données étant bien séparé, une large gamme de valeurs converge rapidement sans oscillation excessive[cite: 18].
2. On lance l'entraînement (*trigger a run*)[cite: 18]. L'interface anime alors étape par étape chaque mise à jour déclenchée par les points mal classés jusqu'à ce que la droite sépare proprement les deux classes[cite: 18].

---

### 🚩 Étape 3 : Convergence à 100 % et obtention du Flag

Une fois que tous les points du jeu de données sont correctement classés (précision de **100 %**)[cite: 18], l'entraînement s'arrête et le serveur affiche le flag sur l'interface.

**Flag :** `academy{...}` *(remplacez par le flag exact affiché sur votre instance)*

---

### 💡 Key Takeaways / Notions retenues

- **Théorème de convergence du Perceptron :** Si un ensemble d'entraînement est linéairement séparable, la règle de mise à jour classique du perceptron (correction uniquement sur les erreurs) trouve obligatoirement un hyperplan séparateur en un nombre fini d'itérations.
- **Apprentissage piloté par l'erreur (*Error-Driven Learning*) :** Les points déjà bien classés n'ont aucun impact sur les poids du modèle ; seule l'erreur de classification déclenche une mise à jour[cite: 18].
- **Stabilité sur données simples :** Lorsque les deux classes sont clairement espacées, le modèle est peu sensible au choix exact du taux d'apprentissage et converge rapidement vers une solution valide[cite: 18].

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Train Classic 0
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 18]

---

### 📝 Description

> _"Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. This dataset is intentionally gentle, so many learning rates still converge quickly. Dial in a rate, trigger a run, and the interface will animate each step until every point is classified correctly. Visit the service in your browser: `http://xebec.cylabacademy.net:40103/`"_[cite: 18]

---

### 🔍 Step 1: Understanding the Classic Perceptron Update Rule

Unlike non-linear problems such as XOR or XNOR, the dataset in this challenge is **linearly separable** and intentionally well-behaved ("intentionally gentle")[cite: 18].

The training process follows the **classic perceptron learning rule**:
- The model evaluates points against its linear decision boundary (a straight line).
- If a point is **correctly classified**, the weights and bias remain unchanged.
- If a point is **misclassified**, the weights ($w$) and bias ($b$) are updated proportionally to the learning rate ($\eta$) to shift the decision boundary toward classifying that point properly[cite: 18].

According to the Perceptron Convergence Theorem, whenever a dataset is linearly separable, this algorithm is mathematically guaranteed to find a separating line in a finite number of steps.

---

### 🛠️ Step 2: Configuring and Running the Training

Visiting the web service (`http://xebec.cylabacademy.net:40103/`)[cite: 18] opens the interactive perceptron trainer.

1. Select a standard learning rate (such as `0.1`, `0.5`, or `1.0`). Because the dataset is clean and well-separated, a wide range of learning rates converges quickly without overshooting[cite: 18].
2. Trigger a training run[cite: 18]. The interface animates each update step caused by misclassified points until the line cleanly separates both classes[cite: 18].

---

### 🚩 Step 3: Reaching 100% Accuracy & Retrieving the Flag

Once every point in the dataset is classified correctly (**100%** accuracy)[cite: 18], the simulation finishes and reveals the flag on screen.

**Flag:** `academy{...}` *(replace with the exact flag displayed on your instance)*

---

### 💡 Key Takeaways

- **Perceptron Convergence Theorem:** Whenever a training set is linearly separable, the classic perceptron update rule (updating solely on misclassifications) is guaranteed to converge to a valid separating hyperplane in finite steps.
- **Error-Driven Learning:** Correctly classified examples exert zero influence on model weights; learning only occurs when the model makes a mistake[cite: 18].
- **Robustness on Clean Datasets:** When classes have a clear margin between them, the perceptron is tolerant to a broad spectrum of learning rates and converges reliably[cite: 18].