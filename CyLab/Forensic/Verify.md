# Write-Up : Verify

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge
* **Nom du challenge :** Verify
* **Plateforme / Événement :** picoCTF 2024
* **Auteur :** Jeffery John
* **Catégorie :** Forensics
* **Difficulté :** Easy

---

### 📝 Description
> *"People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate."*

---

### 🔍 Étape 1 : Connexion au serveur et exploration initiale
On se connecte au serveur distant via SSH avec les identifiants fournis dans la description du défi :

```bash
ssh -p 12962 ctf-player@xebec.cylabacademy.net
```
*(Mot de passe : `13792798`)*

Une fois connecté, on liste le contenu du répertoire courant :

```bash
ls
```

**Observation :**
On découvre la présence de trois éléments :
* `checksum.txt` : contient l'empreinte SHA-256 officielle du vrai flag.
* `decrypt.sh` : un script Bash servant à déchiffrer le fichier valide.
* `files/` : un dossier contenant plusieurs fichiers (vrais et faux flags).

---

### 🛠️ Étape 2 : Identification du fichier valide via SHA-256
En s'appuyant sur les indices fournis, on calcule le hash SHA-256 de tous les fichiers du dossier `files/` et on filtre le résultat avec `grep` en utilisant le checksum donné (`bf7701262e3fce45531b13d9866fb0913847a669823064aec1f60be7c2591ba8`) :

```bash
sha256sum files/* | grep "bf7701262e3fce45531b13d9866fb0913847a669823064aec1f60be7c2591ba8"
```

**Résultat :**
La commande permet de repérer précisément le seul fichier dont le hash correspond à l'empreinte authentique (ex: `files/816156e1`).

---

### 🚩 Étape 3 : Déchiffrement et obtention du Flag
Une fois le bon fichier identifié, on exécute le script de déchiffrement `./decrypt.sh` en lui passant le chemin du fichier valide en paramètre :

```bash
./decrypt.sh files/<fichier_valide>
```

**Résultat :**
Le script valide la somme de contrôle et affiche le flag en clair sur le terminal.

**Flag :** `picoCTF{...}` *(à remplacer par le flag obtenu)*

---

### 💡 Key Takeaways / Notions retenues
* Les sommes de contrôle (comme **SHA-256**) permettent de vérifier l'intégrité et l'authenticité d'un fichier.
* Combiner **`sha256sum`** et **`grep`** permet d'isoler rapidement un fichier spécifique parmi un grand volume de fichiers suspects.

---
---

## 🇬🇧 English Version

### 📋 Challenge Info
* **Challenge Name:** Verify
* **Platform / Event:** picoCTF 2024
* **Author:** Jeffery John
* **Category:** Forensics
* **Difficulty:** Easy

---

### 📝 Description
> *"People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate."*

---

### 🔍 Step 1: Remote Server Connection & File Exploration
We connect to the remote server via SSH using the credentials provided in the challenge description:

```bash
ssh -p 12962 ctf-player@xebec.cylabacademy.net
```
*(Password: `13792798`)*

Once connected, we list the contents of the current working directory:

```bash
ls
```

**Observation:**
We notice three main items:
* `checksum.txt`: Contains the official SHA-256 hash of the legitimate flag.
* `decrypt.sh`: A Bash script designed to decrypt the valid file.
* `files/`: A directory containing multiple files (fake and genuine flags).

---

### 🛠️ Step 2: Identifying the Genuine File via SHA-256
Following the hints provided, we compute the SHA-256 hashes of all files in the `files/` directory and pipe the output to `grep` using the authentic checksum (`bf7701262e3fce45531b13d9866fb0913847a669823064aec1f60be7c2591ba8`):

```bash
sha256sum files/* | grep "bf7701262e3fce45531b13d9866fb0913847a669823064aec1f60be7c2591ba8"
```

**Result:**
The command isolates the exact file matching the authentic SHA-256 hash (e.g., `files/816156e1`).

---

### 🚩 Step 3: Decrypting the File & Flag Retrieval
With the correct file identified, we run the `./decrypt.sh` script, passing the valid file path as an argument:

```bash
./decrypt.sh files/<valid_file>
```

**Result:**
The script verifies the hash integrity and outputs the plaintext flag to the terminal.

**Flag:** `picoCTF{...}` *(replace with your actual flag)*

---

### 💡 Key Takeaways
* **SHA-256** checksums ensure data integrity and file authenticity.
* Combining **`sha256sum`** with **`grep`** is an efficient way to isolate a specific legitimate file among multiple decoy files.