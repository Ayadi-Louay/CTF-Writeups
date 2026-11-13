# Write-Up : Binary Search

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Binary Search
- **Plateforme / Événement :** picoCTF 2024
- **Auteur :** Jeffery John
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses."_

---

### 🔍 Étape 1 : Connexion SSH au serveur de jeu

On se connecte à l'instance distante via SSH avec les identifiants fournis dans l'énoncé :

```bash
ssh -p 11960 ctf-player@xebec.cylabacademy.net
```

Dès la connexion établie, le programme interactif démarre automatiquement et demande de deviner un nombre secret compris entre 1 et 1000 en un maximum de 10 tentatives.

### 🛠️ Étape 2 : Application de l'algorithme de recherche dichotomique (Binary Search)

Pour garantir de trouver le nombre cible parmi $1000$ possibilités en au plus $\lceil \log_2(1000) \rceil = 10$ essais, on applique la méthode de recherche dichotomique en divisant systématiquement l'intervalle de recherche par deux à chaque étape :

```Plaintext
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Lower! Try again.
Enter your guess: 250
Lower! Try again.
Enter your guess: 125
Lower! Try again.
Enter your guess: 62
Lower! Try again.
Enter your guess: 31
Lower! Try again.
Enter your guess: 16
Lower! Try again.
Enter your guess: 8
Lower! Try again.
Enter your guess: 4
Lower! Try again.
Enter your guess: 2
Congratulations! You guessed the correct number: 2
```

### 🚩 Étape 3 : Obtention du Flag

Au 9ᵉ essai, le nombre secret 2 est validé et le serveur affiche le flag avant de fermer la session SSH :  
**Flag :** academy{g00d_gu355_7fa0f5da}

### 💡 Key Takeaways / Notions retenues

- **Recherche dichotomique (Binary Search) :** Cet algorithme permet de réduire l'espace de recherche de moitié à chaque itération, offrant une complexité logarithmique de $\mathcal{O}(\log_2 n)$ (soit $10$ essais maximum pour $1000$ valeurs).

- **Exécution automatique à la connexion SSH :** Un serveur SSH peut être configuré (via ForceCommand ou un shell personnalisé) pour lancer directement un programme interactif dès l'authentification de l'utilisateur.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Binary Search
- **Platform / Event:** picoCTF 2024
- **Author:** Jeffery John
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses."

---

### 🔍 Step 1: SSH Connection to the Game Server

We connect to the remote instance via SSH using the provided credentials:

```Bash
ssh -p 11960 ctf-player@xebec.cylabacademy.net
```

Immediately upon authentication, the interactive shell program launches and prompts us to guess a secret integer between 1 and 1000 within 10 attempts.

### 🛠️ Step 2: Applying the Binary Search Algorithm

To guarantee finding the target number among $1000$ possibilities within $\lceil \log_2(1000) \rceil = 10$ guesses[cite: 12], we apply Binary Search by repeatedly selecting the midpoint of the remaining valid range:

```Plaintext
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Lower! Try again.
Enter your guess: 250
Lower! Try again.
Enter your guess: 125
Lower! Try again.
Enter your guess: 62
Lower! Try again.
Enter your guess: 31
Lower! Try again.
Enter your guess: 16
Lower! Try again.
Enter your guess: 8
Lower! Try again.
Enter your guess: 4
Lower! Try again.
Enter your guess: 2
Congratulations! You guessed the correct number: 2
```

### 🚩 Step 3: Flag Retrieval

On the 9th guess, the secret number 2 is confirmed and the server prints the flag before closing the SSH connection:  
**Flag:** `academy{g00d_gu355_7fa0f5da}`

### 💡 Key Takeaways

- **Binary Search Efficiency:** By halving the search space at each step, binary search achieves $\mathcal{O}(\log_2 n)$ time complexity, requiring at most $10$ guesses for $1000$ sorted possibilities.

- **Restricted SSH Environments:** SSH services can execute specific interactive applications immediately upon login rather than spawning a standard interactive shell.
