# TIA Archive Exporter – Landingpage

Statische Landingpage und Bedienungsanleitung für den TIA Archive Exporter. Es werden keine Frameworks oder Build-Schritte benötigt.

## Aufrufbare Seiten

### Lokal testen

Im Ordner `Landingpage` einen lokalen HTTP-Server starten:

```powershell
python -m http.server 8000
```

Anschließend im Browser öffnen:

- [Startseite lokal](http://localhost:8000/) – leitet zur Landingpage weiter
- [Landingpage lokal](http://localhost:8000/tia-archive-exporter-landingpage.html)
- [Bedienungsanleitung lokal](http://localhost:8000/tia-archive-exporter-bedienungsanleitung.html)

Falls `python` unter Windows nicht verfügbar ist, kann alternativ `py -m http.server 8000` verwendet werden, sofern der Python-Launcher installiert ist. Den Server im Terminal mit `Strg+C` beenden.

### Öffentlich über GitHub Pages

Vorgesehene URLs:

- [GitHub-Pages-Startseite](https://johannkern.github.io/TiaArchiveExporter/)
- [Landingpage direkt](https://johannkern.github.io/TiaArchiveExporter/tia-archive-exporter-landingpage.html)
- [Bedienungsanleitung direkt](https://johannkern.github.io/TiaArchiveExporter/tia-archive-exporter-bedienungsanleitung.html)

**Veröffentlichungsstatus:** Diese Links werden erst erreichbar, wenn das Repository öffentlich ist und GitHub Pages aktiviert wurde. Die Projektseite muss unter **Settings → Pages → Build and deployment** mit **Deploy from a branch**, Branch **`main`** und Ordner **`/(root)`** eingerichtet werden. Für ein öffentlich erreichbares Pages-Angebot muss dieses persönliche Repository öffentlich sein.

## Dateien

- `index.html` – relativer Weiterleitungseinstieg zur Landingpage mit Link-Fallback
- `tia-archive-exporter-landingpage.html` – Produkt-Landingpage
- `tia-archive-exporter-bedienungsanleitung.html` – Anleitung mit eingebetteten Screenshots

## Repository

[JohannKern/TiaArchiveExporter auf GitHub](https://github.com/JohannKern/TiaArchiveExporter)
