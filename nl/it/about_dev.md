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

# Informazioni su Developer Insights
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Developer Insights fornisce un modo completo di esplorare il rischio di sviluppo del tuo progetto. Puoi identificare i file con alta tendenza all'errore e ottenere una vista di conformità del progetto per le procedure DevOps.
{:shortdesc}

Dopo aver aperto {{site.data.keyword.DRA_short}} dalla tua toolchain, fai clic su **Developer Insights**. Da lì, puoi selezionare una categoria analitica per un approfondimento sulla base di codice del tuo progetto. Cosa ogni serie di dati indica può variare da team a team e puoi eseguire il drill down in ogni visualizzazione per supporto e assistenza. Puoi filtrare i dati in base alla data, così come a molti altri criteri.

## Categorie di dati
I dati che {{site.data.keyword.DRA_short}} utilizza per popolare il suo dashboard sono estratti automaticamente dal repository di controllo dell'origine del tuo team. Puoi ottenere ulteriori informazioni sul significato dei dati e su come puoi applicarli al tuo progetto facendo clic su **Information** o **Guidance** nei grafici delle procedure ottimali. Per ulteriori informazioni puoi anche esaminare le ricerche e i dettagli che fanno parte delle altre visualizzazioni.

### Procedure ottimali per lo sviluppatore

Developer Insights fornisce vari grafici che misurano il tuo progetto per buone procedure da sviluppatore e DevOps. Utilizza questa categoria per ottenere una vista di alto livello della maturità, integrità e efficienza del tuo progetto.

### Problemi

La categoria Problemi visualizza tutti i problemi di traccia del lavoro del tuo team in un solo posto. I problemi vengono automaticamente raggruppati per tipo, priorità e tag e possono essere visualizzati nel tempo.

Questi raggruppamenti di problemi possono essere diversi nel significato da team a team. Un team potrebbe voler sapere se molti elementi contrassegnati con tag per una release in particolare sono chiusi, mentre un altro team potrebbe non contrassegnare con tag le release e invece lavorare in base alla priorità di apertura del problema.  

### Commit

La categoria Commit visualizza tutti i commit del tuo team in un solo posto. I commit vengono automaticamente raggruppati in base al tipo, alla tag e alle modifiche riga. Puoi visualizzarli su un periodo di tempo da te scelto.

I commit indicano il contributo dei tuoi membri del team alla tua base di codice. Esamina i tuoi dati di commit per comprendere dove stanno venendo profusi gli sforzi storicamente e come puoi migliorare il bilanciamento dei carichi di lavoro dei tuoi membri del team.

### File

La categoria File visualizza quali file del tuo progetto sono i più impegnati. Sia tramite le modifiche riga o i commit o i difetti, questi dati indicano dove il tuo team è più attivo.

In generale, tenta di ridurre sia il numero di mani che toccano un file che la frequenza di modifica di tale file. Questo obiettivo potrebbe essere impossibile con alcuni file, come i file di configurazione comuni. Tuttavia, molti sviluppatori che effettuano molte modifiche allo stesso file contemporaneamente è un ricettacolo di problemi.

### Richieste di pull

La categoria Richieste di pull mostra le richieste di pull del tuo team in un solo posto. Viene eseguita una valutazione della tendenza all'errore delle richieste di pull utilizzando il machine learning.Puoi visualizzare rapidamente quali richieste di pull stanno aggiungendo del rischio alla tua base di codice.

Le richieste di pull visualizzano il lavoro che i membri del tuo team stanno tentando di unire nella tua base di codice. Esamina i tuoi dati di richiesta di pull per comprendere tutti i rischi ad essi associati e come puoi ridurre tali rischi in futuro.

## Filtro dell'estensione file

DevOps Insights ignora i file con queste estensioni:

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
