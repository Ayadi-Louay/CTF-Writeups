# Write-Up : Piece by Piece

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Piece by Piece[cite: 15]
- **Plateforme / Événement :** picoCTF 2026[cite: 15]
- **Auteur :** Yahaya Meddy[cite: 15]
- **Catégorie :** General Skills[cite: 15]
- **Difficulté :** Easy[cite: 15]

---

### 📝 Description

> _"After logging in, you will find multiple file parts in your home directory. These parts need to be combined and extracted to reveal the flag. SSH to chatelaine.cylabacademy.net:41892 and login as ctf-player with password d137d16e."_[cite: 15]

---

### 🔍 Étape 1 : Connexion SSH et exploration du répertoire

On se connecte au serveur distant en utilisant SSH avec les identifiants fournis[cite: 15] :

```bash
ssh -p 41892 ctf-player@chatelaine.cylabacademy.net
```

_(Mot de passe : `d137d16e`)_[cite: 15]

Une fois connecté, on liste le contenu du répertoire utilisateur :

```bash
ls
```

**Observation :**
On découvre plusieurs fichiers représentant les segments d'une archive scindée : `part_aa`, `part_ab`, `part_ac`, `part_ad`, `part_ae`, ainsi qu'un fichier `instructions.txt`.

---

### 🛠️ Étape 2 : Reconstitution de l'archive ZIP

Pour réassembler les morceaux fractionnés en une seule archive ZIP valide, on utilise la commande `cat` couplée au caractère joker (`*`) pour fusionner les fichiers dans l'ordre alphabétique :

```bash
cat part_a* >> part.zip
```

On vérifie la création de l'archive `part.zip` dans le dossier courant :

```bash
ls
```

---

### 🚩 Étape 3 : Extraction et décompresseion du Flag

On décompresse l'archive reconstituée à l'aide de la commande `unzip` :

```bash
unzip part.zip
```

L'extraction génère le fichier `flag.txt`. On affiche ensuite son contenu directement dans le terminal :

```bash
cat flag.txt
```

**Flag :** `academy{z1p_and_spl1t_f1l3s_4r3_fun_6af185ac}`

---

### 💡 Key Takeaways / Notions retenues

- La commande **`cat`** (concaténation) permet de fusionner plusieurs segments de fichiers (générés par exemple avec `split`) pour reformer le fichier original.
- L'utilisation du joker shell `part_a*` traite les fichiers par ordre alphabétique (`part_aa`, `part_ab`, etc.), ce qui garantit le bon séquençage des données lors de la fusion.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Piece by Piece[cite: 15]
- **Platform / Event:** picoCTF 2026[cite: 15]
- **Author:** Yahaya Meddy[cite: 15]
- **Category:** General Skills[cite: 15]
- **Difficulty:** Easy[cite: 15]

---

### 📝 Description

> _"After logging in, you will find multiple file parts in your home directory. These parts need to be combined and extracted to reveal the flag. SSH to chatelaine.cylabacademy.net:41892 and login as ctf-player with password d137d16e."_[cite: 15]

---

### 🔍 Step 1: SSH Connection & Directory Exploration

We log in to the remote server via SSH using the provided credentials[cite: 15]:

```bash
ssh -p 41892 ctf-player@chatelaine.cylabacademy.net
```

_(Password: `d137d16e`)_[cite: 15]

After logging in, we inspect the directory contents:

```bash
ls
```

**Observation:**
We find several file parts corresponding to a split archive: `part_aa`, `part_ab`, `part_ac`, `part_ad`, `part_ae`, alongside `instructions.txt`.

---

### 🛠️ Step 2: Reassembling the Split ZIP Archive

To combine all split file chunks back into a single valid ZIP archive, we concatenate them using `cat` with the wildcard `part_a*`:

```bash
cat part_a* >> part.zip
```

We verify the newly synthesized `part.zip` file:

```bash
ls
```

---

### 🚩 Step 3: Archive Extraction & Flag Retrieval

We extract the reassembled archive using the `unzip` utility:

```bash
unzip part.zip
```

The operation extracts `flag.txt`. We display its content directly to the terminal:

```bash
cat flag.txt
```

**Flag:** `academy{z1p_and_spl1t_f1l3s_4r3_fun_6af185ac}`

---

### 💡 Key Takeaways

- The **`cat`** utility can concatenate split file fragments (commonly created by tools like `split`) back into their original contiguous file structure.
- Shell expansion (`part_a*`) processes filenames in lexicographical sequence, ensuring proper alignment during the reassembly phase.
