### 9.9 Frammento YAML di configurazione componente - Tipologia: Tipologia: DatiSQL - Tecnologia: Oracle

Al momento della stesura di questa documentazione sono state identificate una serie di informazioni di seguito descritte in tabella (Tabella 1). 
Tali informazioni sono corredate da una ipotesi di struttura del frammento yaml contenente i tag delle informazioni previste per la sezione di *runtime environment* 
afferente alla Tipologia: *Tipologia: UI Applicativa - Tecnologia: Oracle* prevista per i template delle blueprint architetturali.

<br />

| Tag yaml              | Descrizione                                                         | Obbligatorio | Valori Possibili     |
|-----------------------|---------------------------------------------------------------------|--------------|----------------------|
| nomeIstanzaDB         |  nome dell'istanza di installazione Orale                           |       X      |                      |
| ipIstanzaDB           |  IP dell'istanza di installazione Orale                             |       X      |                      |
| nomePDB               |  nome del pdb Oracle                                                |       X      |                      |
| nomeSchema            |  nome dello schema del database Oracle                              |       X      |                      |
| nomeUtenza            |  nome dell'utenza associata allo schema                             |       X      | default:nomeSchema   |
| tableSpace            |  nome del table space del database Oracle                           |       X      |                      |
| oracleScannabled      |  indica se abilitato l'iutilizzo di oracleScan                      |       X      |     true \| false    |
| oracleScan            |  stringa di connessione composta da 2 hostname e 2 servcename       |       X      |                      |
| hostName1             |  nome dell'host 1                                                   |       X      |                      |
| serviceName1          |  nome del service 1                                                 |       X      |                      |
| hostName2             |  nome dell'host 2                                                   |       X      |                      |
| serviceName2          |  nome del service 2                                                 |       X      |                      |
| portNumber            |  nomero della porta                                                 |       X      |                      |
| secret-key            |  chiave per una possibile gestione dei file seecret                 |       X      |                      |



<br />
<br />

Di seguito un'ipotesi di struttura su file yaml dei tag attaulmente identificati e candidati per la sezione di *runtime environment* dal template di blueprint.  

<br />


<pre>

              nomePDB: pimCI
              nomeSchema: gestinfra-sql
              tablespace: TS_gestinfra_sql
              hostname: 
              service_name: 
              porta: 1521
              oracleScan: true
                     hostname1: nomehost1
                     hostname2: nomehost2
                     service_name1: servizio1
                     service_name2: servizio2
                     porta: 1521
                     
</pre>

<br />
<br />


Di seguito la struttura su file yaml per la sezione di *runtime environment* dal template di blueprint generata per tutti gli ambienti previsti. 
(ci = continuous integration alias integrazione, coll = collaudo, cert = certificazione, prod = produzione) 

<br />


<pre>
       runtimeEnvironment: 
              ci:
                     nomeIstanzaDB:
                     ipIstanzaDB:
                     nomePDB:
                     nomeSchema:
                     nomeUtenza:
                     tableSpace:
                     oracleScanEnabled: true|false
                            oracleScan:
                            hostName1:
                            serviceName1:
                            hostName2:
                            serviceName2:
                            portNumber:
                     secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste
              coll:
                     nomeIstanzaDB:
                     ipIstanzaDB:
                     nomePDB:
                     nomeSchema:
                     nomeUtenza:
                     tableSpace:
                     oracleScanEnabled: true|false
                            oracleScan:
                            hostName1:
                            serviceName1:
                            hostName2:
                            serviceName2:
                            portNumber:
                     secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste
              cert:
                     nomeIstanzaDB:
                     ipIstanzaDB:
                     nomePDB:
                     nomeSchema:
                     nomeUtenza:
                     tableSpace:
                     oracleScanEnabled: true|false
                            oracleScan:
                            hostName1:
                            serviceName1:
                            hostName2:
                            serviceName2:
                            portNumber:
                     secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste
              prod:
                     nomeIstanzaDB:
                     ipIstanzaDB:
                     nomePDB:
                     nomeSchema:
                     nomeUtenza:
                     tableSpace:
                     oracleScanEnabled: true|false
                            oracleScan:
                            hostName1:
                            serviceName1:
                            hostName2:
                            serviceName2:
                            portNumber:
                     secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste

</pre>

<br />
<br />