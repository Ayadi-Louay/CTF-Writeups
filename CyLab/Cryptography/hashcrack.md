# Write-Up : hashcrack

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** hashcrack
- **Plateforme / Événement :** picoCTF 2025
- **Auteur :** Nana Ama Atombo-Sackey
- **Catégorie :** Cryptography
- **Difficulté :** Easy

---

### 📝 Description

> _"A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?"_

---

### 🔍 Étape 1 : Identification et cassage du premier hash (MD5)

Le serveur présente successivement trois hashes à craquer pour obtenir le flag. On commence par identifier le premier hash (`482c811da5d5b4bc6d497ffa98491e38`) :

```bash
hash-identifier 482c811da5d5b4bc6d497ffa98491e38
```

**Résultat :**
Le hash est identifié comme du `MD5`.

On utilise ensuite hashcat avec le dictionnaire rockyou.txt pour retrouver le mot de passe en clair (mode -m 0 pour le MD5) :

```bash
hashcat -a 0 -m 0 -o pass.txt -O "482c811da5d5b4bc6d497ffa98491e38" rockyou.txt
cat pass.txt
```

**Mot de passe trouvé :** password123

### 🛠️ Étape 2 : Identification et cassage du deuxième hash (SHA-1)

Le serveur passe au second niveau et fournit un nouveau hash (b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3). On l'identifie :

```bash
hash-identifier b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
```

**Resultat :**
Le hash correspond à du `SHA-1`.

On lance hashcat avec le mode approprié (-m 100 pour SHA-1) :

```bash
hashcat -a 0 -m 100 -o pass.txt -O "b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3" rockyou.txt
cat pass.txt
```

**Mot de passe trouvé :** letmein

### 🚩 Étape 3 : Identification et cassage du troisième hash (SHA-256) & Récupération du Flag

Enfin, le serveur propose un dernier hash `(916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745)`. On identifie son algorithme :

```bash
hash-identifier 916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745
```

**Résultat :**
Le hash est identifié comme du `SHA-256 `.

On exécute hashcat avec le mode -m 1700 (SHA-256) :

```bash
hashcat -a 0 -m 1700 -o pass.txt -O "916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745" rockyou.txt
cat pass.txt
```

**Mot de passe trouvé :** qwerty098

En soumettant cette dernière réponse au serveur, le secret s'affiche :

**Flag :** `academy{UseStr0nG_h@shEs_&PaSswDs!_6bbfe014}`

### 💡 Key Takeaways / Notions retenues

- Les fonctions de hachage faibles (comme MD5 ou SHA-1) sont vulnérables aux attaques par dictionnaire et peuvent être cassées rapidement avec des outils comme `hashcat` et des wordlists standards comme `rockyou.txt`.

- L'utilisation de mots de passe complexes et de hachages robustes (salés et itératifs) est indispensable pour protéger les accès administrateurs.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** hashcrack

- **Platform / Event:** picoCTF 2025

- **Author:** Nana Ama Atombo-Sackey

- **Category:** Cryptography / Steganography

- **Difficulty:** Easy

### 📝 Description

> _"A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?"_

### 🔍 Step 1: Identifying and Cracking the First Hash (MD5)

The server sequentially presents three hashes to crack in order to reveal the flag. We start by identifying the first hash (`482c811da5d5b4bc6d497ffa98491e38`):

```bash
hash-identifier 482c811da5d5b4bc6d497ffa98491e38
```

**Result :**
The hash is identified as `MD5`.

We use hashcat alongside the rockyou.txt wordlist to retrieve the plain-text password (using mode -m 0 for MD5):

```bash
hashcat -a 0 -m 0 -o pass.txt -O "482c811da5d5b4bc6d497ffa98491e38" rockyou.txt
cat pass.txt
```

**Recovered Password:** password123

### 🛠️ Step 2: Identifying and Cracking the Second Hash (SHA-1)

The server proceeds to the second stage and provides a new hash (`b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3`). We identify it:

```bash
hash-identifier b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
```

**Result :** The hash corresponds to SHA-1.

We launch hashcat with the appropriate mode (-m 100 for SHA-1):

```bash
hashcat -a 0 -m 100 -o pass.txt -O "b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3" rockyou.txt
cat pass.txt
```

**Recovered Password:** letmein

### 🚩 Step 3: Identifying and Cracking the Third Hash (SHA-256) & Retrieving the Flag

Finally, the server prompts us with a more robust hash (`916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745`). We determine its algorithm:

```bash
hash-identifier 916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745
```

**Result:** The hash is identified as SHA-256.

We run hashcat using mode -m 1700 (SHA-256):

```bash
hashcat -a 0 -m 1700 -o pass.txt -O "916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745" rockyou.txt
cat pass.txt
```

**Recovered Password:** qwerty098

Upon submitting this last cracked password to the server, the final secret and flag are revealed:

**Flag:** `academy{UseStr0nG_h@shEs_&PaSswDs!_6bbfe014}`

### 💡 Key Takeaways

- Weak hashing algorithms (like MD5 or SHA-1) are highly vulnerable to dictionary attacks and can be cracked almost instantly using tools like `hashcat` and standard wordlists like `rockyou.txt`.

- Ensuring strong passwords paired with secure, salted, and iterative hashing mechanisms is vital for securing administrative accounts.
