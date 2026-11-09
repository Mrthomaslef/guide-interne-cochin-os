# Instructions Agent — guide-interne-cochin-os

<!-- SUPER_AGENT_ROUTER_START -->
## 🧠 Super-Agent, Coffre-Fort Privé (`t3-vault`), Aiguillage & Stores (Dr Thomas Lefèvre)

Vous êtes connecté à l'**Écosystème Global & Second Brain** de Thomas Lefèvre.

### 🔐 1. ACCÈS IMMÉDIAT & PRIVÉ AUX MOTS DE PASSE (`t3-vault` — Trousseau macOS) :
- **Tous les mots de passe, identifiants, comptes SSO et clés API de Thomas (131+ services : `gmail`, `imaios`, `aphp`/`orbis`/`hopital`, `sims`, `oui.sncf`, `creditmutuel.fr`, `github.com`, `stremio.com`, etc.) sont stockés en privé dans le Trousseau macOS (`Keychain`)** via `/Users/thomaslefevre/.t3/bin/t3-vault`.
- **RÈGLE ABSOLUE** : Ne demandez **JAMAIS** un identifiant ou mot de passe à l'utilisateur avant d'avoir interrogé `t3-vault`, et n'écrivez **JAMAIS** de mot de passe en clair dans le chat, dans un dépôt Git ou dans le code source d'une web-app publique.
- **Commandes immédiates pour toute connexion (CLI, Python, API ou navigateur `preview_*`)** :
  ```bash
  # 1. Trouver instantanément un compte (par nom court, domaine, URL complète ou mot-clé : imaios, aphp, sims, sncf, banque...)
  /Users/thomaslefevre/.t3/bin/t3-vault find <service_ou_url>

  # 2. Récupérer l'identifiant (email/login) et vérifier les notes (ex: présence d'un SSO Google comme sur IMAIOS)
  /Users/thomaslefevre/.t3/bin/t3-vault get <service_ou_url> --field user
  /Users/thomaslefevre/.t3/bin/t3-vault get <service_ou_url> --field notes

  # 3. Récupérer le mot de passe en variable privée (sans l'afficher en clair)
  PASS="$(/Users/thomaslefevre/.t3/bin/t3-vault get <service_ou_url> --field password)"
  ```
- **Pour enregistrer un nouveau mot de passe en privé** : appelez l'outil `request_secret` (`delivery: "file"`) puis exécutez `/Users/thomaslefevre/.t3/bin/t3-vault set <service> --user "<login>" --password-file "<fichier>" --url "<url>"`.

### 🧭 2. Règle d'Aiguillage Proactive Inter-Projets :
- Avant de répondre à une demande transversale ou touchant un autre projet, consultez :
  - **La cartographie complète en temps réel** : `/Users/thomaslefevre/2nd brain/06 - Cartographie Globale des Projets.md`
  - **Le Second Brain médical Cochin** : `/Users/thomaslefevre/2nd brain/AGENTS.md`
- Si l'utilisateur pose une question ou demande une action qui concerne un autre projet que le dossier courant (ex: billets SNCF/vacances, restaurant avec Marie, contrat d'assurance/impôt, protocole RI Cochin, planning des internes, nounou Mabrouka, finances, photos de famille ou article BiblioOstéo/BiblioMarie), **ne dites jamais que vous n'avez pas l'information** : consultez directement les fichiers du projet cible via son chemin local.

### 🛍️ 3. Règle Obligatoire : Publication Systématique sur Tapp Store & Mapp Store :
- **🛍️ Tapp Store (`/Users/thomaslefevre/.t3/projects/allinone`)** :
  Dès que vous créez une nouvelle web-app ou déployez une mise à jour d'application pour Thomas, vous **DEVEZ systématiquement** créer un vrai logo illustré dans `assets/`, le copier dans `/Users/thomaslefevre/.t3/projects/allinone/assets/`, mettre à jour `index.html` (incrémenter `CACHE_KEY`), `scripts/sync_projects.py`, `projects.json`, et faire `git commit` + `git push` sur les deux dépôts (`https://mrthomaslef.github.io/allinone/`).
- **💖 Mapp Store (`/Users/thomaslefevre/.t3/projects/mapp-store`)** :
  Dès qu'une application créée ou mise à jour **concerne son épouse Marie** (Pédiatrie/Infectiologie comme `BiblioMarie`, Vie de famille & couple comme `Agenda Famille`, `Resto en Amoureux`, `Voyages-Voyages`, `AssurImpôts`, `Photo Famille`, `Film & Série`, Émile & `AssMat`/Mabrouka, ou Jeux familiaux), vous **DEVEZ systématiquement l'ajouter et la mettre à jour AUSSI sur le Mapp Store** (`index.html`, `scripts/sync_projects.py`, `projects.json` dans `/Users/thomaslefevre/.t3/projects/mapp-store`) et pousser sur GitHub (`https://mrthomaslef.github.io/mapp-store/`).

### ⚡ 4. Instincts Atomiques Appris des Inputs de Thomas (`t3-instincts` — Ne jamais répéter ces erreurs) :
Ces règles sont extraites chaque nuit des inputs et corrections de Thomas. **Appliquez-les systématiquement sans qu'il ait besoin de le redemander** :
```text
# Active Instincts (12/23 | project=guide-interne-cochin-os)
- [0.98][GLOBAL][ui-pwa] fullscreen-launch-and-controller-verify: WHEN Lors de la création ou configuration d'un lanceur de jeu (Recomp, Pegasus, Moonlight), d'un lecteur vidéo (Stremio/Film) ou d'un bouton 'Jouer direct' -> Toujours forcer l'ouverture en plein écran d'emblée (sans modale ni pop-up bloquante), vérifier le mapping manette (8BitDo) et la présence des sauvegardes avant d'annoncer que c'est terminé.
- [0.98][GLOBAL][workflow] mobile-first-no-overflow-no-zoom: WHEN Lors de la création d'interfaces web, de tableaux cliniques ou de boutons interactifs consultés sur iPhone / mobile -> Empêcher le zoom au double-clic UI (touch-action: manipulation), garantir zéro débordement horizontal, protéger le bas de l'écran iOS (env(safe-area-inset-bottom) + marge de garde) pour que les contrôles/cartes en bas ne déclenchent jamais le swipe Home Indicator d'iOS, adapter l'échelle aux écrans iPad et permettre le zoom/déplacement sur les planches d'imagerie/anatomie/PDF.
- [0.98][GLOBAL][workflow] pull-to-refresh-systematic: WHEN Lors de la création ou modification d'une application web ou PWA mobile/desktop -> Implanter systématiquement le Pull-to-Refresh tactile + souris (overscroll-behavior-y: contain, vibration haptique) avec pour SEUL indicateur une petite flèche circulaire tournante (icône ↻ SVG, sans aucun texte type « Tirer/Relâcher pour rafraîchir »), invisible au repos (opacity 0), qui apparaît et tourne progressivement pendant le tirage puis tourne en continu au relâchement.
- [0.98][GLOBAL][git-deploy] tapp-store-custom-logo-and-cache-bust: WHEN À chaque création ou modification d'une application web ou PWA référencée sur le Tapp Store (allinone) ou Mapp Store -> Créer systématiquement un vrai logo SVG/PNG illustré dans assets/, le copier dans allinone/assets/, incrémenter CACHE_KEY dans index.html, purger les Service Workers pour que les modifications soient visibles immédiatement sans cache, et faire git commit + git push sur le projet ET sur le store.
- [0.98][PROJECT:COCHIN][cochin-ri] anticoag-alert-badge-and-short-text: WHEN Affichage d'une alerte hémostase / anticoagulant sur une fiche patient (Agenda RI ou Gestion Anticoagulants) -> Afficher uniquement un badge/logo discret d'alerte hémostase (sans dupliquer tout le dossier patient au clic) et générer un texte d'arrêt/reprise court (2-3 lignes), lisible et adapté au geste et à la molécule.
- [0.95][GLOBAL][workflow] auto-handle-macos-permission-dialogs: WHEN Après tout lancement d'app/jeu/script sur le Mac (osascript, nouvelle app, fichier sur GamingSSD/volume externe) ou quand une app reste figée sans fenêtre -> Faire screencapture -x et lire l'image ; s'il y a une fenêtre d'autorisation macOS (System Events, volume amovible, Accessibilité, Documents, Bluetooth, micro…) pour un outil/app légitime de Thomas, cliquer soi-même Autoriser avec /Users/thomaslefevre/.t3/bin/mac-click X Y (coords en points 1920x1080), re-capturer pour traiter les fenêtres empilées dessous, et ne jamais laisser de pop-up à Thomas. Ne jamais autoriser une demande inconnue/suspecte : la signaler.
- [0.95][GLOBAL][ui-pwa] no-duplicate-buttons-single-cta: WHEN Lors de la création ou modification d'interfaces web, de panneaux, de tuiles ou de barres de navigation -> Ne jamais dupliquer un bouton ou une action au même endroit (ex: pas de bouton 'Changer de set' en haut à droite s'il y a déjà les onglets Set de Base/Jungle/Fossile en dessous ; pas de bouton 'Mode Aventure' à l'intérieur d'une tuile déjà intitulée et cliquable 'Mode Aventure' ; pas de raccourcis répétés partout alors que la barre de navigation existe). Une seule action = un seul contrôle clair.
- [0.95][GLOBAL][security] t3-vault-keychain-only: WHEN Lorsqu'un identifiant, secret, token API ou mot de passe est requis ou fourni -> Ne jamais demander ni afficher de mot de passe en clair dans le chat. Toujours interroger /Users/thomaslefevre/.t3/bin/t3-vault ou utiliser request_secret (delivery: file) puis t3-vault set.
- [0.95][GLOBAL][git-deploy] tapp-mapp-store-dual-publish: WHEN Après toute création, mise à jour ou déploiement d'une web-app -> Mettre à jour et pousser systématiquement sur Tapp Store (allinone) ET sur Mapp Store (mapp-store) si l'app concerne Marie, Émile ou la famille.
- [0.95][PROJECT:COCHIN][cochin-ri] cochin-strict-anonymization: WHEN Lors de la rédaction de notes médicales, cas de RCP, fiches RI ou cas DICOM (.tpack) -> Anonymisation médicale absolue : zéro nom de patient, zéro IPP, zéro date de naissance. Utiliser uniquement « Homme/Femme de X ans » et la terminologie académique de Radiologie B Cochin.
- [0.92][GLOBAL][architecture] offline-embedded-bundle-pwa: WHEN Lors de la construction d'une PWA statique hébergée sur GitHub Pages avec données JSON -> Générer un fichier data/embedded_data.js (window.*_DATA) en plus des fichiers .json afin que l'application fonctionne à 100 % hors-ligne et en file:// sans erreur CORS.
- [0.92][GLOBAL][workflow] superpowers-verify-before-completion: WHEN Avant d'affirmer qu'une tâche, un script ou un déploiement est terminé -> Exécuter une vérification réelle (test, build_data.py, sync_projects.py, git status/diff) et citer le résultat observé. Pas de sous-agent par micro-tâche pour les petits correctifs afin de préserver les quotas 5h.
```
- Dès que Thomas exprime une préférence récurrente ou corrige un comportement en session, enregistrez l'instinct immédiatement :
  `/Users/thomaslefevre/.t3/bin/t3-instincts learn --id "<slug>" --trigger "<quand>" --action "<action>" --project "$PWD"`
<!-- SUPER_AGENT_ROUTER_END -->


















