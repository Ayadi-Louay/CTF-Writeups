# Write-Up : Bit-0-Asm-2

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Bit-0-Asm-2
- **Plateforme / Événement :** picoCTF
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Reverse Engineering
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."_

---

### 🔍 Étape 1 : Téléchargement et inspection du fichier dump

On télécharge le fichier texte contenant le dump d'instructions assembleur x86_64 et on l'ouvre dans un éditeur de texte :

```assembly
<+0>:     endbr64
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    mov    eax,DWORD PTR [rbp-0x4]
<+25>:    pop    rbp
<+26>:    ret
```

### 🛠️ Étape 2 : Analyse des instructions et conversion de la base numérique

En suivant le flux d'exécution sur la pile (stack) :L'instruction <+15> stocke la valeur hexadécimale 0x9fe1a à l'adresse mémoire [rbp-0x4] :

```assembly
mov    DWORD PTR [rbp-0x4],0x9fe1a
```

L'instruction <+22> lit la valeur située à l'adresse [rbp-0x4] et la charge dans le registre eax :

```assembly
mov    eax,DWORD PTR [rbp-0x4]
```

Le registre eax contient donc la valeur hexadécimale 0x9fe1a.On convertit cette valeur hexadécimale vers la base décimale (base 10) :
$$0\text{x}9\text{FE1A} = (9 \times 16^4) + (15 \times 16^3) + (14 \times 16^2) + (1 \times 16^1) + (10 \times 16^0) = 654874$$

### 🚩 Étape 3 : Obtention du Flag

On insère la valeur décimale 654874 au format du flag requis (academy{n}) :

`Flag : academy{654874}`

### 💡 Key Takeaways / Notions retenues

1-Les pointeurs mémoire (DWORD PTR [rbp-0x4]) servent d'emplacements pour stocker des variables locales sur la pile.

2-Suivre le flux de transfert de données entre la mémoire et les registres (mov) permet d'isoler la valeur finale chargée dans eax.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Bit-0-Asm-2
- **Platform / Event:** picoCTF
- **Author:** LT 'syreal' Jones[cite: 9]
- **Category:** Reverse Engineering[cite: 9]
- **Difficulty:** Easy[cite: 9]

### 📝 Description

"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."

### 🔍 Step 1: File Retrieval & Assembly Dump Inspection

We download the provided text file containing the x86_64 assembly code dump and inspect its contents:

```assembly
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    mov    eax,DWORD PTR [rbp-0x4]
<+25>:    pop    rbp
<+26>:    ret
```

### 🛠️ Step 2: Instruction Analysis & Base Conversion

Tracing the data flow through the local stack frame:Instruction <+15> moves the hexadecimal constant 0x9fe1a into memory location [rbp-0x4]:

```assembly
mov    DWORD PTR [rbp-0x4],0x9fe1a
```

Instruction <+22> reads the 32-bit DWORD from [rbp-0x4] and loads it directly into register eax:

```assembly
mov    eax,DWORD PTR [rbp-0x4]
```

Register eax now holds the hexadecimal value 0x9fe1a.We convert this hexadecimal number to decimal base representation:
$$0\text{x}9\text{FE1A} = (9 \times 16^4) + (15 \times 16^3) + (14 \times 16^2) + (1 \times 16^1) + (10 \times 16^0) = 654874$$

### 🚩 Step 3: Flag Retrieval

We construct the flag by wrapping the converted decimal value 654874 inside the target flag wrapper (academy{n}):

`Flag: academy{654874}`

### 💡 Key Takeaways

1-Pointer directives such as DWORD PTR [rbp-0x4] reference memory addresses on the stack frame used for local variables.

2-Tracing sequential data transfers (mov) from immediate literals to memory locations and then to hardware registers reveals program state.
