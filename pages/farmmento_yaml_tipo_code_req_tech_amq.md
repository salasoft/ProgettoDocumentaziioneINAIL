### 9.10 Frammento YAML di configurazione componente - Tipologia: Code request - Tecnologia: AMQ

Al momento della stesura di questa documentazione sono state identificate una serie di informazioni di seguito descritte in tabella (Tabella 1). 
Tali informazioni sono corredate da una ipotesi di struttura del frammento yaml contenente i tag delle informazioni previste per la sezione di *runtime environment* 
afferente alla Tipologia: *Tipologia: Code request - Tecnologia: AMQ* prevista per i template delle blueprint architetturali.

La coda request è uno scenario in cui un messaggio inviato da un producer ha un solo consumer. Se più consumer sono connessi alla stessa coda i messaggi vengono distribuiti equamente tra ogni consumer.
Definisce un instradamento di tipo "anycast" per un adress affinche le sue code ricevano i messaggi in modo "point-to-point".

<br />

| Tag yaml    | Descrizione                                                                                                                                                   | Obbligatorio | Valori possibili                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| nomeCoda    | Il nome della coda è definito da   DEV.<br>     [nome coda] deve descrivere la funzione che dovrà svolgere                                                    | x            | nomeCoda = [nome prodotto].[nome modulo].que.[nome coda]                                                                                                                                                                                                                                                                                                                                                                                |
| nomeAddress | address deve coincidere con [nome coda]                                                                                                                       | x            |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| RoutingType | Anycast                                                                                                                                                       | x            |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| url broker  | Coppia IP:porta endpoint sul quale il broker espone il servizio. <br>Al momento in fase di deploy viene utilizzato l'IP è da valutare l'utilizzo del hostname | x            | CI=cofamq01.inail.it      tcp://10.1.60.172:61616<br>Collaudo= cofamqtest.inail.it    tcp://10.1.79.15:61616<br>Certificazione= <br>            Master : cefamq01.inail.it      tcp://10.1.97.69:61616<br>            Slave  : cesamq02.inail.it      tcp://10.1.97.70:61617<br>Produzione=<br>            Master : prfamq01.inail.it      tcp://10.1.31.38:61616<br>            Slave  : prsamq01.inail.it      tcp://10.1.31.40:61617 |
| username    | Username unica per il broker                                                                                                                                  | x            |                                                                                                                                                                                                                                                                                                                                                                                                                                         |

Di seguito un'ipotesi di struttura su file yaml dei tag attualmente identificati e candidati per la sezione di *runtime environment* dal template di blueprint.  

<br />


<pre>

    runtimeEnvironment:
            nomeCoda:
            nomeAdress:
            RoutingType: anycast
            urlBroker:
            secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste
                        


</pre>

<br />
<br />



Di seguito la struttura su file yaml per la sezione di *runtime environment* dal template di blueprint generata per tutti gli ambienti previsti. 
(ci = continuous integration alias integrazione, coll = collaudo, cert = certificazione, prod = produzione) 

<br />


<pre>
    runtimeEnvironment:
        ci:
            nomeCoda:
            nomeAdress:
            RoutingType: anycast
            urlBroker:
            secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste
        coll:
            nomeCoda:
            nomeAdress:
            RoutingType: anycast
            urlBroker:
            secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste
        cert:
            nomeCoda:
            nomeAdress:
            RoutingType: anycast
            urlBroker:
            secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste
        prod:
            nomeCoda:
            nomeAdress:
            RoutingType: anycast
            urlBroker:
            secret-key: #soluzione generica per la gestione delle credenziali, sono ancora da definire le soluzione dei secrets previste

</pre>

<br />
<br />
