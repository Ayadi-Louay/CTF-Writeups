# Write-Up : Collaborative Development

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Collaborative Development
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Jeffery John
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"My team has been working very hard on new features for our flag printing program! I wonder how they'll work together? You can download the challenge files here: challenge.zip"_

---

### 🔍 Étape 1 : Exploration du dépôt et des branches

Après avoir téléchargé et extrait l'archive, on se rend dans le dossier `drop-in` qui contient un fichier `flag.py` et un dépôt Git caché. En affichant le contenu initial de `flag.py`, on ne trouve qu'une simple instruction d'impression : `print("Printing the flag...")`.

Le premier indice du challenge nous suggère d'utiliser la commande `git branch -a` pour voir les différentes branches disponibles. En exécutant cette commande, on découvre trois branches de développement en plus de la branche principale :

- `feature/part-1`
- `feature/part-2`
- `feature/part-3`

---

### 🛠️ Étape 2 : Inspection des développements parallèles

En naviguant d'une branche à l'autre avec la commande `git checkout`, on s'aperçoit que chaque développeur a ajouté un morceau du flag dans son propre environnement :

- Sur `feature/part-1` : `print("academy{t3@mw0rk_", end='')`
- Sur `feature/part-2` : `print("m@k3s_th3_dr3@m_", end='')`
- Sur `feature/part-3` : `print("w0rk_f92d3827}")`

---

### 🚩 Étape 3 : Fusion et résolution de conflits

L'objectif est de regrouper le travail de l'équipe sur la branche `main`. On fusionne la première branche sans encombre avec `git merge feature/part-1`.  
Cependant, lorsqu'on tente de fusionner `feature/part-2` et `feature/part-3`, Git rencontre des **conflits de fusion (Merge conflicts)** car les modifications touchent les mêmes lignes du fichier `flag.py`.

Comme le rappelle l'indice du challenge, les conflits peuvent être délicats et il est conseillé d'utiliser un éditeur de texte (comme `nano`, `emacs` ou `vim`). On ouvre donc `flag.py` avec `vi` pour résoudre le conflit manuellement en supprimant les marqueurs Git (`<<<<<<< HEAD`, `=======`, `>>>>>>>`) et en alignant les trois instructions `print()`.

Une fois le fichier nettoyé, on l'exécute avec Python :

```bash
python flag.py
```

Le programme assemble et affiche le flag complet !  
**Flag :** `academy{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_f92d3827}`

---

### 💡 Key Takeaways / Notions retenues

- **Branches Git :** Le développement collaboratif implique souvent de travailler sur des branches parallèles (feature branches) pour isoler les nouvelles fonctionnalités avant de les intégrer au projet principal.
- **Résolution de conflits :** Lors d'un merge, si deux branches modifient la même partie d'un fichier, Git signale un conflit de fusion. Il faut alors éditer le fichier manuellement pour choisir quelles modifications conserver et retirer les balises de conflit générées par Git.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Collaborative Development
- **Platform / Event:** picoCTF 2024
- **Author:** Jeffery John
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "My team has been working very hard on new features for our flag printing program! I wonder how they'll work together? You can download the challenge files here: challenge.zip"[cite: 13]

---

### 🔍 Step 1: Repository & Branch Exploration

After downloading and extracting the archive, we enter the `drop-in` directory containing a `flag.py` file and a hidden Git repository. Reading the initial `flag.py` file only reveals a single print statement: `print("Printing the flag...")`.

The first challenge hint points us toward using the `git branch -a` command to check the available branches. Running this command reveals three distinct feature branches alongside the main branch:

- `feature/part-1`
- `feature/part-2`
- `feature/part-3`

---

### 🛠️ Step 2: Inspecting Parallel Development

By using the `git checkout` command to switch between branches, we discover that the team has split the flag across their respective workspaces. Checking the contents of flag.py in each branch reveals:

- On `feature/part-1: print("academy{t3@mw0rk_", end='')`
- On `feature/part-2: print("m@k3s_th3_dr3@m_", end='')`
- On `feature/part-3: print("w0rk_f92d3827}")`

---

### 🚩 Step 3: Merging & Conflict Resolution

Our goal is to combine the team's code into the `main` branch. We successfully merge the first branch using `git merge feature/part-1`.  
However, when we try to merge `feature/part-2` and `feature/part-3`, Git throws Merge conflicts because multiple branches modified the exact same lines in `flag.py`.

As the challenge hint suggests, merge conflicts can be tricky and it's best to use a text editor (like `nano`, `emacs`, or `vim`) to fix them. We open `flag.py` using `vi` and manually resolve the conflicts by deleting Git's injected conflict markers (`<<<<<<< HEAD`, `=======`, `>>>>>>>`) and stacking the three print statements properly.

Once the file is cleaned up and saved, we run it:

```Bash
python flag.py
The program successfully pieces together the full string and outputs the flag!
```

**Flag:** `academy{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_f92d3827}`

---

### 💡 Key Takeaways

- **Git Branches:** Collaborative development frequently relies on parallel branches (feature branches) so developers can work on new features in isolation before combining their work.
- **Merge Conflict Resolution:** When merging branches that alter the exact same lines of code, Git will stop the process and generate a merge conflict. Developers must then open the affected files, manually decide which code to keep, and remove the conflict markers before completing the commit.
