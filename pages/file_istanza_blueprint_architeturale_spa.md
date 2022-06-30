### 9.2. File di istanza della Blueprint Architetturale Single Page Application della soluzione Product Infrastructure Management - PIM
<br/>
Di seguito è riportato il file di istanza di Blueprint Architetturale compilato per la componente di front-end a partire dal template identificato.

-   Istanza Blueprint Architetturale PIM front-end: [file](../files/esempio_istanza_blueprint_pim_fe.yml)

<br/>

<pre>
Prodotto:
    identificativoProdotto: 'pimui'
    nomeProdotto: 'Portale Gestione Infrastruttura di prodotto'
    tipoProdotto: 'front-end'
    descrizioneProdotto: 'Prodotto per la gestione delle informazioni di infrastrutura previste dai template blueprint'
    dataCensimento: '2021-05-25'
    stato: 'attivo'
    modulo:
        idModulo: 'gestinfra-ui'
        nomeModulo: 'gestinfra-ui'
        tipoModulo: 'Client'
        descrizioneModulo: 'Breve descrizione del modulo applicativo'
        componente:
            idComponente: 'pim-ui'
            nomeComponente: 'pim-ui'
            tipoComponente: 'Logica applicativa'
            descrizioneComponente: 'Breve descrizione della componente applicativa'
            tecnologia: 'angular'
            deployEnvironment: 'apache-spa'
</pre>