# Impatto delle Condizioni Meteorologiche sulla Qualità dell'Aria: Analisi Integrata

Questo progetto si concentra sull'analisi dell'impatto delle condizioni meteorologiche sulla qualità dell'aria nelle capitali europee. Integra dati meteorologici da Weather API e dati sulla qualità dell'aria da IQAir AirVisual API per fornire un'analisi completa delle interazioni tra clima e inquinamento atmosferico.

## Indice

1.  [Introduzione](#introduzione)
2.  [Acquisizione Dati](#acquisizione-dati)
3.  [Integrazione Dati](#integrazione-dati)
    * [Struttura del Processo di Integrazione](#struttura-del-processo-di-integrazione)
    * [Qualità dei Dati](#qualità-dei-dati)
    * [Metodologia di Integrazione](#metodologia-di-integrazione)
    * [Arricchimento dei Dati](#arricchimento-dei-dati)
    * [Sfide e Soluzioni](#sfide-e-soluzioni)
4.  [Memorizzazione Dati](#memorizzazione-dati)
5.  [Query](#query)
6.  [Conclusioni e Sviluppi Futuri](#conclusioni-e-sviluppi-futuri)
7.  [Fonti Dati](#fonti-dati)
8.  [Suddivisione del Lavoro](#suddivisione-del-lavoro)

## Introduzione

Il progetto mira ad analizzare i dati meteorologici e gli indici di qualità dell'aria delle capitali europee per comprendere come le variazioni climatiche possano influenzare direttamente i livelli di qualità dell'aria in queste città[cite: 5, 13]. Vengono utilizzati parametri come temperatura, umidità e modelli di vento per comprendere il contesto climatico più ampio[cite: 7]. Lo studio evidenzia l'importanza di comprendere l'interazione tra clima e inquinamento atmosferico, dato che il tempo può influenzare significativamente la dispersione degli inquinanti e gli alti livelli di inquinamento atmosferico hanno effetti negativi sulla salute pubblica[cite: 10, 11, 12].

## Acquisizione Dati

La fase di acquisizione dei dati è stata realizzata utilizzando due API distinte[cite: 16]:

* **Weather API**: utilizzata per raccogliere dati meteorologici (città, temperatura, condizione, umidità, velocità del vento) per 21 capitali europee[cite: 16, 17, 18, 19].
* **IQAir AirVisual API**: utilizzata per acquisire dati sulla qualità dell'aria (città, stato, paese, AQI, inquinanti)[cite: 19, 20, 21, 22].

Poiché le versioni gratuite di entrambe le API non offrono accesso a dati storici, è stato implementato uno script automatico che acquisisce quotidianamente i dati per costruire progressivamente un dataset storico integrato[cite: 22, 23, 24, 25].

## Integrazione Dati

L'integrazione dei dati è una fase cruciale per combinare efficacemente le informazioni meteorologiche e quelle sulla qualità dell'aria provenienti da fonti diverse[cite: 26].

### Struttura del Processo di Integrazione

Il processo si articola in tre fasi principali[cite: 28]:

* **Raccolta e armonizzazione dei dati giornalieri**: Acquisizione simultanea dei dati meteorologici e sulla qualità dell'aria con controlli di qualità immediati[cite: 29].
* **Creazione di archivi giornalieri**: I dati validati vengono salvati in file JSON giornalieri[cite: 30, 31].
* **Integrazione temporale dei dati**: I file giornalieri vengono combinati periodicamente in un unico file JSON per creare una base dati storica[cite: 32, 33].

### Qualità dei Dati

Durante l'acquisizione e l'integrazione, viene posta particolare attenzione alla verifica della qualità dei dati. Un processo di validazione controlla la completezza e la coerenza semantica, verificando la presenza di attributi specifici (città, temperatura, umidità, condizione atmosferica, velocità del vento per i dati meteorologici; città, regione, stato, AQI e inquinanti per la qualità dell'aria) e la validità dei tipi di dato e dei valori[cite: 34, 35, 36]. Solo i record che superano questi controlli sono inclusi nel dataset finale[cite: 37].

### Metodologia di Integrazione

La metodologia si basa su un approccio orientato ai documenti, creando un documento strutturato per ciascuna città e data che include entrambe le tipologie di informazioni[cite: 38, 39]. Vengono eliminate le ridondanze informative, come la duplicazione dei nomi delle città e dei timestamp non essenziali[cite: 40, 41, 42]. La struttura finale del documento integrato segue una gerarchia `data` → `città` → `dettagli`[cite: 43, 44].

### Arricchimento dei Dati

È stato implementato un sistema di categorizzazione dell'indice di qualità dell'aria (AQI) basato sugli standard internazionali dell'EPA (Environmental Protection Agency) americana. A ciascun valore di AQI viene associata una descrizione qualitativa (Good, Moderate, Unhealthy for Sensitive Groups, Unhealthy, Very Unhealthy, Hazardous) per facilitare l'interpretazione[cite: 46, 47].

### Sfide e Soluzioni

* **Sincronizzazione temporale**: Affrontata implementando un sistema di acquisizione simultanea dei dati da entrambe le fonti[cite: 48, 49, 81].
* **Limitazioni delle API**: Gestite con l'implementazione di un sistema di ritardo controllato tra le chiamate per evitare di superare i limiti imposti[cite: 50, 82].
* **Gestione delle inconsistenze**: Risolte implementando controlli di integrità e coerenza dei dati e meccanismi di retry per le chiamate fallite[cite: 52, 53, 83].

## Memorizzazione Dati

Per lo storage dei dati è stato scelto MongoDB, un database NoSQL, per la sua flessibilità, scalabilità e capacità di gestire grandi volumi di dati eterogenei e non strutturati[cite: 55, 56, 57]. MongoDB si basa sul modello BASE (Basic Availability, Soft State, Eventual Consistency), offrendo disponibilità continua e convergenza verso uno stato consistente[cite: 58, 59, 60, 61]. La struttura gerarchica `data` → `città` → `dettagli` ha facilitato l'accesso alle informazioni[cite: 78].

## Query

Sono state progettate diverse query sul database MongoDB per rispondere a domande specifiche relative alla variabilità dell'inquinamento atmosferico in relazione alle condizioni climatiche. Le query complesse sono state incapsulate in funzioni Python per migliorare l'usabilità[cite: 62, 63, 64].

Esempi di query:

* **Qualità dell'aria in una città e giorno specifici**: Restituisce l'indice AQI per una determinata città in una data specifica[cite: 65].
* **Correlazione tra temperatura e AQI**: Calcola la correlazione lineare tra temperatura e qualità dell'aria per tutte le capitali in un dato giorno[cite: 66].
* **Città più ventose del giorno**: Estrae le 5 città con la velocità del vento più elevata, visualizzando anche l'AQI[cite: 68].
* **Città con la peggiore qualità dell'aria**: Mostra le capitali con i peggiori valori di AQI in una data specifica[cite: 69].

Le interrogazioni supportano l'analisi esplorativa e forniscono insight utili sulle dinamiche tra clima e qualità dell'aria[cite: 71].

## Conclusioni e Sviluppi Futuri

Il progetto ha dimostrato la fattibilità e l'efficacia di un approccio sistematico per l'acquisizione, integrazione e analisi di dati da fonti eterogenee, costruendo un dataset storico integrato[cite: 73, 74]. La pipeline di acquisizione dati e i processi di qualità dei dati hanno garantito l'affidabilità delle informazioni[cite: 75, 76].

### Sviluppi futuri includono:

* **Espansione geografica e temporale**: Inclusione di altre città e dati storici più estesi[cite: 85, 86].
* **Integrazione di fonti dati aggiuntive**: Aggiunta di dati da sensori IoT, stazioni di monitoraggio governative, dataset satellitari, traffico veicolare, attività industriali e dati demografici[cite: 87, 88].
* **Analisi predittive e machine learning**: Sviluppo di modelli predittivi per la qualità dell'aria basati sulle condizioni meteorologiche previste[cite: 89, 90].
* **Analisi delle correlazioni avanzate**: Approfondimento delle analisi statistiche tramite tecniche multivariate, clustering spazio-temporale e identificazione di anomalie[cite: 91].

Il progetto ha dimostrato come l'integrazione di moderne tecnologie di data management, API esterne e database NoSQL possa creare sistemi informativi efficaci per l'analisi di fenomeni complessi[cite: 93].

## Fonti Dati

* **Fonte dati meteorologici**: [https://www.weatherapi.com/my/](https://www.weatherapi.com/my/) [cite: 4]
* **Fonte dati qualità dell'aria**: [https://www.iqair.com/it/](https://www.iqair.com/it/) [cite: 4]
* **Documentazione API Weather API**: [https://www.weatherapi.com/docs/](https://www.weatherapi.com/docs/) [cite: 4]
* **Documentazione API IQAir**: [https://api-docs.iqair.com/?version=latest](https://api-docs.iqair.com/?version=latest) [cite: 4]

## Suddivisione del Lavoro

* **Davide Fabio Loreti**: Data Integration, Data quality, Data Storage [cite: 4]
* **Carlo Pegoraro**: Data acquisition, Data enrichment, query [cite: 4]
