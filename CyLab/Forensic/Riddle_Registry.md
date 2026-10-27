# Write-Up : Riddle Registry

## 📋 Informations du Challenge

- **Nom du challenge :** Riddle Registry
- **Plateforme / Événement :** picoMini by CMU-Africa
- **Auteur :** Prince Niyonshuti N.
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

## 📝 Description

> _"Hi, intrepid investigator! 📄 🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here Hidden Confidential Document and uncover the flag within the metadata."_

---

## 🔍 Étape 1 : Inspection initiale & Premières tentatives

Après avoir téléchargé le fichier PDF fourni, l'analyse initiale n'a rien révélé d'anormal à première vue :

1. **Ouverture du fichier :** Le document s'ouvre normalement et s'affiche comme un fichier PDF standard.
2. **Recherche de chaînes brutes :** J'ai tenté d'extraire directement le flag à l'aide de l'outil `strings` combiné avec `grep` :
   ```bash
   strings document.pdf | grep -i "pico"
   ```
   _Résultat :_ Aucune donnée ou chaîne intéressante n'apparaît par cette méthode.

---

## 🛠️ Étape 2 : Analyse des métadonnées (`exiftool`)

En l'absence d'indices dans le contenu visible ou les chaînes textuelles brutes, j'ai inspecté les métadonnées du document avec **ExifTool** :

```bash
exiftool document.pdf
```

**Observation :**
Dans les champs de métadonnées, le champ **Author** contient une chaîne de caractères suspecte encodée en **Base64**.

---

## 🚩 Étape 3 : Décodage du Flag avec CyberChef

1. Copie de la chaîne Base64 présente dans le champ **Author**.
2. Ouverture de l'outil **CyberChef**.
3. Collage du texte dans le panneau **Input**.
4. Application de la recette **`From Base64`** dans la section **Recipe**.
5. Le flag apparaît en clair dans le panneau **Output**.

**Flag :** `picoCTF{...}` _(à remplacer par ton flag)_

# Write-Up: Riddle Registry

## 📋 Challenge Info

- **Challenge Name:** Riddle Registry
- **Platform / Event:** picoMini by CMU-Africa
- **Author:** Prince Niyonshuti N.
- **Category:** Forensics
- **Difficulty:** Easy

---

## 📝 Description

> _"Hi, intrepid investigator! 📄 🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here Hidden Confidential Document and uncover the flag within the metadata."_

---

## 🔍 Step 1: Initial Inspection & First Attempts

After downloading the provided PDF file, the initial inspection yielded no obvious visual leads:

1. **Opening the file:** The document opens normally as a standard PDF file.
2. **Raw string search:** I attempted to find the flag directly using `strings` piped into `grep`:
   ```bash
   strings document.pdf | grep -i "pico"
   ```
   _Result:_ No relevant hits or flags were found using this command.

---

## 🛠️ Step 2: Metadata Analysis (`exiftool`)

Since searching through the raw content was unsuccessful, I inspected the document's metadata using **ExifTool**:

```bash
exiftool document.pdf
```

**Observation:**
Within the metadata fields, the **Author** attribute contains a suspicious Base64-encoded string.

---

## 🚩 Step 3: Flag Decoding via CyberChef

1. Copy the Base64 string found inside the **Author** field.
2. Open **CyberChef**.
3. Paste the string into the **Input** box.
4. Add the **`From Base64`** recipe.
5. The plaintext flag is decoded and displayed in the **Output** box.

**Flag:** `picoCTF{...}` _(replace with your actual flag)_
