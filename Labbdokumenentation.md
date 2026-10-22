William Avramidis 21-11-2026 ICX26.  Sätter upp fil och map till konsultgrupp

Installerat ubuntu server med inget extra tillägg och svensk tangetbord

Satt upp en statisk ip address som är då 192.168.10.10/24 och default är 192.168.10.1 och DNS är 8.8.8.8 (googles) alternativt 1.1.1.1

| Hostname | Operativesystem | IP address | Subnetmask | Gateway |
| :--- | :--- | :--- | :--- | :--- |
| Wille | Ubuntu 26.01 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| wille | windows 11 | 192.168.10.15 | 255.255.255.0 |192.168.10.1 |
| | | |  |  |


Har lagt in anteckningar samt satt chmod 640 på den filen och tilldelat 750 på mappen, samt har tilldelat mappen och filen till konsultgruppen
# Kommandos som användes för att kunna utföra detta:

# sudo groupadd konsulter
Är kommandot för att lägga till en grupp

# sudo mkdir -p /data/konsultdata
Detta kommandot skapar en mapp

# sudo touch /var/systementor/konsultdata/anteckningar.txt

Med detta kommandot så skapas anteckningar inom mappen konsultdata

# sudo chmod 750 /data/konsultdata
(Ägaren / User): rwx – Ägaren (root) kan läsa, skriva och gå in i/exekvera i mappen.
5 (Gruppen / Group): r-x – Medlemmar i mappens grupp kan läsa och gå in i/exekvera i mappen, men inte skapa eller ta bort filer.
0 (Övriga / Others): --- – Alla andra användare på systemet saknar helt tillgång.

# sudo chmod 640 /var/systementor/konsultdata/anteckningar.txt

6 (Ägaren / User): rw- – Ägaren kan läsa och skriva (ändra) i filen.
4 (Gruppen / Group): r-- – Medlemmar i filens grupp kan enbart läsa filen (inte ändra).
0 (Övriga / Others): --- – Alla andra användare har ingen tillgång alls.

# sudo nano /etc/netplan/00-installer.yaml (kan vara annorlunda för andra)

Kommandot för att kunna ändra nätverks inställningar inom linux server tex, i mitt fall från dhcp 4 till Statisk IP address, obs kan vara annorlunda just i 00-installer.yaml

# sudo netplan apply

Då sparas din nätverks config med hjälp av denna kommandot 

# ls -ld /var/systementor/konsultdata /var/systementor/konsultdata/anteckningar.txt
Detta kommandot kan du se vilken som är mappen och vilken som är filen.


# Windows delen (Gammal)

# New-item -itemtype Directory -Path C:\Systementor\Konsultdata

Med detta kommandot so skapades en mapp genom CLI


# (Get-Acl "C: \systementor\"). access | format-table identityReference, FilesystemRights, AccessControlType, IsInherited

Detta kommandot tilldelade rättigheter för mappen Konsultdata 

# Ipconfig

Där kan man se vilken ip address du har osv




# AI logg och utvärdering 

Prompten var följande Ge mig information om hur IPconfig /all fungerar och vilka scenarion är det viktigt att använda det https://chatgpt.com/uc/6abe2bc6-b770-83ea-b34a-0568a37f8585

Detta var svaret och det var korrekt då den beskriver i vilka scenario som Ipconfig /all kan användas i och visar exempel när det kan vara använtbart tex flushdns eller renew, samt visar vilka andra commandos som kan användas med hjälp av Ipconfig / dns tex och beskriver vad /all gör exakt men också ger ut information om vad exakt de dem gör och vad som kommer hända om den kommandos körs. Den informationen de gav, stammer väldig bra om man jämför med andra källor: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig https://www.teamviewer.com/en/insights/what-does-ipconfigall-do/