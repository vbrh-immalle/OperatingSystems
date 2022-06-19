# Operating Systems

Een OS is systeem-software met een aantal belangrijke taken:

- **procesbeheer** (programma's in het RAM-geheugen laden, uitvoeren, *killen*, ...)
- **geheugenbeheer** (zorgen dat elk proces het werkgeheugen mag gebruiken waar het om vraagt)
- **communicatie met de hardware** (een hardware-fabrikant schrijft een **driver** om het apparaat met een OS te laten samenwerken)

> Indien bepaalde hardware aanwezig is, zijn er nog enkele elementaire taken die OS's voor zich kunnen nemen, b.v.:

- USB-apparaten
	- toetsenborden
		- ondersteuning voor verschillende toetsenbord-layouts
- schijf-controllers
	- een OS kan overweg met verschillende soorten opslagmedia zoals HD's, SSD's, optische schijven, USB-sticks, ...
	- elk OS ondersteunt meerdere **bestandssystemen** zoals
		- Windows: FAT, FAT32, NTFS, ...
		- Linux: ext3, ext4, ...
		- macOS: APFS, ...
		- ...
- netwerkkaarten (WiFi, Bluetooth, UTP, ...)
	- een netwerk-OS heeft een **TCP/IP-stack** waardoor een machine volgens vastgelegde afspraken (protocols, netwerklagenmodel) kan communiceren met andere computers (zelfs met andere OS's) en apparaten op een netwerk of het Internet

## User- vs kernel-space
Een OS-distributie bestaat altijd uit een *systeem*-gedeelte maar meestal ook een hele hoop *tools* en *applicaties*.

> Denk b.v. aan het programma `notepad` bij Windows. Dit is een user-space applicatie maar wordt wel met Windows meegedistribueerd.

- User-space: hierin worden gewone processen uitgevoerd
	- Het OS beheert het (virtuele) geheugen, beslist hoeveel rekenkracht het proces krijgt, ...
	- Een user-space programma heeft maar beperkte rechten en meestal geen weet van de precieze hardware waarop het draait
- Kernel-space: hier wordt de low-level systeem-software (zoals drivers) uitgevoerd

> Een slecht geschreven driver kan gans het systeem crashen!

## Virtueel geheugen
Applicaties hoeven niet te weten hoeveel RAM-geheugen werkelijk. Het OS kan dit *faken* en gebruikt achter de schermen een *wisselbestand* (**swap-file**).

> Processen of b.v. tabbladen in de webbrowser die al het langst niet meer actief zijn geweest, wordt *geswapt* naar disk en worden door het OS pas terug in het fysieke RAM-geheugen geladen als ze weer actief worden gemaakt.

## Multi-tasking
Een multi-tasking OS kan meerdere processen tegelijk draaien. Het geeft de CPU dan de opdracht om zeer snel te wisselen tussen de verschillende processen. Het lijkt dan of al deze processen gelijktijdig draaien maar bij een single-core CPU is dit niet zo.

## Multi-threading
Multi-threading is een manier om binnen een proces toch verschillende *code-paden* te hebben en dingen gelijktijdig te doen. De evolutie naar multi-core CPU's heeft ervoor gezorgd dat meer software op een multi-threaded manier wordt geprogrammeerd.

Threads behoren tot hetzelfde proces maar kunnen b.v. gepauzeerd worden terwijl ze wachten op data. In het beste geval kunnen meerdere threads effectief gelijktijdig worden uitgevoerd door de verschillende CPU-cores. Soms moeten ze natuurlijk met elkaar overeenstemmen en moet een thread wachten op een andere thread.

## DLL's
**Dynamically Loadable Libraries** zijn *bibliotheken* met uitvoerbare code die door het OS *dynamisch* in het RAM-geheugen kunnen geladen worden. 

Een `.exe`-bestand dat van schijf wordt uitgevoerd, zal door het OS worden uitgelezen en de uitvoerbare code zal ergens in het RAM-geheugen worden gezet. Zeer vaak gebruiken `.exe`'s ook nog op het systeem aanwezige `.dll`-bestanden voor extra uitvoerbare code. Het OS zorgt ervoor dat alle uitvoerbare code die in een proces nodig heeft, ergens in het geheugen kan terugvinden.

DLL's zijn ook een manier waarmee processen een stukje uitvoerbare code kunnen delen met elkaar. 

> Denk b.v. aan het dialoogvenster om bestanden te openen in Windows. Vele applicaties gebruiken dit. Dankzij DLL's kan de uitvoerbare code voor zo'n dialoogvenster slechts 1x in het RAM-geheugen aanwezig zijn, terwijl toch verschillende van de code gebruik kunnen maken.
