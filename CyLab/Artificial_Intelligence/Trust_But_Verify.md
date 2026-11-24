# Write-Up : Trust But Verify

---

## 🇫🇷 Version Française

### 📋 Informations du Challenge

- **Nom du challenge :** Trust But Verify
- **Plateforme / Événement :** AI Foundations I
- **Auteur :** LT 'syreal' Jones
- **Catégorie :** Artificial Intelligence
- **Difficulté :** Easy

---

### 📝 Description

> _"Play through an AI ethics interactive fiction where confident AI outputs can be wrong, subtly wrong, or almost-right. Verify claims, code, and citations to learn practical habits for safe AI-assisted work. Connect with netcat: `$ nc xebec.cylabacademy.net 32764`"_

Les indices précisent que le jeu fait fréquemment des pauses (il faut appuyer sur `Entrée` à chaque invite) et que le flag s'affiche vers la fin de l'histoire.

---

### 🔍 Étape 1 : Connexion à l'instance via Netcat

Pour démarrer cette fiction interactive sur l'éthique de l'IA, on se connecte au serveur distant depuis un terminal à l'aide de la commande `netcat` fournie dans la description :

```bash
nc xebec.cylabacademy.net 32764
```

L'histoire met en scène Ren, un lycéen utilisant son assistant IA nommé ARIA pour rédiger une proposition de projet scientifique.

### 🛠️ Étape 2 : Résolution des trois scénarios (Vérification systématique)

Tout au long du récit, ARIA génère des contenus plausibles mais contenant des erreurs subtiles. Pour progresser efficacement, il faut adopter le réflexe de toujours vérifier les informations :

**Scène 1 — La statistique (Hallucination) :** ARIA affirme qu'un rapport de l'UNEP de 2022 mentionne plus de 500 millions de tonnes métriques de plastique dans les océans. En choisissant l'option B (demander le lien exact de la source), ARIA admet avoir inventé une référence plausible qui n'existe pas (une hallucination).

**Scène 2 — Le code Python (Erreur logique) :** ARIA propose un script de calcul de moyenne contenant un `+ 1` injustifié (`sum(data) / len(years) + 1`). En choisissant l'option B (lire attentivement le code avant de l'exécuter), on repère et corrige cette anomalie pour obtenir la vraie moyenne (`10.83`).

**Scène 3 — La citation académique (Presque juste) :** ARIA cite une étude du Dr Heather Leslie de la Vrije Universiteit Amsterdam de 2021 confirmant la présence de microplastiques dans le sang humain. En choisissant l'option B (vérifier malgré tout), on découvre que l'étude est réelle mais date de 2022 et que ses résultats sont préliminaires, et non définitivement confirmés.

---

### 🚩 Étape 3 : Fin de l'histoire et obtention du Flag

Une fois le projet soumis et les bonnes pratiques de vérification validées, ARIA conclut l'échange et affiche directement le flag dans le terminal.  
**Flag :** `academy{7ru57_15_34rn3d_a5b4c2e0}`

---

### 💡 Key Takeaways / Notions retenues

- **Hallucinations des IA :** Les modèles de langage peuvent générer avec assurance des statistiques ou des références bibliographiques totalement inventées. Il faut toujours exiger et vérifier les sources primaires.
- **Relecture de code obligatoire :** Ne jamais exécuter aveuglément un script généré par une IA. Une erreur logique silencieuse (comme un `+ 1` arbitraire) produit un résultat en apparence cohérent mais faux.
- **Le piège du « presque juste » :** Les réponses les plus trompeuses sont celles qui mélangent des faits réels (vrai chercheur, vraie université) à des détails inexacts (mauvaise année, surinterprétation des conclusions).

## 🇬🇧 English Version

### 📋 Challenge Info

- **Challenge Name:** Trust But Verify
- **Platform / Event:** AI Foundations I
- **Author:** LT 'syreal' Jones
- **Category:** Artificial Intelligence
- **Difficulty:** Easy

---

### 📝 Description

> "Play through an AI ethics interactive fiction where confident AI outputs can be wrong, subtly wrong, or almost-right. Verify claims, code, and citations to learn practical habits for safe AI-assisted work. Connect with netcat: $ nc xebec.cylabacademy.net 32764"

The hints note that the game pauses frequently (requiring you to press `Enter` at each prompt) and that the flag is printed near the end of the story.

---

### 🔍 Step 1: Connecting to the Instance via Netcat

To start the interactive fiction, we connect to the remote server from a terminal using the provided `netcat` command:

```Bash
nc xebec.cylabacademy.net 32764
```

The narrative follows Ren, a high school junior using an AI study companion named ARIA to prepare a science fair proposal.

---

### 🛠️ Step 2: Navigating the Three Scenarios (Systematic Verification)

Throughout the story, ARIA generates confident outputs containing subtle flaws. Applying a "trust but verify" mindset solves each scene:

**Scene 1 — The Statistic (Hallucination):** ARIA claims a 2022 UNEP report states that over 500 million metric tons of plastic enter the oceans annually. Selecting option B (ask for the exact source link) prompts ARIA to admit it hallucinated a plausible-sounding citation that does not exist.

**Scene 2 — The Code (Logic Bug):** ARIA generates a Python script to compute an average, sneaking in an arbitrary `+ 1` (`sum(data) / len(years) + 1`). Selecting option B (read through it carefully before running) catches the bug and restores the accurate average (`10.83`).

**Scene 3 — The Citation (Almost-Right):** ARIA cites a 2021 study by Dr. Heather Leslie at Vrije Universiteit Amsterdam confirming microplastics in human blood. Selecting option B (verify it anyway) reveals that while the researcher and university are real, the study was published in 2022 and its findings were preliminary rather than confirmed.

---

### 🚩 Step 3: Completing the Story & Flag Retrieval

After submitting the corrected proposal and completing the dialogue, ARIA prints the flag directly in the terminal output.  
**Flag:** `academy{7ru57_15_34rn3d_a5b4c2e0}`

---

### 💡 Key Takeaways

- **AI Hallucinations:** Language models can confidently fabricate statistics and citations. Always demand and independently verify primary sources.
- **Always Review Generated Code:** Never run AI-generated code blindly. Silent logic errors (such as an unexplained `+ 1`) can produce plausible-looking yet incorrect outputs.
- **Beware of "Almost-Right" Outputs:** The hardest errors to catch combine real entities (valid researchers and institutions) with subtle factual distortions (wrong dates or overstated conclusions).
