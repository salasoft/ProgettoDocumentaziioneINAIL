
## 12. Dettaglio delle specifiche di integrazione della soluzione Product Infrastructure Management - PIM
<br />

## 12.1 Integrazione con il sistema di autenticazione/autorizzazione - OAuth2 / OIDC

La soluzione deve poter integrarsi, per gli aspetti di autenticazione e autorizzazione, adottando gli standard di riferimento OAuth2 / OIDCS <br />
(Rif: https://gitlab-os-lab.inail.it/DocPaaS/ApiGateway/tree/master/docs/Client)
<br />

## 12.2 Integrazione del microservizio di back-end con il sisgtema GitLab
[In progress]
<br/>

L'integrazione con il repository GitLab è ncessario per il recupero ed il prelievo del file di IStanza di Blueprint.
La composizione dei repository prevista segue una logica basata su alcune informazioni di prodotto.<br/>
Nello specifico è previsto un repository Git per il file di Istanza di Blueprint (configurazione.yaml) per ogni prodotto 
secondo la seguente regola di naming: *[prefisso-url-base]/[identificativo prodotto]/configurazione-prodotto.git* <br/>
Nel caso della soluzione PIM ci sarà quindi:<br/>
- un repository per il file di istanza blueprint per la componente di back-end: http://gitlab-os-lab.inail.it/[pim]/configurazione-prodotto.git
- un repository per il file di istanza blueprint per la componente di front-end: http://gitlab-os-lab.inail.it/[pimui]/configurazione-prodotto.git
<br/>

Al momento non sono ancora state stabilite regole formali sulle policy di branching e di naming, fare riferimento al branch master.

<br/>

## 12.3 Integrazione del microservizio di back-end con il sistema RTC (Rational Team Concert)

La modalità di integrazione prevista per l'importazione delle Istanze di Blueprint associate ad un asset dal sistema RTC è di tipo bidirezionale.

<br/>

Nel primo caso l'integrazione sarà ottenuta richiamando un'operazione di servizio rest esposta dal sistema RTC che da parte del microservizio di back-end della soluzione PIM. L'interfaccia definita per questa modalità di integrazione prevede quanto segue:

Input:
- l'identificativo del prodotto/asset RTC

Output:
- *idProdotto*: identificativo del prodotto
- *tipoProdotto*: tipologia del prodotto
- *nomeProdotto*: nome del prodotto
- *descrizioneProdotto*: descrizione del prodotto
- *dataCensimento*: data censimento su EA di RTC del prodotto

<br/>

Nel secondo caso l'integrazione sarà ottenuta in modalità inversa, il microservizio di back-end della soluzione PIM riceverà un evento di importazione blueprint da parte del tool di EA della Toolchain o da HUb previsto in architettura. In ogni caso l'interfaccia definita per questa modalità di integrazione prevede quanto segue:

Input:
- *idProdotto*: identificativo del prodotto
- *tipoProdotto*: tipologia del prodotto
- *nomeProdotto*: nome del prodotto
- *descrizioneProdotto*: descrizione del prodotto
- *dataCensimento*: data censimento su EA di RTC del prodotto

Output:
- *esito*: OK | KO
- *dettaglio*: messaggio errore in caso di KO

<br/>
