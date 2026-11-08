# Write-Up : StegoRSA

## 🇫🇷 Version Française

### 📋 Informations du Challenge

* **Nom du challenge :** StegoRSA

* **Plateforme / Événement :** picoCTF 2026

* **Auteur :** Yahaya Meddy

* **Catégorie :** Cryptography / Steganography

* **Difficulté :** Easy

### 📝 Description

> *"A message has been encrypted using RSA. The public key is gone... but someone might have been careless with the private key. Can you recover it and decrypt the message? Download the flag and image."*

### 🔍 Étape 1 : Inspection des métadonnées Exif de l'image

On commence par analyser l'image fournie `image.jpg` avec l'outil `exiftool` pour rechercher des métadonnées cachées :

```bash
exiftool image.jpg
```

**Observation :**
Le champ `Comment` des métadonnées contient une longue chaîne hexadécimale débutant par `2d2d2d2d2d424547494e2050524956415445204b4559...`.

### 🛠️ Étape 2 : Extraction et reconstruction de la clé privée RSA

1. **Sauvegarde de la chaîne Hex :**
   On extrait l'intégralité du contenu Hex du champ `Comment` et on le place dans un fichier texte `private_key.txt`.

2. **Conversion Hex vers PEM :**
   On convertit cette représentation hexadécimale en texte brut (qui révèle une clé privée au format PEM `-----BEGIN PRIVATE KEY-----`) à l'aide de `xxd` :

```bash
xxd -r -p private_key.txt rsa-key.pem
```

### 🚩 Étape 3 : Déchiffrement RSA et obtention du Flag

Avec la clé privée `rsa-key.pem` reconstruite, on déchiffre le fichier `flag.enc` à l'aide de l'outil `openssl pkeyutl` :

```bash
openssl pkeyutl -decrypt -inkey rsa-key.pm -in flag.enc -out message_dechiffre.txt
```

On affiche le résultat du message déchiffré :

```bash
cat message_dechiffre.txt
```

**Flag :** `academy{rs4_k3y_1n_1mg_9db27b2c}`

### 💡 Key Takeaways / Notions retenues

* **Stéganographie dans les métadonnées (EXIF) :** Les métadonnées d'images (comme le champ `Comment` ou `UserComment`) sont des endroits classiques utilisés pour cacher des informations ou des clés d'accès.

* **Reconstruction de clés PEM :** Les clés privées RSA stockées en hexadécimal peuvent être directement converties en binaire/ASCII à l'aide de `xxd -r -p`.

* **Déchiffrement RSA via OpenSSL :** La commande `openssl pkeyutl -decrypt` permet de déchiffrer rapidement un contenu chiffré en RSA asymétrique lorsqu'on possède la clé privée correspondante.

## 🇬🇧 English Version

### 📋 Challenge Info

* **Challenge Name:** StegoRSA

* **Platform / Event:** picoCTF 2026

* **Author:** Yahaya Meddy

* **Category:** Cryptography / Steganography

* **Difficulty:** Easy

### 📝 Description

> *"A message has been encrypted using RSA. The public key is gone... but someone might have been careless with the private key. Can you recover it and decrypt the message? Download the flag and image."*

### 🔍 Step 1: Inspecting EXIF Metadata

We start by analyzing the provided image file `image.jpg` using the `exiftool` utility to search for hidden metadata:

```bash
exiftool image.jpg
```

**Observation:**
The `Comment` metadata field contains a long hex-encoded string starting with `2d2d2d2d2d424547494e2050524956415445204b4559...`.

### 🛠️ Step 2: RSA Private Key Extraction & Reconstruction

1. **Saving the Hex String:**
   We copy the raw hex string from the `Comment` tag into a file named `private_key.txt`.

2. **Hex to PEM Decoding:**
   We decode the raw hex representation into printable PEM format (`-----BEGIN PRIVATE KEY-----`) using `xxd`:

```bash
xxd -r -p private_key.txt rsa-key.pem
```

### 🚩 Step 3: RSA Decryption & Flag Retrieval

Using the recovered RSA private key `rsa-key.pem`, we decrypt the encrypted payload `flag.enc` using `openssl pkeyutl`:

```bash
openssl pkeyutl -decrypt -inkey rsa-key.pm -in flag.enc -out message_dechiffre.txt
```

We inspect the decrypted output file:

```bash
cat message_dechiffre.txt
```

**Flag:** `academy{rs4_k3y_1n_1mg_9db27b2c}`

### 💡 Key Takeaways

* **Metadata Steganography (EXIF):** File headers and EXIF metadata tags (such as `Comment`) are common locations for hiding sensitive payload data or cryptographic keys.

* **PEM Key Restoration:** Hexadecimal string dumps of RSA keys can be quickly converted back into valid PEM files using `xxd -r -p`.

* **OpenSSL Asymmetric Decryption:** The `openssl pkeyutl -decrypt` utility provides a straightforward method to perform asymmetric RSA decryption given a valid private key file.