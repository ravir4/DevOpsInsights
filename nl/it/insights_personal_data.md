---

copyright:
  years: 2018
lastupdated: "2018-8-2"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Gestione dei dati personali in DevOps Insights
{: insights_personal_data}

Puoi eliminare i dati personali che vengono raccolti e archiviati in {{site.data.keyword.DRA_full}}.
{: shortdesc}

I dati archiviati in {{site.data.keyword.DRA_short}} sono indicizzati in base all'ID toolchain. Quando elimini una toolchain, tutti i dati correlati ai repository che erano stati raccolti come parte della toolchain vengono eliminati.

IBM non gestisce i dati nel servizio {{site.data.keyword.DRA_short}}. Prima di lasciare il servizio {{site.data.keyword.DRA_short}}, devi eliminare i tuoi dati. Per eliminare i dati, elimina l'integrazione dello strumento {{site.data.keyword.DRA_short}} dalla tua toolchain. Se l'integrazione dello strumento {{site.data.keyword.DRA_short}} non viene aggiunta nuovamente alla toolchain entro sette giorni, i dati vengono eliminati.
{: tip}

## Eliminazione di dati da {{site.data.keyword.DRA_short}}
{: #insights_delete_data}

La seguente tabella elenca gli scenari per eliminare i dati da {{site.data.keyword.DRA_short}} e descrive in che modo si ripercuotono su ciascuna delle categorie di {{site.data.keyword.DRA_short}}.

|  | Sviluppatore e Team Insights | Rischio per le distribuzioni | Security Insights |
|---------|-------------|-------------|-------------|
| [Eliminazione di un repository ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window} |	Vengono eliminati tutti i dati correlati al repository.  | N/D | N/D |
| [Eliminazione dell'integrazione di uno strumento di {{site.data.keyword.DRA_short}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |	Vengono eliminati tutti i dati correlati al repository.  | Vengono eliminati tutti i dati associati alla toolchain di cui fa parte l'integrazione dello strumento. | Vengono eliminati tutti i dati correlati ai repository associati alla toolchain di cui fa parte l'integrazione dello strumento.  |
| [Eliminazione di una toolchain ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} | Vengono eliminati tutti i dati correlati ai repository associati alla toolchain. | Vengono eliminati tutti i dati associati alla toolchain.  | Vengono eliminati tutti i dati associati alla toolchain. |
| [Eliminazione di una pipeline ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window} | N/D | N/D | N/D |
{:caption="Tabella 1. Scenari di eliminazione dei dati" caption-side="top"}

## Eliminazione dell'integrazione di uno strumento di {{site.data.keyword.DRA_short}}
{: #insights_delete_integration}

Se elimini un'integrazione dello strumento dalla tua toolchain, l'operazione di eliminazione non può essere annullata.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina Panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **View Toolchain** e quindi su **Overview**.
1. Nella scheda per l'integrazione dello strumento di {{site.data.keyword.DRA_short}} che vuoi eliminare, fai clic sul menu per accedere alle opzioni di configurazione.
1. Per eliminare l'integrazione dello strumento dalla tua toolchain, fai clic su **Delete**.

  ![Menu Configurazione](images/delete_insights_integration.png)

1. Conferma facendo clic su **Delete**. 
