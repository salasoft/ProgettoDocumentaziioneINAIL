
### 9.5. Tipologie di componenti e relative tecnologie previste per una Blueprint Architetturale

Di seguito sono rappresentate tutte le casistiche al momento previste per la compilazione delle istanze di blueprint architetturali.
Nella colonna In Scope sono indicate quelle a cui si deve fare riferimento per lo sviluppo delle funzionalità applicative.

|     | Tipo Componente          | Cod. Tipo Componente | Tecnologia   | Deploy Environemt  | In Scope | 
| --- | -----------------------  | -------------------- |------------- | ------------------ | -------- |  
|  1  |   Logica Applicativa     |   ms                 | Spring-Boot  | openshift          |    SI    | 
|  2  |   Logica Applicativa     |   ms                 | NodeJS       | openshift          |    NO    | 
|  3  |   Logica Applicativa     |   ms                 | DotNet       | openshift          |    NO    | 
|  4  |   UI Applicativa         |   spa                | Angular      | Apache             |    SI    | 
|  4  |   UI Applicativa         |   cdn                | CDN          | Apache             |    NO    | 
|  5  |   Api sincrone           |   api                | OpenApi3     | apigateway         |    SI    | 
|  6  |   Code request           |   que                | AMQ          | broker             |    SI    | 
|  7  |   Code Pub               |   pub                | AMQ          | broker             |    NO    | 
|  8  |   Code Sub               |   sub                | AMQ          | broker             |    NO    | 
|  9  |   DatiSQL                |   sql                | Oracle       | sql                |    SI    | 
|  10 |   DatiSQL                |   sql                | SQL Server   | sql                |    NO    | 
|  11 |   DatiSQL                |   sql                | DB2 Luw      | sql                |    NO    | 
|  12 |   DatiSQL                |   sql                | Postgresql   | sql                |    NO    | 
|  13 |   DatiNoSQL              |   nosql              | MongoDB      | nosql              |    NO    | 

<br />
Facciamo un esempio. Se esiste in EA un prodotto censito come indoc a cui è stata associata una blueprint servizi stateless su OpenShift, il Dev potrà creare un modulo di prodotto di tipo microservizio che supponiamo voglia chiamare protocollo.
<br />
La toolchain in questo caso chiamerà quel microservizio indoc.protocollo. Poiché il modulo ha più componenti si avrà che ognuno di essi sarà  identificato da:
<br />
`[NOME_ PRODOTTO].[NOME_MODULO].[COD_TIPO_COMPONENTE].[NOME_COMPONENTE]`
<br />

I componenti di indoc.protocollo saranno, per esempio:

| Nome Prodotto    | Nome Modulo      | Tipo Componente | Nome Componente  | Naming                          |
| ---------------- | ---------------- | --------------- | ---------------- | ------------------------------- |
|  indoc           | indoc            | spa             | indoc            | indoc.indoc.spa.indoc           |
|  indoc           | indoc            | cdn             | indoc            | indoc.indoc.cdn.indoc           |
|  indoc           | indoc            | ms              | protocollo       | indoc.indoc.ms.protocollo       |
|  indoc           | indoc            | ms              | pratica          | indoc.indoc.ms.pratica          |
|  indoc           | protocollo       | sql             | protocollo1      | indoc.indoc.sql.protocollo1     |
|  indoc           | protocollo       | sql             | protocollo2      | indoc.indoc.sql.protocollo2     | 
|  indoc           | protocollo       | nosql           | protocollo       | indoc.indoc.nosql.protocollo    |
|  indoc           | protocollo       | que             | coda1            | indoc.indoc.que.coda1            |
|  indoc           | protocollo       | pub             | eventoX          | indoc.indoc.pub.eventoX         |
|  indoc           | protocollo       | sub             | eventoY          | indoc.indoc.pub.eventoY         |
|  indoc           | protocollo       | sub             | eventoZ          | indoc.indoc.pub.eventoZ         |
|  indoc           | protocollo       | api             | interfaccia1     | indoc.indoc.api.interfaccia1    |
|  indoc           | protocollo       | api             | interfaccia2     | indoc.indoc.api.interfaccia2    |



<br />
Laddove il componente di un certo tipo all'interno di un modulo sia soltanto uno, allora il nome del componente potrà essere uguale al nome del modulo.
<br />
Nell'esempio il servizio indoc.protocollo ha 13 componenti: 2 di logica applicativa, 3 sorgenti dati, 4 code di messaggi asincroni, 
pubblicatore di 1 evento, sottoscrittore di 2 eventi, 1 interfaccia verso Internet ed 1 interfaccia verso Intranet.

<br />
<br />
