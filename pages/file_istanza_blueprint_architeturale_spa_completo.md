### 9.2. File di istanza della Blueprint Architetturale Single Page Application della soluzione Product Infrastructure Management - PIM
<br/>
Di seguito è riportato il file di istanza di Blueprint Architetturale compilato per la componente di front-end a partire dal template identificato.

-   Istanza Blueprint Architetturale PIM front-end: [file](../files/esempio_istanza_blueprint_pim_fe_completo.yml)

<br/>

<pre>
prodotto:
  identificativoProdotto: pimui
  nomeProdotto: Portale gestione infrastruttura di prodotto test
  tipoProdotto: front-end
  descrizioneProdotto: Prodotto front-end per la gestione delle informazioni di infrastrutura previste dai template di blueprint test
  dataCensimento: 2021-05-25T00:00:00Z
  stato: attivo
  modulo:
  - idModulo: gestinfra-ui
    nomeModulo: gestinfra-ui
    tipoModulo: Client
    descrizioneModulo: Breve descrizione del modulo applicativo test
    componente:
    - idComponente: pim-ui
      nomeComponente: pim-ui
      tipoComponente: Logica applicativa
      descrizioneComponente: Componente di front-end, client del prodotto Gestione Infrastruttura di prodotto test mirco
      tecnologia: angular
      deployEnvironment: apache-spa
      runtimeEnvironment:
        coll:
          nomeSPA: Nome co
          contesto: Nome della co
        ci:
          nomeSPA: Nome ci
          contesto: Nome della ci
        cert:
          nomeSPA: Nome ce
          contesto: Nome della ce

</pre>