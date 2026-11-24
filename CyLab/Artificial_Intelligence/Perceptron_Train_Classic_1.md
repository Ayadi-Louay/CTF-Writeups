# Write-Up : Perceptron Train Classic 1

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Train Classic 1
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy

---

### 📝 Description

> _"Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. In this variant you must find 5 successful learning rates (each reaching 100% accuracy) before the flag is revealed. Dial in a rate, trigger a run, and the interface animates each step. Visit the service in your browser: `http://chatelaine.cylabacademy.net:13287/`"_

L'indice principal rappelle la contrainte d'entraînement : vous disposez d'un budget strict de **16 mises à jour** par exécution, et les points correctement classés ne modifient pas les poids du modèle selon la règle classique.

---

### 🔍 Étape 1 : Comprendre l'impact du taux d'apprentissage sous contrainte d'itérations

Contrairement à _Perceptron Train Classic 0_ où une seule exécution réussie suffisait, cette variante exige de trouver **5 taux d'apprentissage (_learning rates_) distincts** permettant chacun d'atteindre **100 % de précision** en au plus **16 mises à jour**.

Le jeu de données étant plus sensible, le choix du _learning rate_ ($\eta$) devient déterminant :

- **S'il est trop élevé :** Chaque correction sur un point mal classé déplace la frontière de décision trop brutalement, provoquant des oscillations qui empêchent le modèle de se stabiliser en 16 étapes.
- **S'il est faible à modéré :** Les ajustements des poids ($w$) et du biais ($b$) sont plus fins et progressifs, permettant à la droite de se glisser précisément entre les deux classes dans le budget d'itérations imparti.

---

### 🛠️ Étape 2 : Sélection et validation des 5 taux d'apprentissage

En accédant à l'interface web du challenge (`http://chatelaine.cylabacademy.net:13287/`), on teste systématiquement des valeurs de _learning rate_ relativement faibles afin d'éviter toute divergence.

En lançant successivement les entraînements avec les 5 valeurs suivantes :

- `0.2`
- `0.15`
- `0.11`
- `0.02`
- `0.09`

Chacun de ces 5 taux d'apprentissage permet au perceptron de converger proprement vers une séparation linéaire parfaite (**100 % de précision**) avant d'épuiser les 16 mises à jour autorisées.

---

### 🚩 Étape 3 : Obtention du Flag

Une fois la cinquième valeur validée à **100 % de précision**, le compteur de réussites (`5/5`) se complète et le serveur affiche le flag sur l'interface.

**Flag :** `academy{...}` _(remplacez par le flag exact affiché sur votre instance)_

---

### 💡 Key Takeaways / Notions retenues

- **Sensibilité au taux d'apprentissage (_Learning Rate Sensitivity_) :** Lorsque la marge séparant deux classes est étroite, des taux d'apprentissage faibles (ici entre `0.02` et `0.2`) offrent la précision nécessaire pour ajuster finement l'hyperplan sans dépasser la cible (_overshooting_).
- **Budget de calcul et convergence :** Un algorithme théoriquement convergent peut échouer en pratique s'il est soumis à une limite stricte d'itérations (16 mises à jour) avec un pas d'apprentissage mal calibré.
- **Exploration d'hyperparamètres :** En apprentissage automatique, tester méthodiquement plusieurs valeurs dans une plage pertinente permet d'identifier la zone de stabilité d'un modèle.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Train Classic 1
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy

---

### 📝 Description

> _"Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. In this variant you must find 5 successful learning rates (each reaching 100% accuracy) before the flag is revealed. Dial in a rate, trigger a run, and the interface animates each step. Visit the service in your browser: `http://chatelaine.cylabacademy.net:13287/`"_

The first hint reiterates the training constraint: you only get **16 updates** per run, and correctly classified points do not modify the model under the classic update rule.

---

### 🔍 Step 1: Understanding Learning Rate Sensitivity Under Step Limits

Unlike _Perceptron Train Classic 0_ where a single successful run was enough, this variant requires finding **5 distinct learning rates** that each achieve **100% accuracy** within a strict budget of **16 updates**.

Because the dataset has a tighter margin, choosing the right learning rate ($\eta$) is critical:

- **Too high:** Each misclassified point triggers an overly aggressive weight update, causing the decision boundary to swing past the optimal position and fail to converge within 16 steps.
- **Low to moderate:** Weight ($w$) and bias ($b$) adjustments are finer and more controlled, allowing the separating line to settle cleanly between the two classes within the allotted update budget.

---

### 🛠️ Step 2: Testing and Validating the 5 Learning Rates

Opening the challenge web interface (`http://chatelaine.cylabacademy.net:13287/`), we focus on testing small learning rate values to prevent oscillation.

Running the perceptron sequentially with the following 5 values:

- `0.2`
- `0.15`
- `0.11`
- `0.02`
- `0.09`

Each of these 5 learning rates guides the perceptron smoothly to **100% classification accuracy** before exhausting the 16-update limit.

---

### 🚩 Step 3: Retrieving the Flag

Once the fifth successful learning rate hits **100% accuracy**, the completion counter (`5/5`) finishes and the service reveals the flag.

**Flag:** `academy{...}` _(replace with the exact flag displayed on your instance)_

---

### 💡 Key Takeaways

- **Learning Rate Sensitivity:** When the margin between classes is narrow, smaller learning rates (here between `0.02` and `0.2`) provide the granularity needed to fine-tune the decision boundary without overshooting.
- **Iteration Budgets & Practical Convergence:** Even when a dataset is linearly separable, an algorithm can fail to converge in practice if constrained by a tight update budget (16 steps) alongside an overly large step size[cite: 14].
- **Hyperparameter Exploration:** Systematically probing values within a promising range is a core workflow for identifying stable operating regimes in machine learning models.
