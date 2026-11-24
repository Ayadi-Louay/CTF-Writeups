# Write-Up : Perceptron Play 1D Alpha

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Perceptron Play 1D Alpha
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy

---

### 📝 Description

> _"Play with the weight and bias of a 1D perceptron on a number line. Adjust the parameters until every labeled point is classified correctly and you will earn the flag. Connect with netcat: `$ nc xebec.cylabacademy.net 40196`"_

---

### 🔍 Étape 1 : Connexion et analyse des points sur la droite numérique

En se connectant à l'instance via `netcat` (`nc xebec.cylabacademy.net 40196`), on accède à un environnement interactif représentant un perceptron monocouche à une dimension. La fonction d'activation calcule $z = w \cdot x + b$, classant le point en classe `1` si $z \ge 0$ et en classe `0` si $z < 0$.

Avec les paramètres initiaux (`w = 1`, `b = 0`), la frontière de décision ($w \cdot x + b = 0$) se situe exactement en $x = 0$. En inspectant la liste des points via la commande `POINTS`, on observe la répartition suivante :

- **Classe `0` :** $x \in \{-4, -2, 0\}$
- **Classe `1` :** $x \in \{+2, +3, +4\}$

Le point en $x = 0$ (étiqueté `0`) donne une activation $z = 1 \cdot 0 + 0 = 0$, ce qui le fait basculer à tort dans la classe `1` (marqué `x` sur la droite).

---

### 🛠️ Étape 2 : Déplacement de la frontière de décision

Pour séparer proprement les deux classes, il faut placer le seuil de décision $x = -b / w$ strictement entre $0$ et $+2$ (par exemple en $x = +1$).

En conservant le poids $w = 1$ et en fixant le biais à $b = -1$ à l'aide de la commande `SET` (en passant directement les deux valeurs numériques sans les noms des variables) :

```text
> SET 1 -1
```

L'équation devient z=1⋅x−1, plaçant la frontière de décision (^) en x=+1 :

- At $x = 0$: $z = 1(0) - 1 = -1 < 0 \rightarrow$ **Class `0`** (correct)
- At $x = +2$: $z = 1(2) - 1 = +1 \ge 0 \rightarrow$ **Class `1`** (correct)

Tous les points de la droite numérique s'affichent désormais avec leur étiquette valide (`0 . 0 . 0 . 1 1 1`).

### 🚩 Étape 3 : Vérification et obtention du Flag

Une fois l'ensemble des points correctement classés, on exécute la commande CHECK pour valider la configuration et obtenir le flag.

```Plaintext
> CHECK
```

Perfect! All points are classified correctly.  
**Flag :** `academy{...}` (remplacez par le flag exact affiché juste en dessous sur votre terminal)

### 💡 Key Takeaways / Notions retenues

- **Rôle géométrique du Biais (Bias) en 1D :** Dans l'équation w⋅x+b=0, le poids w détermine l'orientation et l'échelle de l'activation, tandis que le biais b permet de translater le seuil de décision (x=−b/w) le long de l'axe sans être contraint de passer par l'origine x=0.
- **Convention de seuil (z≥0) :** Un point situé exactement sur la frontière (w⋅x+b=0) est généralement assigné à la classe positive (1). Décaler légèrement le biais garantit une marge franche pour les points situés à l'origine.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Perceptron Play 1D Alpha
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy

### 📝 Description

> "Play with the weight and bias of a 1D perceptron on a number line. Adjust the parameters until every labeled point is classified correctly and you will earn the flag. Connect with netcat: $ `nc xebec.cylabacademy.net 40196`"

### 🔍 Step 1: Connecting and Analyzing the Number Line Points

Connecting to the challenge instance via `netcat` (nc xebec.cylabacademy.net 40196) launches an interactive 1D single-layer perceptron playground. The perceptron computes z=w⋅x+b, predicting class `1` when z≥0 and class 0 when z<0.

With the default parameters (`w = 1`, `b = 0`), the decision boundary (w⋅x+b=0) sits directly at x=0. Running `POINTS` reveals the target labels:

Class `0`: x∈{−4,−2,0}  
Class `1`: x∈{+2,+3,+4}

Because x=0 (labeled `0`) evaluates to z=1⋅0+0=0, the perceptron misclassifies it as class `1` (marked `x` on the number line).

### 🛠️ Step 2: Shifting the Decision Boundary

To cleanly separate both classes, we need to move the decision threshold x=−b/w strictly between 0 and +2 (for instance, at x=+1).

Keeping the weight at w=1 and setting the bias to b=−1 using the `SET` command (passing the two numeric arguments directly):

```Plaintext
> SET 1 -1
```

The activation equation becomes $z = 1 \cdot x - 1$, shifting the decision boundary marker (`^`) to $x = +1$:

- At $x = 0$: $z = 1(0) - 1 = -1 < 0 \rightarrow$ **Class `0`** (correct)
- At $x = +2$: $z = 1(2) - 1 = +1 \ge 0 \rightarrow$ **Class `1`** (correct)

Every point on the number line now displays as correctly classified (`0 . 0 . 0 . 1 1 1`).

### 🚩 Step 3: Verification and Flag Retrieval

With all points properly separated, running the `CHECK` command validates the solution and prints the flag.

```Plaintext
> CHECK
```

Perfect! All points are classified correctly.  
**Flag:** `academy{...}` (replace with the exact flag printed immediately below in your terminal)

💡 Key Takeaways

- **Geometric Role of Bias in 1D:** In w⋅x+b=0, the weight w controls the slope and direction of activation, while the bias b shifts the decision threshold (x=−b/w) along the number line so the boundary does not have to pass through the origin x=0.
- **Boundary Thresholding (z≥0):** Points landing directly on the decision boundary (w⋅x+b=0) are typically assigned to the positive class (`1`). Shifting the bias creates a clean margin away from boundary points.
