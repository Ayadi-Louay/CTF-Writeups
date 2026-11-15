# Write-Up : Commitment Issues

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Commitment Issues
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Jeffery John
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"I accidentally wrote the flag down. Good thing I deleted it! You download the challenge files here: challenge.zip"_

---

### 🔍 Étape 1 : Téléchargement et extraction

On télécharge l'archive `challenge.zip` fournie (à l'aide de `wget`) puis on l'extrait avec la commande `unzip`. L'extraction crée un dossier `drop-in` qui contient un dépôt Git local caché (`.git`).

On se déplace dans ce dossier et on liste les fichiers :

```bash
cd drop-in/
ls
```

Le dossier contient flag.py et message.txt. En affichant le contenu de message.txt, on ne trouve que la mention "TOP SECRET". Le fichier flag.py ne contient quant à lui qu'un faux morceau de flag.

---

### 🛠️ Étape 2 : Analyse de l'historique et "Checkout"

L'auteur indique qu'il a écrit le flag puis l'a supprimé. Les indices du challenge nous rappellent que le contrôle de version (Git) permet de récupérer des fichiers modifiés ou perdus et qu'il est possible d'utiliser la commande checkout pour voir l'état des fichiers dans des commits précédents.  
On affiche d'abord l'historique des modifications avec :

```Bash
git log
```

Dans l'historique, on repère un commit précédent (l'identifiant `08c903aa2824148d91cd462d37def218762455fc` dans ce cas) qui correspond au moment où le flag a été ajouté avant d'être écrasé.  
On utilise alors la commande checkout pour revenir à l'état de ce commit spécifique :

```Bash
git checkout 08c903aa2824148d91cd462d37def218762455fc
```

---

### 🚩 Étape 3 : Obtention du Flag

Maintenant que nous sommes revenus dans le passé (en mode detached HEAD), le fichier message.txt a retrouvé son état d'origine. On l'affiche de nouveau :

```Bash
cat message.txt
```

Le flag originellement sauvegardé s'affiche dans le terminal.  
**Flag :** `academy{s@n1t1z3_43665d2b}`

---

### 💡 Key Takeaways / Notions retenues

- **Persistance des données sous Git :** Lorsqu'un fichier est modifié ou supprimé dans Git et qu'un nouveau commit est créé, l'ancienne version n'est pas détruite. L'historique conserve une trace immuable de tous les états précédents.
- **Récupération avec Checkout :** La commande git checkout <commit_hash> est extrêmement utile pour naviguer dans l'historique d'un dépôt et examiner le code tel qu'il était à un instant T.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Commitment Issues
- **Platform / Event:** picoCTF 2024
- **Author:** Jeffery John
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "I accidentally wrote the flag down. Good thing I deleted it! You download the challenge files here: challenge.zip"

---

### 🔍 Step 1: Downloading & Extracting

We begin by downloading the provided challenge.zip file (using wget) and unzipping it. The extraction creates a drop-in directory containing a hidden local Git repository (.git).  
We navigate into the directory and list the available files:

```Bash
cd drop-in/
ls
```

The folder contains flag.py and message.txt. Reading message.txt using the cat command only reveals the text "TOP SECRET". The flag.py file only contains a dummy partial flag.

---

### 🛠️ Step 2: History Analysis & Git Checkout

The author mentions they accidentally wrote the flag down and then deleted it. The challenge hints remind us that version control helps recover changed or lost files and that we can 'checkout' specific commits to view the files inside them at that point in time.  
First, we view the commit history by running:

```Bash
git log
```

From the log, we identify a previous commit (specifically hash 08c903aa2824148d91cd462d37def218762455fc in this instance) representing the moment the flag was initially added before being sanitized. We then use the checkout command to restore the repository to that exact commit:

```Bash
git checkout 08c903aa2824148d91cd462d37def218762455fc
```

---

### 🚩 Step 3: Flag Retrieval

Now that our working directory is rolled back in time (in a detached HEAD state), the message.txt file has reverted to its previous, unredacted version. We read it again:

```Bash
cat message.txt
```

The original flag is successfully revealed in the terminal output.  
**Flag:** `academy{s@n1t1z3_43665d2b}`

---

### 💡 Key Takeaways

- **Data Persistence in Git:** Deleting or changing a line of text and pushing a new commit does not completely erase the data. Git's version control system keeps a permanent, immutable record of all committed states.
- **Time Travel with Checkout:** The git checkout <commit_hash> command is a vital tool for exploring a repository's timeline, allowing you to instantly restore and inspect historical file versions.
