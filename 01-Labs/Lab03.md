# LAB 03 — Enterprise Access Control

## 1. Obiettivo
![[Pasted image 20261016114730.png|686]]

Simulare la gestione degli accessi in un'azienda, implementando una struttura Active Directory con reparti, utenti, gruppi di sicurezza e autorizzazioni differenziate.

## 2. Scenario aziendale

- Dominio: `lab.test`
    
- Domain Controller: `DC01`
    
- Reparti: IT e HR
    
- Utenti: Mario Rossi, Luca Verdi e Giulia Bianchi
    

L'obiettivo finale **è consentire ai dipendenti di accedere esclusivamente alle risorse per cui possiedono le autorizzazioni necessarie.**

## 3. Implementazione

### 3.1 Organizational Units

Vengono create le OU:

- CyberLab
    
    - IT
        
    - HR
        
    - Groups
        
    - Workstations
        

**Scopo:** **organizzare gli oggetti Active Directory** e preparare l'applicazione di criteri e deleghe amministrative.

**Comando utilizzato:** `New-ADOrganizationalUnit`

`$base = "DC=lab,DC=test"

`New-ADOrganizationalUnit -Name "CyberLab" -Path $base`

`$root = "OU=CyberLab,$base"`
`New-ADOrganizationalUnit -Name "IT" -Path $root`
`New-ADOrganizationalUnit -Name "HR" -Path $root`
`New-ADOrganizationalUnit -Name "Groups" -Path $root`
`New-ADOrganizationalUnit -Name "Workstations" -Path $root`


### 3.2 Verifica

**Comando:** `Get-ADOrganizationalUnit`

**Risultato atteso:** presenza delle cinque OU previste.

**Risultato ottenuto:**![[Pasted image 20261016120427.png]]
### 3.3 Creazione dei gruppi di sicurezza

**Obiettivo:** gestire le autorizzazioni aziendali attraverso gruppi Active Directory.

**Ambiente:** DC01 — Active Directory Users and Computers.

Sono previsti due gruppi:

|Gruppo|Scope|Type|
|---|---|---|
|GG_IT|Global|Security|
|GG_HR|Global|Security|

I gruppi di sicurezza permettono di assegnare autorizzazioni alle risorse a insiemi di utenti.

l'OU `IT` stabilisce dove Mario è organizzato in Active Directory; il gruppo `GG_IT` determina quali autorizzazioni Mario può ottenere attraverso la sua appartenenza al gruppo.
![[Pasted image 20261022185645.png]]

**Procedura:** ADUC → CyberLab → Groups → New → Group.

**Risultato ottenuto:** ![[Pasted image 20261022181734.png|460]]![[Pasted image 20261022181931.png]]
I gruppi di sicurezza permettono di assegnare permessi a più utenti senza gestirli individualmente.
### 3.4 Creazione degli account utente

**Obiettivo:** creare identità aziendali associate ai diversi reparti.

|Account|Reparto|
|---|---|
|mario.rossi|IT|
|luca.verdi|IT|
|giulia.bianchi|HR|

**Procedura:** ADUC → OU del reparto → New → User.

Ogni account viene creato con una password temporanea, da cambiare al primo accesso.

**Risultato ottenuto:**![[Pasted image 20261022183857.png]]

### 3.5 Assegnazione ai gruppi

Gli account vengono associati ai gruppi di sicurezza:

- GG_IT → mario.rossi, luca.verdi
    
- GG_HR → giulia.bianchi
    

L'appartenenza ai gruppi sarà utilizzata nei prossimi esercizi per assegnare permessi alle risorse condivise.
****![[Pasted image 20261022183754.png]]+![[Pasted image 20261022183645.png]]
### 3.6 Verifica

**Comandi PowerShell:**

`Get-ADGroupMember -Identity "GG_IT"`

`Get-ADGroupMember -Identity "GG_HR"`

**Risultato atteso:** ciascun gruppo contiene esclusivamente gli utenti assegnati al reparto.

**Risultato ottenuto:** ![[Pasted image 20261022190334.png]]

![[Pasted image 20261022190604.png]]

### 3.7 Creazione delle risorse aziendali

**Ambiente:** Windows Server 2025 — DC01

**Obiettivo:** creare due directory destinate ai documenti dei reparti IT e HR, sulle quali applicare successivamente permessi differenziati.

**Directory:**

- `C:\LabShares\IT`
    
- `C:\LabShares\HR`
    

**Comandi PowerShell:**

```
New-Item -Path "C:\LabShares\IT" -ItemType Directory -Force
New-Item -Path "C:\LabShares\HR" -ItemType Directory -Force
```

Il comando `New-Item` crea nuovi elementi nel filesystem. Con il parametro `-ItemType Directory` viene specificata la creazione di una directory.

**Verifica:**

```
Get-ChildItem "C:\LabShares"
```

**Risultato atteso:** presenza delle cartelle IT e HR.

**Risultato ottenuto:**![[Pasted image 20261022191433.png]]

**Prossime operazioni:**

- Configurazione delle autorizzazioni NTFS.
    
- Creazione delle condivisioni SMB.
    
- Verifica degli accessi autorizzati e negati.
## 4. Conclusione
Creato correttamente l'elenco delle Organizational Units (OU) all'interno di Active Directory, nel dominio `lab.test`.
Le OU sono contenitori logici della directory, nei quali organizzerò gli oggetti dell'azienda virtuale.

![[Pasted image 20261016121904.png]]

![[Pasted image 20261016121919.png|465]]
## 5. Concetti collegati

- [[Active Directory]]
    
- [[Organizational Unit]]
    
- [[Security Group]]
    
- [[Access Control List]]
    
- [[Group Policy]]