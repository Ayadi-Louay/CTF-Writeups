# Write-Up : endianness

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** endianness
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Nana Ama Atombo-Sackey
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Know of little and big endian?"_

---

### 🔍 Étape 1 : Connexion et conversion en Hexadécimal

On commence par se connecter au serveur du challenge à l'aide de la commande fournie : `nc chatelaine.cylabacademy.net 31781`. Le programme nous accueille et nous donne un mot aléatoire (dans ce cas, `jyxrt`) dont il faut trouver les représentations en _Little Endian_ et _Big Endian_.

En suivant le premier indice du challenge, on utilise une table ASCII (ou un outil comme CyberChef) pour convertir chaque lettre du mot en sa valeur hexadécimale :

- j -> `6a`
- y -> `79`
- x -> `78`
- r -> `72`
- t -> `74`

La chaîne hexadécimale brute est donc : `6a 79 78 72 74`.

---

### 🚩 Étape 2 : Application de l'Endianness et obtention du Flag

Il faut maintenant formater cette chaîne selon les deux architectures de mémoire demandées par le programme :

- **Little Endian :** L'octet le moins significatif est stocké en premier. Il faut donc inverser l'ordre des octets (en gardant les paires intactes). La chaîne devient `747278796a`.
- **Big Endian :** L'octet le plus significatif est stocké en premier, ce qui correspond à l'ordre de lecture naturel (de gauche à droite). La chaîne reste `6a79787274`.

En soumettant correctement ces deux chaînes (sans espaces) au programme, le serveur valide les réponses et nous renvoie le flag.

**Flag :** `academy{3ndi4n_sw4p_su33ess_66f9bdaa}`

---

### 💡 Key Takeaways / Notions retenues

- **Endianness :** Il s'agit de l'ordre dans lequel les octets composant un mot de données sont stockés en mémoire d'ordinateur.
- **Big Endian vs Little Endian :** Le format _Big Endian_ stocke les données comme on les lit de gauche à droite, tandis que le format _Little Endian_ commence par la fin (l'octet de poids faible en premier), ce qui est typique des processeurs d'architecture x86.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** endianness
- **Platform / Event:** picoCTF 2024
- **Author:** Nana Ama Atombo-Sackey
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> _"Know of little and big endian?"_

---

### 🔍 Step 1: Connection & Hexadecimal Conversion

We start by connecting to the challenge server using the provided command: `nc chatelaine.cylabacademy.net 31781`. The program greets us and provides a random word (in this instance, `jyxrt`) for which we need to find both the Little Endian and Big Endian representations.

Following the first hint, we check an ASCII table (or use a tool like CyberChef) to find the hexadecimal representation of each character:

- j -> `6a`
- y -> `79`
- x -> `78`
- r -> `72`
- t -> `74`

The raw hexadecimal string is: `6a 79 78 72 74`.

---

### 🚩 Step 2: Applying Endianness & Flag Retrieval

Next, we must format this hex string according to the two memory architectures requested by the prompt:

- **Little Endian:** The least significant byte is stored first. This means we must reverse the order of the bytes (keeping the hex pairs intact). The string becomes `747278796a`.
- **Big Endian:** The most significant byte is stored first, meaning it reads in the normal left-to-right sequential order. The string remains `6a79787274`.

By inputting these two strings correctly (without spaces) into the terminal, the server validates the conversions and prints out the flag.

**Flag:** `academy{3ndi4n_sw4p_su33ess_66f9bdaa}`

---

### 💡 Key Takeaways

- **Endianness:** This refers to the sequential order in which bytes are arranged into larger numerical values when stored in computer memory.
- **Big Endian vs Little Endian:** _Big Endian_ stores data sequentially just as we read it, whereas _Little Endian_ stores the least significant byte first (reversing the byte order), which is the standard behavior for x86 architecture processors.
