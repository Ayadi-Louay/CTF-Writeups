# Write-Up : DISKO 1

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** DISKO 1
- **Auteur :** Darkraicg492
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you find the flag in this disk image?"_

---

### 🔍 Étape 1 : Décompression de l'image disque

Après avoir téléchargé l'archive compressée `disko-1.dd.gz`, la première étape consiste à la décompresser pour obtenir l'image disque brute au format `.dd` :

```bash
gzip -d disko-1.dd.gz
```

---

### 🛠️ Étape 2 : Inspection du fichier

Afin d'explorer le contenu binaire du fichier extrait, une tentative d'affichage brut du fichier a été effectuée :

```bash
cat disko-1.dd
```

**Observation :**
Le fichier contient des données binaires brutes d'une image disque. L'affichage direct produit des caractères non imprimables, ce qui confirme la nécessité d'extraire les chaînes de texte lisibles.

---

### 🚩 Étape 3 : Extraction du Flag avec `strings`

En suivant l'indice du challenge, j'ai utilisé l'outil `strings` pour filtrer les caractères imprimables et la commande `grep` pour isoler le motif du flag :

```bash
strings disko-1.dd | grep academy
```

**Résultat :**
La commande extrait la chaîne de caractères contenant le flag recherché.

**Flag :** `academy{...}` _(à remplacer par ton flag)_

---

### 💡 Key Takeaways / Notions retenues

- L'outil **`strings`** permet d'extraire toutes les chaînes de texte imprimables d'un fichier binaire ou d'une image disque brute (`.dd`).
- Combiner `strings` avec `grep` est une méthode rapide et efficace en Forensics pour retrouver un flag sans avoir à monter l'image disque.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** DISKO 1
- **Author:** Darkraicg492
- **Category:** Forensics
- **Difficulty:** Easy

---

### 📝 Description

> _"Can you find the flag in this disk image?"_

---

### 🔍 Step 1: Decompressing the Disk Image

After downloading the compressed archive `disko-1.dd.gz`, the first step is to decompress it to retrieve the raw `.dd` disk image:

```bash
gzip -d disko-1.dd.gz
```

---

### 🛠️ Step 2: File Inspection

To inspect the extracted binary file, a quick raw inspection was conducted:

```bash
cat disko-1.dd
```

**Observation:**
The file contains raw binary disk data. Displaying it directly outputs unprintable characters, confirming the need to extract human-readable text strings.

---

### 🚩 Step 3: Flag Extraction using `strings`

Following the challenge hint, I used the `strings` utility to filter out printable characters and piped the output into `grep` to locate the flag pattern:

```bash
strings disko-1.dd | grep academy
```

**Result:**
The command successfully isolates and displays the target flag.

**Flag:** `academy{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- The **`strings`** utility extracts readable ASCII/Unicode text strings from binary files or raw disk images (`.dd`).
- Pairing `strings` with `grep` is a fast forensics technique to extract flags without needing to mount the full disk image.
