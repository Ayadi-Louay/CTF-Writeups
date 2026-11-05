# Write-Up : ASCII FTW

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** ASCII FTW
- **Plateforme / Événement :** picoCTF
- **Auteur :** Abhishek Agarwal
- **Catégorie :** Reverse Engineering
- **Difficulté :** Easy

---

### 📝 Description

> _"This program has constructed the flag using hex ascii values. Identify the flag text by disassembling the program. You can download the file from here."_

---

### 🔍 Étape 1 : Exploration du binaire et désassemblage avec GDB

On commence par vérifier le type de fichier binaire avec la commande `file` :

```bash
file asciiftw
```

**Résultat :** Il s'agit d'un binaire Linux ELF 64 bits dynamique et non dépouillé (_not stripped_).

On exécute ensuite le débogueur GDB pour analyser le programme :

```bash
gdb ./asciiftw
```

Une fois dans GDB, on cherche la liste des fonctions puis on désassemble la fonction principale `main` :

```text
(gdb) info functions
(gdb) disas main
```

---

### 🛠️ Étape 2 : Analyse de la pile et extraction des octets Hex

En examinant le code assembleur décompilé de `main`, on observe une séquence d'instructions `movb` qui stockent successivement des octets hexadécimaux sur la pile (registre `%rbp`) :

```assembly
movb $0x61,-0x30(%rbp)
movb $0x63,-0x2f(%rbp)
movb $0x61,-0x2e(%rbp)
movb $0x64,-0x2d(%rbp)
movb $0x65,-0x2c(%rbp)
movb $0x6d,-0x2b(%rbp)
movb $0x79,-0x2a(%rbp)
movb $0x7b,-0x29(%rbp)
...
```

On extrait l'intégralité des octets hexadécimaux placés en mémoire :
`0x61, 0x63, 0x61, 0x64, 0x65, 0x6d, 0x79, 0x7b, 0x41, 0x53, 0x43, 0x49, 0x49, 0x5f, 0x49, 0x53, 0x5f, 0x45, 0x41, 0x53, 0x59, 0x5f, 0x36, 0x41, 0x37, 0x33, 0x46, 0x43, 0x35, 0x38, 0x7d`

---

### 🚩 Étape 3 : Décodage ASCII et obtention du Flag

On convertit chaque valeur hexadécimale vers son équivalent en caractère ASCII (à l'aide d'un tableau d'encodage ASCII, de CyberChef ou d'une ligne de commande Python) :

```python
bytes.fromhex("61636164656d797b41534349495f49535f454153595f36413733464335387d").decode()
```

**Tableau de correspondance partiel :**

- `0x61 0x63 0x61 0x64 0x65 0x6d 0x79 0x7b` ➔ `academy{`
- `0x41 0x53 0x43 0x49 0x49 0x5f` ➔ `ASCII_`
- `0x49 0x53 0x5f` ➔ `IS_`
- `0x45 0x41 0x53 0x59 0x5f` ➔ `EASY_`
- `0x36 0x41 0x37 0x33 0x46 0x43 0x35 0x38 0x7d` ➔ `6A73FC58}`

**Flag :** `academy{ASCII_IS_EASY_6A73FC58}`

---

### 💡 Key Takeaways / Notions retenues

- En rétro-ingénierie (Reverse Engineering), la reconstruction manuelle de chaînes de caractères sur la pile est une technique courante (_stack strings_) pour masquer du texte aux outils d'analyse statique simples comme `strings`.
- Le désassemblage via GDB ou un décompilateur (Ghidra, IDA Pro) permet de lire les opérations d'écriture en mémoire octet par octet (`movb`) pour reconstruire les secrets cachés.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** ASCII FTW
- **Platform / Event:** picoCTF
- **Author:** Abhishek Agarwal
- **Category:** Reverse Engineering
- **Difficulty:** Easy

---

### 📝 Description

> _"This program has constructed the flag using hex ascii values. Identify the flag text by disassembling the program. You can download the file from here."_

---

### 🔍 Step 1: Binary Exploration & GDB Disassembly

We begin by analyzing the target file properties using the `file` utility:

```bash
file asciiftw
```

**Result:** The target binary is an unstripped 64-bit ELF executable.

We launch GDB to inspect the executable binary structure:

```bash
gdb ./asciiftw
```

Inside GDB, we check defined functions and disassemble the `main` entry point:

```text
(gdb) info functions
(gdb) disas main
```

---

### 🛠️ Step 2: Assembly Inspection & Hex Byte Extraction

Reviewing the disassembled assembly code for `main`, we notice a series of consecutive `movb` instructions pushing individual hex byte values onto the local stack frame (`%rbp`):

```assembly
movb $0x61,-0x30(%rbp)
movb $0x63,-0x2f(%rbp)
movb $0x61,-0x2e(%rbp)
movb $0x64,-0x2d(%rbp)
movb $0x65,-0x2c(%rbp)
movb $0x6d,-0x2b(%rbp)
movb $0x79,-0x2a(%rbp)
movb $0x7b,-0x29(%rbp)
...
```

We collect the complete hex byte array stored in memory:
`0x61, 0x63, 0x61, 0x64, 0x65, 0x6d, 0x79, 0x7b, 0x41, 0x53, 0x43, 0x49, 0x49, 0x5f, 0x49, 0x53, 0x5f, 0x45, 0x41, 0x53, 0x59, 0x5f, 0x36, 0x41, 0x37, 0x33, 0x46, 0x43, 0x35, 0x38, 0x7d`

---

### 🚩 Step 3: ASCII Decoding & Flag Retrieval

We translate each hex byte to its printable ASCII character representation (via an ASCII table, CyberChef, or Python CLI one-liner):

```python
bytes.fromhex("61636164656d797b41534349495f49535f454153595f36413733464335387d").decode()
```

**Byte Breakdown:**

- `0x61 0x63 0x61 0x64 0x65 0x6d 0x79 0x7b` ➔ `academy{`
- `0x41 0x53 0x43 0x49 0x49 0x5f` ➔ `ASCII_`
- `0x49 0x53 0x5f` ➔ `IS_`
- `0x45 0x41 0x53 0x59 0x5f` ➔ `EASY_`
- `0x36 0x41 0x37 0x33 0x46 0x43 0x35 0x38 0x7d` ➔ `6A73FC58}`

**Flag:** `academy{ASCII_IS_EASY_6A73FC58}`

---

### 💡 Key Takeaways

- **Stack Strings** are a common technique in software development and malware to construct strings byte-by-byte at runtime to bypass basic `strings` static extraction.
- Disassembling binary routines using GDB or reverse engineering frameworks (Ghidra, IDA Pro) allows quick identification of raw stack assignments (`movb`) to reconstruct embedded data.