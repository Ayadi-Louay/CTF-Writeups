# Write-Up : Flag in Flame

## Frensh Version

### 📋 Informations du Challenge

Nom du challenge : Flag in Flame  
Plateforme / Événement : picoMini by CMU-Africa  
Auteur : Prince Niyonshuti N.  
Catégorie : Forensics  
Difficulté : Easy

### 📝 Description

"The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it..."

### 🔍 Étape 1 : Inspection du fichier journal

Après avoir téléchargé le fichier journal fourni, je l'ai ouvert avec l'éditeur de texte Mousepad sous Linux.  
Observation :
Le fichier contient un bloc massif de données textuelles encodées sous forme de chaîne Base64.

### 🛠️ Étape 2 : Décodage et Rendu de l'image via CyberChef

Copie du texte brut depuis Mousepad vers la section Input de CyberChef.Application de la recette From Base64.  
Utilisation de l'option de rendu/prévisualisation d'image dans CyberChef (ou enregistrement du résultat au format image).  
Enregistrement / Téléchargement du fichier image généré.

### 🚩 Étape 3 : Extraction et Décodage Hexadécimal du Flag

Ouverture de l'image générée.  
Copie du texte (chaîne de caractères hexadécimaux) figurant sur l'image.  
Décodage de cette chaîne hexadécimale (recette From Hex sur CyberChef) pour obtenir le texte en clair.

#### Flag : picoCTF{...} (à remplacer par ton flag)

## English Version

### 📋 Challenge Info

Challenge Name: Flag in Flame  
Platform / Event: picoMini by CMU-Africa  
Author: Prince Niyonshuti N.  
Category: Forensics  
Difficulty: Easy

### 📝 Description

"The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it..."

### 🔍 Step 1: Inspecting the Log File

After downloading the provided log file, I opened it using the Mousepad text editor on Linux.  
Observation:
The file contains a massive block of encoded text in Base64 format.

### 🛠️ Step 2: Decoding and Rendering the Image with CyberChef

Copy the raw text from Mousepad into CyberChef's Input section.Apply the From Base64 recipe.  
Use the image render option in CyberChef to view/render the binary output as an image.  
Download and save the rendered image file.

#### 🚩 Step 3: Hexadecimal Decoding and Flag

RetrievalOpen the saved image.  
Copy the hexadecimal text string displayed inside the image.  
Decode the hexadecimal string (using the From Hex recipe in CyberChef) to retrieve the plaintext flag.

#### Flag: picoCTF{...} (replace with your actual flag)
