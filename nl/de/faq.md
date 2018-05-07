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

# Häufig gestellte Fragen
{: #faqs}

Diese Seite enthält eine in kurzen Abständen aktualisierte Liste häufig gestellter Fragen zu {{site.data.keyword.DRA_full}}.

## Wie entferne ich Daten, die {{site.data.keyword.DRA_short}} mithilfe einer Mining-Operation aus einem Repository gefiltert hat?

Ändern Sie den Datenfilter des Repositorys so, dass er die zu entfernenden Daten ausschließt. 

Klicken Sie zum Ändern des {{site.data.keyword.DRA_short}}-Datenfilters auf **Einstellungen** und dann auf **Filter**. 

## Einige Probleme werden nicht aufgeführt. Wie kann ich sie hinzufügen?

Falls der Problemverfolgungsservice nicht Teil Ihrer Toolchain ist, fügen Sie ihn hinzu. {{site.data.keyword.DRA_short}} filtert Daten per Mining nur aus den Services, die Teil der Toolchain sind. 

Falls der Problemverfolgungsservice Teil Ihrer Toolchain ist, stellen Sie sicher, dass die {{site.data.keyword.DRA_short}}-Bezeichnungen den vom Service verwendeten Bezeichnungen zugeordnet sind. Klicken Sie auf **Einstellungen** und dann auf **Bezeichnungen** und verifizieren Sie anschließend die Zuordnung.

Schließlich können Sie noch den Problemverfolgungsservice von der Toolchain entfernen. Fügen Sie ihn anschließend wieder hinzu. {{site.data.keyword.DRA_short}} startet das Mining des Servcie von Anfang an. Das Mining kann einige Stunden in Anspruch nehmen. 

## Wie wird ein erneutes Mining für ein Repository durchgeführt?

Für ein erneutes Mining eines Repositorys löschen Sie die {{site.data.keyword.DRA_short}}-Integration aus der Toolchain. Fügen Sie sie anschließend wieder hinzu.

## Wie kann ich ein Repository für das Mining hinzufügen?

Fügen Sie das Repository zu einer Toolchain hinzu, indem Sie auf der Übersichtsseite der Toolchain auf **Tool hinzufügen** klicken. Nachdem das Repository zur Toolchain hinzugefügt wurde, führt Insights ein erneutes Mining der Daten unter Einbeziehung dieses Repositorys durch.

Wählen Sie beim Hinzufügen eines Repositorys das Feld **GitHub-Probleme aktivieren** aus, um das Mining von Problemen zu aktivieren. 

## Warum werden keine Builds oder Bereitstellungen angezeigt?

DevOps Insights führt automatisch Mining für Code-Repositorys und Probleme durch, die Teil einer Toolchain sind; für die Überwachung von Builds und Bereitstellungen müssen Sie die Pipeline jedoch konfigurieren. 

Stellen Sie zuerst sicher, dass eine Continuous Delivery- oder Jenkins-Pipeline in der Toolchain vorhanden ist. 

Vergewissern Sie sich dann, dass die Pipeline für die Überwachung von Builds und Bereitstellungen konfiguriert ist. Informationen zum Konfigurieren der Pipeline finden Sie in der [Continuous Delivery-Integrationsdokumentation](risk_cd.html) bzw. der [Jenkins-Integrationsdokumentation](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
