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


## 4. Concetti collegati

- [[Active Directory]]
    
- [[Organizational Unit]]
    
- [[Security Group]]
    
- [[Access Control List]]
    
- [[Group Policy]]