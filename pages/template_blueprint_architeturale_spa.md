
### 9.1. Template Blueprint Architetturale Single Page Application

Di seguito è riportato il template di Blueprint Architetturale identificato per la componente di front-end.

-   Tipo Prodotto: front-end
-   Template Tipologia Blueprint Architetturale: spa monolitica [file template](files/template_blueprint_spa_monolitica.yml)

<pre>
nome     : spa monolitica
versione : 1.0
prodotto : front-end
data     : 2021-02-25
stato    : attiva
- tipoModulo: Client
         min: 1
         max: 1
    - tipoComponente: Logica applicativa
                 min: 1
                 max: 1
          tecnologia: angular | react
   deployEnvironment: apache-spa
    - tipoComponente: Risorse statiche
                 min: 1
                 max: 1
          tecnologia: css-html
   deployEnvironment: apache-cdn
- tipoModulo: Libreria
         min: 0
         max: 1
    - tipoComponente: Logica applicativa
                 min: 1
                 max: N
          tecnologia: JavaScript
</pre>

