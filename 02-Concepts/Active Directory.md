Functions as both a **database** and a **directory service**. 
AD doesn’t just store data, but actively **manages** the **who, what, and where of network resources through authentication and authorization.**

directory service that stores lists and organizes info in a microsoft environment
provides an authentication and authorization system to network resources. it allows users to find and access certain resources
autenticazione -> user ha il PERMESSO di vedere la risorsa
AD OBJECTS: info stored in the AD
1. users
2. resources: hardwares
3. groups
![[Pasted image 20261014153806.png|323]]

![[Pasted image 20261014153850.png|386]]
GPOs: policies that restrics certain actions.

AD tree: domain and subdomains (child domains)
Forest: groups of AD trees![[Pasted image 20261014154041.png|526]]
trust relationships: grants permissions between domains


## In breve
Active Directory è il **servizio di directory** di Microsoft per ambienti Windows. Si basa su un database gerarchico e replicato ([[NTDS.dit]]) che memorizza gli oggetti del dominio (utenti, gruppi, computer, OU) con i loro attributi. Viene ospitato dai **domain controller** ed esposto tramite protocolli standard: **[[LDAP]]** per l’interrogazione, **[[Kerberos]]** (e NTLM per retrocompatibilità) per l’autenticazione e **[[DNS]]** per la localizzazione dei servizi. Fornisce **autenticazione centralizzata** (single sign-on nel dominio) e costituisce la base per l’**autorizzazione**: le risorse proteggono l’accesso tramite ACL che fanno riferimento ai SID di utenti e gruppi definiti in AD. Permette inoltre la gestione centralizzata delle configurazioni tramite **Group Policy**

Ha tre caratteristiche che lo distinguono da un normale database SQL:
- È **gerarchico**, organizzato ad albero (dominio → OU → oggetti), non a tabelle con righe e colonne.
- È **ottimizzato per le letture**: lo interroghi moltissimo e lo modifichi poco, quindi è velocissimo in ricerca.
- È **distribuito e replicato** su più server che si sincronizzano.