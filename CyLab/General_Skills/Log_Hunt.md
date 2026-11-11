# Write-Up : Log Hunt

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Log Hunt
- **Plateforme / Événement :** picoMini by CMU-Africa
- **Auteur :** Yahaya Meddy
- **Catégorie :** General Skills
- **Difficulté :** Easy

---

### 📝 Description

> _"Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag? Download the logs and figure out the full flag from the fragments."_

---

### 🔍 Étape 1 : Exploration du fichier journal (Log)

On télécharge le fichier journal `server.log`. En tentant une ouverture initiale avec un éditeur graphique tel que `mousepad`, on constate que le fichier est très volumineux.

On passe donc par le terminal Linux et la commande `grep` pour rechercher des expressions cibles comme `academy` :

```bash
cat server.log | grep academy
```

**Observation :**
On repère plusieurs entrées de journal contenant le motif INFO FLAGPART: `academy{us3_`.

### 🛠️ Étape 2 : Extraction et filtrage des fragments du Flag

Pour récupérer l'ensemble des morceaux du flag dissimulés à travers le fichier de log, on extrait toutes les lignes contenant le mot-clé FLAGPART :

```Bash
cat server.log | grep FLAGPART
```

Résultat de la recherche :

```Plaintext
[1990-08-09 10:00:10] INFO FLAGPART: academy{us3_
[1990-08-09 10:02:55] INFO FLAGPART: y0urlinux_
[1990-08-09 10:05:54] INFO FLAGPART: sk1lls_
[1990-08-09 10:10:54] INFO FLAGPART: cedfa5fb}
...
```

En analysant la chronologie des horodatages (timestamps), on identifie les 4 fragments distincts qui composent le flag complet :

1-`academy{us3_`  
2-`y0urlinux_`  
4-`sk1lls_`  
5-`cedfa5fb}`

### 🚩 Étape 3 : Assemblage et obtention du Flag

On concatène chronologiquement les fragments isolés pour reconstituer la chaîne finale.

**Flag :** `academy{us3_y0urlinux_sk1lls_cedfa5fb}`

### 💡 Key Takeaways / Notions retenues

- **Traitement de fichiers volumineux en CLI :** L'utilisation d'outils en ligne de commande comme grep évite de surcharger la mémoire système lors du traitement de gros fichiers journaux.

- **Analyse de logs et motifs (Pattern Matching) :** Filtrer un fichier de log par des mots-clés spécifiques (FLAGPART, INFO) permet d'isoler rapidement des morceaux d'information disséminés ou dupliqués.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Log Hunt
- **Platform / Event:** picoMini by CMU-Africa
- **Author:** Yahaya Meddy
- **Category:** General Skills
- **Difficulty:** Easy

---

### 📝 Description

> "Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag? Download the logs and figure out the full flag from the fragments."

---

### 🔍 Step 1: Log File Inspection

We download the server.log file provided in the challenge. Attempting to open the log file in a GUI text editor like mousepad fails to perform efficiently due to the large file size.

We pivot to the Linux terminal using grep to scan for target keyphrases such as academy:

```Bash
cat server.log | grep academy
```

**Observation:**
We observe multiple log entries formatted as INFO FLAGPART: `academy{us3_`.

### 🛠️ Step 2: Extracting & Filtering Flag Fragments

To isolate all scattered fragments across the log file, we filter for lines containing FLAGPART:

```Bash
cat server.log | grep FLAGPART
```

Filtered Log Stream Output:

```Plaintext
[1990-08-09 10:00:10] INFO FLAGPART: academy{us3_
[1990-08-09 10:02:55] INFO FLAGPART: y0urlinux_
[1990-08-09 10:05:54] INFO FLAGPART: sk1lls_
[1990-08-09 10:10:54] INFO FLAGPART: cedfa5fb}
...
```

By following the chronological sequence of the log timestamps, we extract the four unique ordered fragments:  
1-`academy{us3_`  
2-`y0urlinux_`  
3-`sk1lls_`  
4-`cedfa5fb}`

### 🚩 Step 3: Flag Assembly & Retrieval

We concatenate the ordered fragments to reconstruct the original flag.

**Flag:** `academy{us3_y0urlinux_sk1lls_cedfa5fb}`

### 💡 Key Takeaways

- **CLI Log Processing:** Command-line utilities like grep allow efficient searching through oversized log files without GUI editor overhead.

- **Pattern Matching & Log Analysis:** Filtering log streams using specific keywords (FLAGPART) isolates fragmented and duplicated string segments across timestamps.
