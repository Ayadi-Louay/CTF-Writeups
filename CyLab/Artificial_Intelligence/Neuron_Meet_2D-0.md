# Write-Up : Neuron Meet 2D-0

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Neuron Meet 2D-0
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 13]

---

### 📝 Description

> _"Probe a 2D perceptron over the network. Send it pairs of numbers (x, y) and watch whether the neuron fires or not. Use those responses to figure out the decision boundary, then line up the last eight outputs to read the ASCII for `p` (`01110000`) and you'll earn the flag."_[cite: 13]

---

### 🔍 Étape 1 : Connexion et analyse de la boîte noire (Black-Box Probing)

Après avoir lancé l'instance et rejoint le service via `netcat` (`nc xebec.cylabacademy.net 14984`), on interagit avec un neurone artificiel (perceptron 2D) dont les poids internes ($w_1, w_2$) et le biais ($b$) sont cachés.

Le neurone applique la règle d'activation classique :
$$z = w_1 \cdot x + w_2 \cdot y + b$$
- Si $z \ge 0$, le neurone s'active (**`1`**, *Perceptron fires!*).
- Si $z < 0$, le neurone reste silencieux (**`0`**, *Perceptron stays quiet.*).

L'objectif est de générer exactement la séquence binaire **`01110000`** (correspondant au caractère ASCII `'p'`, soit $112$ en décimal) sur les 8 dernières sorties, tout en respectant la contrainte interdisant d'envoyer deux fois de suite exactement la même paire $(x, y)$ dans l'intervalle $[-10.0, 10.0]$.

---

### 🛠️ Étape 2 : Sondage et génération de la séquence ASCII `'p'` (`01110000`)

En testant quelques coordonnées simples pour repérer la frontière de décision séparant les deux demi-plans :
1. Le point `(1, 1)` renvoie **`0`** (*quiet*), ce qui indique que la zone autour de l'origine et des faibles valeurs positives se situe du côté négatif de la frontière ($z < 0$).
2. En envoyant des valeurs positives plus élevées comme `(5, 8)`, le neurone renvoie **`1`** (*fires!*), révélant la zone positive ($z \ge 0$).

Grâce à cette séparation linéaire claire, on peut facilement produire les 8 bits de `01110000` en alternant des points distincts dans chaque région :

```text
[1/128] (x,y)> 1 1     -> 0  (Recent outputs: 0)
[2/128] (x,y)> 5 8     -> 1  (Recent outputs: 01)
[3/128] (x,y)> 7 9     -> 1  (Recent outputs: 011)
[4/128] (x,y)> 7 7     -> 1  (Recent outputs: 0111)
[5/128] (x,y)> 0 0     -> 0  (Recent outputs: 01110)
[6/128] (x,y)> -1 0    -> 0  (Recent outputs: 011100)
[7/128] (x,y)> -1 -1   -> 0  (Recent outputs: 0111000)
[8/128] (x,y)> -1 -2   -> 0  (Recent outputs: 01110000)
```

---

### 🚩 Étape 3 : Validation du motif et obtention du Flag

Dès le 8ᵉ envoi, la mémoire tampon des 8 dernières sorties correspond exactement au code binaire de `'p'` (`01110000`) et le serveur affiche immédiatement le flag :

```text
Pattern matched! ASCII 'p' unlocked. Here is your flag:
academy{2d_n3ur0n_m3t_8c453797}
```

**Flag :** `academy{2d_n3ur0n_m3t_8c453797}`

---

### 💡 Key Takeaways / Notions retenues

- **Inférence par sondage (*Black-Box Probing*) :** Même sans connaître les paramètres internes ($w_1, w_2, b$) d'un classifieur linéaire, il suffit de quelques requêtes ciblées pour cartographier ses demi-plans positif et négatif.
- **Représentation binaire ASCII :** En informatique, chaque caractère ASCII standard est codé sur 8 bits (1 octet) — ici `'p'` vaut $112_{10} = 01110000_2$.
- **Attaques par extraction de modèle (*Model Extraction*) :** Ce mécanisme illustre à petite échelle comment un attaquant peut reconstruire la frontière de décision d'un modèle d'IA exposé via une API en observant simplement ses prédictions en sortie.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Neuron Meet 2D-0
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 13]

---

### 📝 Description

> _"Probe a 2D perceptron over the network. Send it pairs of numbers (x, y) and watch whether the neuron fires or not. Use those responses to figure out the decision boundary, then line up the last eight outputs to read the ASCII for `p` (`01110000`) and you'll earn the flag."_[cite: 13]

---

### 🔍 Step 1: Connecting and Black-Box Probing

After launching the challenge instance and connecting via `netcat` (`nc xebec.cylabacademy.net 14984`), we interact with a 2D single-layer perceptron whose internal weights ($w_1, w_2$) and bias ($b$) are hidden.

The neuron evaluates inputs using the standard step activation rule:
$$z = w_1 \cdot x + w_2 \cdot y + b$$
- If $z \ge 0$, the perceptron fires (**`1`**, *Perceptron fires!*).
- If $z < 0$, the perceptron stays quiet (**`0`**, *Perceptron stays quiet.*).

The goal is to make the last 8 outputs match **`01110000`** (the 8-bit ASCII binary representation of `'p'`, decimal $112$), while respecting the constraint against sending identical $(x, y)$ pairs back-to-back within $[-10.0, 10.0]$.

---

### 🛠️ Step 2: Probing the Boundary & Generating `'p'` (`01110000`)

By querying a few test coordinates, we quickly identify which side of the linear boundary triggers each output:
1. Probing `(1, 1)` returns **`0`** (*quiet*), showing that the origin and small coordinates lie on the negative side ($z < 0$).
2. Probing larger positive coordinates such as `(5, 8)` returns **`1`** (*fires!*), confirming the positive half-plane ($z \ge 0$).

Using distinct coordinates from each region, we construct the exact 8-bit sequence `01110000` in 8 steps:

```text
[1/128] (x,y)> 1 1     -> 0  (Recent outputs: 0)
[2/128] (x,y)> 5 8     -> 1  (Recent outputs: 01)
[3/128] (x,y)> 7 9     -> 1  (Recent outputs: 011)
[4/128] (x,y)> 7 7     -> 1  (Recent outputs: 0111)
[5/128] (x,y)> 0 0     -> 0  (Recent outputs: 01110)
[6/128] (x,y)> -1 0    -> 0  (Recent outputs: 011100)
[7/128] (x,y)> -1 -1   -> 0  (Recent outputs: 0111000)
[8/128] (x,y)> -1 -2   -> 0  (Recent outputs: 01110000)
```

---

### 🚩 Step 3: Pattern Match & Flag Retrieval

On the 8th query, the sliding output buffer matches `01110000` (ASCII `'p'`) and the server immediately prints the flag:

```text
Pattern matched! ASCII 'p' unlocked. Here is your flag:
academy{2d_n3ur0n_m3t_8c453797}
```

**Flag:** `academy{2d_n3ur0n_m3t_8c453797}`

---

### 💡 Key Takeaways

- **Black-Box Probing:** Even when a linear classifier's weights ($w_1, w_2, b$) are hidden, a handful of targeted input queries is enough to map out its positive and negative half-planes.
- **ASCII Binary Encoding:** Standard ASCII characters map directly to 8-bit binary sequences—here `'p'` corresponds to $112_{10} = 01110000_2$.
- **Model Extraction Fundamentals:** Querying a model with chosen inputs to infer its decision boundary is the core mechanism behind model extraction attacks against ML APIs.