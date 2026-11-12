# Write-Up : FANTASY CTF

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** FANTASY CTF
- **Plateforme / Événement :** picoCTF 2025
- **Auteur :** syreal
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Play this short game to get familiar with terminal applications and some of the most important rules in scope for picoCTF."_

---

### 🔍 Étape 1 : Lancement de l'instance et connexion Netcat

On clique sur le bouton **Launch Instance** pour générer les hôtes et ports distants de connexion.

On se connecte au serveur d'application en ligne de commande à l'aide de l'outil **Netcat** (`nc`) :

```bash
nc <host> <port>
```

(Exemple : nc chatelaine.cylabacademy.net 12253)

### 🛠️ Étape 2 : Navigation dans le jeu interactif et choix éthiques

Une fois connecté, l'application lance une simulation textuelle interactive sous forme d'histoire. Tout au long de la partie, le programme demande d'effectuer des choix matérialisés sous la forme [a/b/c] :

1-À la question sur l'inscription aux CTF, on sélectionne l'option conforme aux règles de la plateforme (c : s'inscrire avec un seul compte personnel et privé).

2-Aux questions suivantes concernant l'obtention du flag, on choisit de jouer au jeu normalement plutôt que d'essayer de chercher les flags d'autres participants.

### 🚩 Étape 3 : Obtention du Flag

Une fois l'ensemble des étapes du scénario franchies en respectant les règles d'éthique du CTF, le programme affiche le flag final à l'écran.

**Flag :** `academy{m1113n1um_3d1710n_07462474}` (ou selon l'instance attribuée)

### 💡 Key Takeaways / Notions retenues

- **Utilisation de Netcat (nc) :** Netcat est un outil CLI essentiel en cybersécurité pour établir des connexions TCP brutes avec des services distants en mode interactif.

- **Règles d'engagement CTF :** Respecter les règles éthiques des compétitions CTF (compte unique, non-partage de flags ou de secrets, jeu équitable).

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** FANTASY CTF
- **Platform / Event:** picoCTF 2025
- **Author:** syreal
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "Play this short game to get familiar with terminal applications and some of the most important rules in scope for picoCTF."

---

### 🔍 Step 1: Instance Launch & Netcat Connection

We click Launch Instance to generate the remote host and port credentials.

We connect to the challenge server using the Netcat (nc) utility in the terminal:

```Bash
nc <host> <port>
```

(Example: nc chatelaine.cylabacademy.net 12253)

### 🛠️ Step 2: Interactive Story Navigation & Ethical Choices

Upon connection, a terminal-based interactive simulation launches. Prompts require selecting choices formatted as [a/b/c]:

1-When asked about account creation rules, we choose option c (registering a single personal account).

2-For subsequent gameplay choices, we opt to solve the challenge fairly instead of seeking leaked flags.

### 🚩 Step 3: Flag Retrieval

Completing the interactive storyline reveals the final flag at the conclusion of the simulation.

**Flag:** `academy{m1113n1um_3d1710n_07462474}` (or instance-specific variant)

### 💡 Key Takeaways

- **Netcat (nc) Basics:** Netcat is a fundamental command-line utility used to open raw TCP network socket connections with interactive remote services.

- **CTF Rules of Engagement:** Understanding and adhering to standard CTF competition rules (single-account registration, fair gameplay, and no flag sharing).
