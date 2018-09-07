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


# Benutzerzugriff mit Identity and Access Management verwalten

Der {{site.data.keyword.DRA_full}}-Service delegiert die Zugriffssteuerung an die Toolchain, an die er gebunden ist. Ein Benutzer kann {{site.data.keyword.DRA_short}} für eine Toolchain in einer Cloud Foundry-Organisation oder in einer Ressourcengruppe verwewnden. 

Ein Benutzer kann {{site.data.keyword.DRA_short}} mit einer Toolchain in einer Cloud Foundry-Organisation verwenden, wenn er Mitglied dieser Organisation ist.

Ein Benutzer kann {{site.data.keyword.DRA_short}} mit einer Toolchain in einer Ressourcengruppe verwenden, wenn ihm eine Richtlinie von {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) zugewiesen ist, die ihm eine der Rollen 'Anzeigeberechtigter', 'Operator', 'Bearbeiter' oder 'Administrator' erteilt, und wenn diese Richtlinie für die Toolchain oder die Ressourcengruppe angewendet wird, zu der sie gehört.

Weitere Informationen zur Zugriffssteuerung für Toolchains in Ressourcengruppen finden Sie in [Zugriff auf Toolchains in Ressourcengruppen verwalten](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_resource_groups). Weitere Informationen zur Zugriffssteuerung für Toolchains in Cloud Foundry-Organisationen finden Sie in [Zugriff auf Toolchains in Cloud Foundry-Organisationen verwalten](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_orgs).
