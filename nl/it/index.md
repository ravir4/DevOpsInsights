---

copyright:
  years: 2016, 2018
lastupdated: "2018-8-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Esercitazione introduttiva (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} applica le analisi dello sviluppatore, del team e di distribuzione ai tuoi progetti DevOps più impegnati. Utilizzalo per imparare quanto il tuo team è conforme con le procedure DevOps e dello sviluppatore, per gestire il rischio nei tuoi codici di base e per applicare automaticamente gli standard di qualità nei progetti di fornitura continua. 
{:shortdesc}

{{site.data.keyword.DRA_short}} è disponibile solo nella regione Stati Uniti Sud.
{: tip}

Per utilizzare {{site.data.keyword.DRA_short}}, devi aggiungerlo a una toolchain. Molti template toolchain già includono {{site.data.keyword.DRA_short}}. Assicurati anche di [aggiungerlo al tuo gruppo di risorse o alla tua organizzazione {{site.data.keyword.Bluemix_notm}} come un servizio](/docs/services/reqnsi.html) in modo da poter visualizzare le informazioni su {{site.data.keyword.DRA_short}} e accedere ad alcuni template toolchain che lo includono dal tuo dashboard {{site.data.keyword.Bluemix_notm}}.  

## Passo 1: aggiungi DevOps Insights a una toolchain
{: #catalog}

{{site.data.keyword.DRA_short}} è disponibile attraverso l'integrazione con le toolchain {{site.data.keyword.contdelivery_full}}. Puoi aggiungere {{site.data.keyword.DRA_short}} a qualsiasi toolchain selezionandolo dal catalogo di integrazione dello strumento.

{{site.data.keyword.DRA_short}} fa parte di molti template toolchain. Se crei una toolchain da un template che include {{site.data.keyword.DRA_short}}, assicurati che {{site.data.keyword.DRA_short}} sia impostato su **Advanced**. Quindi, crea la toolchain e vai al [Passo 2](/docs/services/DevOpsInsights/index.html#using).
{: tip}

1. Fai clic su **Add a Tool**.

2. Fai clic su **{{site.data.keyword.DRA_short}}**.

3. Fai clic su **Create Integration**.

{{site.data.keyword.DRA_short}} è ora disponibile nella pagina della panoramica della tua toolchain. Il tuo sistema di traccia dei problemi e quello di repository vengono scansionati automaticamente per rilevare se sono presenti eventuali dati. 

## Passo 2: esplora i dati del tuo progetto
{: #using}

Se la tua toolchain include GitHub, GitLab o JIRA, {{site.data.keyword.DRA_short}} ti fornisce automaticamente le informazioni sul tuo codice di base e sul team dopo la raccolta e l'analisi di alcuni dati iniziali. Se la tua toolchain non include alcuna di queste integrazioni, aggiungine una.
{: tip}

1. Dalla pagina della panoramica della tua toolchain, fai clic su **{{site.data.keyword.DRA_short}}**.

2. Fai clic su **Team ** or **Developer Insights** e scegli quindi una categoria di dati. 

3. Esplora i dati del tuo progetto visualizzando i dashboard nella categoria dei dati. Se desideri avere ulteriori informazioni su un grafico o su cosa puoi fare con queste informazioni, fai clic su **Information** o **Guidance**.

## Passi successivi
{: #next_steps}

Dopo che hai esplorato Team e Developer Insights, configura [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) per aiutarti a implementare la qualità del codice. Deployment Risk è compatibile con Delivery Pipeline per {{site.data.keyword.contdelivery_short}} e Jenkins.
