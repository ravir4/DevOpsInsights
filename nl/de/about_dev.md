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

# Informationen zu Developer Insights
{: #gettingstarted}

Mit {{site.data.keyword.DRA_full}} Developer Insights können Sie die Risiken bei der Entwicklung Ihres Projekts umfassend untersuchen. Sie können fehleranfällige Dateien ermitteln und eine Konformitätsansicht des Projekts im Hinblick auf die DevOps-Verfahren erhalten.
{:shortdesc}

Klicken Sie nach dem Öffnen von {{site.data.keyword.DRA_short}} über die Toolchain auf **Developer Insights**. Von hier aus können Sie eine Analysekategorie auswählen, um einen tieferen Einblick in die Codebasis Ihres Projekts zu erhalten. Was einzelne Datensätze aussagen, kann von Team zu Team unterschiedlich sein. Sie können daher für jede Visualisierung einen Drilldown durchführen, um eine weitere Orientierungshilfe zu erhalten. Sie können die Daten anhand des Datums sowie zahlreicher weiterer Kriterien filtern.

## Datenkategorien
Für die Daten, die von {{site.data.keyword.DRA_short}} zum Auffüllen der Dashboards verwendet wird, wird automatisch ein Data-Mining aus dem Repository für die Quellcodeverwaltung des Teams durchgeführt. Weitere Informationen zur Bedeutung der Daten und zu Anwendungsmöglichkeiten für Ihr Projekt erhalten Sie durch Klicken auf **Informationen** oder **Anweisungen** in den Diagrammen für bewährte Verfahren. Darüber hinaus können Sie auch die Ergebnisse und Details der anderen Visualisierungen anzeigen, um weitere Informationen zu erhalten.

### Bewährte Verfahren für Entwickler

Developer Insights stellt eine Reihe von Diagrammen bereit, anhand derer Sie Ihr Projekt gegenüber bewährten DevOps- und Entwicklerverfahren messen können. Verwenden Sie diese Kategorie, um eine übergeordnete Ansicht über den Reifegrad, den Zustand und die Effizienz Ihres Projekts zu erhalten.

### Probleme

Die Kategorie 'Probleme' fast alle Probleme bei der Leistungserfassung für Ihr Team zentral zusammen. Die Probleme werden automatisch nach Typ, Priorität und Tag gruppiert und können im Zeitverlauf angezeigt werden.

Diese Problemgruppierungen können sich von Team zu Team in ihrer Bedeutung unterscheiden. Für ein Team könnte es beispielsweise interessant sein, ob die meisten mit Tags versehenen Elemente für ein bestimmtes Release geschlossen sind, während ein anderes Team Releases nicht mit Tags versieht und diese gemäß der Priorität der offenen Probleme verarbeitet.  

### Commits

In der Kategorie 'Commits' werden alle Commits Ihres Teams zentral angezeigt. Die Commits werden automatisch nach Typ, Tag und Zeilenänderungen gruppiert. Sie können über einen von Ihnen ausgewählten Zeitraum hinweg angezeigt werden.

Commits zeigen den Arbeitsumfang an, den Ihre Teammitglieder zur Codebasis beitragen. Untersuchen Sie Ihre Commitdaten, um zu verstehen, an welcher Stelle im Zeitverlauf gesehen ein großer Aufwand betrieben wird und wie Sie die Arbeitslasten Ihres Teams besser verteilen können.

### Dateien

Die Kategorie 'Dateien' zeigt, welche Dateien in Ihrem Projekt am häufigsten verwendet werden. Ganz gleich, ob Sie Daten anhand der Anzahl der Zeilenänderungen, Commits oder Fehler bewerten: Diese Daten verraten Ihnen, in welchen Bereichen Ihr Team besonders aktiv ist.

Versuchen Sie allgemein sowohl die Anzahl der Mitglieder zu verringern, die eine Datei bearbeiten dürfen, als auch die Häufigkeit, mit der diese Datei geändert wird. Dieses Ziel kann jedoch für einige Dateien, wie allgemeine Konfigurationsdateien, unrealistisch sein. Jedoch sind für einzelne Dateien, an denen Entwickler gleichzeitig viele Änderungen vornehmen, Probleme vorprogrammiert.

### Pull-Anforderungen

In der Kategorie 'Pull-Anforderungen' werden die Pull-Anforderungen Ihres Teams zentral angezeigt. Die Pull-Anforderungen werden mithilfe von maschinellem Lernen auf ihre Fehleranfälligkeit hin analysiert. Auf diese Weise können Sie schnell erkennen, welche Pull-Anforderungen ein zusätzliches Risiko für die Codebasis bedeuten.

Mit Pull-Anforderungen wird die Arbeit angezeigt, die die Teammitglieder in die Codebasis mergen möchten. Untersuchen Sie die Pull-Anforderungsdaten, um alle damit verbundenen Risiken zu analysieren und zu ermitteln, wie Risiken in Zukunft vermieden werden können.

## Filtern nach Dateierweiterung

DevOps Insights ignoriert Dateien mit den folgenden Erweiterungen:

* .bin
* .cdr
* .jpeg
* .jpg
* .json
* .markdown
* .md
* .png
* .pyc
* .svg
* .text
* .yaml
* .yml
