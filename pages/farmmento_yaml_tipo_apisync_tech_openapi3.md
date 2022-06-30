### 9.8 Frammento YAML di configurazione componente - Tipologia: Api Sincrona - Tecnologia: OpenApi3

Al momento della stesura di questa documentazione sono state identificate una serie di informazioni di seguito descritte in tabella (Tabella 1). 
Tali informazioni sono corredate da una ipotesi di struttura del frammento yaml contenente i tag delle informazioni previste per la sezione di *runtime environment* 
afferente alla Tipologia: *Tipologia: Api Sincorne - Tecnologia: OpenApi3* prevista per i template delle blueprint architetturali.

<br />

| Tag yaml              |Descrizione                                                          | Obbligatorio | Valori Possibili     |
|-----------------------|---------------------------------------------------------------------|--------------|----------------------|
| clusterName           |  nome del cluster                                                   |       X      |                      |
| clusterURL            |  url del cluster                                                    |       X      |                      |
| publicURL             |  ulr pubblica dell'api                                              |       X      |                      |
| gruppo                |  stringa per il nome del gruppo di appartenenza                     |       X      |                      |
| categoria             |  stringa per il nome della categoria di appartenenza                |       X      |                      |


<br />
<br />

Di seguito un'ipotesi di struttura su file yaml dei tag attaulmente identificati e candidati per la sezione di *runtime environment* dal template di blueprint.  

<br />


<pre>

            cluster: ClusterCI
            cluster_url: https://ciportale.inail.it
            $compid.nome: ab123
            $compid.descrizione: Componente API del microservizio del prodotto PIM
            $compid.apig.url_pub: https://collportale.inail.it/api/pim.protocollo.api.gestinfra-api/protocollo/gestinfra-api
            $compid.pdd.url_pub: https://spc.test.inail.it/pdd/api-id_auth_channel_02/2.pim.gestinfra-api.pimui
            $compid.apim.url_pub: https://apicoll.inailcloud.it/irestgw/pim.gestinfra-api.pimui
            $compid.categoria: pim


</pre>


Di seguito la struttura su file yaml per la sezione di *runtime environment* dal template di blueprint generata per tutti gli ambienti previsti. 
(ci = continuous integration alias integrazione, coll = collaudo, cert = certificazione, prod = produzione) 

<br />


<pre>
    runtimeEnvironment:
        ci:
              clusterName:
              clusterURL:
              publicURL:
              gruppo:
              categoria:
        coll:
              clusterName:
              clusterURL:
              publicURL:
              gruppo:
              categoria:
        cert:
              clusterName:
              clusterURL:
              publicURL:
              gruppo:
              categoria:
        prod:
              clusterName:
              clusterURL:
              publicURL:
              gruppo:
              categoria:

</pre>

<br />
<br />