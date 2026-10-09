Write-Up : Binary Digits

📋 Informations du ChallengeNom du challenge : Binary Digits  
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
