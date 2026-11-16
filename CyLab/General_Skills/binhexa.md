# Write-Up : binhexa

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** binhexa[cite: 17]
- **Plateforme / Événement :** picoCTF 2024[cite: 17]
- **Auteur :** Nana Ama Atombo-Sackey[cite: 17]
- **Catégorie :** General Skills[cite: 17]
- **Difficulté :** Easy[cite: 17]

---

### 📝 Description

> _"How well can you perfom basic binary operations? Start searching for the flag here `nc xebec.cylabacademy.net 10695`"_[cite: 17]

---

### 🔍 Étape 1 : Connexion au serveur

En lançant l'instance, le challenge nous fournit une commande pour nous connecter à un serveur interactif via Netcat : `nc xebec.cylabacademy.net 10695`[cite: 17].
Une fois connecté, le serveur nous accueille dans le "Binary Challenge!" et nous donne deux nombres binaires de base avec lesquels nous allons devoir travailler :

- Nombre Binaire 1 : `10010010`
- Nombre Binaire 2 : `11101100`

---

### 🛠️ Étape 2 : Résolution des opérations binaires

Le défi consiste à répondre à une série de 6 questions en effectuant des opérations mathématiques et logiques sur ces nombres :

1. **Opération 1 (`+`) :** Addition des deux nombres.
   - Résultat binaire : `101111110`
2. **Opération 2 (`*`) :** Multiplication des deux nombres.
   - Résultat binaire : `1000011010011000`
3. **Opération 3 (`>>`) :** Décalage vers la droite (Right shift) du Nombre Binaire 2 par 1 bit.
   - Résultat binaire : `01110110`
4. **Opération 4 (`|`) :** OU logique (Bitwise OR) entre les deux nombres.
   - Résultat binaire : `11111110`
5. **Opération 5 (`&`) :** ET logique (Bitwise AND) entre les deux nombres.
   - Résultat binaire : `10000000`
6. **Opération 6 (`<<`) :** Décalage vers la gauche (Left shift) du Nombre Binaire 1 par 1 bit.
   - Résultat binaire : `100100100`

---

### 🚩 Étape 3 : Conversion finale et obtention du Flag

Après avoir réussi les 6 opérations, le serveur nous demande une dernière tâche : convertir le résultat de la dernière opération (`100100100`) en système hexadécimal.

En convertissant `100100100` (binaire) en hexadécimal, on obtient `124`.
Une fois cette réponse validée, le serveur nous félicite et affiche le flag.

**Flag :** `academy{b1tw^3se_0p3eR@tI0n_su33essFuL_da08c409}`

---

### 💡 Key Takeaways / Notions retenues

- **Opérations bit à bit (Bitwise) :** Les opérations logiques comme le OU (`|`), le ET (`&`) et les décalages de bits (`<<`, `>>`) sont fondamentales en informatique, particulièrement en rétro-ingénierie et en cryptographie.
- **Conversions de bases :** Passer du binaire (base 2) à l'hexadécimal (base 16) est une compétence indispensable. Chaque groupe de 4 bits correspond exactement à un chiffre hexadécimal.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** binhexa[cite: 17]
- **Platform / Event:** picoCTF 2024[cite: 17]
- **Author:** Nana Ama Atombo-Sackey[cite: 17]
- **Category:** General Skills[cite: 17]
- **Difficulty:** Easy[cite: 17]

---

### 📝 Description

> _"How well can you perfom basic binary operations? Start searching for the flag here `nc xebec.cylabacademy.net 10695`"_[cite: 17]

---

### 🔍 Step 1: Connecting to the Server

Upon launching the instance, we are given a Netcat command to connect to the challenge server: `nc xebec.cylabacademy.net 10695`[cite: 17].
Once connected, we are welcomed to the "Binary Challenge!" and provided with two base binary numbers to work with:

- Binary Number 1: `10010010`
- Binary Number 2: `11101100`

---

### 🛠️ Step 2: Solving the Binary Operations

The challenge prompts us to answer a series of 6 questions by performing mathematical and bitwise operations on the provided numbers:

1. **Operation 1 (`+`):** Addition of the two numbers.
   - Binary result: `101111110`
2. **Operation 2 (`*`):** Multiplication of the two numbers.
   - Binary result: `1000011010011000`
3. **Operation 3 (`>>`):** Right shift of Binary Number 2 by 1 bit.
   - Binary result: `01110110`
4. **Operation 4 (`|`):** Bitwise OR on both numbers.
   - Binary result: `11111110`
5. **Operation 5 (`&`):** Bitwise AND on both numbers.
   - Binary result: `10000000`
6. **Operation 6 (`<<`):** Left shift of Binary Number 1 by 1 bit.
   - Binary result: `100100100`

---

### 🚩 Step 3: Final Conversion & Flag

After successfully completing the 6 operations, the server requests one final task: converting the result of the last operation (`100100100`) into hexadecimal format.

Converting `100100100` (binary) to hexadecimal yields `124`.
Submitting this final answer successfully completes the challenge, and the server reveals the flag.

**Flag:** `academy{b1tw^3se_0p3eR@tI0n_su33essFuL_da08c409}`

---

### 💡 Key Takeaways

- **Bitwise Operations:** Understanding logical operations like OR (`|`), AND (`&`), and bit shifting (`<<`, `>>`) is fundamental in computer science, especially in reverse engineering and cryptography.
- **Base Conversions:** Converting between binary (base 2) and hexadecimal (base 16) is a crucial skill. Grouping binary numbers into sets of 4 bits makes translation to hex straightforward.
