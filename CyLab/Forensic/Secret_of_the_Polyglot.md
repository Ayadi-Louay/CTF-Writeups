# Write-Up : Secret of the Polyglot

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Secret of the Polyglot
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** syreal
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

### 📝 Description

> _"The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?"_

---

### 🔍 Étape 1 : Ouverture initiale et seconde partie du Flag

On télécharge le fichier fourni et on suit l'indice du challenge (_"This problem can be solved by just opening the file in different ways"_).

1. On ouvre d'abord le fichier avec un navigateur web ou un lecteur de document PDF.
2. Le document s'ouvre correctement et affiche la **seconde partie du flag**.

---

### 🛠️ Étape 2 : Changement d'extension et première partie du Flag

Puisqu'il s'agit d'un fichier _polyglotte_ (un fichier valide dans plusieurs formats à la fois) :

1. On renomme le fichier en lui ajoutant l'extension `.png` (ou on l'ouvre directement avec un visualiseur d'images).
2. L'image s'affiche correctement et révèle la **première partie du flag**.

---

### 🚩 Étape 3 : Reconstitution du Flag

On rassemble la première partie (obtenue depuis l'image PNG) et la seconde partie (obtenue depuis le document PDF) pour former le flag complet.

**Flag :** `picoCTF{...}` _(à remplacer par le flag obtenu)_

---

### 💡 Key Takeaways / Notions retenues

- Un **fichier polyglotte** (Polyglot file) est un fichier conçu de manière à être interprété comme deux (ou plusieurs) formats de fichiers valides différents selon l'application qui l'ouvre (par exemple, un fichier à la fois PDF et PNG).
- Explorer différentes façons d'ouvrir ou de traiter un fichier suspect est une technique d'analyse Forensics incontournable.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Secret of the Polyglot
- **Platform / Event:** picoCTF 2024
- **Author:** syreal
- **Category:** Forensics
- **Difficulty:** Easy

---

### 📝 Description

> _"The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?"_

---

### 🔍 Step 1: Initial Inspection & Second Flag Portion

We download the challenge file and reference the hint (_"This problem can be solved by just opening the file in different ways"_).

1. We open the file using a web browser or a standard PDF reader.
2. The document renders correctly, displaying the **second portion of the flag**.

---

### 🛠️ Step 2: Extension Modification & First Flag Portion

Since the file is a _polyglot_ file (a file valid in multiple formats simultaneously):

1. We change the file extension to `.png` (or force-open it with an image viewer).
2. The image renders successfully, revealing the **first portion of the flag**.

---

### 🚩 Step 3: Reassembling the Flag

We concatenate the first half (extracted from the PNG image) with the second half (extracted from the PDF view) to form the full flag.

**Flag:** `picoCTF{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- A **polyglot file** is crafted to be simultaneously valid in two or more distinct file formats (e.g., both PDF and PNG valid headers/structures).
- Opening suspicious files with different context viewers (PDF readers, image viewers, text editors) is a key forensic inspection technique.
