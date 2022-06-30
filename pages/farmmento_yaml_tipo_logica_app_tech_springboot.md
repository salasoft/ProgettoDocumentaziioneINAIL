
### 9.6 Frammento YAML di configurazione componente - Tipologia: Logica Applicativa - Tecnologia: Spring-Boot

### 9.6.1 Informazioni di natura infrastrutturale candidate per il template della Blueprint Architettrurali 

Uno dei principali obiettivi previsti, anche parte delle specifiche funzionali dello sviluppo della soluzione in oggetto, è quello di identificare le 
informazioni relative alle specifiche di natura infrastrutturale che dovranno far parte del template della blueprint e caratterizzano uno specifico prodotto software.

Le informazioni candidate sono tutte quelle che risulteranno essere abilitanti all'automazione di un deploy sulla piattafomrma Red Hat Open Shift Container Platform.

Di seguito (Figura 6) è rappresentato ad alto livello lo scambio di informazioni di input ed output tra dev ed ops per il deploy sulla piattaforma Red Hat Open Shift Container Platform a partire da un ticket RTC (Rational Team Concert)

![Diagramma processo alto livello](images/disegno_AS_IS_Properties_Microservizio.jpg)

Figura 6

Di seguito (Figura 7) è rappresentato in dettaglio l'attuale processo di deploy eseguito sulla piattaforma Red Hat Open Shift Container Platform a partire da un ticket RTC (Rational Team Concert)

![Diagramma processo deploy di un microservizio sulla piattaforma Red Hat Open Shift Container Platform](images/diagramma_flusso_deploy_ocp.jpg)

L’analisi dell'attuale processo di deploy di un ticket RTC ha lo scopo di identificare i deploy enviroment per l’enrichment della bluprint di prodotto.
Le informazioni raccolte in questa fase saranno inserite nella sezione “deployEnvironment”.

Il processo di deploy del rilascio (baseline) è attualmente suddiviso in due fasi:

-	<ins>Deploy Properties</ins>:
	-	I file di properties utilizzati per il deploy del microservizio sono indicati nel campo note del ticket: “Rilasciata ConfigMap data xx/xx/xx”
	-	I file properties (BE_properties) sono allegati al ticket e possono essere:
    	-	appIication.yml
    	-	Secret.yml
    	-	Cacerts (opzionale)
    	-	Keystore.jks (opzionale)
	-	I file properties vengono rilasciati per i 3 ambienti: collaudo, certificazione e produzione

-	<ins>Deploy Componente</ins>:
	-	Creazione Microservizio
	-	Deploy e associazione di 3 configMap
	-	Creazione Route
	-	Scale up POD
	-	Verifica Health Check

<ins>Fase Deploy Properties</ins>:

	1.	Viene eseguito il download in locale dei file properties contenuti nell’area RAM del ticket RTC (<NomeApplicazione>-BE_properties) 
	2.	Attraverso la CLI di OpenShift (comando ‘oc’) sono eseguite le seguenti operazioni manuali:
		- Connessione all’ambiente di progetto del microservizio
		- Creazione di 2 configmap dai file properties (una per il file appIication.yml, e una unica per i file Secret.yml, Cacerts e Keystore.jks)
		- Upload dei 2 file configmap in OCP

<ins>Fase Deploy Componente</ins>:

	1.	Depoy del microservizio attraverso url dell’immagine nexus presente in RTC, per deploy image del microservizio è necessario inserire manualmente su GUI OCP
		-	Nome microservizio (da RTC) 
		-	Variabili d’ambiente (da scheda tecnica)
	2.	Deploy associazione di 3 configmap:
		-	Deploy associazione configmap relativa al file application.yml creata in fase di deploy properties (inserimento manuale del path di default nella GUI di OCP)
		-	Deploy configmap health check (paremetri inseriti manualmente presi da scheda tecnica: URL, delay e timeout)
		-	Deploy associazione configmap per secret relativa ai file Secret.yml, Cacerts e Keystore.jks creata in fase di deploy properties (inserimento manuale del path presente sulla scheda tecnica)
	3.	Create route del mocroservizio
	4.	SCALE UP POD (creazione POD – run microservizio)
	5.	Verifica healt check del microservizio (respons json: readness, liveness)



### 9.6.2 Informazioni di natura infrastrutturale candidate per il template della Blueprint Architettrurali 


Al momento della stesura di questa documentazione sono state identificate una serie di informazioni di seguito descritte in tabella (Tabella 1). 
Tali informazioni sono corredate da una ipotesi di struttura del frammento yaml contenente i tag delle informazioni previste per la sezione di *runtime environment* 
afferente alla Tipologia: *Logica Applicativa - Tecnologia: Spring-Boot* prevista per i template delle blueprint architetturali.

<br />

| Tag yaml              |Descrizione                                                                                                     | Obbligatorio | Valori Possibili     |
|-----------------------|----------------------------------------------------------------------------------------------------------------|--------------|----------------------|
| istanzaOpenShift      | nome/IP del nodo su cui è presente l'installazione di Open Shift a cui fare riferimento microservizio          |       X      |                      |
| nomeProgettoOpenShift | nome del progetto Open Shift che ospita il microservizio                                                       |       X      |                      |
| nomeDeploymentConfig  | nome del file deploymentConfig di OCP                                                                          |       X      |                      |
| imageName             | url Nexus dell'immagine Docker da scaricare per il deploy                                                      |       X      |                      |
| podScale              | informazioni di scaling del POD                                                                                |       X      | (default:1; max:2)   |
| configMapPod          | elenco config maps associate al POD, per convenzione previsti solo 2 item                                      |              |                      |
| configMap             | tipicamente la config-map fornita da dev come item di properties del ticket RTC,  l'applicazione dovrà <br/> generare un file di config-map per OCP a partire dal file  recuperato dal ticket RTC, archiviarlo sul repository git e salvare il link. (Fase 2)  |              |                      |
| source                | link al file di config-map, generato a partire dai files di properties caricati su ticket RTC                  |              |                      |
| mounthPath            | path di mount del file delle config map (informazione attualmente indicata nella scheda tecnica)               |              |                      |
| configMapSecrets      | tipicamente la config-map dei secrets ,fornita da dev come item di properties del ticket RTC.  <br/> l'applicazione dovrà generare un file di secrets per OCP a partire dal file  recuperato dal ticket RTC, archiviarlo sul repository git e salvare il link. (Fase 2) |              |                      |
| source                | link al file di secrets, generato a partire dai files di properties caricati su ticket RTC                     |              |                      |
| mounthPath            | path di mount del file del file di secrets (informazione attualmente indicata nella scheda tecnica)            |              |                      |
| routeEnalbed          | Necessità dell'oggetto route                                                                                   |       X      |     true \| false    |
| route                 | Nome dell'oggetto Route del POD univoco per la rotta                                                           |       X      |                      |
| hostName              | nome publico dell'hostname per la rotta, se non specificato sarà autogenerato da OCP                           |       X      |                      |
| path                  | path monitorato per l'instradamento del traffico verso il servizio                                             |       X      |                      |
| service               | nome del servizio verso cui instradare                                                                         |       X      |                      |
| targetPortProtocol    | protocollo per la porta target per il traffico dati (da verificare)                                            |       X      |                      |
| targetPort            | porta target per il traffico dati (default=8080)                                                               |       X      |                      |
| healtChecks           | informazioni per il monitoring dello stato dei POD (informazione attualmente indicata nella scheda tecnica)    |       X      |                      |
| readynessProbeEnabled | abilitazione tipologia di healtCheck                                                                           |       X      |     true \| false    |
| protocolType          | tipo di protocollo della chiamata healtCheck                                                                   |       X      | httpGet \| tcpSocket |
| useHttps              | indica se previsto protocollo https, valido solo per type:httpGet                                              |       X      |     true \| false    |
| path                  | path della URL per la request di healtCheck del microservizio (es: /health/ready)                              |       X      |       default: /     |
| port                  | numero di porta della URL per la request di healtCheck del microservizio                                       |       X      |                      |
| initialDelay          | durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check           |       X      |                      |
| timeOut               | durata in secondi del tempo di attesa per la chiamate di probe                                                 |       X      |                      |
| livenessProbeEnabled  | abilitazione tipologia di healtCheck                                                                           |       X      |     true \| false    |
| protocolType          | tipo di protocollo della chiamata healtCheck                                                                   |       X      | httpGet \| tcpSocket |
| useHttps              | indica se previsto protocollo https, valido solo per type:httpGet                                              |       X      |     true \| false    |
| path                  | path della URL per la request di healtCheck del microservizio (es: /health/live)                               |       X      |                      |
| port                  | numero di porta della URL per la request di healtCheck del microservizio                                       |       X      |                      |
| initialDelay          | durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check           |       X      |                      |
| timeOut               | durata in secondi del tempo di attesa per la chiamate di probe                                                 |       X      |                      |

<br />
<br />

Di seguito un'ipotesi di struttura su file yaml dei tag attaulmente identificati e candidati per la sezione di *runtime environment* dal template di blueprint.  
Per alcuni degli attributi sono stati intodottii i valori possibili ove previsto (es. true | false) e per alcuni altri attributi sono stati riportati dei valori di esempio.

<br />


<pre>

        nomeProgettoOpenShift: pim
        nomeDeploymentConfig: gestinfra-app
        configMapPod: 
            configMap: 
                urlGit: https://gitlab-os-lab.inail.it/../	
                source: pim-gestinfra-app-config
                mounthPath: /deployments/config
            secretConfigMap: 
                urlGit: https://gitlab-os-lab.inail.it/../
                source: pim-gestinfra-app-secret
                mounthPath: /deployments/config
        envVarPod:
        routing: true
            route: gestinfra-app
            hostName: gestinfra-app-pim.os-lab.inail.it
            path: /
            service: gestinfra-app
            targetPortProtocol: 8080
            targetPort: 8080
        healtChecks:
            readynessProbe:
                protocolType: httpGet
                useHttps: true
                path: /health/probe
                port: 8080
                initialDelay: 1
                timeOut: 10
            livenessProbe:
                protocolType: httpGet
                useHttps: true
                path: /health/live
                port: 8080
                initialDelay: 1
                timeOut: 5


</pre>

<br />
<br />

Di seguito la struttura su file yaml per la sezione di *runtime environment* dal template di blueprint generata per tutti gli ambienti previsti. 
(ci = continuous integration alias integrazione, coll = collaudo, cert = certificazione, prod = produzione) 

<br />


<pre>

       runtimeEnvironment:      
          ci:
              nomeProgettoOpenShift: #nome del progetto Open Shift che ospita il microservizio
                            nomePod: #nome del POD del progetto di Open Shift che ospita il microservizio
                          imageName: #url Nexus dell'immagine Docker da scaricare per il deploy
                           podScale: #informazioni di scaling del POD
                                 min: 1
                                 max: N
                                size: small | medium | large # small (1 cpu, RAM 2GB), medium (2 cpu, RAM 4GB), large (4 cpu, RAM 8GB) tipologie sizing per JDK (spring-boot)
                       configMapPod: #elenco config maps associate al POD, tipicamente al minimo 2 item
                          - configMap:
                               source: #link al file di config-map, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map (informazione attualmente indicata nella scheda tecnica)   
                          - configMap:
                               source: #link al file di secrets, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map, informazione indicata nella scheda tecnica  
                          envVarPod: #elenco variabili d'ambiente del POD non definite in config-map (informazione attualmente indicata nella scheda tecnica)   
                               - nome: #nome della variabile d'ambiente
                               valore: #valore della variabile d'ambiente
                               
                       serviceRoute: #informazioni di Route del POD 
                                 name: #nome univoco per la rotta
                             hostName: #nome publico dell'hostname per la rotta, se non specificato sarà autogenerato da OCP
                                 path: #path monitorato per l'instradamento del traffico verso il servizio
                              service: #nome del servizio verso cui instradare
                   targetPortProtocol: #protocollo per la porta target per il traffico dati (da verificare)
                           targetPort: #porta target per il traffico dati (8080)
                           
                        healtChecks: #informazioni per il monitoring dello stato dei POD (informazione attualmente indicata nella scheda tecnica)
                       readynessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false
                                   path: #/health/live
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallita
                        livenessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false #(valido solo per type:httpGet)
                                   path: #/health/live (valido solo per type:httpGet)
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallita
          coll:
              nomeProgettoOpenShift: #nome del progetto Open Shift che ospita il microservizio
                            nomePod: #nome del POD del progetto di Open Shift che ospita il microservizio
                          imageName: #url Nexus dell'immagine Docker da scaricare per il deploy
                           podScale: #informazioni di scaling del POD
                                 min: 1
                                 max: N
                                size: small | medium | large # small (1 cpu, RAM 2GB), medium (2 cpu, RAM 4GB), large (4 cpu, RAM 8GB) tipologie sizing per JDK (spring-boot)
                       configMapPod: #elenco config maps associate al POD, tipicamente al minimo 2 item
                          - configMap:
                               source: #link al file di config-map, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map (informazione attualmente indicata nella scheda tecnica)   
                          - configMap:
                               source: #link al file di secrets, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map, informazione indicata nella scheda tecnica  
                          envVarPod: #elenco variabili d'ambiente del POD non definite in config-map (informazione attualmente indicata nella scheda tecnica)   
                               - nome: #nome della variabile d'ambiente
                               valore: #valore della variabile d'ambiente
                               
                       serviceRoute: #informazioni di Route del POD 
                                 name: #nome univoco per la rotta
                             hostName: #nome publico dell'hostname per la rotta, se non specificato sarà autogenerato da OCP
                                 path: #path monitorato per l'instradamento del traffico verso il servizio
                              service: #nome del servizio verso cui instradare
                   targetPortProtocol: #protocollo per la porta target per il traffico dati (da verificare)
                           targetPort: #porta target per il traffico dati (8080)
                           
                        healtChecks: #informazioni per il monitoring dello stato dei POD (informazione attualmente indicata nella scheda tecnica)
                       readynessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false
                                   path: #/health/live
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallita
                        livenessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false #(valido solo per type:httpGet)
                                   path: #/health/live (valido solo per type:httpGet)
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallit
          cert:
              nomeProgettoOpenShift: #nome del progetto Open Shift che ospita il microservizio
                            nomePod: #nome del POD del progetto di Open Shift che ospita il microservizio
                          imageName: #url Nexus dell'immagine Docker da scaricare per il deploy
                           podScale: #informazioni di scaling del POD
                                 min: 1
                                 max: N
                                size: small | medium | large # small (1 cpu, RAM 2GB), medium (2 cpu, RAM 4GB), large (4 cpu, RAM 8GB) tipologie sizing per JDK (spring-boot)
                       configMapPod: #elenco config maps associate al POD, tipicamente al minimo 2 item
                          - configMap:
                               source: #link al file di config-map, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map (informazione attualmente indicata nella scheda tecnica)   
                          - configMap:
                               source: #link al file di secrets, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map, informazione indicata nella scheda tecnica  
                          envVarPod: #elenco variabili d'ambiente del POD non definite in config-map (informazione attualmente indicata nella scheda tecnica)   
                               - nome: #nome della variabile d'ambiente
                               valore: #valore della variabile d'ambiente
                               
                       serviceRoute: #informazioni di Route del POD 
                                 name: #nome univoco per la rotta
                             hostName: #nome publico dell'hostname per la rotta, se non specificato sarà autogenerato da OCP
                                 path: #path monitorato per l'instradamento del traffico verso il servizio
                              service: #nome del servizio verso cui instradare
                   targetPortProtocol: #protocollo per la porta target per il traffico dati (da verificare)
                           targetPort: #porta target per il traffico dati (8080)
                           
                        healtChecks: #informazioni per il monitoring dello stato dei POD (informazione attualmente indicata nella scheda tecnica)
                       readynessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false
                                   path: #/health/live
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallita
                        livenessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false #(valido solo per type:httpGet)
                                   path: #/health/live (valido solo per type:httpGet)
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallita
          prod:
              nomeProgettoOpenShift: #nome del progetto Open Shift che ospita il microservizio
                            nomePod: #nome del POD del progetto di Open Shift che ospita il microservizio
                          imageName: #url Nexus dell'immagine Docker da scaricare per il deploy
                           podScale: #informazioni di scaling del POD
                                 min: 1
                                 max: N
                                size: small | medium | large # small (1 cpu, RAM 2GB), medium (2 cpu, RAM 4GB), large (4 cpu, RAM 8GB) tipologie sizing per JDK (spring-boot)
                       configMapPod: #elenco config maps associate al POD, tipicamente al minimo 2 item
                          - configMap:
                               source: #link al file di config-map, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map (informazione attualmente indicata nella scheda tecnica)   
                          - configMap:
                               source: #link al file di secrets, generato a partire dai files di properties caricati su ticket RTC   
                           mounthPath: #path di mount del file delle config map, informazione indicata nella scheda tecnica  
                          envVarPod: #elenco variabili d'ambiente del POD non definite in config-map (informazione attualmente indicata nella scheda tecnica)   
                               - nome: #nome della variabile d'ambiente
                               valore: #valore della variabile d'ambiente
                               
                       serviceRoute: #informazioni di Route del POD 
                                 name: #nome univoco per la rotta
                             hostName: #nome publico dell'hostname per la rotta, se non specificato sarà autogenerato da OCP
                                 path: #path monitorato per l'instradamento del traffico verso il servizio
                              service: #nome del servizio verso cui instradare
                   targetPortProtocol: #protocollo per la porta target per il traffico dati (da verificare)
                           targetPort: #porta target per il traffico dati (8080)
                           
                        healtChecks: #informazioni per il monitoring dello stato dei POD (informazione attualmente indicata nella scheda tecnica)
                       readynessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false
                                   path: #/health/live
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallita
                        livenessProbe: #
                                   type: httpGet | tcpSocket # (verificare i valori possibili)
                               useHttps: true | false #(valido solo per type:httpGet)
                                   path: #/health/live (valido solo per type:httpGet)
                                   port: #default 8080
                           initialDelay: #durata in secondi del tempo di attesa per l'avvio del container per l'inizio delle chiamate di check
                                timeOut: #durata in secondi del tempo di attesa per la chiamate di probe, se il tempo di attesa viene superato la probe si considera fallita

</pre>