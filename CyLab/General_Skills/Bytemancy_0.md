# Write-Up : bytemancy 0

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** bytemancy 0
- **Plateforme / Événement :** picoCTF 2026
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you conjure the right bytes? The program's source code can be downloaded here. Connect to the program with netcat: nc xebec.cylabacademy.net 33427"_

---

### 🔍 Étape 1 : Connexion au service distant

On se connecte au serveur interactif en utilisant l'outil Netcat :

```bash
nc xebec.cylabacademy.net 33427
```

**Message du serveur :**

```text
Send me ASCII DECIMAL 101, 101, 101, side-by-side, no space.
```

---

### 🛠️ Étape 2 : Conversion ASCII et envoi

Le serveur demande d'envoyer trois fois la valeur ASCII décimale `101` côte à côte sans espace.

1. Dans la table d'encodage ASCII, la valeur décimale **`101`** correspond à la lettre minuscule **`e`**.
2. On saisit donc la chaîne de caractères **`eee`** en réponse au prompt.

_(Alternative en une seule ligne de commande)_ :

```bash
echo "eee" | nc xebec.cylabacademy.net 33427
```

---

### 🚩 Étape 3 : Obtention du Flag

Dès la réception des octets attendus, le serveur valide la réponse et retourne le flag.

**Flag :** `academy{pr1n74813_ch4r5_b44ec13d}`

---

### 💡 Key Takeaways / Notions retenues

- Chaque caractère imprimable possède une représentation numérique unique dans la table **ASCII** (ex: `101` = `'e'`).
- Automatiser l'envoi de réponses via des _one-liners_ (ex: `echo "data" | nc <host> <port>`) facilite la résolution rapide des défis réseaux interactifs.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** bytemancy 0
- **Platform / Event:** picoCTF 2026
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> _"Can you conjure the right bytes? The program's source code can be downloaded here. Connect to the program with netcat: nc xebec.cylabacademy.net 33427"_

---

### 🔍 Step 1: Service Connection

We connect to the interactive challenge instance using Netcat:

```bash
nc xebec.cylabacademy.net 33427
```

**Server Output:**

```text
Send me ASCII DECIMAL 101, 101, 101, side-by-side, no space.
```

---

### 🛠️ Step 2: ASCII Conversion & Input

The service prompts for three consecutive ASCII decimal `101` characters placed side-by-side without spaces.

1. Referring to the ASCII table, the decimal value **`101`** maps to the lowercase character **`e`**.
2. We submit the string **`eee`** to the server prompt.

_(Automated one-liner alternative)_:

```bash
echo "eee" | nc xebec.cylabacademy.net 33427
```

---

### 🚩 Step 3: Flag Retrieval

Upon receiving the correct byte sequence, the program validates the payload and returns the flag.

**Flag:** `academy{pr1n74813_ch4r5_b44ec13d}`

---

### 💡 Key Takeaways

- Printable characters are encoded as numerical values in the **ASCII table** (e.g., `101` = `'e'`).
- Piping stdout directly into Netcat (`echo ... | nc`) provides a clean one-liner method for solving interactive socket challenges.
