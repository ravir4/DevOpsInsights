---

copyright:
  years: 2016, 2018
lastupdated: "2018-3-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni su Deployment Risk

{{site.data.keyword.DRA_short}} Deployment Risk fornisce un gran numero di informazioni sulle tue distribuzioni, particolarmente a rischio. Puoi utilizzarlo per automatizzare la protezione della qualità nella tua delivery pipeline utilizzando politiche e gate. Fornisce i dati su frequenza di distribuzione e build, insieme alle tendenze di test e copertura del codice.
{:shortdesc}

Dopo aver aperto {{site.data.keyword.DRA_short}} dalla tua toolchain, fai clic su **Deployment Risk**. Da lì, puoi selezionare una categoria analitica per un approfondimento di quanto sta accadendo con le tue distribuzioni.  

Puoi utilizzare Deployment Risk per applicare gli standard di qualità nella tua toolchain tramite politiche e gate. Le politiche comprendono le serie di regole; i gate applicano le politiche. Ad esempio, potresti creare una politica "Unit Testing and Test Coverage" che richiede che le le build rispettino gli standard di verifica dell'unità e di copertura del test. Successivamente aggiungi un gate che fa riferimento alla politica al tuo processo di fornitura continua. Le build che non soddisfano la politica vengono arrestate da questo gate. 

## Analisi dei rischi

Con l'analisi dei rischi, ottieni una panoramica dei rischi associati alle applicazioni nei tuoi ambienti di preparazione e produzione. Puoi eseguire il drill-down per comprendere la copertura del codice, le prestazioni del test e i report di sicurezza. I dashboard sono automaticamente popolati con le informazioni più recenti dai test {{site.data.keyword.DRA_short}} della tua pipeline.

## Frequenza distribuzione

Puoi visualizzare le tendenze delle frequenze di distribuzione per i tuoi ambienti di produzione, preparazione o di altro tipo. Questa vista mostra anche, per le distribuzioni, se sono riuscite e se non sono riuscite. Puoi fare clic su una specifica distribuzione per visualizzarne i dettagli. Se fai parte di un team dinamico, dovresti vedere una tendenza della frequenza di distribuzione in crescita nel tempo. 

## Frequenza di build

Puoi visualizzare le tendenze delle frequenze di build per i tuoi rami a lunga esecuzione. Questa vista mostra anche, per le build, se sono riuscite e se non sono riuscite. Puoi fare clic su un punto di interesse e visualizzare i dettagli della build. Se fai parte di un team dinamico, vuoi vedere molte build giornaliere sul ramo di integrazione. Altrimenti, il tuo team non sta unendo il suo codice frequentemente.

## Tendenza dei test di unità

Puoi visualizzare le tendenze per i test di unità per le build che provengono da uno specifico ramo o che sono distribuite a uno specifico ambiente. Ad esempio, puoi vedere le tendenze dei test per le build dal ramo master. Se qualche test non riesce per le build che sono andate in produzione, sarebbe opportuno un tuo intervento. Inoltre, se il numero di test si sta riducendo nel tempo, la cosa potrebbe essere un motivo di preoccupazione.

## Tendenze dei test di verifica funzionale

Puoi visualizzare le tendenze per i test di verifica funzionale per le build che provengono da uno specifico ramo o che sono distribuite a uno specifico ambiente. Ad esempio, puoi vedere le tendenze dei test per le build dal ramo master. Se qualche test non riesce per le build che sono andate in produzione, sarebbe opportuno un tuo intervento. Inoltre, se il numero di test si sta riducendo nel tempo, la cosa potrebbe essere un motivo di preoccupazione.

## Tendenze della copertura del codice

Puoi visualizzare le tendenze della copertura del codice per le build distribuite a uno specifico ambiente. Ad esempio, puoi visualizzare le tendenze della copertura del codice per le build che sono andate in produzione. Idealmente, dovresti vedere che la copertura del codice aumenta nel tempo per le build che vanno in produzione. Se la copertura del codice sta diminuendo, sarebbe opportuno un tuo intervento.

## Politiche

Le politiche sono serie di regole che controllano i gate nella tua delivery pipeline. Se il tuo codice non soddisfa o supera una politica approvata in un gate particolare, la distribuzione viene arrestata per prevenire che vengano rilasciati dei rischi.


## Prerequisiti
{: #prerequisites}

Deployment Risk richiede alcune configurazioni oltre a quelle descritte in [Introduzione a {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Per utilizzare Deployment Risk, hai bisogno di due cose:

* Una istanza di {{site.data.keyword.deliverypipeline}} o un progetto Jenkins
* I test che desideri utilizzare per valutare il tuo progetto

## Informazioni sull'integrazione

Deployment Risk si integra con {{site.data.keyword.deliverypipeline}}, che è parte di {{site.data.keyword.contdelivery_full}} e con i progetti Jenkins. Ad alto livello, le istruzioni per l'utilizzo di entrambi sono simili.  

Se si sta utilizzando {{site.data.keyword.deliverypipeline}}, procedi come segue:

1. [Crea le politiche e le regole](risk_policies.html) per {{site.data.keyword.DRA_short}} da gestire.
2. [Prepara le fasi della tua pipeline](risk_cd.html) per l'integrazione con {{site.data.keyword.DRA_short}}.
3. [Crea o modifica i lavori di verifica](risk_cd.html) nella pipeline che carica i risultati in {{site.data.keyword.DRA_short}}.
4. [Aggiungi i gate](risk_cd.html) alla pipeline che effettua le decisioni di promozione basate su quei risultati e sulle tue politiche.
5. Esegui la pipeline e [visualizza i risultati](results.html).

Se stai utilizzando Jenkins, segui questa procedura:

1. [Crea le politiche e le regole](risk_policies.html) per {{site.data.keyword.DRA_short}} da gestire.
2. [Installa e configura il plugin Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
3. [Crea i gate e i lavori di verifica come descritto nelle istruzioni del plugin](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin). I test caricano i risultati in {{site.data.keyword.DRA_short}} per le analisi e i gate utilizzano questi risultati per effettuare decisioni di promozione.
4. Esegui il progetto e [visualizza i risultati](results.html). 

Non importa come crei e distribuisci il tuo codice, i risultati sono gli stessi: le build che soddisfano gli standard saranno spostate oltre i gate Deployment Risk, mentre quelle che non li soddisfano saranno arrestate. 
