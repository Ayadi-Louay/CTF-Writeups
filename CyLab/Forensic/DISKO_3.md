# Write-Up : DISKO 3

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** DISKO 3
- **Auteur :** Darkraicg492
- **Catégorie :** Forensics
- **Difficulté :** Medium

---

### 📝 Description

> _"Can you find the flag in this disk image? This time, its not as plain as you think it is! Download the disk image here."_

---

### 🔍 Étape 1 : Décompression et premières tentatives

Après avoir téléchargé l'archive `disko-3.dd.gz`, la première étape a été de la décompresser avec `gzip` :

```bash
gzip -d disko-3.dd.gz
```

J'ai ensuite tenté d'extraire directement le flag via les chaînes de texte imprimables :

```bash
strings disko-3.dd | grep academy
```

**Observation :**
Contrairement aux défis précédents, cette commande ne renvoie aucun résultat. Le flag n'est pas stocké en texte brut dans l'image.

---

### 🛠️ Étape 2 : Inspection des partitions (`fdisk`)

J'ai tenté de vérifier la structure du disque avec `fdisk` :

```bash
fdisk -lu disko-3.dd
```

**Observation :**
L'outil n'affiche pas de table de partition standard directement exploitable avec cette méthode.

---

### ✂️ Étape 3 : Carving et extraction avec `binwalk`

En suivant l'indice du challenge (_"How will you search and extract files in a partition?"_), j'ai utilisé l'outil **`binwalk`** pour analyser la signature binaire du fichier et extraire automatiquement les fichiers ou archives encapsulés :

```bash
binwalk -e disko-3.dd
```

**Résultat :**
`binwalk` identifie et extrait la structure interne du système de fichiers dans un répertoire nommé `_disko-3.dd.extracted/`.

---

### 🚩 Étape 4 : Récupération du Flag

1. Accès au répertoire d'extraction généré par `binwalk`.
2. Recherche du fichier contenant le flag (nommé `flag`).
3. Lecture du contenu du fichier :

```bash
cat _disko-3.dd.extracted/flag
```

**Flag :** `academy{...}` _(à remplacer par ton flag)_

---

### 💡 Key Takeaways / Notions retenues

- Lorsque le texte brut n'est pas lisible avec `strings`, le fichier recherché peut être compressé, archivé ou imbriqué à l'intérieur d'un système de fichiers.
- **`binwalk -e`** est l'un des outils de stéganographie/forensics les plus puissants pour scanner des données binaires et extraire automatiquement des fichiers cachés (_file carving_).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** DISKO 3
- **Author:** Darkraicg492
- **Category:** Forensics
- **Difficulty:** Medium

---

### 📝 Description

> _"Can you find the flag in this disk image? This time, its not as plain as you think it is! Download the disk image here."_

---

### 🔍 Step 1: Decompression & Initial Attempts

After downloading `disko-3.dd.gz`, I extracted the archive using `gzip`:

```bash
gzip -d disko-3.dd.gz
```

I first attempted to locate the flag using printable strings:

```bash
strings disko-3.dd | grep academy
```

**Observation:**
Unlike previous challenges, no matching strings were found. The flag is not stored in plain text.

---

### 🛠️ Step 2: Partition Inspection (`fdisk`)

I tried inspecting the partition layout using `fdisk`:

```bash
fdisk -lu disko-3.dd
```

**Observation:**
No standard partition scheme was returned for immediate partition isolation.

---

### ✂️ Step 3: File Carving with `binwalk`

Following the challenge hint (_"How will you search and extract files in a partition?"_), I utilized **`binwalk`** to scan the raw binary for signatures and automatically carve out hidden embedded files:

```bash
binwalk -e disko-3.dd
```

**Result:**
`binwalk` successfully analyzed the image and extracted the inner file system contents into a directory named `_disko-3.dd.extracted/`.

---

### 🚩 Step 4: Flag Retrieval

1. Navigated to the extracted contents directory `_disko-3.dd.extracted/`.
2. Located the file named `flag`.
3. Displayed its contents:

```bash
cat _disko-3.dd.extracted/flag
```

**Flag:** `academy{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- If `strings` yields no results, target files might be archived, compressed, or buried deeper within file system structures.
- **`binwalk -e`** is an essential forensics tool for automated file carving and signature analysis in binary files and raw disk images.
