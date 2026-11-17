# Write-Up : Blame Game

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Blame Game
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Jeffery John
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Someone's commits seems to be preventing the program from working. Who is it? You can download the challenge files here: challenge.zip"_

---

### 🔍 Étape 1 : Téléchargement et extraction

La première étape consiste à télécharger l'archive `challenge.zip` fournie dans l'énoncé, puis à l'extraire. En explorant le dossier extrait, on remarque qu'il s'agit d'un dépôt Git, ce qui correspond aux indices du challenge suggérant d'inspecter les modifications faites par de multiples utilisateurs.

---

### 🛠️ Étape 2 : Inspection de l'historique des commits

La description nous demande de trouver l'auteur d'un commit spécifique qui empêcherait le programme de fonctionner. Pour explorer l'historique des modifications d'un dépôt Git, la commande `git log` est l'outil idéal.

En exécutant `git log` dans le terminal, on affiche la liste complète des commits réalisés sur le projet, incluant l'identifiant du commit, l'auteur, la date et le message associé.

---

### 🚩 Étape 3 : Obtention du Flag

En parcourant les résultats de la commande `git log`, on tombe rapidement sur un commit dont l'auteur attire l'attention. L'adresse email est classique (`ops@cylabacademy.org`), mais le nom de l'auteur a été remplacé par le format exact du flag :

```text
commit d621b1a352d14b62e3ec51e8d0bc91ba14b44eae
Author: academy{@sk_th3_1nt3rn_8bd9c746} <ops@cylabacademy.org>
Date:   Wed Sep 23 05:07:00 2026 +0000

    optimize file size of prod code
```

**Flag :** `academy{@sk_th3_1nt3rn_8bd9c746}`

---

### 💡 Key Takeaways / Notions retenues

- **Historique Git (git log) :** La commande `git log` est indispensable pour retracer l'historique d'un projet, comprendre quelles modifications ont été apportées, quand, et surtout par qui.
- **L'importance des métadonnées :** Dans les défis CTF (et dans les incidents de sécurité réels), les informations sensibles ou les identifiants peuvent se cacher dans les métadonnées (comme le nom de l'auteur d'un commit) plutôt que dans le code source lui-même.
- **Alternative (git blame) :** Comme le suggère le titre du challenge, une autre approche aurait pu être d'utiliser `git blame <fichier>` pour voir ligne par ligne quel auteur a effectué la dernière modification, mais une simple lecture du log était ici suffisante.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Blame Game
- **Platform / Event:** picoCTF 2024
- **Author:** Jeffery John
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "Someone's commits seems to be preventing the program from working. Who is it? You can download the challenge files here: challenge.zip"

---

### 🔍 Step 1: Downloading and Extracting

The first step is to download the `challenge.zip` file provided in the prompt and extract it. Upon exploring the extracted folder, we find a Git repository, aligning with the challenge hints about inspecting changes made by multiple users in collaborative projects.

---

### 🛠️ Step 2: Inspecting Commit History

The description asks us to identify "Who is it?" regarding a problematic commit. To review the history of a Git repository, the `git log` command is the standard tool.

Running `git log` in the terminal outputs the chronological sequence of commits, showing the commit hash, the author, the date, and the commit message.

---

### 🚩 Step 3: Flag Retrieval

Scrolling through the `git log` output, we spot a commit where the author's name is highly unusual. While the email (`ops@cylabacademy.org`) looks normal, the author's name field contains our target flag:

```text
commit d621b1a352d14b62e3ec51e8d0bc91ba14b44eae
Author: academy{@sk_th3_1nt3rn_8bd9c746} <ops@cylabacademy.org>
Date:   Wed Sep 23 05:07:00 2026 +0000

    optimize file size of prod code
```

**Flag:** `academy{@sk_th3_1nt3rn_8bd9c746}`

---

### 💡 Key Takeaways

- **Git History (git log):** The `git log` command is crucial for tracking a project's timeline, understanding what changes were made, when they were made, and by whom.
- **Hidden Metadata:** In CTFs (and real-world security scenarios), sensitive information or flags can be hidden in configuration metadata (like a Git commit author name) rather than directly in the source code files.
- **Alternative Approach (git blame):** The challenge title hints at the `git blame <file>` command, which annotates each line of a file with the revision and author who last modified it. However, a simple log review was more than enough to solve this challenge.
