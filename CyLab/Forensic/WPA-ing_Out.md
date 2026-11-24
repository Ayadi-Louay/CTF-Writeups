# Write-Up : WPA-ing Out

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** WPA-ing Out
- **Auteur :** MistressVampy
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

### 📝 Description

> _"I thought that my password was super-secret, but it turns out that passwords passed over the AIR can be CRACKED, especially if I used the same wireless network password as one in the rockyou.txt credential dump. Use this 'pcap file' and the rockyou wordlist. The flag should be entered in the academy{XXXXXX} format."_

---

### 🔍 Étape 1 : Analyse de la capture réseau avec Wireshark

La première étape consiste à télécharger le fichier de capture réseau (`wpa-ing_out.pcap`) fourni dans l'énoncé. En l'ouvrant avec **Wireshark** (comme suggéré par le premier indice), on observe que la majorité des paquets capturés appartiennent au protocole sans fil **IEEE 802.11** (Wi-Fi).

Ce type de capture réseau sans fil contient généralement un _4-way handshake_ WPA/WPA2 capturé lors de la connexion d'un client au point d'accès, ce qui permet de tenter un cassage du mot de passe hors ligne.

---

### 🛠️ Étape 2 : Cassage du mot de passe avec Aircrack-ng

L'énoncé précise que le mot de passe utilisé fait partie de la célèbre liste `rockyou.txt`, et le deuxième indice recommande d'utiliser l'outil **Aircrack-ng** pour analyser le fichier `.pcap` et retrouver le mot de passe.

On lance donc une attaque par dictionnaire dans le terminal avec la commande suivante :

```bash
aircrack-ng -w rockyou.txt wpa-ing_out.pcap
```

L'outil teste les mots de passe de la wordlist contre le handshake capturé et trouve rapidement la correspondance :

```Plaintext
KEY FOUND! [ mickeymouse ]
```

---

### 🚩 Étape 3 : Formatage et obtention du Flag

Une fois le mot de passe du réseau sans fil (`mickeymouse`) récupéré, il ne reste plus qu'à l'encadrer avec le format exigé dans la description du challenge (`academy{XXXXXX}`).  
**Flag :** `academy{mickeymouse}`

---

### 💡 Key Takeaways / Notions retenues

- **Analyse de trafic Wi-Fi (IEEE 802.11) :** Wireshark permet d'inspecter les trames sans fil 802.11 et de repérer les échanges d'authentification (comme le EAPOL 4-way handshake utilisé par WPA/WPA2).
- **Attaque par dictionnaire hors ligne (`aircrack-ng`) :** La robustesse d'un réseau Wi-Fi protégé par WPA/WPA2 Personal dépend directement de la complexité de sa phrase secrète. Si un attaquant capture le handshake, il peut tester des millions de mots de passe hors ligne avec `aircrack-ng` et `rockyou.txt` sans jamais envoyer de trafic supplémentaire sur le réseau.

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** WPA-ing Out
- **Author:** MistressVampy
- **Category:** Forensics
- **Difficulty:** Easy

---

### 📝 Description

> "I thought that my password was super-secret, but it turns out that passwords passed over the AIR can be CRACKED, especially if I used the same wireless network password as one in the rockyou.txt credential dump. Use this 'pcap file' and the rockyou wordlist. The flag should be entered in the academy{XXXXXX} format."

---

### 🔍 Step 1: Analyzing the Packet Capture with Wireshark

The first step is to download the provided packet capture file (`wpa-ing_out.pcap`). Opening it in Wireshark (as recommended by the first hint) reveals that the vast majority of the captured traffic uses the IEEE 802.11 wireless protocol.

Wireless packet captures like this typically contain a WPA/WPA2 4-way handshake recorded when a device connects to an access point, allowing us to perform an offline password-cracking attack.

---

### 🛠️ Step 2: Cracking the Password with Aircrack-ng

The prompt mentions that the wireless password is included in the `rockyou.txt` wordlist, and the second hint points directly to using Aircrack-ng to crack the password from the `.pcap` file.

We run a dictionary attack in the terminal using the following command:

```Bash
aircrack-ng -w rockyou.txt wpa-ing_out.pcap
```

Aircrack-ng tests the passwords from the wordlist against the captured handshake and quickly identifies the wireless key:

```Plaintext
KEY FOUND! [ mickeymouse ]
```

---

### 🚩 Step 3: Formatting and Flag Retrieval

With the wireless password (`mickeymouse`) recovered, we wrap it in the required flag format specified in the challenge description (`academy{XXXXXX}`).  
**Flag:** `academy{mickeymouse}`

---

### 💡 Key Takeaways

- **Wi-Fi Traffic Analysis (IEEE 802.11):** Wireshark allows analysts to inspect 802.11 wireless frames and identify authentication exchanges (such as the EAPOL 4-way handshake used in WPA/WPA2).
- **Offline Dictionary Attacks (`aircrack-ng`):** The security of a WPA/WPA2 Personal network relies heavily on the strength of its passphrase. Once an attacker captures a handshake, they can brute-force or dictionary-attack the password completely offline using tools like `aircrack-ng` and common wordlists like `rockyou.txt`.
