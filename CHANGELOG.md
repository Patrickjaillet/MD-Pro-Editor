# Changelog

Toutes les modifications notables de MD Pro Editor sont documentées dans ce fichier.

Le format s'appuie sur [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/),
et ce projet suit le [Semantic Versioning](https://semver.org/lang/fr/).

## [Non publié]

## [0.7.0] - 2026-07-22

### Ajouté

- Logo et icône de l'application (.ico multi-résolutions 16 à 256 px).
- Installeur Windows complet via Inno Setup : installation dans Program Files, raccourcis Bureau et Menu Démarrer, association optionnelle des fichiers `.md`/`.markdown`, désinstalleur propre.
- Publication self-contained (runtime .NET embarqué) : aucune installation de prérequis nécessaire pour l'utilisateur final.
- Signature numérique de l'exécutable et de l'installeur.
- Script `installer/build-installer.ps1` automatisant la publication, la signature et la compilation de l'installeur pour les prochaines releases.
- Fichier `LICENSE.txt` (contrat de licence utilisateur final) inclus dans l'installeur.

### Limitations connues

- La signature utilise un certificat auto-signé de test : Windows SmartScreen affichera un avertissement à l'installation tant qu'un certificat de signature de code acheté auprès d'une autorité reconnue n'est pas utilisé.
- Installation testée en conditions réelles sur Windows 10 Enterprise LTSC (cette machine). Les tests sur Windows 10 grand public et Windows 11 restent à effectuer sur des machines dédiées avant publication officielle.

## [0.6.0] - 2026-07-22

### Ajouté

- Essai gratuit de 7 jours sans aucune limitation fonctionnelle.
- Fenêtre « Achat / Activation » s'ouvrant avant la fenêtre principale : jours d'essai restants, bouton d'achat PayPal (2,99 €), saisie de code de licence, lien de renvoi de code par e-mail.
- Identification machine (empreinte matérielle CPU + volume disque, hachée) et détection de manipulation de l'horloge système pour limiter la fraude sur l'essai.
- Double stockage anti-triche de la date de première exécution (registre Windows + fichier caché), avec auto-réparation en cas d'incohérence entre les deux.
- Génération et validation hors ligne des clés de licence (format `MDPE-XXXX-XXXX-XXXX`, liées à l'e-mail acheteur).
- Verrouillage de l'application après expiration de l'essai sans licence active : retour obligatoire à la fenêtre d'activation.
- Outil interne en ligne de commande (`tools/LicenseKeyGeneratorTool`) pour générer une clé de licence à partir de l'e-mail d'un acheteur après réception d'un paiement PayPal.

### Limitations connues

- Pas de vérification d'horodatage serveur en cas de manipulation de l'horloge : la détection repose uniquement sur le dernier horodatage local connu (suffisant contre la fraude occasionnelle, pas contre un attaquant déterminé).
- Remise de la clé de licence après paiement : processus manuel uniquement (pas de webhook PayPal IPN automatisé pour l'instant).
- La protection de la clé de licence est raisonnable pour un shareware indépendant, pas inviolable face à la rétro-ingénierie.

## [0.5.0] - 2026-07-22

### Ajouté

- Gestion de workspace (« Coffre ») avec restauration automatique du dernier dossier ouvert au démarrage.
- Liens internes façon wiki `[[Nom]]` avec autocomplétion à la frappe et commande « Créer les notes manquantes » pour générer les notes cibles inexistantes.
- Panneau de rétroliens (backlinks) indiquant quels fichiers référencent le document courant.
- Gestion des images : collage direct depuis le presse-papier (Ctrl+V) et glisser-déposer depuis l'Explorateur Windows, copie automatique dans un dossier `assets/` relatif au document.
- Redimensionnement des images directement dans la preview (glisser le coin de l'image), répercuté dans le Markdown source.
- Éditeur de frontmatter YAML avec formulaire visuel clé/valeur.
- Système de templates et snippets réutilisables, gérables via une fenêtre dédiée et insérables depuis la Command Palette.
- Thèmes CSS de la preview (Clair, Sépia, Sombre) et import d'une feuille de style CSS personnalisée.
- Recherche globale dans tous les fichiers Markdown du workspace, avec navigation directe vers la ligne trouvée.
- Export vers HTML autonome (CSS inliné), PDF (impression fidèle de la preview), DOCX (Word natif via OpenXML) et EPUB.

### Limitations connues

- Vue graphe des liens entre notes non implémentée (chantier conséquent, reporté).
- Éditeur de tableaux visuel non implémenté (édition des tableaux en Markdown brut pour l'instant).
- Correcteur orthographique/grammatical FR/EN non implémenté (nécessite l'empaquetage de dictionnaires).
- Import DOCX/HTML vers Markdown non implémenté (seul l'export est disponible).
- Intégration Git et système de plugins internes non implémentés.
- L'export HTML autonome reste dépendant d'un CDN pour KaTeX/Mermaid/Prism (comme la preview).

## [0.4.0] - 2026-07-22

### Ajouté

- Thème Fluent Design v2 complet avec fond Mica (repli automatique Acrylic/Blur sur les OS ne le supportant pas) et barre de titre personnalisée.
- Command Palette (Ctrl+Maj+P) pour accéder rapidement à toutes les actions principales.
- Barre d'outils contextuelle flottante à la sélection de texte (gras, italique, lien, surlignage), façon Notion.
- Explorateur de fichiers latéral : ouverture de dossier, arborescence, ouverture de fichier au double-clic, renommage inline (F2), glisser-déposer de fichiers Windows pour les ouvrir directement.
- Onglets réorganisables par glisser-déposer.
- Mode Focus / Distraction-free : atténue le texte en dehors du paragraphe en cours d'édition.
- Mode Machine à écrire : centrage vertical de la ligne active pendant la frappe.
- Panneau Sommaire (TOC) généré automatiquement à partir des titres, navigation en un clic.
- Temps de lecture estimé ajouté à la barre de statut.
- Icônes vectorielles Fluent cohérentes dans toute l'interface (barre d'outils, explorateur, onglets).
- Fenêtre Préférences : personnalisation des polices (éditeur et aperçu, taille et famille) et des raccourcis clavier (capture de combinaison, persistés dans settings.json).
- Micro-animations sur les boutons, bascules et panneaux.

### Limitations connues

- Réorganisation interne de l'explorateur de fichiers par glisser-déposer non implémentée (seule l'ouverture par glisser-déposer depuis l'Explorateur Windows est disponible).
- Aperçu au survol des onglets non implémenté.
- Réorganisation des sections du sommaire par glisser-déposer non implémentée.
- Les raccourcis clavier personnalisés sont appliqués au prochain démarrage de l'application.

## [0.3.0] - 2026-07-22

### Ajouté

- Moteur de rendu Markdown complet via Markdig (tables, listes de tâches, notes de bas de page, frontmatter YAML, liens automatiques, émojis, mathématiques, diagrammes).
- Preview HTML en temps réel dans une WebView native (Microsoft Edge WebView2 sur Windows), avec debounce de 300 ms pour rester fluide sur les gros documents.
- Défilement synchronisé de l'éditeur vers la preview.
- Bascule Split View / Source View (affichage ou masquage de la preview).
- Rendu des formules mathématiques (KaTeX) et des diagrammes Mermaid.
- Coloration syntaxique multi-langages des blocs de code dans la preview (Prism.js).
- Tableaux GFM avec alignement, et cases à cocher des listes de tâches cliquables directement depuis la preview (répercutées dans le document source).
- Zoom de la preview (Ctrl + molette, boutons +/−) et impression directe depuis la preview.

### Limitations connues

- Le défilement synchronisé n'est actif que de l'éditeur vers la preview (sens inverse reporté).
- Le mode « Live Preview / WYSIWYG hybride » façon Typora est reporté à une phase ultérieure.
- KaTeX, Mermaid.js et Prism.js sont chargés depuis un CDN : un accès internet est requis pour un rendu enrichi de la preview (le texte Markdown brut reste toujours visible dans l'éditeur hors ligne).

## [0.2.0] - 2026-07-22

### Ajouté

- Coloration syntaxique Markdown complète (titres, gras, italique, code inline, blocs de code, liens, images, citations, listes, tâches, tableaux, frontmatter YAML).
- Pliage de code (folding) par section de titre (`#` à `######`).
- Indentation intelligente des listes et sous-listes (Tab / Maj+Tab).
- Auto-fermeture des paires `**`, `_`, `` ` ``, `[]`, `()`, `{}`.
- Auto-continuation des listes (à puces, numérotées, tâches) à la touche Entrée.
- Recherche et remplacement intégrés (panneau de recherche AvaloniaEdit, regex, casse, mot entier).
- Support multi-onglets : plusieurs documents ouverts simultanément, avec indicateur de modification non enregistrée.
- Sauvegarde automatique configurable (intervalle et à la perte de focus de la fenêtre).
- Historique de versions locales par fichier (façon « Time Machine » léger, 50 instantanés conservés).

### Limitations connues

- Multi-curseurs simultanés non disponibles (limitation d'AvaloniaEdit) ; la sélection rectangulaire native (Alt+glisser) reste utilisable.
- Mini-carte (minimap) et coloration des erreurs de syntaxe Markdown reportées à une phase ultérieure.

## [0.1.0] - 2026-07-22

### Ajouté

- Création de la solution .NET 10 (LTS) avec les projets Avalonia : App, Core, Editor, Preview, UI, Licensing, Export, Plugins.
- Intégration de FluentAvalonia et du thème Fluent Design v2 (blanc uniquement).
- Mise en place de l'architecture MVVM (CommunityToolkit.Mvvm) avec injection de dépendances (Microsoft.Extensions.DependencyInjection).
- Fenêtre principale avec layout 3 zones redimensionnables : Explorateur de fichiers | Éditeur | Preview.
- Intégration initiale d'AvaloniaEdit comme composant d'édition (MarkdownTextEditor).
- Système de logging interne avec rotation automatique des fichiers (conservation 14 jours, `%AppData%\MDProEditor\logs`).
- Système de configuration utilisateur persistant (`%AppData%\MDProEditor\settings.json`, obfusqué).
- Versioning sémantique automatique (MAJOR.MINOR.PATCH.BUILD), numéro de build auto-incrémenté à chaque compilation.
- Documentation initiale : ROADMAP.md, CHANGELOG.md, README.md.

[Non publié]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.7.0...HEAD
[0.7.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.6.0...v0.7.0
[0.6.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.5.0...v0.6.0
[0.5.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.4.0...v0.5.0
[0.4.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.3.0...v0.4.0
[0.3.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/releases/tag/v0.1.0
