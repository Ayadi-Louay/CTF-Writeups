# Write-Up : ASCII Numbers

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** ASCII Numbers[cite: 18]
- **Catégorie :** General Skills[cite: 18]
- **Difficulté :** Easy[cite: 18]

---

### 📝 Description

> _"Convert the following string of ASCII numbers into a readable string: 0x61 0x63 0x61 0x64 0x65 0x6d 0x79 0x7b 0x34 0x35 0x63 0x31 0x31 0x5f 0x6e 0x30 0x5f 0x71 0x75 0x33 0x35 0x37 0x31 0x30 0x6e 0x35 0x5f 0x31 0x6c 0x6c 0x5f 0x74 0x33 0x31 0x31 0x5f 0x79 0x33 0x5f 0x6e 0x30 0x5f 0x6c 0x31 0x33 0x35 0x5f 0x65 0x39 0x36 0x63 0x38 0x63 0x61 0x38 0x7d"_[cite: 18]

---

### 🔍 Étape 1 : Analyse des données

Le challenge nous fournit une longue séquence de nombres commençant tous par `0x`[cite: 18]. Le préfixe `0x` indique que ces valeurs sont écrites en système **hexadécimal** (base 16). Le titre du challenge suggère que ces valeurs hexadécimales correspondent à des caractères selon la table ASCII[cite: 18].

---

### 🛠️ Étape 2 : Décodage avec CyberChef

Comme vous l'avez mentionné dans votre démarche et comme le suggèrent les indices du challenge, l'outil idéal pour cela est **CyberChef**[cite: 18]. 
En utilisant la fonction "From Hex" sur CyberChef (recommandée par le deuxième indice[cite: 18]), l'outil prend chaque bloc hexadécimal et le traduit en son caractère ASCII lisible correspondant (par exemple, `0x61` devient `a`, `0x63` devient `c`, etc.).

---

### 🚩 Étape 3 : Obtention du Flag

Une fois la chaîne décodée, le texte en clair apparaît directement sous la forme du flag complet.

**Flag :** `academy{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_e96c8ca8}`

---

### 💡 Key Takeaways / Notions retenues

- **Encodage ASCII et Hexadécimal :** Chaque caractère que nous lisons sur un écran (lettres, chiffres, symboles) possède une valeur numérique correspondante dans la table ASCII. Cette valeur est très souvent représentée en format hexadécimal (indiqué par le préfixe `0x`) dans les défis de type CTF.
- **Utilisation des outils d'encodage :** Des plateformes comme CyberChef sont des "couteaux suisses" indispensables pour la cybersécurité, permettant d'enchaîner rapidement des opérations de décodage (comme passer de l'Hexadécimal au texte brut).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** ASCII Numbers[cite: 18]
- **Category:** General Skills[cite: 18]
- **Difficulty:** Easy[cite: 18]

---

### 📝 Description

> _"Convert the following string of ASCII numbers into a readable string: 0x61 0x63 0x61 0x64 0x65 0x6d 0x79 0x7b 0x34 0x35 0x63 0x31 0x31 0x5f 0x6e 0x30 0x5f 0x71 0x75 0x33 0x35 0x37 0x31 0x30 0x6e 0x35 0x5f 0x31 0x6c 0x6c 0x5f 0x74 0x33 0x31 0x31 0x5f 0x79 0x33 0x5f 0x6e 0x30 0x5f 0x6c 0x31 0x33 0x35 0x5f 0x65 0x39 0x36 0x63 0x38 0x63 0x61 0x38 0x7d"_[cite: 18]

---

### 🔍 Step 1: Analyzing the Data

The challenge provides a long sequence of numbers that all begin with `0x`[cite: 18]. The `0x` prefix is standard notation indicating that the numbers are in **hexadecimal** (base 16) format. The challenge title implies these hex values map directly to standard ASCII characters[cite: 18].

---

### 🛠️ Step 2: Decoding with CyberChef

As you noted in your approach, and as the challenge hints suggest, **CyberChef** is the perfect tool for this job[cite: 18].
By pasting the string into CyberChef and applying the "From Hex" recipe (which is explicitly recommended in hint 2[cite: 18]), the application translates each hex byte into its readable ASCII equivalent (for instance, `0x61` is translated to `a`, `0x63` to `c`, and so on).

---

### 🚩 Step 3: Flag Retrieval

Upon decoding the hexadecimal sequence, the plaintext directly reveals the complete flag.

**Flag:** `academy{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_e96c8ca8}`

---

### 💡 Key Takeaways

- **ASCII & Hexadecimal Encoding:** Every readable character (letters, numbers, symbols) has a corresponding numerical value in the ASCII table. In CTFs, these values are frequently represented in hexadecimal format, identifiable by the `0x` prefix.
- **Decoding Tools:** Platforms like CyberChef are essential "Swiss Army knives" in cybersecurity, allowing you to rapidly perform data translation operations (such as Hex to plaintext).