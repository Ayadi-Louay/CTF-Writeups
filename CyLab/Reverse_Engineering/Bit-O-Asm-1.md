# Write-Up : Bit-0-Asm-1

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Bit-0-Asm-1
- **Plateforme / Événement :** picoCTF
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Reverse Engineering
- **Difficulté :** Easy

---

### 📝 Description

> _"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."_

---

### 🔍 Étape 1 : Téléchargement et inspection du fichier dump

On télécharge le fichier texte contenant le dump d'instructions assembleur x86_64 et on l'ouvre dans un éditeur de texte.

```assembly
<+0>:    endbr64
<+4>:    push   rbp
<+5>:    mov    rbp,rsp
<+8>:    mov    DWORD PTR [rbp-0x4],edi
<+11>:   mov    QWORD PTR [rbp-0x10],rsi
<+15>:   mov    eax,0x30
<+20>:   pop    rbp
<+21>:   ret
```

### 🛠️ Étape 2 : Analyse de l'instruction et conversion de la base numérique

En isolant la ligne d'instruction qui affecte la valeur au registre eax :
`mov    eax,0x30`

On observe que la valeur hexadécimale `0x30` est chargée directement dans le registre `eax`.

Le challenge demande d'exprimer la valeur du registre `eax` en base décimale. On effectue la conversion de l'hexadécimal vers le décimal (via CyberChef, Python ou calcul direct) :$$0\text{x}30 = (3 \times 16^1) + (0 \times 16^0) = 48$$

### 🚩 Étape 3 : Obtention du Flag

On insère la valeur décimale 48 au format demandé (academy{n}).

`Flag : academy{48}`

### 💡Key Takeaways / Notions retenues

1-L'instruction x86 mov permet de transférer une valeur immédiate (comme une constante hexadécimale 0x30) directement dans un registre processeur (eax).

2-La notation 0x indique une représentation en base 16 (hexadécimale), qu'il convient de convertir en base 10 (décimale) selon les besoins d'analyse.

## 🇬🇧 English Version

### 📋Challenge InfoChallenge

- **Name:** Bit-0-Asm-1
- **Platform / Event:** picoCTF
- **Author:** LT 'syreal' Jones
- **Category:** Reverse Engineering
- **Difficulty:** Easy

### 📝 Description

"Can you figure out what is in the eax register? Put your answer in the academy flag format: academy{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be academy{17}. Download the assembly dump here."

### 🔍 Step 1: File Retrieval & Assembly Dump Inspection

We download the provided text file containing the x86_64 assembly code dump and open it for review.

```asembly
<+4>:    push   rbp
<+5>:    mov    rbp,rsp
<+8>:    mov    DWORD PTR [rbp-0x4],edi
<+11>:   mov    QWORD PTR [rbp-0x10],rsi
<+15>:   mov    eax,0x30
<+20>:   pop    rbp
<+21>:   ret
```

### 🛠️ Step 2: Instruction Analysis & Base Conversion

Isolating the target instruction line affecting the eax register:
`mov eax,0x30`

We observe that the hexadecimal literal `0x30` is loaded into register `eax`.Per the challenge instructions, the value inside eax must be formatted in decimal representation.

We convert the hex value `0x30` to decimal (using CyberChef, Python, or standard arithmetic):$$0\text{x}30 = (3 \times 16^1) + (0 \times 16^0) = 48$$

### 🚩 Step 3: Flag Retrieval

We construct the flag by placing the decimal integer 48 inside the required flag wrapper (academy{n}).

`Flag: academy{48}`

### 💡 Key Takeaways

1-The x86 mov instruction copies an immediate value (such as hexadecimal 0x30) directly into a target register (eax).

2-Values prefixed with 0x represent base-16 hexadecimal numbers and must be converted to base-10 when decimal output is requested.
