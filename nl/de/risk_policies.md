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

# Richtlinien und Regeln erstellen
{: #policies_and_rules}

Richtlinien sind Gruppen von Regeln, die die Gates in Ihrer Delivery Pipeline steuern. Entspricht Ihr Code keiner Richtlinie oder überschreitet Ihr Code eine Richtlinie, die an einem bestimmten Gate durchgesetzt wird, wird die Bereitstellung angehalten; dadurch wird verhindert, dass sicherheitsbedenkliche Änderungen freigegeben werden.

Sie können Richtlinien in {{site.data.keyword.DRA_short}} festlegen. Richtlinien werden in der {{site.data.keyword.Bluemix_notm}}-Organisation erstellt, die {{site.data.keyword.DRA_short}} enthält. Alle Anwendungen, die sich in ein und derselben Organisation befinden, können die Richtlinie nutzen. 

## Richtlinien erstellen
{: #create_policies}

Führen Sie zum Erstellen einer Richtlinie die folgenden Schritte aus:

1. Klicken Sie im Navigationsmenü von {{site.data.keyword.DRA_short}} auf **Einstellungen**.

2. Klicken Sie auf **Richtlinien**.

3. Klicken Sie auf **Richtlinie erstellen** und geben Sie anschließend einen Namen und eine Beschreibung für die neue Richtlinie ein.

4. Klicken Sie auf **Weiter**.

4. Fügen Sie mindestens eine Regel zur Richtlinie hinzu:
  1. Klicken Sie auf **Regel zu Richtlinie hinzufügen**.
  2. Wählen Sie den Regeltyp aus.
  3. Geben Sie Details und Bedingungen für die Regel ein.
  4. Klicken Sie auf **Speichern**.

5. Wenn Sie mit dem Hinzufügen von Regeln zu der Richtlinie fertig sind, klicken Sie auf die Option zum Abschließen des Vorgangs.

## Regeln erstellen
{: #creating_rules}

Mit Regeln werden die Kriterien festgelegt, anhand derer Richtlinien Erfolg oder Fehlschlagen bewerten. Sie können beispielsweise eine Richtlinie "Komponententest und Testumfang" erstellen, die eine Regel für Komponententests enthält, die eine 80-prozentige Erfolgsquote für Komponententests fordert, und eine Regel für den Testumfang, die eine 100-prozentige Codeabdeckung verlangt. Wenn Sie ein Gate hinzufügen, das sich auf diese Regel in einer Pipeline bezieht, verhindert das Gate, dass Builds, die nicht beiden Regeln entsprechen, weiter durchgeführt werden können. 

Sie können immer eine erfolgreiche Durchführung verlangen, indem Sie Tests als kritisch markieren. Wählen Sie zum Erstellen einer Regel eine Richtlinie aus und klicken Sie dann auf **Regel zu Richtlinie hinzufügen**. 

### Regeln für Funktionsüberprüfungstests erstellen
{: #criteria_fvt}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle. Lesen Sie zum Ermitteln von Testfallnamen
[Formate und Tools für Testergebnisse](#criteria_formats).

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


### Regeln für Komponententests erstellen
{: #criteria_ut}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle. Lesen Sie zum Ermitteln von Testfallnamen
[Formate und Tools für Testergebnisse](#criteria_formats).

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


### Regeln für Codeabdeckung erstellen
{: #criteria_codecoverage}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viel Codeabdeckung erforderlich ist, damit sie als erfolgreich deklariert werden kann.

3. Wählen Sie für die Überwachung von Codeabdeckungsregressionen das entsprechende Kontrollkästchen aus.

4. Klicken Sie auf **Speichern**.

### Regeln für statische Sicherheitsscans erstellen
{: #criteria_static}

Sie können {{site.data.keyword.DRA_short}} mit IBM Application Security on Cloud integrieren, um statische Code-Scans und dynamische App-Scans durchzuführen. Weitere Informationen zu Application Security on Cloud finden Sie in der [offiziellen Dokumentation](/docs/services/ApplicationSecurityonCloud/index.html) zu diesem Produkt.

1. Geben Sie eine Beschreibung ein.

2. Geben Sie jeweils die maximale Anzahl von Problemen mit hohem, mittlerem und niedrigem Schweregrad an, die gemäß der Regel zulässig sind. 

3. Klicken Sie auf **Speichern**.

### Regeln für dynamische Sicherheitsscans erstellen
{: #criteria_dynamic}

Sie können {{site.data.keyword.DRA_short}} mit {{site.data.keyword.appseccloudfull}} integrieren, um dynamische App-Scans durchzuführen. Weitere Informationen zu Application Security on Cloud finden Sie in der [offiziellen Dokumentation](/docs/services/ApplicationSecurityonCloud/index.html) zu diesem Produkt.

1. Geben Sie eine Beschreibung ein.

2. Geben Sie jeweils die maximale Anzahl von Problemen mit hohem, mittlerem und niedrigem Schweregrad an, die gemäß der Regel zulässig sind. 

3. Klicken Sie auf **Speichern**.

## Formate und Tools für Testergebnisse
{: #criteria_formats}

Für Testfälle unterstützt {{site.data.keyword.DRA_short}} folgende Typen von Metriken und Formaten:

* Funktionsüberprüfungstest (Mocha, xUnit)
* Komponententest (Mocha, xUnit, Karma/Mocha)
* Codeabdeckung (Cobertura, lcov, Istanbul als JSON-Format für Übersichtsberichte, Blanket.js)

{{site.data.keyword.DRA_short}} unterstützt auch Selenium- und Jasmine-Tests. Diese Tests müssen in den offiziell unterstützten Tools wie xUnit und Mocha integriert sein. Weitere Informationen zur gemeinsamen Verwendung von {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}} und Selenium finden Sie unter [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Für Elemente mit Testfällen können Sie kritische Testfälle angeben; dabei handelt es sich um Tests, die unabhängig vom zulässigen Prozentsatz bestanden werden müssen. Namen für kritische Testfälle müssen mit dem Attribut `full title` des Testfalls übereinstimmen.    
* Bei Karma/Mocha-Tests sind die Beschreibungszeichenfolgen `describe()` und `it()` durch Leerzeichen verbunden.
* Bei xUnit-Tests sind Paketname, Klassenname und Funktionsname durch Leerzeichen verbunden. Dies wird durch das folgende Beispiel veranschaulicht:
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  Dieses Beispiel generiert die folgenden Testfallnamen:
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

Sie können Sauce Labs mit {{site.data.keyword.DRA_short}} verwenden; fügen Sie hierfür die Sauce Labs-Toolintegration zu Ihrer Pipeline hinzu. Integrieren Sie anschließend die Umgebungsvariablen `SAUCE_USERNAME` und `SAUCE_ACCESS_KEY` als Berechtigungsnachweise in die Selenium-Tests.

Sie können die vollständigen Titel aller Tests nach einer Ausführung in den Protokollen sehen.  

**Anmerkungen:**
* {{site.data.keyword.DRA_short}} unterstützt keine kritischen Tests, die einen Bindestrich im vollständigen Titel enthalten.    
* Wenn Sie Ihren Organisationsnamen ändern, müssen Sie die Richtlinien, die dem vorherigen Namen zugeordnet waren, neu erstellen. Der Zugriff auf Entscheidungsberichte, die vor der Namensänderung generiert wurden, geht sonst verloren.
