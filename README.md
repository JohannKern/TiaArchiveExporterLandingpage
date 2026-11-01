# TIA Archive Exporter – Landingpage

Statische Landingpage und Bedienungsanleitung für den TIA Archive Exporter. Es werden keine Frameworks oder Build-Schritte benötigt.

## Aufrufbare Seiten

### Lokal testen

1. In VS Code den Workspace-Hauptordner öffnen und über **Terminal → Neues Terminal** ein integriertes Terminal starten. Das Terminal steht dann normalerweise im Workspace-Hauptordner `TiaArchiveExporter_Landingpage`.
2. Den Server mit dem Unterordner `Landingpage` als Web-Root starten:

```powershell
python -m http.server 8000 --directory .\Landingpage
```

Falls das Terminal bereits im Ordner `Landingpage` steht, genügt stattdessen:

```powershell
python -m http.server 8000
```

Wichtig: Wird `python -m http.server 8000` im Workspace-Hauptordner ohne `--directory` gestartet, liegen die HTML-Dateien unter `/Landingpage/`. Dann führt die direkte URL ohne diesen Unterordner zu einem 404.

Das Terminal während des Tests geöffnet lassen. Anschließend im Browser öffnen:

- [Startseite lokal](http://localhost:8000/) – leitet zur Landingpage weiter
- [Landingpage lokal](http://localhost:8000/tia-archive-exporter-landingpage.html)
- [Bedienungsanleitung lokal](http://localhost:8000/tia-archive-exporter-bedienungsanleitung.html)

Falls `python` unter Windows nicht verfügbar ist, kann alternativ `py -m http.server 8000 --directory .\Landingpage` verwendet werden, sofern der Python-Launcher installiert ist. Den Server im Terminal mit **Strg+C** beenden. Danach ist `http://localhost:8000/` nicht mehr erreichbar; zum erneuten Testen den Server wieder starten.

### Öffentlich über GitHub Pages

Vorgesehene URLs:

- [GitHub-Pages-Startseite](https://johannkern.github.io/TiaArchiveExporterLandingpage/)
- [Landingpage direkt](https://johannkern.github.io/TiaArchiveExporterLandingpage/tia-archive-exporter-landingpage.html)
- [Bedienungsanleitung direkt](https://johannkern.github.io/TiaArchiveExporterLandingpage/tia-archive-exporter-bedienungsanleitung.html)

**Veröffentlichungsstatus:** Die Website ist veröffentlicht. Der erste GitHub-Pages-Deployment-Lauf war erfolgreich.

## Dateien

- `index.html` – relativer Weiterleitungseinstieg zur Landingpage mit Link-Fallback
- `tia-archive-exporter-landingpage.html` – Produkt-Landingpage
- `tia-archive-exporter-bedienungsanleitung.html` – Anleitung mit eingebetteten Screenshots

## Repository

[JohannKern/TiaArchiveExporterLandingpage auf GitHub](https://github.com/JohannKern/TiaArchiveExporterLandingpage)
