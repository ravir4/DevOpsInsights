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

# Domande frequenti (FAQ)
{: #faqs}

Questa pagina è un elenco aggiornato regolarmente delle domande frequenti su {{site.data.keyword.DRA_full}}.

## Come rimuovo i dati di cui {{site.data.keyword.DRA_short}} ha eseguito il mining da un repository?

Modifica i filtri dei dati del repository in modo che escluda i dati che vuoi rimuovere. 

Per modificare il filtro dei dati di {{site.data.keyword.DRA_short}}, fai clic su **Settings** e quindi su **Filters**. 

## Mancano alcuni dei miei problemi. Come li aggiungo?

Se il servizio di traccia dei problemi non fa parte della tua toolchain, aggiungilo. {{site.data.keyword.DRA_short}} esegue il mining solo dei servizi che fanno parte della toolchain. 

Se il servizio di traccia dei problemi fa parte della tua toolchain, controlla che le etichette di {{site.data.keyword.DRA_short}} siano associate alle etichette utilizzate dal tuo servizio. Fai clic su **Settings**, quindi su **Labels** e verifica quindi l'associazione.

Come ultima risorsa, rimuovi il servizio di traccia dei problemi dalla tua toolchain. Procedi quindi ad aggiungerlo nuovamente. {{site.data.keyword.DRA_short}} eseguirà il mining del servizio da zero. Il mining può richiedere qualche ora. 

## Come eseguo il remining di un repository?

Per eseguire il remining di un repository, elimina l'integrazione di {{site.data.keyword.DRA_short}} dalla tua toolchain. Procedi quindi ad aggiungerlo nuovamente.

## Come posso aggiungere un repository di cui eseguire il mining?

Aggiungilo a una toolchain facendo clic su **Add a tool** nella pagina della panoramica della toolchain. Dopo che il repository è parte della tua toolchain, Insights eseguirà nuovamente il mining dei tuoi dati per includere tale repository.

Seleziona la casella **Enable GitHub Issues** durante l'aggiunta di un repository per abilitare il mining dei problemi. 

## Perché non vedo alcuna build o distribuzione?

DevOps Insights esegue automaticamente il mining dei problemi e dei repository di codice che fanno parte di una toolchain, ma devi configurare la tua pipeline perché esegua il monitoraggio di build e distribuzioni. 

Assicurati innanzitutto di avere una pipeline Jenkins o Continuous Delivery nella tua toolchain. 

Verifica quindi che la tua pipeline sia configurata per il monitoraggio di build e distribuzione. Per informazioni su come configurare la tua pipeline, consulta la [documentazione di Continuous Delivery](risk_cd.html) o la [documentazione dell'integrazione Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
