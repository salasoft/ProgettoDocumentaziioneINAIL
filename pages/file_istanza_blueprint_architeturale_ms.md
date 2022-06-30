### 9.4. File di istanza della Blueprint Architetturale Microservizio della soluzione Product Infrastructure Management - PIM
<br/>
Di seguito è riportato il file di istanza di Blueprint Architetturale compilato per la componente di back-end a partire dal template identificato.

-   Istanza Blueprint Architetturale PIM back-end: [file](../files/esempio_istanza_blueprint_pim_be.yml)

<br/>

<pre>
Prodotto:
    identificativoProdotto: 'pim'
    nomeProdotto: 'Gestione Infrastruttura di prodotto'
    tipoProdotto: 'back-end'
    descrizioneProdotto: 'Prodotto per la gestione delle informazioni di infrastrutura previste dai template blueprint'
    dataCensimento: '2021-05-25'
    stato: 'attivo'
    modulo:
        idModulo: 'gestinfra'
        nomeModulo: 'gestinfra'
        tipoModulo: 'Servizio'
        descrizioneModulo: 'Breve descrizione del modulo applicativo'
        componente:
            idComponente: 'gestinfra-app'
            nomeComponente: 'gestinfra-app'
            tipoComponente: 'Logica applicativa'
            descrizioneComponente: 'Breve descrizione della componente applicativa'
            tecnologia: 'SpringBoot'
            deployEnvironment: 'openshift'
        componente:
            idComponente: 'gestinfra-sql'
            nomeComponente: 'gestinfra-sql'
            tipoComponente: 'DatiSQL'
            tecnologia: 'oracle'
            deployEnvironment: 'exadata'
        componente:
            idComponente: 'gestinfra-api'
            nomeComponente: 'gestinfra-api'
            tipoComponente: 'OpenAPI3'
            tecnologia: 'xml'
            deployEnvironment: 'apigateway'
</pre>