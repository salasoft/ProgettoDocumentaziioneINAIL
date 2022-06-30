# User Story - Id 8 - Archviazione Istanza Blueprint


## Descrizione

- COME: utente con ruolo OPS o con ruolo ADMIN

- DEVO POTER: eseguire la funzionalità di compilazione delle configurazioni dei componenti definiti nel file dell'istanza di blueprint per uno specifico ambiente.
  1. Accedo alla funzionalità di Ricerca Istanza Blueprint [(US 4)](us_4_ricerca_istanza_blueprint.md) ed eseguo la funzionalità di ricerca per identificare l'evento di censimento asset oppure l'identificativo del prodotto/asset RTC di cui eseguire l'archiviazione. [(UI 8.1)](#user-interface)
  2. Il sistema esegue la funzionalità di ricerca in archivio [(US 4)](us_4_ricerca_istanza_blueprint.md)
  3. Il sistema visualizza l'elenco dei risultati della ricerca in funzione dei paramentri inseriti [(US 4)](us_4_ricerca_istanza_blueprint.md) [(UI 8.2)](#user-interface)
  4. Identifico l'item di interesse dai risultati della ricerca:<br />
    4.1 clicco su apposito pulsante Dettaglio per una istanza in stato *In Compilazione*<br /> [(UI 8.3)](#user-interface)
    4.2 il sistema esegue la [US 6](us_6_compilazione_istanza_blueprint.md)<br />
  5. Sulla pagina visualizzata, clicco il pulsante *Archiviazione*, visibile solo se lo stato dell'istanza di blueprint è in stato *In Compilazione*.
  6. Il sistema: <br />
    6.1. Recupera le informazioni dei frammenti YAML (YAML_OPS_BLUEPRINT_TARGET) dalle occorrenze di AMBIENTE_COMPONENTE_BLUEPRINT associate alla istanza di blueprint<br />
    6.2. Recupera il file originale (FILE_BLUEPRINT_ORIG) associato all'occorrenza dell'istanza di blueprint presente in tabella ISTANZA_BLUEPRINT<br />
    6.3. Genera il nuovo file di blueprint introducendo in una copia del file originale tutti i frammenti YAML delle sezioni *runtimeEnvironment* dei componenti presenti in tabella AMBIENTE_COMPONENTE_BLUEPRINT.<br />
    6.4. Salva il nuovo file generato (FILE_BLUEPRINT_TARGET) in tabella ISTANZA_BLUEPRINT<br />
    6.5. Esegue l'operazione di *git clone* del repository (URL_REPOSITORY_GIT)<br />
    6.6. Esegue l'operazione di *git check-out* del branch (NOME_BRANCH_GIT) indicati in tabella ISTANZA_BLUEPRINT<br />
    6.7. Esegue l'operazione di *git commit* e *git push* del file compilato (FILE_BLUEPRINT_TARGET) sul repository Git.<br />
    6.8. Cambia lo stato dell'istanza inserendo una nuova occorrenza nella tabella STATO_ISTANZA_BLUEPRINT con stato *Archviata*<br />
        Il dettaglio delle informazioni che il sistema deve persistere è stato modellato sulla struttura prevista del template delle blueprint e descritto nella sezione [Data Model della US](#data-model)<br />
  7.  Il sistema visualizza il messaggio: "Operazione eseguita correttamente!"<br />
 
- AL FINE DI: archiviare il file associato all'occoorrenza dell'istanza di blueprint compilata (FILE_BLUEPRINT_TARGET) sul sistema SCM.



## Riferimenti

Di seguito i riferimenti e/o collegamenti ad altre US citate in questa

### [User Story - Id 4 - Ricerca Istanza di Blueprint](user_stories/us_4_ricerca_istanza_blueprint.md)
### [User Story - Id 5 - Visualizzazione Istanza di Blueprint](user_stories/us_5_visualizzazione_istanza_blueprint.md)


## Criteri di accettazione

- DATO: un codice evento di censimento asset oppure ad un identificativo del prodotto/asset RTC

- QUANDO: l'utente OPS o ADMIN ha ultimato la compilazione delle informazioni per tutti gli ambienti previsti e deve archiviare il file di una istanza di blueprint generato ed in archivio sul sistema SCM Git.

- QUINDI: 
  - Il sistema deve permettere di archiviare il file associato all'occoorrenza dell'istanza di blueprint compilata (FILE_BLUEPRINT_TARGET) sul sistema SCM Git
  - Al termine delle operazioni il sistema dovrà aver inserito una occorrenza nelle seguenti tabelle: STATO_ISTANZA_BLUEPRINT <br />

<br />

## Controlli e vincoli

Al momento sono previsti i seguenti controlli/vincoli:
- Il passaggio di stato a *Archiviata* pùo essere eseguito solo per le istanze in stato *In Compilazione*


<br />                        
<br />

## Trigger

Esigenza di finalizzare la compilazione delle configurazioni dei componenti definiti nel file dell'istanza di blueprint ed archiviare il file sul sistema SCM Git.

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

![Sequence diagram della user story](../files/sequence_diagram_us_8.jpg)
<br />

[Download file visio del sequence diagram della user story ](../files/sequence_diagram_us_8.vsdx)

<br />
<br />

## User Interface Mockup

- UI 8.1

![User Interface](../images/ui_us_4_ricerca_istanza_blueprint.jpg)

<br />
<br />

- UI 8.2


![User Interface](../images/ui_us_4_ricerca_istanza_blueprint_risultati.jpg)

<br />
<br />

- UI 8.3


![User Interface](../images/ui_us_8_archiviazione_istanza_blueprint.jpg)

<br />
<br />

## Interfaccia Applicativa con Correlazione Chiamate ai Metodi Corrispondenti

Di seguito è riportata l'interfaccia applicativa (screen) Archiviazione Istanza Blueprint di PIM prodotta nella FASE1 con conseguente correlazione alla chiamata al metodo della specifica funzionalità evidenziata, al fine di agevolare lo sviluppo della FASE2 (in fase di definizione).

Per l'"Archiviazione Istanza Blueprint", oggetto della corrente US, dopo aver correttamente eseguito l'attività di compilazione (Vedi [User Story - Id 6 - Compilazione Istanza Blueprint](us_6_compilazione_istanza_blueprint.md)) è possibile cambiare lo stato da "in Compilazione" ad "Archiviata".

![Compilazione](../images/Compilazione_5.png)

Per farlo è necessario cliccare sul PURPLE BOX "Archiviazione" al fine di poter richiamare il metodo PUT archivia e cambiare lo stato in "Archiviata".

![CambioStato](../images/In_esercizio_In_compilazione.png)

Una volta effettuato il cambio stato è possibile ritornare nello stato in compilazione cliccando sul GREY BOX "In compilazione" (vedi [User Story - Id 9 - Compilazione Istanza Blueprint - Back In Compilazione](us_9_compilazione_istanza_blueprint_back.md)) o sul BLACK BOX "In esercizio" (vedi [User Story - Id 10 - Esercizio Istanza Blueprint](us_10_esercizio_istanza_blueprint.md)) per passare allo stato successivo. 

<br/>

Nella tabella in basso, viene mostrato un riepilogo con relativa chiamata al metodo di tutti i buttons presentati in queste interfacce con relativo PATH: 

|Colore di riferimento|Pulsante Definito nell'Applicativo  |Tipologia Chiamata  |Nome chiamata | Path |Note|
|---------|---------|---------|---------|---------|---------|
|PURPLE|Archiviazione|PUT |archivia |{{baseUrl}}/pim-api/blueprint/:id/archivia |/|
|BLACK|In Esercizio |/ |/ |/ |vedi [User Story - Id 10 - Esercizio Istanza Blueprint](us_10_esercizio_istanza_blueprint.md)|
|GREY|In Compilazione |/ |/ |/ |vedi [User Story - Id 9 - Compilazione Istanza Blueprint - Back In Compilazione](us_9_compilazione_istanza_blueprint_back.md) |
|GREY|Copia Ambiente|/ |/|/|vedi [User Story - Id 7 - Compilazione Istanza Blueprint - Generazione Versione - Ambiente](us_7_compilazione_istanza_blueprint_gen_versione.md)|
|ROSE|YAML|/ |/|/|vedi [User Story - Id 6 - Compilazione Istanza Blueprint](us_6_compilazione_istanza_blueprint.md)|