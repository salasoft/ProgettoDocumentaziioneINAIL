# User Story - Id 10 - Esercizio Istanza Blueprint


## Descrizione

- COME: utente con ruolo OPS o con ruolo ADMIN

- DEVO POTER: eseguire la funzionalità di compilazione delle configurazioni dei componenti definiti nel file dell'istanza di blueprint per uno specifico ambiente.
  1. Accedo alla funzionalità di Ricerca Istanza Blueprint [(US 4)](us_4_ricerca_istanza_blueprint.md) ed eseguo la funzionalità di ricerca per identificare l'evento di censimento asset oppure l'identificativo del prodotto/asset RTC di cui eseguire il cambio stato. [(UI 10.1)](#user-interface)
  2. Il sistema esegue la funzionalità di ricerca in archivio [(US 4)](us_4_ricerca_istanza_blueprint.md)
  3. Il sistema visualizza l'elenco dei risultati della ricerca in funzione dei paramentri inseriti [(US 4)](us_4_ricerca_istanza_blueprint.md) [(UI 10.2)](#user-interface)
  4. Identifico l'item di interesse dai risultati della ricerca:<br />
    4.1 clicco su apposito pulsante Dettaglio per una istanza in stato *Archiviata*<br /> [(UI 10.3)](#user-interface)
    4.2 il sistema esegue la [US 5](us_5_visualizzazione_istanza_blueprint.md)<br />
  5. Sulla pagina visualizzata, clicco il pulsante *In Esercizio*, visibile solo se lo stato dell'istanza di blueprint è in stato *Archiviata*.
  6. Il sistema: cambia lo stato dell'istanza inserendo una nuova occorrenza nella tabella STATO_ISTANZA_BLUEPRINT con stato *In Esercizio*<br />
     Il dettaglio delle informazioni che il sistema deve persistere è stato modellato sulla struttura prevista del template delle blueprint e descritto nella sezione [Data Model della US](#data-model)<br />
  7. Il sistema visualizza il messaggio: "Operazione eseguita correttamente!"<br />
 
- AL FINE DI: poter cambiare lo stato dell'istanza della blueprint a seguito di un rilascio in esercizio del software del prodotto di riferimento.



## Riferimenti

Di seguito i riferimenti e/o collegamenti ad altre US citate in questa

### [User Story - Id 4 - Ricerca Istanza di Blueprint](user_stories/us_4_ricerca_istanza_blueprint.md)
### [User Story - Id 5 - Visualizzazione Istanza di Blueprint](user_stories/us_5_visualizzazione_istanza_blueprint.md)


## Criteri di accettazione

- DATO: un codice evento di censimento asset oppure ad un identificativo del prodotto/asset RTC

- QUANDO: l'utente OPS o ADMIN ha esigenza di segnalare un cambio di stato per l'istanza della blueprint a seguito di un rilascio in esercizio del software del prodotto di riferimento.

- QUINDI: 
  - Il sistema deve permettere di poter cambiare lo stato dell'istanza della blueprint.
  - Al termine delle operazioni il sistema dovrà aver inserito una occorrenza nelle seguenti tabelle: STATO_ISTANZA_BLUEPRINT <br />

<br />

## Controlli e vincoli

Al momento sono previsti i seguenti controlli/vincoli:
- Il passaggio di stato a *In Esercizio* pùo essere eseguito solo per le istanze in stato *Archiviata*


<br />                        
<br />

## Trigger

Esigenza di indicare che il software afferente ad una specifica istanza di blueprint è stata rilasciata in ambiente di esercizio.

## Pre-Requisiti

L'utente ha eseguito l'accesso autenticandosi sul portale intranet

## Data Model

Di seguito è descritta la porzione di modello dati a cui fa riferimento la funzionalità illustrata nella user story. <br />

<br />
<br />

- Tabella ISTANZA_BLUEPRINT

|    Attributo             |   Tipo    | Descrizione                                                                                 |
|  ----------------------  |  -------  | ------------------------------------------------------------------------------------------- | 
|   ID_ISTANZA             |    INT    | Identificativo autogenerato                                                                 |
|   ID_CENSIMENTO_ASSET    |  VARCHAR  | Identificativo del censimento del prodotto come assett su EA di RTC                         |
|   ID_PRODOTTO*            |  VARCHAR  | Valore dell'attributo *idProdotto* presente nella testata dell'istanza di blueprint imporata, fornita in input durante l'importazione |
|   TIPO_PRODOTTO*          |  VARCHAR  | Valore dell'attributo *tipoProdotto* presente nella testata dell'istanza di blueprint imporata, fornita in input durante l'importazione |
|   NOME_PRODOTTO*          |  VARCHAR  | Valore dell'attributo *nomeProdotto* presente nella testata dell'istanza di blueprint imporata, fornita in input durante l'importazione |
|   DESCRIZIONE_PRODOTTO*   |  VARCHAR  | Valore dell'attributo *descrizioneProdotto* presente nella testata dell'istanza di blueprint imporata, fornita in input durante l'importazione |
|   DATA_DENSIMENTO*        | TIMESTAMP | Valore dell'attributo *dataCensimento* presente nella testata dell'istanza di blueprint imporata, fornita in input durante l'importazione |
|   FILE_BLUEPRINT_ORIG    |   FILE    | File di istanza di bleuprint associato al censimento e recuperato da GitLab durante l'importazione    |
|   FILE_BLUEPRINT_TARGET  |   FILE    | File di istanza di bleuprint associato elaborato ed archiviato su GitLab con il passaggio di stato in *Archiviato*      |
|   URL_REPOSITORY_GIT     |  VARCHAR  | Valore del path/url del repository git dove presente il file archiviato, generata a partire da un base path url/*idProdotto* / configurazione-prodotto.git |
|   NOME_BRANCH_GIT        |  VARCHAR  | Valore del nome del branch del repository git dove presente il file archiviato. Requisito in fase di definizione, al momento valore fisso = master |
|   DATA_CREAZIONE         | TIMESTAMP | Data di creazione dell'occorrenza in tabella                                                |
|   UTENTE_CREAZIONE       |  VARCHAR  | Utente applicativo che ha eseguito la creazione dell'occorrenza in tabella                  |
|   DATA_ULTIMA_MODIFICA   | TIMESTAMP | Data di ultimo aggiornamento dell'occorrenza in tabella                                     |         
|   UTENTE_ULTIMA_MODIFICA |  VARCHAR  | Utente applicativo che ha eseguito l'ultimo aggiornamento dell'occorrenza in tabella        |


<br />
<br />

### Tabella STATO_ISTANZA_BLUEPRINT

|    Attributo               |   Tipo    | Descrizione                                                                                 |
|  ----------------------    |  -------  | ------------------------------------------------------------------------------------------- | 
|   ID_STATO_ISTANZA         |    INT    | Identificativo autogenerato                                                                 |
|   ID_ISTANZA               |    INT    | Identificativo dell'occorrenza ISTANZA_BLUEPRINT a cui lo stato fa riferimento (chiave esterna ISTANZA_BLUEPRINT)   |
|   ID_STATO                 |    INT    | Identificativo dell'occorrenza ANAGRAFICA_STATO a cui l'istanza fa riferimento (chaive esterna ANAGRAFICA_STATO) |
|   DATA_CAMBIO_STATO        | TIMESTAMP | Data dell'inserimento dell'occorrenza in tabella, al primo inserimento ed ad ognicambio di stato  | 
|   UTENTE_CAMBIO_STATO      |  VARCHAR  | Utente che ha eseguito l'inserimento dell'occorrenza in tabella, al primo inserimento ed ad ognicambio di stato  |

<br />
<br />


## Diagrammi

Di seguito il sequence diagram che illustra le azioni previste dalla User Story
<br />

![Sequence diagram della user story](../files/sequence_diagram_us_10.jpg)
<br />

[Download file visio del sequence diagram della user story ](../files/sequence_diagram_us_10.vsdx)

<br />
<br />

## User Interface Mockup

- UI 10.1

![User Interface](../images/ui_us_4_ricerca_istanza_blueprint.jpg)

<br />
<br />

- UI 10.2


![User Interface](../images/ui_us_4_ricerca_istanza_blueprint_risultati.jpg)

<br />
<br />

- UI 10.3


![User Interface](../images/ui_us_10_esercizio_istanza_blueprint.jpg)

<br />
<br />

## Interfaccia Applicativa con Correlazione Chiamate ai Metodi Corrispondenti

Di seguito è riportata l'interfaccia applicativa (screen) Esercizio Istanza Blueprint di PIM prodotta nella FASE1 con conseguente correlazione alla chiamata al metodo della specifica funzionalità evidenziata, al fine di agevolare lo sviluppo della FASE2 (in fase di definizione).

![CambioStato](../images/In_esercizio_In_compilazione.png)

Per l'"Esercizio Istanza Blueprint", oggetto della corrente US, è possibile passare dallo stato "archiviata" allo stato "in esercizio" cliccando sul BLACK BOX "In Esercizio" (solo se lo stato corrente si trova in "archiviata"). Al click del BLACK BOX "in esercizio" verrà richiamato il metodo PUT inEsercizio.

![CambioStato](../images/In_esercizio.png)

Il risultato garantisce il passaggio allo stato successivo "In Esercizio" con conseguente possibilità di poter procedere alla dismissione cliccando sul GREEN BOX "Dismissione" (vedi [User Story - Id 11 - Dismissione Istanza Blueprint](us_12_dismissione_istanza_blueprint.md)) o sul ROSE BOX "YAML" vedi [User Story - Id 6 - Compilazione Istanza Blueprint](us_6_compilazione_istanza_blueprint.md). 

Nella tabella in basso, viene mostrato un riepilogo con relativa chiamata al metodo di tutti i buttons presentati in queste interfacce con relativo PATH: 

|Colore di riferimento|Pulsante Definito nell'Applicativo  |Tipologia Chiamata  |Nome chiamata | Path |Note|
|---------|---------|---------|---------|---------|---------|
|GREY|In Compilazione |/ |/ |/ |vedi [User Story - Id 9 - Compilazione Istanza Blueprint - Back In Compilazione](us_9_compilazione_istanza_blueprint_back.md)|
|BLACK|In Esercizio|PUT |in Esercizio |{{baseUrl}}/pim-api/blueprint/:id/inEsercizio |/|
|GREEN|Dismissione |/ |/ |/ |vedi [User Story - Id 11 - Dismissione Istanza Blueprint](us_12_dismissione_istanza_blueprint.md)|
|ROSE|YAML |/ |/ |/ |vedi [User Story - Id 6 - Compilazione Istanza Blueprint](us_6_compilazione_istanza_blueprint.md)|
