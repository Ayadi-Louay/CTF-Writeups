# Write-Up : Password Profiler

## 🇫🇷 Version Française

### 📋 Informations du Challenge

* **Nom du challenge :** Password Profiler

* **Plateforme / Événement :** picoCTF 2026

* **Auteur :** Yahaya Meddy

* **Catégorie :** General Skills / OSINT

* **Difficulté :** Easy

### 📝 Description

> *"We intercepted a suspicious file from a system, but instead of the password itself, it only contains its SHA-1 hash. Using OSINT techniques, you are provided with personal details about the target. Your task is to leverage this information to generate a custom password list and recover the original password by matching its hash. Download the following files: userinfo, hash, check_password."*

### 🔍 Étape 1 : Analyse des fichiers et choix de l'outil

En examinant le répertoire de travail, on trouve les fichiers fournis pour le challenge :

```
ls
check_password.py  cupp  hash.txt  userinfo.txt

```

Le fichier `userinfo.txt` contient les informations personnelles de la cible. Comme suggéré dans l'indice du challenge, on utilise l'outil **CUPP** (*Common User Passwords Profiler*) pour générer un dictionnaire personnalisé basé sur ces données d'ingénierie sociale / OSINT.

### 🛠️ Étape 2 : Profilage et génération du dictionnaire

1. **Exécution de CUPP :**
   On se déplace dans le répertoire de CUPP et on génère un dictionnaire interactif en renseignant les détails contenus dans `userinfo.txt` :

```
cd cupp
python3 cupp.py -i

```

CUPP génère le dictionnaire `alice.txt` contenant toutes les combinaisons possibles.

2. **Préparation de la liste de mots de passe :**
   On déplace et renomme ce dictionnaire vers le dossier parent sous le nom `passwords.txt` pour qu'il soit accessible par le script de vérification :

```
mv alice.txt /home/kali/Downloads/passwords.txt
cd ..

```

### 🚩 Étape 3 : Brute-force local et obtention du Flag

On lance ensuite le script Python `check_password.py` qui va comparer le hash SHA-1 présent dans `hash.txt` avec les mots de passe générés dans `passwords.txt` :

```
python check_password.py

```

**Résultat du terminal :**

```
Password found: academy{aliceaj7515}

```

**Flag :** `academy{aliceaj7515}`

### 💡 Key Takeaways / Notions retenues

* **Social Engineering & Password Profiling :** Les utilisateurs créent très souvent leurs mots de passe à partir d'informations personnelles (prénom, date de naissance, nom de famille, pseudos).

* **Utilisation de CUPP :** CUPP (*Common User Passwords Profiler*) permet de générer automatiquement des dictionnaires ciblés et très efficaces lors d'un test d'intrusion ou d'un défi OSINT.

* **Attaque par dictionnaire sur Hash SHA-1 :** Lorsqu'un hash simple (sans sel) est intercepté, une attaque par dictionnaire basée sur des règles de profilage est bien plus rapide et efficace qu'un brute-force complet.

## 🇬🇧 English Version

### 📋 Challenge Info

* **Challenge Name:** Password Profiler

* **Platform / Event:** picoCTF 2026

* **Author:** Yahaya Meddy

* **Category:** General Skills / OSINT

* **Difficulty:** Easy

### 📝 Description

> *"We intercepted a suspicious file from a system, but instead of the password itself, it only contains its SHA-1 hash. Using OSINT techniques, you are provided with personal details about the target. Your task is to leverage this information to generate a custom password list and recover the original password by matching its hash. Download the following files: userinfo, hash, check_password."*

### 🔍 Step 1: Inspecting Challenge Files & Tool Selection

Checking the working directory reveals the challenge resources:

```
ls
check_password.py  cupp  hash.txt  userinfo.txt

```

The `userinfo.txt` file contains personal profiling data regarding the target. Following the challenge hint, we leverage **CUPP** (*Common User Passwords Profiler*) to generate a customized wordlist based on these OSINT details.

### 🛠️ Step 2: User Profiling & Wordlist Generation

1. **Running CUPP:**
   We navigate into the CUPP directory and execute the interactive profiling command, filling in the personal details extracted from `userinfo.txt`:

```
cd cupp
python3 cupp.py -i

```

CUPP outputs the generated wordlist file named `alice.txt`.

2. **Moving the Wordlist:**
   We rename and move the dictionary file to the parent directory as `passwords.txt` so the cracking script can read it:

```
mv alice.txt /home/kali/Downloads/passwords.txt
cd ..

```

### 🚩 Step 3: Local Hash Matching & Flag Retrieval

We run the provided verification script `check_password.py` to match the target SHA-1 hash in `hash.txt` against our newly generated wordlist `passwords.txt`:

```
python check_password.py

```

**Terminal Output:**

```
Password found: academy{aliceaj7515}

```

**Flag:** `academy{aliceaj7515}`

### 💡 Key Takeaways

* **Targeted Password Profiling:** Users frequently craft passwords using combinations of personal identifiers (first names, birthdates, nicknames, pet names).

* **CUPP Utility:** CUPP (*Common User Passwords Profiler*) is a specialized tool for generating targeted dictionaries using OSINT and social engineering data.

* **SHA-1 Dictionary Cracking:** When unsalted hashes are exposed, targeted dictionary attacks driven by user profiling offer a significantly faster path to recovery than blind brute-force attacks.