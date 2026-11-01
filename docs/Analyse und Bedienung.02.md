# **Beschreibung des Programms**

Der **TIA Archive Exporter** ist ein Windows-Programm, das Informationen aus einem **bereits geöffneten Siemens TIA-Portal-Projekt** automatisch ausliest und als übersichtliches Dateiarchiv ablegt.

Der eigentliche Zweck des Exports besteht darin, die technischen Projektdaten so aufzubereiten, dass sie anschließend von einer **KI analysiert und für die Erstellung einer qualitativ hochwertigen HMI-Betriebsanleitung verwendet werden können**.

Dazu liest der Exporter gezielt Informationen aus dem TIA-Projekt aus, zum Beispiel zu **HMI-Bildern, Bedienobjekten, Meldungen, Variablen, SPS-Bausteinen, Hardware und verwendeten Bibliotheken**. Die Daten werden strukturiert abgelegt, damit die KI einen möglichst vollständigen Überblick über die Bedienoberfläche und die dahinterliegenden Anlagenfunktionen erhält.

Das Ziel ist daher nicht nur eine Sicherung von Projektdaten. Der Exporter bildet vielmehr die **technische Datengrundlage für die spätere Dokumentation**. Aus den exportierten Informationen kann nachvollzogen werden, welche HMI-Seiten vorhanden sind, welche Funktionen bedient werden können, welche Meldungen auftreten und welche technischen Zusammenhänge dahinterstehen.

Für den technischen Redakteur bedeutet das, dass die benötigten Informationen nicht mühsam einzeln aus dem TIA-Projekt zusammengesucht werden müssen. Stattdessen erzeugt der Exporter eine strukturierte Grundlage, die von einer KI ausgewertet und für die Erstellung einer verständlichen und möglichst anlagennahen HMI-Betriebsanleitung verwendet werden kann.

Die Bedienung des Exporters selbst ist dabei bewusst einfach gehalten. Im normalen Ablauf wird das richtige TIA-Projekt geöffnet, der Exporter gestartet und der Export durchgeführt. Die technische Aufbereitung der Projektdaten erfolgt anschließend automatisch.

So ist es deutlich näher an einer echten **Produkt- bzw. Funktionsbeschreibung** und weniger an einer Beschreibung des Archivinhalts.

Wenn du möchtest, kann ich im gleichen Stil jetzt direkt den Abschnitt **„Bedienung“** anschließen.

***

# **Bedienablauf**

## Bedienung

Für den Export muss das gewünschte Projekt zunächst im **Siemens TIA Portal** geöffnet sein. Der TIA Archive Exporter greift auf dieses bereits geöffnete Projekt zu und liest die benötigten Informationen daraus aus.

### 1. TIA Archive Exporter starten

Nach dem Start versucht der TIA Archive Exporter automatisch, eine laufende TIA-Portal-Instanz und ein darin geöffnetes Projekt zu finden.

Kann noch nicht auf TIA Portal zugegriffen werden, bleibt das Feld **„Projekt“** zunächst leer. Im unteren Bereich des Fensters wird angezeigt, dass noch kein geöffnetes bzw. erreichbares Projekt gefunden wurde.

![](media/3e77bdddf56b5379e9016c277cbdd530.png)

Abbildung 1: TIA Archive Exporter nach dem Start – noch ohne Zugriff auf das geöffnete TIA-Projekt.

Das ist beim ersten Start nicht unbedingt ein Fehler. TIA Portal muss dem Exporter zunächst erlauben, über **TIA Openness** auf das Projekt zuzugreifen.

***

### 2. Zugriff auf TIA Portal erlauben

Sobald der Exporter auf TIA Portal zugreifen möchte, erscheint in TIA Portal die Sicherheitsabfrage **„Openness Zugriff“**.

Hier wird festgelegt, ob der TIA Archive Exporter auf die geöffnete TIA-Portal-Instanz zugreifen darf.

![](media/7006dbba711a322cf6a1dd9038f93b57.png)

Abbildung 2: Sicherheitsabfrage von TIA Portal für den Zugriff durch den TIA Archive Exporter.

Für die normale Verwendung muss der Zugriff erlaubt werden.

Mit **„Ja“** wird der Zugriff für diesen Vorgang freigegeben.

Mit **„Ja, alle“** wird der Zugriff erlaubt und die Freigabe gespeichert. Dadurch muss die Abfrage bei weiteren Zugriffen normalerweise nicht erneut bestätigt werden.

Mit **„Nein“** wird der Zugriff verweigert. In diesem Fall kann der Exporter das TIA-Projekt nicht auslesen.

***

### 3. TIA-Projekt auswählen

Nach erfolgreicher Freigabe erkennt der Exporter das geöffnete TIA-Projekt. Dieses wird im Feld **„Projekt“** angezeigt.

Sind mehrere geeignete Projekte bzw. TIA-Instanzen vorhanden, kann das gewünschte Projekt über das Auswahlfeld ausgewählt werden.

Über **„Aktualisieren“** kann die Suche nach geöffneten Projekten erneut durchgeführt werden.

**Bild einfügen:** `TiaArchiveExporter.03.png`

![](media/cc9cd866b702f21345db7e6856b65d46.png)

Abbildung 3: Das geöffnete TIA-Projekt wurde erkannt und kann für den Export verwendet werden.

Vor dem Export sollte kurz geprüft werden, ob im Feld **„Projekt“** tatsächlich das Projekt angezeigt wird, aus dem später die HMI-Dokumentation erstellt werden soll.

***

### 4. Speicherort für den Export festlegen

Im Feld **„Exportziel“** wird festgelegt, wo die ausgelesenen Projektdaten gespeichert werden.

Über die Schaltfläche **„Durchsuchen…“** kann der gewünschte Speicherort ausgewählt werden. Der Exporter legt dort die benötigte Ordnerstruktur für das Projekt automatisch an.

![](media/00c9263f66106826a89020dbc285d6d4.png)

Abbildung 4: Auswahl des Speicherortes für die exportierten Projektdaten.

Der Bediener muss die einzelnen Unterordner nicht selbst anlegen. Sie werden beim Export automatisch erzeugt.

Diese Ordner bilden später die strukturierte Datengrundlage für die **KI-Analyse und die Erstellung der HMI-Betriebsanleitung**.

***

### 5. Export starten

Sind das richtige Projekt und der gewünschte Speicherort ausgewählt, wird der Vorgang mit **„Export starten“** begonnen.

Ab diesem Zeitpunkt liest der Exporter die benötigten Informationen automatisch aus dem TIA-Projekt aus. Im unteren Bereich des Fensters kann verfolgt werden, welche Projektbereiche gerade verarbeitet werden.

**Bild einfügen:** `TiaArchiveExporter.04.png`

![](media/7ce7f5dc65b21b7e60a81e904f8c04aa.png)

Abbildung 5: Laufender Export – im unteren Bereich werden die bereits bearbeiteten Projektdaten angezeigt.

Während des Exports ist normalerweise keine weitere Bedienung erforderlich.

**Wichtig:** TIA Portal und das geöffnete Projekt sollten während des Exports nicht geschlossen werden.

Der Exporter sammelt dabei die für die spätere Dokumentation wichtigen Informationen, beispielsweise aus den Bereichen **HMI, SPS, Hardware und Projektbibliothek**.

***

### 6. Export abschließen und Ergebnis öffnen

Nach erfolgreichem Abschluss meldet der Exporter, dass der Export beendet wurde.

Über **„Exportordner öffnen“** kann anschließend direkt der erzeugte Projektordner im Windows-Explorer geöffnet werden.

**Bild einfügen:** `TiaArchiveExporter.05.png`

![](media/5d93ab8c145ec5916aec3bb0d4d0627e.png)

Abbildung 6: Erfolgreich abgeschlossener Export und geöffneter Exportordner.

Im Exportordner sind die Projektdaten nach technischen Bereichen gegliedert. Beispielsweise entstehen Ordner für **Projektinformationen, SPS, HMI, Hardware, Bibliotheken und Auswertungen**.

Diese Dateien sind nicht in erster Linie dafür gedacht, vom Bediener einzeln ausgewertet zu werden. Sie bilden die **technische Informationsbasis für die anschließende KI-Analyse**.

Die KI kann dadurch die im TIA-Projekt vorhandenen HMI-Seiten, Bedienfunktionen, Meldungen, Variablen und technischen Zusammenhänge wesentlich systematischer erfassen. Auf dieser Grundlage kann anschließend eine **detaillierte und möglichst genau zur tatsächlichen Anlage passende HMI-Betriebsanleitung** erstellt werden.

### Bedienablauf in Kurzform

Für den Anwender besteht der gesamte Vorgang damit im Wesentlichen aus:

**TIA-Projekt öffnen → TIA Archive Exporter starten → Openness-Zugriff erlauben → Projekt prüfen → Exportziel auswählen → Export starten → Exportordner öffnen.**

Die eigentliche technische Auswertung und Aufbereitung der Projektdaten übernimmt der Exporter automatisch.

**Die Bildreihenfolge würde ich also bewusst als** `01 → 02 → 03 → 00 → 04 → 05` **verwenden.** Die Dateinummern selbst entsprechen nämlich nicht vollständig der tatsächlichen Bedienreihenfolge.

So bekommt man eher eine **bebilderte Arbeitsanweisung** als eine klassische Softwarebeschreibung – und ein Monteur, Inbetriebnehmer oder technischer Redakteur kann den Ablauf anhand der Bildschirmbilder praktisch nachmachen.
