# Write-Up : vault-door-training

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** vault-door-training[cite: 17]
- **Plateforme / Événement :** picoCTF 2019[cite: 17]
- **Auteur :** Mark E. Haase[cite: 17]
- **Catégorie :** Reverse Engineering[cite: 17]
- **Difficulté :** Easy[cite: 17]

---

### 📝 Description

> _"Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: VaultDoorTraining.java"_[cite: 17]

---

### 🔍 Étape 1 : Téléchargement et inspection du code Java

On télécharge le fichier source Java `VaultDoorTraining.java` fourni dans la description du défi[cite: 17]. On affiche ensuite son contenu dans le terminal ou un éditeur de texte[cite: 17, 18] :

```bash
cat VaultDoorTraining.java
```

---

### 🛠️ Étape 2 : Analyse de la méthode de vérification

En examinant le code source Java, on repère la méthode `main` qui extrait le mot de passe saisi entre le préfixe du flag et l'accolade fermante[cite: 18] :

```java
String input = userInput.substring("academy{".length(), userInput.length()-1);[cite: 18]
```

On inspecte ensuite la méthode `checkPassword` chargée de valider l'entrée[cite: 18] :

```java
public boolean checkPassword(String password) {
    return password.equals("w4rm1ng_Up_w1tH_jAv4_c02db1ca2a4");[cite: 18]
}
```

**Observation :**
Le mot de passe recherché est directement inscrit en texte brut (_hardcoded_) au sein de la condition de comparaison[cite: 18].

---

### 🚩 Étape 3 : Assemblage du Flag

On associe le mot de passe extrait au format du flag (`academy{...}`) pour obtenir la solution complète[cite: 18] :

**Flag :** `academy{w4rm1ng_Up_w1tH_jAv4_c02db1ca2a4}`[cite: 18]

---

### 💡 Key Takeaways / Notions retenues

- Il ne faut jamais intégrer d'identifiants ou de secrets en texte brut (_hardcoding_) dans le code source d'une application.
- L'analyse statique du code source d'un binaire ou d'une application (Java, C, Python, etc.) permet souvent de repérer rapidement des clés d'accès ou des logiques de validation simplistes.

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** vault-door-training[cite: 17]
- **Platform / Event:** picoCTF 2019[cite: 17]
- **Author:** Mark E. Haase[cite: 17]
- **Category:** Reverse Engineering[cite: 17]
- **Difficulty:** Easy[cite: 17]

---

### 📝 Description

> _"Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: VaultDoorTraining.java"_[cite: 17]

---

### 🔍 Step 1: Downloading & Inspecting the Source Code

We download the `VaultDoorTraining.java` source file provided in the challenge prompt[cite: 17]. We display its content using the terminal[cite: 17, 18]:

```bash
cat VaultDoorTraining.java
```

---

### 🛠️ Step 2: Code Inspection & Validation Logic

While reviewing the Java code, we locate the `main` method stripping the flag wrapper[cite: 18]:

```java
String input = userInput.substring("academy{".length(), userInput.length()-1);[cite: 18]
```

Next, we inspect the `checkPassword` verification function[cite: 18]:

```java
public boolean checkPassword(String password) {
    return password.equals("w4rm1ng_Up_w1tH_jAv4_c02db1ca2a4");[cite: 18]
}
```

**Observation:**
The secret vault key is stored in plain text directly inside the string equality comparison method[cite: 18].

---

### 🚩 Step 3: Flag Reassembly

We wrap the recovered password string inside the target flag wrapper (`academy{...}`)[cite: 18]:

**Flag:** `academy{w4rm1ng_Up_w1tH_jAv4_c02db1ca2a4}`[cite: 18]

---

### 💡 Key Takeaways

- Hardcoding sensitive credentials or secret keys directly inside application source code exposes them to basic static code analysis.
- Performing static inspection on client-side code is a foundational reverse engineering technique for uncovering validation routines.
