> From: https://chatgpt.com/c/6ae09949-84e4-83eb-a754-a2437af5ecc6?temporary-chat=true

# you asked

message time: 2026-10-27 13:30:01

Machen wir weiter

---

# chatgpt response

Ja. Wir machen genau dort weiter.

Der letzte bestätigte Stand ist: Der Export **einer einzelnen verwendeten Faceplate-Version als XML funktioniert**, und als Nächstes wollten wir die **40 tatsächlich verwendeten Faceplate-Typversionen gezielt exportieren** – ohne den kompletten Projektlauf. 

Falls du die zuletzt vorbereitete `Program.cs` bereits eingesetzt hast, führe jetzt nur aus:

```powershell
cd C:\Users\Administrator\sources\TiaOpennessTest
dotnet build
dotnet run -- faceplate-library-used
```

Wichtig: **nicht** einfach `dotnet run`, sondern ausdrücklich:

```powershell
dotnet run -- faceplate-library-used
```

Das gewünschte Ergebnis am Ende ist ungefähr:

```text
ERGEBNIS FACEPLATE-LIBRARY-USED-EXPORT
  Verwendete Versionen: 40
  Exportiert:           40
  Fehler:               0
  Ziel:                 ...
  Report:               ...\UsedFaceplateVersions.csv
```

Die XML-Dateien sind dabei die **Definitionen der verwendeten WinCC-Unified-Faceplate-Typversionen**, keine PLC-Bausteine. Danach nehmen wir uns exemplarisch eine dieser XML-Dateien vor und prüfen, welche **Schnittstellen, Datentypen, internen Objekte und sonstigen Definitionen** tatsächlich enthalten sind. Daraus bauen wir dann die Verbindung **Faceplate-Definition ↔ Instanz ↔ konkrete Parameterbelegung**.

Schick mir einfach die Ausgabe von `dotnet run -- faceplate-library-used`.

---

# you asked

message time: 2026-10-27 13:35:07

Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\WINDOWS\system32> cd C:\Users\Administrator\sources\TiaOpennessTest
PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet build
  Wiederherzustellende Projekte werden ermittelt...
  Alle Projekte sind für die Wiederherstellung auf dem neuesten Stand.
  TiaOpennessTest -> C:\Users\Administrator\sources\TiaOpennessTest\bin\Debug\net48\TiaOpennessTest.exe

Der Buildvorgang wurde erfolgreich ausgeführt.
    0 Warnung(en)
    0 Fehler

Verstrichene Zeit 00:00:00.86
PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet run -- faceplate-library-used
FACEPLATE-LIBRARY-USED-EXPORT
  Exportiert nur die in einem vorhandenen vollständigen Archiv verwendeten Faceplate-Versionen.
  [USED] GetProcesses START
  [USED] GetProcesses OK (1)
  [USED] Attach START (TIA PID 11324)
  [USED] Attach OK
  Projekt: 2250264_V21
  Quellarchiv: C:\TiaProjectArchive\2250264_V21_20261027_113351
  FaceplateInstances.csv: 6
  Verwendete Typ/Version-Kombinationen: 40

  FP_2Pos_2Ini_Minimal V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\Cylinder\2Pos\2Pos_2Ini
    OK: 4827 Bytes

  FP_2Pos_4Ini_Minimal V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\Cylinder\2Pos\2Pos_4Ini
    OK: 4827 Bytes

  FP_ABB_Robot_System V8.3.0
    Pfad: 9999_Standard_Visu\Robots\ABB
    OK: 4821 Bytes

  FP_BoschRexrothScrewer V0.0.7
    Pfad: 9998_Machine_Visu
    OK: 3080 Bytes

  FP_Btn V8.3.0
    Pfad: 9999_Standard_Visu\SubItems
    OK: 3024 Bytes

  FP_CylinderPneu V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\Cylinder\2Pos
    OK: 4815 Bytes

  FP_EStop V8.3.0
    Pfad: 9999_Standard_Visu\Safety
    OK: 4816 Bytes

  FP_FeedingSystem V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\FeedingSystem
    OK: 4818 Bytes

  FP_Footer_OP_Mode V8.2.21
    Pfad: 9999_Standard_Visu\Operation Mode
    OK: 3050 Bytes

  FP_Footer_OP_Mode V8.3.0
    Pfad: 9999_Standard_Visu\Operation Mode
    OK: 4842 Bytes

  FP_Graph_Info V8.3.0
    Pfad: 9999_Standard_Visu\Graph
    OK: 4815 Bytes

  FP_HomeView_Global V8.1.50
    Pfad: 9998_Machine_Visu\HomeView
    OK: 3037 Bytes

  FP_HomeView_Light V0.0.11
    Pfad: 9998_Machine_Visu\HomeView
    OK: 3049 Bytes

  FP_Kistler_maXymosNC V8.3.0
    Pfad: 9999_Standard_Visu\Measurement\Kistler\maXXymosNC
    OK: 4828 Bytes

  FP_LineOverviewSelection V8.1.3
    Pfad: 9998_Machine_Visu\LineOverview
    OK: 3047 Bytes

  FP_MD_RotaryUnit V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\RotaryUnit\MultiDirection
    OK: 4824 Bytes

  FP_Messages_Archiv V8.3.0
    Pfad: 9999_Standard_Visu\Information\Message
    OK: 4820 Bytes

  FP_Messages_Archiv V8.3.2
    Pfad: 9999_Standard_Visu\Information\Message
    OK: 3271 Bytes

  FP_ModeSelector V8.3.0
    Pfad: 9999_Standard_Visu\Operation Mode
    OK: 4817 Bytes

  FP_Operating_Mode_Compact V8.3.0
    Pfad: 9999_Standard_Visu\Operation Mode
    OK: 4827 Bytes

  FP_OutputControl V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\OutputControl
    OK: 4824 Bytes

  FP_PartCounter_Ges_OK_NOK_V2 V8.3.0
    Pfad: 9999_Standard_Visu\CounterAndTimes\PartCounter
    OK: 4835 Bytes

  FP_PosAxis V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\Drive\TO_PosAxis
    OK: 4853 Bytes

  FP_SafetyDoor_Indication V8.1.2
    Pfad: 9998_Machine_Visu\Safety
    OK: 3278 Bytes

  FP_Safety_Light_Curtain V0.0.6
    Pfad: 9998_Machine_Visu\Safety
    OK: 3046 Bytes

  FP_Safety_Light_Curtain_Vertical V0.0.2
    Pfad: 9998_Machine_Visu\Safety
    OK: 3050 Bytes

  FP_Saxlift V0.0.6
    Pfad: 9998_Machine_Visu\Saxlift
    OK: 3040 Bytes

  FP_ScreenNavigator_Footer V8.3.0
    Pfad: 9999_Standard_Visu\ScreenNavigator
    OK: 4830 Bytes

  FP_ScreenNavigator_Footer V8.3.1
    Pfad: 9999_Standard_Visu\ScreenNavigator
    OK: 4831 Bytes

  FP_ScreenNavigator_Section V8.3.5
    Pfad: 9999_Standard_Visu\ScreenNavigator
    OK: 3279 Bytes

  FP_ScreenNavigator_Station V8.3.0
    Pfad: 9999_Standard_Visu\ScreenNavigator
    OK: 4834 Bytes

  FP_ScreenNavigator_Vertikal V8.3.1
    Pfad: 9999_Standard_Visu\ScreenNavigator
    OK: 4829 Bytes

  FP_ShiftCounter_V2 V8.3.0
    Pfad: 9999_Standard_Visu\CounterAndTimes\ShiftCounter
    OK: 4818 Bytes

  FP_Sinamics_Infeed_TLG370 V0.0.2
    Pfad: 9998_Machine_Visu\Siemens\Sinamics
    OK: 5274 Bytes

  FP_Sirius_Motorstarter V8.3.0
    Pfad: 9999_Standard_Visu\Actuator\Motorstarter
    OK: 4824 Bytes

  FP_Sirius_Motorstarter_LR V0.0.5
    Pfad: 9998_Machine_Visu\Motorstarter LR
    OK: 3274 Bytes

  FP_TabControl V8.3.0
    Pfad: 9999_Standard_Visu\Helper
    OK: 4812 Bytes

  FP_Typschild V8.3.0
    Pfad: 9999_Standard_Visu\Information\MachineTyp
    OK: 4814 Bytes

  FP_Typschild_ABB V0.0.3
    Pfad: 9998_Machine_Visu
    OK: 3039 Bytes

  FP_WPCStopper_1S1T_Minimal V8.3.1
    Pfad: 9999_Standard_Visu\Actuator\Stopper
    OK: 4834 Bytes

ERGEBNIS FACEPLATE-LIBRARY-USED-EXPORT
  Verwendete Versionen: 40
  Exportiert:           40
  Fehler:               0
  Ziel:                 C:\TiaProjectArchive\2250264_V21_20261027_113351\40_Library\Faceplates\UsedVersions
  Report:               C:\TiaProjectArchive\2250264_V21_20261027_113351\40_Library\Faceplates\UsedVersions\UsedFaceplateVersions.csv
  Laufzeit:             22,627 s
PS C:\Users\Administrator\sources\TiaOpennessTest>

---

# chatgpt response

Perfekt. Damit ist dieser Baustein vollständig bestätigt:

- **40 verwendete Faceplate-Typ/Version-Kombinationen**
- **40 erfolgreich exportiert**
- **0 Fehler**
- die Zuordnung über die Library-Pfade funktioniert sauber
- die XML-Dateien liegen jetzt vollständig unter  
  `40_Library\Faceplates\UsedVersions`

Besonders gut ist, dass auch mehrere Versionen desselben Typs korrekt getrennt archiviert wurden, z. B. `FP_Footer_OP_Mode` in `V8.2.21` und `V8.3.0` sowie `FP_Messages_Archiv` in `V8.3.0` und `V8.3.2`. Damit ist die spätere Dokumentation versionsgenau möglich.

Der nächste sinnvolle Schritt ist jetzt **nicht sofort ein Vollrun**, sondern zunächst eine dieser exportierten XML-Dateien strukturell zu analysieren. Ich würde dafür `FP_ModeSelector_V8.3.0.xml` nehmen, weil wir dazu bereits Instanzen und konkrete Bindings kennen.

Bitte führe als nächsten kleinen Schritt nur Folgendes aus:

```powershell
Get-Content "C:\TiaProjectArchive\2250264_V21_20261027_113351\40_Library\Faceplates\UsedVersions\9999_Standard_Visu\Operation Mode\FP_ModeSelector\V8.3.0\FP_ModeSelector_V8.3.0.xml" | Select-Object -First 160
```

Schick mir die Ausgabe. Dann bestimmen wir exakt, **was Siemens in dieser LibraryTypeVersion-XML tatsächlich liefert** – insbesondere Interface-Definitionen, Typinformationen und mögliche interne Struktur. Danach entscheiden wir, was wir daraus automatisiert extrahieren und mit `FaceplateBindings.csv` verknüpfen.

---

# you asked

message time: 2026-10-27 13:36:35

PS C:\Users\Administrator\sources\TiaOpennessTest> Get-Content "C:\TiaProjectArchive\2250264_V21_20261027_113351\40_Library\Faceplates\UsedVersions\9999_Standard_Visu\Operation Mode\FP_ModeSelector\V8.3.0\FP_ModeSelector_V8.3.0.xml" | Select-Object -First 160
<?xml version="1.0" encoding="utf-8"?>
<Document>
  <Engineering version="V21" />
  <DocumentInfo>
    <Created>2026-10-27T12:34:13.9510322Z</Created>
    <ExportSetting>WithReadOnly</ExportSetting>
    <InstalledProducts>
      <Product>
        <DisplayName>Totally Integrated Automation Portal</DisplayName>
        <DisplayVersion>V21</DisplayVersion>
      </Product>
      <Product>
        <DisplayName>SINAMICS Startdrive Advanced</DisplayName>
        <DisplayVersion>V21 HF1</DisplayVersion>
      </Product>
      <OptionPackage>
        <DisplayName>SINAMICS Startdrive G130, G150, S120, S150, G200, G220, S200, S210, S220, Innomotics MVD</DisplayName>
        <DisplayVersion>V21 HF1</DisplayVersion>
      </OptionPackage>
      <OptionPackage>
        <DisplayName>SINAMICS Startdrive G110M, G120, G120C, G120D, G120P, G115D</DisplayName>
        <DisplayVersion>V21 HF1</DisplayVersion>
      </OptionPackage>
      <Product>
        <DisplayName>STEP 7 Professional</DisplayName>
        <DisplayVersion>V21</DisplayVersion>
      </Product>
      <OptionPackage>
        <DisplayName>STEP 7 Safety</DisplayName>
        <DisplayVersion>V21</DisplayVersion>
      </OptionPackage>
      <OptionPackage>
        <DisplayName>Tech WebApplication</DisplayName>
        <DisplayVersion>V21</DisplayVersion>
      </OptionPackage>
      <Product>
        <DisplayName>WinCC Basic/Comfort/Advanced</DisplayName>
        <DisplayVersion>V21</DisplayVersion>
      </Product>
      <Product>
        <DisplayName>WinCC Unified</DisplayName>
        <DisplayVersion>V21</DisplayVersion>
      </Product>
    </InstalledProducts>
  </DocumentInfo>
  <Library.Types.LibraryTypeVersion ID="0">
    <AttributeList>
      <Author>wehrle</Author>
      <Guid ReadOnly="true">a6a50b79-8d99-4033-b52f-921777096c83</Guid>
      <IsDefault ReadOnly="true">true</IsDefault>
      <LibraryTypeGuid ReadOnly="true">7c0509b1-ecc1-4189-a11e-f29da6aa1861</LibraryTypeGuid>
      <LibraryTypeName ReadOnly="true">FP_ModeSelector</LibraryTypeName>
      <ModifiedDate ReadOnly="true">2026-01-22T09:23:56.2042167Z</ModifiedDate>
      <OriginalLibrary ReadOnly="true">LibAKE_Entwicklung_V20</OriginalLibrary>
      <State ReadOnly="true">Committed</State>
      <VersionNumber>8.3.0</VersionNumber>
    </AttributeList>
    <ObjectList>
      <MultilingualText ID="1" CompositionName="Comment">
        <ObjectList>
          <MultilingualTextItem ID="2" CompositionName="Items">
            <AttributeList>
              <Culture>de-DE</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="3" CompositionName="Items">
            <AttributeList>
              <Culture>en-GB</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="4" CompositionName="Items">
            <AttributeList>
              <Culture>zh-CN</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="5" CompositionName="Items">
            <AttributeList>
              <Culture>pl-PL</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="6" CompositionName="Items">
            <AttributeList>
              <Culture>ro-RO</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="7" CompositionName="Items">
            <AttributeList>
              <Culture>es-ES</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="8" CompositionName="Items">
            <AttributeList>
              <Culture>fr-FR</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="9" CompositionName="Items">
            <AttributeList>
              <Culture>it-IT</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="A" CompositionName="Items">
            <AttributeList>
              <Culture>ja-JP</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="B" CompositionName="Items">
            <AttributeList>
              <Culture>en-US</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
        </ObjectList>
      </MultilingualText>
    </ObjectList>
  </Library.Types.LibraryTypeVersion>
</Document>
PS C:\Users\Administrator\sources\TiaOpennessTest>

---

# chatgpt response

Die XML ist aufschlussreich: **Sie enthält nur Metadaten der Library-Version**, nicht die eigentliche Faceplate-Definition. Ich prüfe kurz, welcher V21-Zugriff für den Inhalt selbst vorgesehen ist, damit wir nicht am falschen Exportweg weiterbauen.

Das Ergebnis ist eindeutig: **Der XML-Export von `LibraryTypeVersion` liefert nicht den eigentlichen Faceplate-Inhalt.** Er exportiert nur den Versionsdatensatz der Bibliothek: Autor, GUIDs, Typname, Version, Status, Ursprungsbibliothek, Änderungsdatum und Kommentare. Genau dieses Verhalten beschreibt Siemens für `LibraryTypeVersion.Export()`. ([Totally Integrated Automation](https://docs.tia.siemens.cloud/r/de-de/v21/tia-portal-openness-api-fur-die-automatisierung-von-engineering-workflows/tia-portal-openness-api/funktionen-fur-bibliotheken/zugriff-auf-bausteine-in-bibliotheken?utm_source=chatgpt.com))

Das erklärt auch die geringe Dateigröße von rund 3–5 KB. In deiner `FP_ModeSelector_V8.3.0.xml` fehlen komplett:

```text
Faceplate-Schnittstellen
ScreenItems
interne Tags
Dynamisierungen
Events
Skripte
interne Visualisierung
```

Wir sollten die 40 XML-Dateien trotzdem behalten. Sie sind als **versionsgenaue Library-Metadaten** wertvoll und enthalten unter anderem `LibraryTypeGuid`, `Guid`, `OriginalLibrary`, `VersionNumber` und `ModifiedDate`.

Der entscheidende Hinweis in der Siemens-V21-Dokumentation ist aber ein anderer: Eine `LibraryTypeVersion` besitzt zusätzlich einen Navigator **`ContentObject`**, über den zum tatsächlichen Versionsinhalt navigiert werden kann. Außerdem gibt es seit V20 spezialisierte Typen wie `FaceplateLibraryTypeVersion`. ([Totally Integrated Automation](https://docs.tia.siemens.cloud/r/en-us/v21/tia-portal-openness-api-for-automation-of-engineering-workflows/tia-portal-openness-api/functions-on-libraries/accessing-type-versions?utm_source=chatgpt.com))

Damit ändert sich unser nächster Schritt etwas:

```text
LibraryTypeVersion
│
├─ Metadaten                 ← haben wir jetzt als XML
│
└─ ContentObject             ← DAS müssen wir untersuchen
      │
      └─ eigentlicher Faceplate-Inhalt
```

Das passt auch zu unserem bisherigen Befund: Die **Schnittstelle einer Faceplate-Instanz konnten wir bereits direkt lesen**. Und Siemens beschreibt die Unified-Faceplate-Typen selbst als Objekte mit Tag-, Property- und Event-Schnittstellen sowie einer internen Visualisierung. ([Totally Integrated Automation](https://docs.tia.siemens.cloud/r/en-us/v21/configuring-screens-rt-unified/configuring-faceplates-rt-unified/editing-faceplates-rt-unified/interface-properties-in-faceplates-rt-unified/configure-interface-property-rt-unified?contentId=elXfxT2rLt5~RVF8cNQBEg&utm_source=chatgpt.com))

### Nächster Schritt

Ich würde jetzt **noch keinen weiteren großen Export einbauen**. Wir testen nur an:

```text
FP_ModeSelector V8.3.0
```

welchen konkreten .NET-Typ und welche Objekte `ContentObject` liefert.

Die gewünschte Diagnose sollte ungefähr Folgendes ausgeben:

```text
Library-Typ: FP_ModeSelector
Version: 8.3.0
Runtime-Typ:
  Siemens.Engineering....

ContentObject:
  ...
```

und anschließend die verfügbaren Properties/Compositions dieses Objekts.

Wenn dort der eigentliche Unified-Faceplate-Inhalt erreichbar ist, haben wir den richtigen Weg gefunden. Dann können wir anschließend gezielt **Definition + Interface + interne Elemente** archivieren, statt weiter Metadaten-XMLs zu analysieren.

**Stand damit:**

```text
520 Faceplate-Instanzen                 ✓
40 verwendete Typ/Versionen             ✓
40 Library-Pfade                        ✓
Instanz-Bindings                        ✓
40 Versions-Metadaten als XML           ✓
eigentlichen Faceplate-Inhalt           ← jetzt
```

Ich würde dafür als Nächstes wieder eine **kleine `faceplate-content-smoke`-Diagnose** bauen, nur für `FP_ModeSelector V8.3.0`.

---

# you asked

message time: 2026-10-27 13:38:27

wenn uns das unbedingt weiter bringt und dann echt mal an das finale Ende führt?

---

# chatgpt response

Ja — **aber nur noch als gezielter Abschluss-Schritt, nicht als neue Baustelle**.

Der Grund ist einfach: Für die Faceplates haben wir bereits fast alles, was für die technische Dokumentation wichtig ist:

- 520 Instanzen
- 40 tatsächlich verwendete Typ/Versionen
- eindeutige Library-Pfade
- Instanz-Bindings
- versionsgenaue Library-Metadaten als XML

Was noch fehlt, ist nur die Frage: **Kommen wir an die eigentliche Faceplate-Definition selbst heran?** Wenn `ContentObject` uns diese liefert, gewinnen wir noch die Definitionsebene dazu. Wenn nicht, markieren wir diesen Punkt sauber als API-Grenze und gehen weiter zum Abschluss. Genau deshalb lohnt sich dieser eine Smoke-Test noch.

Ich würde danach **keine weiteren Faceplate-Experimente** mehr machen. Das Ziel ist jetzt klar:

```text
1. ContentObject einmal testen
2. Ergebnis bewerten
3. Faceplate-Thema abschließen
4. restliche Archivbereiche bündeln
5. V21 finalisieren
6. anschließend Versionsadapter für V20/V19/...
```

Wir sind also nicht mehr in einer offenen Forschungsphase. Der nächste Test ist eine **Go/No-Go-Entscheidung** für den letzten fehlenden Faceplate-Inhalt.

Wenn du möchtest, gebe ich dir jetzt direkt die komplette kleine `Program.cs` für `faceplate-content-smoke`, damit wir das einmal sauber entscheiden und danach wirklich weiter Richtung finales Ende gehen.

---

# you asked

message time: 2026-10-27 13:39:16

Ja bitte mach das

---

# chatgpt response

Ja. Wir machen daraus jetzt **einen einzigen klaren Abschluss-Test für Faceplates**: `FP_ModeSelector V8.3.0` öffnen, `ContentObject` auflösen und nur die tatsächlich erreichbaren Eigenschaften/Compositions ausgeben. Wenn dort kein verwertbarer Inhalt steckt, schließen wir Faceplates an dieser Stelle ab.

Ich habe die Siemens-V21-Doku gegengeprüft: `LibraryTypeVersion` besitzt tatsächlich den Navigator **`ContentObject`**, aber Siemens dokumentiert dafür keinen einfachen C#-Beispielzugriff. Deshalb machen wir den Test bewusst per Reflection: Er zeigt uns exakt, was deine installierte V21-API an diesem Faceplate wirklich veröffentlicht, ohne etwas am Projekt zu verändern.

Genau. Wir machen jetzt **nur diesen Smoke-Test**. Er verändert nichts am TIA-Projekt und entscheidet danach endgültig, ob wir aus `ContentObject` noch echten Faceplate-Inhalt bekommen oder das Thema abschließen.

Siemens bestätigt für V21 sowohl den `ContentObject`-Navigator einer `LibraryTypeVersion` als auch die speziellen `FaceplateLibraryTypeVersion`-Klassen. ([Totally Integrated Automation](https://docs.tia.siemens.cloud/r/de-de/v21/tia-portal-openness-api-fur-die-automatisierung-von-engineering-workflows/tia-portal-openness-api/funktionen-fur-bibliotheken/zugriff-auf-bausteine-in-bibliotheken?utm_source=chatgpt.com))

Da deine aktuelle `Program.cs` wertvoll ist, sichere sie zuerst:

```powershell
Copy-Item .\Program.cs .\Program_before_faceplate_content_smoke.bak -Force
```

Dann **die komplette `Program.cs`** durch diese Diagnoseversion ersetzen:

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Reflection;

using Siemens.Engineering;

namespace TiaOpennessTest
{
    internal class Program
    {
        private const string TargetTypeName =
            "FP_ModeSelector";

        private const string TargetVersion =
            "8.3.0";

        private static readonly string[] TargetFolderPath =
        {
            "9999_Standard_Visu",
            "Operation Mode"
        };

        static void Main(string[] args)
        {
            try
            {
                Run();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("SCHWERER FEHLER:");
                Console.WriteLine(ex.GetType().FullName);
                Console.WriteLine(ex.Message);
                Console.WriteLine();
                Console.WriteLine(ex.StackTrace);
            }
        }

        private static void Run()
        {
            Console.WriteLine(
                "FACEPLATE-CONTENT-SMOKE");

            Console.WriteLine(
                "==================================================");

            Console.WriteLine(
                $"Typ:     {TargetTypeName}");

            Console.WriteLine(
                $"Version: {TargetVersion}");

            Console.WriteLine(
                "Pfad:    " +
                string.Join(
                    "\\",
                    TargetFolderPath));

            Console.WriteLine();

            var processes =
                TiaPortal.GetProcesses();

            Console.WriteLine(
                $"Gefundene TIA-Instanzen: {processes.Count}");

            if (processes.Count == 0)
            {
                Console.WriteLine(
                    "Keine laufende TIA-V21-Instanz gefunden.");

                return;
            }

            Console.WriteLine(
                $"Attach an PID {processes[0].Id} ...");

            using (
                TiaPortal tiaPortal =
                    processes[0].Attach())
            {
                Console.WriteLine(
                    "Attach OK.");

                if (tiaPortal.Projects.Count == 0)
                {
                    Console.WriteLine(
                        "Kein geöffnetes Projekt gefunden.");

                    return;
                }

                var project =
                    tiaPortal.Projects[0];

                Console.WriteLine(
                    $"Projekt: {project.Name}");

                Console.WriteLine();

                object projectLibrary =
                    GetPropertyValue(
                        project,
                        "ProjectLibrary");

                if (projectLibrary == null)
                {
                    Console.WriteLine(
                        "ProjectLibrary nicht erreichbar.");

                    return;
                }

                object typeFolder =
                    GetPropertyValue(
                        projectLibrary,
                        "TypeFolder");

                if (typeFolder == null)
                {
                    Console.WriteLine(
                        "ProjectLibrary.TypeFolder nicht erreichbar.");

                    return;
                }

                object currentFolder =
                    typeFolder;

                foreach (
                    string folderName
                    in TargetFolderPath)
                {
                    Console.WriteLine(
                        $"Suche Ordner: {folderName}");

                    object folders =
                        GetPropertyValue(
                            currentFolder,
                            "Folders");

                    object nextFolder =
                        FindByName(
                            folders,
                            folderName);

                    if (nextFolder == null)
                    {
                        Console.WriteLine(
                            $"FEHLER: Ordner nicht gefunden: {folderName}");

                        return;
                    }

                    currentFolder =
                        nextFolder;
                }

                Console.WriteLine(
                    $"Suche Library-Typ: {TargetTypeName}");

                object types =
                    GetPropertyValue(
                        currentFolder,
                        "Types");

                object libraryType =
                    FindByName(
                        types,
                        TargetTypeName);

                if (libraryType == null)
                {
                    Console.WriteLine(
                        "FEHLER: Library-Typ wurde nicht gefunden.");

                    return;
                }

                Console.WriteLine(
                    "Library-Typ gefunden.");

                DumpObjectIdentity(
                    "LIBRARY TYPE",
                    libraryType);

                object versions =
                    GetPropertyValue(
                        libraryType,
                        "Versions");

                object version =
                    FindVersion(
                        versions,
                        TargetVersion);

                if (version == null)
                {
                    Console.WriteLine();
                    Console.WriteLine(
                        $"FEHLER: Version {TargetVersion} wurde nicht gefunden.");

                    Console.WriteLine(
                        "Vorhandene Versionen:");

                    foreach (
                        object v
                        in EnumerateObjects(versions))
                    {
                        Console.WriteLine(
                            "  " +
                            GetSimplePropertyText(
                                v,
                                "VersionNumber"));
                    }

                    return;
                }

                Console.WriteLine();
                Console.WriteLine(
                    "Library-Version gefunden.");

                DumpObjectIdentity(
                    "LIBRARY TYPE VERSION",
                    version);

                Console.WriteLine();
                Console.WriteLine(
                    "Versionsattribute:");

                DumpSelectedProperty(
                    version,
                    "LibraryTypeName");

                DumpSelectedProperty(
                    version,
                    "VersionNumber");

                DumpSelectedProperty(
                    version,
                    "Guid");

                DumpSelectedProperty(
                    version,
                    "LibraryTypeGuid");

                DumpSelectedProperty(
                    version,
                    "State");

                DumpSelectedProperty(
                    version,
                    "IsDefault");

                DumpSelectedProperty(
                    version,
                    "Author");

                DumpSelectedProperty(
                    version,
                    "OriginalLibrary");

                DumpSelectedProperty(
                    version,
                    "ModifiedDate");

                Console.WriteLine();
                Console.WriteLine(
                    "==================================================");

                Console.WriteLine(
                    "SUCHE NACH CONTENTOBJECT");

                Console.WriteLine(
                    "==================================================");

                object contentObject =
                    TryGetContentObject(
                        version);

                Console.WriteLine();

                if (contentObject == null)
                {
                    Console.WriteLine(
                        "ERGEBNIS:");

                    Console.WriteLine(
                        "  ContentObject konnte nicht direkt aufgelöst werden.");

                    Console.WriteLine();
                    Console.WriteLine(
                        "Wir geben deshalb die relevanten CLR-Member der");

                    Console.WriteLine(
                        "LibraryTypeVersion aus.");

                    DumpRelevantMembers(
                        version);

                    Console.WriteLine();
                    Console.WriteLine(
                        "FACEPLATE-CONTENT-SMOKE ABGESCHLOSSEN.");

                    return;
                }

                Console.WriteLine(
                    "ContentObject wurde gefunden.");

                DumpObjectIdentity(
                    "CONTENT OBJECT",
                    contentObject);

                Console.WriteLine();
                Console.WriteLine(
                    "ContentObject-Inhalt:");

                int contentCount =
                    DumpContent(
                        contentObject);

                Console.WriteLine();
                Console.WriteLine(
                    "==================================================");

                Console.WriteLine(
                    "ERGEBNIS FACEPLATE-CONTENT-SMOKE");

                Console.WriteLine(
                    $"  ContentObject vorhanden: True");

                Console.WriteLine(
                    $"  Gefundene Content-Elemente: {contentCount}");

                Console.WriteLine(
                    "==================================================");
            }
        }

        private static object FindByName(
            object collection,
            string wantedName)
        {
            if (collection == null)
                return null;

            foreach (
                object item
                in EnumerateObjects(collection))
            {
                string name =
                    GetSimplePropertyText(
                        item,
                        "Name");

                if (string.Equals(
                    name,
                    wantedName,
                    StringComparison.OrdinalIgnoreCase))
                {
                    return item;
                }
            }

            return null;
        }

        private static object FindVersion(
            object versions,
            string wantedVersion)
        {
            if (versions == null)
                return null;

            foreach (
                object version
                in EnumerateObjects(versions))
            {
                string versionText =
                    GetSimplePropertyText(
                        version,
                        "VersionNumber");

                if (string.Equals(
                    versionText,
                    wantedVersion,
                    StringComparison.OrdinalIgnoreCase))
                {
                    return version;
                }
            }

            return null;
        }

        private static object TryGetContentObject(
            object version)
        {
            Type runtimeType =
                version.GetType();

            Console.WriteLine(
                $"Runtime-Typ: {runtimeType.FullName}");

            Console.WriteLine();

            //
            // 1. Exakte Property ContentObject
            //
            PropertyInfo property =
                FindPropertyRecursive(
                    runtimeType,
                    "ContentObject");

            if (property != null)
            {
                Console.WriteLine(
                    "Property 'ContentObject' gefunden:");

                Console.WriteLine(
                    $"  DeclaringType: {property.DeclaringType.FullName}");

                Console.WriteLine(
                    $"  PropertyType:  {property.PropertyType.FullName}");

                try
                {
                    object result =
                        property.GetValue(
                            version,
                            null);

                    Console.WriteLine(
                        $"  Wert: {(result == null ? "<null>" : "vorhanden")}");

                    if (result != null)
                        return result;
                }
                catch (Exception ex)
                {
                    Console.WriteLine(
                        "  Zugriff fehlgeschlagen:");

                    PrintException(
                        ex,
                        "    ");
                }
            }
            else
            {
                Console.WriteLine(
                    "Keine CLR-Property mit dem Namen ContentObject gefunden.");
            }

            Console.WriteLine();

            //
            // 2. Interfaces prüfen
            //
            foreach (
                Type interfaceType
                in runtimeType.GetInterfaces())
            {
                PropertyInfo interfaceProperty =
                    interfaceType.GetProperty(
                        "ContentObject",
                        BindingFlags.Instance |
                        BindingFlags.Public |
                        BindingFlags.NonPublic);

                if (interfaceProperty == null)
                    continue;

                Console.WriteLine(
                    "ContentObject über Interface gefunden:");

                Console.WriteLine(
                    $"  Interface: {interfaceType.FullName}");

                Console.WriteLine(
                    $"  Typ:       {interfaceProperty.PropertyType.FullName}");

                try
                {
                    object result =
                        interfaceProperty.GetValue(
                            version,
                            null);

                    if (result != null)
                        return result;
                }
                catch (Exception ex)
                {
                    PrintException(
                        ex,
                        "    ");
                }
            }

            //
            // 3. Methoden suchen, die ContentObject heißen
            //    oder enthalten.
            //
            MethodInfo[] methods =
                runtimeType.GetMethods(
                    BindingFlags.Instance |
                    BindingFlags.Public |
                    BindingFlags.NonPublic);

            foreach (
                MethodInfo method
                in methods)
            {
                if (method.Name.IndexOf(
                    "ContentObject",
                    StringComparison.OrdinalIgnoreCase) < 0)
                {
                    continue;
                }

                Console.WriteLine();
                Console.WriteLine(
                    "Methode mit ContentObject gefunden:");

                Console.WriteLine(
                    $"  {FormatMethod(method)}");

                if (method.GetParameters().Length != 0)
                    continue;

                if (method.ReturnType == typeof(void))
                    continue;

                try
                {
                    object result =
                        method.Invoke(
                            version,
                            null);

                    if (result != null)
                    {
                        Console.WriteLine(
                            "  Aufruf erfolgreich.");

                        return result;
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine(
                        "  Aufruf fehlgeschlagen:");

                    PrintException(
                        ex,
                        "    ");
                }
            }

            return null;
        }

        private static PropertyInfo FindPropertyRecursive(
            Type type,
            string propertyName)
        {
            Type current =
                type;

            while (current != null)
            {
                PropertyInfo property =
                    current.GetProperty(
                        propertyName,
                        BindingFlags.Instance |
                        BindingFlags.Public |
                        BindingFlags.NonPublic |
                        BindingFlags.DeclaredOnly);

                if (property != null)
                    return property;

                current =
                    current.BaseType;
            }

            return null;
        }

        private static int DumpContent(
            object contentObject)
        {
            IEnumerable enumerable =
                contentObject as IEnumerable;

            if (enumerable == null)
            {
                Console.WriteLine(
                    "  ContentObject ist keine IEnumerable-Collection.");

                Console.WriteLine();
                Console.WriteLine(
                    "  Öffentliche Eigenschaften:");

                DumpPublicProperties(
                    contentObject,
                    "    ");

                return 1;
            }

            int count =
                0;

            foreach (
                object item
                in enumerable)
            {
                count++;

                Console.WriteLine();
                Console.WriteLine(
                    $"  Content #{count}");

                if (item == null)
                {
                    Console.WriteLine(
                        "    <null>");

                    continue;
                }

                Console.WriteLine(
                    $"    Runtime-Typ: {item.GetType().FullName}");

                Console.WriteLine(
                    $"    Assembly:    {item.GetType().Assembly.GetName().Name}");

                DumpLikelyUsefulProperties(
                    item,
                    "    ");

                if (count >= 50)
                {
                    Console.WriteLine();
                    Console.WriteLine(
                        "  Ausgabe bei 50 Elementen begrenzt.");

                    break;
                }
            }

            if (count == 0)
            {
                Console.WriteLine(
                    "  Collection ist leer.");
            }

            return count;
        }

        private static void DumpLikelyUsefulProperties(
            object obj,
            string indent)
        {
            string[] preferredNames =
            {
                "Name",
                "Type",
                "ObjectType",
                "ScreenItems",
                "Items",
                "Interface",
                "Tags",
                "Properties",
                "Events",
                "Dynamizations",
                "Dynamizations",
                "Scripts",
                "ContainedType"
            };

            HashSet<string> written =
                new HashSet<string>(
                    StringComparer.OrdinalIgnoreCase);

            foreach (
                string name
                in preferredNames)
            {
                PropertyInfo property =
                    FindPropertyRecursive(
                        obj.GetType(),
                        name);

                if (property == null)
                    continue;

                written.Add(
                    property.Name);

                PrintProperty(
                    obj,
                    property,
                    indent);
            }

            PropertyInfo[] properties =
                obj.GetType().GetProperties(
                    BindingFlags.Instance |
                    BindingFlags.Public);

            foreach (
                PropertyInfo property
                in properties.OrderBy(
                    p => p.Name))
            {
                if (written.Contains(
                    property.Name))
                {
                    continue;
                }

                if (!IsInterestingPropertyName(
                    property.Name))
                {
                    continue;
                }

                PrintProperty(
                    obj,
                    property,
                    indent);
            }
        }

        private static bool IsInterestingPropertyName(
            string name)
        {
            string[] terms =
            {
                "Name",
                "Type",
                "Interface",
                "Item",
                "Tag",
                "Property",
                "Event",
                "Dynamic",
                "Script",
                "Screen",
                "Content"
            };

            foreach (
                string term
                in terms)
            {
                if (name.IndexOf(
                    term,
                    StringComparison.OrdinalIgnoreCase) >= 0)
                {
                    return true;
                }
            }

            return false;
        }

        private static void DumpPublicProperties(
            object obj,
            string indent)
        {
            PropertyInfo[] properties =
                obj.GetType().GetProperties(
                    BindingFlags.Instance |
                    BindingFlags.Public);

            foreach (
                PropertyInfo property
                in properties.OrderBy(
                    p => p.Name))
            {
                PrintProperty(
                    obj,
                    property,
                    indent);
            }
        }

        private static void PrintProperty(
            object obj,
            PropertyInfo property,
            string indent)
        {
            try
            {
                if (property.GetIndexParameters().Length != 0)
                    return;

                object value =
                    property.GetValue(
                        obj,
                        null);

                if (value == null)
                {
                    Console.WriteLine(
                        $"{indent}{property.Name}: <null>");

                    return;
                }

                if (IsSimpleValue(
                    value.GetType()))
                {
                    Console.WriteLine(
                        $"{indent}{property.Name}: {value}");

                    return;
                }

                int? count =
                    TryGetCount(
                        value);

                if (count.HasValue)
                {
                    Console.WriteLine(
                        $"{indent}{property.Name}: " +
                        $"{value.GetType().FullName} " +
                        $"(Count={count.Value})");
                }
                else
                {
                    Console.WriteLine(
                        $"{indent}{property.Name}: " +
                        value.GetType().FullName);
                }
            }
            catch (Exception ex)
            {
                Exception real =
                    UnwrapException(
                        ex);

                Console.WriteLine(
                    $"{indent}{property.Name}: " +
                    $"<Zugriff fehlgeschlagen: " +
                    $"{real.GetType().Name}: {real.Message}>");
            }
        }

        private static int? TryGetCount(
            object value)
        {
            if (value == null)
                return null;

            ICollection collection =
                value as ICollection;

            if (collection != null)
                return collection.Count;

            try
            {
                PropertyInfo countProperty =
                    value.GetType().GetProperty(
                        "Count",
                        BindingFlags.Instance |
                        BindingFlags.Public);

                if (countProperty == null)
                    return null;

                object countValue =
                    countProperty.GetValue(
                        value,
                        null);

                if (countValue == null)
                    return null;

                return Convert.ToInt32(
                    countValue);
            }
            catch
            {
                return null;
            }
        }

        private static bool IsSimpleValue(
            Type type)
        {
            if (type.IsPrimitive)
                return true;

            if (type.IsEnum)
                return true;

            return
                type == typeof(string) ||
                type == typeof(decimal) ||
                type == typeof(DateTime) ||
                type == typeof(TimeSpan) ||
                type == typeof(Guid) ||
                type == typeof(Version);
        }

        private static void DumpRelevantMembers(
            object obj)
        {
            Type type =
                obj.GetType();

            Console.WriteLine();
            Console.WriteLine(
                "Relevante Properties:");

            PropertyInfo[] properties =
                type.GetProperties(
                    BindingFlags.Instance |
                    BindingFlags.Public |
                    BindingFlags.NonPublic);

            foreach (
                PropertyInfo property
                in properties
                    .Where(
                        p =>
                            ContainsRelevantTerm(
                                p.Name))
                    .OrderBy(
                        p => p.Name))
            {
                Console.WriteLine(
                    $"  {property.PropertyType.FullName} " +
                    $"{property.Name}");
            }

            Console.WriteLine();
            Console.WriteLine(
                "Relevante Methoden:");

            MethodInfo[] methods =
                type.GetMethods(
                    BindingFlags.Instance |
                    BindingFlags.Public |
                    BindingFlags.NonPublic);

            foreach (
                MethodInfo method
                in methods
                    .Where(
                        m =>
                            ContainsRelevantTerm(
                                m.Name))
                    .OrderBy(
                        m => m.Name))
            {
                Console.WriteLine(
                    "  " +
                    FormatMethod(
                        method));
            }

            Console.WriteLine();
            Console.WriteLine(
                "Basisklassen:");

            Type current =
                type;

            while (current != null)
            {
                Console.WriteLine(
                    $"  {current.FullName}");

                current =
                    current.BaseType;
            }

            Console.WriteLine();
            Console.WriteLine(
                "Interfaces:");

            foreach (
                Type interfaceType
                in type.GetInterfaces()
                    .OrderBy(
                        i => i.FullName))
            {
                Console.WriteLine(
                    $"  {interfaceType.FullName}");
            }
        }

        private static bool ContainsRelevantTerm(
            string name)
        {
            string[] terms =
            {
                "Content",
                "Navigator",
                "Composition",
                "Object",
                "Version",
                "Faceplate"
            };

            foreach (
                string term
                in terms)
            {
                if (name.IndexOf(
                    term,
                    StringComparison.OrdinalIgnoreCase) >= 0)
                {
                    return true;
                }
            }

            return false;
        }

        private static string FormatMethod(
            MethodInfo method)
        {
            string parameters =
                string.Join(
                    ", ",
                    method.GetParameters()
                        .Select(
                            p =>
                                p.ParameterType.Name +
                                " " +
                                p.Name));

            return
                method.ReturnType.Name +
                " " +
                method.Name +
                "(" +
                parameters +
                ")";
        }

        private static void DumpObjectIdentity(
            string heading,
            object obj)
        {
            Console.WriteLine();
            Console.WriteLine(
                heading);

            Console.WriteLine(
                "--------------------------------------------------");

            if (obj == null)
            {
                Console.WriteLine(
                    "<null>");

                return;
            }

            Type type =
                obj.GetType();

            Console.WriteLine(
                $"Runtime-Typ: {type.FullName}");

            Console.WriteLine(
                $"Assembly:    {type.Assembly.GetName().Name}");

            Console.WriteLine(
                $"Basistyp:    " +
                $"{(type.BaseType == null ? "<none>" : type.BaseType.FullName)}");
        }

        private static void DumpSelectedProperty(
            object obj,
            string propertyName)
        {
            string value =
                GetSimplePropertyText(
                    obj,
                    propertyName);

            Console.WriteLine(
                $"  {propertyName}: " +
                $"{(value ?? "<nicht verfügbar>")}");
        }

        private static string GetSimplePropertyText(
            object obj,
            string propertyName)
        {
            object value =
                GetPropertyValue(
                    obj,
                    propertyName);

            if (value == null)
                return null;

            return value.ToString();
        }

        private static object GetPropertyValue(
            object obj,
            string propertyName)
        {
            if (obj == null)
                return null;

            try
            {
                PropertyInfo property =
                    FindPropertyRecursive(
                        obj.GetType(),
                        propertyName);

                if (property == null)
                    return null;

                if (property.GetIndexParameters().Length != 0)
                    return null;

                return property.GetValue(
                    obj,
                    null);
            }
            catch
            {
                return null;
            }
        }

        private static IEnumerable<object> EnumerateObjects(
            object collection)
        {
            if (collection == null)
                yield break;

            IEnumerable enumerable =
                collection as IEnumerable;

            if (enumerable == null)
                yield break;

            foreach (
                object item
                in enumerable)
            {
                yield return item;
            }
        }

        private static void PrintException(
            Exception ex,
            string indent)
        {
            Exception real =
                UnwrapException(
                    ex);

            Console.WriteLine(
                $"{indent}{real.GetType().FullName}");

            Console.WriteLine(
                $"{indent}{real.Message}");
        }

        private static Exception UnwrapException(
            Exception ex)
        {
            TargetInvocationException tie =
                ex as TargetInvocationException;

            if (tie != null &&
                tie.InnerException != null)
            {
                return tie.InnerException;
            }

            return ex;
        }
    }
}
```

Dann:

```powershell
dotnet build
```

Wenn wieder

```text
0 Warnung(en)
0 Fehler
```

kommt, ausschließlich:

```powershell
dotnet run
```

Dieser Test sucht nur:

```text
ProjectLibrary
→ 9999_Standard_Visu
→ Operation Mode
→ FP_ModeSelector
→ V8.3.0
→ ContentObject
```

Er exportiert nichts und verändert nichts.

**Danach brauche ich die komplette Konsolenausgabe.** Besonders entscheidend sind nur drei mögliche Ergebnisse:

```text
ContentObject vorhanden: True
Gefundene Content-Elemente: > 0
```

→ sehr gut, dann nehmen wir die Definition noch mit.

```text
ContentObject vorhanden: True
Gefundene Content-Elemente: 0
```

→ Siemens liefert für diesen Faceplate-Typ über den Navigator keinen Inhalt; Faceplates werden damit abgeschlossen.

Oder:

```text
ContentObject konnte nicht direkt aufgelöst werden
```

→ dann verrät uns die anschließende Member-Diagnose, ob der Navigator unter einem anderen CLR-Zugriff verborgen ist. **Danach gibt es höchstens noch eine gezielte Korrektur – keine weitere Faceplate-Testserie.**

Die 40 bereits exportierten Dateien bleiben in jedem Fall als versionsgenaue Library-Metadaten erhalten; der bisherige Stand mit 40/40 erfolgreichen Exporten wird dadurch nicht angetastet.

---

# you asked

message time: 2026-10-27 13:52:20

PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet build
  Wiederherzustellende Projekte werden ermittelt...
  Alle Projekte sind für die Wiederherstellung auf dem neuesten Stand.
  TiaOpennessTest -> C:\Users\Administrator\sources\TiaOpennessTest\bin\Debug\net48\TiaOpennessTest.exe

Der Buildvorgang wurde erfolgreich ausgeführt.
    0 Warnung(en)
    0 Fehler

Verstrichene Zeit 00:00:01.77
PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet run
FACEPLATE-CONTENT-SMOKE
==================================================
Typ:     FP_ModeSelector
Version: 8.3.0
Pfad:    9999_Standard_Visu\Operation Mode

Gefundene TIA-Instanzen: 1
Attach an PID 11324 ...
Attach OK.
Projekt: 2250264_V21

Suche Ordner: 9999_Standard_Visu
Suche Ordner: Operation Mode
Suche Library-Typ: FP_ModeSelector
Library-Typ gefunden.

LIBRARY TYPE
--------------------------------------------------
Runtime-Typ: Siemens.Engineering.Library.Types.LibraryType
Assembly:    Siemens.Engineering.Base
Basistyp:    System.Object

Library-Version gefunden.

LIBRARY TYPE VERSION
--------------------------------------------------
Runtime-Typ: Siemens.Engineering.Library.Types.LibraryTypeVersion
Assembly:    Siemens.Engineering.Base
Basistyp:    System.Object

Versionsattribute:
  LibraryTypeName: <nicht verfügbar>
  VersionNumber: 8.3.0
  Guid: a6a50b79-8d99-4033-b52f-921777096c83
  LibraryTypeGuid: <nicht verfügbar>
  State: Committed
  IsDefault: True
  Author: wehrle
  OriginalLibrary: LibAKE_Entwicklung_V20
  ModifiedDate: 22.01.2026 09:23:56

==================================================
SUCHE NACH CONTENTOBJECT
==================================================
Runtime-Typ: Siemens.Engineering.Library.Types.LibraryTypeVersion

Keine CLR-Property mit dem Namen ContentObject gefunden.


ERGEBNIS:
  ContentObject konnte nicht direkt aufgelöst werden.

Wir geben deshalb die relevanten CLR-Member der
LibraryTypeVersion aus.

Relevante Properties:
  Siemens.Engineering.Library.Types.LibraryType TypeObject
  System.Version VersionNumber

Relevante Methoden:
  LibraryType get_TypeObject()
  Version get_VersionNumber()
  IEngineeringObject global::Siemens.Engineering.IEngineeringObject.Create(String compositionName, Type type, IEnumerable`1 parameters)
  IEngineeringCompositionOrObject global::Siemens.Engineering.IEngineeringObject.GetComposition(String name)
  IList`1 global::Siemens.Engineering.IEngineeringObject.GetCompositionInfos()
  IList`1 global::Siemens.Engineering.IEngineeringObject.GetCreationInfos(String compositionName)
  IList`1 global::Siemens.Engineering.IEngineeringObject.GetInvocationInfos()
  Object global::Siemens.Engineering.IEngineeringObject.Invoke(String name, IEnumerable`1 parameters)

Basisklassen:
  Siemens.Engineering.Library.Types.LibraryTypeVersion
  System.Object

Interfaces:
  Siemens.Engineering.IEngineeringCompositionOrObject
  Siemens.Engineering.IEngineeringInstance
  Siemens.Engineering.IEngineeringObject
  Siemens.Engineering.IEngineeringServiceProvider
  Siemens.Engineering.Private.IInternalBaseAccess
  Siemens.Engineering.Private.IInternalInstanceAccess
  Siemens.Engineering.Private.IInternalObjectAccess
  System.IEquatable`1[[System.Object, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089]]
  System.IServiceProvider

FACEPLATE-CONTENT-SMOKE ABGESCHLOSSEN.
PS C:\Users\Administrator\sources\TiaOpennessTest>

---
Powered by [AI Exporter](https://saveai.net)