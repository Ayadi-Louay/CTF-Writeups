# Write-Up : Corrupted file

## Fresnsh Version

## 📋 Informations du Challenge

- **Nom du challenge :** Corrupted file
- **Plateforme / Événement :** picoMini by CMU-Africa
- **Auteur :** Yahaya Meddy
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

## 📝 Description

> _"This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life? Download the file here."_

---

## 🔍 Étape 1 : Inspection du fichier corrompu

Après avoir téléchargé le fichier fourni, la tentative d'ouverture en tant qu'image échoue car le fichier apparaît comme corrompu.

En suivant les indices, j'ai inspecté les premiers octets de l'en-tête du fichier avec la commande `xxd` :

```bash
xxd file | head
```

**Observation :**
Les premiers octets (la signature du fichier ou _Magic Bytes_) étaient altérés et ne correspondaient pas au format d'image attendu.

---

## 🛠️ Étape 2 : Réparation de l'en-tête Hexadécimal

1. Ouverture du fichier dans un éditeur hexadécimal en ligne (ou un outil comme `hexedit` / `Ghex`).
2. Modification des octets d'en-tête corrompus (`5c 78 ...`) pour les remplacer par les _Magic Bytes_ valides d'un fichier JPEG (`FF D8`).
3. Enregistrement et exportation du nouveau fichier réparé.

---

## 🚩 Étape 3 : Récupération du Flag

1. Ouverture du nouveau fichier réparé avec un visualiseur d'images.
2. L'image s'affiche correctement et le flag y est clairement lisible.

**Flag :** `picoCTF{...}` _(à remplacer par ton flag)_

---

## 💡 Key Takeaways / Notions retenues

- Les fichiers binaires utilisent des **Magic Bytes** au début du fichier pour indiquer leur format (ex: `FF D8 FF` pour le format JPEG).
- Quand un fichier ne s'ouvre pas, vérifier et réparer son en-tête hexadécimal avec un éditeur hex (Hex Editor) permet de restaurer le fichier d'origine.

## English Version

## 📋 Challenge Info

- **Challenge Name:** Corrupted file
- **Platform / Event:** picoMini by CMU-Africa
- **Author:** Yahaya Meddy
- **Category:** Forensics
- **Difficulty:** Easy

---

## 📝 Description

> _"This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life? Download the file here."_

---

## 🔍 Step 1: Inspecting the Corrupted File

After downloading the challenge file, trying to open it as a standard image failed because the file was corrupted.

Following the challenge hints, I inspected the header bytes using the `xxd` tool:

```bash
xxd file | head
```

**Observation:**
The initial file signature (_Magic Bytes_) was corrupted, preventing image viewers from recognizing the file format properly.

---

## 🛠️ Step 2: Hex Header Repair

1. Loaded the file into an online hex editor.
2. Replaced the corrupted header bytes with the correct JPEG file magic bytes (`FF D8`).
3. Exported and saved the repaired file.

---

## 🚩 Step 3: Image Opening & Flag Retrieval

1. Opened the repaired file using a standard image viewer.
2. The image rendered correctly, revealing the flag written on it.

**Flag:** `picoCTF{...}` _(replace with your actual flag)_

---

## 💡 Key Takeaways

- File types rely on **Magic Bytes** at the beginning of the file to define their structure (e.g., `FF D8 FF` for JPEG).
- Corrupted file headers can be fixed manually via a hex editor to restore readable media files.
