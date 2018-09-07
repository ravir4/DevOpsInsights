---

copyright:
  years:  2018
lastupdated: "2018-7-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Gestione dell'accesso utente con Identity and Access Management

Il servizio {{site.data.keyword.DRA_full}} delega il controllo dell'accesso alla toolchain a cui è associato. Un utente può utilizzare {{site.data.keyword.DRA_short}} per una toolchain in un'organizzazione Cloud Foundry o in un gruppo di risorse. 

Un utente può utilizzare {{site.data.keyword.DRA_short}} con una toolchain in un'organizzazione Cloud Foundry se è membro di tale organizzazione.

Un utente può utilizzare {{site.data.keyword.DRA_short}} con una toolchain in un gruppo di risorse se viene assegnata una politica di {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) che concede i ruoli di Visualizzatore, Operatore, Editor o Amministratore e tale politica viene applicata alla toolchain o al gruppo di risorse di cui fa parte.

Per ulteriori informazioni sul controllo dell'accesso per le toolchain nei gruppi di risorse, vedi [Gestione dell'accesso alle toolchain nei gruppi di risorse](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_resource_groups). Per ulteriori informazioni sul controllo dell'accesso per le toolchain nelle organizzazioni Cloud Foundry, vedi [Gestione dell'accesso alle toolchain nelle organizzazioni Cloud Foundry](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_orgs).
