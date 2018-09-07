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

# Lernprogramm zur Einführung (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} wendet Analysen für Entwickler, Teams und die Bereitstellung auf Ihre wichtigsten DevOps-Projekte an. Mithilfe dieser Komponente können Sie ermitteln, wie konform Ihr Team mit DevOps und Entwicklerverfahren arbeitet. Außerdem ist sie ideal für das Risikomanagement Ihrer Codebasis und die automatische Durchsetzung von Qualitätsstandards in Continuous Delivery-Projekten. 
{:shortdesc}

{{site.data.keyword.DRA_short}} ist nur in der Region 'Vereinigte Staaten (Süden)' verfügbar.
{: tip}

Um {{site.data.keyword.DRA_short}} verwenden zu können, müssen Sie die Komponente zu einer Toolchain hinzufügen. Viele Toolchain-Vorlagen enthalten bereits {{site.data.keyword.DRA_short}}. [Sie müssen die Komponenten darüber hinaus zu Ihrer {{site.data.keyword.Bluemix_notm}}-Ressourcengruppe oder -Organisation als Service hinzufügen](/docs/services/reqnsi.html), damit Sie Informationen zu {{site.data.keyword.DRA_short}} anzeigen und über das {{site.data.keyword.Bluemix_notm}}-Dashboard auf einige der Toolchain-Vorlagen zugreifen können, die {{site.data.keyword.DRA_short}} enthalten.  

## Schritt 1: DevOps Insights zu einer Toolchain hinzufügen
{: #catalog}

{{site.data.keyword.DRA_short}} steht über eine Integration mit Toolchains von
{{site.data.keyword.contdelivery_full}} zur
Verfügung. Sie können {{site.data.keyword.DRA_short}} zu jeder Toolchain hinzufügen, indem Sie die Komponente aus dem Toolintegrationskatalog auswählen.

{{site.data.keyword.DRA_short}} ist in vielen Toolchain-Vorlagen enthalten. Wenn Sie eine Toolchain aus einer Vorlage erstellen, die {{site.data.keyword.DRA_short}} enthält, stellen Sie sicher, dass {{site.data.keyword.DRA_short}} auf **Erweitert** gesetzt ist. Erstellen Sie dann die Toolchain und fahren Sie mit [Schritt 2](/docs/services/DevOpsInsights/index.html#using) fort.
{: tip}

1. Klicken Sie auf **Tool hinzufügen**.

2. Klicken Sie auf **{{site.data.keyword.DRA_short}}**.

3. Klicken Sie auf **Integration erstellen**.

{{site.data.keyword.DRA_short}} ist nun auf der Übersichtsseite Ihrer Toolchain verfügbar. Das Repository und das Problemverfolgungssystem werden automatisch nach Daten durchsucht. 

## Schritt 2: Projektdaten erkunden
{: #using}

Wenn Ihre Toolchain GitHub, GitLab oder JIRA enthält, stellt Ihnen {{site.data.keyword.DRA_short}} automatisch nach einer anfänglichen Datenerfassung und -analyse Informationen zu Ihrer Codebasis und Ihrem Team bereit. Wenn Ihre Toolchain keine dieser Integrationen umfasst, fügen Sie eine dieser Integrationen hinzu.{: tip}

1. Klicken Sie auf der Übersichtsseite der Toolchain auf **{{site.data.keyword.DRA_short}}**.

2. Klicken Sie auf **Team** oder **Developer Insights** und wählen Sie dann eine Datenkategorie aus. 

3. Untersuchen Sie die Projektdaten, indem Sie die Dashboards in der Datenkategorie anzeigen. Wenn Sie mehr über ein Diagramm oder darüber wissen möchten, wie Sie die darin enthaltenen Informationen verarbeiten sollen, klicken Sie auf **Informationen** oder **Anweisungen**.

## Weitere Schritte
{: #next_steps}

Konfigurieren Sie nach der Durchsicht von Team und Developer Insights [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html), um Codequalität durchsetzen zu können. Deployment ist sowohl mit Delivery Pipeline for {{site.data.keyword.contdelivery_short}} als auch mit Jenkins kompatibel.
