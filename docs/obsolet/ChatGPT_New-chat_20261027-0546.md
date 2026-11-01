> From: https://chatgpt.com/c/6ae027e0-341c-83ed-81a1-837e3d309ac6?temporary-chat=true

# you asked

message time: 2026-10-27 05:26:07

So, machen wir weiter

---

# chatgpt response

Ja. Wir machen genau an der Stelle weiter, an der wir aufgehört haben: Der rekursive Export ungeschützter Bausteine der ersten PLC funktioniert bereits fehlerfrei; `MC_Servo` und `MC_Interpolator` werden korrekt als Know-how-geschützt erkannt und bislang übersprungen. 

Der nächste Schritt ist daher wie geplant: **einen geschützten Baustein ohne Entsperren direkt exportieren** und anschließend prüfen, was TIA V21 tatsächlich in die XML schreibt. Noch **kein Passwort und kein Entsperren**.

Nimm dafür als nächsten Test `MC_Servo`. Ersetze deine `Program.cs` komplett durch:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Siemens.Engineering;
using Siemens.Engineering.HW;
using Siemens.Engineering.HW.Features;
using Siemens.Engineering.SW;
using Siemens.Engineering.SW.Blocks;

namespace TiaOpennessTest
{
    internal class Program
    {
        static void Main(string[] args)
        {
            var processes = TiaPortal.GetProcesses();

            Console.WriteLine($"Gefundene TIA-Instanzen: {processes.Count}");

            if (processes.Count == 0)
                return;

            using (TiaPortal tiaPortal = processes[0].Attach())
            {
                var project = tiaPortal.Projects[0];

                PlcSoftware firstPlc = null;

                foreach (Device device in project.Devices)
                {
                    firstPlc = GetPlcSoftware(device);

                    if (firstPlc != null)
                        break;
                }

                if (firstPlc == null)
                {
                    Console.WriteLine("Keine PLC gefunden.");
                    return;
                }

                Console.WriteLine($"PLC: {firstPlc.Name}");

                PlcBlock block = FindBlock(
                    firstPlc.BlockGroup,
                    "MC_Servo");

                if (block == null)
                {
                    Console.WriteLine("MC_Servo wurde nicht gefunden.");
                    return;
                }

                Console.WriteLine($"Baustein: {block.Name}");
                Console.WriteLine($"Typ: {block.GetType().Name}");
                Console.WriteLine(
                    $"Know-how-geschützt: {block.IsKnowHowProtected}");

                string exportDirectory =
                    @"C:\TiaExportTest\ProtectedTest";

                Directory.CreateDirectory(exportDirectory);

                string exportFile =
                    Path.Combine(
                        exportDirectory,
                        block.Name + ".xml");

                try
                {
                    block.Export(
                        new FileInfo(exportFile),
                        ExportOptions.WithDefaults);

                    Console.WriteLine();
                    Console.WriteLine("Export-Aufruf erfolgreich.");
                    Console.WriteLine(exportFile);

                    FileInfo fileInfo = new FileInfo(exportFile);

                    if (fileInfo.Exists)
                    {
                        Console.WriteLine(
                            $"Dateigröße: {fileInfo.Length} Bytes");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine();
                    Console.WriteLine("Export fehlgeschlagen:");
                    Console.WriteLine(ex.GetType().FullName);
                    Console.WriteLine(ex.Message);
                }
            }
        }

        private static PlcSoftware GetPlcSoftware(
            HardwareObject hardwareObject)
        {
            Queue<HardwareObject> queue =
                new Queue<HardwareObject>();

            queue.Enqueue(hardwareObject);

            while (queue.Count > 0)
            {
                HardwareObject current = queue.Dequeue();

                foreach (DeviceItem deviceItem in current.Items)
                {
                    if (!deviceItem.IsPlugged)
                        continue;

                    if (deviceItem.Classification.HasFlag(
                        DeviceItemClassifications.CPU))
                    {
                        SoftwareContainer softwareContainer =
                            deviceItem.GetService<SoftwareContainer>();

                        if (softwareContainer?.Software
                            is PlcSoftware plcSoftware)
                        {
                            return plcSoftware;
                        }
                    }

                    queue.Enqueue(deviceItem);
                }
            }

            return null;
        }

        private static PlcBlock FindBlock(
            PlcBlockGroup group,
            string blockName)
        {
            foreach (PlcBlock block in group.Blocks)
            {
                if (string.Equals(
                    block.Name,
                    blockName,
                    StringComparison.OrdinalIgnoreCase))
                {
                    return block;
                }
            }

            foreach (PlcBlockGroup childGroup in group.Groups)
            {
                PlcBlock result =
                    FindBlock(childGroup, blockName);

                if (result != null)
                    return result;
            }

            return null;
        }
    }
}
```

Danach nur:

```powershell
dotnet build
dotnet run
```

Wenn der Export akzeptiert wird, sollte anschließend ungefähr diese Datei existieren:

```text
C:\TiaExportTest\ProtectedTest\MC_Servo.xml
```

Schick mir danach einfach die Ausgabe von `dotnet run`. Dann prüfen wir **erst im nächsten Schritt** den Inhalt dieser XML.

---

# you asked

message time: 2026-10-27 05:30:37

PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet build
  Wiederherzustellende Projekte werden ermittelt...
  Alle Projekte sind für die Wiederherstellung auf dem neuesten Stand.
  TiaOpennessTest -> C:\Users\Administrator\sources\TiaOpennessTest\bin\Debug\net48\TiaOpennessTest.exe

Der Buildvorgang wurde erfolgreich ausgeführt.
    0 Warnung(en)
    0 Fehler

Verstrichene Zeit 00:00:01.03
PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet run
Gefundene TIA-Instanzen: 1
PLC: =ST010+CAB1-KF0
Baustein: Main ... exportiert
Baustein: Global_Datatransfer ... exportiert
Baustein: MC_Servo ... übersprungen (Know-how-geschützt)
Baustein: MC_Interpolator ... übersprungen (Know-how-geschützt)

Export abgeschlossen.
Exportiert:           2
Geschützt übersprungen: 2
Fehler:               0
Zielordner:           C:\TiaExportTest\=ST010+CAB1-KF0
PS C:\Users\Administrator\sources\TiaOpennessTest> 
 *  Verlauf wiederhergestellt 

PS C:\Users\Administrator\sources\TiaOpennessTest> 
 *  Verlauf wiederhergestellt 

PS C:\Users\Administrator\sources\TiaOpennessTest> 
 *  Verlauf wiederhergestellt 

PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet build
  Wiederherzustellende Projekte werden ermittelt...
  Alle Projekte sind für die Wiederherstellung auf dem neuesten Stand.
  TiaOpennessTest -> C:\Users\Administrator\sources\TiaOpennessTest\bin\Debug\net48\TiaOpennessTest.exe

Der Buildvorgang wurde erfolgreich ausgeführt.
    0 Warnung(en)
    0 Fehler

Verstrichene Zeit 00:00:02.77
PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet run
Gefundene TIA-Instanzen: 1
PLC: =ST010+CAB1-KF0
Baustein: MC_Servo
Typ: OB
Know-how-geschützt: True

Export-Aufruf erfolgreich.
C:\TiaExportTest\ProtectedTest\MC_Servo.xml
Dateigröße: 4080 Bytes
PS C:\Users\Administrator\sources\TiaOpennessTest>

---

# chatgpt response

Sehr gut. Damit ist der nächste wichtige Punkt bestätigt:

**TIA V21 erlaubt den XML-Export eines Know-how-geschützten Bausteins auch ohne Passwort.** In deinem Fall wurde `MC_Servo` erfolgreich als 4080-Byte-XML exportiert.

Siemens dokumentiert für V21 genau dieses Verhalten: Ohne vorheriges Entsperren enthält der Export **nur die öffentliche Bausteinschnittstelle**; der geschützte Programmcode wird nicht exportiert. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v21/tia-portal-openness-api-for-automation-of-engineering-workflows/export/import/importing/exporting-data-of-a-plc-device/blocks/exporting-blocks-with-know-how-protection?utm_source=chatgpt.com))

Jetzt prüfen wir nur den tatsächlichen Inhalt deiner XML. Führe bitte diesen PowerShell-Befehl aus:

```powershell
Get-Content "C:\TiaExportTest\ProtectedTest\MC_Servo.xml"
```

Falls die Ausgabe zu lang/unübersichtlich ist, nimm stattdessen:

```powershell
Get-Content "C:\TiaExportTest\ProtectedTest\MC_Servo.xml" | Select-Object -First 100
```

Schick mir diese Ausgabe. Dann schauen wir konkret nach, **was bei `MC_Servo` noch enthalten ist und was wegen des Know-how-Schutzes fehlt**. Erst danach gehen wir ans Entsperren mit `PlcBlockProtectionProvider`.

---

# you asked

message time: 2026-10-27 05:32:24

PS C:\WINDOWS\system32> Get-Content "C:\TiaExportTest\ProtectedTest\MC_Servo.xml" | Select-Object -First 100
<?xml version="1.0" encoding="utf-8"?>
<Document>
  <Engineering version="V21" />
  <DocumentInfo>
    <Created>2026-10-27T04:30:23.7201457Z</Created>
    <ExportSetting>WithDefaults</ExportSetting>
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
  <SW.Blocks.OB ID="0">
    <AttributeList>
      <Interface>
        <Sections xmlns="http://www.siemens.com/automation/Openness/SW/Interface/v5">
          <Section Name="Input">
            <Member Name="Initial_Call" Datatype="Bool" Accessibility="Public" Informative="true" />
            <Member Name="PIP_Input" Datatype="Bool" Accessibility="Public" Informative="true" />
            <Member Name="PIP_Output" Datatype="Bool" Accessibility="Public" Informative="true" />
            <Member Name="IO_System" Datatype="USInt" Accessibility="Public" Informative="true" />
            <Member Name="Event_Count" Datatype="Int" Accessibility="Public" Informative="true" />
            <Member Name="Synchronous" Datatype="Bool" Accessibility="Public" Informative="true" />
          </Section>
        </Sections>
      </Interface>
      <IsIECCheckEnabled>false</IsIECCheckEnabled>
      <Name>MC_Servo</Name>
      <Namespace />
      <Number>91</Number>
      <ProgrammingLanguage>LAD</ProgrammingLanguage>
      <SecondaryType>MCServo</SecondaryType>
      <SetENOAutomatically>false</SetENOAutomatically>
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
        </ObjectList>
      </MultilingualText>
      <MultilingualText ID="4" CompositionName="Title">
        <ObjectList>
          <MultilingualTextItem ID="5" CompositionName="Items">
            <AttributeList>
              <Culture>de-DE</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
          <MultilingualTextItem ID="6" CompositionName="Items">
            <AttributeList>
              <Culture>en-GB</Culture>
              <Text />
            </AttributeList>
          </MultilingualTextItem>
        </ObjectList>
      </MultilingualText>
PS C:\WINDOWS\system32>

---

# chatgpt response

Ja — das bestätigt exakt das erwartete Verhalten.

In deiner XML steht bei `MC_Servo` nur die sichtbare Struktur mit Metadaten und der öffentlichen Schnittstelle, zum Beispiel `Interface`, `Name`, `Number`, `ProgrammingLanguage` und `SecondaryType`. Ein eigentlicher Programmkörper ist in deinem Ausschnitt nicht enthalten. Siemens dokumentiert für TIA Portal V21 ausdrücklich: Wird ein Know-how-geschützter Baustein **ohne vorheriges Entsperren** exportiert, wird nur die öffentliche Bausteinschnittstelle exportiert. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v21/tia-portal-openness-api-for-automation-of-engineering-workflows/export/import/importing/exporting-data-of-a-plc-device/blocks/exporting-blocks-with-know-how-protection?utm_source=chatgpt.com))

Damit ist unser Test erfolgreich:

- `MC_Servo` wird als geschützt erkannt.
- `Export()` funktioniert trotzdem.
- Die XML enthält sichtbare Daten und Schnittstelle.
- Der geschützte Programmcode bleibt verborgen.
- Für den vollständigen Export müssen wir den Baustein vorher über `PlcBlockProtectionProvider` mit dem korrekten Passwort entsperren. Dafür muss die PLC offline sein. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v21/tia-portal-openness-api-for-automation-of-engineering-workflows/export/import/importing/exporting-data-of-a-plc-device/blocks/exporting-blocks-with-know-how-protection?utm_source=chatgpt.com))

Der nächste sinnvolle Schritt ist jetzt **nur zu testen, ob wir für `MC_Servo` den `PlcBlockProtectionProvider` bekommen**. Noch geben wir **kein Passwort ein und ändern keinen Schutz**.

Ich würde als Nächstes einen kleinen Testcode machen, der lediglich ausgibt:

```text
Baustein: MC_Servo
Know-how-geschützt: True
ProtectionProvider verfügbar: True
```

Wenn das klappt, gehen wir danach separat an `Unprotect()` und den Passwortdialog.

---

# you asked

message time: 2026-10-27 05:33:53

ok

---

# chatgpt response

Gut. Jetzt testen wir wirklich nur, ob TIA für den geschützten Baustein `MC_Servo` den `PlcBlockProtectionProvider` bereitstellt. Siemens sieht dafür `block.GetService<PlcBlockProtectionProvider>()` vor; für das spätere Entsperren ist die PLC offline erforderlich. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v20/tia-portal-openness-api-for-automation-of-engineering-workflows/tia-portal-openness-api/functions-for-accessing-the-data-of-a-plc-device/blocks/setting-and-removing-protections-from-a-block?utm_source=chatgpt.com))

Ersetze `Program.cs` komplett durch:

```csharp
using System;
using System.Collections.Generic;
using Siemens.Engineering;
using Siemens.Engineering.HW;
using Siemens.Engineering.HW.Features;
using Siemens.Engineering.SW;
using Siemens.Engineering.SW.Blocks;

namespace TiaOpennessTest
{
    internal class Program
    {
        static void Main(string[] args)
        {
            var processes = TiaPortal.GetProcesses();

            Console.WriteLine($"Gefundene TIA-Instanzen: {processes.Count}");

            if (processes.Count == 0)
                return;

            using (TiaPortal tiaPortal = processes[0].Attach())
            {
                var project = tiaPortal.Projects[0];

                PlcSoftware firstPlc = null;

                foreach (Device device in project.Devices)
                {
                    firstPlc = GetPlcSoftware(device);

                    if (firstPlc != null)
                        break;
                }

                if (firstPlc == null)
                {
                    Console.WriteLine("Keine PLC gefunden.");
                    return;
                }

                Console.WriteLine($"PLC: {firstPlc.Name}");

                PlcBlock block = FindBlock(
                    firstPlc.BlockGroup,
                    "MC_Servo");

                if (block == null)
                {
                    Console.WriteLine("MC_Servo wurde nicht gefunden.");
                    return;
                }

                Console.WriteLine($"Baustein: {block.Name}");
                Console.WriteLine(
                    $"Know-how-geschützt: {block.IsKnowHowProtected}");

                PlcBlockProtectionProvider protectionProvider =
                    block.GetService<PlcBlockProtectionProvider>();

                Console.WriteLine(
                    $"ProtectionProvider verfügbar: " +
                    $"{(protectionProvider != null)}");
            }
        }

        private static PlcSoftware GetPlcSoftware(
            HardwareObject hardwareObject)
        {
            Queue<HardwareObject> queue =
                new Queue<HardwareObject>();

            queue.Enqueue(hardwareObject);

            while (queue.Count > 0)
            {
                HardwareObject current = queue.Dequeue();

                foreach (DeviceItem deviceItem in current.Items)
                {
                    if (!deviceItem.IsPlugged)
                        continue;

                    if (deviceItem.Classification.HasFlag(
                        DeviceItemClassifications.CPU))
                    {
                        SoftwareContainer softwareContainer =
                            deviceItem.GetService<SoftwareContainer>();

                        if (softwareContainer?.Software
                            is PlcSoftware plcSoftware)
                        {
                            return plcSoftware;
                        }
                    }

                    queue.Enqueue(deviceItem);
                }
            }

            return null;
        }

        private static PlcBlock FindBlock(
            PlcBlockGroup group,
            string blockName)
        {
            foreach (PlcBlock block in group.Blocks)
            {
                if (string.Equals(
                    block.Name,
                    blockName,
                    StringComparison.OrdinalIgnoreCase))
                {
                    return block;
                }
            }

            foreach (PlcBlockGroup childGroup in group.Groups)
            {
                PlcBlock result =
                    FindBlock(childGroup, blockName);

                if (result != null)
                    return result;
            }

            return null;
        }
    }
}
```

Dann wieder nur:

```powershell
dotnet build
dotnet run
```

Im Idealfall sehen wir:

```text
Baustein: MC_Servo
Know-how-geschützt: True
ProtectionProvider verfügbar: True
```

Schick mir danach die Ausgabe. **Noch kein Passwort und kein `Unprotect()`** – zuerst stellen wir sicher, dass V21 den Provider bei deinem konkreten Baustein tatsächlich liefert.

---

# you asked

message time: 2026-10-27 05:35:21

PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet build
  Wiederherzustellende Projekte werden ermittelt...
  Alle Projekte sind für die Wiederherstellung auf dem neuesten Stand.
  TiaOpennessTest -> C:\Users\Administrator\sources\TiaOpennessTest\bin\Debug\net48\TiaOpennessTest.exe

Der Buildvorgang wurde erfolgreich ausgeführt.
    0 Warnung(en)
    0 Fehler

Verstrichene Zeit 00:00:00.90
PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet run
Gefundene TIA-Instanzen: 1
PLC: =ST010+CAB1-KF0
Baustein: MC_Servo
Know-how-geschützt: True
ProtectionProvider verfügbar: False
PS C:\Users\Administrator\sources\TiaOpennessTest>

---

# chatgpt response

Das Ergebnis ist wichtig: `MC_Servo` ist zwar Know-how-geschützt, aber **für genau diesen Block stellt TIA keinen `PlcBlockProtectionProvider` bereit**.

Das ist nicht automatisch ein Fehler in unserem Code. Siemens nennt mehrere Bedingungen dafür, dass der Provider verfügbar ist: Der Block muss unter anderem Know-how-schützbar, kompiliert, editierbar/unterstützt und kein Read-only-Objekt sein. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v20/tia-portal-openness-api-for-automation-of-engineering-workflows/tia-portal-openness-api/functions-for-accessing-the-data-of-a-plc-device/blocks/setting-and-removing-protections-from-a-block?utm_source=chatgpt.com))

Bei `MC_Servo` fällt auf, dass es ein spezieller System-OB mit `SecondaryType=MCServo` ist. Daher liegt nahe, dass dieser Motion-OB zwar als geschützt angezeigt wird, aber **nicht über Openness entsperrbar/editierbar ist**. Das ist eine Schlussfolgerung aus deinem konkreten Ergebnis; die Siemens-Seite bestätigt nur die allgemeinen Voraussetzungen für den Provider.

Wichtig ist außerdem: Der Export ohne Entsperren funktioniert weiterhin korrekt und liefert bei geschützten Blöcken nur die öffentliche Schnittstelle. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v21/tia-portal-openness-api-for-automation-of-engineering-workflows/export/import/importing/exporting-data-of-a-plc-device/blocks/exporting-blocks-with-know-how-protection?utm_source=chatgpt.com))

Als nächsten Schritt sollten wir deshalb **nicht mit `Unprotect()` weitermachen**, sondern prüfen, ob irgendein anderer geschützter, normaler Anwenderbaustein im Projekt einen Provider liefert. In deinem aktuellen Projekt sind die einzigen geschützten Bausteine aber offenbar `MC_Servo` und `MC_Interpolator`.

Ich würde deshalb jetzt als kleinen nächsten Test **für alle Bausteine ausgeben, ob ein `PlcBlockProtectionProvider` vorhanden ist**. Dann wissen wir sicher, ob das nur bei `MC_Servo` so ist oder generell bei diesen Motion-OBs.

---

# you asked

message time: 2026-10-27 05:36:05

ok

---

# chatgpt response

Dann testen wir jetzt alle Bausteine der ersten PLC und geben jeweils aus:

- Name
- Typ
- Know-how-Schutz
- ob ein `PlcBlockProtectionProvider` verfügbar ist

Ersetze `Program.cs` komplett durch:

```csharp
using System;
using System.Collections.Generic;
using Siemens.Engineering;
using Siemens.Engineering.HW;
using Siemens.Engineering.HW.Features;
using Siemens.Engineering.SW;
using Siemens.Engineering.SW.Blocks;

namespace TiaOpennessTest
{
    internal class Program
    {
        static void Main(string[] args)
        {
            var processes = TiaPortal.GetProcesses();

            Console.WriteLine($"Gefundene TIA-Instanzen: {processes.Count}");

            if (processes.Count == 0)
                return;

            using (TiaPortal tiaPortal = processes[0].Attach())
            {
                var project = tiaPortal.Projects[0];

                PlcSoftware firstPlc = null;

                foreach (Device device in project.Devices)
                {
                    firstPlc = GetPlcSoftware(device);

                    if (firstPlc != null)
                        break;
                }

                if (firstPlc == null)
                {
                    Console.WriteLine("Keine PLC gefunden.");
                    return;
                }

                Console.WriteLine($"PLC: {firstPlc.Name}");
                Console.WriteLine();

                ListProtectionProviders(firstPlc.BlockGroup);
            }
        }

        private static PlcSoftware GetPlcSoftware(
            HardwareObject hardwareObject)
        {
            Queue<HardwareObject> queue =
                new Queue<HardwareObject>();

            queue.Enqueue(hardwareObject);

            while (queue.Count > 0)
            {
                HardwareObject current = queue.Dequeue();

                foreach (DeviceItem deviceItem in current.Items)
                {
                    if (!deviceItem.IsPlugged)
                        continue;

                    if (deviceItem.Classification.HasFlag(
                        DeviceItemClassifications.CPU))
                    {
                        SoftwareContainer softwareContainer =
                            deviceItem.GetService<SoftwareContainer>();

                        if (softwareContainer?.Software
                            is PlcSoftware plcSoftware)
                        {
                            return plcSoftware;
                        }
                    }

                    queue.Enqueue(deviceItem);
                }
            }

            return null;
        }

        private static void ListProtectionProviders(
            PlcBlockGroup group)
        {
            foreach (PlcBlock block in group.Blocks)
            {
                PlcBlockProtectionProvider protectionProvider =
                    block.GetService<PlcBlockProtectionProvider>();

                Console.WriteLine($"Baustein: {block.Name}");
                Console.WriteLine($"  Typ: {block.GetType().Name}");
                Console.WriteLine(
                    $"  Know-how-geschützt: {block.IsKnowHowProtected}");
                Console.WriteLine(
                    $"  ProtectionProvider: {(protectionProvider != null)}");
                Console.WriteLine();
            }

            foreach (PlcBlockGroup childGroup in group.Groups)
            {
                ListProtectionProviders(childGroup);
            }
        }
    }
}
```

Dann:

```powershell
dotnet build
dotnet run
```

Besonders interessant sind die Zeilen für:

```text
MC_Servo
MC_Interpolator
```

Wenn dort beide `ProtectionProvider: False` zeigen, wissen wir ziemlich sicher, dass diese beiden Motion-OBs über diesen Openness-Mechanismus nicht entsperrbar sind. Schick mir danach einfach die komplette Ausgabe.

---

# you asked

message time: 2026-10-27 05:37:12

PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet build
  Wiederherzustellende Projekte werden ermittelt...
  Alle Projekte sind für die Wiederherstellung auf dem neuesten Stand.
  TiaOpennessTest -> C:\Users\Administrator\sources\TiaOpennessTest\bin\Debug\net48\TiaOpennessTest.exe

Der Buildvorgang wurde erfolgreich ausgeführt.
    0 Warnung(en)
    0 Fehler

Verstrichene Zeit 00:00:01.00
PS C:\Users\Administrator\sources\TiaOpennessTest> dotnet run
Gefundene TIA-Instanzen: 1
PLC: =ST010+CAB1-KF0

Baustein: Main
  Typ: OB
  Know-how-geschützt: False
  ProtectionProvider: True

Baustein: Global_Datatransfer
  Typ: GlobalDB
  Know-how-geschützt: False
  ProtectionProvider: True

Baustein: MC_Servo
  Typ: OB
  Know-how-geschützt: True
  ProtectionProvider: False

Baustein: MC_Interpolator
  Typ: OB
  Know-how-geschützt: True
  ProtectionProvider: False

PS C:\Users\Administrator\sources\TiaOpennessTest>

---

# chatgpt response

Genau. Jetzt haben wir die Ursache sauber eingegrenzt:

`Main` und `Global_Datatransfer` liefern jeweils einen `PlcBlockProtectionProvider`. `MC_Servo` und `MC_Interpolator` dagegen nicht.

Das passt zur Siemens-Dokumentation: Der `PlcBlockProtectionProvider` steht nur für Bausteine zur Verfügung, die u. a. **Know-how-schützbar, unterstützt bzw. editierbar und nicht schreibgeschützt** sind. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v20/tia-portal-openness-api-for-automation-of-engineering-workflows/tia-portal-openness-api/functions-for-accessing-the-data-of-a-plc-device/blocks/setting-and-removing-protections-from-a-block?utm_source=chatgpt.com))

Für die beiden Motion-Control-OBs ist das entscheidend: Siemens beschreibt `MC_Servo` und `MC_Interpolator` ausdrücklich als Know-how-geschützte System-OBs, deren Programmcode **nicht eingesehen oder verändert werden kann**. ([Siemens TIA](https://docs.tia.siemens.cloud/r/de-de/v21/s7-1200-motion-control-einsetzen-s7-1200/grundlagen-fur-das-arbeiten-mit-s7-1200-motion-control-s7-1200/profidrive-antrieb/analoge-antriebsanbindung-s7-1200/ablaufverhalten-s7-1200/organisationsbausteine-fur-motion-control-s7-1200?utm_source=chatgpt.com))

Damit ist klar: **Wir brauchen für diese beiden Bausteine keinen Passwortdialog. Sie lassen sich über Openness nicht entsperren.** Beim Export können wir nur die öffentliche Schnittstelle sichern, genau wie bei unserem erfolgreichen `MC_Servo.xml`-Test. Siemens bestätigt auch, dass ein geschützter Baustein ohne Entsperren nur mit seiner öffentlichen Schnittstelle exportiert wird. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v21/tia-portal-openness-api-for-automation-of-engineering-workflows/export/import/importing/exporting-data-of-a-plc-device/blocks/exporting-blocks-with-know-how-protection?utm_source=chatgpt.com))

Für unser späteres Exportprogramm sollten wir daher drei Fälle unterscheiden:

```text
Ungeschützt
→ vollständig exportieren

Geschützt + ProtectionProvider vorhanden
→ Passwort anfordern
→ entsperren
→ vollständig exportieren
→ Schutz wiederherstellen

Geschützt + ProtectionProvider NICHT vorhanden
→ sichtbare/öffentliche Schnittstelle exportieren
→ im Report als "nicht entsperrbar" kennzeichnen
```

Das ist für unser Tool eine wichtige Verbesserung gegenüber dem ursprünglichen Konzept: **`IsKnowHowProtected == true` bedeutet nicht automatisch, dass ein Passwort zum Entsperren verwendet werden kann.**

Als nächsten Schritt würde ich jetzt einen **normalen Baustein testweise selbst mit Know-how-Schutz versehen**, damit wir anschließend an einem tatsächlich entsperrbaren Baustein den kompletten Ablauf `Protect → Unprotect → Export` testen können. Dafür könnten wir z. B. mit einem eigens angelegten kleinen Test-FB arbeiten, damit wir `Main` oder deinen Global-DB nicht anfassen.

---

# you asked

message time: 2026-10-27 05:39:43

ok

---

# chatgpt response

Gut. Dann machen wir als nächsten Schritt einen **separaten Testbaustein**, damit wir an deinen echten Bausteinen nichts verändern.

Lege in TIA in der ersten PLC einen kleinen FB an, zum Beispiel:

```text
FB_OpennessTest
```

Der Inhalt kann minimal sein, zum Beispiel nur eine BOOL-Eingangsvariable und eine BOOL-Ausgangsvariable. Wichtig ist nur:

- der Baustein ist zunächst **nicht** Know-how-geschützt,
- er ist kompiliert,
- die PLC ist offline.

Wenn der FB angelegt ist, sag einfach **„fertig“**. Dann gebe ich dir den nächsten kleinen Testcode, der nur prüft, ob für `FB_OpennessTest` ein `PlcBlockProtectionProvider` verfügbar ist.

---

# you asked

message time: 2026-10-27 05:40:20

Können wir das auch überspringen?

---

# chatgpt response

Ja, können wir überspringen.

Dann halten wir für das spätere Tool einfach fest:

- normale ungeschützte Bausteine → vollständig exportieren
- geschützte Bausteine mit `ProtectionProvider` → später optional per Passwort behandeln
- geschützte Bausteine ohne `ProtectionProvider` → nur öffentliche Schnittstelle exportieren und entsprechend kennzeichnen

Der nächste sinnvolle Schritt ist damit: **nicht weiter am Schutz testen, sondern den Export auf alle PLCs im Projekt erweitern** statt nur auf die erste PLC.

---

# you asked

message time: 2026-10-27 05:43:12

Wir sollten nicht vergessen, ich bin technischer Redakteur und benötige ein weites gehend vollständiges Archiv aller Bausteine damit ich in Kombination mit weiteren Unterlagen zum Projekt neben allen anderen in der Betriebsanleitung auch das HMI detailliert und umfassend beschreiben kann

---

# chatgpt response

Ja — das ändert die Zielsetzung sinnvoll. Wir sollten nicht nur einen PLC-Block-Exporter bauen, sondern ein **möglichst vollständiges technisches Projektarchiv**, aus dem du später PLC, HMI und deren Zusammenhänge dokumentieren kannst.

Genau — dann sollten wir das Tool ab jetzt breiter denken. Der bisherige PLC-Blockexport bleibt ein Teil davon, aber dein eigentliches Ziel ist ein **technisches Projektarchiv für die Dokumentation**.

Für TIA Portal V21 können wir über Openness deutlich mehr exportieren als nur PLC-Bausteine. Siemens nennt unter anderem PLC-Bausteine, PLC-Variablentabellen, Variablen/Konstanten, Anwenderdatentypen und Technologieobjekte sowie auf HMI-Seite Bilder, Bildvorlagen, globale Bilder, Pop-ups, Slide-ins, Skripte, Text-/Grafiklisten, Zyklen, Verbindungen, Variablentabellen und Variablen. ([Siemens TIA](https://docs.tia.siemens.cloud/r/de-de/v21/tia-portal-openness-api-fur-die-automatisierung-von-engineering-workflows/export/import/uberblick/grundlagen-zum-import/export?utm_source=chatgpt.com))

Für deine Arbeit als technischer Redakteur würde ich deshalb als Zielstruktur ungefähr Folgendes vorsehen:

```text
Projektarchiv\
│
├─ 00_Project\
│   ├─ Manifest
│   ├─ Projektinformationen
│   └─ Geräteübersicht
│
├─ 10_PLC\
│   ├─ =ST010+CAB1-KF0\
│   │   ├─ Blocks\
│   │   ├─ PLC_Tags\
│   │   ├─ DataTypes\
│   │   ├─ TechnologyObjects\
│   │   └─ ExportReport
│   ├─ =ST020+CAB1-KF0\
│   └─ =ST030+CAB1-KF0\
│
├─ 20_HMI\
│   ├─ <HMI-Gerät>\
│   │   ├─ Screens\
│   │   ├─ ScreenTemplates\
│   │   ├─ Popups\
│   │   ├─ SlideIns\
│   │   ├─ Tags\
│   │   ├─ Connections\
│   │   ├─ Scripts\
│   │   ├─ TextLists\
│   │   ├─ GraphicLists\
│   │   └─ Cycles\
│
├─ 30_Hardware\
│   └─ Geräte-/Modulübersichten
│
└─ 90_Report\
    ├─ export_manifest.json
    └─ ExportReport.html
```

Gerade für die HMI-Dokumentation sind **Screens + Tags + PLC-Verbindungen + Skripte + Textlisten** besonders wertvoll. Damit können wir später beispielsweise nachvollziehen, welches Bild welche Variablen verwendet, welche PLC dahintersteht, welche Bedienhandlungen vorgesehen sind und welche Skripte beteiligt sind. Bei Unified lassen sich beispielsweise auch Tag-Tabellen in strukturierten `.hmi.yml`-Dateien und globale Skripte als JavaScript/YAML exportieren. ([Siemens TIA](https://docs.tia.siemens.cloud/r/en-us/v21/functions-for-accessing-the-data-of-an-hmi-unified-device/hmisoftware/tagtables/exporting-and-importing-tag-tables?contentId=c~Q5ydoG0Zy2i5dOG8rGrQ&utm_source=chatgpt.com))

Und ganz wichtig: Wir sollten nicht nur „erfolgreich exportiert“ zählen. Das Archiv sollte bei **jedem Objekt dokumentieren, wie vollständig der Export ist**. Bei deinen `MC_Servo`-/`MC_Interpolator`-OBs würden wir beispielsweise festhalten: *Know-how-geschützt, ProtectionProvider nicht verfügbar, nur öffentliche Schnittstelle archiviert*. So weißt du später bei der Dokumentation sofort, dass dort bewusst Informationen fehlen und nicht etwa der Exporter etwas vergessen hat.

Der bisherige Test hat bereits gezeigt, dass wir die PLCs erkennen, Bausteine rekursiv finden, Schutzstatus unterscheiden und XML exportieren können. 

**Ich würde daher jetzt nicht weiter am Passwortthema arbeiten.** Als nächsten Schritt sollten wir die **HMI-Geräte im Projekt erkennen und auflisten**, genau so klein und kontrolliert wie wir es bei den PLCs gemacht haben. Noch kein HMI-Export – zunächst nur feststellen: *Welche HMI-Geräte sind vorhanden, welcher Typ, welcher Name, welche HMI-Software?* Danach bauen wir den vollständigen Archivexport Stück für Stück auf.

---

# you asked

message time: 2026-10-27 05:45:28

ok, aber wir sollten auch berücksichtigen, dass wir auch auf vorherige TIA-Versionen zugreifen müssen?

---
Powered by [AI Exporter](https://saveai.net)