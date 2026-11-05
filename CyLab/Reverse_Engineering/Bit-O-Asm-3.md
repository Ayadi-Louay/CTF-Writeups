# Write-Up : Bit-O-Asm-3

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Bit-O-Asm-3
- **Plateforme / Événement :** picoCTF
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Reverse Engineering
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."_

---

### 🔍 Étape 1 : Inspection du code assembleur

On commence par examiner les instructions contenues dans le fichier d'assemblage fourni :

```bash
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret
```

---

### 🛠️ Étape 2 : Analyse des opérations arithmétiques et registres

Suivons le flux d'exécution instruction par instruction pour calculer la valeur finale de `eax` :

1. **Initialisation des variables locales (`<+15>` & `<+22>`) :**
   - L'adresse mémoire `[rbp-0xc]` reçoit la valeur `0x9fe1a`.
   - L'adresse mémoire `[rbp-0x8]` reçoit la valeur `0x4`.

2. **Chargement dans le registre `eax` (`<+29>`) :**
   - La valeur `0x9fe1a` contenue dans `[rbp-0xc]` est copiée dans le registre `eax`.

3. **Multiplication signée (`<+32>`) :**
   - L'instruction `imul` multiplie la valeur de `eax` (`0x9fe1a`) par celle de `[rbp-0x8]` (`0x4`) :
   
   $$0x9fe1a \times 0x4 = 0x27f868$$

4. **Addition (`<+36>`) :**
   - L'instruction `add` ajoute `0x1f5` à la valeur courante de `eax` (`0x27f868`) :
   
   $$0x27f868 + 0x1f5 = 0x27fa5d$$

5. **Stockage et rechargement (`<+41>` & `<+44>`) :**
   - La valeur `0x27fa5d` est sauvegardée sur la pile à l'adresse `[rbp-0x4]`, puis directement rechargée dans `eax`.

---

### 🚩 Étape 3 : Conversion Décimale et Obtention du Flag

Pour former le flag final, on convertit la valeur hexadécimale contenue dans `eax` (`0x27fa5d`) en base décimale :

```python
int("0x27fa5d", 16)
# Résultat : 2619997
```

**Calcul détaillé :**
- $0x9fe1a = 654874$ (décimal)
- $0x4 = 4$ (décimal)
- $0x1f5 = 501$ (décimal)
- $(654874 \times 4) + 501 = 2619496 + 501 = 2619997$

**Flag :** `academy{2619997}`

---

### 💡 Key Takeaways / Notions retenues

- **Instructions arithmétiques x86_64 :** L'instruction `imul` effectue des multiplications entières signées et `add` réalise des additions directement sur les registres.
- **Inefficiences de compilation (Unoptimized Code) :** Le va-et-vient d'écriture puis de relecture entre la mémoire localisée sur la pile (`[rbp-0x4]`) et le registre `eax` illustre du code généré sans optimisations (`-O0`).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Bit-O-Asm-3
- **Platform / Event:** picoCTF
- **Author:** LT 'syreal' Jones
- **Category:** Reverse Engineering
- **Difficulty:** Easy

---

### 📝 Description

> _"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."_

---

### 🔍 Step 1: Inspecting the Assembly Code

We begin by examining the sequence of assembly instructions provided in the target file:

```bash
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret
```

---

### 🛠️ Step 2: Arithmetic Operations & Register Tracing

Let's step through the instructions linearly to evaluate the value ending up in `eax`:

1. **Local Variable Initialization (`<+15>` & `<+22>`):**
   - Memory address `[rbp-0xc]` receives hex value `0x9fe1a`.
   - Memory address `[rbp-0x8]` receives hex value `0x4`.

2. **Loading value to `eax` (`<+29>`):**
   - The value `0x9fe1a` at `[rbp-0xc]` is loaded into register `eax`.

3. **Signed Multiplication (`<+32>`):**
   - The `imul` instruction multiplies `eax` (`0x9fe1a`) by `[rbp-0x8]` (`0x4`):
   
   $$0x9fe1a \times 0x4 = 0x27f868$$

4. **Addition (`<+36>`):**
   - The `add` instruction adds `0x1f5` to the current `eax` value (`0x27f868`):
   
   $$0x27f868 + 0x1f5 = 0x27fa5d$$

5. **Stack Store and Reload (`<+41>` & `<+44>`):**
   - The computed value `0x27fa5d` is temporarily written to `[rbp-0x4]` and immediately restored into `eax`.

---

### 🚩 Step 3: Hexadecimal to Decimal Conversion & Flag Retrieval

We convert the final value in register `eax` (`0x27fa5d`) into decimal base format:

```python
int("0x27fa5d", 16)
# Output: 2619997
```

**Step-by-step arithmetic check:**
- $0x9fe1a = 654874$ (decimal)
- $0x4 = 4$ (decimal)
- $0x1f5 = 501$ (decimal)
- $(654874 \times 4) + 501 = 2619496 + 501 = 2619997$

**Flag:** `academy{2619997}`

---

### 💡 Key Takeaways

- **x86_64 Arithmetic Instructions:** The `imul` opcode performs signed integer multiplication, while `add` executes basic binary additions.
- **Unoptimized Compiler Output:** Redundant memory store/load sequences (`mov DWORD PTR [rbp-0x4], eax` followed by `mov eax, DWORD PTR [rbp-0x4]`) are typical indicators of code compiled without optimization flags (`-O0`).