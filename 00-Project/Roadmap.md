# Cybersecurity Home Lab — Roadmap

> [!info] Project Overview  
> Progettazione, implementazione e analisi di un'infrastruttura IT aziendale virtualizzata, con l'obiettivo di acquisire competenze pratiche in System Administration, Networking, Cybersecurity, Threat Detection e Incident Response.

**Stato:** In progress  
**Inizio:** Ottobre 2026  
**Host:** Windows 11  
**Hypervisor:** Oracle VirtualBox  
**Dominio:** `lab.test`  
**Rete di laboratorio:** `CYBER-LAB`

---

## Phase 0 — Virtual Infrastructure Setup

**Obiettivo:** creare un ambiente virtualizzato isolato e controllato.

- Installazione di Oracle VirtualBox
    
- Creazione della macchina virtuale DC01
    
- Installazione di Windows Server 2025
    
- Configurazione hostname `DC01`
    
- Creazione rete interna `CYBER-LAB`
    
- Verifica definitiva dell'IP statico `192.168.50.10`
    
- Creazione di uno snapshot della configurazione iniziale
    

**Competenze:** Virtualization, TCP/IP, Network Isolation, Windows Server Administration.

**Documentazione:** [[LAB 01 - Configurazione DC01]]

---

## Phase 1 — Active Directory Infrastructure

**Obiettivo:** costruire un'infrastruttura di dominio Microsoft con autenticazione centralizzata.

### Domain Controller & DNS

- Installazione del ruolo Active Directory Domain Services
    
- Avvio della procedura `Install-ADDSForest`
    
- Verifica della promozione di DC01 a Domain Controller
    
- Verifica del dominio `lab.test`
    
- Verifica del servizio DNS
    
- Analisi dei record DNS SRV
    
- Verifica dello stato del Domain Controller con `dcdiag`
    

### Identity & Access Management

- Creazione delle Organizational Units (OU)
    
- Creazione dei reparti IT, HR e Finance
    
- Creazione degli account utente
    
- Creazione dei gruppi di sicurezza
    
- Gestione dell'appartenenza ai gruppi
    
- Configurazione dei permessi sulle risorse condivise
    
- Applicazione del principio del minimo privilegio
    

### Group Policy

- Creazione delle Group Policy Objects (GPO)
    
- Configurazione password e account lockout policies
    
- Applicazione di policy specifiche alle OU
    
- Verifica delle policy con `gpresult`
    
- Analisi di policy applicate ed eventuali errori
    

**Competenze:** Active Directory, DNS, IAM, RBAC, Group Policy, Windows Server.

**Documentazione:** [[LAB 02 - Deploy Active Directory]]

---

## Phase 2 — Windows Client & Kerberos

**Obiettivo:** simulare il computer di un dipendente e comprendere i meccanismi di autenticazione del dominio.

### Domain Client

- Creazione VM `CLIENT01`
    
- Installazione Windows Client
    
- Configurazione rete e DNS
    
- Join del client al dominio `lab.test`
    
- Login con account di dominio
    
- Test delle autorizzazioni utente
    

### Kerberos Authentication

- Analisi del ruolo del Key Distribution Center (KDC)
    
- Osservazione dei Ticket Granting Ticket (TGT)
    
- Analisi dei Service Ticket
    
- Utilizzo di `klist`
    
- Cattura del traffico Kerberos con Wireshark
    
- Analisi degli eventi Windows 4768, 4769 e 4771
    
- Simulazione di errori di autenticazione
    

**Competenze:** Kerberos, Authentication, Windows Security, Network Protocol Analysis.

---

## Phase 3 — Security Monitoring & SIEM

**Obiettivo:** costruire un piccolo Security Operations Center (SOC) per monitorare l'infrastruttura.

### Wazuh Deployment

- Preparazione di una VM Linux
    
- Installazione di Wazuh
    
- Configurazione degli agent Windows
    
- Raccolta dei Windows Event Logs
    
- Analisi degli eventi di autenticazione
    
- Configurazione delle regole di rilevamento
    
- Creazione di dashboard per il monitoraggio
    

### Threat Detection

- Simulazione di accessi falliti
    
- Rilevamento di account lockout
    
- Analisi di processi e attività sospette
    
- Ricerca di Indicators of Compromise (IoC)
    
- Correlazione degli eventi di sicurezza
    
- Analisi e classificazione degli alert
    

**Competenze:** SIEM, Log Analysis, Threat Detection, Windows Event Logging, SOC Operations.

---

## Phase 4 — MITRE ATT&CK & Threat Investigation

**Obiettivo:** imparare a investigare attività sospette e riconoscere le tecniche degli attaccanti.

- Studio della struttura MITRE ATT&CK
    
- Analisi delle tattiche e delle tecniche
    
- Identificazione di eventi sospetti nei log
    
- Associazione degli eventi alle tecniche MITRE
    
- Analisi di un incidente simulato
    
- Costruzione di una timeline dell'incidente
    
- Produzione di un report tecnico
    

**Competenze:** Threat Analysis, MITRE ATT&CK, Incident Investigation, Security Reporting.

---

## Phase 5 — Web Application Security

**Obiettivo:** studiare le vulnerabilità delle applicazioni web e sperimentare tecniche di protezione.

### OWASP Top 10

- Installazione di OWASP Juice Shop
    
- Configurazione di Burp Suite
    
- Analisi delle richieste HTTP/HTTPS
    
- Esercitazioni sulle vulnerabilità di autenticazione
    
- Esercitazioni sulle injection
    
- Analisi dei controlli di accesso
    
- Documentazione delle vulnerabilità e delle mitigazioni
    

### Web Application Firewall

- Configurazione di Nginx
    
- Installazione di ModSecurity e OWASP CRS
    
- Analisi delle regole WAF
    
- Esecuzione di richieste di test
    
- Studio dei log delle richieste bloccate
    
- Analisi dei falsi positivi
    

**Competenze:** Web Security, OWASP Top 10, HTTP, Burp Suite, WAF.

---

## Phase 6 — Network Access Control

**Obiettivo:** sperimentare meccanismi di autenticazione e autorizzazione degli accessi alla rete.

- Studio dell'architettura NAC
    
- Configurazione di un laboratorio RADIUS
    
- Installazione di FreeRADIUS
    
- Simulazione di autenticazioni autorizzate
    
- Simulazione di accessi negati
    
- Analisi delle richieste RADIUS
    
- Valutazione delle policy di accesso
    

**Competenze:** NAC, RADIUS, Network Authentication, Access Control.

---

## Phase 7 — XDR & SOAR

**Obiettivo:** comprendere la correlazione degli eventi e l'automazione della risposta agli incidenti.

### XDR Concepts

- Raccolta di eventi da endpoint, identità e rete
    
- Correlazione di eventi appartenenti allo stesso incidente
    
- Ricostruzione della sequenza delle attività sospette
    
- Valutazione di strumenti e funzionalità XDR
    

### SOAR & Automation

- Studio dei workflow di incident response
    
- Configurazione di una piattaforma di automazione
    
- Creazione di un playbook
    
- Simulazione della gestione automatica di un alert
    
- Test di una risposta controllata
    
- Verifica e documentazione del workflow
    

**Competenze:** Security Automation, SOAR, XDR Concepts, Incident Response.

---

## Phase 8 — Final Security Assessment

**Obiettivo:** eseguire una valutazione tecnica dell'infrastruttura realizzata.

- Inventario dei sistemi e dei servizi
    
- Analisi delle configurazioni di sicurezza
    
- Valutazione di account e permessi
    
- Verifica delle policy aziendali
    
- Simulazione di incidenti in ambiente isolato
    
- Analisi degli alert prodotti
    
- Individuazione delle configurazioni migliorabili
    
- Applicazione delle misure correttive
    
- Redazione di un report finale
    

### Deliverables

- Documentazione tecnica completa
    
- Diagramma dell'architettura di rete
    
- Configurazioni e script riproducibili
    
- Evidenze e screenshot dei laboratori
    
- Report di analisi degli incidenti
    
- Repository GitHub documentato
    

---

## Current Progress

**Fase attuale:** Phase 1 — Active Directory Infrastructure

**Ultima attività:** avvio della promozione di DC01 a Domain Controller del dominio `lab.test`.

**Prossimi obiettivi:**

1. Verificare il corretto funzionamento del dominio.
    
2. Controllare DNS e i record SRV.
    
3. Creare Organizational Units, utenti e gruppi.
    
4. Applicare le prime Group Policy.
    
5. Preparare CLIENT01 per l'autenticazione Kerberos.
    

---

## Knowledge Base

- [[Active Directory]]
    
- [[DNS SRV]]
    
- [[Kerberos]]
    
- [[NTDS.dit]]
    
- [[SIEM]]
    

## Project Documentation

[[Progetto cyberlab]]

> [!note] Progress Tracking  
> Una checkbox viene contrassegnata come completata soltanto dopo aver eseguito l'attività e verificato il risultato. Ogni laboratorio deve contenere procedura, comandi, evidenze, eventuali errori e conclusioni.