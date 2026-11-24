# Write-Up : Perceptron Train Classic 2 Alpha

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Train Classic 2 Alpha
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 15]

---

### 📝 Description

> _"Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. In this variant you must find 5 successful learning rates (each reaching 100% accuracy) before the flag is revealed. The dataset is still linearly separable, but it is less toy-like and the separation is less obvious. Dial in a rate, trigger a run, and the interface animates each step. Visit the service in your browser: `http://chatelaine.cylabacademy.net:26060/`"_[cite: 15]

---

### 🔍 Étape 1 : Analyse d'un jeu de données à séparation moins évidente

Dans cette nouvelle étape de la série *Perceptron Train Classic*, le problème reste **linéairement séparable**, ce qui garantit mathématiquement l'existence d'une droite capable de classer 100 % des points[cite: 15]. Cependant, la distribution est moins triviale (« *less toy-like and the separation is less obvious* ») : les deux classes sont beaucoup plus proches et imbriquées, réduisant fortement la marge de séparation[cite: 15].

Conséquences directes sur l'entraînement :
- La plage de taux d'apprentissage (*learning rates*) permettant une convergence rapide devient beaucoup plus étroite.
- Un *learning rate* trop grand fait rebondir la frontière de décision d'un côté à l'autre de la zone critique sans jamais réussir à se caler dans l'interstice étroit séparant les deux classes.
- Un *learning rate* trop faible risque de ne pas déplacer la droite suffisamment vite avant la fin du budget de mises à jour.

---

### 🛠️ Étape 2 : Recherche et validation des 5 taux d'apprentissage

En accédant à l'interface web du challenge (`http://chatelaine.cylabacademy.net:26060/`), on teste méthodiquement des taux d'apprentissage fins compris entre `0.05` et `0.30` afin d'identifier la zone optimale de convergence[cite: 15].

En exécutant successivement l'entraînement avec les 5 valeurs suivantes :
- `0.09`
- `0.18`
- `0.27`
- `0.25`
- `0.19`

Chacun de ces 5 taux d'apprentissage permet au perceptron d'ajuster suffisamment finement ses poids et son biais pour trouver la frontière exacte séparant les deux groupes de points et atteindre **100 % de précision**[cite: 15].

---

### 🚩 Étape 3 : Obtention du Flag

Une fois les 5 taux d'apprentissage validés à **100 % de précision**, l'interface confirme la réussite de l'entraînement (`5/5`) et révèle le flag[cite: 15].

**Flag :** `academy{...}` *(remplacez par le flag exact affiché sur votre instance)*

---

### 💡 Key Takeaways / Notions retenues

- **Marge géométrique et vitesse de convergence :** Plus la marge entre deux classes linéairement séparables est étroite, plus le perceptron a besoin d'itérations et d'un pas d'apprentissage fin pour positionner précisément l'hyperplan séparateur.
- **Éviter le phénomène de dépassement (*Overshooting*) :** Sur des données réalistes et serrées, des mises à jour trop agressives empêchent la stabilisation du modèle ; des valeurs modérées (ici entre `0.09` et `0.27`) offrent le bon compromis entre vitesse de déplacement et précision.
- **Tuning empirique des hyperparamètres :** Lorsque la géométrie des données se complexifie, le réglage des hyperparamètres passe d'une large tolérance à une fenêtre précise qu'il convient d'explorer méthodiquement.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Train Classic 2 Alpha
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 15]

---

### 📝 Description

> _"Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. In this variant you must find 5 successful learning rates (each reaching 100% accuracy) before the flag is revealed. The dataset is still linearly separable, but it is less toy-like and the separation is less obvious. Dial in a rate, trigger a run, and the interface animates each step. Visit the service in your browser: `http://chatelaine.cylabacademy.net:26060/`"_[cite: 15]

---

### 🔍 Step 1: Analyzing a Less Obvious Linear Separation

In this next installment of the *Perceptron Train Classic* series, the dataset remains **linearly separable**, mathematically guaranteeing that a 100% accurate separating line exists[cite: 15]. However, the point distribution is much closer together ("*less toy-like and the separation is less obvious*"), significantly narrowing the margin between the two classes[cite: 15].

This directly impacts training behavior:
- The window of learning rates that converge within the step limit becomes noticeably tighter.
- Overly large learning rates cause the decision boundary to bounce back and forth across the narrow gap without ever settling cleanly between the classes.
- Overly small learning rates move the boundary too slowly to reach full separation before the update budget runs out.

---

### 🛠️ Step 2: Finding and Validating the 5 Learning Rates

Opening the challenge web interface (`http://chatelaine.cylabacademy.net:26060/`), we systematically test fine-grained learning rates in the `0.05` to `0.30` range to locate the stable convergence zone[cite: 15].

Running the perceptron sequentially with the following 5 values:
- `0.09`
- `0.18`
- `0.27`
- `0.25`
- `0.19`

Each of these 5 learning rates enables the perceptron to fine-tune its weights and bias cleanly into the narrow separating margin, achieving **100% classification accuracy**[cite: 15].

---

### 🚩 Step 3: Retrieving the Flag

Once all 5 successful learning rates reach **100% accuracy**, the progress counter (`5/5`) completes and the application reveals the flag[cite: 15].

**Flag:** `academy{...}` *(replace with the exact flag displayed on your instance)*

---

### 💡 Key Takeaways

- **Geometric Margin & Convergence:** The narrower the margin separating two linearly separable classes, the more delicate the weight updates must be to thread the hyperplane cleanly between them.
- **Preventing Overshooting:** On tighter, more realistic datasets, aggressive step sizes prevent convergence; moderate values (here between `0.09` and `0.27`) balance movement speed with positional precision.
- **Empirical Hyperparameter Tuning:** As data geometry becomes less trivial, viable hyperparameter ranges shrink, making structured, methodical probing essential.