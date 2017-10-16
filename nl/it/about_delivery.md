---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Informazioni su Delivery Insights
{: #about_delivery}

Delivery Insights, una parte di {{site.data.keyword.DRA_short}}, mostra le metriche, le statistiche di distribuzione e altre informazioni sulla tua installazione di IBM UrbanCode Deploy. Ad esempio, può mostrare i grafici della durata della distribuzione, degli esiti positivi e negativi, tutti elencati per ambienti raggruppati logicamente.
{:shortdesc}

Delivery Insights richiede un'installazione di DevOps Connect. Per le informazioni di configurazione, consulta [Visualizzazione dei dati dai server IBM UrbanCode Deploy](uc_insights_connect_ucd.html).

![Due grafici dai dati demo di UrbanCode Insights](images/uc_insights_demo_data.gif)

Alcune delle informazioni che puoi visualizzare in Delivery Insights includono:

- Le statistiche sulla distribuzione, che includono la durata e il volume della distribuzione nel tempo.
- Le statistiche sulla frequenza di errore della distribuzione per applicazione e ambiente.
- Le statistiche sulla distribuzione del componente, incluse la frequenza di errore, l'ora di distribuzione e la durata.

## Panoramica dei sistemi
{: #systems_overview}

La topologia per Delivery Insights include una o più installazioni in loco di IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> e il programma di utilità DevOps Connect.

Il seguente diagramma mostra un'installazione tipica di questi sistemi.

![Topologia di panoramica per UrbanCode Insights, che include i sistemi installati in loco del cliente e i servizi IBM Cloud](images/uc_insights_overview_topology_multi_ucd.png)

- Un'installazione di **IBM UrbanCode Deploy** fornisce le informazioni sulle distribuzioni con esito positivo e negativo per le metriche. IBM UrbanCode Deploy richiede una patch per comunicare con IBM Bluemix DevOps Connect.

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect**, in precedenza noto come programma di utilità IBM UrbanCode Sync, coordina la comunicazione tra le installazioni in loco di IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> e i servizi ospitati da IBM come UrbanCode Insights. DevOps Connect utilizza la comunicazione HTTPS sicura ai server in loco e l'autenticazione token per fornire i dati a UrbanCode Insights.

  DevOps Connect richiede dei plugin per il collegamento ad altri sistemi nella topologia.

- **Delivery Insights**, parte di {{site.data.keyword.DRA_short}}, fornisce le metriche sull'attività di distribuzione su IBM UrbanCode Deploy, inclusi i tempi di distribuzione e le frequenze di errore in base ai gruppi di ambienti. L'autorizzazione viene controllata dagli account {{site.data.keyword.Bluemix}}.
