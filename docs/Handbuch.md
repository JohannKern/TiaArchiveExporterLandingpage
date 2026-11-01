# Handbuch – TIA Archive Exporter V21

## 1. Zweck und Nutzen

Der TIA Archive Exporter erstellt aus einem **geöffneten TIA-Portal-V21-Projekt**
ein strukturiertes, maschinenlesbares Projektarchiv. Er ist eine technische
Datenbasis für Analyse und Dokumentation – nicht selbst ein
KI-Handbuchgenerator und kein Ersatz für die Prüfung durch Fachpersonal.

Ein Screenshot zeigt, **was** gerade auf einem Bildschirm zu sehen ist. Das
Exportarchiv kann zusätzlich technische Zusammenhänge sichtbar machen:

> **HMI-Bedienelement → HMI-Tag → Verbindung → PLC-Variable → Programmbaustein**

Damit lässt sich eine Darstellung später besser in ihren technischen Kontext
einordnen. Je nach Projekt und auslesbaren Objekten enthält das Archiv unter
anderem HMI-Screens und ScreenItems, Tags, PLC-Zuordnungen und Verbindungen,
Faceplate-Informationen, Meldungen, Scripts, Text-/Grafiklisten, Hardware,
PLC-Bausteine sowie Beziehungs- und Exportberichte.

### Auf einen Blick

| Der Exporter leistet | Der Exporter leistet nicht |
|---|---|
| Liest strukturierte Projektinformationen über TIA Openness aus. | Erzeugt nicht automatisch ein fertiges Bedienerhandbuch. |
| Ordnet die Dateien in nachvollziehbaren Projektbereichen. | Ersetzt keine Screenshots, E-Pläne, Konstruktionsunterlagen oder Risikobeurteilung. |
| Schreibt Zusammenfassungen und einen Bericht über Exportstatus und Fehler. | Beweist nicht allein, dass eine abgeleitete Maschinenfunktion korrekt oder sicher ist. |
| Liefert eine wiederverwendbare Grundlage für eine spätere KI-Analyse. | Ändert oder programmiert die Maschine nicht. |

Der Nutzen für Sondermaschinenbauer liegt darin, dass wiederkehrendes
Zusammentragen und Zuordnen technischer Informationen deutlich besser
vorbereitet und teilweise automatisiert werden kann. Programmierer können
dadurch weniger Zeit für manuelle Bestandsdokumentation aufwenden und mehr Zeit
in Entwicklung, Inbetriebnahme und fachliche Prüfung investieren. Die konkrete
Zeitersparnis hängt vom Projekt und vom bisherigen Dokumentationsprozess ab;
eine pauschale Einsparung wird nicht zugesichert. Technische Verantwortung und
Freigabe bleiben bei den zuständigen Personen.

## 2. Voraussetzungen

- Windows-PC mit **TIA Portal V21 und TIA Openness V21**.
- Das betreffende Projekt ist in einer erreichbaren TIA-Portal-V21-Instanz
  geöffnet.
- Die GUI und `TiaArchiveExporter.V21.exe` sind gemeinsam verfügbar
  (im Release-Paket nebeneinander oder im passenden Build-Verzeichnis).
- Ein vorhandener Ordner mit Schreibberechtigung als Exportziel.
- Für eine spätere vollständige Maschinenbeschreibung zusätzlich die
  freigegebenen Unterlagen, die nicht Teil des TIA-Projekts sind, zum Beispiel
  Elektropläne, Konstruktionsunterlagen, Funktionsbeschreibungen sowie
  Pneumatik-/Hydraulikpläne.

Der aktuelle Release-Stand ist der **V21-Exporter**. Ein Exporter für andere
TIA-Versionen ist damit nicht zugesagt.

## 3. Bedienoberfläche – schematische Ansicht

Die folgende Darstellung ist eine Lesehilfe, kein Screenshot:

```text
+--------------------------------------------------------------+
| TIA Archive Exporter                                         |
|                                                              |
| TIA-Version   [ V21                                      ]   |
| Projekt       [ geöffnetes Projekt auswählen           v ]  |
|                               [ Aktualisieren ]              |
| Exportziel    [ Zielordner                                  ]|
|                               [ Durchsuchen... ]              |
|                                                              |
|                 [ Export starten ] [ Exportordner öffnen ]   |
|                 [======= Fortschrittsanzeige ========]       |
|                                                              |
| Status / Meldungen                                           |
| +----------------------------------------------------------+ |
| | erkannte Projekte, Exportfortschritt und Hinweise        | |
| +----------------------------------------------------------+ |
+--------------------------------------------------------------+
```

### Elemente der Oberfläche

- **TIA-Version** zeigt die gefundene Exporterversion. In diesem Release ist
  das V21.
- **Projekt** enthält die in geöffneten TIA-Instanzen erkannten Projekte.
- **Aktualisieren** liest die Projektliste erneut ein. Verwenden Sie dies,
  wenn Sie ein Projekt erst nach dem Start der GUI geöffnet haben.
- **Exportziel** und **Durchsuchen...** bestimmen den vorhandenen Ordner, in
  dem das Archiv angelegt wird.
- **Export starten** beginnt den Export des ausgewählten Projekts.
- **Fortschrittsanzeige** signalisiert während des laufenden Exports, dass die
  Arbeit noch läuft. Sie zeigt keinen prozentualen Fertigstellungsgrad an.
- **Exportordner öffnen** wird verfügbar, wenn ein erreichbarer Exportordner
  erkannt wurde.
- Das **Meldungsfeld** zeigt erkannte Projekte, Statusmeldungen und Fehler.

## 4. Schritt-für-Schritt: Export ausführen

1. Starten Sie TIA Portal V21 und öffnen Sie das gewünschte Projekt.
2. Starten Sie die GUI des TIA Archive Exporters.
3. Kontrollieren Sie, dass unter **TIA-Version** `V21` angezeigt wird.
4. Wählen Sie das richtige Projekt aus. Ist es nicht in der Liste, klicken Sie
   auf **Aktualisieren** und prüfen Sie, ob das Projekt in TIA weiterhin
   geöffnet ist.
5. Klicken Sie auf **Durchsuchen...** und wählen Sie einen vorhandenen
   Exportordner. Die GUI legt den gewählten Ordner nicht automatisch neu an;
   über den Ordnerdialog kann bei Bedarf ein neuer Ordner angelegt werden,
   bevor Sie ihn auswählen.
6. Prüfen Sie Projekt und Zielordner noch einmal und klicken Sie auf
   **Export starten**.
7. Warten Sie, bis die Fortschrittsanzeige beendet ist und eine Abschluss- oder
   Fehlermeldung im Meldungsfeld erscheint. Schließen Sie TIA währenddessen
   nicht.
8. Öffnen Sie mit **Exportordner öffnen** das Ergebnis oder navigieren Sie
   selbst zum gewählten Ziel.
9. Prüfen Sie in `90_Report\Summary.txt` die erfassten Zähler und in
   `90_Report\ExportReport.csv` die Status- und Fehlerdetails. Ein gestarteter
   Export ist nicht automatisch ein vollständig fehlerfreier Export.

**Wichtig:** Das Archiv wird als Unterordner mit Projektname und Zeitstempel im
gewählten Ziel angelegt. Bei nicht angegebenem Ziel verwendet der Exporter
standardmäßig `C:\TiaProjectArchive`.

## 5. So ist das Archiv aufgebaut

Die Hauptordner des Archivs sind nach Aufgabenbereichen getrennt:

```text
<Exportziel>\
└── <Projektname>_<Zeitstempel>\
    ├── 00_Project\      Projektinformationen
    ├── 10_PLC\          PLC-Geräte und Bausteinexporte
    ├── 20_HMI\          HMI-Geräte, Screens und HMI-Daten
    ├── 30_Hardware\     Hardware- und Geräteübersicht
    ├── 40_Library\      Projektbibliothek, u. a. Faceplates
    └── 90_Report\       Zusammenfassung und Exportbericht
```

| Ordner | Zweck und typische Inhalte |
|---|---|
| `00_Project` | Projektname, Projektpfad, Exportdatum und TIA-Version in `ProjectInfo.txt`. |
| `10_PLC` | PLC-Übersicht und exportierte PLC-Bausteine; Unterordner orientieren sich an den Geräten. |
| `20_HMI` | HMI-Inventar, Screens/ScreenItems, Tags, Verbindungen, Meldungen, Scripts, Text-/Grafiklisten, Faceplate-Instanzen und Beziehungen, soweit exportierbar. |
| `30_Hardware` | Geräteübersicht wie `Devices.csv`, Baumdarstellung wie `HardwareTree.txt` und gerätebezogene Details. |
| `40_Library` | Projektbibliotheksinhalte, darunter Faceplate-Typen und -Versionen, soweit verfügbar. |
| `90_Report` | `Summary.txt` mit Kennzahlen sowie `ExportReport.csv` mit einzelnen Exportstatusmeldungen. |

Das Beispiel im Handbuch bildet die Hauptstruktur ab. Welche einzelnen Dateien
und Datensätze enthalten sind, hängt vom Projekt, den vorhandenen Objekten und
dem erfolgreichen Zugriff über Openness ab. Prüfen Sie deshalb immer den
Exportbericht, statt aus einem vorhandenen Ordner auf Vollständigkeit zu
schließen.

## 6. Von Projektdaten zur verständlichen Maschinenbeschreibung

### Die technische Spur

Das Archiv ermöglicht eine strukturierte Nachverfolgung. Ein Analysewerkzeug
kann beispielsweise versuchen, folgende Kette aufzubauen:

```text
HMI-Screen
   │ enthält
   ▼
ScreenItem / Bedienelement
   │ verwendet
   ▼
HMI-Tag
   │ ist verbunden mit
   ▼
PLC-Variable
   │ wird verarbeitet in
   ▼
PLC-Baustein ──► fachlich bestätigte Funktionsbeschreibung
```

Die Kette ist nur so belastbar wie ihre tatsächlich exportierten Zuordnungen
und die ergänzenden Quellen. Ein ähnlicher Name allein beweist keine
funktionale Verbindung.

### Beispiel für eine belegbare Erklärung

| Dokumentationsaussage | Benötigter Beleg |
|---|---|
| „Auf dem Übersichtsbild wird der Zustand des Aggregats angezeigt.“ | Zugehöriger Screen und ScreenItem mit Beschriftung/Anzeigeeigenschaft. |
| „Der angezeigte Wert kommt vom PLC-Tag `…`.“ | HMI-Tag und aufgelöste Verbindung zum PLC-Tag. |
| „Der PLC-Tag wird im Baustein `…` ausgewertet.“ | PLC-Referenz und Bausteininhalt oder ein weiterer eindeutiger Quellennachweis. |
| „Das Aggregat wird durch diesen Ablauf eingeschaltet.“ | Funktionsbeschreibung und/oder geprüfte PLC-Logik; bloße Namensähnlichkeit genügt nicht. |
| „Bei Alarm `…` ist Maßnahme `…` erforderlich.“ | Freigegebene Alarm-/Störungsbeschreibung oder Herstellerunterlage. Aus einem Alarmnamen allein darf keine Maßnahme abgeleitet werden. |

### Ergänzende Unterlagen gezielt zuordnen

Für eine verständliche Maschinen- und Bedienerdokumentation sollten Sie das
TIA-Archiv mit den freigegebenen Quellen zusammenführen:

1. **E-Plan und Hardwareunterlagen** zur Einordnung von Geräten, Sensoren,
   Aktoren und elektrischen Kennzeichnungen.
2. **Konstruktionsunterlagen** zur mechanischen Maschinenstruktur und
   Komponentenbezeichnung.
3. **Funktionsbeschreibung und Betriebsartenbeschreibung** zur fachlichen
   Erklärung von Abläufen, Automatik, Einrichten und Handbetrieb.
4. **Pneumatik-/Hydraulikpläne** zur Beschreibung fluidischer Funktionen.
5. **Sicherheitskonzept, Risikobeurteilung und freigegebene
   Herstellerunterlagen** für sicherheitsrelevante Aussagen.

Eine KI kann aus dieser Kombination beispielsweise Kapitel zu HMI-Bildern,
Navigationswegen, Anzeigen, Bedienelementen, nachvollziehbaren
Tag-/PLC-Zuordnungen, Faceplates, Alarmen und typischen Bedienabläufen
vorbereiten. Das setzt voraus, dass die dafür nötigen Quellen im Paket
enthalten und ihre Aussagen überprüft sind. Das Ergebnis muss fachlich geprüft
und freigegeben werden. Der Exporter erzeugt selbst keine DOCX- oder
PDF-Bedienungsanleitung.

## 7. Regeln für eine quellengebundene KI-Analyse

Damit aus einer Analyse keine plausibel klingenden, aber unbelegten Aussagen
werden, sollten Sie für jeden wiederkehrenden Analyseauftrag feste Regeln
verwenden:

1. **Nur gelieferte Quellen verwenden.** Jede technische Behauptung muss auf
   eine konkrete Datei bzw. ein konkretes Objekt im Export oder in den
   ergänzenden Unterlagen zurückführbar sein.
2. **Belege angeben.** Nennen Sie möglichst Dateipfad, Objektname, Tag,
   Baustein, Planseite oder Abschnitt.
3. **Lücken sichtbar machen.** Wenn eine gewünschte Aussage in den gelieferten
   Quellen nicht belegt ist, schreiben Sie ausdrücklich:
   **NICHT AUS DEN QUELLEN ERMITTELBAR**.
4. **Beobachtung und Interpretation trennen.** Exportierte Namen und
   Verbindungen sind Beobachtungen; ihre Bedeutung für die Maschine ist eine
   Interpretation, die einen zusätzlichen Beleg und eine Prüfung benötigen
   kann.
5. **Widersprüche nicht auflösen oder erraten.** Abweichende Bezeichnungen
   zwischen HMI, SPS, E-Plan und Konstruktion als Klärungspunkt aufführen.
6. **Sicherheit nicht aus Code ableiten.** Not-Halt, Schutztüren, sichere
   Bewegungen, Freigaben, Gefahrenbereiche und vorgeschriebene Handlungen
   ausschließlich anhand des freigegebenen Sicherheitskonzepts, der
   Risikobeurteilung und maßgeblicher Herstellerunterlagen beschreiben.

Beispiel für die Kennzeichnung:

> **Ursache:** NICHT AUS DEN QUELLEN ERMITTELBAR.  
> **Beleglage:** Im Export ist die HMI-Meldung `…` mit dem Meldebit `…`
> dokumentiert. Eine freigegebene Störungsbeschreibung wurde nicht
> bereitgestellt.

## 8. Was ein Sondermaschinenbauer dadurch gewinnen kann

Die Einsparung entsteht nicht dadurch, dass Dokumentation oder Prüfung
entfallen, sondern dadurch, dass Informationen nicht jedes Mal von Hand aus
verschiedenen Engineering-Ansichten zusammengesucht und in neue Tabellen
übertragen werden müssen.

- **Weniger wiederkehrende Fleißarbeit:** Tags, Screens, Verbindungen,
  Bausteine und Meldungen lassen sich strukturiert als Ausgangsmaterial
  bereitstellen.
- **Schnellerer Einstieg in die Dokumentation:** Eine einheitliche
  Archivstruktur erleichtert die Zuordnung und den Vergleich von Projekten.
- **Weniger Medienbrüche:** Technische Kennungen können aus dem Projekt
  übernommen und mit den Bezeichnungen aus E-Plan und Konstruktion
  abgeglichen werden.
- **Bessere Wartbarkeit:** Bei Änderungen kann ein neuer Export als
  aktualisierte technische Grundlage dienen; eine manuelle Prüfung der
  resultierenden Dokumentation bleibt notwendig.
- **Mehr Zeit für Engineering:** Programmierer können weniger Aufwand in das
  manuelle Erstellen wiederkehrender Bestandslisten und mehr in Entwicklung,
  Inbetriebnahme und technische Qualität investieren.

Nicht eingesparte Tätigkeiten sind die fachliche Bewertung, die Verifikation
an der realen Maschine, die Sicherheitsprüfung sowie die Freigabe der
Betriebsanleitung. Die gewonnene Zeit ist daher eine **Verschiebung von
manueller Datensammlung zu qualifizierter Prüfung**, nicht die Abschaffung
verantwortlicher Dokumentation.

## 9. Fehlersuche

| Beobachtung | Prüfen |
|---|---|
| V21-Exporter nicht gefunden | Liegt `TiaArchiveExporter.V21.exe` neben der GUI oder ist der passende Build vorhanden? |
| Kein geöffnetes TIA-V21-Projekt gefunden | Ist TIA Portal V21 gestartet und das gewünschte Projekt geöffnet? Danach **Aktualisieren** anklicken. |
| Projektliste bleibt leer oder schlägt fehl | Prüfen Sie TIA-/Openness-Installation, Erreichbarkeit der TIA-Instanz und Meldungen im Statusfeld. |
| Exportziel wird abgelehnt | Wählen Sie einen existierenden Ordner, auf den Ihr Benutzerkonto zugreifen kann. |
| Export endet mit Fehlern | Öffnen Sie `90_Report\Summary.txt` und `90_Report\ExportReport.csv`; prüfen Sie die dort genannten Kategorien, Objekte und Details. |
| Exportordner lässt sich nicht öffnen | Prüfen Sie, ob der Export abgeschlossen ist und der Zielordner erreichbar ist. |

Bei fehlgeschlagenen Einzelobjekten ist der Gesamtexport nicht automatisch
unbrauchbar; die fehlenden Inhalte müssen jedoch vor einer darauf gestützten
Dokumentation bewertet und gegebenenfalls nachgeliefert werden.

## 10. Begriffe

- **TIA Openness:** Siemens-Schnittstelle, über die der Exporter auf Inhalte
  einer laufenden TIA-Portal-Instanz zugreift.
- **HMI-Tag:** Im HMI verwendetes Datenobjekt, das je nach Projekt mit einer
  PLC-Variablen oder einer anderen Quelle verbunden sein kann.
- **ScreenItem:** Einzelnes Element eines HMI-Bildes, zum Beispiel eine
  Anzeige, Schaltfläche oder grafische Komponente.
- **Faceplate:** Wiederverwendbare HMI-Komponente, beispielsweise für einen
  Motor oder ein Ventil. Die tatsächliche Bedeutung seiner Schnittstellen
  muss anhand der Bindings und Funktionsquellen überprüft werden.
- **PLC-Baustein:** Programmobjekt der speicherprogrammierbaren Steuerung,
  dessen Funktion aus Typ, Inhalt und Projektzusammenhang zu beurteilen ist.
- **Exportbericht:** `90_Report\ExportReport.csv`; protokolliert Ergebnisse
  und Details zu einzelnen Exportobjekten.
