# Write-Up : information

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** information[cite: 16]
- **Plateforme / Événement :** picoCTF 2021[cite: 16]
- **Auteur :** susie[cite: 16]
- **Catégorie :** Forensics[cite: 16]
- **Difficulté :** Easy[cite: 16]

---

### 📝 Description

> _"Files can always be changed in a secret way. Can you find the flag? cat.jpg"_[cite: 16]

---

### 🔍 Étape 1 : Inspection initiale avec `strings`

On télécharge le fichier image `cat.jpg`[cite: 16]. On tente d'abord d'extraire les chaînes textuelles brutes du fichier binaire :

```bash
strings cat.jpg
```

**Observation :**
Aucun flag ni indice évident n'apparaît directement dans la sortie de cette commande.

---

### 🛠️ Étape 2 : Analyse des métadonnées (`exiftool`)

En s'appuyant sur l'indice du challenge (_"Look at the details of the file"_)[cite: 16], on inspecte les métadonnées EXIF cachées dans l'image à l'aide d'**ExifTool** :

```bash
exiftool cat.jpg
```

**Observation :**
En parcourant les différents champs de métadonnées, on remarque que le champ **License** contient une chaîne de caractères suspecte encodée en **Base64**.

---

### 🚩 Étape 3 : Décodage du Flag

On extrait la chaîne du champ **License** et on la décode depuis le terminal :

```bash
echo "<chaine_base64>" | base64 -d
```

**Résultat :**
Le décodage de la chaîne révèle directement le flag en clair.

**Flag :** `picoCTF{...}` _(ou `academy{...}` selon le format du challenge)_[cite: 16]

---

### 💡 Key Takeaways / Notions retenues

- Lorsque l'outil `strings` ne donne aucun résultat, les métadonnées (EXIF) sont la cible privilégiée suivante en analyse Forensics d'images.
- Les champs de métadonnées moins habituels comme **`License`**, **`Copyright`** ou **`Comment`** sont fréquemment utilisés pour masquer des charges utiles encodées en Base64.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** information[cite: 16]
- **Platform / Event:** picoCTF 2021[cite: 16]
- **Author:** susie[cite: 16]
- **Category:** Forensics[cite: 16]
- **Difficulty:** Easy[cite: 16]

---

### 📝 Description

> _"Files can always be changed in a secret way. Can you find the flag? cat.jpg"_[cite: 16]

---

### 🔍 Step 1: Initial Inspection (`strings`)

We download the `cat.jpg` image file[cite: 16]. We first attempt to extract printable ASCII strings from the binary:

```bash
strings cat.jpg
```

**Observation:**
No plaintext flag or obvious hints are revealed through this method.

---

### 🛠️ Step 2: Metadata Analysis (`exiftool`)

Following the challenge hint (_"Look at the details of the file"_)[cite: 16], we analyze the image's EXIF metadata using **ExifTool**:

```bash
exiftool cat.jpg
```

**Observation:**
Inspecting the metadata output reveals a suspicious Base64-encoded string stored inside the **License** field.

---

### 🚩 Step 3: Base64 Decoding & Flag Retrieval

We extract the Base64 string from the **License** attribute and decode it in the terminal:

```bash
echo "<base64_string>" | base64 -d
```

**Result:**
The command decodes the string and outputs the plaintext flag.

**Flag:** `picoCTF{...}` _(or `academy{...}` depending on the environment requirements)_[cite: 16]

---

### 💡 Key Takeaways

- When standard printable text extraction (`strings`) yields no leads, examining embedded EXIF metadata using **ExifTool** is the next essential step.
- Non-standard metadata attributes such as **`License`**, **`Copyright`**, or **`UserComment`** are common places for hiding Base64-encoded flags.
