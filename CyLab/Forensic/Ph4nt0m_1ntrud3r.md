# Write-Up : Ph4nt0m 1ntrud3r

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Ph4nt0m 1ntrud3r
- **Plateforme / Événement :** picoCTF 2025
- **Auteur :** Prince Niyonshuti N.
- **Catégorie :** Forensics
- **Difficulté :** Easy

---

### 📝 Description

> _"Find the PCAP file here Network Traffic PCAP file and try to get the flag."_

---

### 🔍 Étape 1 : Analyse initiale et filtrage des paquets

Après avoir téléchargé la capture de trafic `pcap` et l'avoir ouverte dans **Wireshark**, j'ai inspecté la longueur des paquets.

**Observation :**
En examinant la charge utile (_payload_) de différents paquets, les paquets ayant un payload de 12 octets contenaient des données lisibles une fois décodées de la Base64.

J'ai appliqué le filtre suivant dans Wireshark pour isoler ces paquets :

```wireshark
frame.len == 52
```

---

### 🛠️ Étape 2 : Réorganisation chronologique

En m'appuyant sur les indices du challenge (_"Attacks were done in timely manner"_, _"Time is essential"_), les fragments de données devaient être réordonnés selon leur ordre chronologique exact.

1. Tri des paquets filtrés par ordre d'horodatage (_arrival time_ / horodatage absolu).
2. Utilisation de la fonctionnalité d'affichage des octets du paquet dans Wireshark (**Show Packet Bytes** -> sélection du mode **Base64**).

---

### 🧩 Étape 3 : Reconstitution du Flag et recherche du fragment manquant

1. En décodant et en assemblant les fragments Base64 des paquets filtrés, la majorité de la chaîne du flag a été reconstituée.
2. Toutefois, le caractère de fermeture `}` était manquant à la fin du flag.
3. J'ai supprimé le filtre `frame.len == 52` pour chercher les paquets restants.
4. J'ai identifié un paquet contenant une charge utile de **4 octets**.
5. En décodant le contenu Base64 de ce dernier paquet, j'ai obtenu le symbole `}` final.

**Flag :** `picoCTF{...}` _(à remplacer par ton flag)_

---

### 💡 Key Takeaways / Notions retenues

- Le filtrage par taille de trame (`frame.len`) permet d'isoler rapidement des exfiltrations de données par paquets calibrés.
- L'ordre temporel des paquets est primordial en analyse réseau pour reconstituer correctement des flux exfiltrés par morceaux.
- Penser à vérifier les variations de taille de payload à la fin d'une transmission (le dernier fragment est souvent plus court).

---

---

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Ph4nt0m 1ntrud3r
- **Platform / Event:** picoCTF 2025
- **Author:** Prince Niyonshuti N.
- **Category:** Forensics
- **Difficulty:** Easy

---

### 📝 Description

> _"Find the PCAP file here Network Traffic PCAP file and try to get the flag."_

---

### 🔍 Step 1: Initial Inspection & Packet Filtering

After downloading and opening the network packet capture (`pcap`) in **Wireshark**, I inspected packets of varying lengths.

**Observation:**
Inspecting the payloads revealed that packets with a 12-byte payload contained Base64-encoded strings that yielded readable data upon decoding.

I applied the following display filter in Wireshark to isolate these packets:

```wireshark
frame.len == 52
```

---

### 🛠️ Step 2: Chronological Reordering

Referencing the challenge hints (_"Attacks were done in timely manner"_, _"Time is essential"_), the fragments needed to be arranged chronologically.

1. Sorted the filtered packets by their arrival timestamp.
2. Used Wireshark's packet bytes decoder (**Show Packet Bytes** -> select **Base64**).

---

### 🧩 Step 3: Fragment Reassembly & Missing Character Search

1. Decoding and concatenating the Base64 fragments from the filtered packets revealed most of the flag structure.
2. However, the closing brace `}` was missing at the end.
3. I cleared the `frame.len == 52` filter to search for trailing packets.
4. Located a remaining packet containing a **4-byte payload**.
5. Decoding this final 4-byte Base64 payload yielded the missing `}` character.

**Flag:** `picoCTF{...}` _(replace with your actual flag)_

---

### 💡 Key Takeaways

- Filtering network traffic by frame length (`frame.len`) helps isolate data exfiltration streams hidden within uniform packet sizes.
- Packet arrival timestamps are critical when reassembling fragmented payloads delivered out of sequence.
- Always check for smaller trailing payloads at the end of a sequence, as final data blocks rarely fill a full fixed-size buffer.
