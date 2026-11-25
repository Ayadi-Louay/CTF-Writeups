# Write-Up : Neuron Express 0

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Neuron Express 0
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy

---

### 📝 Description

> _"Probe the 1D perceptron, then submit its weight and bias. Send an integer within the bounds to see if the perceptron fires (1) or stays quiet (0)."_

Contraintes et règles de l'environnement :
- **Domaine d'entrée :** Entiers $x \in [-10, 10]$
- **Règle d'activation :** $w \cdot x + b \ge 0 \rightarrow \mathbf{1}$, sinon $\mathbf{0}$
- **Validation :** La commande `TEST w b` vérifie que le couple $(w, b)$ reproduit exactement les sorties du perceptron cible pour tous les entiers $x$ de l'intervalle $[-10, 10]$.

---

### 🔍 Étape 1 : Sondage par recherche dichotomique (Binary Search)

Contrairement aux défis précédents où il fallait simplement produire une séquence de sortie, l'objectif ici est d'**extraire les paramètres du modèle** ($w$ et $b$) qui gouvernent la frontière de décision en 1D.

En envoyant quelques entiers ciblés pour localiser le point de bascule ($w \cdot x + b = 0$) :
1. Pour $x = 0$ : le neurone reste silencieux (**`0`**), donc $b < 0$.
2. Pour $x = 1$ : le neurone reste silencieux (**`0`**), donc $w + b < 0$.
3. Pour $x = 2$ : le neurone s'active (**`1`**), donc $2w + b \ge 0$.

---

### 🛠️ Étape 2 : Déduction des paramètres $(w, b)$

Les trois requêtes précédentes encadrent strictement le seuil de décision entre $x = 1$ (sortie `0`) et $x = 2$ (sortie `1`) :
- Pour tout entier $x \le 1$, la sortie est `0`.
- Pour tout entier $x \ge 2$, la sortie est `1`.

Comme la validation porte uniquement sur les valeurs entières de $[-10, 10]$, n'importe quel couple $(w, b)$ dont le seuil $x = -b / w$ appartient à l'intervalle $]1, 2]$ est équivalent sur ce domaine. En choisissant un poids unitaire $w = 1$ et un biais $b = -2$ (plaçant le seuil exactement en $x = 2$), on obtient :
$$z = 1 \cdot x - 2$$
- Pour $x = 1$ : $z = 1(1) - 2 = -1 < 0 \rightarrow \mathbf{0}$
- Pour $x = 2$ : $z = 1(2) - 2 = 0 \ge 0 \rightarrow \mathbf{1}$

---

### 🚩 Étape 3 : Soumission et obtention du Flag

On soumet les paramètres déduits à l'aide de la commande `TEST` :

```text
[1/128] x> 0
Perceptron stays quiet.
[2/128] x> 1
Perceptron stays quiet.
[3/128] x> 2
Perceptron fires!
[4/128] x> test 1 -2
Perfect match! Here is your flag:
academy{n3ur0n_expr_a7737bfb}
```

**Flag :** `academy{n3ur0n_expr_a7737bfb}`

---

### 💡 Key Takeaways / Notions retenues

- **Extraction de modèle (*Model Extraction*) :** En observant les réponses d'un classifieur linéaire sur des entrées stratégiques, on peut localiser sa frontière de décision et reconstruire des poids fonctionnellement équivalents en seulement quelques requêtes.
- **Équivalence fonctionnelle sur domaine discret :** Sur un ensemble discret d'entrées (ici les entiers de $[-10, 10]$), une infinité de couples $(w, b)$ partageant la même frontière entre deux entiers consécutifs produisent exactement les mêmes prédictions.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Neuron Express 0
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy

---

### 📝 Description

> _"Probe the 1D perceptron, then submit its weight and bias. Send an integer within the bounds to see if the perceptron fires (1) or stays quiet (0)."_

Environment rules and constraints:
- **Input bounds:** Integers $x \in [-10, 10]$
- **Output rule:** $w \cdot x + b \ge 0 \rightarrow \mathbf{1}$, else $\mathbf{0}$
- **Submission:** The `TEST w b` command verifies that your $(w, b)$ pair matches the target perceptron's outputs for every integer $x \in [-10, 10]$.

---

### 🔍 Step 1: Probing the Threshold

Unlike earlier challenges focused on generating a specific output sequence, the goal here is **model extraction**: recovering a weight ($w$) and bias ($b$) that replicate the hidden 1D decision boundary.

By probing consecutive integers to pinpoint where the output flips from `0` to `1`:
1. At $x = 0$: the perceptron stays quiet (**`0`**), meaning $b < 0$.
2. At $x = 1$: the perceptron stays quiet (**`0`**), meaning $w + b < 0$.
3. At $x = 2$: the perceptron fires (**`1`**), meaning $2w + b \ge 0$.

---

### 🛠️ Step 2: Deducing the Weight and Bias $(w, b)$

These three probes strictly bracket the decision threshold between $x = 1$ (output `0`) and $x = 2$ (output `1`):
- For every integer $x \le 1$, the output is `0`.
- For every integer $x \ge 2$, the output is `1`.

Because the verification checks outputs strictly across integers in $[-10, 10]$, any $(w, b)$ pair whose threshold $x = -b / w$ lies in the interval $(1, 2]$ is functionally identical on this domain. Choosing $w = 1$ and $b = -2$ places the threshold right at $x = 2$:
$$z = 1 \cdot x - 2$$
- At $x = 1$: $z = 1(1) - 2 = -1 < 0 \rightarrow \mathbf{0}$
- At $x = 2$: $z = 1(2) - 2 = 0 \ge 0 \rightarrow \mathbf{1}$

---

### 🚩 Step 3: Submitting the Guess & Retrieving the Flag

We submit the deduced parameters using the `TEST` command:

```text
[1/128] x> 0
Perceptron stays quiet.
[2/128] x> 1
Perceptron stays quiet.
[3/128] x> 2
Perceptron fires!
[4/128] x> test 1 -2
Perfect match! Here is your flag:
academy{n3ur0n_expr_a7737bfb}
```

**Flag:** `academy{n3ur0n_expr_a7737bfb}`

---

### 💡 Key Takeaways

- **Model Extraction via Probing:** Querying a linear classifier with targeted inputs makes it possible to locate its decision boundary and reconstruct functionally equivalent parameters in just a few steps.
- **Functional Equivalence on Discrete Domains:** When inputs are restricted to discrete integers ($[-10, 10]$), infinitely many $(w, b)$ pairs whose decision boundary falls between the same two adjacent integers produce identical classification behavior.