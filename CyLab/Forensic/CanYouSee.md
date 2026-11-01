# Write-Up : CanYouSee

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** CanYouSee[cite: 15]
- **Plateforme / Événement :** picoCTF 2024[cite: 15]
- **Auteur :** Mubarak Mikail[cite: 15]
- **Catégorie :** Forensics[cite: 15]
- **Difficulté :** Easy[cite: 15]

---

### 📝 Description

> _"How about some hide and seek? Download this file here."_[cite: 15]

---

### 🔍 Étape 1 : Inspection des métadonnées avec `exiftool`

On télécharge le fichier image fourni[cite: 15]. En suivant le premier indice (_"How can you view the information about the picture?"_)[cite: 15], on inspecte ses métadonnées à l'aide de l'outil **ExifTool** :

```bash
exiftool image.jpg
```

**Observation :**
En analysant la liste des métadonnées affichées, on remarque que le champ **Author** (ou **Artist**) contient une chaîne de caractères anormale encodée en **Base64**[cite: 15].

---

### 🛠️ Étape 2 : Décodage du Flag

On extrait la chaîne de caractères du champ **Author** et on la décode depuis le terminal (ou à l'aide de CyberChef)[cite: 15] :

```bash
echo "<chaine_base64>" | base64 -d
```

**Résultat :**
Le décodage de la chaîne révèle directement le flag en clair.

**Flag :** `picoCTF{...}` _(à remplacer par le flag obtenu)_

---

### 💡 Key Takeaways / Notions retenues

- L'outil **ExifTool** permet de lire et analyser les métadonnées (EXIF) masquées au sein des fichiers multimédias.
- Les champs de métadonnées tels que `Author`, `Artist` ou `Comment` sont très souvent exploités en Forensics pour cacher des informations encodées.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** CanYouSee[cite: 15]
- **Platform / Event:** picoCTF 2024[cite: 15]
- **Author:** Mubarak Mikail[cite: 15]
- **Category:** Forensics[cite: 15]
- **Difficulty:** Easy[cite: 15]

---

### 📝 Description

> _"How about some hide and seek? Download this file here."_[cite: 15]

---

### 🔍 Step 1: Metadata Inspection using `exiftool`

We download the provided image file[cite: 15]. Following the first hint (_"How can you view the information about the picture?"_)[cite: 15], we inspect its metadata using **ExifTool**:

```bash
exiftool image.jpg
```

**Observation:**
While reviewing the metadata output, we notice a suspicious Base64-encoded string inside the **Author** (or **Artist**) field[cite: 15].

---

### 🛠️ Step 2: Flag Decoding

We extract the Base64 string from the **Author** attribute and decode it using the terminal (or CyberChef)[cite: 15]:

```bash
echo "<base64_string>" | base64 -d
```

**Result:**
The decoded payload reveals the plaintext flag.

**Flag:** `picoCTF{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- **ExifTool** is an essential CLI tool for inspecting hidden metadata attributes embedded within media files.
- Metadata fields such as `Author`, `Artist`, or `Comment` are frequently utilized in forensics challenges to store encoded payloads (Base64, Hex, etc.).
