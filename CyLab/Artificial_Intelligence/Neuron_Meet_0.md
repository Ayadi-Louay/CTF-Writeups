# Write-Up : Neuron Meet 0

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Neuron Meet 0
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy[cite: 12]

---

### 📝 Description

> _"Probe a 1D perceptron over the network. Send it numbers and watch whether the neuron fires or not. Use those responses to figure out the decision boundary, then line up the last eight outputs to read the ASCII for `p` (`01110000`) and you'll earn the flag. Connect with netcat: `$ nc xebec.cylabacademy.net 28068`"_[cite: 12]

> _"The input bounds are shown on connect to keep the search small. You cannot submit the same number back-to-back."_[cite: 12]

---

### 🔍 Étape 1 : Connexion et analyse du perceptron 1D en boîte noire

En se connectant au service via `netcat` (`nc xebec.cylabacademy.net 28068`), on interagit avec un perceptron monocouche à une dimension dont le poids ($w$) et le biais ($b$) sont cachés[cite: 12].

Le neurone évalue chaque nombre $x \in [-10.0, 10.0]$ selon la règle d'activation linéaire :
$$z = w \cdot x + b$$
- Si $z \ge 0$, le neurone s'active (**`1`**, *Perceptron fires!*).
- Si $z < 0$, le neurone reste silencieux (**`0`**, *Perceptron stays quiet.*).

L'objectif est d'aligner les 8 dernières sorties sur la séquence binaire **`01110000`** (représentant le caractère ASCII `'p'`, soit $112$ en décimal) sans jamais envoyer deux fois de suite exactement la même valeur de $x$[cite: 12].

---

### 🛠️ Étape 2 : Sondage du seuil et génération de `'p'` (`01110000`)

En envoyant quelques valeurs tests sur la droite numérique, on identifie rapidement de quel côté se trouve la frontière de décision ($x = -b / w$) :
1. L'entrée `0` renvoie **`0`** (*quiet*), indiquant que l'origine et les valeurs négatives se situent sous le seuil d'activation ($z < 0$).
2. L'entrée `5` renvoie **`1`** (*fires!*), confirmant que les valeurs positives plus élevées dépassent le seuil d'activation ($z \ge 0$).

En choisissant des nombres distincts dans chacune des deux régions, on reconstruit la séquence binaire `01110000` en 8 requêtes consécutives :

```text
[1/128] x> 0     -> 0  (Recent outputs: 0)
[2/128] x> 5     -> 1  (Recent outputs: 01)
[3/128] x> 6     -> 1  (Recent outputs: 011)
[4/128] x> 7     -> 1  (Recent outputs: 0111)
[5/128] x> -1    -> 0  (Recent outputs: 01110)
[6/128] x> -2    -> 0  (Recent outputs: 011100)
[7/128] x> -3    -> 0  (Recent outputs: 0111000)
[8/128] x> -4    -> 0  (Recent outputs: 01110000)
```

---

### 🚩 Étape 3 : Validation du motif et obtention du Flag

Au 8ᵉ envoi, la mémoire tampon des 8 dernières sorties correspond exactement au code binaire ASCII de `'p'` (`01110000`) et le serveur affiche immédiatement le flag :

```text
Pattern matched! ASCII 'p' unlocked. Here is your flag:
academy{n3ur0n_m3t_fa5886bd}
```

**Flag :** `academy{n3ur0n_m3t_fa5886bd}`

---

### 💡 Key Takeaways / Notions retenues

- **Identification d'un seuil en 1D :** Sur une droite numérique, un perceptron divise l'espace en deux demi-droites autour d'un unique point seuil ($x = -b/w$). Quelques requêtes suffisent à borner et exploiter cette frontière.
- **Représentation binaire ASCII :** Chaque caractère ASCII standard est codé sur 8 bits ; le caractère `'p'` correspond à $112_{10} = 01110000_2$.
- **Sondage de modèles (*Black-Box Probing*) :** Observer les réponses binaires d'un modèle face à des entrées choisies permet d'inférer son comportement sans avoir accès à ses paramètres internes.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Neuron Meet 0
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy[cite: 12]

---

### 📝 Description

> _"Probe a 1D perceptron over the network. Send it numbers and watch whether the neuron fires or not. Use those responses to figure out the decision boundary, then line up the last eight outputs to read the ASCII for `p` (`01110000`) and you'll earn the flag. Connect with netcat: `$ nc xebec.cylabacademy.net 28068`"_[cite: 12]

> _"The input bounds are shown on connect to keep the search small. You cannot submit the same number back-to-back."_[cite: 12]

---

### 🔍 Step 1: Connecting and Probing the 1D Black-Box Perceptron

Connecting to the instance via `netcat` (`nc xebec.cylabacademy.net 28068`) gives us access to a 1D single-layer perceptron whose weight ($w$) and bias ($b$) are hidden[cite: 12].

The neuron evaluates each scalar input $x \in [-10.0, 10.0]$ using the linear threshold rule:
$$z = w \cdot x + b$$
- If $z \ge 0$, the perceptron fires (**`1`**, *Perceptron fires!*).
- If $z < 0$, the perceptron stays quiet (**`0`**, *Perceptron stays quiet.*).

Our objective is to align the last 8 outputs to **`01110000`** (the 8-bit ASCII binary encoding for `'p'`, decimal $112$), while obeying the rule against submitting the exact same number twice in a row[cite: 12].

---

### 🛠️ Step 2: Locating the Threshold & Generating `'p'` (`01110000`)

By probing a couple of test numbers along the number line, we quickly determine which side of the threshold ($x = -b / w$) produces each output:
1. Sending `0` outputs **`0`** (*quiet*), showing that zero and negative numbers fall below the firing threshold ($z < 0$).
2. Sending `5` outputs **`1`** (*fires!*), confirming that larger positive values exceed the threshold ($z \ge 0$).

Using distinct numbers from both regions, we construct the exact 8-bit sequence `01110000` in 8 queries:

```text
[1/128] x> 0     -> 0  (Recent outputs: 0)
[2/128] x> 5     -> 1  (Recent outputs: 01)
[3/128] x> 6     -> 1  (Recent outputs: 011)
[4/128] x> 7     -> 1  (Recent outputs: 0111)
[5/128] x> -1    -> 0  (Recent outputs: 01110)
[6/128] x> -2    -> 0  (Recent outputs: 011100)
[7/128] x> -3    -> 0  (Recent outputs: 0111000)
[8/128] x> -4    -> 0  (Recent outputs: 01110000)
```

---

### 🚩 Step 3: Pattern Match & Flag Retrieval

On the 8th input, the sliding history buffer matches `01110000` (ASCII `'p'`) and the server reveals the flag:

```text
Pattern matched! ASCII 'p' unlocked. Here is your flag:
academy{n3ur0n_m3t_fa5886bd}
```

**Flag:** `academy{n3ur0n_m3t_fa5886bd}`

---

### 💡 Key Takeaways

- **1D Threshold Discovery:** On a number line, a single perceptron partitions inputs into two half-lines around a single threshold point ($x = -b/w$). Just a few probes are enough to locate and exploit this boundary.
- **ASCII Binary Representation:** Standard ASCII characters map directly to 8-bit binary strings—here `'p'` equals $112_{10} = 01110000_2$.
- **Black-Box Model Probing:** Observing binary classification outputs for chosen inputs allows an attacker or analyst to infer a model's decision boundary without direct access to its weights or bias.