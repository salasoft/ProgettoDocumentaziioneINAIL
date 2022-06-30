### 9.19. Template Infrastruttura PIM TEST BACK-END

Di seguito è riportato il template di infrastruttura identificato per la componente back-end.

-   Tipo Prodotto: back-end

<pre>
prodotto:
  idProdotto: "servizi_per_la_release_management_platform"
  nomeProdotto: "Servizi per la Release Management Platform"
  versioneProdotto: "1.0.0"
  tipoProdotto: "headless"
  blueprint: "servizi-ocp"
  descrizioneProdotto: "Il prodotto espone le api necessarie ad erogare le funzionalità\
    \ di release management, di amministrazione della soluzione e di integrazione\
    \ con gli altri sistemi coinvolti nel ciclo di rilascio del prodotto)"
  dataCensimento: "14/03/2022"
  stato: "Sviluppo"
  moduli:
  - idModulo: "gestionepa-be"
    nomeModulo: "gestionepa-be"
    versioneModulo: "1.0.0"
    tipoModulo: "Servizio"
    pattern: "mongodb-oracle-springboot"
    descrizioneModulo: ""
    componenti:
    - idComponente: "database-component"
      nomeComponente: "database-component"
      descrizioneComponente: "database-component"
      layer: "dati"
      tipoComponente: "Dati SQL"
      repoGit: "https://gitlab-os-lab.inail.it/servizi-ocp/servizi_per_la_release_management_platform"
      versioneComponente: null
      versioneConfig: "1.0.0"
      tecnologia: "oracle"
      deployEnvironment: "sql"
      runtimeEnvironment: {}
      config-repoGit: "https://gitlab-os-lab.inail.it/servizi-ocp/servizi_per_la_release_management_platform/configurazione-infrastrutturale-prodotto"
    - idComponente: "logica-be-component"
      nomeComponente: "logica-be-component"
      descrizioneComponente: "logica-be-component"
      layer: "BE"
      tipoComponente: "Logica Applicativa BE"
      repoGit: "https://gitlab-os-lab.inail.it/servizi-ocp/servizi_per_la_release_management_platform"
      versioneComponente: null
      versioneConfig: "1.0.0"
      tecnologia: "springboot"
      deployEnvironment: "openshift"
      runtimeEnvironment: {}
      config-repoGit: "https://gitlab-os-lab.inail.it/servizi-ocp/servizi_per_la_release_management_platform/configurazione-infrastrutturale-prodotto"
</pre>
