> From: https://chatgpt.com/c/6ae1f455-2fc0-83eb-87a2-c61a9296764d?temporary-chat=true

# you asked

message time: 2026-10-28 14:10:44

Das in Abbildung sieht auch soweit schon gut aus.
 Unter Berücksichtigung der Datei „Handbuch.md“- und „REPOSITORY_ANALYSE.md“, geht es in erster Linie um das Programm „TiaArchiveExporter“ und dient das der KI-Analyse zur Erstellung von Betriebsanleitungen und ich brauche das auch für das Marketing- Linkedin, Landingpage, Angebot?

Außerdem sollte noch erwähnt werden, was ein Sondermaschinenbauer einspart, wenn die SPS-Programmierer nicht mehr dokumentieren müssen.

---

# chatgpt response

Ja. Aus beiden Dateien ergibt sich ziemlich klar, dass der **TiaArchiveExporter nicht als „Dokumentationsprogramm“ im engeren Sinn positioniert werden sollte, sondern als technische Datengrundlage für eine nachgelagerte KI-gestützte Analyse und Dokumentation**. Er liest strukturierte Informationen aus TIA Portal aus und erzeugt daraus ein maschinenlesbares Archiv; die eigentliche Betriebsanleitung entsteht erst in einem nachgelagerten Analyse-/Dokumentationsprozess. Genau diese Abgrenzung steht auch im Handbuch. 

Die technische Stärke ist dabei wesentlich größer als „TIA-Daten exportieren“: Das Archiv kann Zusammenhänge wie **HMI-Bedienelement → HMI-Tag → Verbindung → PLC-Variable → Programmbaustein** nachvollziehbar machen und HMI, PLC, Hardware, Faceplates, Meldungen, Skripte und Beziehungen strukturiert bereitstellen.  Das Repository ist außerdem bereits darauf ausgerichtet, langfristig getrennte Exporter für mehrere TIA-Versionen zu ermöglichen, damit beispielsweise ältere Projekte nicht erst auf V21 migriert werden müssen. 

Für **LinkedIn, Landingpage und Angebot** würde ich deshalb nicht das Programm selbst in den Mittelpunkt stellen, sondern das wirtschaftliche Ergebnis:

> **Document: Positionierung TIA Archive Exporter**
> 
> ## Aus TIA-Projekten wird eine belastbare Datengrundlage für KI-Dokumentation
> 
> Der **TIA Archive Exporter** erschließt die technischen Informationen eines TIA-Portal-Projekts für eine strukturierte, KI-gestützte Analyse.
> 
> Statt Informationen manuell aus HMI-Bildern, SPS-Programmen, Tag-Tabellen, Alarmen, Hardwarekonfigurationen und Faceplates zusammenzusuchen, erzeugt der Exporter ein einheitliches, maschinenlesbares Projektarchiv.
> 
> Damit kann eine nachgelagerte KI technische Zusammenhänge nachvollziehen – beispielsweise:
> 
> **HMI-Bedienelement → HMI-Tag → SPS-Variable → Programmbaustein → Maschinenfunktion**
> 
> In Kombination mit Schaltplan, Konstruktion, Funktionsbeschreibung und weiteren freigegebenen Unterlagen entsteht daraus die Grundlage für detaillierte Maschinen- und Betriebsdokumentation.
> 
> ### Der Nutzen für Sondermaschinenbauer
> 
> Der entscheidende Vorteil liegt nicht nur in der automatisierten Datenerfassung, sondern in der Entlastung hochqualifizierter SPS-Programmierer.
> 
> Heute müssen SPS-Programmierer für Dokumentation häufig Informationen zusammensuchen, Screens erklären, Variablen und Funktionen zuordnen, Tabellen erstellen oder Rückfragen der technischen Dokumentation beantworten.
> 
> Diese Arbeit kann zu einem großen Teil vorbereitet und strukturiert werden.
> 
> **Das bedeutet: weniger Dokumentations-Fleißarbeit für SPS-Programmierer – und mehr Zeit für Entwicklung, Inbetriebnahme und Optimierung der Maschine.**
> 
> Der Exporter schafft dafür eine reproduzierbare technische Datenbasis. Änderungen am Projekt können erneut exportiert und anschließend nach demselben Schema analysiert werden.
> 
> ### Vom Engineering zur Betriebsanleitung
> 
> Der TIA Archive Exporter ist dabei ein Baustein einer größeren Prozesskette:
> 
> **TIA Portal + Schaltplan + Konstruktion + weitere technische Unterlagen**  
> ↓  
> **strukturierte technische Datenbasis**  
> ↓  
> **quellengebundene KI-Analyse**  
> ↓  
> **Entwurf von Maschinenbeschreibung und Betriebsanleitung**  
> ↓  
> **fachliche Prüfung und Freigabe**
> 
> Die KI ersetzt dabei weder die technische Prüfung noch die Verantwortung des Maschinenbauers. Sie übernimmt vor allem die zeitaufwendige Aufgabe, vorhandene technische Informationen zusammenzuführen, zu strukturieren und für die Dokumentation vorzubereiten.

Das passt sehr gut zu der Argumentation im bestehenden Handbuch: Dort wird ausdrücklich beschrieben, dass die Einsparung dadurch entsteht, dass Informationen **nicht mehr jedes Mal manuell aus verschiedenen Engineering-Ansichten zusammengesucht und in Tabellen übertragen werden müssen**.  Gleichzeitig bleibt die wichtige seriöse Einschränkung bestehen: Fachliche Bewertung, Sicherheitsprüfung und Freigabe werden nicht automatisiert. 

### Die Einsparung würde ich unbedingt konkreter machen

Für Marketing und insbesondere für Angebote ist der Satz „SPS-Programmierer müssen weniger dokumentieren“ noch zu abstrakt. Besser funktioniert ein **Zeit-/Kostenmodell**, ohne eine unbelegte feste Einsparung zu versprechen.

Ein Beispiel:

> Ein SPS-Programmierer kostet einen Sondermaschinenbauer intern beispielsweise 70–100 € pro Stunde. Wenn bei einer Maschine 15–30 Stunden für das manuelle Zusammentragen von HMI-Bildern, Variablen, Alarmen, Bausteinen und Funktionsinformationen anfallen, entstehen allein dafür etwa 1.050–3.000 € Engineering-Aufwand je Maschine.
>
> Wenn der TIA Archive Exporter zusammen mit der KI-Analyse einen wesentlichen Teil dieser vorbereitenden Dokumentationsarbeit übernimmt, wird diese Zeit nicht „wegrationalisiert“, sondern für wertschöpfendere Tätigkeiten frei: Programmierung, Inbetriebnahme, Optimierung und Fehleranalyse.

Die **70–100 € und 15–30 Stunden sind dabei Beispielannahmen von mir und nicht aus deinen Dateien abgeleitet**. Im Handbuch steht bewusst, dass die konkrete Zeitersparnis projekt- und prozessabhängig ist und keine pauschale Einsparung zugesichert werden sollte.  Für eine Landingpage kann man deshalb beispielsweise einen ROI-Rechner daraus machen:

**Einsparpotenzial pro Maschine = Dokumentationsstunden des SPS-Programmierers × interner Stundensatz × automatisierbarer Anteil**

Bei 25 Stunden, 85 €/h und beispielsweise 60 % vorbereitend automatisierbarer Arbeit wären das **1.275 € freigesetzte Engineering-Kapazität je Maschine**. Bei 40 Maschinen pro Jahr wären es **51.000 € pro Jahr**. Das sollte dann ausdrücklich als Rechenbeispiel und nicht als zugesicherte Einsparung bezeichnet werden.

Für die Kommunikation würde ich daraus drei unterschiedliche Kernbotschaften machen: **LinkedIn:** „Ihre SPS-Programmierer wurden zum Programmieren eingestellt – nicht zum Abschreiben von TIA-Projekten.“ **Landingpage:** „Vom TIA-Projekt zur strukturierten KI-Datenbasis für die Betriebsanleitung.“ **Angebot:** „Reduzierung manueller Engineering-Aufwände bei der technischen Bestandsaufnahme und Dokumentationsvorbereitung.“

Der stärkste Verkaufsansatz ist damit aus meiner Sicht nicht **„Wir haben einen TIA Exporter“**, sondern **„Wir holen die technische Dokumentationsarbeit aus den Köpfen Ihrer SPS-Programmierer und machen vorhandene Engineering-Daten systematisch für KI nutzbar.“** Der `TiaArchiveExporter` ist die technische Grundlage, die diesen Anspruch glaubwürdig macht.

---
Powered by [AI Exporter](https://saveai.net)