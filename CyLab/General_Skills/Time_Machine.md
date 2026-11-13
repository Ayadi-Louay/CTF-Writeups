# Write-Up : Time Machine

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Time Machine
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Jeffery John
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"What was I last working on? I remember writing a note to help me remember... You can download the challenge files here: challenge.zip"_

---

### 🔍 Étape 1 : Extraction et inspection des fichiers

On commence par décompresser l'archive `challenge.zip` fournie à l'aide de la commande `unzip` :

```bash
unzip challenge.zip
cd drop-in
```

En listant le contenu du dossier extrait (`drop-in`), on remarque la présence d'un fichier `message.txt` et d'un dossier caché `.git`, indiquant qu'il s'agit d'un dépôt Git local.

On affiche le contenu du fichier texte :

```Bash
cat message.txt
```

**Résultat :** This is what I was working on, but I'd need to look at my commit history to know why...

### 🛠️ Étape 2 : Analyse de l'historique Git

Comme l'indique le message (et le troisième indice du challenge : "When commiting a file with git, a message can (and should) be included."), la solution se trouve dans l'historique des commits.  
On utilise la commande Git appropriée pour afficher l'historique des modifications :

```Bash
git log
```

Le terminal nous retourne les détails du dernier commit, et on y découvre que le flag a été utilisé comme message de commit :

```Plaintext
commit f6a4efde6c5f14fb257c993e1fd26bc3d9607ec8 (HEAD -> master)
Author: academy <ops@cylabacademy.org>
Date: Wed Sep 23 05:12:19 2026 +0000

    academy{t1m3m@ch1n3_238dc8a1}
```

#### 🚩 Étape 3 : Obtention du Flag

Le flag est directement lisible dans le message du commit.  
**Flag :** `academy{t1m3m@ch1n3_238dc8a1}`

### 💡 Key Takeaways / Notions retenues

- **Reconnaissance Git :** La présence d'un dossier `.git` signifie que l'historique complet du projet est disponible localement.
- **Fuite d'informations (Information Disclosure) :** Les messages de commit Git (`git log`) peuvent souvent contenir des informations sensibles, des secrets ou des mots de passe laissés par erreur par les développeurs.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Time Machine
- **Platform / Event:** picoCTF 2024
- **Author:** Jeffery John
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "What was I last working on? I remember writing a note to help me remember... You can download the challenge files here: challenge.zip"

---

### 🔍 Step 1: Extracting & Inspecting the Files

We begin by unzipping the provided `challenge.zip` file:

```Bash
unzip challenge.zip
cd drop-in
```

Listing the contents of the extracted drop-in directory reveals a `message.txt` file and a hidden `.git` folder, indicating this is a local Git repository.

We read the text file:

```Bash
cat message.txt
```

**Result:** This is what I was working on, but I'd need to look at my commit history to know why...

### 🛠️ Step 2: Analyzing the Git History

As hinted by the text file and the challenge's third hint ("When commiting a file with git, a message can (and should) be included."[cite: 2]), the solution lies within the version control history.

We use the standard Git command to view the commit log:

```Bash
git log
```

The output displays the most recent commit, revealing that the flag was used directly as the commit message:

```Plaintext
commit f6a4efde6c5f14fb257c993e1fd26bc3d9607ec8 (HEAD -> master)
Author: academy <ops@cylabacademy.org>
Date: Wed Sep 23 05:12:19 2026 +0000

    academy{t1m3m@ch1n3_238dc8a1}
```

### 🚩 Step 3: Flag Retrieval

The flag is plainly visible in the commit message block.  
**Flag:** `academy{t1m3m@ch1n3_238dc8a1}`

### 💡 Key Takeaways

- **Git Reconnaissance:** Finding a hidden `.git` folder means you have access to the entire local version history of the project.
- **Information Disclosure:** Git commit messages (`git log`) are a common place to find accidentally leaked sensitive data, secrets, or credentials left behind by developers.
