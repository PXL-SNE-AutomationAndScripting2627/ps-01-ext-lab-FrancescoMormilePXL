# Deel 1 — Introductie en installatie

## 1. Waarom scripting?

Scripting is nuttig voor systeem- en netwerkbeheer omdat je hiermee veel beheertaken kunt automatiseren.

### Enkele voordelen zijn:

1. Herhalende taken kunnen automatisch uitgevoerd worden, waardoor je tijd bespaart.
2. Je kunt dezelfde configuratie op meerdere computers uitvoeren zonder alles handmatig te doen.
3. Scripts verkleinen de kans op menselijke fouten omdat dezelfde opdrachten telkens op dezelfde manier uitgevoerd worden.
4. Je kunt scripts gebruiken om informatie over systemen, gebruikers, processen en netwerken op te vragen.
5. Scripts kunnen gebruikt worden voor onderhoudstaken zoals software installeren, processen beheren en firewallregels configureren.

## 2. Package managers

### 2.1 Wat is een package manager?

Een package manager is een programma waarmee softwarepakketten beheerd kunnen worden. Een package manager kan software automatisch zoeken, downloaden, installeren, bijwerken en verwijderen. Hierbij worden ook afhankelijkheden en de juiste installatiebestanden automatisch beheerd.

### 2.2 Waarom gebruik je een package manager?

Voordelen van een package manager zijn:

1. Software kan met een commando geinstalleerd worden.
2. Updates kunnen eenvoudiger en sneller uitgevoerd worden.
3. De package manager zoekt automatisch de juiste versie en afhankelijkheden.
4. Je hoeft niet zelf websites af te zoeken en installatiebestanden te downloaden.
5. Installaties zijn gemakkelijker te automatiseren met scripts.

### 2.3 Software installeren met een package manager

#### 2.3.1 PowerShell 7.x

Package manager: Winget

Gebruikte commando's:

```powershell
winget search PowerShell
winget list --id Microsoft.PowerShell

#### 2.3.2 Windows Terminal

Package manager: Winget

Gebruikte commando's:

```powershell
winget search "Windows Terminal"
winget install --id Microsoft.WindowsTerminal -e

#### 2.3.3 Visual Studio Code

Package manager: Winget

Gebruikte commando's:

```powershell
winget search "Visual Studio Code"
winget install --id Microsoft.VisualStudioCode -e

#### 2.3.4 Windows-versie van grep

Package manager: Winget

Gebruikte commando's:

```powershell
winget search grep
winget install --id GnuWin32.Grep -e

#### 2.3.5 BusyBox

Package manager: Winget

Gebruikte commando's:

```powershell
winget search BusyBox
winget install --id frippery.busybox-w32 -e

#### 2.3.6 Hoe werk je BusyBox bij?

BusyBox kan met Winget bijgewerkt worden met:

```powershell
winget upgrade --id frippery.busybox-w32 -e

## 3. PowerShell-versie

### 3.1 Toon de PowerShell-versie in je huidige sessie

Gebruikt commando:

```powershell
$PSVersionTable

### 3.2 Andere manieren om de PowerShell-versie op te vragen

Alternatief 1:

```powershell
$Host.Version

Dit toont alleen de versie-informatie van de huidige PowerShell-host, zoals Major, Minor, Build en Revision.

Alternatief 2:

```powershell
Get-Host

Dit toont informatie over de huidige PowerShell-host, waaronder de versie, naam en andere hostgegevens.

Vergelijking:

$PSVersionTable toont de meeste informatie over PowerShell en het systeem.

$Host.Version toont vooral alleen het versienummer.
Get-Host toont informatie over de PowerShell-host, inclusief de versie.

## 4. PowerShell execution policies

### 4.1 Controleer de actieve execution policy

Gebruikt commando:

```powershell
Get-ExecutionPolicy

### 4.2 Toon de execution policies voor alle scopes

Gebruikt commando:

```powershell
Get-ExecutionPolicy -List

Dit commando toont de execution policy voor alle scopes, waaronder:
- MachinePolicy
- UserPolicy
- Process
- CurrentUser
- LocalMachine

### 4.3 Stel de policy voor LocalMachine in

Om de execution policy voor `LocalMachine` op `RemoteSigned` te zetten:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine

Voor Unrestricted:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope LocalMachine

### 4.4 Zoek help over execution policies

Algemene informatie:

```powershell
Get-Help about_Execution_Policies

Gedetailleerde informatie over de cmdlet:

```powershell
Get-Help Set-ExecutionPolicy -Full

### 4.5 Zoek help over één parameter

Gebruikt commando:

```powershell
Get-Help Set-ExecutionPolicy -Parameter ExecutionPolicy

## 5. PowerShell gebruiken in Visual Studio Code

Ik installeerde de extensie `PowerShell` van Microsoft in Visual Studio Code.

Ik controleerde of de extensie werkte door een `.ps1`script uit te voeren met het volgende inhoud:

```powershell
Write-Output "PowerShell werkt in VS Code"

uitvoer:
PowerShell werkt in VS Code

## 6. Eerste script: Naam.ps1

Ik maakte het script `scripts/Naam.ps1` met de volgende inhoud:

```powershell
Write-Output "Naam: Francesco Mormile"
Write-Output "Woonplaats: Houthalen-Helchteren"

Voerde het uit vanuit de terminal van mijn pc met:

```powershell
cd C:\ps-01-ext-lab-FrancescoMormilePXL
.\scripts\naam.ps1

in VS Code met:
.\scripts\naam.ps1

### 6.2 Hernoem het script

Ik heb `Naam.ps1` hernoemd naar `Mijn Naam.ps1`.

Omdat de bestandsnaam een spatie bevat, moet het pad tussen aanhalingstekens geplaatst worden zodat PowerShell de volledige bestandsnaam als één pad behandelt.

Ik voerde het script uit met:

```powershell
& ".\scripts\Mijn Naam.ps1"

Daarna heb ik het script ook uitgevoerd vanuit Visual Studio Code.

## 7. Visual Studio Code starten als administrator

Ik heb Windows Taakplanner gebruikt om Visual Studio Code met administratorrechten te starten zonder bij elke start opnieuw een UAC-melding te krijgen.

Ik maakte een taak met de naam `VSCode Admin`.

Bij de taak heb ik ingesteld:
- Alleen uitvoeren als gebruiker is aangemeld
- Met hoogste bevoegdheden uitvoeren
- De energievoorwaarden voor netstroom uitgeschakeld

Als programma gebruikte ik:

C:\Users\franc\AppData\Local\Programs\Microsoft VS Code\Code.exe

Met de parameters:

--new-window --user-data-dir  "C:\Users\franc\AppData\Roaming\Code-Admin"

Daarna maakte ik twee snelkoppelingen die deze geplande taak uitvoeren.
Beide snelkoppelingen heb ik getest en Visual Studio Code opende met administratorrechten zonder dat ik de UAC-instellingen moest verlagen.

## 8. Help over processen

### 8.1 Zoek help met de algemene zoekterm process

Gebruikt commando:

```powershell
Get-Help *process*

### 8.2 Vraag meer gedetailleerde informatie op

Voor gedetailleerde help:

```powershell
Get-Help Get-Process -Detailed

Voor volledige help:

```powershell
Get-Help Get-Process -Full

Voor Online help:

```powershell
Get-Help Get-Process -Online

## 9. Cmdlets ontdekken met Get-Command

### 9.1 Geef een overzicht van alle Cmdlets

Gebruikt commando:

```powershell
Get-Command -CommandType Cmdlet

### 9.2 Leg de volgende opdrachten uit

#### 9.2.1 `Get-Command -Name *process*`

Gebruikt commando:

```powershell
Get-Command -Name *process*
```

Antwoord:

Dit commando zoekt naar alle beschikbare PowerShell-commando's waarvan de naam het woord `process` bevat.

De `*` is een wildcard. Dit betekent dat er vóór en na het woord `process` nog andere tekst mag staan.

Dit commando zoekt dus breed naar commando's die iets met processen te maken hebben.

#### 9.2.2 `Get-Command -Noun Process`

Gebruikt commando:

```powershell
Get-Command -Noun Process

Antwoord:

Dit commando toont alle PowerShell-cmdlets waarvan de `Noun` gelijk is aan `Process`.

Bij deze cmdlets is `Process` telkens de `Noun`.

#### 9.2.3 `Get-Command -Verb Get -Noun Process`

Gebruikt commando:

```powershell
Get-Command -Verb Get -Noun Process
```

Antwoord:

Dit commando zoekt specifiek naar een PowerShell-cmdlet met het werkwoord `Get` en het zelfstandig naamwoord `Process`.

Het resultaat is:

```text
Get-Process
```

`Get` betekent dat informatie wordt opgevraagd en `Process` geeft aan dat het over processen gaat.

#### 9.2.4 `Get-Command -Verb Out`

Gebruikt commando:

```powershell
Get-Command -Verb Out

Antwoord:

Dit commando toont alle beschikbare PowerShell-cmdlets waarvan het werkwoord `Out` is.

`Out`-cmdlets worden gebruikt om uitvoer naar een bepaalde bestemming of vorm te sturen.

Voorbeelden zijn:

```text
Out-File
Out-Host
Out-Printer
Out-String
```

`Out-File` stuurt uitvoer naar een bestand.  
`Out-Host` stuurt uitvoer naar het scherm.  
`Out-Printer` stuurt uitvoer naar een printer.  
`Out-String` zet uitvoer om naar tekst.

## 10. Processen en PowerShell-objecten

### 10.1 Welke twee cmdlets gebruik je om informatie over processen te zoeken?

Gebruikte cmdlets:

```powershell
Get-Help *process*

```powershell
Get-Command -Name *process*

Antwoord:

`Get-Help` gebruik ik om helpinformatie over processen te zoeken.

`Get-Command` gebruik ik om beschikbare PowerShell-commando's te zoeken die met processen te maken hebben.
````

### 10.2 Welke cmdlet vraagt alle systeemprocessen op?

Gebruikt commando:

```powershell
Get-Process
```

Antwoord:

De cmdlet `Get-Process` vraagt alle actieve processen op het systeem op.

De uitvoer toont informatie over de processen, zoals de procesnaam, het proces-ID en het geheugengebruik.

### 10.3 Hoe open je de online help van deze cmdlet?

Gebruikt commando:

```powershell
Get-Help Get-Process -Online
```

Antwoord:

Met de parameter `-Online` opent PowerShell de online help en documentatie van de cmdlet `Get-Process`.

### 10.4 Hoe toon je alleen de syntaxis van deze cmdlet?

Gebruikt commando:

```powershell
Get-Help Get-Process -Syntax
```

Antwoord:

Met de parameter `-Syntax` toont PowerShell alleen de mogelijke syntaxis van de cmdlet `Get-Process`.

### 10.5 Hoe toon je help over de parameter `Id`?

Gebruikt commando:

```powershell
Get-Help Get-Process -Parameter Id
```

Antwoord:

Met `-Parameter Id` toont PowerShell alleen de helpinformatie over de parameter `Id` van de cmdlet `Get-Process`.

### 10.6 Hoe toon je alle properties van de uitgevoerde processen?

Gebruikt commando:

```powershell
Get-Process | Get-Member -MemberType Properties
```

Antwoord:

`Get-Process` vraagt de processen op en stuurt deze via de pipeline `|` door naar `Get-Member`.

Met `-MemberType Properties` worden de properties van de procesobjecten weergegeven.

### 10.7 Hoe toon je alle methods van de uitgevoerde processen?

Gebruikt commando:

```powershell
Get-Process | Get-Member -MemberType Methods
```

Antwoord:

`Get-Process` vraagt de processen op en stuurt de procesobjecten via de pipeline door naar `Get-Member`.

Met `-MemberType Methods` worden alle methods weergegeven die op deze procesobjecten beschikbaar zijn.