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

# Integrazione di Deployment Risk Analytics con Continuous Delivery

Puoi instrumentare le pipeline di {{site.data.keyword.contdelivery_full}} per utilizzare le funzionalità di analisi di {{site.data.keyword.DRA_short}} Deployment Risk. Puoi quindi pubblicare i dati da questi lavori e aggiungere i gate che applicano le politiche di rischio.

Per una spiegazione di livello superiore dell'{{site.data.keyword.DRA_short}} analisi di Deployment Risk, consulta [Informazioni su Deployment Risk](./about_risk.html).

Per ulteriori informazioni sulle pipeline di Continuous Delivery, consulta [la documentazione ufficiale](../ContinuousDelivery/pipeline_working.html).

## Preparazione delle fasi e dei lavori della pipeline
{: #integrate_pipeline}

Per iniziare, devi instrumentare la tua pipeline per comunicare con {{site.data.keyword.DRA_short}}. Per farlo, definisci variabili di ambiente specifiche per tutti i lavori della tua pipeline che creano, testano o distribuiscono il codice. Devi anche aggiungere le variabili di ambiente per verificare i lavori che applicano le politiche di rischio utilizzando il tipo di tester Gate DevOps Insights.

* Record di build
* Record di distribuzione
* Risultati del test

I risultati del test devono fornire i dati in uno di questi formati supportati:

|     Tipo di test                 | Formati supportati                                               |
|------------------------------|-----------------------------------------------------------------|
|     Test di verifica funzionale  | Mocha, xUnit                                                    |
| Test di unità                    | Mocha, xUnit, Karma/Mocha                                       |
|     Copertura del codice         | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Scansione applicazione statica   | Scansioni dell'applicazione statica fornite da IBM Application Security on Cloud  |
| Scansione applicazione dinamica  | Scansioni dell'applicazione dinamica fornite da IBM Application Security on Cloud  |
| SonarQube                    | Dati di scansione forniti dalle scansioni di SonarQube                           |

Le variabili di ambiente che definisci nella pipeline forniscono il contesto per pubblicare questi record. Puoi definirle utilizzando il comando `export` negli script dei tuoi lavori. Puoi anche impostarle nel menu Proprietà ambiente delle fasi di ogni pipeline.

Variabili di ambiente:

| Variabile di ambiente  | Funzione | Richiesta in |
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | Il nome dell'applicazione nel dashboard. | Tutti i lavori che creano, testano, distribuiscono e applicano le politiche di rischio di {{site.data.keyword.DRA_short}}. |
| `BUILD_PREFIX`  | Testo che viene aggiunto come prefisso alle build della fase. Questo testo viene visualizzato anche nel dashboard.| Tutti i lavori che creano, testano, distribuiscono e applicano le politiche di rischio di {{site.data.keyword.DRA_short}}. |
| `LOGICAL_ENV_NAME`  | L'ambiente in cui viene eseguita l'applicazione. | Lavori di test e distribuzione.|

### Configurazione dei lavori di build

Per l'ultimo lavoro di build in una fase, imposta le variabili di ambiente per un nome applicazione e prefisso di build. Uno script di esempio potrebbe includere questi comandi:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Una volta completato questo lavoro di build, la pipeline pubblicherà un messaggio in {{site.data.keyword.DRA_short}} che indica che la build di SampleApp è stata completata.

### Configurazione dei lavori di distribuzione

Per l'ultimo lavoro di distribuzione nella fase, imposta un nome applicazione, un prefisso di build e un nome ambiente. Uno script di esempio potrebbe includere questi comandi:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Una volta terminato il lavoro di distribuzione, la pipeline pubblicherà un messaggio in {{site.data.keyword.DRA_short}} che indica che la build e l'applicazione specificate sono state distribuite in un ambiente.

### Configurazione dei lavori di test

Per tutti i lavori che producono risultati di test, imposta un nome applicazione e prefisso di build.

Se il lavoro genera risultati per i test di verifica funzionale (FVT), devi impostare anche il nome dell'ambiente logico in cui vengono eseguiti questi test.

Uno script di esempio potrebbe includere questi comandi:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

Assicurati che i nomi applicazione e gli ambienti corrispondano, dove opportuno. Ad esempio, potresti volere un lavoro di test di produzione che viene eseguito in una distribuzione della produzione per avere valori `LOGICAL_ENV_NAME` identici.

## Pubblicazione dei dati di test in DevOps Insights
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} utilizza i risultati di test dei tuoi lavori per generare report e applicare le politiche di rischio. Puoi pubblicare i dati di test da tutti i tuoi tipi di lavoro.

Ci sono due opzioni per pubblicare i risultati del test:

* Richiamare una semplice CLI (command-line interface) in uno script del lavoro.

* Aggiungere un lavoro di test con il tipo Advanced Tester alla tua pipeline.

Quando utilizzi il metodo Advanced Tester, non pubblichi i risultati del test utilizzando la CLI. Invece, tu specifichi la posizione del file dei risultati nel lavoro della pipeline e il lavoro carica i risultati non appena saranno disponibili.

Qualunque sia il metodo di pubblicazione che utilizzi, i risultati del test devono essere in uno dei formati supportati da {{site.data.keyword.DRA_short}}:

<table><thead>
<tr>
<th>Tipo di test</th>
<th>Formati supportati</th>
</tr>
</thead><tbody>
<tr>
<td>Test di verifica funzionale</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Test di unità</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Copertura del codice</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

### Pubblicazione dei dati di test da qualsiasi tipo di lavoro

In una pipeline, puoi utilizzare qualsiasi tipo di lavoro per eseguire un test. Una volta eseguito quel test, puoi caricare i risultati in {{site.data.keyword.DRA_short}}. I risultati vengono caricati richiamando una CLI nello script di shell del lavoro. 

Puoi caricare questi tipi di risultati del test dalla CLI:

* Test di unità
* Copertura del codice
* Test di verifica funzionale
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

Per ulteriori informazioni sul comando `idra`, vedi la [pagina del pacchetto grunt-idra3 su npm](https://www.npmjs.com/package/grunt-idra3). 

### Pubblicazione dei dati di test dai lavori Advanced Tester

Puoi aggiungere lavori di test con il tipo Advanced Tester a una pipeline. Una volta eseguiti, questi caricano automaticamente i propri risultati in {{site.data.keyword.DRA_short}}. 

1. Nella fase in cui vuoi aggiungere il lavoro che carica i risultati, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase pipeline](images/pipeline-stage-configuration-icon.png). Fai clic su **Configura fase**.
2. Crea un lavoro di verifica ed immetti un nome per esso. 
3. Per il tipo di lavoro, seleziona **Advanced Tester**.
4. Riempi i campi **Test Command** e **Working Directory** come preferisci per una lavoro di verifica di una pipeline normale. 
5. Riempi i campi rimanenti per caricare i risultati del test per un tipo di test particolare. 

 1. Scegli il tipo di metrica che corrisponde a quella definita nella politica {{site.data.keyword.DRA_short}} che desideri utilizzare.
 2. Immetti un'ubicazione del file del risultato. Questa ubicazione è relativa alla directory di lavoro. 

6. Se desideri caricare i risultati per un secondo tipo di test, riempi i campi con il prefisso *Ulteriori*.
7. Fai clic su **Salva** per ritornare alla pipeline.

La figura 1 mostra un lavoro di test configurato per eseguire i test di unità, per caricare i risultati nel formato Mocha e per caricare i risultati della copertura del codice nel formato Istanbul.

![Lavoro di caricamento DevOps Insights](images/insights_upload_job.png)
*Figura 1. Carica i risultati in DevOps Insights*



## Definizione dei gate
{: #configure_pipeline_gates}

I gate {{site.data.keyword.DRA_short}} verificano se i tuoi risultati di test soddisfano una politica definita. Se la politica non viene soddisfatta, il gate {{site.data.keyword.DRA_short}} ha un malfunzionamento per impostazione predefinita. Puoi inoltre configurare i gate per funzionare nella modalità advisory per consentire l'avanzamento della pipeline anche dopo un malfunzionamento.

Il dashboard Deployment Risk si basa sulla presenza di un gate dopo un lavoro di distribuzione di preparazione. Se desideri utilizzare il dashboard, assicurati di avere un gate dopo aver distribuito l'ambiente in fase di preparazione, ma prima di distribuire un ambiente di produzione.

Di solito, i gate sono posizionati prima della promozione della build nella tua pipeline. Queste ubicazioni sono ideali per controllare la qualità della build nelle tue politiche per assicurati che siano sicure da promuovere da un ambiente a un altro. Tuttavia, puoi posizionare i gate ovunque nella pipeline in cui desideri che venga controllato un criterio specifico. I gate che sono posizionati prima di distribuire un ambiente in fase di preparazione ancora utilizzeranno le politiche, ma non compariranno nel dashboard Deployment Risk.

1. In una fase, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase pipeline](images/pipeline-stage-configuration-icon.png) e fai clic su **Configura fase**.
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
