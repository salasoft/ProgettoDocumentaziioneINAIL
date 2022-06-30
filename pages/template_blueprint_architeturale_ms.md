
### 9.3. Template Blueprint Architetturale Microservizio

Di seguito è riportato il template di Blueprint Architetturale identificato per la componente di back-end.

-   Tipo Prodotto: back-end
-   Tipologia Blueprint Architetturale: servizi stateless su OpenShift [file template](files/template_blueprint_servizi_ocp.yml)


<pre>
nome     : servizi stateless su OpenShift
versione : 1.0
prodotto : back-end
data     : 2021-02-25
stato    : attiva
- tipoModulo: Interfaccia
         min: 1
         max: 1
    - tipoComponente: OpenAPI3
                 min: 1
                 max: N
   deployEnvironment: apigateway
- tipoModulo: Servizio
         min: 1
         max: N
    - tipoComponente: Logica applicativa
                 min: 1
                 max: 1
          tecnologia: spring-boot | nodejs | dotnet | python
   deployEnvironment: openshift
    - tipoComponente: DatiSQL
                 min: 0
                 max: 1
          tecnologia: oracle | db2luv | sqlserver
   deployEnvironment: sql
    - tipoComponente: DatiNoSQL
                 min: 0
                 max: 1
          tecnologia: mongodb
   deployEnvironment: nosql
    - tipoComponente: Coda request interna
                 min: 0
                 max: N
   deployEnvironment: internal broker
    - tipoComponente: Coda request esterna
                 min: 0
                 max: N
   deployEnvironment: broker
    - tipoComponente: Evento interno
                 min: 0
                 max: N
   deployEnvironment: internal broker
    - tipoComponente: Evento esterno
                 min: 0
                 max: N
   deployEnvironment: broker
- tipoModulo: Libreria
         min: 0
         max: 1
    - tipoComponente: Logica applicativa
                 min: 1
                 max: N
          tecnologia: Java
- tipoModulo: Componente a catalogo interno al prodotto
         min: 0
         max: 1
    - tipoComponente: internal cache
                 min: 0
                 max: N
        voceCatalogo: Redis
   deployEnvironment: openshift
    - tipoComponente: internal broker
                 min: 0
                 max: 1
        voceCatalogo: AMQ
   deployEnvironment: openshift
</pre>
