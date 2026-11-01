# TIA Archive Exporter – Landingpage

Statische Landingpage und Bedienungsanleitung für den TIA Archive Exporter. Es werden keine Frameworks oder Build-Schritte benötigt.

## Aufrufbare Seiten

### Lokal testen

1. In VS Code den Ordner `Landingpage` öffnen und über **Terminal → Neues Terminal** ein integriertes Terminal starten. Das Terminal muss im Projektordner stehen, in dem diese README liegt.
2. Den lokalen HTTP-Server starten:

```powershell
python -m http.server 8000
```

Das Terminal während des Tests geöffnet lassen. Anschließend im Browser öffnen:

- [Startseite lokal](http://localhost:8000/) – leitet zur Landingpage weiter
- [Landingpage lokal](http://localhost:8000/tia-archive-exporter-landingpage.html)
- [Bedienungsanleitung lokal](http://localhost:8000/tia-archive-exporter-bedienungsanleitung.html)

Falls `python` unter Windows nicht verfügbar ist, kann alternativ `py -m http.server 8000` verwendet werden, sofern der Python-Launcher installiert ist. Den Server im Terminal mit **Strg+C** beenden. Danach ist `http://localhost:8000/` nicht mehr erreichbar; zum erneuten Testen den Server wieder starten.

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
