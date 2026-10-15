Il nome sta per **NT Directory Services . Directory Information Tree**. È il **file fisico** in cui AD salva tutto il suo database. Si trova sul domain controller, di default in `C:\Windows\NTDS\ntds.dit`.

Punti chiave:

- **Formato:** è un database **ESE** (Extensible Storage Engine, detto anche Jet Blue), lo stesso motore usato storicamente da Exchange. Quindi è un vero DB transazionale, con i suoi file di log (`edb.log`) e checkpoint per garantire consistenza.
- **Cosa contiene:** ogni oggetto del dominio con tutti i suoi attributi. Compresi, ed è qui che diventa interessante per la security, gli **hash delle password** di tutti gli utenti del dominio.
NTDS è il **database vivo di un servizio** replicato tra server
## attacchi di estrazione NTDS.dit
https://netwrix.com/it/cybersecurity-glossary/cyber-security-attacks/ntds-dit-attack/

**DCSync** è una tecnica d’attacco in cui ti **fingi un domain controller** per farti consegnare gli hash delle password dal DC vero.