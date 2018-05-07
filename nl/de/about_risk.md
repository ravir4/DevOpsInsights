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

# Informationen zu Deployment Risk

{{site.data.keyword.DRA_short}} Deployment Risk stellt eine Fülle von Informationen zu Ihren Bereitstellungen, insbesondere zu Risiken, bereit. Mit dieser Komponente können Sie den Qualitätsschutz in Ihrer Delivery Pipeline mithilfe von Richtlinien und Gates automatisieren. Es werden Daten zur Build- und Bereitstellungshäufigkeit sowie Daten zur Codeabdeckung und Testtrends bereitgestellt.
{:shortdesc}

Klicken Sie nach dem Öffnen von {{site.data.keyword.DRA_short}} über die Toolchain auf **Bereitstellungsrisiko**. Von hier aus können Sie eine Analysekategorie auswählen, um einen tieferen Einblick in Ihre Bereitstellungen zu erhalten.  

Mit Deployment Risk können Sie Qualitätsstandards in Ihrer Toolchain mithilfe von Richtlinien und Gates durchsetzen. Richtlinien umfassen Regeln; Gates setzen Richtlinien um. Sie können beispielsweise eine Richtlinie "Komponententest und Testumfang" erstellen, die verlangt, dass Builds Standards für Komponententests und Testumfang einhalten. Sie fügen dann ein Gate hinzu, das die Richtlinie zu Ihrem Continuous Delivery-Prozess referenziert. Builds, die nicht der Richtlinie entsprechen, werden am Gate gestoppt. 

## Risikoanalyse

Mit der Risikoanalyse erhalten Sie einen Überblick über die Risiken im Zusammenhang mit Anwendungen in den Staging- und Produktionsumgebungen. Mithilfe von Drilldowns können Sie sich Einblicke in die Codeabdeckung, die Testleistung und Sicherheitsberichte verschaffen. Die Dashboards werden automatisch mit den aktuellen Informationen aus den {{site.data.keyword.DRA_short}}-Tests der Pipelines gefüllt.

## Bereitstellungshäufigkeit

Sie können Trends zur Bereitstellungshäufigkeit für Produktions-, Staging- oder andere Umgebungen anzeigen. Darüber hinaus sind in dieser Ansicht erfolgreiche und fehlgeschlagene Bereitstellungen aufgeführt. Sie können auf eine bestimmte Bereitstellung klicken, um Details dazu anzuzeigen. Wenn Sie in einem agilen Team arbeiten, können Sie den ansteigenden Trend der Bereitstellungshäufigkeit über einen bestimmten Zeitraum hinweg beobachten. 

## Buildhäufigkeit

Sie können Trends für die Buildhäufigkeit für Zweige mit langer Laufzeit anzeigen. Darüber hinaus sind in dieser Ansicht erfolgreiche und fehlgeschlagene Builds aufgeführt. Sie können auf einen Punkt klicken, der für Sie von Interesse ist, und Builddetails dazu anzeigen. Wenn Sie in einem agilen Team arbeiten, werden zahlreiche tägliche Builds im Integrationszweig angezeigt. Andernfalls führt das Team keine häufigen Codemergeoperationen durch.

## Trends für Komponententests

Sie können Trends für Komponententests für die Builds anzeigen, die für einen bestimmten Zweig durchgeführt werden oder die in einer bestimmten Umgebung bereitgestellt werden. So können Sie beispielsweise Testtrends für Builds des Masterzweigs anzeigen. Wenn Test für Builds, die zur Produktion übergeben wurden, fehlschlagen, sollten entsprechende Maßnahmen ergriffen werden. Auch eine zurückgehende Anzahl von Tests über einen bestimmten Zeitraum hinweg kann auf ein mögliches Problem hinweisen.

## Trends für Funktionsüberprüfungstests

Sie können Trends für Funktionsüberprüfungstests für die Builds anzeigen, die für einen bestimmten Zweig durchgeführt werden oder die in einer bestimmten Umgebung bereitgestellt werden. So können Sie beispielsweise Testtrends für Builds des Masterzweigs anzeigen. Wenn Test für Builds, die an die Produktion übergeben wurden, fehlschlagen, sollten Maßnahmen ergriffen werden. Auch eine zurückgehende Anzahl von Tests über einen bestimmten Zeitraum hinweg kann auf ein mögliches Problem hinweisen.

## Trends für die Codeabdeckung

Sie können Trends für die Codeabdeckung für die Builds anzeigen, die in einer bestimmten Umgebung bereitgestellt werden. So können Sie beispielsweise Trends für die Codeabdeckung für Builds anzeigen, die an die Produktion übergeben wurden. Idealerweise sollte die Codeabdeckung für Builds, die an die Produktion übergeben werden, im Laufe der Zeit eine Verbesserung aufweisen. Wenn eine Verschlechterung der Codeabdeckung auftritt, sollten entsprechende Maßnahmen ergriffen werden.

## Richtlinien

Richtlinien sind Gruppen von Regeln, die die Gates in Ihrer Delivery Pipeline steuern. Entspricht Ihr Code keiner Richtlinie oder überschreitet Ihr Code eine Richtlinie, die an einem bestimmten Gate durchgesetzt wird, wird die Bereitstellung angehalten; dadurch wird verhindert, dass sicherheitsbedenkliche Änderungen freigegeben werden.


## Voraussetzungen
{: #prerequisites}

Für Deployment Risk sind neben der in [Einführung in {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html) beschriebenen Konfiguration einige zusätzliche Konfigurationsschritte erforderlich.

Für die Verwendung von Deployment Risk benötigen Sie zwei Dinge:

* Eine Instanz von {{site.data.keyword.deliverypipeline}} oder ein Jenkins-Projekt
* Tests, mit denen Sie Ihr Projekt bewerten möchten

## Informationen zu Integrationen

Deployment Risk kann mit {{site.data.keyword.deliverypipeline}} integriert werden, das Bestandteil von {{site.data.keyword.contdelivery_full}} ist, sowie mit Jenkins-Projekten. Auf einer höheren Ebene ähneln sich die Anweisungen zur Verwendung beider Optionen.  

Wenn Sie {{site.data.keyword.deliverypipeline}} verwenden, führen Sie die folgenden Schritte aus:

1. [Erstellen Sie Richtlinien und Regeln](risk_policies.html) für die {{site.data.keyword.DRA_short}}-Verwaltung.
2. [Bereiten Sie die Pipelinestufen vor](risk_cd.html), um sie mit {{site.data.keyword.DRA_short}} zu integrieren.
3. [Erstellen oder bearbeiten Sie Testjobs](risk_cd.html) in der Pipeline, mit denen Ergebnisse nach {{site.data.keyword.DRA_short}} hochgeladen werden.
4. [Fügen Sie Gates zu der Pipeline hinzu](risk_cd.html), die basierend auf diesen Ergebnissen und Ihren Richtlinien Entscheidungen zu Hochstufungen fällen.
5. Führen Sie die Pipeline aus und [zeigen Sie die Ergebnisse an](results.html).

Wenn Sie Jenkins verwenden, führen Sie die folgenden Schritte aus:

1. [Erstellen Sie Richtlinien und Regeln](risk_policies.html) für die {{site.data.keyword.DRA_short}}-Verwaltung.
2. [Installieren Sie das Jenkins-Plug-in und konfigurieren Sie es](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
3. [Erstellen Sie Testjobs und Gates gemäß den Anweisungen in der Plug-in-Anleitung](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin). Die Tests laden Ergebnisse zum Analysieren nach {{site.data.keyword.DRA_short}} hoch und die Gates verwenden diese Ergebnisse für Hochstufungsentscheidungen.
4. Führen Sie das Projekt aus und [zeigen Sie die Ergebnisse an](results.html). 

Unabhängig davon, wie Sie Ihren Code erstellen und bereitstellen, sind die Ergebnisse gleich: Die Builds, die Standards entsprechen, passieren die Deployment Risk-Gates; Builds, die nicht den angegebenen Standards entsprechen, werden gestoppt. 
