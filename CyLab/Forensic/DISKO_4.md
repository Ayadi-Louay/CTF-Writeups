# Write-Up : DISKO 4

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** DISKO 4
- **Plateforme / Événement :** picoCTF 2026
- **Auteur :** Darkraicg492
- **Catégorie :** Forensics
- **Difficulté :** Medium

---

### 📝 Description

> _"Can you find the flag in this disk image? This time I deleted the file! Let see you get it now! Download the disk image here."_

---

### 🔍 Étape 1 : Décompression et vérifications initiales

Après avoir téléchargé l'archive `disko-4.dd.gz`, je l'ai décompressée avec `gzip` :

```bash
gzip -d disko-4.dd.gz
```

Comme pour les étapes précédentes, j'ai d'abord tenté les commandes de recherche standard :

```bash
strings disko-4.dd | grep academy
fdisk -lu disko-4.dd
```

**Observation :**
Aucune chaîne correspondant au flag n'apparaît avec `strings`, et `fdisk` ne renvoie pas de table de partition standard directement exploitable.

---

### 🛠️ Étape 2 : Extraction du fichier supprimé avec `binwalk`

En analysant l'indice du challenge (_"How would you look for deleted files?"_), l'objectif est d'extraire des fichiers cachés ou supprimés du système de fichiers.

J'ai exécuté l'outil **`binwalk`** avec l'option d'extraction automatique (`-e`) :

```bash
binwalk -e disko-4.dd
```

**Résultat :**
`binwalk` analyse la structure binaire et réussit à restaurer/extraire les fichiers encapsulés dans le dossier `_disko-4.dd.extracted/`.

---

### 🚩 Étape 3 : Récupération du Flag

1. Accès au dossier des fichiers extraits :
   ```bash
   cd _disko-4.dd.extracted/
   ```
2. Un fichier nommé **`dont-delete`** a été récupéré.
3. Affichage du contenu du fichier :
   ```bash
   cat dont-delete
   ```

**Flag :** `academy{...}` _(à remplacer par ton flag)_

---

### 💡 Key Takeaways / Notions retenues

- Lorsqu'un fichier est supprimé sur une image disque, son contenu binaire reste souvent présent dans les secteurs non alloués.
- L'outil **`binwalk -e`** permet de réaliser du _file carving_ efficace pour récupérer des fichiers supprimés ou masqués sans avoir besoin d'outils complexes de reconstitution de système de fichiers.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** DISKO 4
- **Platform / Event:** picoCTF 2026
- **Author:** Darkraicg492
- **Category:** Forensics
- **Difficulty:** Medium

---

### 📝 Description

> _"Can you find the flag in this disk image? This time I deleted the file! Let see you get it now! Download the disk image here."_

---

### 🔍 Step 1: Decompression & Initial Checks

After downloading the compressed archive `disko-4.dd.gz`, I decompressed it using `gzip`:

```bash
gzip -d disko-4.dd.gz
```

I first performed standard forensic reconnaissance:

```bash
strings disko-4.dd | grep academy
fdisk -lu disko-4.dd
```

**Observation:**
No flags were found in plain printable text, and `fdisk` provided no straightforward partition layout.

---

### 🛠️ Step 2: Carving Deleted Files with `binwalk`

Referencing the challenge hint (_"How would you look for deleted files?"_), the challenge requires extracting files that were removed from the file system.

I executed **`binwalk`** with the automated extraction flag (`-e`):

```bash
binwalk -e disko-4.dd
```

**Result:**
`binwalk` scanned the disk dump's binary structure and extracted the embedded file remnants into the `_disko-4.dd.extracted/` directory.

---

### 🚩 Step 3: Flag Retrieval

1. Navigate to the extracted output folder:
   ```bash
   cd _disko-4.dd.extracted/
   ```
2. Located the recovered file named **`dont-delete`**.
3. Display its contents:
   ```bash
   cat dont-delete
   ```

**Flag:** `academy{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- Deleting a file from a disk image often leaves its raw data intact in unallocated space.
- **`binwalk -e`** is an effective file carving tool for recovering deleted or hidden files directly from raw binary disk images.
