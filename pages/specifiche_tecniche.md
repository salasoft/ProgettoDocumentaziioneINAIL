
## 7. Specifiche tecniche e tecnologie

- La soluzione deve poter essere disponibile in ambiente Openshift, con riferimento alla sola componente di back-end (microservizio).

  - Il microservizio sarà implementato con tecnologia Java 1.8 - SpringBoot Versione 2.4.5.

  - Il componente client di front-end sarà implementato con tecnologia Angular Versione 8.2.x.

  - Il componente database sarà implementato con tecnologia Oracle 18c.

- La soluzione deve poter integrarsi, per gli aspetti di gestione del versioning dei file yaml delle istanze di blueprint architetturali, con il SCM GitLab dell’Istituto. [(Specifiche di integrazione)](specifiche_integrazione.md)


- La soluzione deve poter integrarsi, per gli aspetti di autenticazione e autorizzazione, adottando gli standard di riferimento OAuth2 / OIDCS [(Specifiche di integrazione)](specifiche_integrazione.md) 


- La soluzione deve poter integrarsi con il sistema EA (Enterpise Architecture) di RTC (Rational Team Concert) per la ricezione delle informazioni relative agli eventi di censimento asset sull'applicazione di Enterprise Architecture, così come previsto dal nuovo processo. [(Specifiche di integrazione)](specifiche_integrazione.md)
    