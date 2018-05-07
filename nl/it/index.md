---

copyright:
  years: 2016, 2018
lastupdated: "2018-4-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a DevOps Insights (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} applica le analisi dello sviluppatore, del team e di distribuzione ai tuoi progetti DevOps più impegnati. Utilizzalo per imparare quanto il tuo team è conforme con le procedure DevOps e dello sviluppatore, per gestire il rischio nei tuoi codici di base e per applicare automaticamente gli standard di qualità nei progetti di fornitura continua.
{:shortdesc}

**Nota**: {{site.data.keyword.DRA_short}} è disponibile solo nella regione Stati Uniti Sud.

{{site.data.keyword.DRA_short}} comprende molti gruppi di funzionalità:

   * Developer Insights fornisce un modo completo di esplorare la maturità dello sviluppo del tuo progetto. Puoi identificare i file con alta tendenza all'errore e ottenere una vista di conformità del progetto per le procedure dello sviluppatore.

   * Team utilizza le analisi di social coding per aiutarti a capire come il tuo team collabora e come può funzionare in modo migliore.

   * Deployment Risk è come una rete di sicurezza per la fornitura continua. Analizza i risultati dagli strumenti di test di unità, di test funzionali, di scansioni di sicurezza e dell'applicazione e di copertura del codice nei gate specificati nel tuo processo di distribuzione e previene il rilascio di modifiche rischiose. Mostra i grafici delle tendenze nella copertura del codice, nelle build e nelle distribuzioni.

{{site.data.keyword.DRA_short}} è un'integrazione nel catalogo delle toolchain aperte Bluemix. Per ulteriori informazioni sulle toolchain, vedi [Gestione delle toolchain](/docs/services/ContinuousDelivery/toolchains_working.html).

Per utilizzare {{site.data.keyword.DRA_short}}, devi aggiungerlo a una toolchain. Molti template toolchain già includono {{site.data.keyword.DRA_short}}. Assicurati anche di [aggiungerlo alla tua organizzazione {{site.data.keyword.Bluemix_notm}} come un servizio](/docs/services/reqnsi.html) in modo da poter visualizzare le informazioni su {{site.data.keyword.DRA_short}} e accedere ad alcuni template toolchain che lo includono dal tuo dashboard {{site.data.keyword.Bluemix_notm}}.  

Inoltre, IBM esegue Developer Insights e Team su molti dei progetti open source più di successo in GitHub. Vai a [DevOpsInsights.io](http://devopsinsights.io/) per visualizzare i loro dati di sviluppo e team.

## Aggiunta di DevOps Insights a una toolchain
{: #catalog}

{{site.data.keyword.DRA_short}} è disponibile attraverso l'integrazione con le toolchain {{site.data.keyword.contdelivery_full}}. Puoi aggiungere {{site.data.keyword.DRA_short}} a qualsiasi toolchain selezionandolo dal catalogo di integrazione dello strumento.

{{site.data.keyword.DRA_short}} fa anche parte di molti template toolchain. Se crei una toolchain da un template che include {{site.data.keyword.DRA_short}}, assicurati che {{site.data.keyword.DRA_short}} sia impostato su **Advanced**. Quindi, crea la toolchain e passa a [Utilizzo di Insights](/docs/services/DevOpsInsights/index.html#using).

Per aggiungere {{site.data.keyword.DRA_short}} a una toolchain:

1. Fai clic su **Add a Tool**.

2. Fai clic su **{{site.data.keyword.DRA_short}}**.

3. Fai clic su **Create Integration**.

{{site.data.keyword.DRA_short}} è ora disponibile nella pagina della panoramica della tua toolchain. Il tuo sistema di traccia dei problemi e quello di repository vengono scansionati automaticamente per rilevare se sono presenti eventuali dati.

## Utilizzo di DevOps Insights
{: #using}

Se la tua toolchain include GitHub, GitLab o JIRA, {{site.data.keyword.DRA_short}} ti fornisce automaticamente le informazioni sul tuo codice di base e sul team dopo la raccolta e l'analisi di alcuni dati iniziali. Se la tua toolchain non include alcuna di queste integrazioni, aggiungine una e segui quindi questa procedura:

1. Dalla pagina della panoramica della tua toolchain, fai clic su **{{site.data.keyword.DRA_short}}**.

2. Fai clic su **Team ** or **Developer Insights** e scegli quindi una categoria di dati.

3. Esplora i dati del tuo progetto visualizzando i dashboard nella categoria dei dati. Se desideri avere ulteriori informazioni su un grafico o su cosa puoi fare con queste informazioni, fai clic su **Information** o **Guidance**.

Dopo che hai esplorato Team e Developer Insights, configura [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) per aiutarti a implementare la qualità del codice. Deployment Risk è compatibile con Delivery Pipeline per {{site.data.keyword.contdelivery_short}} e Jenkins.
