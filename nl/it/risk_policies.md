---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creazione di politiche e regole
{: #policies_and_rules}

Le politiche sono serie di regole che controllano i gate nella tua delivery pipeline. Se il tuo codice non soddisfa o supera una politica approvata in un gate particolare, la distribuzione viene arrestata per prevenire che vengano rilasciati dei rischi.

Definisci le politiche in {{site.data.keyword.DRA_short}}. Le politiche sono create nell'organizzazione (org) {{site.data.keyword.Bluemix_notm}} che contiene {{site.data.keyword.DRA_short}}. Tutte le applicazioni nella stessa organizzazione possono utilizzare la politica. 

## Creazione di politiche
{: #create_policies}

Per creare una politica:

1. Dal menu di navigazione {{site.data.keyword.DRA_short}}, fai clic su **Settings**.

2. Fai clic su **Policies**.

3. Fai clic su **Create Policy** e immetti quindi un nome e una descrizione per la nuova politica.

4. Fai clic su **Next**.

4. Aggiungi almeno una regola alla politica:
  1. Fai clic su **Add Rule to Policy**.
  2. Seleziona il tipo di regola.
  3. Immetti i dettagli e le condizioni per la regola.
  4. Fai clic su **Save**.

5. Quando ha terminato di aggiungere le regole alla politica, fai clic su **Complete**.

## Creazione di regole
{: #creating_rules}

Le regole definiscono i criteri che le tue politiche utilizzano per valutare un esito positivo o negativo. Potresti creare una politica "Unit Testing and Test Coverage" che contiene una regola di verifica dell'unità che richiede l'80% di esito positivo della verifica dell'unità e una regola di copertura del test che richiede il 100% di copertura di codice. Se aggiungi un gate che fa riferimento a questa regola in una pipeline, il gate previene a tutte le build che non soddisfano entrambe le regole di procedere. 

Puoi richiedere l'esito positivo indipendentemente se hai contrassegnato i test come critici. Per creare una regola, seleziona una politica e fai clic su **Add Rule to Policy**. 

### Creazione delle regole del test di verifica funzionale
{: #criteria_fvt}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di scenari di test che deve essere superata per essere considerata con esito positivo.

3. Definisci ogni scenario di test che è critico. Per determinare i nomi per lo scenario di test, vedi [Formati e strumenti per i risultati di test](#criteria_formats).

4. Per monitorare le regressioni dello scenario di test, seleziona la casella di spunta **Monitor for test case regression**.

5. Fai clic su **Save**.


### Creazione delle regole per i test di unità
{: #criteria_ut}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di scenari di test che deve essere superata per essere considerata con esito positivo.

3. Definisci ogni scenario di test che è critico. Per determinare i nomi per lo scenario di test, vedi [Formati e strumenti per i risultati di test](#criteria_formats).

4. Per monitorare le regressioni dello scenario di test, seleziona la casella di spunta **Monitor for test case regression**.

5. Fai clic su **Save**.


### Creazione delle regole di copertura del codice
{: #criteria_codecoverage}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di copertura del codice necessaria per essere considerato con esito positivo.

3. Per monitorare le regressioni di copertura del codice, seleziona la casella di spunta **Monitor for test case regression**.

4. Fai clic su **Save**.

### Creazione di regole di scansione sicura statica
{: #criteria_static}

Puoi integrare {{site.data.keyword.DRA_short}} con IBM Application Security on Cloud per eseguire le scansioni dell'applicazione dinamica e del codice statico. Per ulteriori informazioni su Application Security on Cloud, consulta [la documentazione ufficiale](/docs/services/ApplicationSecurityonCloud/index.html).

1. Immetti una descrizione.

2. Specifica i numeri massimi dei problemi di severità bassa, alta e media consentiti dalla regola. 

3. Fai clic su **Save**.

### Creazione di regole di scansione sicura dinamica
{: #criteria_dynamic}

Puoi integrare {{site.data.keyword.DRA_short}} con {{site.data.keyword.appseccloudfull}} per eseguire le scansioni dell'applicazione dinamica. Per ulteriori informazioni su Application Security on Cloud, consulta [la documentazione ufficiale](/docs/services/ApplicationSecurityonCloud/index.html).

1. Immetti una descrizione.

2. Specifica i numeri massimi dei problemi di severità bassa, alta e media consentiti dalla regola. 

3. Fai clic su **Save**.

## Formati e strumenti per i risultati di test
{: #criteria_formats}

Per i risultati di test, {{site.data.keyword.DRA_short}} supporta questi tipi di metriche e formati:

* Test di verifica funzionale (Mocha, xUnit)
* Test di unità (Mocha, xUnit, Karma/Mocha)
* Copertura del codice (Cobertura, lcov, Istanbul come formato del report di riepilogo json, Blanket.js)

{{site.data.keyword.DRA_short}} supporta inoltre i test Selenium e Jasmine. Questi test devono essere inclusi negli strumenti supportati ufficiali, come xUnit e Mocha. Per ulteriori informazioni sull'utilizzo contemporaneo di {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}} e Selenium, consulta [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Per gli elementi con scenari di test, puoi specificare gli scenari di test critici, che sono test che devono essere superati indipendentemente dalla percentuale accettabile. Il nome degli scenari di test critici devono corrispondere all'attributo `full title` dello scenario di test.    
* Per i test Karma/Mocha, le stringhe della descrizione `describe()` e `it()` sono collegate tra loro con gli spazi.
* Per i test xUnit, il nome del pacchetto e della funzione sono collegati tra loro con gli spazi. Ciò è riportato nel seguente esempio:
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  Questo esempio produce questi nomi di scenari di test:
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

Puoi utilizzare Sauce Labs con {{site.data.keyword.DRA_short}} aggiungendo l'integrazione dello strumento Sauce Labs alla tua pipeline. Quindi, incorpora le variabili di ambiente `SAUCE_USERNAME` e `SAUCE_ACCESS_KEY` nei test Selenium come credenziali.

Puoi visualizzare i titoli completi di tutti i test nei log dopo un'esecuzione.  

**Note:**
* {{site.data.keyword.DRA_short}} non supporta i test critici che contengono un trattino nel titolo completo.    
* Se modifichi il tuo nome dell'organizzazione, devi ricreare le politiche che sono state associate con il nome precedente. Perderai l'accesso a tutti i report di decisione generati prima della modifica del nome.
