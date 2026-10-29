# Write-Up : DISKO 2

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** DISKO 2
- **Auteur :** Darkraicg492
- **Catégorie :** Forensics
- **Difficulté :** Medium

---

### 📝 Description

> _"Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!"_

---

### 🔍 Étape 1 : Décompression et premières tentatives

Après avoir téléchargé l'archive `disko-2.dd.gz`, je l'ai décompressée avec `gzip` :

```bash
gzip -d disko-2.dd.gz
```

Une recherche globale avec `strings disko-2.dd | grep academy` retourne un grand nombre de faux flags (rabbit holes), rendant l'analyse directe sur l'ensemble du disque inefficace.

---

### 🛠️ Étape 2 : Analyse de la table des partitions (`fdisk`)

En suivant l'indice du challenge (_"How can you extract/isolate a partition?"_) et la description indiquant que le vrai flag se trouve sur la partition **Linux**, j'ai inspecté la structure du disque :

```bash
fdisk -lu disko-2.dd
```

**Observation :**
La commande affiche la liste des partitions. La partition de type **Linux** commence au secteur `2048` avec une taille de `51200` secteurs.

---

### ✂️ Étape 3 : Extraction de la partition Linux (`dd`)

Afin d'isoler uniquement la partition Linux, j'ai utilisé l'outil `dd` avec les paramètres `skip` (secteur de départ) et `count` (nombre de secteurs à copier) :

```bash
dd if=disko-2.dd of=disko-2.dd1 skip=2048 count=51200
```

---

### 🚩 Étape 4 : Extraction du vrai Flag

Une fois la partition Linux isolée dans le fichier `disko-2.dd1`, l'extraction des chaînes de caractères permet d'obtenir directement le bon flag sans subir les faux flags des autres partitions :

```bash
strings disko-2.dd1 | grep academy
```

**Flag :** `academy{...}` _(à remplacer par ton flag)_

---

### 💡 Key Takeaways / Notions retenues

- Un disque complet (`.dd`) peut contenir plusieurs partitions et de fausses pistes destinées à piéger une recherche globale par `strings`.
- L'outil **`fdisk -lu`** permet de repérer le secteur de départ (`Start`) et la taille des partitions.
- La commande **`dd`** avec le paramètre `skip` permet d'extraire de manière chirurgicale une partition spécifique d'une image disque.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** DISKO 2
- **Author:** Darkraicg492
- **Category:** Forensics
- **Difficulty:** Medium

---

### 📝 Description

> _"Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!"_

---

### 🔍 Step 1: Decompression and Initial Attempt

After downloading `disko-2.dd.gz`, I extracted the archive using `gzip`:

```bash
gzip -d disko-2.dd.gz
```

Running a global search with `strings disko-2.dd | grep academy` returned numerous decoy flags (rabbit holes), making a direct search on the entire raw disk impractical.

---

### 🛠️ Step 2: Partition Analysis (`fdisk`)

Following the challenge hint (_"How can you extract/isolate a partition?"_) and the description highlighting that the true flag is on the **Linux** partition, I examined the partition structure:

```bash
fdisk -lu disko-2.dd
```

**Observation:**
The command reveals the partition table, showing the **Linux** partition starting at sector `2048` with a length of `51200` sectors.

---

### ✂️ Step 3: Extracting the Linux Partition (`dd`)

To isolate the Linux partition, I used `dd` with the `skip` (start offset) and `count` (sector count) parameters:

```bash
dd if=disko-2.dd of=disko-2.dd1 skip=2048 count=51200
```

---

### 🚩 Step 4: True Flag Retrieval

With the Linux partition isolated in `disko-2.dd1`, running `strings` exclusively on this volume filters out all decoys and isolates the correct flag:

```bash
strings disko-2.dd1 | grep academy
```

**Flag:** `academy{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- Full disk dumps (`.dd`) often contain multiple partitions filled with decoy flags to disrupt naive `strings` searches.
- **`fdisk -lu`** provides the sector offset details required to inspect individual disk partitions.
- **`dd`** with the `skip` option allows precise extraction of targeted partitions from raw disk dumps.
