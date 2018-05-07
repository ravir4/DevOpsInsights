---

copyright:
  years: 2016, 2018
lastupdated: "2017-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrazione di Deployment Risk Analytics con Continuous Delivery

{{site.data.keyword.DRA_short}} tiene traccia del rischio di distribuzione in base ai dati del test che pubblichi su di esso. Questi dati possono includere i test di unità, la copertura del codice, i test di verifica funzionale, i dati SonarQube o i dati di scansione da IBM Application Security su Cloud. Dopo che hai pubblicato questi dati, puoi aggiungere dei gate alle tue pipeline in modo da poter arrestare le build che non soddisfano le politiche relative ai rischi.

Per una spiegazione di livello superiore dell'{{site.data.keyword.DRA_short}} analisi di Deployment Risk, consulta [Informazioni su Deployment Risk](./about_risk.html).

Per ulteriori informazioni sulle pipeline di Continuous Delivery, consulta [la documentazione ufficiale](../ContinuousDelivery/pipeline_working.html).

## Panoramica
{: #integrate_pipeline}

{{site.data.keyword.DRA_short}} richiede queste informazioni dalla tua pipeline per analizzare il rischio di distribuzione:

* Record di build
* Record di distribuzione
* Risultati del test

I risultati del test devono fornire i dati in uno di questi formati supportati:

| Tipo di test                    | Formati supportati                                               |
|------------------------------|-----------------------------------------------------------------|
| Test di verifica funzionale | Mocha, xUnit                                                    |
| Test di unità                    | Mocha, xUnit, Karma/Mocha                                       |
| Copertura del codice                | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Scansione applicazione statica              | Scansioni dell'applicazione statica fornite da IBM Application Security on Cloud  |
| Scansione applicazione dinamica             | Scansioni dell'applicazione dinamica fornite da IBM Application Security on Cloud |
| SonarQube                    | Dati di scansione forniti dalle scansioni di SonarQube                           |

Le variabili di ambiente che definisci nella pipeline forniscono il contesto per pubblicare questi record. Puoi definirle utilizzando il comando `export` negli script dei tuoi lavori. Puoi anche impostarle nel menu Proprietà ambiente delle fasi di ogni pipeline.

Variabili di ambiente:

| Variabile di ambiente  | Funzione | Richiesta in |
|-----------------------|-------- |-------------|
| `LOGICAL_APP_NAME`    | Il nome dell'applicazione nel dashboard. | Tutti i lavori che creano, testano, distribuiscono e applicano le politiche di rischio di {{site.data.keyword.DRA_short}}. |
| `BUILD_PREFIX`  | Testo che viene aggiunto come prefisso alle build della fase. Questo testo viene visualizzato anche nel dashboard. | Tutti i lavori che creano, testano, distribuiscono e applicano le politiche di rischio di {{site.data.keyword.DRA_short}}. |
| `LOGICAL_ENV_NAME`  | L'ambiente in cui viene eseguita l'applicazione. | Lavori di test e distribuzione. |

Assicurati di utilizzare queste variabili in modo congruente:

* Per una specifica applicazione, usa lo stesso `LOGICAL_APP_NAME` in tutti i lavori o in tutte le fasi. 
* Il valore `BUILD_PREFIX` deve essere lo stesso per una specifica applicazione e uno specifico tipo di build. Ad esempio, per le build dal ramo master, `BUILD_PREFIX` può essere `"master"`. 
* Utilizza lo stesso valore `LOGICAL_ENVIRONMENT_NAME` nei corrispondenti lavori di distribuzione e di test. Se utilizzi il valore `LOGICAL_ENVIRONMENT_NAME` di `"PRODUCTION"` in un lavoro di distribuzione, usa lo stesso valore quando pubblichi i risultati dai test che sono stati eseguiti anche in tale ambiente.

## Variabili di ambiente del lavoro di build

Per l'ultimo lavoro di build in una fase, imposta le variabili di ambiente per un nome applicazione e prefisso di build. Uno script di esempio potrebbe includere questi comandi:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Una volta completato questo lavoro di build, la pipeline pubblicherà un messaggio in {{site.data.keyword.DRA_short}} che indica che la build di SampleApp è stata completata.

## Variabili di ambiente del lavoro di distribuzione

Per l'ultimo lavoro di distribuzione nella fase, imposta un nome applicazione, un prefisso di build e un nome ambiente. Uno script di esempio potrebbe includere questi comandi:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Una volta terminato il lavoro di distribuzione, la pipeline pubblicherà un messaggio in {{site.data.keyword.DRA_short}} che indica che la build e l'applicazione specificate sono state distribuite in un ambiente.

## Variabili di ambiente del lavoro di test

Per tutti i lavori che producono risultati di test, imposta un nome applicazione e prefisso di build.

Se il lavoro genera risultati per i test di verifica funzionale (FVT), devi impostare anche il nome dell'ambiente logico in cui vengono eseguiti questi test.

Uno script di esempio potrebbe includere questi comandi:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

## Pubblicazione dei risultati del test
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} utilizza i risultati di test dei tuoi lavori per generare report e applicare le politiche di rischio.

In una pipeline, puoi utilizzare qualsiasi tipo di lavoro per eseguire un test. Una volta eseguito quel test, puoi caricare i risultati in {{site.data.keyword.DRA_short}}. I risultati vengono caricati richiamando una CLI nello script di shell del lavoro. 

Puoi caricare questi tipi di risultati del test dalla CLI:

* Test di unità
* Copertura del codice
* Test di verifica funzionale
* Risultati SonarQube
* Risultati della scansione dell'applicazione statica e dinamica da IBM Application Security on Cloud. 

Questo è uno script di esempio che esegue i test e quindi carica i risultati in {{site.data.keyword.DRA_short}}: 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

In tale esempio, il comando `idra` eseguito con l'indicatore `--publishtestresult` specifica che lo script eseguirà l'upload dei risultati. L'indicatore `--filelocation` indica l'ubicazione del file dei risultati del test relativamente alla directory root del lavoro. L'indicatore `--type` indica il tipo di test che vengono eseguiti.

Il comando `idra` supporta i seguenti valori `type`: 

| Tipo | Descrizione |
|------|-------------|
| `unittest` | Risultati del test di unità | 
| `fvt` | Risultati del test di verifica funzionale |
| `code` | Risultati della copertura del codice | 
| `sonarqube` | Risultati della scansione SonarQube | 
| `staticsecurityscan` | Risultati della scansione di sicurezza statica da IBM Application Security su Cloud |
| `dynamicsecurityscan` | Risultati della scansione di sicurezza dinamica da IBM Application Security su Cloud |

Per ulteriori informazioni sul comando `idra`, vedi la [pagina del pacchetto grunt-idra3 su npm](https://www.npmjs.com/package/grunt-idra3). 

## Definizione dei gate
{: #configure_pipeline_gates}

I gate {{site.data.keyword.DRA_short}} verificano se i tuoi risultati di test soddisfano una politica definita. Se la politica non viene soddisfatta, il gate {{site.data.keyword.DRA_short}} ha un malfunzionamento per impostazione predefinita. Puoi inoltre configurare i gate per funzionare nella modalità advisory per consentire l'avanzamento della pipeline anche dopo un malfunzionamento.

Il dashboard Deployment Risk si basa sulla presenza di un gate dopo un lavoro di distribuzione di preparazione. Se desideri utilizzare il dashboard, assicurati di avere un gate dopo aver distribuito l'ambiente in fase di preparazione, ma prima di distribuire un ambiente di produzione.

Di solito, i gate sono posizionati prima della promozione della build nella tua pipeline. Queste ubicazioni sono ideali per controllare la qualità della build nelle tue politiche per assicurati che siano sicure da promuovere da un ambiente a un altro. Tuttavia, puoi posizionare i gate ovunque nella pipeline in cui desideri che venga controllato un criterio specifico. I gate che sono posizionati prima di distribuire un ambiente in fase di preparazione ancora utilizzeranno le politiche, ma non compariranno nel dashboard Deployment Risk.

1. In una fase, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase pipeline](images/pipeline-stage-configuration-icon.png) e fai clic su **Configure Stage**.
2. Fai clic su **Aggiungi lavoro**. Per il tipo di lavoro, seleziona **Test**.
3. Per il tipo di tester, seleziona **Gate {{site.data.keyword.DRA_short}}**.
4. Specifica il nome dell'ambiente. Assicurati che questo valore corrisponda al valore che è stato definito nelle tue [proprietà di ambiente](#toolchain_pipeline_props).
5. Immetti il nome della politica da controllare in questo gate.

 Questo nome deve corrispondere esattamente a uno dei nomi della politica che hai definito. Puoi specificare solo politiche definite nella stessa organizzazione {{site.data.keyword.Bluemix_notm}} della tua toolchain.

6. Facoltativo: per passare una funzione gate ella modalità advisory, annulla la spunta della casella **Arrestare l'esecuzione di questa fase se il lavoro non riesce**. Nella modalità advisory, {{site.data.keyword.DRA_short}} completa le stesse analisi della politica nel gate e genera i report, ma se incontra un malfunzionamento, la pipeline non viene arrestata.
7. Fai clic su **Salva** per ritornare alla pipeline.
8. Configura i gate per tutte le politiche {{site.data.keyword.DRA_short}} ripetendo questi passi.

![Lavoro Deployment Risk Mocha](images/insights_gate_job.png)
*Figura 2. Gate DevOps Insights*

Dopo aver configurato la tua pipeline, inizia ad utilizzare {{site.data.keyword.DRA_short}}. 
