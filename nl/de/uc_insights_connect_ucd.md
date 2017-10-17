---

copyright:
  years: 2017

lastupdated: "2017-07-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Daten von IBM UrbanCode Deploy-Servern anzeigen
{: #connect_ucd}

Um Daten von einem IBM UrbanCode Deploy-Server in Delivery Insights anzeigen zu können, müssen Sie eine DevOps Connect-Instanz einrichten, ein Patch auf dem Server installieren und dann diesen Server mit DevOps Connect verbinden.
{:shortdesc}

## Voraussetzungen
{: #prereqs}

Um Informationen von den IBM UrbanCode Deploy-Servern in {{site.data.keyword.DRA_short}} zu sehen, müssen Sie eine Instanz von DevOps Connect auf einem System hosten, das eine Verbindung mit den IBM UrbanCode Deploy-Servern herstellen kann. Dieses System kann ein physischer Computer oder eine virtuelle Maschine sein. 

Das System, das DevOps Connect hostet, muss die folgenden Voraussetzungen erfüllen:
- Das System muss über Java Runtime Environment (JRE) Version 8 oder höher verfügen.
- Die Systemvariable `PATH` muss die Position der JRE enthalten.
- Es muss vom System her möglich sein, dass DevOps Connect abgehenden Verbindungen zu IBM Bluemix erstellen kann.

Darüber hinaus muss der verwendete IBM UrbanCode Deploy-Server die Version 6.2 oder höher aufweisen.

## {{site.data.keyword.DRA_short}}-Service konfigurieren
{: #configure_service}

Falls Sie nicht über den Service {{site.data.keyword.DRA_short}} verfügen, fügen Sie ihn hinzu:
1. Melden Sie sich bei {{site.data.keyword.Bluemix}} an und klicken Sie auf **Services > Dashboard**.
1. Klicken Sie auf **Service erstellen**.
1. Klicken Sie auf den Service {{site.data.keyword.DRA_short}}.
1. Wählen Sie einen Preistarif aus und klicken Sie dann auf **Erstellen**.
1. Klicken Sie auf **Verwalten** und klicken Sie anschließend unter der Option für Einblicke in die Bereitstellung
von UrbanCode auf **Hier starten**.
1. Klicken Sie im Fenster für die Toolchain-Vorlage auf **Erstellen**.  
Delivery Insights erstellt eine Toolchain für Ihre Organisation. Toolchains sind Sammlungen von Toolintegrationen und im vorliegenden Fall sind IBM UrbanCode Deploy und {{site.data.keyword.DRA_short}} Teile der Toolchain. Weitere Informationen zu Toolchains finden Sie in [Arbeiten mit Toolchains](../ContinuousDelivery/toolchains_working.html).
1. Klicken Sie in der Toolchain auf das Tool 'IBM UrbanCode Deploy'.
1. Klicken Sie auf die Schaltfläche 'Einstellungen' und anschließend auf **Einrichten**.

In Zukunft können Sie {{site.data.keyword.DRA_short}} aufrufen, indem Sie auf **Services
> Dashboard** klicken und anschließend auf Ihre Instanz des Service {{site.data.keyword.DRA_short}} klicken.

Wenn Sie bereits über eine Toolchain verfügen, können Sie IBM UrbanCode Deploy und {{site.data.keyword.DRA_short}}-Tools zu dieser
Toolchain hinzufügen und über diese Tools auf Delivery Insights zugreifen. Klicken Sie anschließend auf das Tool 'IBM UrbanCode Deploy', klicken
Sie auf die Schaltfläche 'Einstellungen' und klicken Sie dann auf **Einrichten**.

Nun können Sie die Anweisungen auf der Seite **Einrichten** ausführen, um DevOps Connect zu installieren und eine
Verbindung zu {{site.data.keyword.DRA_short}} herzustellen, wie im folgenden Abschnitt beschrieben.

## DevOps Connect installieren und eine Verbindung zu {{site.data.keyword.DRA_short}} herstellen
{: #install_connect}

1. Führen Sie auf der Seite **Einrichten** die Schritte zum Einrichten von DevOps Connect aus und verbinden Sie Ihre
IBM UrbanCode Deploy-Server. Diese Schritte umfassen Folgendes:
{: #set_up_connect}
  1. Einrichten eines Systems zur Ausführung von DevOps Connect, wie in den [Voraussetzungen](uc_insights_connect_ucd.html#prereqs) beschrieben.
  1. Herunterladen von DevOps Connect, das in einer ausführbaren JAR-Datei bereitgestellt wird.

  1. Wenn Sie für die Verbindung zum Internet einen Proxy verwenden, legen Sie für die Umgebungsvariable
`_JAVA_OPTIONS` folgenden Wert fest:
    * Wenn der Proxy HTTPS verwendet, legen Sie für `_JAVA_OPTIONS` den Wert
`-Dhttps.proxyHost=HOSTNAME -Dhttps.proxyPort=PORT` fest; dabei ist `HOSTNAME` der Hostname des Proxy-Servers
und `PORT` der HTTPS-Port des Proxy-Servers.
    * Wenn der Proxy HTTP verwendet, legen Sie für `_JAVA_OPTIONS` den Wert
`-Dhttp.proxyHost=HOSTNAME -Dhttp.proxyPort=PORT` fest; dabei ist `HOSTNAME` der Hostname des Proxy-Servers
und `PORT` der HTTP-Port des Proxy-Servers.

  1. Kopieren Sie den Befehl von der Seite mit den Anweisungen für **Einrichten**. Mit diesem Befehl wird DevOps Connect mit einem Token gestartet, das die Herstellung einer Verbindung zu Ihrer Organisation in {{site.data.keyword.Bluemix}} ermöglicht.
  1. DevOps Connect wird standardmäßig an Port 8443 ausgeführt; dies ist derselbe Port, an dem auch der IBM UrbanCode Deploy-Server
standardmäßig ausgeführt wird. Wenn der IBM UrbanCode Deploy-Server oder ein beliebiger anderer
Service an Port 8443 ausgeführt wird, ändern Sie daher für DevOps Connect den Port, indem Sie den Parameter `-Dserver.port`
zum Befehl hinzufügen. Wenn Sie beispielsweise festlegen möchten, dass DevOps Connect Port 8888 verwendet, sieht der Anfang des Befehls ähnlich
dem Folgenden aus:  
```bash
java -Dserver.port=8888 -jar devops-connect-2.0.92clear0618.jar -Dserver.port=8888
```  

Der vollständige Befehl enthält Informationen zu Ihrem Bluemix-Konto, das automatisch eine Konfiguration von DevOps Connect ausführt, wie
im folgenden Beispiel gezeigt:

```bash
java -Dserver.port=8888 -jar devops-connect-2.0.920618.jar --sync.id=a2c12cb9-9a09-9832-479b01bf --sync.token=j0zs325U6qp080pzpcQ  --sync.registrar=jsmith@example.com
```

  1. Führen Sie den Befehl aus und warten Sie, bis DevOps Connect gestartet wurde.

  1. Stellen Sie zwischen Ihren IBM UrbanCode Deploy-Servern und DevOps Connect eine Verbindung her, wie im folgenden Abschnitt beschrieben.

## Verbindung für IBM UrbanCode Deploy-Server zu DevOps Connect herstellen
{: #connect_ucd_to_connect}

1. Wenn Ihr IBM UrbanCode Deploy-Server eine Version vor 6.2.5 aufweist, installieren Sie ein Patch auf dem Server. Für die Versionen
ab 6.2.5 ist kein Patch erforderlich.
  1. Laden Sie das für Ihre Version von IBM UrbanCode Deploy erforderliche Patch von der folgenden Seite herunter. Der Name der Patchdatei
für beispielsweise IBM UrbanCode Deploy 6.2.4.x lautet
[ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/6_2_4_X/ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar).  
  
    [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Stoppen Sie den Server. Informationen hierzu finden Sie in der Veröffentlichung zum [Starten und Stoppen des Servers](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Legen Sie die Dateien im Ordner <code><em>anwendungsdaten</em>/patches</code> ab, wobei <code><em>anwendungsdaten</em></code> der Ordner mit den Serveranwendungsdaten ist. Der Standardanwendungsdatenordner lautet unter Linux `/opt/ibm-ucd/server/appdata` und unter Windows `C:\Programme\ibm-ucd\server\appdata`. Auf Hochverfügbarkeitssystemen befindet sich der Anwendungsdatenorder immer auf einem gemeinsam genutzten Netzlaufwerk, auf das jeder Server Zugriff hat.

  1. Optional: Während der Server gestoppt ist, können Sie den Datenimport von diesem Server verbessern, indem Sie für die Datenbank
die folgenden SQL-Befehle ausführen. Diese Befehle sind für Version 6.2.5 und höhere Versionen nicht erforderlich.  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  Verwenden Sie den Namen Ihrer Datenbank für `MyUCDDatabase`.
  
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Starten Sie den Server. 

    **Hinweis:** Es kann möglicherweise länger als normal dauern, bis der IBM UrbanCode Deploy-Server gestartet wird. Falls der Server letztendlich nicht startet oder nicht ordnungsgemäß funktioniert, löschen Sie die Patchdateien und starten Sie dann den Server erneut. Die Patchdateien wirken sich nicht permanent auf den Server aus.

1. Für einige Versionen von IBM UrbanCode Deploy ist ein zusätzlicher Patch für den Server erforderlich, damit eine Verbindung zu DevOps Connect hergestellt werden kann. Wenn Sie IBM UrbanCode Deploy Version 6.2 bis 6.2.1.2 verwenden, müssen Sie das folgende zusätzliche Patch auf dem Server installieren:
  1. Laden Sie das Patch herunter: [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Stoppen Sie den Server.
  1. Legen Sie die Patchdatei im Ordner <code><em>anwendungsdaten</em>/patches</code> ab.
  1. Starten Sie den Server.

1. Erstellen Sie eine Integration zwischen DevOps Connect und dem IBM UrbanCode Deploy-Server:  

  **Wichtig:** Bei der ersten Ausführung der Integration ruft DevOps Connect Daten für die letzten 90 Tage ab. Wenn Sie über eine große Menge an Bereitstellungsdaten verfügen, kann dieser Prozess sehr lange dauern. Informationen darüber, wie Sie Daten für weniger als 90 Tage abrufen, finden Sie in [Fehlerbehebung](uc_insights_connect_ucd.html#troubleshooting).
  1. Erstellen Sie in IBM UrbanCode Deploy ein Authentifizierungstoken. Weitere Informationen finden Sie in der Veröffentlichung [Tokens](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. Klicken Sie in DevOps Connect auf **Integrationen** und dann auf **Neue hinzufügen**.
  1. Geben Sie einen Namen und eine Beschreibung für die Integration an. Die Standardposition von DevOps Connect ist `https://hostname:8443/`, wobei `hostname` der Hostname des Systems ist, das DevOps Connect hostet.
  1. Wählen Sie aus der Liste mit den Integrationstypen die Option **IBM UrbanCode Deploy for Cloud Reporting** aus.
  1. Geben Sie im Feld für den Server-URI die öffentliche URL des IBM UrbanCode Deploy-Servers ein. Beispiel: `https://my_UCD.example.com:8447`.
  1. Geben Sie im Feld für das Authentifizierungstoken das Authentifizierungstoken an, das von IBM UrbanCode Deploy generiert wurde.
  1. Geben Sie im Feld für den Benutzer mit Administratorberechtigung eine durch Kommas getrennte Liste mit IBM IDs ein, die Zugriff auf die DevOps Connect-Schnittstelle erhalten sollen.
  1. Optional: Klicken Sie auf **Integration ausführen**, um die Integration sofort auszuführen. Standardmäßig werden Integrationen jede Minute ausgeführt.
  1. Klicken Sie auf **Speichern**.

  ![Integration in DevOps Connect einrichten](images/uc_insights_dc_integration.gif)

Nun sind Ihre Daten mit Delivery Insights synchronisiert. Basierend auf diesen Daten können Sie jetzt Berichte erstellen und anzeigen. Ordnen Sie als nächsten Schritt die Umgebungen auf Ihren IBM UrbanCode Deploy-Servern den logischen Umgebungen in Delivery Insights zu.

## Umgebungen zu Berichten zuordnen
{: #mapping}

### Logische Umgebungen

Delivery Insights gruppiert die IBM UrbanCode Deploy-Umgebungen (auch als *physische Umgebungen* bezeichnet) in eine oder mehrere logische Umgebungen. So können Sie Umgebungen in Gruppen zusammenfassen, die für Ihre Anforderungen und Ihre Organisation geeignet sind. Wenn Sie beispielsweise mehrere Produktionsumgebungen für mehrere Anwendungen haben, können Sie alle diese Umgebungen in einer einzelnen logischen Umgebung gruppieren und Metriken für alle diese Umgebungen in einem einzelnen Produktionsumgebungs-Dashboard kombinieren. Die Zuordnung erfolgt nach Zeichenfolge, sodass Sie Umgebungen in einer Art und Weise gruppieren können, die für die IBM UrbanCode Deploy-Server Sinn macht.

### Logische Standardumgebungen

Standardmäßig umfassen Ihre Berichte logische Umgebungen, die IBM UrbanCode Deploy-Umgebungen anhand von Zeichenfolgen zugeordnet werden können. Beispielsweise werden alle Umgebungen mit "dev" im Namen zur logischen Entwicklungsumgebung (development = Entwicklung) und alle Umgebungen mit "prod" im Namen zur logischen Produktionsumgebung zugeordnet.

![Die logischen Standardumgebungen](images/uc_insights_mapping.gif)

### Umgebungen zu logischen Umgebungen zuordnen

Sie können physische Umgebungen manuell zu logischen Umgebungen zuordnen oder physische Umgebungen mithilfe von Mustern dynamisch mit logischen Umgebungen verknüpfen.

Führen Sie die folgenden Schritte aus, um physische Umgebungen zu logischen Umgebungen zuzuordnen:

1. Öffnen Sie Delivery Insights, klicken Sie auf die Schaltfläche 'Einstellungen' und klicken Sie auf
die Option für **Umgebungen zuordnen**.
1. Klicken Sie auf der Seite für die Zuordnung von Umgebungen auf eine vorhandene logische Umgebung oder erstellen Sie eine logische
Umgebung, indem Sie auf die Option für **Logische Umgebung hinzufügen** klicken.
1. Bei ausgewählter logischer Umgebung können Sie Muster angeben, wie Umgebungen zur logischen Umgebung hinzugefügt werden sollen. Klicken
Sie unter der Option für enthaltene Muster auf **Muster hinzufügen** und geben Sie ein zu verwendendes Muster an. Alle
Umgebungen mit Namen, die mit dem Muster übereinstimmen, einschließlich Umgebungen, die Sie später erstellen, werden der logischen Umgebung
hinzugefügt. Sie können dabei den Stern (*) als Platzhalter verwenden. Das Muster `env` entspricht beispielsweise den Umgebungen `env1`, `env2` und `env`.
1. Um Umgebungen manuell zu logischen Umgebungen zuzuordnen, klicken Sie auf **Manuell hinzufügen** und wählen Sie die Umgebungen aus, die hinzugefügt oder entfernt werden sollen.
1. Prüfen Sie, ob die logische Umgebung die von Ihnen gewünschten Umgebungen enthält.

![Zuordnung zur logischen Umgebung einrichten](images/uc_insights_mapping_manually.gif)

Nachdem Sie Umgebungen logischen Umgebungen zugeordnet haben, können Sie nun Berichtsinformationen nach diesen logischen Gruppen zusammenfassen.

## Anwendungen zu Geschäftsbereichen zuordnen
{: #lines}

Geschäftsbereiche sind Gruppen von Anwendungen, die einem gemeinsamen Geschäftszweck dienen. Sie können Ihre Anwendungen
Geschäftsbereichen zuordnen, um das Filtern der Anwendungen in Diagrammen zu vereinfachen. Sie können auch Diagramme erstellen, die auf
Geschäftsbereichen basieren.

Führen Sie folgende Schritte aus, um Geschäftsbereiche (LOBs - Lines of Business) einzurichten:

1. Klicken Sie in {{site.data.keyword.DRA_short}} auf **Delivery Insights**, klicken Sie auf die Schaltfläche
'Einstellungen' und klicken Sie anschließend auf die Option für **Geschäftsbereiche zuordnen**.
1. Klicken Sie auf der Seite für die Zuordnung von Geschäftsbereichen auf einen vorhandenen Geschäftsbereich oder erstellen Sie
einen Geschäftsbereich durch Eingeben eines Namens und Klicken auf **Erstellen**.
1. Bei ausgewähltem Geschäftsbereich können Sie Muster angeben, mithilfe derer Anwendungen zum Geschäftsbereich zugeordnet werden
sollen. Klicken
Sie unter der Option für enthaltene Muster auf **Muster hinzufügen** und geben Sie ein zu verwendendes Muster an. Alle
Anwendungen mit Namen, die mit dem Muster übereinstimmen, einschließlich Anwendungen, die Sie später erstellen, werden dem Geschäftsbereich
hinzugefügt.  Sie können dabei den Stern (*) als Platzhalter verwenden. Das Muster `env` entspricht beispielsweise den Umgebungen `env1`, `env2` und `env`.
1. Sie können Anwendungen auch manuell zum Geschäftsbereich hinzufügen, indem Sie auf die Option für **Einzeln zugeordnete
Anwendungen** klicken und anschließend auf die Option zum Hinzufügen von Anwendungen klicken.

Nach dem Einrichten Ihrer Geschäftsbereiche können Sie Diagramme filtern, um nur Anwendungen in bestimmten Geschäftsbereichen
anzuzeigen. Andere Diagramme zeigen Metriken, die auf Geschäftsbereichen basieren.

## Berichte erstellen

Zum Erstellen eines Berichts öffnen Sie {{site.data.keyword.DRA_short}}, klicken Sie auf **Delivery
Insights** und anschließend auf die Option für **Bericht hinzufügen**. Wenn die Option für **Bericht
hinzufügen** nicht angezeigt wird, sind Ihre IBM UrbanCode Deploy-Server nicht verbunden. Klicken Sie auf die Schaltfläche
'Einstellungen' und klicken Sie anschließend auf **Einrichten**, um eine Verbindung für Ihre Server herzustellen.

Aus dem Bericht heraus können Sie Karten zum Abschnitt **Metriken** hinzufügen, die Aktivität unter **Letzte Anwendungsaktivität** filtern und Diagramme zum Abschnitt mit den Berichtsdetails hinzufügen. Jedes Diagramm im Abschnitt mit den Berichtsdetails kann individuell gefiltert und angepasst werden. Um die Rohdaten hinter einem Diagramm zu sehen, klicken Sie oben rechts im Diagramm auf die Schaltfläche für die Einstellungen und dann auf **Berichtsdaten**.

Um die Reihenfolge der Diagramme zu ändern, klicken Sie oben rechts auf der Seite auf die Schaltfläche für die Einstellungen und anschließend auf **Diagrammlayout bearbeiten**. Sie können dann die Reihenfolge der Diagramme im Bericht durch Ziehen und Ablegen festlegen.

## Berichte gemeinsam nutzen
Standardmäßig werden nur die Delivery Insights-Berichte angezeigt. Sie können einen solchen Bericht mit anderen Benutzern in Ihrer Bluemix-Organisation gemeinsam nutzen. Um einen Bericht mit einer Person zu teilen, öffnen Sie den Bericht, klicken Sie oben rechts im Bericht auf die Schaltfläche für die Einstellungen und dann auf **Gemeinsam nutzen**.  

![Einen Bericht gemeinsam nutzen](images/uc_insights_sharing.gif).

## Prüfberichte erstellen

Prüfberichte zeigen eine vollständige Liste aller Aktivitäten, die den von Ihnen festgelegten Filtern entsprechen, im PDF-Format an. Klicken
Sie zum Erstellen eines Prüfberichts auf **Delivery Insights**, klicken Sie auf die Schaltfläche 'Einstellungen' und klicken
Sie anschließend auf die Option für **Prüfbericht erstellen**. Legen Sie dann die Informationen für den Bericht, einschließlich eines Namens, fest. Geben Sie zudem den Kontext für den Bericht an, beispielsweise für eine Anwendung, eine logische Umgebung oder eine Umgebung auf einem IBM UrbanCode Deploy-Server (eine physische Umgebung). Wählen Sie von hier aus die Daten aus, die im Bericht enthalten sein sollen, und klicken Sie auf **Erstellen**. 

## Fehlerbehebung
{: #troubleshooting}

Wenn viele Prozessanforderungen für Anwendungen und Komponenten in der IBM UrbanCode Deploy-Serverdatenbank gespeichert sind, können während des Abrufens Fehler auftreten. Dann wird eine Nachricht ähnlich der folgenden Nachricht im Ausgabeprotokoll des Servers aufgezeichnet:

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

Um dieses Verhalten zu umgehen, bearbeiten Sie die Datei `plugin.properties` für das Plug-in, um die Anzahl der Tage zu reduzieren, für die Daten abgerufen werden. Die Datei `plugin.properties` befindet sich im Verzeichnis `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` auf dem Computer, auf dem DevOps Connect installiert ist. Bearbeiten Sie die folgende Zeile, um das Nummernzeichen (#) zu entfernen und die Anzahl der Tage zu reduzieren:

`#numDaysToRetrieve=90`

Ändern Sie beispielsweise die Zeile in den folgenden Text, um nur Daten für die letzten 30 Tage abzurufen:

`numDaysToRetrieve=30`

Speichern Sie die Datei und führen Sie die Integration dann erneut aus. Überprüfen Sie die Serverprotokolle, um sicherzustellen, dass keine Fehler aufgetreten sind.
