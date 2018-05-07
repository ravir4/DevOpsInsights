---

copyright:
  years: 2018
lastupdated: "2018-4-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Persönliche Daten in DevOps Insights verwalten
{: insights_personal_data}

Sie können persönliche Daten, die in {{site.data.keyword.DRA_full}} erfasst und gespeichert werden, löschen.
{: shortdesc}

Daten, die in {{site.data.keyword.DRA_short}} gespeichert werden, werden anhand der Toolchain-ID indexiert. Wenn Sie eine Toolchain löschen, werden alle Daten im Zusammenhang mit Repositorys, die als Teil der Toolchain erfasst wurden, gelöscht. 

## Daten aus {{site.data.keyword.DRA_short}} löschen
{: #insights_delete_data}

In der folgenden Tabelle sind Szenarios für das Löschen von Daten aus {{site.data.keyword.DRA_short}} und Beschreibungen der Auswirkungen auf die jeweiligen {{site.data.keyword.DRA_short}}-Kategorien aufgeführt.

|  | Developer und Team Insights | Deployment Risk | Security Insights |
|---------|-------------|-------------|-------------|
| [Repository löschen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window} |	Alle zum betreffenden Repository gehörenden Daten werden gelöscht.  | Nicht zutreffend| Nicht zutreffend|
| [{{site.data.keyword.DRA_short}}-Toolintegration löschen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |	Alle zum betreffenen Repository gehörenden Daten werden gelöscht.  | Alle Daten, die der Toolchain zugeordnet sind, von der die Toolintegration ein Teil ist, werden gelöscht. | Alle Daten, die zu Repositorys gehören, die der Toolchain zugeordnet sind, von der die Toolintegration ein Teil ist, werden gelöscht. |
| [Toolchain löschen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} | Alle Daten, die zu Repositorys gehören, die der Toolchain zugeordnet sind, werden gelöscht. | Alle Daten, die der Toolchain zugeordnet sind, werden gelöscht. | Alle Daten, die der Toolchain zugeordnet sind, werden gelöscht. |
| [Pipeline löschen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window} | Nicht zutreffend| Nicht zutreffend| Nicht zutreffend|
{:caption="Tabelle 1. Szenarios für das Löschen von Daten" caption-side="top"}

## {{site.data.keyword.DRA_short}}-Toolintegration löschen
{: #insights_delete_integration}

Wenn Sie eine Toolintegration aus der Toolchain löschen, kann der Löschvorgang nicht rückgängig gemacht werden.

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf eine Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ dazu können Sie auch auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und anschließend auf **Übersicht** klicken.
1. Klicken Sie auf der Karte für die {{site.data.keyword.DRA_short}}-Toolintegration, die gelöscht werden soll, auf das Menü für den Zugriff auf die Konfigurationsoptionen.
1. Klicken Sie zum Löschen der Toolintegration aus der Toolchain auf **Löschen**.

  ![Konfigurationsmenü](images/delete_insights_integration.png)

1. Bestätigen Sie die Aktion, indem Sie auf **Löschen** klicken. 
