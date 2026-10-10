Write-Up : Binary Digits

##French Version:

📋 Informations du Challenge
Nom du challenge : Binary Digits  
Plateforme / Événement : picoCTF 2026  
Auteur : Yahaya Meddy  
Catégorie : Forensics  
Difficulté : Easy

📝 Description
"This file doesn't look like much... just a bunch of 1s and 0s. But maybe it's not just random noise. Can you recover anything meaningful from this?"

🔍 Étape 1 : Analyse du fichier
Après avoir téléchargé le fichier fourni via le lien du challenge, je l'ai ouvert avec un éditeur de texte sous Kali Linux.  
Observation :Le fichier contient uniquement une suite de caractères bruts composés de 0 et de 1 (données sous forme binaire ASCII).

🛠️ Étape 2 : Décodage avec CyberChef
Pour convertir cette suite binaire en un fichier exploitable :
1-Ouverture de l'outil CyberChef.
2-Copie-collé du contenu du fichier dans la section Input.
3-Application de la recette From Binary dans la section Recipe.
Résultat :Le décodage binaire a reconstruit les octets originaux du fichier, révélant qu'il s'agissait en réalité d'un fichier image (ex: PNG/JPG).

🚩 Étape 3 : Récupération du Flag
1-Téléchargement / enregistrement de l'image restituée depuis CyberChef.
2-Ouverture et lecture du fichier image.
3-Le flag apparaît directement écrit sur l'image.

Flag : picoCTF{...} (à remplacer par ton flag)

##English Version:

📋 Challenge Info
Challenge Name: Binary Digits
Platform / Event: picoCTF 2026
Author: Yahaya Meddy
Category: Forensics
Difficulty: Easy

📝 Description
"This file doesn't look like much... just a bunch of 1s and 0s. But maybe it's not just random noise. Can you recover anything meaningful from this?"

🔍 Step 1: File Analysis
After downloading the file provided via the challenge link, I opened it using a text editor on Kali Linux.
Observation:
The file contains only a raw stream of characters consisting of 0s and 1s (data in ASCII binary format).

🛠️ Step 2: Decoding with CyberChef
To convert this binary stream into an executable/usable file:
1-Open the CyberChef tool.
2-Copy and paste the file contents into the Input section.
3-Apply the "From Binary" recipe in the Recipe section.
Result : The binary decoding reconstructed the file's original bytes, revealing that it was actually an image file (e.g., PNG/JPG).

🚩 Step 3: Flag Retrieval
1-Download / save the restored image from CyberChef.
2-Open and view the image file.
3-The flag appears directly written on the image.

Flag: picoCTF{...} (replace with your actual flag)
