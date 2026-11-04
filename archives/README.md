<img src="assets/icon.svg" width="64" height="64" alt="Archives des Internes — COCHIN·OS">

# Archives des Internes — COCHIN·OS (`07`)

Application web & mobile ultra-légère permettant de conserver, compresser et consulter instantanément les présentations PowerPoint (`.pptx`) des internes de **Radiologie B (Ostéo-Articulaire & RI)** de l'Hôpital Cochin :

- **🩻 Cas Cliniques (`CAS`)** — Dossiers de staff radio-cliniques avec **Mode Staff / Diagnostic Caché** (floutage du diagnostic jusqu'à la diapositive finale pour s'entraîner)
- **🎓 Présentations & Cours DES (`PRÉSENTATIONS`)** — Mises au point sémiologiques IRM/TDM, arthroscanner et protocoles de Radiologie Interventionnelle
- **📚 Bibliographies / Journal Club (`BIBLIO`)** — Analyses critiques d'articles majeurs avec `PMID`, `DOI`, Impact Factor et *« Ce que ça change en pratique à Cochin »*

---

## ⚡ Architecture « Smart-Slim » : Comment le stockage reste ultra-léger (< 600 Ko au lieu de > 400 Mo)

Un fichier PowerPoint (`.pptx`) de radiologie pèse classiquement **30 à 100 Mo** à cause des captures PACS PNG/BMP/TIFF non compressées dans `ppt/media/` et nécessite un téléchargement complet avant lecture.

L'application résout ce problème grâce à une architecture à **3 niveaux** :

1. **Extraction & Indexation Plein-Texte Découplée (`data/archives-index.json` + `data/decks/<id>.json`)** :
   - Le catalogue d'accueil charge uniquement l'index léger (`< 90 Ko` pour toute la base) en **< 20 ms**.
   - La barre de recherche (`/`) interroge en temps réel le titre, les tags, le diagnostic ET **le contenu texte de chaque diapositive** (avec saut direct vers la diapo correspondante `🎯 Trouvé dans Diapo #N`).
2. **Compresseur `.PPTX` Natif Côté Navigateur (`JSZip` + `Canvas JPEG/WebP`) & CLI (`scripts/slim_pptx.py`)** :
   - Glissez-déposez n'importe quel fichier `.pptx` dans le **Studio Slim (`+ ARCHIVER / SLIM .PPTX`)** :
     - Décompresse l'archive OpenXML `.pptx` directement dans le navigateur (zéro serveur).
     - Extrait automatiquement les titres, listes à puces, notes de l'orateur (`ppt/notesSlides/`) et images de chaque diapositive (`ppt/slides/`).
     - Ré-encode les images lourdes de `ppt/media/*` en JPEG/WebP optimisé (`max 1360–1440px`, qualité `0.78–0.80`) et reconstruit un fichier **`.pptx` Slim 5× à 20× plus léger** (100 % ouvrable dans PowerPoint / Keynote).
3. **Stockage Local Haute Capacité (`IndexedDB`) + Visionneuse PACS / Négatoscope** :
   - Les présentations ajoutées depuis le navigateur sont stockées dans `IndexedDB` (sans la limite de 5 Mo du `localStorage`), avec export/import en 1 clic d'un pack `.json`.
   - Visionneuse intégrée avec zoom, contraste radiologique, inversion Négatif/Positif (`I`), navigation clavier (`←`/`→`) et mode Staff (`B`).

---

## 🛠️ Commandes utiles (CLI)

```bash
# Régénérer la base initiale (9 présentations, 30 diapos, fichiers .pptx Slim et index JSON)
python3 scripts/generate_initial_archives.py

# Compresser et extraire un fichier PowerPoint (.pptx) en ligne de commande
python3 scripts/slim_pptx.py mon_staff.pptx --category cas --region "Genou" --author "Thomas L."
```
