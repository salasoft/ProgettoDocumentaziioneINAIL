
### 9.1. Template Blueprint Architetturale Single Page Application

Di seguito è riportato il template di Blueprint Architetturale identificato per la componente di front-end.

-   Tipo Prodotto: front-end
-   Template Tipologia Blueprint Architetturale: spa monolitica [file template](files/template_blueprint_spa_monolitica_nuova_versione.yml)

<pre>
nome     : "Spa monolitica"
id       : "spa-monolitica"
versione : "1.0"
prodotto : "front-end"
data     : "2021-02-25"
stato    : "attiva"
moduli:
- tipoModulo: "Client"
         min: "1"
         max: "1"
         esposizione: "Intranet | Internet | SOL"
         componenti:
             - tipoComponente: "Spa"
                 min: "1"
                 max: "1"
                 layer: "FE"
                 tecnologia: "angular | react"
                 deployEnvironment: "apache-spa"
             - tipoComponente: "CDN"
                 min: "1"
                 max: "1"
                 tecnologia: "js-css-html"
                 layer: "FE"
                 deployEnvironment: "apache-cdn"
             - tipoComponente: "Client APIG"
                 min: "1"
                 max: "1"
                 tecnologia: "json"
                 layer: "mediation"
                 deployEnvironment: "APIGateway"

</pre>

