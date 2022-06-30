
### 9.6. Informazioni di natura infrastrutturale candidate per il template della Blueprint Architettrurali

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
