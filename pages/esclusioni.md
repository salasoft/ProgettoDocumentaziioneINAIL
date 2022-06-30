## 4. Esclusioni

FASE 1:

Di seguito sono rappresentate tutte le casistiche al momento previste per la compilazione delle istanze di blueprint architetturali.

Nella colonna In Scope sono indicate quelle a cui si deve fare riferimento per lo sviluppo delle funzionalità applicative.

|     |    Tipo Componente       |   Tecnologia    | Deploy Environemt     |  In Scope  |  Riferimento                   |
| --- |  ----------------------  |  -------------  | --------------------  |  --------  |  ----------------------------- |
|  1  |   Logica Applicativa     |   Spring-Boot   | openshift             |     SI     |                                | 
|  2  |   Logica Applicativa     |   NodeJS        | openshift             |     NO     |                                |           
|  3  |   Logica Applicativa     |   DotNet        | openshift             |     NO     |                                |
|  4  |   Logica Applicativa     |   Angular       | Apache                |     SI     |                                |
|  5  |   Api sincrone           |   OpenApi3      | apigateway            |     SI     |                                |
|  6  |   Code request           |   AMQ           | broker                |     SI     |                                | 
|  7  |   DatiSQL                |   Oracle        | sql                   |     NO     |                                | 
|  8  |   DatiSQL                |   SQL Serve     | sql                   |     NO     |                                | 
|  9  |   DatiSQL                |   DB2 Luw       | sql                   |     NO     |                                | 
|  10 |   DatiSQL                |   Postgresql    | sql                   |     NO     |                                | 
|  11 |   DatiNoSQL              |   MongoDB       | nosql                 |     NO     |                                | 


***
FASE 2:

Di seguito sono rappresentate tutte le casistiche aggiornate in relazione alla nuova fase: 

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