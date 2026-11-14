# Write-Up : Super SSH

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Super SSH
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Jeffery John
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Using a Secure Shell (SSH) is going to be pretty important. Can you ssh as ctf-player to chatelaine.cylabacademy.net at port 48490 to get the flag? You'll also need the password fa1a82ad. If asked, accept the fingerprint with yes."_

---

### 🔍 Étape 1 : Connexion au serveur via SSH

En lisant la description du challenge, on récupère les informations de connexion : l'utilisateur (`ctf-player`), l'hôte (`chatelaine.cylabacademy.net`) et le port spécifique (`48490`).
On utilise la commande `ssh` dans le terminal en spécifiant le port avec l'option `-p` :

```bash
ssh -p 48490 ctf-player@chatelaine.cylabacademy.net
```

(Si le terminal demande d'accepter l'empreinte du serveur (fingerprint), on tape yes et on valide.)

---

### 🚩 Étape 2 : Authentification et obtention du Flag

Le serveur nous demande ensuite le mot de passe de l'utilisateur ctf-player. On saisit le mot de passe fourni dans la description (fa1a82ad).
(Note : sous Linux, les caractères du mot de passe ne s'affichent pas lors de la frappe, c'est normal.)

```Plaintext
ctf-player@chatelaine.cylabacademy.net's password:
Welcome ctf-player, here's your flag: academy{s3cur3_c0nn3ct10n_fbd97b2a}
Connection to chatelaine.cylabacademy.net closed.
```

Dès que l'authentification réussit, le serveur affiche un message de bienvenue contenant le flag et ferme immédiatement la connexion.  
**Flag :** `academy{s3cur3_c0nn3ct10n_fbd97b2a}`

---

### 💡 Key Takeaways / Notions retenues

- **Client SSH :** La commande ssh est l'outil standard pour se connecter à distance et de manière sécurisée à une machine Linux.
- **Port spécifique :** Par défaut, SSH utilise le port 22. Si un serveur écoute sur un autre port (comme ici le 48490), il est obligatoire d'utiliser le drapeau -p <port> pour s'y connecter.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Super SSH
- **Platform / Event:** picoCTF 2024
- **Author:** Jeffery John
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "Using a Secure Shell (SSH) is going to be pretty important. Can you ssh as ctf-player to chatelaine.cylabacademy.net at port 48490 to get the flag? You'll also need the password fa1a82ad. If asked, accept the fingerprint with yes."

---

### 🔍 Step 1: Connecting to the Server via SSH

From the challenge description, we gather the necessary connection details: the username (`ctf-player`), the hostname (`chatelaine.cylabacademy.net`), and the custom port (`48490`).
We construct our `ssh` command, making sure to use the `-p` flag to specify the non-standard port:

```Bash
ssh -p 48490 ctf-player@chatelaine.cylabacademy.net
```

(If prompted to verify the host fingerprint, we simply type yes and press Enter.)

---

### 🚩 Step 2: Authentication & Flag Retrieval

The server then prompts us for the ctf-player password. We input the password provided in the prompt (fa1a82ad).
(Note: As a standard security feature in Linux terminals, passwords are completely hidden when typed.)

```Plaintext
ctf-player@chatelaine.cylabacademy.net's password:
Welcome ctf-player, here's your flag: academy{s3cur3_c0nn3ct10n_fbd97b2a}
Connection to chatelaine.cylabacademy.net closed.
```

Upon successful authentication, the server immediately prints a welcome message containing the flag and terminates the connection.  
**Flag:** `academy{s3cur3_c0nn3ct10n_fbd97b2a}`

---

### 💡Key Takeaways

- **SSH Client:** The ssh command is the standard utility for accessing remote Linux machines securely over a network.
- **Custom Ports:** SSH defaults to port 22. If a service is running on a different port (like 48490 here), you must explicitly tell the client which port to connect to using the -p <port> argument.
