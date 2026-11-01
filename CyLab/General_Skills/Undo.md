# Write-Up : Undo

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Undo
- **Plateforme / Événement :** picoCTF 2026
- **Auteur :** Yahaya Meddy
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you reverse a series of Linux text transformations to recover the original flag? Start searching for the flag here nc chatelaine.cylabacademy.net 35998"_

---

### 🔍 Étape 1 : Connexion au service interactif

On se connecte au serveur distant en utilisant l'utilitaire Netcat :

```bash
nc chatelaine.cylabacademy.net 35998
```

Un défi interactif s'affiche, demandant d'inverser étape par étape une série de transformations appliquées sur une chaîne de caractères textuelle.

---

### 🛠️ Étape 2 : Résolution des étapes de transformation

1. **Inversion du Base64 (Step 1) :**
   - _Indice :_ "Base64 encoded the string."
   - _Commande :_ `base64 -d`

2. **Inversion du sens de lecture (Step 2) :**
   - _Indice :_ "Reversed the text."
   - _Commande :_ `rev`

3. **Remplacement des tirets par des tirets bas (Step 3) :**
   - _Indice :_ "Replaced underscores with dashes."
   - _Commande :_ `tr - _`

4. **Remplacement des parenthèses par des accolades (Step 4) :**
   - _Indice :_ "Replaced curly braces with parentheses."
   - _Commande :_ `tr () {}`

5. **Décodage ROT13 (Step 5) :**
   - _Indice :_ "Applied ROT13 to letters."
   - _Commande :_ `tr 'a-zA-Z' 'n-za-mN-ZA-M'`

---

### 🚩 Étape 3 : Obtention du Flag

Une fois toutes les transformations inversées dans l'ordre chronologique inverse, le serveur affiche le flag original en clair.

**Flag :** `academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_8064a2ad}`

---

### 💡 Key Takeaways / Notions retenues

- Les utilitaires de traitement de texte Linux standards (`base64`, `rev`, `tr`) permettent de manipuler rapidement des chaînes de caractères en ligne de commande.
- La commande **`tr`** (translate) est très polyvalente pour effectuer des substitutions simples de caractères ou pour déchiffrer des substitutions monoalphabétiques comme le **ROT13**.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Undo
- **Platform / Event:** picoCTF 2026
- **Author:** Yahaya Meddy
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> _"Can you reverse a series of Linux text transformations to recover the original flag? Start searching for the flag here nc chatelaine.cylabacademy.net 35998"_

---

### 🔍 Step 1: Remote Service Connection

We connect to the interactive remote server instance using Netcat:

```bash
nc chatelaine.cylabacademy.net 35998
```

The challenge presents a multi-step interactive shell asking to reverse each text transformation applied to the flag.

---

### 🛠️ Step 2: Reversing Text Transformations

1. **Reversing Base64 Encoding (Step 1):**
   - _Hint:_ "Base64 encoded the string."
   - _Command:_ `base64 -d`

2. **Reversing String Direction (Step 2):**
   - _Hint:_ "Reversed the text."
   - _Command:_ `rev`

3. **Replacing Dashes with Underscores (Step 3):**
   - _Hint:_ "Replaced underscores with dashes."
   - _Command:_ `tr - _`

4. **Replacing Parentheses with Braces (Step 4):**
   - _Hint:_ "Replaced curly braces with parentheses."
   - _Command:_ `tr () {}`

5. **Decoding ROT13 Cipher (Step 5):**
   - _Hint:_ "Applied ROT13 to letters."
   - _Command:_ `tr 'a-zA-Z' 'n-za-mN-ZA-M'`

---

### 🚩 Step 3: Flag Retrieval

After successfully entering the inverse commands step-by-step, the service displays the recovered plaintext flag.

**Flag:** `academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_8064a2ad}`

---

### 💡 Key Takeaways

- Standard Linux text manipulation CLI utilities (`base64`, `rev`, `tr`) allow quick composition of shell pipelines to process strings.
- The **`tr`** (translate) command is essential for single-character substitution and decoding simple ciphers such as **ROT13**.
