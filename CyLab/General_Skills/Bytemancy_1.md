# Write-Up : bytemancy 1

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** bytemancy 1
- **Plateforme / Événement :** picoCTF 2026
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you conjure the right bytes? The program's source code can be downloaded here. Connect to the program with netcat: nc chatelaine.cylabacademy.net 42898"_

---

### 🔍 Étape 1 : Connexion au service distant

On se connecte au serveur distant en utilisant l'utilitaire Netcat :

```bash
nc chatelaine.cylabacademy.net 42898
```

**Message du serveur :**

```text
Send me ASCII DECIMAL 101 1751 times, side-by-side, no space.
```

---

### 🛠️ Étape 2 : Génération de la charge utile en Python

Le serveur demande la répétition de la valeur ASCII décimale `101` (qui correspond au caractère **`e`** ou `\x65` en hexadécimal) à exactement **1751 reprises**.

En s'appuyant sur l'indice du défi (_"No copy-pasta, please - use Python!"_), copier-coller manuellement cette longueur est inefficace. On génère et transmet automatiquement la charge utile en utilisant un _one-liner_ Python réinjecté directement dans Netcat :

```bash
python3 -c 'print("e" * 1751)' | nc chatelaine.cylabacademy.net 42898
```

_(Ou en notation hexadécimale : `python3 -c 'print("\x65" _ 1751)' | nc chatelaine.cylabacademy.net 42898`)\*

---

### 🚩 Étape 3 : Obtention du Flag

Dès que le serveur reçoit le flux de 1751 caractères `e`, il valide la réponse et renvoie le flag.

**Flag :** `academy{h0w_m4ny_e's???_17ac1ce5}`

---

### 💡 Key Takeaways / Notions retenues

- La multiplication de chaînes en Python (`"char" * N`) permet de générer instantanément de longues répétitions de caractères.
- Automatiser l'envoi de données réseau volumineuses avec `python3 -c '...' | nc <host> <port>` évite les erreurs manuelles de saisie et d'encodage.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** bytemancy 1
- **Platform / Event:** picoCTF 2026
- **Author:** LT 'syreal' Jones
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> _"Can you conjure the right bytes? The program's source code can be downloaded here. Connect to the program with netcat: nc chatelaine.cylabacademy.net 42898"_

---

### 🔍 Step 1: Service Connection

We connect to the interactive server using Netcat:

```bash
nc chatelaine.cylabacademy.net 42898
```

**Server Output:**

```text
Send me ASCII DECIMAL 101 1751 times, side-by-side, no space.
```

---

### 🛠️ Step 2: Python Payload Generation

The service asks for ASCII decimal `101` (which maps to the lowercase letter **`e`** or `\x65` in hex) repeated **1751 times**.

Following the challenge hint (_"No copy-pasta, please - use Python!"_), manual entry is impractical. We generate the payload on the fly using a Python one-liner piped straight into Netcat:

```bash
python3 -c 'print("e" * 1751)' | nc chatelaine.cylabacademy.net 42898
```

_(Or via hex representation: `python3 -c 'print("\x65" _ 1751)' | nc chatelaine.cylabacademy.net 42898`)\*

---

### 🚩 Step 3: Flag Retrieval

Upon receiving the 1751-byte stream of `e` characters, the program validates the input payload and prints the flag.

**Flag:** `academy{h0w_m4ny_e's???_17ac1ce5}`

---

### 💡 Key Takeaways

- Python string multiplication (`"char" * N`) provides a quick way to construct repeated byte patterns.
- Piping CLI output (`python3 -c '...' | nc`) streamlines sending dynamically calculated payloads directly into socket connections.
