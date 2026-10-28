# Write-Up : RED

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** RED
- **Plateforme / Événement :** picoCTF 2025
- **Auteur :** Shuailin Pan (LeConjuror)
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

### 📝 Description

> _"RED, RED, RED, RED Download the image: red.png"_

---

### 🔍 Étape 1 : Analyse initiale avec `strings`

Après avoir téléchargé et visualisé l'image `red.png`, j'ai inspecté les chaînes de texte contenues dans le fichier binaire à l'aide de l'outil `strings` :

```bash
strings red.png
```

**Observation :**
Un poème apparaît dans les résultats. En observant la première lettre de chaque ligne du poème, on découvre un acrostiche formant le mot-clé : **`CHECKLSB`**. Cela indique que des données sont dissimulées via la technique du **LSB** (Least Significant Bit).

---

### 🛠️ Étape 2 : Extraction LSB avec CyberChef

1. Chargement de l'image `red.png` dans **CyberChef**.
2. Utilisation de l'outil d'extraction LSB (**Extract LSB**).
3. Configuration des canaux de couleurs (Red, Green, Blue, Alpha / Red Ged Bed Aed).
4. Un texte encodé en **Base64** est extrait des bits de poids faible de l'image.

---

### 🚩 Étape 3 : Décodage et obtention du Flag

1. Passage du texte extrait dans la recette **`From Base64`** sur CyberChef.
2. Le flag apparaît en clair après décodage.

**Flag :** `picoCTF{...}` _(à remplacer par ton flag)_

---

### 💡 Key Takeaways / Notions retenues

- La stéganographie **LSB (Least Significant Bit)** dissimule des données cachées dans les bits de poids faible des canaux de couleurs d'une image.
- L'analyse des chaînes de caractères (`strings`) permet souvent de trouver des indices subtils (comme des acrostiches) laissés par les concepteurs du challenge.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** RED
- **Platform / Event:** picoCTF 2025
- **Author:** Shuailin Pan (LeConjuror)
- **Category:** Forensics
- **Difficulty:** Easy

---

### 📝 Description

> _"RED, RED, RED, RED Download the image: red.png"_

---

### 🔍 Step 1: Initial Inspection with `strings`

After downloading and viewing `red.png`, I inspected the readable strings inside the binary file using the `strings` command:

```bash
strings red.png
```

**Observation:**
A poem is revealed in the output. Looking at the first letter of each line forms an acrostic spelling **`CHECKLSB`**, hinting at the use of **LSB** (Least Significant Bit) steganography.

---

### 🛠️ Step 2: LSB Extraction using CyberChef

1. Load `red.png` into **CyberChef**.
2. Apply the **Extract LSB** operation.
3. Configure the color channel settings (Red, Green, Blue, Alpha / Red Ged Bed Aed).
4. A **Base64** encoded string is extracted from the image's least significant bits.

---

### 🚩 Step 3: Base64 Decoding and Flag Retrieval

1. Pass the extracted string into the **`From Base64`** recipe in CyberChef.
2. The plaintext flag is decoded.

**Flag:** `picoCTF{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- **LSB (Least Significant Bit)** steganography hides data within the least significant bits of an image's color channels.
- Running `strings` on media files can reveal subtle text hints, such as acrostics, indicating the extraction technique required.
