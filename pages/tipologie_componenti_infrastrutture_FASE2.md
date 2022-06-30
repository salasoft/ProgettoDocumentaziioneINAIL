### 9.15. Tipologie di componenti e relative tecnologie previste per una infrastruttura

Di seguito sono rappresentate tutte le casistiche al momento previste per la compilazione delle infrastrutture di prodotto.

|| Tipo Componente        | Tecnologia   |  
|-|-----------------------  | -------------|
|1| Logica Applicativa BE  | springboot   |
|2| Logica Applicativa BE  | nodejs       |
|3| Logica Applicativa BE  | dotnet       |
|4| SPA                    | angular      |
|5| CDN                    | js-css-html  |
|6| Api Sincrone           | openapi3     |
|7| Code Request Esterna   | amq          |  
|8| Evento Esterno Pub     | amq          |
|9| Evento Esterno Sub     | amq          |
|10| Dati SQL               | oracle       |
|11| Dati SQL               | sqlserver    |
|12| Dati SQL               | db2luw       |
|13| Dati SQL               | postgresql   |
|14| Dati NoSQL             | mongodb      |

<br />
Facciamo un esempio. Se esiste in EA un prodotto censito come indoc a cui è stata associata una infrastruttura servizi stateless su OpenShift, il Dev potrà creare un modulo di prodotto di tipo microservizio che supponiamo voglia chiamare protocollo.
<br />
La toolchain in questo caso chiamerà quel microservizio indoc.protocollo. Poiché il modulo ha più componenti si avrà che ognuno di essi sarà identificato da:
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
