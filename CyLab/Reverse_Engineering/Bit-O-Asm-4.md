# Write-Up : Bit-O-Asm-4

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Bit-O-Asm-4
- **Plateforme / Événement :** picoCTF
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Reverse Engineering
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."_

---

### 🔍 Étape 1 : Inspection du code assembleur

On ouvre le fichier d'assemblage fourni pour analyser la suite d'instructions x86_64 :

```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret
```

---

### 🛠️ Étape 2 : Analyse du flux d'exécution et des registres

Suivons pas à pas la valeur stockée à l'adresse mémoire `[rbp-0x4]` :

1. **Initialisation (`<+15>`) :**
   La valeur hexadécimale `0x9fe1a` est stockée dans `[rbp-0x4]`.
   
2. **Comparaison (`<+22>`) :**
   L'instruction `cmp` compare `[rbp-0x4]` (`0x9fe1a`) avec la valeur `0x2710`.

3. **Saut conditionnel (`<+29>`) :**
   L'instruction `jle` (*Jump if Less than or Equal*) vérifie si `0x9fe1a <= 0x2710`.
   Comme `0x9fe1a` (654874 en décimal) est strictment supérieur à `0x2710` (10000 en décimal), le saut vers `<main+37>` n'est **pas** effectué.

4. **Soustraction (`<+31>`) :**
   Le programme poursuit son exécution et soustrait `0x65` de la valeur présente dans `[rbp-0x4]` :
   $$0x9fe1a - 0x65 = 0x9fdb5$$

5. **Saut inconditionnel (`<+35>`) :**
   L'instruction `jmp` saute directement à `<main+41>`, en ignorant la branche `add` à `<main+37>`.

6. **Transfert vers `eax` (`<+41>`) :**
   La valeur résultante dans `[rbp-0x4]` (`0x9fdb5`) est copiée dans le registre `eax`.

---

### 🚩 Étape 3 : Conversion Décimale et Obtention du Flag

Pour valider le flag, il faut convertir la valeur hexadécimale de `eax` (`0x9fdb5`) en base décimale :

```python
int("0x9fdb5", 16)
# Résultat : 654773
```

Calcul détaillé :
- $0x9fe1a = 654874$ (décimal)
- $0x65 = 101$ (décimal)
- $654874 - 101 = 654773$

**Flag :** `academy{654773}`

---

### 💡 Key Takeaways / Notions retenues

- **Contrôle de flux en Assembleur :** L'association des instructions `cmp` et des instructions de saut (`jle`, `jmp`) permet de représenter les structures conditionnelles `if / else` du code haut niveau.
- **Dépassement de branches :** Analyser correctement les branchements conditionnels évite de prendre en compte du code mort ou des branches non exécutées (comme le `add` ici).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Bit-O-Asm-4
- **Platform / Event:** picoCTF
- **Author:** LT 'syreal' Jones
- **Category:** Reverse Engineering
- **Difficulty:** Easy

---

### 📝 Description

> _"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."_

---

### 🔍 Step 1: Inspecting the Assembly Code

We open the provided assembly dump to analyze the x86_64 instructions sequence:

```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret
```

---

### 🛠️ Step 2: Execution Flow & Register Analysis

Let's trace the execution step-by-step focusing on the variable at `[rbp-0x4]`:

1. **Initialization (`<+15>`):**
   The hex value `0x9fe1a` is assigned to `[rbp-0x4]`.

2. **Comparison (`<+22>`):**
   The `cmp` instruction compares `[rbp-0x4]` (`0x9fe1a`) with `0x2710`.

3. **Conditional Jump (`<+29>`):**
   The `jle` (*Jump if Less than or Equal*) evaluates if `0x9fe1a <= 0x2710`.
   Since `0x9fe1a` (654874 in decimal) is strictly greater than `0x2710` (10000 in decimal), the jump to `<main+37>` is **not** taken.

4. **Subtraction (`<+31>`):**
   Execution continues linearly and subtracts `0x65` from `[rbp-0x4]`:
   $$0x9fe1a - 0x65 = 0x9fdb5$$

5. **Unconditional Jump (`<+35>`):**
   The `jmp` instruction skips directly to `<main+41>`, bypassing the `add` instruction at `<main+37>`.

6. **Assignment to `eax` (`<+41>`):**
   The final value stored at `[rbp-0x4]` (`0x9fdb5`) is moved into the `eax` register.

---

### 🚩 Step 3: Hexadecimal to Decimal Conversion & Flag Retrieval

To format the final flag, we convert the hexadecimal value inside `eax` (`0x9fdb5`) into decimal representation:

```python
int("0x9fdb5", 16)
# Output: 654773
```

Detailed calculation:
- $0x9fe1a = 654874$ (decimal)
- $0x65 = 101$ (decimal)
- $654874 - 101 = 654773$

**Flag:** `academy{654773}`

---

### 💡 Key Takeaways

- **Control Flow in Assembly:** The combination of `cmp` and jump instructions (`jle`, `jmp`) forms high-level `if / else` conditional blocks.
- **Tracing Branching:** Accurately tracing conditional branches is essential to avoid evaluating dead code segments (such as the skipped `add` operation).