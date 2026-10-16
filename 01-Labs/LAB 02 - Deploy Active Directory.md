# LAB 02 - Deploy Active Directory

## 1. Obiettivo e stato del laboratorio

Installare Active Directory Domain Services (AD DS) su Windows Server 2025 e promuovere **DC01** a primo Domain Controller di una nuova foresta, con dominio **`lab.test`** e DNS.

## 2. Ambiente documentato

| Componente | Valore riportato |
| --- | --- |
| Hypervisor | VirtualBox |
| VM / nome server previsto | DC01 |
| Sistema operativo | Windows Server 2025 |
| Indirizzo IP | `192.168.50.10` |
| Dominio | `lab.test` |
| Nome NetBIOS | `LAB` |
| Rete | `CYBER-LAB` |

Configurazione iniziale: [[LAB 01 - Configurazione DC01]].

Questi sono i valori riportati nella nota, non nuove misurazioni sulla VM. Prefisso di rete, gateway, DNS della scheda e modalità di rete VirtualBox non sono specificati qui: non vanno dedotti dal solo indirizzo IP o dal nome `CYBER-LAB`.

## 3. Procedura eseguita — comandi riportati nella nota

Questa sezione conserva la procedura documentata. Gli output di installazione e promozione non sono riportati; non è quindi una conferma indipendente del loro completamento. **Non rieseguire i comandi di installazione prima di controllare lo stato attuale.**

### 3.1 Installazione del ruolo AD DS

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

Installa il ruolo AD DS e gli strumenti di amministrazione. L'installazione del ruolo non promuove da sola il server a Domain Controller.

### 3.2 Creazione della foresta e promozione

```powershell
Install-ADDSForest -DomainName "lab.test" -DomainNetbiosName "LAB" -InstallDNS -SafeModeAdministratorPassword (Read-Host "DSRM Password" -AsSecureString) -Force
```

Il comando richiede la creazione di una nuova foresta con dominio radice `lab.test`, nome NetBIOS `LAB`, installazione DNS e promozione del server. La password DSRM serve per la modalità di ripristino dei servizi directory e non deve essere salvata nella nota.

Il riavvio è previsto al termine della promozione riuscita; il suo effettivo completamento non è documentato. `-Force` sopprime le richieste di conferma, ma non garantisce il successo. Il comando non imposta il nome del computer né il suo indirizzo IP.

## 4. Verifiche 
### Ruolo AD DS

```powershell
Get-WindowsFeature AD-Domain-Services
```


![[Pasted image 20261015163500.png]]
Eseguire su **DC01**, in **Windows PowerShell aperto come amministratore**, un passaggio alla volta. Dopo ogni comando, confrontare il risultato con quello atteso e annotare l'output reale. In caso di errore, fermarsi e riportarlo prima di procedere.

### 4.1 Verificare il dominio

```powershell
Get-ADDomain | Select-Object DNSRoot,NetBIOSName,DomainMode
```

**Risultato atteso:** `DNSRoot` = `lab.test` e `NetBIOSName` = `LAB`. Registrare il valore effettivo di `DomainMode`: il sistema operativo non basta, da solo, a documentare il livello funzionale configurato.

**Esito reale:**![[Pasted image 20261016112450.png]]

### 4.2 Verificare DC01

```powershell
Get-ADDomainController -Identity "DC01" | Select-Object HostName,IPv4Address,Site
```

**Risultato atteso:** `HostName` = `DC01.lab.test` (maiuscole/minuscole non rilevanti) e `IPv4Address` = `192.168.50.10`. Registrare il sito restituito senza presumerne il nome. L'identità esplicita seleziona DC01.

**Esito reale:**![[Pasted image 20261016112509.png|700]]

### 4.3 Verificare i record DNS per individuare il Domain Controller

```powershell
Resolve-DnsName "_ldap._tcp.dc._msdcs.lab.test" -Type SRV
```

**Risultato atteso:** un record SRV con destinazione `DC01.lab.test` e porta LDAP `389`. Eventuali altri record vanno registrati e valutati, non eliminati automaticamente.

Il comando usa il resolver configurato sulla VM: un risultato corretto verifica questa interrogazione DNS, non tutti i servizi DNS del dominio.

**Esito reale:** ![[Pasted image 20261016112528.png]]

### 4.4 Verificare la pubblicazione dei servizi del DC

```powershell
dcdiag /test:Advertising
```

**Risultato atteso:** test `Advertising` superato per DC01. Conservare anche eventuali avvisi o errori presenti nell'output.

Questo test verifica che il DC si annunci nei ruoli previsti; non costituisce una diagnostica completa di Active Directory.
                           
**Esito reale:**
![[Pasted image 20261016112744.png]]

## 5. Registro delle verifiche

Spuntare soltanto dopo aver raccolto e controllato l'evidenza reale.

- [x] Confermato `Installed` per il ruolo AD DS nello screenshot o con una nuova esecuzione del comando.
- [x] Confermati `lab.test` e `LAB`; registrato `DomainMode`.
- [x] Confermati nome e indirizzo IP di DC01; registrato il sito.
- [x] Verificato il record SRV LDAP del dominio.
- [x] Verificato il superamento del test `Advertising`.

Per ogni controllo, aggiungere data, output o screenshot ed eventuali anomalie nella relativa sezione. Non sostituire i risultati attesi con la dicitura “superato” senza evidenza.

## 6. Problemi riscontrati

Nella nota originale non sono descritti errori specifici. Questo non dimostra che non se ne siano verificati.

In caso di problemi, annotare:

- Comando eseguito e messaggio di errore completo.
- Causa accertata, distinguendola dalle ipotesi.
- Correzione applicata e risultato della verifica successiva.

## 7. Conclusione

**Laboratorio in attesa di validazione.** La procedura è riportata, ma le evidenze disponibili non permettono ancora di dichiarare verificato il funzionamento del dominio.

Completare la conclusione dopo i controlli della sezione 5, indicando quali verifiche sono riuscite e quali problemi restano aperti. Il superamento di questi controlli documenta le verifiche di base previste nel laboratorio, non una validazione completa dell'infrastruttura.

## 8. Concetti e collegamenti

- **AD DS:** servizio per la gestione centralizzata di utenti, computer, gruppi e autenticazione. Vedi [[Active Directory]].
- **Domain Controller:** server che ospita la directory e fornisce i servizi di dominio. Vedi [[Domain Controller]].
- **Foresta:** struttura logica che contiene uno o più domini Active Directory.
- **DNS:** consente di individuare host e servizi del dominio, anche tramite record SRV. Vedi [[DNS]].
- **Kerberos:** protocollo di autenticazione utilizzato in Active Directory. Vedi [[Kerberos]].
- Laboratorio precedente: [[LAB 01 - Configurazione DC01]].

### Riferimenti tecnici

- [Microsoft Learn — Install-ADDSForest](https://learn.microsoft.com/en-us/powershell/module/addsdeployment/install-addsforest?view=windowsserver2025-ps)
- [Microsoft Learn — dcdiag e test Advertising](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/dcdiag)
