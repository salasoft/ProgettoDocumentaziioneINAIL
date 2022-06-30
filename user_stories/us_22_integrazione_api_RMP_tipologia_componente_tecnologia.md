# User Story - Id 22 - Integrazione API dell'applicativo RMP per la condivisione delle informazioni di Tipologia Componente/Tecnologia previste

## Descrizione

- COME: processo automatizzato asincrono e schedulato rispetto al Front-End;

- DEVE POTER: eseguire la funzionalità di integrazione con le API disponibili dell'applicativo RMP (Release Management Platform);

1. il sistema avvia l'esecuzione di un processo asincrono e schedulato rispetto al front-end;
2. il processo richiama l'API esposta da RMP per recuperare l'elenco delle Tipologie Componente e relative Tecnologie nel formato esempio JSON riportato in basso:

<pre>{
    "status": 200,
    "payload": [
        {
            "id": 0,
            "nome": "Logica Applicativa BE",
            "descrizione": "Descrizione del componente Logica applicativa BE",
            "stato": "ATTIVO",
            "tecnologie": [
                "python",
                "dotnet",
                "nodejs",
                "springboot"
            ]
        },
        {
            "id": 1,
            "nome": "Dati SQL",
            "descrizione": "Descrizione del componente Dati SQL",
            "stato": "ATTIVO",
            "tecnologie": [
                "oracle",
                "sqlserver",
                "postgresql",
                "db2luw"
            ]
        },
        {
            "id": 2,
            "nome": "Logica applicativa FE",
            "descrizione": "Descrizione del componente Logica applicativa FE",
            "stato": "ATTIVO",
            "tecnologie": []
        }
    ],
    "message": "",
    "error": false
}</pre>

3. nel caso in cui perviene o pervengono delle nuove Tipologia Componente/Tecnologia da RMP:
    1. il sistema inserisce l'occorrenza "Identificativo Esterno" nella tabella: [TIPO_COMPONENTE - Identificativo Esterno] al fine di salvare l'identificativo (id) proveniente dall'API di RMP;
    
     *N.B: In fase di esecuzione, il processo dovrà identificare le occorrenze da inserire/aggiornare in base al valore dell' "Identificativo Esterno" della Tipologia Componente.*
    
    2. il sistema inserisce l'occorrenza "Da Definire" nella tabella: [TECNOLOGIA - Definizione Runtime];
    
    *N.B: L'attributo denominato "Definizione Runtime" potrà avere tre valori possibili: "Da Definire", "Definita", "Non Necessaria"*

    |STATO    |DESCRIZIONE  |
    |---------|---------|
    |Da Definire      | La struttura Runtime non è stata ancora definita                  |
    |Definita         | La struttura Runtime è stata definita  (VEDI [US. 20.1](us_20.1_gestione_sezione_runtime_environment_(funzionalità_CRUD_create).md))                         |
    |Non Necessaria   | La struttura Runtime non è necessaria per questa Tecnologia [valori impostabile dall'operatore] (VEDI US. [US. 23](us_23_ricerca_tipo_componente_tecnologia_stato.md))        |

    3. il sistema inserisce l'occorrenza di inizio validità (in formato data) della Tipologia Componente nella tabella: [TIPO_COMPONENTE - Data Inizio Validita];
    4. il sistema imposta l'occorrenza di fine validità della Tipologia Componente a NULL nella tabella: [TIPO_COMPONENTE - Data Fine Validita];
    5. il sistema inserisce l'occorrenza di inizio validità (in formato data) della Tecnologia nella tabella: [TECNOLOGIA - Data Inizio Validita];
    6. il sistema imposta l'occorrenza di fine validità della Tecnologia a NULL nella tabella: [TECNOLOGIA - Data Fine Validita];

    *N.B: in caso di qualsiasi modifica il processo non elimina mai le occorrenze dalle entità: TIPO_COMPONENTE/TECNOLOGIA, motivo per cui in fase di eliminazione/modifica cambio stato da "ATTIVO" a "NON ATTIVO" (stato ricevuto da RMP visibile nel JSON in alto) sarà valorizzata la "Data Fine Validità" con la data dell'operazione, sia per la Tipologia Componente e sia per la Tecnologia.*

4. nel caso in cui avviene un eliminazione/cambio stato sulla Tipologia Componente/Tecnologia da RMP:
    1. il sistema verifica il valore "Identificativo Esterno" presente nella tabella: [TIPO_COMPONENTE - Identificativo Esterno] al fine di individuare le Tipologie Componenti/Tecnologie già presenti a sistema;
    2. se lo STATO ricevuto da RMP per la Tipologia Componente passa a *Non Attivo*:
        1. il sistema imposta l'occorrenza di fine validità della Tipologia Componente con la data effettiva di fine validità nella tabella: [TIPO_COMPONENTE - Data Fine Validita];
        2. il sistema imposta l'occorrenza di fine validità delle Tecnologie associate a quella Tipologia Componente "Non Attiva" con la data effettiva di fine validità nella tabella: [TIPO_COMPONENTE - Data Fine Validita];
        3. il sistema nasconde la Tipologia Componente non attiva e reletive Tecnologie associate nell'applicativo PIM;
    3. se lo STATO ricevuto da RMP per la Tecnologia passa a *Non attivo*: 
        1. il sistema imposta l'occorrenza di fine validità della Tecnologia con una data effettiva di fine validità nella tabella: [TECNOLOGIA - Data Fine Validita];
        2. il sistema nasconde la Tecnologia non attiva nell'applicativo PIM;
    
    |STATO ricevuto da RMP    |DESCRIZIONE  |
    |---------|---------|
    |Attivo            | La Tipologia Componente/Tecnologia è Attiva (in uso) - Data Fine Validita impostata a NULL                |
    |Non Attivo        | La Tipologia Componente/Tecnologia è Non Attiva (non in uso) - Data Fine Validita impostata con una data effettiva          |

- AL FINE DI: poter condividere (inserire/aggiornare) le informazioni ricevute inserendo o modificando le occorrenze nella tabelle TIPO_COMPONENTE e TECNOLOGIA della base dati PIM;

## Riferimenti

Di seguito i riferimenti e/o collegamenti ad altre US citate in questa:

- [User Story - Id 20.1 - Gestione Sezione Runtime Environment (Funzionalità CRUD (CREATE)) - Anagrafica Sezioni Runtime](us_20.1_gestione_sezione_runtime_environment_(funzionalità_CRUD_create).md)

- [User Story - Id 23 - Ricerca Tipologie Componenti, Tecnologie, Stato e modifica Stato](us_23_ricerca_tipo_componente_tecnologia_stato.md) 

## Criteri di accettazione

- DATO: un processo automatico, asincrono e schedulato; 

- QUANDO: una Tipologia Componente/Tecnologia viene aggiunta/modificato di stato mediante API esposta da RMP (Release Management Platform);

- QUINDI: il processo deve permettere:
    - l'inserimento nell'applicativo PIM di una nuova Tipologia Componente/Tecnologia;
    - la modifica dello stato di una Tipologia Componente/Tecnologia già presente a sistema. 

## Controlli e vincoli

N/A

## Trigger

Processo automatizzato, asincrono e schedulato al fine di poter inserire e/o modificare lo stato di una Tipologia Componente/Tecnologia nell'applicativo PIM.

## Pre-Requisiti

L'utente ha eseguito l'accesso autenticandosi sul portale intranet.

## Data Model

Di seguito è descritta la porzione di modello dati (solo titolo tabelle utilizzate) a cui fa riferimento la funzionalità illustrata nella user story: <br />

- Tabella TECNOLOGIA

- Tabella TIPO_COMPONENTE

- Tabella TECNOLOGIA_TIPO_COMPONENTE

- Tabella ANAGRAFICA_STATO_DEFINIZIONE_RUNTIME

Consultare [Modello dati della soluzione Product Infrastructure Management - PIM - FASE 3](../pages/modello_dati_FASE3.md) per ulteriori approfondimenti sul modello dati predisposto per la FASE 3.


## Diagrammi

Di seguito il sequence diagram che illustra le azioni previste dalla User Story:

N/A


## User Interface Mockup

N/A
