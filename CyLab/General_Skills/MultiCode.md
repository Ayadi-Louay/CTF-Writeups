# Write-Up : MultiCode

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** MultiCode
- **Plateforme / Événement :** picoCTF 2026
- **Auteur :** Yahaya Meddy
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

_"We intercepted a suspiciously encoded message, but it's clearly hiding a flag. No encryption, just multiple layers of obfuscation. Can you peel back the layers and reveal the truth? Download the message."_

---

### 🔍 Étape 1 : Récupération du message encodé

On télécharge le fichier `message` fourni dans le défi. Le contenu récupéré est une chaîne de caractères encodée sous plusieurs couches :

```text
NmU3MDZlNzE3MjdhNmMyNTM3NDI2MTcyNjY2NzcyNzE1ZjcyNjE3MDMwNzE3NjYxNzQ1ZjM4MzYzOTM3NzA3MDczMzIyNTM3NDQ=
```

### 🛠️ Étape 2 : Décodage séquentiel avec CyberChef

Au lieu d'utiliser la ligne de commande, on charge l'outil web CyberChef et on configure la recette (Recipe) en enchaînant les opérations de décodage dans l'ordre inverse de leur application :

1- **From Base64 :**  
**Raison :** La chaîne se termine par **=** et utilise le jeu de **caractères standard Base64**.  
**Résultat intermédiaire :** `6e706e71727a6c2537426172666772715f72617030717661745f3836393770707332253744`

2- **From Hex :**  
**Raison :** La sortie intermédiaire ne comporte que des caractères hexadécimaux **(0-9, a-f)**.  
**Résultat intermédiaire :** `npnqrzl%7Barfgrq_rap0qvat_8697pps2%7D`

3- **URL Decode :**
**Raison :** Présence des caractères encodés **%7B** (qui correspond à {) et **%7D** (qui correspond à }).  
**Résultat intermédiaire :** `npnqrzl{arfgrq_rap0qvat_8697pps2}`

4- **ROT13 :**  
**Raison :** La structure npnqrzl{...} est la version chiffrée par décalage de 13 positions du préfixe academy{...}.  
**Résultat final :** `academy{nested_enc0ding_8697ccf2}`

### 🚩 Étape 3 : Obtention du Flag

Une fois les 4 opérations appliquées dans la recette CyberChef, le flag déchiffré apparaît dans la zone de sortie (Output).

`Flag : academy{nested_enc0ding_8697ccf2}`

### 💡 Key Takeaways / Notions retenues

- Encodages multiples en cascade : Lorsque des données subissent plusieurs couches d'obfuscation, le déchiffrement doit s'effectuer strictly dans l'ordre inverse de leur application.

- Recette CyberChef : CyberChef permet de construire une recette graphique dynamique (Recipe) pour traiter et visualiser en temps réel chaque étape de transformation d'une chaîne complexe.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** MultiCode
- **Platform / Event:** picoCTF 2026
- **Author:** Yahaya Meddy
- **Category:** General Skills
- **Difficulty:** Easy

### 📝 Description

"We intercepted a suspiciously encoded message, but it's clearly hiding a flag. No encryption, just multiple layers of obfuscation. Can you peel back the layers and reveal the truth? Download the message."

### 🔍 Step 1: Input Retrieval

We download the provided message file containing the multi-layered obfuscated string:

```
NmU3MDZlNzE3MjdhNmMyNTM3NDI2MTcyNjY2NzcyNzE1ZjcyNjE3MDMwNzE3NjYxNzQ1ZjM4MzYzOTM3NzA3MDczMzIyNTM3NDQ=
```

### 🛠️ Step 2: Sequential Decoding via CyberChef

Instead of running command-line utilities, we use CyberChef to build a multi-step decoding recipe, peeling back each layer in reverse order:

1- **From Base64:**  
**Indicator:** Padding trailing **=** character and standard **Base64 charset**.  
**Intermediate Output:** `6e706e71727a6c2537426172666772715f72617030717661745f3836393770707332253744`

2-**From Hex:**
**Indicator:** String composed exclusively of hexadecimal digits **(0-9, a-f)**.  
**Intermediate Output:** `npnqrzl%7Barfgrq_rap0qvat_8697pps2%7D`

3-**URL Decode:**  
**Indicator:** URL-encoded characters **%7B** (opening bracket {) and **%7D** (closing bracket }).  
**Intermediate Output:** `npnqrzl{arfgrq_rap0qvat_8697pps2}`

4-**ROT13:**  
**Indicator:** The prefix npnqrzl{...} matches the ROT13 cipher offset of academy{...}.  
**Final Output:** `academy{nested_enc0ding_8697ccf2}`

### 🚩 Step 3: Flag Retrieval

Executing the combined recipe inside CyberChef reveals the recovered flag in the output pane.

`Flag: academy{nested_enc0ding_8697ccf2}`

### 💡 Key Takeaways

- Multi-Layer Encoding: Reversing nested obfuscation schemes requires identifying each encoding pattern and peeling them back in reverse sequence.
- CyberChef Automation: Using CyberChef's pipeline recipe capability streamlines complex multi-stage decoding without switching between terminal tools.
