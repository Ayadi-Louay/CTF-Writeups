# Write-Up : Transformation

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Transformation[cite: 16]
- **Plateforme / Événement :** picoCTF 2021[cite: 16]
- **Auteur :** madStacks[cite: 16]
- **Catégorie :** Reverse Engineering[cite: 16]
- **Difficulté :** Easy[cite: 16]

---

### 📝 Description

> _"I wonder what this really is... enc"_[cite: 16]

---

### 🔍 Étape 1 : Analyse du mécanisme d'encodage

On télécharge le fichier `enc` qui contient une chaîne de caractères Unicode apparue sous forme d'idéogrammes : `慣慤敭祻ㄶ形楴獟楮獴㌴摟潦弸強㤰扡㌷敽`[cite: 16].

La description du défi fournit l'expression Python d'une ligne ayant servi à générer ce fichier[cite: 16] :

```python
''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])
```

**Explication du chiffrement :**

- Le script prend les caractères du flag deux par deux.
- Le premier caractère de 8 bits est décalé de 8 bits vers la gauche (`<< 8`).
- Le second caractère de 8 bits y est ajouté (`+ ord(flag[i + 1])`).
- La valeur de 16 bits qui en résulte est reconvertie en un unique caractère Unicode 16 bits (`chr(...)`).

---

### 🛠️ Étape 2 : Écriture du script de déchiffrement

Pour inverser cette transformation, on doit extraire les deux octets de 8 bits contenus dans chaque caractère de 16 bits :

1. **Premier caractère (MSB) :** On décale la valeur numérique du caractère de 8 bits vers la droite (`value >> 8`).
2. **Second caractère (LSB) :** On applique un masque binaire `0xFF` (`value & 0xFF`) pour ne conserver que les 8 bits de poids faible.

On exécute le script Python suivant :

```python
def reverse_operation(combined_char):
    combined_value = ord(combined_char)
    # Extraction du premier caractère (décalé de 8 bits vers la droite)
    first_char = chr(combined_value >> 8)
    # Extraction du second caractère (masque binaire 8 bits)
    second_char = chr(combined_value & 0xFF)
    return first_char, second_char

enc_flag = '慣慤敭祻ㄶ形楴獟楮獴㌴摟潦弸強㤰扡㌷敽'

flag = ''
for combined_char in enc_flag:
    first_char, second_char = reverse_operation(combined_char)
    flag += first_char + second_char

print(flag)
```

---

### 🚩 Étape 3 : Obtention du Flag

L'exécution du script décode la totalité des caractères Unicode 16 bits et restitue la chaîne ASCII originale.

**Flag :** `academy{16_bits_inst34d_of_8_790ba37e}`

---

### 💡 Key Takeaways / Notions retenues

- L'utilisation des opérateurs bit à bit en Python (**`<<`**, **`>>`**, **`&`**) permet de manipuler directement la représentation binaire des données.
- Combiner deux caractères ASCII 8 bits dans un entier 16 bits pour créer un caractère Unicode est une technique classique d'empaquetage de données (_byte packing_).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Transformation[cite: 16]
- **Platform / Event:** picoCTF 2021[cite: 16]
- **Author:** madStacks[cite: 16]
- **Category:** Reverse Engineering[cite: 16]
- **Difficulty:** Easy[cite: 16]

---

### 📝 Description

> _"I wonder what this really is... enc"_[cite: 16]

---

### 🔍 Step 1: Analyzing the Encryption One-Liner

We download the `enc` file containing a string of 16-bit Unicode characters: `慣慤敭祻ㄶ形楴獟楮獴㌴摟潦弸強㤰扡㌷敽`[cite: 16].

The challenge snippet details how the flag was encrypted using a Python list comprehension[cite: 16]:

```python
''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])
```

**Algorithm Mechanics:**

- The cipher processes the original ASCII string in pairs of adjacent characters.
- The first byte is shifted left by 8 bits (`<< 8`).
- The second byte is added directly (`+ ord(...)`).
- The combined 16-bit integer is converted into a single Unicode character using `chr()`.

---

### 🛠️ Step 2: Writing the Reversal Script

To reverse the operation and reconstruct the original plaintext, we extract both 8-bit characters from each 16-bit combined value:

1. **First character (MSB):** Shift right by 8 bits (`value >> 8`).
2. **Second character (LSB):** Bitwise AND with `0xFF` mask (`value & 0xFF`).

We execute the following Python script:

```python
def reverse_operation(combined_char):
    combined_value = ord(combined_char)
    # Extract the first character (shift right by 8 bits)
    first_char = chr(combined_value >> 8)
    # Extract the second character (bitwise AND with 0xFF)
    second_char = chr(combined_value & 0xFF)
    return first_char, second_char

enc_flag = '慣慤敭祻ㄶ形楴獟楮獴㌴摟潦弸強㤰扡㌷敽'

flag = ''
for combined_char in enc_flag:
    first_char, second_char = reverse_operation(combined_char)
    flag += first_char + second_char

print(flag)
```

---

### 🚩 Step 3: Flag Retrieval

Running the reversal script reconstructs the original ASCII byte stream.

**Flag:** `academy{16_bits_inst34d_of_8_790ba37e}`

---

### 💡 Key Takeaways

- Python bitwise operators (**`<<`**, **`>>`**, **`&`**) are vital for performing bit-level data extraction and reverse engineering.
- Packing pairs of 8-bit ASCII characters into 16-bit UTF-16 values can be undone by bit-shifting and masking operations.
