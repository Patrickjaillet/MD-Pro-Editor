# 🗺️ ROADMAP.md — MD Pro Editor

> L'éditeur Markdown le plus puissant, le plus beau et le plus complet au monde.
> Plateforme cible : **Windows 10 LTSC / Windows 10 / Windows 11**
> Stack : **C# / .NET 8+ / Avalonia UI 11+ / FluentAvalonia / AvaloniaEdit / Markdig**

---

## 📜 License and Copyright

**MD Pro Editor**
Copyright © 2026 Patrick JAILLET — All rights reserved
Email: contact.shaderstudio@gmail.com
Website: https://patrickjaillet.github.io/sandefjord-software

---

## ⚙️ Development Conventions

- [ ] General language only French/English
- [ ] Theme White only
- [ ] No comments in the source code
- [ ] Strict Windows 10 LTSC/10/11 compatibility only
- [ ] Every added feature must be reflected in this ROADMAP.md
- [ ] Automatic software version serialization for each Phase and each build
- [ ] Every modification must be reflected for the end-user in the CHANGELOG.md
- [ ] The README.md must be created and updated for the end-user and include a software screenshot in docs/screenshot.png
- [ ] Systematic synchronization (commit+push + Release) with the [https://github.com/Patrickjaillet/MD-Pro-Editor](https://github.com/Patrickjaillet/MD-Pro-Editor) repository upon every project modification
- [ ] Never integrate Claude AI into GitHub, the files, or the GitHub contributors list
- [ ] Creation of all files and documents required for the GitHub repository
- [ ] Integrate Logo / copyright / Email / Website information into an "About" tab
- [ ] Create icons for both the "Inno Setup" installer and the software
- [ ] No source code must be in the GitHub repository, Only documentation for GitHub
- [ ] In Repository details, add the Topic "sandefjord-software"

---

## 🎯 Vision du projet

Créer un éditeur Markdown natif Windows qui surpasse **Typora**, **Obsidian**, **Mark Text**, **Zettlr**, **iA Writer** et **Ghostwriter** sur trois axes simultanément :

1. **Performance** — rendu instantané, aucun lag, même sur des documents de 50 000+ lignes.
2. **UI/UX** — design Fluent 2 natif Windows 11 (Mica, Acrylic, animations fluides, dark/light natif), niveau app "AAA".
3. **Fonctionnalités** — couverture complète du Markdown (CommonMark + GFM + extensions), édition WYSIWYG hybride, exports multi-formats, organisation de notes façon Obsidian (liens, graphe), sans jamais sacrifier la simplicité d'usage.

Modèle économique : **Shareware** — version complète à 100% pendant **7 jours d'essai**, puis verrouillage jusqu'à achat via **PayPal (2,99 €)**, débloqué par **code de licence**.

---

## 🧱 Stack technique retenue

| Domaine | Technologie |
|---|---|
| UI Framework | Avalonia UI (v11+) |
| Design System | FluentAvalonia (Fluent Design v2, Mica/Acrylic, thème natif Windows 11) |
| Éditeur de texte | AvaloniaEdit (portage AvalonEdit) + coloration syntaxique custom Markdown |
| Moteur Markdown | Markdig (parsing AST + extensions GFM, tables, footnotes, task lists, emoji, math, mermaid…) |
| Preview HTML | WebView (CefGlue / WebView Avalonia) ou moteur de rendu Avalonia natif pour la preview |
| Diagrammes | Mermaid.js (injecté dans la preview HTML) |
| Formules mathématiques | KaTeX (injecté dans la preview HTML) |
| Export PDF | QuestPDF ou moteur HTML→PDF (Puppeteer-sharp léger / PdfSharp) |
| Export DOCX | OpenXML SDK |
| Packaging installeur | Inno Setup |
| Licensing | Système custom (voir Phase 6) |
| Langage | C# / .NET 8 (LTS) |
| Contrôle de version | Git + GitHub (repo binaire/releases uniquement, pas de code source public) |

---

## 📁 Structure de solution proposée

```
MDProEditor.sln
├── src/
│   ├── MDProEditor.App/              (point d'entrée, Avalonia App, DI, bootstrap)
│   ├── MDProEditor.Core/             (modèles, services, parsing, fichiers)
│   ├── MDProEditor.Editor/           (wrapper AvaloniaEdit, coloration, folding)
│   ├── MDProEditor.Preview/          (moteur Markdig + templates HTML/CSS)
│   ├── MDProEditor.UI/               (vues, ViewModels MVVM, contrôles Fluent custom)
│   ├── MDProEditor.Licensing/        (trial, clé, validation, fenêtre d'achat)
│   ├── MDProEditor.Export/           (PDF, DOCX, HTML, EPUB)
│   └── MDProEditor.Plugins/          (API d'extension interne)
├── assets/
│   ├── icons/
│   ├── themes/
│   └── templates/
├── installer/
│   └── InnoSetup/
└── docs/
    └── screenshot.png
```

---

## 🚀 PHASE 0 — Fondations & Architecture (v0.1.0)

- [x] Création de la solution .NET 8 + projets Avalonia (App, Core, UI, Editor, Preview)
- [x] Configuration MVVM (CommunityToolkit.Mvvm) avec DI (Microsoft.Extensions.DependencyInjection)
- [x] Intégration FluentAvalonia (NuGet) + thème Fluent 2 par défaut
- [x] Mise en place de la fenêtre principale : layout 3 zones (Explorateur fichiers | Éditeur | Preview)
- [x] Système de logging interne (fichiers rotatifs, niveau debug/release)
- [x] Système de configuration utilisateur (fichier settings.json chiffré léger, chemin %AppData%)
- [x] Mise en place du versioning sémantique automatique (MAJOR.MINOR.PATCH.BUILD, incrémenté à chaque build CI)
- [x] Création CHANGELOG.md initial
- [x] Création README.md initial (placeholder screenshot docs/screenshot.png)
- [x] Premier commit + push + tag Release v0.1.0 (commit et tag locaux effectués ; push GitHub à faire — voir note)

---

## ✏️ PHASE 1 — Éditeur de texte Markdown (v0.2.0)

- [x] Intégration AvaloniaEdit comme composant d'édition principal
- [x] Coloration syntaxique Markdown complète (titres, gras, italique, code, liens, images, citations, listes, tableaux, frontmatter YAML)
- [x] Numérotation de lignes + repères de marge (gutter)
- [x] Pliage de code (code folding) par section/titre (##)
- [x] Indentation intelligente listes/sous-listes (Tab/Shift+Tab)
- [x] Auto-fermeture des paires (**, _, `, [], (), {})
- [x] Auto-continuation des listes (-, *, 1.) à la ligne suivante
- [x] Undo/Redo illimité avec granularité par mot (natif AvaloniaEdit)
- [~] Multi-curseurs et sélection colonne (Alt+clic) — sélection rectangulaire native disponible ; multi-curseurs simultanés non supportés par AvaloniaEdit, reporté
- [x] Recherche & remplacement avec regex, casse, mot entier (SearchPanel) — recherche dans tout le dossier reportée à la Phase 4 (recherche globale workspace)
- [ ] Mini-carte (minimap) façon VS Code (optionnelle, activable) — reporté
- [ ] Coloration des erreurs de syntaxe Markdown (liens cassés, tableaux mal formés) — reporté
- [x] Support multi-onglets (plusieurs fichiers ouverts simultanément)
- [x] Sauvegarde automatique configurable (intervalle + à la perte de focus)
- [x] Système de versions locales (historique des sauvegardes, façon "Time Machine" léger)
- [x] Mise à jour CHANGELOG.md + tag Release v0.2.0

---

## 👁️ PHASE 2 — Moteur de rendu & Preview (v0.3.0)

- [x] Intégration Markdig avec pipeline complet : `UseAdvancedExtensions()`, `UsePipeTables()`, `UseTaskLists()`, `UseEmojiAndSmiley()`, `UseFootnotes()`, `UseYamlFrontMatter()`, `UseAutoLinks()`
- [x] Preview HTML en temps réel avec debounce intelligent (300 ms, pas de lag même sur gros documents)
- [~] Défilement synchronisé éditeur → preview (scroll-sync par ratio) ; sens preview → éditeur reporté
- [x] Mode "Split View" (éditeur + preview côte à côte, redimensionnable)
- [x] Mode "Source View" pur (bascule Aperçu on/off, sans preview)
- [ ] Mode "Live Preview / WYSIWYG hybride" façon Typora — reporté à une phase ultérieure (nécessite un moteur de rendu inline dédié dans l'éditeur)
- [x] Support rendu formules mathématiques (KaTeX, syntaxe `$...$` et `$$...$$`, via CDN)
- [x] Support diagrammes Mermaid (flowcharts, séquences, gantt, mindmap, via CDN)
- [x] Support blocs de code avec coloration syntaxique multi-langages (Prism.js dans la preview, via CDN)
- [x] Rendu correct des tableaux GFM avec alignement
- [x] Rendu des tâches (checkboxes `- [ ]` / `- [x]`) cochables directement dans la preview (synchronisées avec le document source)
- [x] Zoom preview (Ctrl + molette, boutons +/−)
- [x] Impression directe depuis la preview
- [x] Mise à jour CHANGELOG.md + tag Release v0.3.0

---

## 🎨 PHASE 3 — UI/UX Fluent haut de gamme (v0.4.0)

- [x] Application du thème Fluent Design v2 complet (Mica en fond de fenêtre principale avec repli Acrylic/Blur automatique selon l'OS)
- [x] Thème unique Blanc (light) — transitions douces sur boutons/bascules/panneaux
- [x] Barre de titre custom intégrée (title bar overlay, boutons min/max/close redessinés)
- [x] Command Palette (Ctrl+Maj+P) façon VS Code pour les actions principales
- [x] Barre d'outils contextuelle flottante à la sélection de texte (façon Notion : gras, italique, lien, surlignage)
- [x] Explorateur de fichiers latéral avec arborescence de dossier, ouverture, renommage inline (F2), glisser-déposer de fichiers Windows pour ouverture — [~] réorganisation interne par glisser-déposer non implémentée
- [x] Onglets réorganisables par glisser-déposer — [ ] aperçu au survol reporté (nécessiterait un rendu miniature du document)
- [x] Mode Focus / Distraction-free (atténue tout le texte hors du paragraphe en cours, façon iA Writer)
- [x] Mode Machine à écrire (typewriter mode — centrage vertical approximatif de la ligne active)
- [x] Panneau Outline / Sommaire (TOC) généré automatiquement, navigable — [ ] réorganisation par glisser-déposer reportée
- [x] Compteur de mots / caractères / temps de lecture estimé en barre de statut
- [x] Micro-animations sur les interactions (hover, clic, transitions de fond)
- [x] Icônes vectorielles cohérentes (FluentAvalonia Symbol Icons) dans toute l'interface
- [x] Personnalisation des polices (police éditeur séparée de la police preview, sélection parmi les polices système) via la fenêtre Préférences
- [x] Raccourcis clavier personnalisables (fenêtre Préférences, capture de combinaison) — persistés en settings.json, appliqués au prochain démarrage
- [x] Mise à jour CHANGELOG.md + tag Release v0.4.0

---

## 🧩 PHASE 4 — Fonctionnalités avancées & organisation (v0.5.0)

- [x] Gestion de "Coffre" / Workspace (dossier de notes façon Obsidian) avec arborescence persistante (dernier dossier ouvert restauré au démarrage)
- [x] Liens internes façon Wiki `[[Nom du fichier]]` avec autocomplétion (fenêtre de complétion `[[`) et création à la volée (commande « Créer les notes manquantes »)
- [x] Panneau de backlinks (quels fichiers référencent le fichier courant)
- [ ] Vue graphe des liens entre notes (graph view interactif, zoom/pan, physics simulation) — reporté, chantier autonome conséquent
- [x] Gestion des images : collage direct (Ctrl+V) depuis le presse-papier avec copie automatique dans un dossier `assets/`
- [x] Gestion des images : drag & drop depuis l'explorateur Windows
- [x] Redimensionnement des images inline dans la preview (glisser le coin de l'image, répercuté dans le Markdown via `{width=...}`)
- [ ] Éditeur de tableaux visuel (ajout/suppression lignes-colonnes, alignement, sans écrire le Markdown à la main) — reporté
- [x] Éditeur de frontmatter YAML avec formulaire visuel (clé/valeur) — mode brut non fourni (frontmatter à structure simple clé/valeur uniquement)
- [x] Système de templates/snippets réutilisables (fenêtre de gestion + insertion via la Command Palette)
- [ ] Correcteur orthographique/grammatical FR/EN intégré — reporté (nécessite des dictionnaires Hunspell à empaqueter)
- [x] Export vers PDF (impression WebView2 vers PDF, fidèle à la preview)
- [x] Export vers DOCX (structure Word native via OpenXML : titres, gras, italique, listes, citations, code)
- [x] Export vers HTML autonome (CSS inliné, un seul fichier portable ; KaTeX/Mermaid/Prism restent chargés via CDN)
- [x] Export vers EPUB (livre électronique, structure OPF/XHTML minimale)
- [ ] Import depuis DOCX/HTML vers Markdown (conversion inverse) — reporté
- [x] Système de thèmes CSS personnalisables pour la preview (Clair/Sépia/Sombre + import d'une feuille de style CSS custom)
- [x] Recherche globale multi-fichiers dans tout le workspace (façon "Rechercher dans les fichiers")
- [ ] Intégration Git basique — reportée
- [ ] Système de plugins interne — reporté (choix d'architecture à faire en amont, pas de plugin à charger pour l'instant)
- [x] Mise à jour CHANGELOG.md + tag Release v0.5.0

---

## 🔐 PHASE 5 — Licensing, Trial 7 jours & PayPal (v0.6.0)

- [x] Génération d'un identifiant machine unique (hardware fingerprint : CPU ID via WMI + numéro de série du volume système, hashés en SHA-256)
- [x] Stockage local de la date de première exécution (registre Windows `HKCU\Software\MDProEditor` + fichier caché `%AppData%\MDProEditor\.state` obfusqué, double vérification anti-triche avec auto-réparation sur la date la plus ancienne)
- [x] Détection de la manipulation de l'horloge système (comparaison avec le dernier horodatage local connu ; pas de vérification serveur — voir limitation ci-dessous)
- [x] Compteur de jours d'essai (7 jours), affichage du nombre de jours restants dans l'interface
- [x] Fenêtre "Achat / Activation" qui s'ouvre **avant** le lancement de la fenêtre principale
  - [x] Design Fluent cohérent avec le reste de l'application (Mica, thème clair)
  - [x] Bouton "Essayer 7 jours" (lance l'app en mode trial si essai non expiré)
  - [x] Bouton "Acheter maintenant — 2,99 €" → ouvre le lien PayPal dans le navigateur par défaut
  - [x] Champ "Entrer mon code de licence" + bouton "Activer"
  - [x] Affichage du nombre de jours d'essai restants ou message "Essai expiré"
  - [x] Lien "Renvoyer mon code" (mailto vers contact.shaderstudio@gmail.com)
- [x] Génération du lien de paiement PayPal (PayPal.Me configuré à 2,99 €)
- [x] Processus de remise du code après paiement :
  - [x] Option manuelle : réception notification paiement PayPal → génération clé via l'outil interne `tools/LicenseKeyGeneratorTool` → envoi par email au client
  - [ ] Option automatisée (webhook PayPal IPN) — reportée, non nécessaire au lancement
- [x] Algorithme de génération/validation de clé de licence (HMAC-SHA256 liée à l'email acheteur, format `MDPE-XXXX-XXXX-XXXX`)
- [x] Validation offline de la clé (aucun accès réseau requis, vérification cryptographique locale)
- [x] Verrouillage total du logiciel après expiration des 7 jours sans achat (retour obligatoire à la fenêtre d'achat/activation, `ShutdownMode` explicite)
- [x] Aucune limitation fonctionnelle pendant les 7 jours (version 100% complète)
- [x] Mise à jour CHANGELOG.md + tag Release v0.6.0

---

## 📦 PHASE 6 — Packaging & Distribution (v0.7.0)

- [x] Création du logo / icône de l'application (format .ico multi-résolutions 16→256px, généré par programme : rounded square Fluent + monogramme « M↓ »)
- [x] Création de l'icône de l'installeur Inno Setup (identique au logo app)
- [x] Script Inno Setup complet (`installer/InnoSetup/MDProEditor.iss`) :
  - [x] Installation dans Program Files
  - [x] Raccourcis Bureau + Menu Démarrer
  - [x] Association fichiers `.md` / `.markdown` à l'application (tâche optionnelle à l'installation)
  - [x] Désinstalleur propre
  - [x] Vérification prérequis : .NET 10 embarqué via publication self-contained single-file (aucune installation de runtime requise)
- [x] Signature de l'exécutable et de l'installeur (certificat auto-signé de test — un certificat de signature de code acheté auprès d'une autorité reconnue sera nécessaire avant publication officielle pour éviter les avertissements SmartScreen)
- [x] Test d'installation propre — testé en conditions réelles sur cette machine (Windows 10 Enterprise LTSC) : installation silencieuse, raccourcis, association de fichiers, lancement avec argument de fichier, désinstallation complète, tous vérifiés avec succès. Tests sur Windows 10 non-LTSC et Windows 11 à réaliser sur des machines dédiées avant publication.
- [x] Mise à jour CHANGELOG.md + tag Release v0.7.0

---

## 📄 PHASE 7 — GitHub, Documentation & About (v0.8.0)

- [ ] Création du repository GitHub `Patrickjaillet/MD-Pro-Editor` (releases + docs uniquement, aucun code source, ni ROADMAP.md)
- [ ] README.md complet : présentation, fonctionnalités, capture d'écran (`docs/screenshot.png`), lien de téléchargement, lien PayPal, licence
- [ ] CHANGELOG.md structuré (format Keep a Changelog) tenu à jour à chaque version
- [ ] Onglet "About" dans le logiciel :
  - [ ] Logo de l'application
  - [ ] Copyright © 2026 Patrick JAILLET
  - [ ] Email : contact.shaderstudio@gmail.com
  - [ ] Website : https://patrickjaillet.github.io/sandefjord-software
  - [ ] Numéro de version affiché automatiquement
- [ ] Publication systématique des Releases GitHub (binaire installeur uniquement) à chaque phase/build
- [ ] Vérification qu'aucun fichier source (.cs, .csproj, .sln) ne se trouve dans le repository
- [ ] Mise à jour CHANGELOG.md + tag Release v0.8.0

---

## 🧪 PHASE 8 — Qualité, Performance & Finitions (v0.9.0)

- [ ] Tests de performance sur fichiers volumineux (50 000+ lignes) : pas de lag frappe/scroll/preview
- [ ] Tests mémoire (pas de fuite sur sessions longues multi-onglets)
- [ ] Tests de compatibilité stricte Windows 10 LTSC (versions .NET, API Win32 utilisées)
- [ ] Relecture UX complète : cohérence des animations, temps de réponse perçu (<100ms sur toute action)
- [ ] Vérification totale FR/EN de toutes les chaînes de l'interface (aucune autre langue)
- [ ] Vérification "No comments in the source code" sur l'ensemble de la base de code
- [ ] Audit accessibilité clavier (navigation 100% clavier possible)
- [ ] Correction de tous les bugs remontés lors des phases précédentes
- [ ] Mise à jour CHANGELOG.md + tag Release v0.9.0

---

## 🏁 PHASE 9 — Release 1.0.0

- [ ] Gel des fonctionnalités (feature freeze)
- [ ] Dernière campagne de tests utilisateurs internes
- [ ] Génération de la release finale signée + installeur Inno Setup final
- [ ] Publication GitHub Release v1.0.0 avec changelog complet
- [ ] Mise à jour finale du README.md (capture d'écran finale, liens à jour)
- [ ] Vérification finale de la fenêtre d'achat/PayPal en conditions réelles (paiement test)
- [ ] Communication de sortie (site web mis à jour)

---

## 🔮 Post-1.0 — Pistes d'évolution (backlog libre, non planifié)

- [ ] Synchronisation cloud optionnelle (OneDrive/Google Drive local sync, pas de serveur propriétaire)
- [ ] Mode collaboratif temps réel (édition partagée)
- [ ] Version portable (sans installation, exécutable unique)
- [ ] Marketplace de thèmes CSS communautaires
- [ ] Assistant de conversion Markdown → Slides (présentation façon Marp)
- [ ] Application mobile compagnon (lecture seule)

---

## 📊 Suivi de version

| Phase | Version cible | Statut |
|---|---|---|
| Phase 0 — Fondations | v0.1.0 | ✅ |
| Phase 1 — Éditeur | v0.2.0 | ✅ |
| Phase 2 — Preview | v0.3.0 | ✅ |
| Phase 3 — UI/UX | v0.4.0 | ✅ |
| Phase 4 — Fonctionnalités avancées | v0.5.0 | ✅ |
| Phase 5 — Licensing/PayPal | v0.6.0 | ✅ |
| Phase 6 — Packaging | v0.7.0 | ✅ |
| Phase 7 — GitHub/Docs | v0.8.0 | ⬜ |
| Phase 8 — QA/Perf | v0.9.0 | ⬜ |
| Phase 9 — Release | v1.0.0 | ⬜ |
