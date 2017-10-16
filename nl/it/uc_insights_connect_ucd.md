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

# Visualizzazione dei dati dai server IBM UrbanCode Deploy
{: #connect_ucd}

Per visualizzare i dati da un server IBM UrbanCode Deploy in Delivery Insights, devi configurare un'istanza di DevOps Connect, devi installare una patch sul server e devi quindi connetterlo a DevOps Connect.
{:shortdesc}

## Prerequisiti
{: #prereqs}

Per visualizzare le informazioni dai tuoi server IBM UrbanCode Deploy in {{site.data.keyword.DRA_short}}, devi ospitare un'istanza di DevOps Connect su un sistema che può collegarsi ai tuoi server IBM UrbanCode Deploy. Questo sistema può essere un computer fisico o una macchina virtuale. 

Il sistema che ospita DevOps Connect deve avere i seguenti prerequisiti:
- Il sistema deve avere una Java Runtime Environment (JRE) alla versione 8 o successiva.
- La variabile `PATH` di sistema deve includere l'ubicazione della JRE.
- Il sistema deve consentire a DevOps Connect di creare le connessioni in uscita a IBM Bluemix.

Inoltre, il tuo server IBM UrbanCode Deploy deve essere alla versione 6.2 o successive.

## Configurazione del servizio {{site.data.keyword.DRA_short}}
{: #configure_service}

Se non hai il servizio {{site.data.keyword.DRA_short}}, aggiungilo:
1. Accedi a {{site.data.keyword.Bluemix}} e fai clic su **Servizi > Dashboard**.
1. Fai clic su **Crea servizio**.
1. Fai clic sul servizio {{site.data.keyword.DRA_short}}.
1. Seleziona un piano dei prezzi e fai clic su **Create**.
1. Fai clic su **Manage** e quindi, sotto "Gain insights into UrbanCode deployments", fai clic su **Start here**.
1. Nella finestra del template di toolchain, fai clic su **Create**.  
Delivery Insights crea una toolchain per la tua organizzazione. Le toolchain sono raccolte di integrazioni dello strumento, in questo caso IBM UrbanCode Deploy, e {{site.data.keyword.DRA_short}} fanno parte della tua toolchain. Per ulteriori informazioni sulle toolchain, vedi [Gestione delle toolchain](../ContinuousDelivery/toolchains_working.html).
1. Nella toolchain, fai clic sullo strumento IBM UrbanCode Deploy.
1. Fai clic sul pulsante delle impostazioni e quindi su **Setup**.

In futuro, puoi arrivare a {{site.data.keyword.DRA_short}} facendo clic su **Servizi > Dashboard** e selezionando la tua istanza del servizio {{site.data.keyword.DRA_short}}.

Se già disponi di una toolchain, puoi aggiungere gli strumenti IBM UrbanCode Deploy e {{site.data.keyword.DRA_short}} e accedere a Delivery Insights attraverso questi strumenti. Seleziona quindi lo strumento IBM UrbanCode Deploy, fai clic sul pulsante delle impostazioni e infine su **Setup**.

Ora puoi attenerti alle istruzioni nella pagina **Setup Instructions** per installare DevOps Connect e connetterlo a {{site.data.keyword.DRA_short}}, come descritto nella prossima sezione.

## Installazione di DevOps Connect e sua connessione a {{site.data.keyword.DRA_short}}
{: #install_connect}

1. Nella pagina **Setup Instructions**, segui i passi per configurare DevOps Connect e collegare i tuoi server IBM UrbanCode Deploy. Questi passi includono:
{: #set_up_connect}
  1. Configurare un sistema per eseguire DevOps Connect, come descritto in [Prerequisiti](uc_insights_connect_ucd.html#prereqs).
  1. Scaricare DevOps Connect, che viene fornito in un file JAR eseguibile.

  1. Se utilizzi un proxy per la connessione a Internet, imposta la variabile di ambiente `_JAVA_OPTIONS` sul seguente valore:
    * Se il proxy utilizza HTTPS, imposta `_JAVA_OPTIONS` su `-Dhttps.proxyHost=HOSTNAME -Dhttps.proxyPort=PORT`, dove `HOSTNAME` è il nome host del server proxy e `PORT` è la porta HTTPS del server proxy.
    * Se il proxy utilizza HTTP, imposta `_JAVA_OPTIONS` su `-Dhttp.proxyHost=HOSTNAME -Dhttp.proxyPort=PORT`, dove `HOSTNAME` è il nome host del server proxy e `PORT` è la porta HTTP del server proxy.

  1. Copia il comando dalla pagina **Setup Instructions**. Questo comando avvia DevOps Connect con un token che gli consente di connettersi alla tua organizzazione su {{site.data.keyword.Bluemix}}.
  1. Per impostazione predefinita, DevOps Connect viene eseguito sulla porta 8443, che è la stessa porta predefinita per l'esecuzione del server IBM UrbanCode Deploy. Pertanto, se il server IBM UrbanCode Deploy o qualsiasi altro servizio viene eseguito sulla porta 844s, cambia la porta per DevOps Connect aggiungendo il parametro `-Dserver.port` al comando. Ad esempio, per impostare DevOps Connect sulla porta 8888, l'inizio del comando è simile al seguente:  
```bash
java -Dserver.port=8888 -jar devops-connect-2.0.92clear0618.jar -Dserver.port=8888
```  

Il comando completo contiene informazioni sul tuo account Bluemix, che configura DevOps Connect automaticamente, come nel seguente esempio:

```bash
java -Dserver.port=8888 -jar devops-connect-2.0.920618.jar --sync.id=a2c12cb9-9a09-9832-479b01bf --sync.token=j0zs325U6qp080pzpcQ  --sync.registrar=jsmith@example.com
```

  1. Esegui il comando e attendi l'avvio di DevOps Connect.

  1. Connetti i tuoi server IBM UrbanCode Deploy a DevOps Connect, come descritto nella prossima sezione.

## Connessione dei server IBM UrbanCode Deploy a DevOps Connect
{: #connect_ucd_to_connect}

1. Se il tuo server IBM UrbanCode Deploy è precedente alla versione 6.2.5, installa una patch sul server. Le versioni 6.2.5 e successive non richiedono una patch.
  1. Scarica la patch corretta per la tua versione di IBM UrbanCode Deploy dalla seguente pagina. Ad esempio, il file di patch per IBM UrbanCode Deploy 6.2.4.x è denominato [ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/6_2_4_X/ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar).  
  
    [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Arresta il server. Consulta [Starting and stopping the server](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Posiziona il file di patch nella cartella <code><em>application_data</em>/patches</code>, dove <code><em>application_data</em></code> è la cartella dei dati dell'applicazione del server. La cartella dei dati dell'applicazione del server predefinita è `/opt/ibm-ucd/server/appdata` su Linux e `C:\Program Files\ibm-ucd\server\appdata` su Windows. Nei sistemi ad elevata disponibilità, la cartella dei dati dell'applicazione è sempre su un'unità di rete condivisa a cui può accedere ogni server.

  1. Facoltativo: mentre il server viene arrestato, per incrementare le prestazioni dell'importazione dei dati da questo server, immetti i seguenti comandi SQL sul database. Questi comandi non sono necessari per la versione 6.2.5 e successive.  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  Utilizza il nome del tuo database per `MyUCDDatabase`.
  
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Avvia il server. 

    **Nota:** potresti dover attendere più a lungo del normale per l'avvio del server IBM UrbanCode Deploy. Nel caso in cui il server non si avvii, o se non funziona correttamente, elimina i file di patch e procedi quindi a riavviarlo. I file di patch non influenzano in modo permanente il server.

1. Alcune versioni di IBM UrbanCode Deploy richiedono una patch aggiuntiva per il collegamento del server a DevOps Connect. Se stai utilizzando dalla versione 6.2 di IBM UrbanCode Deploy alla 6.2.1.2, devi installare la seguente patch aggiuntiva nel server:
  1. Scarica la the patch:  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Arresta il server.
  1. Posiziona il file di patch nella cartella <code><em>application_data</em>/patches</code>.
  1. Avvia il server.

1. Crea un'integrazione tra DevOps Connect e il server IBM UrbanCode Deploy:  

  **Importante:** la prima volta che esegui l'integrazione, DevOps Connect richiama i dati dei precedenti 90 giorni. Se hai una grande quantità di dati di distribuzione, questo processo può impiegare molto tempo. Per richiamare i dati per meno di 90 giorni, consulta [Risoluzione dei problemi](uc_insights_connect_ucd.html#troubleshooting).
  1. In IBM UrbanCode Deploy, crea un token di autenticazione. Consulta [Token](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. In DevOps Connect, fai clic su **Integrations** e su **Add New**.
  1. Specifica un nome e una descrizione per l'integrazione. L'ubicazione predefinita di DevOps Connect è `https://hostname:8443/`, dove `hostname` è il nome host del sistema che ospita DevOps Connect.
  1. Dall'elenco **Integration Type**, seleziona **IBM UrbanCode Deploy for Cloud Reporting**.
  1. Nel campo **Server URI**, immetti l'URL pubblico del server IBM UrbanCode Deploy, come ad esempio `https://my_UCD.example.com:8447`.
  1. Nel campo **Authentication Token**, immetti o incolla il token di autenticazione che è stato generato da IBM UrbanCode Deploy.
  1. Nel campo **Admin User**, immetti un elenco separato da virgole di ID IBM per fornire l'accesso all'interfaccia DevOps Connect.
  1. Facoltativo: fai clic su **Run Integration** per eseguire l'integrazione immediatamente. Per impostazione predefinita, le integrazioni sono eseguite ogni minuto.
  1. Fai clic su **Save**.

  ![Configurazione dell'integrazione in DevOps Connect](images/uc_insights_dc_integration.gif)

Ora i tuoi dati sono sincronizzati con Delivery Insights. Puoi ora creare e visualizzare i report che si basano su tali dati. Associa quindi gli ambienti sui tuoi server IBM UrbanCode Deploy agli ambienti logici in Delivery Insights.

## Associazione degli ambienti ai report
{: #mapping}

### Ambienti logici

Delivery Insights raggruppa i tuoi ambienti IBM UrbanCode Deploy (detti anche *ambienti fisici*) in uno o più ambienti logici. In questo modo puoi raccogliere gli ambienti in gruppi che abbiano senso per te e per la tua organizzazione. Ad esempio, se disponi di molti ambienti di produzione per molte applicazioni, puoi raggruppare tutti questi ambienti in un solo ambiente logico e combinare le metriche per tutti questi ambienti in un solo dashboard dell'ambiente di produzione. L'associazione avviene per stringa di ricerca, così puoi raggruppare gli ambienti in qualsiasi modo abbia senso per i tuoi server IBM UrbanCode Deploy.

### Ambienti logici predefiniti

Per impostazione predefinita, i tuoi report includono gli ambienti logici che corrispondono agli ambienti IBM UrbanCode Deploy utilizzando le stringhe. Ad esempio, tutti gli ambienti con "dev" nel nome sono associati all'ambiente logico DEV e tutti gli ambienti con "prod" all'ambiente logico PROD.

![Gli ambienti logici predefiniti](images/uc_insights_mapping.gif)

### Associazione degli ambienti agli ambienti logici

Puoi associare manualmente gli ambienti fisici agli ambienti logici o puoi utilizzare i modelli per associarli in modo dinamico.

Per associare gli ambienti fisici agli ambienti logici, segui questa procedura:

1. Apri Delivery Insights, fai clic sul pulsante delle impostazioni e seleziona **Map Environments**.
1. Nella pagina Environment Mapping, fai clic su un ambiente logico esistente o crea un ambiente logico facendo clic su **Add Logical Environment**.
1. Con un ambiente logico selezionato, puoi specificare i modelli per associare gli ambienti all'ambiente logico. In **Included Patterns**, fai clic su **Add Pattern** e specifica un modello da utilizzare. Tutti gli ambienti con i nomi che corrispondono al modello, inclusi gli ambienti che crei in seguito, vengono aggiunti all'ambiente logico. Puoi utilizzare l'asterisco (*) come carattere jolly. Ad esempio, il modello `env` corrisponde agli ambienti `env1`, `env2` e `env`.
1. Per associare gli ambienti logici manualmente, fai clic su **Add Manually** e seleziona gli ambienti da aggiungere o rimuovere.
1. Verifica che l'ambiente logico contenga gli ambienti che desideri.

![Configurazione dell'associazione dell'ambiente logico](images/uc_insights_mapping_manually.gif)

Ora che hai associato gli ambienti agli ambienti logici, puoi aggregare le informazioni di report in base a tali ambienti logici.

## Associazione di applicazioni alle linee di business
{: #lines}

Le linee di business sono gruppi di applicazioni che servono un comune scopo aziendale. Puoi associare le tue applicazioni alle linee di business per facilitare il filtraggio delle applicazioni nei grafici. Puoi anche creare grafici che si basano sulle linee di business.

Per impostare le linee di business (LOB), segui questa procedura:

1. In {{site.data.keyword.DRA_short}}, fai clic su **Delivery Insights**, fai clic sul pulsante delle impostazioni e quindi seleziona **Map Lines of Business**.
1. Nella pagina Lines of Business Mapping, fai clic su una LOB esistente o creane una immettendo un nome e facendo clic su **Create**.
1. Con una LOB selezionata, puoi specificare i modelli per associare le applicazioni alla LOB. In **Included Patterns**, fai clic su **Add Pattern** e specifica un modello da utilizzare. Tutte le applicazioni con i nomi che corrispondono al modello, incluse le applicazioni che crei in seguito, vengono aggiunte alla LOB. Puoi utilizzare l'asterisco (*) come carattere jolly. Ad esempio, il modello `env` corrisponde agli ambienti `env1`, `env2` e `env`.
1. Puoi anche associare le applicazioni alla LOB manualmente, facendo clic su **Individually Mapped Applications** e quindi su **Add Applications**.

Dopo aver configurato le LOB, puoi filtrare i grafici per visualizzare solo le applicazioni in determinate LOB. Gli altri grafici mostrano le metriche basate sulle LOB.

## Creazione dei report

Per creare un report, apri {{site.data.keyword.DRA_short}}, fai clic su **Delivery Insights** e seleziona **Add Report**. Se non vedi l'opzione **Add Report**, i tuoi server IBM UrbanCode Deploy non sono connessi. Fai clic sul pulsante delle impostazioni e quindi su **Setup** per connettere i tuoi server.

Dall'interno del report, puoi aggiungere le schede alla sezione **Metrics**, filtrare l'attività in **Recent application activity** e aggiungere i grafici alla sezione **Report Details**. Ogni grafico nella sezione **Report Details** è filtrabile e personalizzabile individualmente. Per visualizzare i dati non elaborati di un grafico, nella parte in alto a destra del grafico, fai clic sul pulsante delle impostazioni del grafico e quindi su **Report Data**.

Per modificare l'ordine dei grafici, nella parte in alto a destra della pagina, fai clic sul pulsante delle impostazioni e quindi su **Edit Chart Layout**. Adesso puoi trascinare e rilasciare i grafici per impostare l'ordine nel report.

## Condivisione di report
Per impostazione predefinita, puoi soltanto visualizzare i tuoi report Delivery Insights. Puoi condividere i report con altri utenti nella tua organizzazione Bluemix. Per condividere un report con qualcuno nella tua organizzazione Bluemix, aprilo e nella parte in alto ad destra, fai clic sul pulsante delle impostazioni e su **Share**.  

![Condivisione di un report](images/uc_insights_sharing.gif).

## Creazione dei report di controllo

I report di controllo visualizzano un elenco completo di tutte le attività che soddisfano i filtri che hai configurato, come un PDF. Per creare un report di controllo, fai clic su **Delivery Insights**, fai clic sul pulsante delle impostazioni e seleziona **Create Audit Report**. Quindi, specifica le informazioni per il report, incluso il nome. Inoltre, configura il contesto del report, come ad esempio un'applicazione, un ambiente logico o un ambiente su un server IBM UrbanCode Deploy (un ambiente fisico). Da lì, seleziona i dati da visualizzare nel report e fai clic su **Create**. 

## Risoluzione dei problemi
{: #troubleshooting}

In molti componenti e applicazioni, le richieste del processo sono archiviate nel tuo database del server IBM UrbanCode Deploy, si possono verificare degli errori durante il processo di richiamo. Viene registrato un messaggio simile al seguente nel log dell'output del server:

`ORA-01652: impossibile estendere il segmento temperatura da 128 nello spazio tabella TEMP`

Per risolvere questo problema, modifica il file `plugin.properties` del plugin per ridurre il numero di giorni validi dei dati da richiamare. Il file `plugin.properties` è nella directory `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` nel computer in cui hai installato DevOps Connect. Modifica la seguente riga per rimuovere il carattere del numero (#) e ridurre il numero di giorni:

`#numDaysToRetrieve=90`

Ad esempio, modifica la riga con il seguente testo per richiamare solo i precedenti 30 giorni validi di dati:

`numDaysToRetrieve=30`

Salva il file e quindi riesegui l'integrazione. Verifica i log del server per assicurarti per non si verifichi più l'errore.
