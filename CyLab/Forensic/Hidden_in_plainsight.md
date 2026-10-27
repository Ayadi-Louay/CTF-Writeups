# Write-Up : Hidden in plainsight

## Fresnsh Version

### 📋 Informations du Challenge

Nom du challenge : Hidden in plainsight  
Plateforme / Événement : picoMini by CMU-Africa  
Auteur : Yahaya Meddy  
Catégorie : Forensics  
Difficulté : Easy

### 📝 Description

"You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag"

### 🔍 Étape 1 : Analyse des métadonnées

Après avoir téléchargé et visualisé l'image JPG, j'ai inspecté ses métadonnées à l'aide de l'outil exiftool :  
exiftool image.jpg
Observation :Le champ Comment (ou User Comment) des métadonnées contient une chaîne de caractères encodée en Base64.

### 🛠️ Étape 2 : Décodage du commentaire et du mot de passe

1-En décodant la valeur du commentaire sur CyberChef (recette From Base64), j'obtiens une indication de la forme steghide: <mot_de_passe_en_base64>.
2-J'utilise à nouveau CyberChef pour décoder le mot de passe encodé en Base64 afin d'obtenir le mot de passe en clair.

### 🔑 Étape 3 : Extraction avec Steghide et obtention du Flag

1-Muni du mot de passe extrait, j'utilise l'outil steghide pour extraire le fichier caché dans l'image :
steghide extract -sf image.jpg -p <mot_de_passe>
2-Un fichier texte contenant le flag est extrait avec succès.
3-J'ouvre le fichier pour lire le flag.

#### Flag : picoCTF{...} (à remplacer par ton flag)

## English Version

### 📋 Challenge InfoChallenge

Name: Hidden in plainsight  
Platform / Event: picoMini by CMU-Africa  
Author: Yahaya Meddy  
Category: Forensics  
Difficulty: Easy

### 📝 Description

"You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag"

### 🔍 Step 1: Metadata Analysis

After downloading and viewing the JPG image, I inspected its metadata using exiftool:  
exiftool image.jpg
Observation:The Comment (or User Comment) metadata field contains a Base64-encoded string.

### 🛠️ Step 2: Decoding the Comment and Passphrase

1-Decoding the comment string on CyberChef (using the From Base64 recipe) revealed a message formatted like steghide: <base64_encoded_passphrase>.
2-I then decoded the Base64 passphrase using CyberChef to retrieve the plaintext passphrase.

### 🔑 Step 3: Extraction via Steghide and Flag Retrieval

1-Using the retrieved passphrase, I extracted the hidden payload from the image with steghide:
steghide extract -sf image.jpg -p <passphrase>
2-A text file containing the flag was extracted successfully.
3-I opened the file and copied the flag.

#### Flag: picoCTF{...} (replace with your actual flag)
