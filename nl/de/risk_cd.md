---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk-Analyse und Continuous Delivery integrieren

Sie können für {{site.data.keyword.contdelivery_full}} Pipelines instrumentieren, um die Deployment Risk-Analysemöglichkeiten von
{{site.data.keyword.DRA_short}} zu nutzen. Anschließend können Sie Daten aus diesen Jobs veröffentlichen und Gates hinzufügen, die
Risikorichtlinien durchsetzen.

Eine allgemeine Erläuterung der Deployment Risk-Analyse von {{site.data.keyword.DRA_short}} finden Sie in
[Informationen zu Deployment Risk](./about_risk.html).

Weitere Informationen zu Continuous-Delivery-Pipelines finden Sie in
[der offiziellen Dokumentation](../ContinuousDelivery/pipeline_working.html).

## Pipelinestufen und Jobs vorbereiten
{: #integrate_pipeline}

Zu Anfang müssen Sie Ihre Pipeline instrumentieren, um mit {{site.data.keyword.DRA_short}} zu kommunizieren. Dafür müssen Sie
bestimmte Umgebungsvariablen definieren, die für alle Pipeline-Jobs gelten, die Code erstellen, testen oder bereitstellen. Sie müssen außerdem
Umgebungsvariablen hinzufügen, um mithilfe des Testertyps 'DevOps Insights-Gate' Jobs zu testen, die Risikorichtlinien durchsetzen.

* Builddatensätze
* Bereitstellungsdatensätze
* Testergebnisse

Testergebnisse müssen Daten in einem der folgenden unterstützten Formate bereitstellen:

| Testtyp                    | Unterstützte Formate                                               |
|------------------------------|-----------------------------------------------------------------|
| Funktionsüberprüfungstest | Mocha, xUnit                                                    |
| Komponententest                    | Mocha, xUnit, Karma/Mocha                                       |
| Codeabdeckung                | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Statische App-Überprüfung              | Statische App-Überprüfungen werden von IBM Application Security on Cloud bereitgestellt  |
| Dynamische App-Überprüfung             | Dynamische App-Überprüfungen werden von IBM Application Security on Cloud bereitgestellt |
| SonarQube                    | Scandaten, die von SonarQube-Überprüfungen bereitgestellt werden                           |

Umgebungsvariablen, die Sie in der Pipeline definieren, stellen für die Veröffentlichung dieser Datensätze Kontext bereit. Sie können
sie in den Scripts Ihrer Jobs mithilfe des Befehls `export` definieren. Sie können sie auf den einzelnen Pipelinestufen auch
im Menü für die Umgebungseigenschaften festlegen.

Umgebungsvariablen:

| Umgebungsvariable  | Zweck | Erforderlich in |
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | Der Name der App im Dashboard. | Alle Jobs, die {{site.data.keyword.DRA_short}}-Risikorichtlinien erstellen, testen, bereitstellen und durchsetzen. |
| `BUILD_PREFIX`  | Text, der dem Build einer Stufe als Präfix hinzugefügt wird. Dieser Text wird auch im Dashboard angezeigt. | Alle Jobs, die {{site.data.keyword.DRA_short}}-Risikorichtlinien erstellen, testen, bereitstellen und durchsetzen. |
| `LOGICAL_ENV_NAME`  | Die Umgebung, in der die Anwendung ausgeführt wird. | Testet Jobs und stellt sie bereit. |

### Build-Jobs konfigurieren

Legen Sie für den letzten Build-Job in einer Stufe Umgebungsvariablen für einen Anwendungsnamen und ein Buildpräfix fest. Ein Beispielscript würde folgende Befehle enthalten:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Nach Abschluss dieses Jobs würde die Pipeline in {{site.data.keyword.DRA_short}} eine Nachricht mit dem Inhalt veröffentlichen, dass
ein Build für eine Beispielanwendung (SampleApp) abgeschlossen wurde.

### Bereitstellungsjobs konfigurieren

Legen Sie für den letzten Bereitstellungsjob in der Stufe einen Anwendungsnamen, ein Buildpräfix und einen Umgebungsnamen fest. Ein Beispielscript würde folgende Befehle enthalten:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Nach Abschluss Ihres Bereitstellungsjobs würde die Pipeline in {{site.data.keyword.DRA_short}} eine Nachricht mit dem Inhalt
veröffentlichen, dass der angegebene Build und die angegebene App in einer Umgebung bereitgestellt wurden.

### Testjobs konfigurieren

Legen Sie für alle Jobs, die Testergebnisse generieren, einen Anwendungsnamen und ein Buildpräfix fest.

Wenn der Job Ergebnisse eines Funktionsüberprüfungstests (FVT - Functional Verification Test) generiert, müssen Sie als Namen der logischen Umgebung
alle entsprechenden Umgebungen festlegen, in denen die Tests ausgeführt werden.

Ein Beispielscript würde folgende Befehle enthalten:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# Die Variable LOGICAL_ENV_NAME ist nur bei der Veröffentlichung von FVT-Ergebnissen erforderlich.
export LOGICAL_ENV_NAME="Production"
```

Stellen Sie sicher, dass die Anwendungsnamen und Umgebungen, wo erforderlich, übereinstimmen. Beispielsweise sollte ein
Produktionstestjob, der für eine Implementierung in der Produktionsumgebung ausgeführt wird, entsprechende Werte für
`LOGICAL_ENV_NAME` aufweisen.

## Testdaten in DevOps Insights veröffentlichen
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} verwendet die Testergebnisse aus Ihren Jobs, um Berichte zu generieren und Risikorichtlinien
zu veröffentlichen. Sie können Testdaten aus allen Jobtypen veröffentlichen.

Es gibt zwei Optionen für die Veröffentlichung von Testergebnissen:

* Rufen Sie eine einfache Befehlszeilenschnittstelle (CLI) in einem Job-Script auf.

* Fügen Sie Ihrer Pipeline einen Testjob mit dem Typ 'Erweiterter Tester' hinzu.

Wenn Sie die Methode 'Erweiterter Tester' verwenden, veröffentlichen Sie Testergebnisse nicht über die CLI. Sie geben stattdessen die
Position der Ergebnisdateien im Pipeline-Job an und der Job lädt die Ergebnisse hoch, sobald diese verfügbar sind.

Unabhängig von der von Ihnen verwendeten Veröffentlichungsmethode müssen die Testergebnisse ein von
{{site.data.keyword.DRA_short}} unterstütztes Format aufweisen:

<table><thead>
<tr>
<th>Testtyp</th>
<th>Unterstützte Formate</th>
</tr>
</thead><tbody>
<tr>
<td>Funktionsüberprüfungstest</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Komponententest</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Codeabdeckung</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

### Testdaten aus einem beliebigen Jobtyp veröffentlichen

Sie können in einer Pipeline jede Art von Job verwenden, um einen Test auszuführen. Nach der Ausführung des Tests können Sie dessen
Ergebnisse in {{site.data.keyword.DRA_short}} hochladen. Sie laden die Ergebnisse durch Aufrufen einer Befehlszeilenschnittstelle im
Shell-Script des Jobs hoch. 

Die folgenden Typen von Testergebnissen können Sie über die CLI hochladen:

* Komponententests
* Codeabdeckung
* Funktionsüberprüfungstests
* Ergebnisse von statischen und dynamischen App-Überprüfungen aus IBM Application Security on Cloud. 

Das Folgende ist ein Beispielscript, mit dem Tests ausgeführt und die Ergebnisse anschließend in
{{site.data.keyword.DRA_short}} hochgeladen werden: 

```
# Führen Sie Tests aus und generieren Sie hier eine Datei mit Testergebnissen.
...

# Veröffentlichen Sie die Ergebnisse anschließend in DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

Weitere Informationen zum Befehl `idra` finden Sie bei
[NPM auf der Seite mit dem Paket des Typs 'grunt-idra3'](https://www.npmjs.com/package/grunt-idra3). 

### Testdaten aus Jobs des Typs 'Erweiterter Tester' veröffentlichen

Sie können Testjobs mit dem Typ 'Erweiterter Tester' zu einer Pipeline hinzufügen. Nach ihrer Ausführung werden ihre Ergebnisse
automatisch in {{site.data.keyword.DRA_short}} hochgeladen. 

1. Klicken Sie auf der Stufe, auf der Sie den Job zum Hochladen von Ergebnissen hinzufügen möchten, auf das Symbol für
**Stufenkonfiguration** ![Symbol für Konfiguration von Pipelinestufen](images/pipeline-stage-configuration-icon.png). Klicken Sie auf die Option zum Konfigurieren der Stufe.
2. Erstellen Sie einen Testjob und geben Sie einen Namen für den Job ein. 
3. Wählen Sie als Jobtyp **Erweiterter Tester** aus.
4. Füllen Sie die Felder für den Testbefehl und das Arbeitsverzeichnis so aus, wie Sie es für einen normalen Testjob für eine Pipeline tun würden. 
5. Füllen Sie die übrigen Felder aus, um die Testergebnisse für einen bestimmten Testtyp hochzuladen. 

 1. Wählen Sie den Metriktyp aus, der dem entspricht, was Sie in der {{site.data.keyword.DRA_short}}-Richtlinie definiert haben, die Sie verwenden möchten.
 2. Geben Sie eine Speicherposition für die Ergebnisdatei ein. Diese Position ist relativ zum Arbeitsverzeichnis. 

6. Wenn Sie Ergebnisse für einen zweiten Testtyp im selben Job hochladen möchten, müssen Sie die Felder ausfüllen, die mit *Additional* markiert sind.
7. Klicken Sie auf **Speichern**, um zu der Pipeline zurückzukehren.

Abbildung 1 zeigt einen Testjob, der für die Ausführung von Komponententests, für das Hochladen der Ergebnisse im Mocha-Format sowie für das Hochladen der Codeabdeckungsergebnisse im Istanbul-Format konfiguriert ist.

![DevOps Insights - Upload-Job](images/insights_upload_job.png)
*Abbildung 1. Ergebnisse nach DevOps Insights hochladen*



## Gates definieren
{: #configure_pipeline_gates}

Mit {{site.data.keyword.DRA_short}}-Gates wird überprüft, ob Ihre Testergebnisse eine definierte Richtlinie einhalten. Wird die Richtlinie nicht erfüllt, schlägt das {{site.data.keyword.DRA_short}}-Gate standardmäßig fehl. Sie können Gates auch so konfigurieren, dass sie eine beratenden Funktion einnehmen, damit selbst nach einem Ausfall die Pipeline fortgeführt werden kann.

Das Deployment Risk-Dashboard ist nach einem Staging-Bereitstellungsjob auf das Vorhandensein eines Gates angewiesen. Wenn Sie das Dashboard verwenden möchten, stellen Sie sicher, dass nach der Bereitstellung für eine Staging-Umgebung (jedoch vor der Bereitstellung für eine Produktionsumgebung) ein Gate vorhanden ist.

Normalerweise werden Gates vor der Hochstufung von Builds in der Pipeline platziert. Diese Positionen sind für die Überprüfung der Qualität des Builds auf Basis Ihrer Richtlinien ideal, um sicherzustellen, dass die Hochstufung von einer Umgebung zu einer anderen sicher ist. Sie können Gates jedoch an einer beliebigen Stelle in der Pipeline platzieren, für die ein bestimmtes Kriterium überprüft werden soll. Gates, die vor der Bereitstellung in einer Staging-Umgebung liegen, setzen Richtlinien zwar weiter durch, erscheinen jedoch nicht im Deployment Risk-Dashboard.

1. Klicken Sie auf einer Stufe auf das Symbol für die **Stufenkonfiguration**
![Symbol für Konfiguration von Pipelinestufen](images/pipeline-stage-configuration-icon.png) und klicken Sie
auf die Option zum Konfigurieren der Stufe.
2. Klicken Sie auf **Job hinzufügen**. Wählen Sie als Jobtyp **Test** aus.
3. Wählen Sie als Testertyp **{{site.data.keyword.DRA_short}}-Gate** aus.
4. Geben Sie den Umgebungsnamen an. Stellen Sie sicher, dass dieser Wert mit der Definition in Ihren [Umgebungseigenschaften](#toolchain_pipeline_props) übereinstimmt.
5. Geben Sie den Richtlinienname ein, der an diesem Gate überprüft werden soll.

 Dieser Name muss genau mit einem der von Ihnen definierten Richtliniennamen übereinstimmen. Sie können nur Richtlinien angeben, die in derselben {{site.data.keyword.Bluemix_notm}}-Organisation wie Ihre Toolchain definiert sind.

6. Optional: Damit ein Gate im Empfehlungsmodus funktioniert, müssen Sie die Auswahl des Kontrollkästchens zum Stoppen dieser Stufe beim Fehlschlagen dieses Jobs zurücknehmen. Im Empfehlungsmodus führt {{site.data.keyword.DRA_short}} dieselbe Richtlinienanalyse für das Gate durch und generiert Berichte; doch wenn ein Fehler auftrittt, wird die Pipeline nicht gestoppt.
7. Klicken Sie auf **Speichern**, um zu der Pipeline zurückzukehren.
8. Richten Sie für all Ihre {{site.data.keyword.DRA_short}}-Richtlinien Gates ein; wiederholen Sie dafür dieser Schritte.

![Deployment Risk - Mocha-Job](images/insights_gate_job.png)
*Abbildung 2. DevOps Insights-Gate*

Beginnen Sie nach der Konfiguration der Pipeline mit der Verwendung von {{site.data.keyword.DRA_short}}. 
