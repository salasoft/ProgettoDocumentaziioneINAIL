### 9.18. Template Infrastruttura PIM TEST FRONT-END

Di seguito è riportato il template di infrastruttura identificato per la componente front-end.

-   Tipo Prodotto: front-end

<pre>
prodotto:
  idProdotto: "pim-ui"
  nomeProdotto: "pim-ui"
  versioneProdotto: "NA"
  blueprint: "spa-monolitica"
  tipoProdotto: "Front End"
  descrizioneProdotto: "Prodotto di front-end per la gestione della infrastruttura fisica di prodotto"
  dataCensimento: "2021-11-12"
  stato: "attivo"
  moduli:
  - idModulo: "gestinfra-ui"
    nomeModulo: "gestinfra-ui"
    tipoModulo: "Client"
    descrizioneModulo: "Interfaccia per la gestione della infrastruttura fisica di prodotto"
    versioneModulo: "NA"
    pattern: "angular-apache-apig"
    componenti:
    - idComponente: "pim-ui"
      nomeComponente: "pim-ui"
      tipoComponente: "SPA"
      descrizioneComponente: "Interfaccia utente per la gestione della infrastruttura fisica di prodotto"
      tecnologia: "angular"
      deployEnvironment: "apache-spa-intranet"
      layer: "FE"
      repoGit: "https://gitlab-os-lab.inail.it/spa-monolitica/gestinfra-ui/pim-ui/pim-spa.git"
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment: {}
    - idComponente: "pim-ui-cdn"
      nomeComponente: "pim-ui-cdn"
      tipoComponente: "CDN"
      descrizioneComponente: "Componente relativa alla configurazione della CDN"
      tecnologia: "js-css-html"
      deployEnvironment: "apache-cdn"
      layer: "FE"
      repoGit: "https://gitlab-os-lab.inail.it/spa-monolitica/gestinfra-ui/pim-ui/pim-cdn.git"
      versioneComponente: "NA"
      versioneConfig: "NA"
    - idComponente: "client-pim-ui"
      nomeComponente: "client-pim-ui"
      tipoComponente: "Client Apig"
      descrizioneComponente: "Componente dedicata alla gstione della configurazione dei servizi, necessari al funzionamento della spa, esposti su apig"
      tecnologia: "json"
      deployEnvironment: "apigateway"
      layer: "Mediation"
      repoGit: "https://gitlab-os-lab.inail.it/spa-monolitica/gestinfra-ui/pim-ui/pim-apig.git"
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment: {}

</pre>
