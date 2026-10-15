# LAB 01 — Configurazione iniziale di DC01

## Obiettivo
![[Pasted image 20261014152523.png]]

Preparare Windows Server 2025 per la successiva installazione di Active Directory Domain Services (AD DS), iniziando dall'identificazione del server nella rete.

## Ambiente di laboratorio

|Componente|Configurazione|
|---|---|
|Host fisico|Windows 11|
|Hypervisor|Oracle VirtualBox|
|Macchina virtuale|DC01|
|Sistema operativo guest|Windows Server 2025 Evaluation|
|RAM|6 GB|
|vCPU|4|
|Disco virtuale|60 GB, VDI dinamico|
|Rete iniziale|NAT, temporanea|

## Concetti teorici

### Hostname

L'hostname è il nome assegnato a un dispositivo all'interno di un sistema informatico. Consente di identificarlo logicamente e può essere utilizzato dai servizi di rete e dai sistemi di risoluzione dei nomi.

### Domain Controller

Un Domain Controller (DC) è un server che esegue Active Directory Domain Services e gestisce le operazioni di autenticazione, autorizzazione e accesso alle risorse di un dominio Windows.

Il server diventerà un Domain Controller solo dopo l'installazione e la configurazione di AD DS.

## Procedura — Rinomina del server

1. Aprire Server Manager.
    
2. Selezionare `Local Server`.
    
3. Accedere alle proprietà `Computer name`.
    
4. Selezionare `Change`.
    
5. Impostare `DC01` come nome del computer.
    
6. Confermare e riavviare Windows Server.
    

### Verifica

Aprire PowerShell ed eseguire:

`hostname`

**Risultato atteso:** `DC01`

**Risultato ottenuto:** Da compilare dopo la verifica.

## Evidenze
![[Pasted image 20261014152205.png]]

![[Pasted image 20261014152135.png]]
## Problemi riscontrati

no errori

## Conclusione

Nome cambiato correttamente
## Concetti collegati

- [[Active Directory]]
    
- [[Domain Controller]]
    
- [[DNS]]
    
- [[Kerberos]]
## Configurazione della rete virtuale

### Obiettivo

Creare una rete interna isolata per consentire la comunicazione tra il Domain Controller DC01 e i futuri client del dominio, senza esporre direttamente i servizi di laboratorio alla rete fisica.

### Concetti teorici

**Rete interna VirtualBox:** modalità di networking virtuale che permette la comunicazione tra macchine virtuali collegate alla stessa rete interna. Non fornisce automaticamente connettività Internet o accesso all'host.

**Indirizzo IP statico:** indirizzo assegnato manualmente a un'interfaccia di rete, che rimane invariato finché non viene modificato. È particolarmente utile per server che devono essere raggiungibili in modo prevedibile.

**Subnet:** suddivisione logica di una rete IP. Nel nostro laboratorio utilizzeremo `192.168.50.0/24`, che comprende 256 indirizzi IPv4, di cui 254 normalmente utilizzabili dagli host.

### Configurazione prevista

|Parametro|Valore|
|---|---|
|Tipo di rete|Internal Network|
|Nome|CYBER-LAB|
|Sottorete|192.168.50.0/24|
|IP DC01|192.168.50.10 (da configurare)|
|Internet|Non disponibile tramite questa interfaccia|

### Procedura

1. Arrestare correttamente Windows Server.
    
2. Aprire le impostazioni della VM DC01 in VirtualBox.
    
3. Selezionare Rete → Scheda 1.
    
4. Impostare la modalità Rete interna.
    
5. Assegnare il nome `CYBER-LAB`.
    
6. Verificare che il cavo virtuale risulti connesso.
    
7. Salvare le impostazioni.
    

	### Evidenze

![[Pasted image 20261014152656.png]]
**Rete interna (CYBER-LAB):** è come uno switch virtuale isolato. Possono parlarsi solo le VM collegate a una rete interna con lo **stesso identico nome**.
Niente host, niente internet, niente LAN di casa.

### Verifica

**Stato:** da verificare al prossimo avvio della VM.

### Collegamenti

- [[Networking]]
    
- [[Indirizzo IP]]
    
- [[Subnet]]
    
- [[Active Directory]]
    
- [[DNS]]
## 5. Configurazione indirizzo IP statico

### 5.1 Obiettivo

Assegnare a DC01 un indirizzo IPv4 statico affinché il server sia raggiungibile in modo prevedibile dagli altri dispositivi della rete CYBER-LAB.

Con NAT, la VM può normalmente accedere a Internet passando attraverso la connessione del computer fisico.
![](data:image/svg+xml;charset=utf-8,%3Csvg%20font-family%3D%22-apple-system%2C%20BlinkMacSystemFont%2C%20%26quot%3BSegoe%20UI%26quot%3B%2C%20sans-serif%22%20font-weight%3D%22430%22%20data-d-component%3D%22svg%22%20fill%3D%22currentColor%22%20style%3D%22color%3Argb\(255%2C%20255%2C%20255\)%22%20viewBox%3D%220%200%20320%20174%22%20width%3D%22100%25%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Crect%20x%3D%22112%22%20y%3D%228%22%20width%3D%2296%22%20height%3D%2238%22%20rx%3D%227%22%20stroke%3D%22%2364748b%22%20fill%3D%22%2364748b%22%20fill-opacity%3D%22.09%22%2F%3E%3Ctext%20x%3D%22160%22%20y%3D%2224%22%20fill%3D%22currentColor%22%20text-anchor%3D%22middle%22%20font-size%3D%2211%22%20font-weight%3D%22600%22%3EInternet%3C%2Ftext%3E%3Ctext%20x%3D%22160%22%20y%3D%2237%22%20fill%3D%22currentColor%22%20text-anchor%3D%22middle%22%20font-size%3D%229%22%3ERete%20esterna%3C%2Ftext%3E%3Cpath%20d%3D%22M160%2046%20V68%22%20stroke%3D%22%230d9488%22%20stroke-width%3D%222%22%2F%3E%3Cpath%20d%3D%22M156%2062%20L160%2068%20L164%2062%22%20stroke%3D%22%230d9488%22%20stroke-width%3D%222%22%20fill%3D%22none%22%2F%3E%3Crect%20x%3D%2296%22%20y%3D%2269%22%20width%3D%22128%22%20height%3D%2237%22%20rx%3D%227%22%20stroke%3D%22%2364748b%22%20fill%3D%22%2364748b%22%20fill-opacity%3D%22.09%22%2F%3E%3Ctext%20x%3D%22160%22%20y%3D%2285%22%20fill%3D%22currentColor%22%20text-anchor%3D%22middle%22%20font-size%3D%2211%22%20font-weight%3D%22600%22%3EWindows%2011%3C%2Ftext%3E%3Ctext%20x%3D%22160%22%20y%3D%2299%22%20fill%3D%22currentColor%22%20text-anchor%3D%22middle%22%20font-size%3D%229%22%3EHost%20%2F%20VirtualBox%20NAT%3C%2Ftext%3E%3Cpath%20d%3D%22M160%20106%20V126%22%20stroke%3D%22%230d9488%22%20stroke-width%3D%222%22%2F%3E%3Cpath%20d%3D%22M156%20120%20L160%20126%20L164%20120%22%20stroke%3D%22%230d9488%22%20stroke-width%3D%222%22%20fill%3D%22none%22%2F%3E%3Crect%20x%3D%2296%22%20y%3D%22128%22%20width%3D%22128%22%20height%3D%2238%22%20rx%3D%227%22%20stroke%3D%22%230d9488%22%20fill%3D%22%230d9488%22%20fill-opacity%3D%22.09%22%2F%3E%3Ctext%20x%3D%22160%22%20y%3D%22144%22%20fill%3D%22currentColor%22%20text-anchor%3D%22middle%22%20font-size%3D%2211%22%20font-weight%3D%22600%22%3EDC01%3C%2Ftext%3E%3Ctext%20x%3D%22160%22%20y%3D%22157%22%20fill%3D%22currentColor%22%20text-anchor%3D%22middle%22%20font-size%3D%229%22%3EWindows%20Server%3C%2Ftext%3E%3C%2Fsvg%3E)



Le VM collegate a CYBER-LAB possono comunicare tra loro, ma non dispongono automaticamente di una connessione verso Internet o verso Windows 11.![[download.svg]]

### 5.2 Concetti teorici

**Indirizzo IP statico:** indirizzo di rete configurato manualmente, che non cambia automaticamente tramite DHCP.

**Subnet mask:** valore che distingue la parte di rete dalla parte host di un indirizzo IPv4. La maschera `255.255.255.0` equivale al prefisso `/24`.

**Default gateway:** dispositivo utilizzato per raggiungere reti esterne alla propria sottorete. Nel nostro laboratorio viene lasciato vuoto perché la rete interna deve rimanere isolata.

**DNS (Domain Name System):** sistema che permette di risolvere nomi di dominio in indirizzi IP e di individuare servizi di rete. Active Directory utilizza DNS anche per permettere ai client di trovare i Domain Controller.

### 5.3 Configurazione prevista

|Parametro|Valore|
|---|---|
|Hostname|DC01|
|IPv4|192.168.50.10|
|Subnet mask|255.255.255.0|
|Prefisso CIDR|/24|
|Gateway|Non configurato|
|DNS preferito|192.168.50.10|
|Rete VirtualBox|CYBER-LAB|

### 5.4 Procedura

1. Avviare DC01 e accedere come Administrator.
    
2. Aprire Server Manager → Local Server.
    
3. Accedere alle proprietà della scheda Ethernet.
    
4. Aprire le proprietà IPv4.
    
5. Configurare manualmente IP, subnet mask e DNS.
    
6. Salvare la configurazione.
    

### 5.5 Verifica

Comando PowerShell:
`ipconfig /all`

**Risultato atteso:** la scheda Ethernet presenta l'indirizzo IPv4 `192.168.50.10/24` e utilizza `192.168.50.10` come DNS preferito.

**Risultato ottenuto:**
![[Pasted image 20261014161754.png|401]]
![[Pasted image 20261014160608.png]]
Perché DNS uguale all'indirizzo del server? Perché successivamente DC01 ospiterà anche il servizio DNS necessario ad Active Directory. 
### 5.7 Collegamenti

- [[Indirizzo IP]]
    
- [[Subnet Mask]]
    
- [[DNS]]
    
- [[Domain Controller]]
    
- [[Active Directory]]
Abbiamo isolato la rete del laboratorio scegliendo Rete interna su VirtualBox, così le macchine virtuali possono comunicare tra loro, ma non direttamente con Internet o con il nostro computer principale, evitando che gli esperimenti di cybersecurity coinvolgano altri dispositivi.

# CYBERLAB — Fase 2: costruire un dominio Active Directory
![[Pasted image 20261014163158.png]]

# LAB 02 — Deploy Active Directory Domain Services

## 1. Obiettivo

Realizzare un'infrastruttura di autenticazione centralizzata basata su Active Directory Domain Services, creando una foresta e un dominio Windows denominato `lab.test`.

## 2. Architettura

| Componente        | Configurazione                |
| ----------------- | ----------------------------- |
| Server            | DC01                          |
| Sistema operativo | Windows Server 2025           |
| Indirizzo IPv4    | 192.168.50.10 (da verificare) |
| Dominio           | lab.test                      |
| Nome NetBIOS      | LAB                           |
| Rete virtuale     | CYBER-LAB                     |
| Servizi previsti  | AD DS, DNS, Kerberos          |

## 3. Concetti teorici

[[Active Directory]] 
### Domain Controller

Un [[Domain Controller]] è un server che ospita Active Directory Domain Services e gestisce, tra le altre cose, l'autenticazione degli utenti del dominio.

### Foresta e dominio

Una foresta Active Directory rappresenta il contenitore logico di livello superiore che comprende uno o più domini e condivide una struttura di directory comune.

Il dominio costituisce un ambito amministrativo e di autenticazione che organizza oggetti quali utenti, gruppi e computer.

### DNS e Active Directory

[[DNS]] consente ai client di individuare i Domain Controller e altri servizi tramite appositi record, inclusi i record SRV.

### Kerberos

[[Kerberos]] è il protocollo di autenticazione principale utilizzato negli ambienti Active Directory moderni. Si basa sull'emissione di ticket.

## 4. Procedura

### Installazione del ruolo AD DS

Comando:

`Install-WindowsFeature AD-Domain-Services -IncludeManagementTools`

**Risultato atteso:** installazione corretta del ruolo AD DS.
![[Pasted image 20261014164129.png]]

### Creazione della foresta

Comando:

`Install-ADDSForest -DomainName "lab.test" -DomainNetbiosName "LAB" -InstallDNS -SafeModeAdministratorPassword (Read-Host "DSRM Password" -AsSecureString) -Force`

**Risultato atteso:** creazione del dominio, installazione DNS e promozione di DC01 a Domain Controller.

**Risultato ottenuto:** da compilare.

## 5. Verifiche

Comandi:

- `Get-ADDomain`
    
- `Get-ADDomainController`
    
- `Resolve-DnsName -Name "_ldap._tcp.dc._msdcs.lab.test" -Type SRV`
    

Documentare gli output e indicare se ciascuna verifica è riuscita.

## 6. Evidenze

Inserire screenshot di:

- Installazione riuscita di AD DS
    ![[Pasted image 20261014190218.png]]
- Informazioni del dominio
    ![[Pasted image 20261014231511.png|363]]
- Informazioni sul Domain Controller
    ![[Pasted image 20261014231543.png|381]]
- Record [[DNS SRV]]![[Pasted image 20261014232146.png]]
    ![[Pasted image 20261014231634.png]]
    
    
differenza fra domain e domain controller
il dominio nel mio caso è lab.test , l'ambiente logico che raccoglie resources e identità
DC01(server) è il domain controller che 
**conserva copia della directory** e fornisce servizi necessari
	Se avessimo più Domain Controller, ciascuno conserverebbe una replica dei dati del dominio, che vengono sincronizzati attraverso la replicazione di Active Directory.
## 7. Problemi ed errori
### Errore durante la promozione a Domain Controller

**Errore:**
![[Pasted image 20261014165507.png]]

**Contesto:**
L'errore si è verificato durante l'esecuzione
del comando Install-ADDSForest.

**Analisi:**
Il parametro -Force è supportato dal cmdlet,
ma è facoltativo. Il motivo per cui PowerShell
non lo ha riconosciuto non è ancora accertato.

**Correzione tentata:**
Esecuzione del comando semplificato:

Install-ADDSForest -DomainName "lab.test" -DomainNetbiosName "LAB" -InstallDNS

**Risultato:** corretta installazione![[Pasted image 20261014165829.png]]
## 8. Conclusioni

Da compilare dopo aver completato e verificato il laboratorio.

## 9. Collegamenti

- [[Active Directory]]
    
- [[Domain Controller]]
    
- [[DNS]]
    
- [[Kerberos]]
    
- [[Hostname]]
    
- [[LAB 01 - Configurazione DC01]]