### 9.7 Frammento YAML di configurazione componente - Tipologia: UI Applicativa - Tecnologia: Angular

Al momento della stesura di questa documentazione sono state identificate una serie di informazioni di seguito descritte in tabella (Tabella 1). 
Tali informazioni sono corredate da una ipotesi di struttura del frammento yaml contenente i tag delle informazioni previste per la sezione di *runtime environment* 
afferente alla Tipologia: *Tipologia: UI Applicativa - Tecnologia: Angular* prevista per i template delle blueprint architetturali.

<br />

| Tag yaml 	| Descrizione                                                                                          	| Obbligatorio 	| Valori possibili 	|
|----------	|------------------------------------------------------------------------------------------------------	|--------------	|------------------	|
| nomeSPA  	| Nome della Single Page Application                                                                   	| x            	| [ID prodotto]    	|
| Contesto 	| Il contesto è la parte dell'url da concatenare a fqdn. Es. https://ciportale.inail.it/app/[contesto] 	| x            	| [ID prodotto]    	|

<br />
<br />

Di seguito un'ipotesi di struttura su file yaml dei tag attaulmente identificati e candidati per la sezione di *runtime environment* dal template di blueprint.  

<br />


<pre>

       runtimeEnvironment: 
                     nomeSPA:
                     contesto:


</pre>


Di seguito la struttura su file yaml per la sezione di *runtime environment* dal template di blueprint generata per tutti gli ambienti previsti. 
(ci = continuous integration alias integrazione, coll = collaudo, cert = certificazione, prod = produzione) 

<br />


<pre>
    runtimeEnvironment:
        ci:
              nomeSPA:
              contesto:
        coll:
              nomeSPA:
              contesto:
        cert:
              nomeSPA:
              contesto:
        prod:
              nomeSPA:
              contesto:

</pre>



<br />
<br />


