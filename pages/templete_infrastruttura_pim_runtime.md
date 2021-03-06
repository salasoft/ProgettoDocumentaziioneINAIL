### 9.17. Template Infrastruttura PIM TEST Completo (con runtime environment)

Di seguito è riportato il template di infrastruttura identificato per la componente di back-end/front-end a scopo di test con le sezioni di runtime environment (ambiente utilizzato CI - Continuos Integration).

-   Tipo Prodotto: back-end/front-end

<pre>
prodotto:
  idProdotto: "pim"
  nomeProdotto: "Gestione Infrastruttura di prodotto"
  versioneProdotto: "NA"
  blueprint: "servizi stateless su Openshift"
  tipoProdotto: "headless"
  descrizioneProdotto: "Prodotto di back-end per la gestione delle informazioni di infrastrutura fisica di prodotto per PIM test"
  dataCensimento: "1635120000000"
  stato: "attivo"
  moduli:
  - idModulo: "gestinfra"
    nomeModulo: "gestinfra"
    tipoModulo: "Servizio"
    descrizioneModulo: "Servizio dedicato alla gestione delle informazioni di infrastrutura fisica di prodotto"
    versioneModulo: "NA"
    pattern: "servizio-springboot"
    componenti:
    - idComponente: "gestinfra-app"
      nomeComponente: "gestinfra-app"
      tipoComponente: "Logica Applicativa BE"
      descrizioneComponente: "Logica applicativa relativa al servizio dedicato alla gestione di infrastrutura fisica di prodotto"
      tecnologia: "springboot"
      deployEnvironment: "openshift"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/..."
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeProgettoOpenShift: "pim"
          nomeDeploymentConfig: "gestinfra-app"
          configMapPod:
            configMap:
              source: "Source Config Map"
              urlGit: "Url Git Config Map"
              mounthPath: "/deployments/config"
            secretConfigMap:
              source: " Source Config Map Secrets"
              urlGit: "Url Git Config Map Secrets"
              mounthPath: "/deployments/config"
          routing:
            enabled: true
            route: "gestinfra-app"
            hostName: "gestinfra-app"
            path: "/"
            service: "gestinfra-app"
            targetPortProtocol: "8081"
            targetPort: "8080"
          healthChecks:
            readynessProbe:
              protocolType: "httpGet"
              useHttps: true
              path: "/health/ready"
              port: "8080"
              initialDelay: "100"
              timeOut: "100"
            livenessProbe:
              protocolType: "httpGet"
              useHttps: true
              path: "/health/live"
              port: "8080"
              initialDelay: "100"
              timeOut: "100"
      config-repoGit: "https://gitlab-os-lab.inail.it/..."
    - idComponente: "admin-app"
      nomeComponente: "admin-app"
      tipoComponente: "Logica Applicativa BE"
      descrizioneComponente: "Logica applicativa relativa al servizio dedicato all'amministrazione di prodotto"
      tecnologia: "dotnet"
      deployEnvironment: "openshift"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/..."
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeProgettoOpenShift: "pim"
          nomeDeploymentConfig: "admin-app"
          configMapPod:
            configMap:
              source: "Source Config Map"
              urlGit: "Url Git Config Map"
              mounthPath: "/deployments/config"
            secretConfigMap:
              source: " Source Config Map Secrets"
              urlGit: "Url Git Config Map Secrets"
              mounthPath: "/deployments/config"
          routing:
            enabled: false
            route: "admin-app"
            hostName: "gestinfra-app"
            path: "/"
            service: "admin-app"
            targetPortProtocol: "8081"
            targetPort: "8080"
          healthChecks:
            readynessProbe:
              protocolType: "httpGet"
              useHttps: true
              path: "/health/ready"
              port: "8080"
              initialDelay: "100"
              timeOut: "100"
            livenessProbe:
              protocolType: "httpGet"
              useHttps: true
              path: "/health/live"
              port: "8080"
              initialDelay: "100"
              timeOut: "100"
      config-repoGit: "https://gitlab-os-lab.inail.it/..."
    - idComponente: "gestinfra-sql"
      nomeComponente: "gestinfra-sql"
      tipoComponente: "Dati SQL"
      descrizioneComponente: "Componente dati relativa al servizio dedicato alla gestione di infrastruttura di prodotto"
      tecnologia: "oracle"
      deployEnvironment: "exadata"
      layer: "Dati"
      repoGit: "https://gitlab-os-lab.inail.it/..."
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomePDB: "PDBpimCI"
          nomeSchema: "gestinfra_sql"
          tableSpace: "TS_gestinfra_sql"
          oracleScan:
            porta: ""
            enabled: false
            hostname1: ""
            service_name1: ""
            hostname2: ""
            service_name2: ""
          porta: "8080"
          hostname: "Hostname SQL"
          service_name: "Service Name - SQL"
      config-repoGit: "https://gitlab-os-lab.inail.it/..."
    - idComponente: "gestinfra-sql-PROVA"
      nomeComponente: "gestinfra-sql-PROVA"
      tipoComponente: "Dati SQL"
      descrizioneComponente: "Componente dati relativa al servizio dedicato alla gestione di infrastruttura di prodotto"
      tecnologia: "oracle"
      deployEnvironment: "exadata"
      layer: "Dati"
      repoGit: "https://gitlab-os-lab.inail.it/..."
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomePDB: "PDBpimCI"
          nomeSchema: "gestinfra_sql_PROVA"
          tableSpace: "TS_gestinfra_sql_PROVA"
          oracleScan:
            porta: "8080"
            enabled: true
            hostname1: "Host Name 1 Oracle Scan"
            service_name1: "Service Name 1 Oracle Scan"
            hostname2: "Host Name 2 Oracle Scan"
            service_name2: "Service Name 2 Oracle Scan"
          porta: ""
          hostname: ""
          service_name: ""
      config-repoGit: "https://gitlab-os-lab.inail.it/..."
    - idComponente: "gestinfra-api"
      nomeComponente: "gestinfra-api"
      tipoComponente: "Api Sincrone"
      descrizioneComponente: "Componente dedicata all'esposizione su API Gateway del servizio dedicato alla gestione di infrastrutura fisica di prodotto"
      tecnologia: "openapi3"
      deployEnvironment: "apigateway"
      layer: "Mediation"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          cluster: "CI"
          cluster_url: "https://collportale.inail.it"
          compid_nome: "pim-gestinfra-api/CODalpha"
          compid_descrizione: "AU servizio tipologiche"
          compid_apig_url_pub: "https://collportale.inail.it/api/au/persona/tipologiche"
          compid_pdd_url_pub: "https://spc.test.inail.it/pdd"
          compid_apim_url_pub: "https://apicoll.inailcloud.it"
          compid_categoria: "pim"
    - idComponente: "gestinfra-sub"
      nomeComponente: "gestinfra-sub"
      tipoComponente: "Evento Esterno Sub"
      descrizioneComponente: "Componente dedicata alla coda Sub AMQ gestione di infrastrutura fisica di prodotto"
      tecnologia: "amq"
      deployEnvironment: "openshif"
      layer: "Mediation"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          routingType: "Multicast"
          urlBroker: "Url Broker SUB"
          nomeCoda: "pim.gest.sub.evento"
    - idComponente: "gestinfra-nosql"
      nomeComponente: "gestinfra-nosql"
      tipoComponente: "Dati NoSQL"
      descrizioneComponente: "Componente dati NOSQL relativa al servizio dedicato alla gestione di infrastruttura di prodotto"
      tecnologia: "mongodb"
      deployEnvironment: "Server"
      layer: "Dati"
      repoGit: "https://gitlab-os-lab.inail.it/..."
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeServer: "Nome Server "
          ruoloServer: "Primario"
          replicaSet: "Repl-pim"
          connectionstring: "jdbc:mongodb://..."
          portaServer: "Porta Server"
          nomeDB: "DB_pimCI"
          nomeUtenza: "Nome Utenza"
      config-repoGit: "https://gitlab-os-lab.inail.it/..."
  - idModulo: "checknaming"
    nomeModulo: "checknaming"
    tipoModulo: "Servizio"
    descrizioneModulo: "Servizio dedicato alla gestione della naming su infrastrutura fisica di prodotto"
    versioneModulo: "NA"
    pattern: "servizio-springboot"
    componenti:
    - idComponente: "check-cdn-app"
      nomeComponente: "check-js-css-html-cdn"
      tipoComponente: "CDN"
      descrizioneComponente: "Componente dedicata alla coda Request AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "js-css-html"
      deployEnvironment: "openshif"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeCDN: "pim-cdn"
          fqdn: "cdnci.inailcloud.it"
    - idComponente: "check-cdn-app-PROVA"
      nomeComponente: "check-js-css-html-cdn-PROVA"
      tipoComponente: "CDN"
      descrizioneComponente: "Componente dedicata alla coda Request AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "js-css-html"
      deployEnvironment: "openshif"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeCDN: "pim-cdn"
          fqdn: "cdnci.inailcloud.it"
    - idComponente: "check-post-gres-sql-app"
      nomeComponente: "check-post-gres-sql-app"
      tipoComponente: "Dati SQL"
      descrizioneComponente: "Componente dedicata alla coda Request AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "postgresql"
      deployEnvironment: "openshif"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeDB: "DB_pim"
          nomeSchema: "Nome Schema"
          nomeUtenza: "check-post-gres-sql-app"
          tablespace: "TS_check-post-gres-sql-app"
          nomeServer: "Nome Server"
          ruoloServer: "Master"
          porta: "Porta"
          connectionString: "Connection String"
          ipserver: "Ip Server"
    - idComponente: "checknaming-app"
      nomeComponente: "checknaming-app"
      tipoComponente: "Logica Applicativa BE"
      descrizioneComponente: "Logica applicativa relativa al servizio della naming su infrastrutura fisica di prodotto"
      tecnologia: "nodejs"
      deployEnvironment: "openshift"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/..."
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeProgettoOpenShift: "Nome Progetto OpenShift"
          nomeDeploymentConfig: "Nome Deployment Config"
          configMapPod:
            configMap:
              source: "Source Config Map"
              urlGit: "Url Git Config Map"
              mounthPath: "Mounth Path Config Map"
            secretConfigMap:
              source: "Source Config Map Secrets"
              urlGit: "Url Git Config Map Secrets"
              mounthPath: "Mounth Path Config Map Secrets"
          routing:
            enabled: false
            route: ""
            hostName: ""
            path: ""
            service: ""
            targetPortProtocol: ""
            targetPort: ""
          healthChecks:
            readynessProbe:
              protocolType: "Protocol Type Readyness"
              useHttps: true
              path: "Path Readyness"
              port: "Port Readyness"
              initialDelay: "Initial Delay Readyness"
              timeOut: "Timeout Readyness"
            livenessProbe:
              protocolType: "Protocol Type Liveness"
              useHttps: true
              path: "Path Liveness"
              port: "8080 "
              initialDelay: "Initial Delay Liveness"
              timeOut: "Timeout Liveness"
      config-repoGit: "https://gitlab-os-lab.inail.it/..."
    - idComponente: "checknaming-sql"
      nomeComponente: "checknaming-sql"
      tipoComponente: "Dati SQL"
      descrizioneComponente: "Componente dati relativa al servizio della naming di infrastruttura di prodotto"
      tecnologia: "sqlserver"
      deployEnvironment: "Server"
      layer: "Dati"
      repoGit: "https://gitlab-os-lab.inail.it/..."
      versioneComponente: "NA"
      versioneConfig: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeIstanzaDB: "Nome Istanza DB"
          ipistanzaDB: "Ip Istanza DB"
          nomeDB: "DBpim"
          connectionString: "jdbc://weblogic:sqlserver//..."
          nomeSchema: "checknaming-sql"
      config-repoGit: "https://gitlab-os-lab.inail.it/..."
    - idComponente: "checknaming-api"
      nomeComponente: "checknaming-api"
      tipoComponente: "Api Sincrone"
      descrizioneComponente: "Componente dedicata all'esposizione su API Gateway del servizio dedicato alla naming su infrastrutura fisica di prodotto"
      tecnologia: "openapi3"
      deployEnvironment: "apigateway"
      layer: "Mediation"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          cluster: "CI"
          cluster_url: "https://collportale.inail.it"
          compid_nome: "pim-checknaming-api/CODalpha"
          compid_descrizione: "AU Servizio Tipologiche "
          compid_apig_url_pub: "https://collportale.inail.it/api/au/persona/tipologiche"
          compid_pdd_url_pub: "https://spc.test.inail.it/pdd"
          compid_apim_url_pub: "https://apicoll.inailcloud.it/irestgw"
          compid_categoria: "pim"
    - idComponente: "checknaming-pub"
      nomeComponente: "checknaming-pub"
      tipoComponente: "Evento Esterno Pub"
      descrizioneComponente: "Componente dedicata alla coda Pub AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "amq"
      deployEnvironment: "openshif"
      layer: "Mediation"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          address: "pim.check.pub.evento"
          routingType: "Multicast"
          urlBroker: "https://urlBroker.it"
    - idComponente: "checknaming-que"
      nomeComponente: "checknaming-que"
      tipoComponente: "Coda Request Esterna"
      descrizioneComponente: "Componente dedicata alla coda Request AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "amq"
      deployEnvironment: "openshif"
      layer: "Mediation"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          address: "pim.checknaming.que.nomeCoda"
          routingType: "Anycast"
          urlBroker: "https://urlBroker.it"
          nomeCoda: "pim.checknaming.que.nomeCoda"
    - idComponente: "checkluw-app"
      nomeComponente: "checkluw-app"
      tipoComponente: "Dati SQL"
      descrizioneComponente: "Componente dedicata alla coda Request AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "db2luw"
      deployEnvironment: "openshif"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeDB: "Nome DB"
          nomeSchema: "Nome Schema"
          nomeUtenza: "Nome Utenza"
          tablespaceDati: "Tablespace Dati"
          tablespaceIDX: "Tablespace IDX"
          tablespaceLOB: "Tablespace LOB"
          connectionString: "Connection String"
    - idComponente: "check-apig-client-app"
      nomeComponente: "check-apig-client-app"
      tipoComponente: "Client Apig"
      descrizioneComponente: "Componente dedicata alla coda Request AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "json"
      deployEnvironment: "openshif"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          compid_client_name: "Clientpim"
          compid_client_batch_name: "BATCH_Clientpim"
    - idComponente: "check-angular-app"
      nomeComponente: "check-angular-app"
      tipoComponente: "SPA"
      descrizioneComponente: "Componente dedicata alla coda Request AMQ gestione della naming su infrastrutura fisica di prodotto"
      tecnologia: "angular"
      deployEnvironment: "openshif"
      layer: "BE"
      repoGit: "https://gitlab-os-lab.inail.it/.."
      versioneComponente: "NA"
      runtimeEnvironment:
        ci:
          available: true
          nomeSPA: "pim"
          contesto: "pim"
          fqdnIntranet: "https://ciportale.inail.it/appintra/"
          fqdnInternet: "https://ciportale.inail.it/app/"

</pre>
