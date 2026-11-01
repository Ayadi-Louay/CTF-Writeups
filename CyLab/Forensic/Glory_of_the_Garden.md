# Write-Up : Glory of the Garden

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Glory of the Garden
- **Plateforme / Événement :** picoCTF 2019
- **Auteur :** jedavis/Danny
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

### 📝 Description

> _"This file contains more than it seems. Get the flag from garden.jpg."_

---

### 🔍 Étape 1 : Téléchargement du fichier

On télécharge l'image `garden.jpg` fournie dans la description du challenge.

---

### 🛠️ Étape 2 : Extraction du texte avec `strings`

En s'appuyant sur l'indice du challenge concernant la consultation du contenu binaire (_"What is a hex editor?"_), on recherche des chaînes de texte lisibles dissimulées dans l'image à l'aide de l'outil `strings` combiné avec `grep` :

```bash
strings garden.jpg | grep academy
```

_(Remarque : selon l'environnement de jeu, le filtre `grep pico` peut également être utilisé)._

**Observation :**
Le flag est directement concaténé en texte brut à la fin du fichier binaire, juste après l'en-tête et les données d'image JPEG.

---

### 🚩 Étape 3 : Obtention du Flag

La commande isole et affiche directement le flag en clair sur le terminal.

**Flag :** `academy{...}` _(à remplacer par le flag obtenu)_

---

### 💡 Key Takeaways / Notions retenues

- L'outil **`strings`** est une première étape essentielle en analyse Forensics pour repérer du texte lisible ou des chaînes concaténées à la fin de fichiers médias.
- Des données supplémentaires peuvent être insérées après le marqueur de fin d'image JPEG (`FF D9`) sans altérer l'affichage visuel de l'image.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Glory of the Garden
- **Platform / Event:** picoCTF 2019
- **Author:** jedavis/Danny
- **Category:** Forensics
- **Difficulty:** Easy

---

### 📝 Description

> _"This file contains more than it seems. Get the flag from garden.jpg."_

---

### 🔍 Step 1: File Retrieval

We download the `garden.jpg` image file provided in the challenge description.

---

### 🛠️ Step 2: String Extraction via `strings`

Following the challenge hint regarding binary analysis (_"What is a hex editor?"_), we search for human-readable text strings embedded inside the image file by piping `strings` into `grep`:

```bash
strings garden.jpg | grep academy
```

_(Note: `strings garden.jpg | grep pico` can also be used depending on the platform flag prefix)._

**Observation:**
The flag string is appended in plain text directly at the end of the image file binary stream.

---

### 🚩 Step 3: Flag Retrieval

The command filters out the binary noise and outputs the plaintext flag directly to the terminal.

**Flag:** `academy{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- Running **`strings`** is an essential first step in forensic file analysis to discover plain text strings appended to media files.
- Data stored past a file's structural end marker (such as the JPEG EOI `FF D9`) remains invisible to standard image viewers while remaining readable via CLI utilities.
