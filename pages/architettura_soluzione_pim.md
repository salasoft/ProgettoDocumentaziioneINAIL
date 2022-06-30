### 8.1. Architettura dalle soluzione

Partendo dall’architettura logica è stata definita e particolareggiata la relativa architettura applicativa rappresentata per componenti nella Figura 2.

La soluzione sarà costituita da due tipologie di prodotti: front-end e back-end e farà riferimento alle relative tipologie di infrastrutture architetturali previste:


| Nome Prodotto                                | Id Prodotto      | Tipo Modulo     | Nome Modulo      | Tipo Componente | Nome Componente  
| -------------------------------------------- | ---------------- | --------------- | ---------------- | --------------- | ---------------- 
|  Portale Gestione Infrastruttura di prodotto |  pimui           | Client          | gestinfra-ui     | spa             | pim-ui           
|  Gestione Infrastruttura di prodotto         |  pim             | Servizio        | gestinfra        | ms              | gestinfra-app    
|  Gestione Infrastruttura di prodotto         |  pim             | Servizio        | gestinfra        | api             | gestinfra-api    
|  Gestione Infrastruttura di prodotto         |  pim             | Servizio        | gestinfra        | sql             | gestinfra-sql    

