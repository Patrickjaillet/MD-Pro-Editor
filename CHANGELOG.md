# Changelog

All notable changes to MD Pro Editor are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

## [0.8.0] - 2026-07-22

### Fixed

- **Major fix**: the text editor (Markdown area) did not display at all — no text, no background, no line numbers — because the `MarkdownTextEditor` subclass did not pick up AvaloniaEdit's visual theme (missing `StyleKeyOverride`, an Avalonia mechanism required for a derived control to inherit its base class's `ControlTemplate`). This bug had been present since Phase 1 but went unnoticed without real visual verification until this phase.
- Missing `AvaloniaEdit` theme inclusion (`avares://AvaloniaEdit/Themes/...`) added to `App.axaml`, a prerequisite for the editor to render at all.
- Fixed a startup crash (`ArgumentException: Invalid document`) caused by the code-folding manager becoming desynchronized when a tab's document changed; the manager is now cleanly reinstalled on every document change.
- Fixed a visual overlap between the system title text and the main window's custom title bar (`WindowDecorations="BorderOnly"`).
- Fixed a permanent lockup on the activation window for already-activated users: the license check ran before the unlock event subscription was wired up.
- Fixed an exception when rewriting the anti-fraud state file once it was already marked hidden/system.

### Added

- "About" tab in the application: logo, copyright, email, website, automatically displayed version number.
- Support for opening a file passed as a command-line argument (required for `.md` file association to actually work).
- Public GitHub repository [`Patrickjaillet/MD-Pro-Editor`](https://github.com/Patrickjaillet/MD-Pro-Editor) created (documentation and releases only, no source code).
- Complete README.md with overview, features, real application screenshot, download link, and PayPal link.

### Known limitations

- Screenshots and visual checks were performed manually on this machine; this major fix underlines the importance of regular visual testing, which remains to be automated.

## [0.7.0] - 2026-07-22

### Added

- Application logo/icon (multi-resolution .ico, 16 to 256 px).
- Complete Windows installer via Inno Setup: installs to Program Files, Desktop and Start Menu shortcuts, optional `.md`/`.markdown` file association, clean uninstaller.
- Self-contained publish (bundled .NET runtime): no prerequisite installation required for end users.
- Digital signature of the executable and the installer.
- `installer/build-installer.ps1` script automating publish, signing, and installer compilation for future releases.
- `LICENSE.txt` (end user license agreement) included in the installer.

### Known limitations

- Signing uses a self-signed test certificate: Windows SmartScreen will show a warning during installation until a code-signing certificate purchased from a recognized authority is used.
- Installation tested under real conditions on Windows 10 Enterprise LTSC (this machine). Testing on consumer Windows 10 and Windows 11 remains to be done on dedicated machines before official release.

## [0.6.0] - 2026-07-22

### Added

- Free 7-day trial with no functional limitations whatsoever.
- "Purchase / Activation" window opening before the main window: days remaining in trial, PayPal purchase button (€2.99), license code entry, "resend code by email" link.
- Machine identification (hashed CPU + disk volume hardware fingerprint) and system clock tampering detection to curb trial abuse.
- Dual anti-fraud storage of the first-run date (Windows registry + hidden file), with self-healing in case of inconsistency between the two.
- Offline license key generation and validation (`MDPE-XXXX-XXXX-XXXX` format, tied to the buyer's email).
- Application lockout after trial expiration without an active license: mandatory return to the activation window.
- Internal command-line tool (`tools/LicenseKeyGeneratorTool`) to generate a license key from a buyer's email after receiving a PayPal payment.

### Known limitations

- No server-side timestamp verification in case of clock tampering: detection relies solely on the last known local timestamp (sufficient against casual abuse, not against a determined attacker).
- License key delivery after payment: manual process only (no automated PayPal IPN webhook yet).
- License key protection is reasonable for an independent shareware title, not tamper-proof against reverse engineering.

## [0.5.0] - 2026-07-22

### Added

- Workspace ("Vault") management with automatic restoration of the last opened folder on startup.
- Wiki-style internal links `[[Name]]` with type-ahead autocompletion and a "Create missing notes" command to generate non-existent target notes.
- Backlinks panel showing which files reference the current document.
- Image handling: direct paste from the clipboard (Ctrl+V) and drag & drop from Windows Explorer, automatically copied into an `assets/` folder relative to the document.
- Image resizing directly in the preview (drag the image corner), reflected back into the source Markdown.
- YAML frontmatter editor with a visual key/value form.
- Reusable templates and snippets system, manageable via a dedicated window and insertable from the Command Palette.
- Preview CSS themes (Light, Sepia, Dark) and import of a custom stylesheet.
- Global search across all Markdown files in the workspace, with direct navigation to the matching line.
- Export to standalone HTML (inlined CSS), PDF (faithful print of the preview), DOCX (native Word via OpenXML), and EPUB.

### Known limitations

- Note graph view not implemented (a substantial undertaking, deferred).
- Visual table editor not implemented (tables are edited as raw Markdown for now).
- FR/EN spelling and grammar checker not implemented (requires bundling dictionaries).
- DOCX/HTML to Markdown import not implemented (only export is available).
- Git integration and internal plugin system not implemented.
- Standalone HTML export still depends on a CDN for KaTeX/Mermaid/Prism (same as the preview).

## [0.4.0] - 2026-07-22

### Added

- Full Fluent Design v2 theme with a Mica backdrop (automatic fallback to Acrylic/Blur on OSes that don't support it) and a custom title bar.
- Command Palette (Ctrl+Shift+P) for quick access to all main actions.
- Floating contextual toolbar on text selection (bold, italic, link, highlight), Notion-style.
- Side file explorer: open folder, tree view, open file on double-click, inline rename (F2), drag & drop Windows files to open them directly.
- Tabs reorderable via drag & drop.
- Focus / Distraction-free mode: dims text outside the paragraph currently being edited.
- Typewriter mode: vertically centers the active line while typing.
- Outline (TOC) panel automatically generated from headings, one-click navigation.
- Estimated reading time added to the status bar.
- Consistent Fluent vector icons throughout the interface (toolbar, explorer, tabs).
- Preferences window: font customization (editor and preview, size and family) and keyboard shortcuts (combination capture, persisted in settings.json).
- Micro-animations on buttons, toggles, and panels.

### Known limitations

- Internal drag & drop reordering of the file explorer not implemented (only drag & drop opening from Windows Explorer is available).
- Tab hover preview not implemented.
- Drag & drop reordering of outline sections not implemented.
- Custom keyboard shortcuts are applied on the next application restart.

## [0.3.0] - 2026-07-22

### Added

- Full Markdown rendering engine via Markdig (tables, task lists, footnotes, YAML frontmatter, autolinks, emoji, math, diagrams).
- Real-time HTML preview in a native WebView (Microsoft Edge WebView2 on Windows), with a 300 ms debounce to stay smooth on large documents.
- Scroll sync from the editor to the preview.
- Split View / Source View toggle (show or hide the preview).
- Rendering of math formulas (KaTeX) and Mermaid diagrams.
- Multi-language syntax highlighting of code blocks in the preview (Prism.js).
- GFM tables with alignment, and task list checkboxes clickable directly from the preview (reflected back into the source document).
- Preview zoom (Ctrl + scroll wheel, +/− buttons) and direct printing from the preview.

### Known limitations

- Scroll sync is only active from the editor to the preview (reverse direction deferred).
- "Live Preview / WYSIWYG hybrid" mode, Typora-style, is deferred to a later phase.
- KaTeX, Mermaid.js, and Prism.js are loaded from a CDN: an internet connection is required for a fully enriched preview (raw Markdown text always remains visible in the editor offline).

## [0.2.0] - 2026-07-22

### Added

- Full Markdown syntax highlighting (headings, bold, italic, inline code, code blocks, links, images, quotes, lists, tasks, tables, YAML frontmatter).
- Code folding by heading section (`#` through `######`).
- Smart indentation for lists and sublists (Tab / Shift+Tab).
- Auto-closing pairs `**`, `_`, `` ` ``, `[]`, `()`, `{}`.
- List auto-continuation (bulleted, numbered, tasks) on Enter.
- Built-in search and replace (AvaloniaEdit search panel, regex, case, whole word).
- Multi-tab support: several documents open at once, with an unsaved-changes indicator.
- Configurable autosave (interval and on window focus loss).
- Local per-file version history (lightweight "Time Machine" style, 50 snapshots retained).

### Known limitations

- Simultaneous multiple cursors not available (AvaloniaEdit limitation); native rectangular selection (Alt+drag) remains usable.
- Minimap and Markdown syntax error highlighting deferred to a later phase.

## [0.1.0] - 2026-07-22

### Added

- Created the .NET 10 (LTS) solution with the Avalonia projects: App, Core, Editor, Preview, UI, Licensing, Export, Plugins.
- Integrated FluentAvalonia and the Fluent Design v2 theme (light only).
- Set up the MVVM architecture (CommunityToolkit.Mvvm) with dependency injection (Microsoft.Extensions.DependencyInjection).
- Main window with a resizable 3-zone layout: File Explorer | Editor | Preview.
- Initial integration of AvaloniaEdit as the editing component (MarkdownTextEditor).
- Internal logging system with automatic file rotation (14-day retention, `%AppData%\MDProEditor\logs`).
- Persistent user configuration system (`%AppData%\MDProEditor\settings.json`, obfuscated).
- Automatic semantic versioning (MAJOR.MINOR.PATCH.BUILD), build number auto-incremented on every compilation.
- Initial documentation: ROADMAP.md, CHANGELOG.md, README.md.

[Unreleased]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.8.0...HEAD
[0.8.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.7.0...v0.8.0
[0.7.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.6.0...v0.7.0
[0.6.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.5.0...v0.6.0
[0.5.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.4.0...v0.5.0
[0.4.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.3.0...v0.4.0
[0.3.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/Patrickjaillet/MD-Pro-Editor/releases/tag/v0.1.0
