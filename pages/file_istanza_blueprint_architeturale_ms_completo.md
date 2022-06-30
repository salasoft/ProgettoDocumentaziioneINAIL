### 9.4. File di istanza della Blueprint Architetturale Microservizio della soluzione Product Infrastructure Management - PIM
<br/>
Di seguito è riportato il file di istanza di Blueprint Architetturale compilato per la componente di back-end a partire dal template identificato.

-   Istanza Blueprint Architetturale PIM back-end: [file](../files/esempio_istanza_blueprint_pim_be_completo.yml)

<br/>

<pre>
prodotto:
  identificativoProdotto: pim
  nomeProdotto: Gestione Infrastruttura di prodotto
  tipoProdotto: back-end
  descrizioneProdotto: Prodotto di back-end per la gestione delle informazioni di infrastrutura previste dai template blueprint
  dataCensimento: 2021-05-25T00:00:00Z
  stato: attivo
  modulo:
  - idModulo: gestinfra
    nomeModulo: gestinfra
    tipoModulo: Servizio
    descrizioneModulo: Breve descrizione del modulo applicativo
    componente:
    - idComponente: gestinfra-app
      nomeComponente: gestinfra-app
      tipoComponente: Logica applicativa
      descrizioneComponente: Componente microservizio di prodotto
      tecnologia: SpringBoot
      deployEnvironment: openshift
      runtimeEnvironment:
        coll:
          istanzaOpenShift: Istanza OpenShift co
          nomeProgettoOpenShift: Progetto OpenShift co
          imageName: Image Name co
          podName: Pod co
          podScale:
            min: '1'
            max: '3'
          configMapPod:
            configMap:
              source: Source co
              mounthPath: Mounth Path co
            configMapSecrets:
              source: Source co
              mounthPath: Mounth Path co
          route:
            enabled: true
            name: Name co
            hostName: '  Host Name co'
            path: Path co
            service: Service co
            targetPortProtocol: Target Port Protocol co
            targetPort: Target Port co
          healtChecks:
            readynessProbe:
              type: Type rp co
              useHttps: false
              path: Path rp co
              port: Port co
              initialDelay: Initial rp co
              timeOut: Timeout co
            livenessProbe:
              type: type co
              useHttps: true
              path: Path co
              port: '1000'
              initialDelay: Initial co
              timeOut: Timeout co
        prod:
          istanzaOpenShift: Istanza OpenShift pr
          nomeProgettoOpenShift: Progetto OpenShift pr
          imageName: Image Name pr
          podName: Pod pr
          podScale:
            min: '1'
            max: '4'
          configMapPod:
            configMap:
              source: Source pr
              mounthPath: Mounth Path pr
            configMapSecrets:
              source: Source pr
              mounthPath: Mounth Path pr
          route:
            enabled: true
            name: Name pr
            hostName: '  Host Name pr'
            path: Path pr
            service: Service pr
            targetPortProtocol: Target Port Protocol pr
            targetPort: Service pr
          healtChecks:
            readynessProbe:
              type: Type rp pr
              useHttps: true
              path: Path rp pr
              port: Port pr
              initialDelay: Initial rp pt
              timeOut: Timeout co
            livenessProbe:
              type: type pr
              useHttps: true
              path: Path pr
              port: '1000'
              initialDelay: Initial pr
              timeOut: Timeout pr
        ci:
          istanzaOpenShift: Istanza OpenShift ci
          nomeProgettoOpenShift: Progetto OpenShift ci
          imageName: Image Name ci
          podName: Pod ci
          podScale:
            min: '1'
            max: '2'
          configMapPod:
            configMap:
              source: Source ci
              mounthPath: Mounth Path ci
            configMapSecrets:
              source: Source ci
              mounthPath: Mounth Path ci
          route:
            enabled: false
            name: null
            hostName: null
            path: null
            service: null
            targetPortProtocol: null
            targetPort: null
          healtChecks:
            readynessProbe:
              type: Type rp ci
              useHttps: true
              path: Path rp ci
              port: Port ci
              initialDelay: Initial rp ci
              timeOut: Timeout ci
            livenessProbe:
              type: type ci
              useHttps: true
              path: Path ci
              port: Port ci
              initialDelay: Initial ci
              timeOut: Timeout ci
    - idComponente: gestinfra-sql
      nomeComponente: gestinfra-sql
      tipoComponente: DatiSQL
      descrizioneComponente: Componente dati del microservizio di prodotto
      tecnologia: oracle
      deployEnvironment: exadata
      runtimeEnvironment:
        coll:
          nomeIstanzaDB: Nome Istanza DB co
          ipIstanzaDB: Istanza co
          nomePDB: Nome PDB co
          nomeSchema: Nome schema co
          nomeUtenza: Nome Utenza co
          tableSpace: Tablespace co
          oracleScannabled: true
          oracleScan: Oracle Scan co
          hostName1: Host Name 1 co
          serviceName1: Service Name 1 co
          hostName2: Host Name 2 co
          serviceName2: Service Name 2 co
          portNumber: '1521'
          secretKey: ffregret4 co
        prod:
          nomeIstanzaDB: Nome Istanza DB pr
          ipIstanzaDB: Istanza pr
          nomePDB: Nome PDB pr
          nomeSchema: Nome schema pr
          nomeUtenza: Nome Utenza pr
          tableSpace: Tablespace pr
          oracleScannabled: true
          oracleScan: Oracle Scan pr
          hostName1: Host Name 1 pr
          serviceName1: Service Name 1 pr
          hostName2: Host Name 2 pr
          serviceName2: Service Name 2 pr
          portNumber: '1521'
          secretKey: ffregret4 pr
        ci:
          nomeIstanzaDB: Nome Istanza DB ci
          ipIstanzaDB: Istanza ci
          nomePDB: Nome PDB ci
          nomeSchema: Nome schema ci
          nomeUtenza: Nome Utenza ci
          tableSpace: Tablespace ci
          oracleScannabled: false
          oracleScan: Oracle Scan ci
          hostName1: Host Name 1 ci
          serviceName1: Service Name 1 ci
          hostName2: Host Name 2 ci
          serviceName2: Service Name 2 ci
          portNumber: '1521'
          secretKey: ffregret4 ci
    - idComponente: gestinfra-api
      nomeComponente: gestinfra-api
      tipoComponente: OpenAPI3
      descrizioneComponente: Componente API del microservizio di prodotto
      tecnologia: xml
      deployEnvironment: apigateway
      runtimeEnvironment:
        coll:
          clusterName: Cluster Name co
          clusterURL: Cluster  url co
          publicURL: Public URL co
          gruppo: Gruppo co
          categoria: Categoria co
        prod:
          clusterName: Cluster Name pr
          clusterURL: Cluster url pr
          publicURL: Public URL pr
          gruppo: Gruppo pr
          categoria: Categoria pr
        ci:
          clusterName: Cluster Name ci
          clusterURL: Cluster  url ci
          publicURL: Public URL ci
          gruppo: Gruppo ci
          categoria: Categoria ci

</pre>