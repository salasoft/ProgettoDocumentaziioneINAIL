# User Story - Id 9 - Compilazione Istanza Blueprint - Back In Compilazione


## Descrizione

- COME: utente con ruolo OPS o con ruolo ADMIN

- DEVO POTER: eseguire la funzionalità di compilazione delle configurazioni dei componenti definiti nel file dell'istanza di blueprint per uno specifico ambiente.
  1. Accedo alla funzionalità di Ricerca Istanza Blueprint [(US 4)](us_4_ricerca_istanza_blueprint.md) ed eseguo la funzionalità di ricerca per identificare l'evento di censimento asset oppure l'identificativo del prodotto/asset RTC di cui eseguire l'importazione del file dal repository Git.
  2. Il sistema esegue la funzionalità di ricerca in archivio [(US 4)](us_4_ricerca_istanza_blueprint.md)
  3. Il sistema visualizza l'elenco dei risultati della ricerca in funzione dei paramentri inseriti [(US 4)](us_4_ricerca_istanza_blueprint.md) [(UI 9.1)](#user-interface)
  4. Identifico l'item di interesse dai risultati della ricerca:<br />
    4.1 clicco su apposito pulsante *Dettaglio* per una istanza in stato *Archiviata*<br /> 
    4.2 il sistema visualizza la pagina come in figura [UI 9.2](#user-interface)
  5. Sulla pagina visualizzata, clicco il pulsante *In Compilazione*, visibile solo se lo stato dell'istanza di blueprint è in stato *Archiviata* o *Da Compilare*.
  6. Il sistema cambia lo stato dell'istanza inserendo una nuova occorrenza nella tabella STATO_ISTANZA_BLUEPRINT con stato *In Compilazione*<br />
     Il dettaglio delle informazioni che il sistema deve persistere è stato modellato sulla struttura prevista del template delle blueprint e descritto nella sezione [Data Model della US](#data-model)<br />
  7. Il sistema visualizza il messaggio: "Operazione eseguita correttamente!"<br />
 
- AL FINE DI: poter generare il file di istanza della blueprint comprensivo di tutti gli item di componenti ambiente configurati durante la compilazione.



## Riferimenti

Di seguito i riferimenti e/o collegamenti ad altre US citate in questa

### [User Story - Id 4 - Ricerca Istanza di Blueprint](user_stories/us_4_ricerca_istanza_blueprint.md)



## Criteri di accettazione

- DATO: una istanza di blueprint in stato *Archiviata*

- QUANDO: l'utente OPS o ADMIN dopo aver ultimato la compilazione delle informazioni per tutti gli ambienti previsti ed archiviato il file di una istanza di blueprint, ha esigenza di modificare nuovamente le informazioni della sezione *runtimeEnvironment* dei files di istanza di una blueprint.

- QUINDI: 
  - Il sistema deve permettere di modificare lo stato di lavorazione dell'istanza di blueprint tornando allo stato in *In Compilazione*
  - Al termine delle operazioni il sistema dovrà aver inserito una occorrenza nelle seguenti tabelle: STATO_ISTANZA_BLUEPRINT 

<br />

## Controlli e vincoli

Al momento sono previsti i seguenti controlli/vincoli:
- Il passaggio di stato a *Compilata* pùo essere eseguito solo per le istanze in stato *In Compilazione*


<br />                        
<br />

## Trigger

Esigenza di finalizzare la compilazione delle configurazioni dei componenti definiti nel file dell'istanza di blueprint generando il file di istanza della blueprint comprensivo di tutti gli item di componenti ambiente configurati durante la compilazione per poter successivamente essere archiviato sul sistema SCM Git [(US 8)](us_9_archiviazione_istanza_blueprint.md).

## Pre-Requisiti

L'utente ha eseguito l'accesso autenticandosi sul portale intranet

## Data Model

Di seguito è descritta la porzione di modello dati a cui fa riferimento la funzionalità illustrata nella user story. <br />
La lettura dei dati per la visualizzazione della tabella pivot e per la generazione del file viene eseguita accedendo in lettura alle tabelle ISTANZA_BLUEPRINT MODULO_BLUEPRINT, COMPONENTE_BLUEPRINT, AMBIENTE_COMPONENTE_BLUEPRINT <br />
Al termine delle operazioni il sistema dovrà aver aggioranto una occorrenza nelle seguenti tabelle: ISTANZA_BLUEPRINT <br />
Al termine delle operazioni il sistema dovrà aver inserito una occorrenza nelle seguenti tabelle: STATO_ISTANZA_BLUEPRINT <br />

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


- Tabella MODULO_BLUEPRINT

|    Attributo               |   Tipo    | Descrizione                                                                                 |
|  ----------------------    |  -------  | ------------------------------------------------------------------------------------------- | 
|   ID_MODULO                |    INT    | Identificativo autogenerato                                                                 |
|   ID_ISTANZA               |    INT    | Identificativo dell'occorrenza ISTANZA_BLUEPRINT a cui lo fa riferimento (chiave esterna ISTANZA_BLUEPRINT)   |
|   ID_MODULO_BP             |  VARCHAR  | Valore dell'attributo *idModulo* presente nella blueprint |
|   NOME_MODULO              |  VARCHAR  | Valore dell'attributo *nomeModulo* presente nella blueprint |
|   TIPO_MODULO              |  VARCHAR  | Valore dell'attributo *tipoModulo* presente nella blueprint |
|   DESCRIZIONER_MODULO      |  VARCHAR  | Valore dell'attributo *descrizioneModulo* presente nella blueprint |


<br />
<br />


- Tabella COMPONENTE_BLUEPRINT

|    Attributo               |   Tipo    | Descrizione                                                                                 |
|  ----------------------    |  -------  | ------------------------------------------------------------------------------------------- | 
|   ID_COMPONENTE            |    INT    | Identificativo autogenerato                                                                 |
|   ID_MODULO                |    INT    | Identificativo dell'occorrenza MODULO_BLUEPRINT a cui lo fa riferimento (chiave esterna MODULO_BLUEPRINT)   |
|   ID_COMPONENTE_BP         |  VARCHAR  | Valore dell'attributo *idComponente* presente nella blueprint |
|   NOME_COMPONENTE          |  VARCHAR  | Valore dell'attributo *nomeComponente* presente nella blueprint |
|   TIPO_COMPONENTE          |  VARCHAR  | Valore dell'attributo *tipoComponente* presente nella blueprint |
|   DESCRIZIONER_COMPONENTE  |  VARCHAR  | Valore dell'attributo *descrizioneComponente* presente nella blueprint |
|   TECNOLOGIA               |  VARCHAR  | Valore dell'attributo *tecnologia* presente nella blueprint |
|   DEPLOY_ENVIRONMENT       |  VARCHAR  | Valore dell'attributo *deployEnvironment* presente nella blueprint |
|   RUNTIME_ENVIRONMENT      |  VARCHAR  | Valore dell'attributo *runtimeEnvironment* presente nella blueprint |

<br />
<br />


- AMBIENTE_COMPONENTE_BLUEPRINT 

|    Attributo                |   Tipo    | Descrizione                                                                                 |
|  ----------------------     |  -------  | ------------------------------------------------------------------------------------------- | 
|   ID_AMBIENTE_COMPONENTE    |    INT    | Identificativo autogenerato                                                                 |
|   ID_COMPONENTE             |    INT    | Identificativo dell'occorrenza COMPONENTE_BLUEPRINT a cui lo fa riferimento (chiave esterna COMPONENTE_BLUEPRINT)   |
|   AMBIENTE                  |  VARCHAR  | Valore dell'ambiente per cui è destinato il frammento di configurazione del componente della blueprint (Integrazione | Collaudo | Certificazione | Esercizio) |
|   YAML_OPS_BLUEPRINT_TARGET |  VARCHAR  | Frammento YAML di configurazione del componente della blueprint |
|   DATA_CREAZIONE            | TIMESTAMP | Data di creazione dell'occorrenza in tabella                                                |
|   UTENTE_CREAZIONE          |  VARCHAR  | Utente applicativo che ha eseguito la creazione dell'occorrenza in tabella                  |
|   DATA_ULTIMA_MODIFICA      | TIMESTAMP | Data di ultimo aggiornamento dell'occorrenza in tabella                                     |         
|   UTENTE_ULTIMA_MODIFICA    |  VARCHAR  | Utente applicativo che ha eseguito l'ultimo aggiornamento dell'occorrenza in tabella        |

<br />
<br />


## Diagrammi

Di seguito il sequence diagram che illustra le azioni previste dalla User Story
<br />

![Sequence diagram della user story](../files/sequence_diagram_us_9.jpg)
<br />

[Download file visio del sequence diagram della user story ](../files/sequence_diagram_us_9.vsdx)

<br />
<br />

## User Interface Mockup

- UI 9.1

![User Interface](../images/ui_us_4_ricerca_istanza_blueprint.jpg)

<br />
<br />

- UI 9.2


![User Interface](../images/us_9_compilazione_istanza_blueprint_back.jpg)

## Interfaccia Applicativa con Correlazione Chiamate ai Metodi Corrispondenti

Di seguito è riportata l'interfaccia applicativa (screen) Compilazione Istanza Blueprint Back di PIM prodotta nella FASE1 con conseguente correlazione alla chiamata al metodo della specifica funzionalità evidenziata, al fine di agevolare lo sviluppo della FASE2 (in fase di definizione).

Per la "Compilazione Istanza Blueprint Back", oggetto della corrente US, è possibile tornare allo stato precedente "in compilazione" cliccando sul GREY BOX "In compilazione" solo se lo stato corrente si trova in "archiviata". Al click del GREY BOX "in compilazione" verrà richiamato il metodo PUT backToInCompilazione. 

![CambioStato](../images/In_esercizio_In_compilazione.png)

Il risultato garantisce il ritorno allo stato precedente con conseguente possibilità di ricompilazione, copia ambiente, riarchiviazione e generazione file YAML (vedi [User Story - Id 6 - Compilazione Istanza Blueprint](us_6_compilazione_istanza_blueprint.md)): 

![Compilazione](../images/Compilazione_5.png)

Nella tabella in basso, viene mostrato un riepilogo con relativa chiamata al metodo di tutti i buttons presentati in queste interfacce con relativo PATH: 

|Colore di riferimento|Pulsante Definito nell'Applicativo  |Tipologia Chiamata  |Nome chiamata | Path |Note|
|---------|---------|---------|---------|---------|---------|
|GREY|In Compilazione|PUT |back To In Compilazione |{{baseUrl}}/pim-api/blueprint/:id/backToInCompilazione |/|
|BLACK|In Esercizio |/ |/ |/ |vedi [User Story - Id 10 - Esercizio Istanza Blueprint](us_10_esercizio_istanza_blueprint.md)|
|GREY|Copia Ambiente|/ |/|/|vedi [User Story - Id 7 - Compilazione Istanza Blueprint - Generazione Versione - Ambiente](us_7_compilazione_istanza_blueprint_gen_versione.md)|
|ROSE|YAML|/ |/|/|vedi [User Story - Id 6 - Compilazione Istanza Blueprint](us_6_compilazione_istanza_blueprint.md)|
|PURPLE|Archiviazione|/|/|/|vedi [User Story - Id 8 - Archviazione Istanza Blueprint](us_8_archiviazione_istanza_blueprint.md)|


