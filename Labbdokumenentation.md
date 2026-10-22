William Avramidis 21-11-2026 ICX26.  
# Beskrvining

Labbmilijön är ubuntu server och windows 11 vm, 
Konfigurat statisk ip addresser, 
fil&mapp behörigheter i windows och linux med least privilege, 
steg för steg hur det utfördes, 

# Labbmiljö & Nätverk
| Hostname | Operativesystem | IP address | Subnetmask | Gateway |
| :--- | :--- | :--- | :--- | :--- |
| Wille | Ubuntu 26.01 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| wille | windows 11 home | 192.168.10.15 | 255.255.255.0 |192.168.10.1 |

Har lagt in anteckningar samt satt chmod 640 på den filen och tilldelat 750 på mappen, samt har tilldelat mappen och filen till konsultgruppen

# Steg för Steg
Jag började med att skapa mappen som konsult gruppen som ska användas

Efter jag skapade mappen och gruppen då la jag till anteckningar, samt rättigheter

(chmod 750) Som då root (ägaren) kan skriva i men inte det överiga inte kan göra utan det kan bara läsa. 

Innan jag satt 640 på filen körde jag sudo chgrp konsulter /data/systementor/konsultdata/anteckningar.txt

samt satt 640 på filen då bara ägaren ska kunna redigera och lägga till saker i de här fallet, vanliga användare kan läsa vad som finns i den.

Sen gick jag in och ändrade på nätverks inställningar och stängde av servers dhcp4 för att kunna sätta en statisk ip address så den kan kommunicera bara med windows 11 vm

efter det så satt jag ditt konfigurationen, samt kollade att alla har rättigheter som behövs och att den kunde kommunicera med windows 11.

# Kommandos som användes för att kunna utföra detta:

# sudo groupadd konsulter
Är kommandot för att lägga till en grupp

<img width="520" height="25" alt="Image" src="https://github.com/user-attachments/assets/79e427bb-16a1-45ff-b9ae-28862669c35a" />

# sudo mkdir -p /data/konsultdata
Detta kommandot skapar en mapp

<img width="537" height="64" alt="Image" src="https://github.com/user-attachments/assets/3ce0bc16-1346-426c-97aa-6150e593f8a0" />

# sudo touch /var/systementor/konsultdata/anteckningar.txt

<img width="459" height="22" alt="Image" src="https://github.com/user-attachments/assets/dadf30ba-5813-4af6-ab38-803a63a87623" />

Med detta kommandot så skapas anteckningar inom mappen konsultdata

# sudo chmod 750 /data/konsultdata
<img width="200" height="19" alt="Image" src="https://github.com/user-attachments/assets/db96b356-4bef-42bb-a2d2-7ebc1f17206b" />

7 (Ägaren / User): rwx – Ägaren (root) kan läsa, skriva och gå in i/exekvera i mappen.

5 (Gruppen / Group): r-x – Medlemmar i mappens grupp kan läsa och gå in i/exekvera i mappen, men inte skapa eller ta bort filer.

0 (Övriga / Others): --- – Alla andra användare på systemet saknar helt tillgång.

# sudo chgrp konsulter /data/systementor/konsultdata/anteckningar.txt & Is -la

Med detta kommandot så tilldelar den filen till gruppen som man namnger (konsulter) samt ändrar gruppägarskap till konsulter och visar vilka behörigheter dem har på filen

<img width="368" height="28" alt="Image" src="https://github.com/user-attachments/assets/c18d022a-2246-40b7-8374-9ee09836b47c" />



<img width="373" height="91" alt="Image" src="https://github.com/user-attachments/assets/651372f6-81f3-4a3d-9388-80dd2deab70e" />


# sudo chmod 640 /var/systementor/konsultdata/anteckningar.txt

<img width="329" height="35" alt="Image" src="https://github.com/user-attachments/assets/90e30cfe-49f3-4bbf-95f0-b7feffeef083" />

6 (Ägaren / User): rw- – Ägaren kan läsa och skriva (ändra) i filen.

4 (Gruppen / Group): r-- – Medlemmar i filens grupp kan enbart läsa filen (inte ändra).

0 (Övriga / Others): --- – Alla andra användare har ingen tillgång alls.

# sudo nano /etc/netplan/00-installer.yaml (kan vara annorlunda för andra)

Kommandot för att kunna ändra nätverks inställningar inom linux server tex, i mitt fall från dhcp 4 till Statisk IP address, obs kan vara annorlunda just i 00-installer.yaml

<img width="863" height="576" alt="Image" src="https://github.com/user-attachments/assets/370aaa62-b1bb-4fc0-9f38-b65a376de561" />


# sudo netplan apply

<img width="155" height="35" alt="Image" src="https://github.com/user-attachments/assets/ffafce09-f92a-4748-bba6-3e1e106ff31b" />

Då sparas din nätverks config med hjälp av denna kommandot 

# ls -ld /var/systementor/konsultdata /var/systementor/konsultdata/anteckningar.txt
Detta kommandot kan du se vilken som är mappen och vilken som är filen.

<img width="454" height="68" alt="Image" src="https://github.com/user-attachments/assets/b77bd7b6-1a7e-4cbb-ba9d-473943dd14f0" />


# Ip addr show

Visar ip address samt dns 



# Windows delen (Gammal)

# New-item -itemtype Directory -Path C:\Systementor\Konsultdata

Med detta kommandot so skapades en mapp genom CLI


<img width="906" height="280" alt="Image" src="https://github.com/user-attachments/assets/7bd29731-d7b9-461c-90df-947b287889fa" />

# (Get-Acl "C: \systementor\"). access | format-table identityReference, FilesystemRights, AccessControlType, IsInherited

Detta kommandot tilldelade rättigheter för mappen Konsultdata 


<img width="1001" height="238" alt="Image" src="https://github.com/user-attachments/assets/040b4a26-8a1e-492c-81d2-b765ec9fe002" />
# Ipconfig

Där kan man se vilken ip address du har osv


<img width="619" height="176" alt="Image" src="https://github.com/user-attachments/assets/523d1395-8d06-4532-a8ec-c5471d526380" />



# Commit logg
<img width="1345" height="722" alt="Image" src="https://github.com/user-attachments/assets/d2cf82fd-66eb-4e26-bfe5-4cf6f72f724b" />

# AI logg och utvärdering 

Prompten var följande Ge mig information om hur IPconfig /all fungerar och vilka scenarion är det viktigt att använda det https://chatgpt.com/uc/6abe2bc6-b770-83ea-b34a-0568a37f8585

Detta var svaret och det var korrekt då den beskriver i vilka scenario som Ipconfig /all kan användas i och visar exempel när det kan vara använtbart tex flushdns eller renew, samt visar vilka andra commandos som kan användas med hjälp av Ipconfig / dns tex och beskriver vad /all gör exakt men också ger ut information om vad exakt de dem gör och vad som kommer hända om den kommandos körs. Den informationen de gav, stammer väldig bra om man jämför med andra källor: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig https://www.teamviewer.com/en/insights/what-does-ipconfigall-do/
