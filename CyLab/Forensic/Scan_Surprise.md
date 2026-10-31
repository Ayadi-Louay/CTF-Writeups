# Write-Up : Scan Surprise

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Scan Surprise
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Jeffery John
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

### 📝 Description

> _"I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? You can download the challenge files here: challenge.zip. The same files are accessible via SSH here: ssh -p 20305 ctf-player@xebec.cylabacademy.net"_

---

### 🔍 Étape 1 : Connexion au serveur

On se connecte au serveur distant en SSH avec la commande fournie :

```bash
ssh -p 20305 ctf-player@xebec.cylabacademy.net
```

_(Mot de passe : `647e170e`)_

**Observation :**
Dès la connexion, un code QR s'affiche directement dans le terminal sous forme de caractères ASCII, et un fichier image `flag.png` est présent dans le répertoire courant.

---

### 🛠️ Étape 2 : Décodage du Code QR avec `zbarimg`

En suivant l'indice conseillant l'utilisation de `zbar-tools`, on utilise l'outil `zbarimg` pour lire et analyser l'image `flag.png` directement en ligne de commande :

```bash
zbarimg flag.png
```

**Sortie de la commande :**

```text
Connection Error (Failed to connect to socket /run/dbus/system_bus_socket: No such file or directory)
Connection Null
QR-Code:academy{p33k_@_b00_36769c4b}
scanned 1 barcode symbols from 1 images in 0 seconds
```

---

### 🚩 Étape 3 : Obtention du Flag

L'outil extrait et affiche directement le contenu textuel encodé dans le code QR.

**Flag :** `academy{p33k_@_b00_36769c4b}`

---

### 💡 Key Takeaways / Notions retenues

- Les **codes QR** servent à encoder des données textuelles, des liens ou des chaînes complexes sous forme visuelle.
- L'utilitaire CLI **`zbarimg`** (du paquet `zbar-tools`) permet de décoder rapidement des codes QR ou barres depuis un fichier image sans avoir besoin de scanner manuellement avec un téléphone.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Scan Surprise
- **Platform / Event:** picoCTF 2024
- **Author:** Jeffery John
- **Category:** Forensics
- **Difficulty:** Easy

---

### 📝 Description

> _"I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? You can download the challenge files here: challenge.zip. The same files are accessible via SSH here: ssh -p 20305 ctf-player@xebec.cylabacademy.net"_

---

### 🔍 Step 1: Remote Server Connection

We connect to the remote server via SSH using the provided command:

```bash
ssh -p 20305 ctf-player@xebec.cylabacademy.net
```

_(Password: `647e170e`)_

**Observation:**
Upon successful login, an ASCII QR code is rendered directly in the terminal, and an image file named `flag.png` is stored in the home directory.

---

### 🛠️ Step 2: QR Code Decoding via `zbarimg`

Following the hint suggesting `zbar-tools`, we run `zbarimg` to extract the payload from `flag.png` directly in the command line:

```bash
zbarimg flag.png
```

**Command Output:**

```text
Connection Error (Failed to connect to socket /run/dbus/system_bus_socket: No such file or directory)
Connection Null
QR-Code:academy{p33k_@_b00_36769c4b}
scanned 1 barcode symbols from 1 images in 0 seconds
```

---

### 🚩 Step 3: Flag Retrieval

The tool parses the barcode layout and outputs the decoded plaintext string directly.

**Flag:** `academy{p33k_@_b00_36769c4b}`

---

### 💡 Key Takeaways

- **QR Codes** encapsulate textual payload, URLs, or arbitrary data inside a matrix barcode.
- The CLI tool **`zbarimg`** (part of `zbar-tools`) allows quick automated decoding of QR codes and barcodes directly within Linux terminal environments.
