---
layout: home
title: "Analisi del testo"
# subtitle: ""
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/ghirigori.jpg
header_title: "Analisi del testo"
vega: true
---

## Dettagli tecnici
L’obiettivo del task di speech recognition è la trascrizione dei dialoghi e dei voiceover presenti negli spot televisivi in modo da poter effettuare la text analysis. Per il riconoscimento vocale abbiamo quindi testato diverse librerie. Whisper è emerso come il modello più adatto in quanto ha fornito le trascrizioni più accurate. 

**Whisper** è un’architettura transformer (encoder-decoder) sequence-to-sequence che estrae feature dall’ audio da cui genera il testo. È sviluppato da OpenAI ed è stato addestrato su vari task di elaborazione vocale tra cui il riconoscimento vocale multilingue, la traduzione vocale e l’identificazione della lingua. È dotato di cinque diversi modelli con precisione crescente nella trascrizione ma con un costo computazionale più elevato. Abbiamo testato in particolare i modelli small, medium e large e abbiamo individuato nel modello medium il compromesso ottimale tra efficienza e accuratezza. 


Uno dei problemi riscontrati è stato rappresentato dal fatto che Whisper può trascrivere erroneamente nomi propri non comuni come nomi di prodotti, aziende o persone. Il problema dell'errata trascrizione è stato risolto con l'aggiunta del parametro _initial_prompt_, che consente di fornire una lista di parole che verranno pronunciate, scritte con la giusta grafia. Come valore di questo parametro è stato quindi impostato il titolo dello spot televisivo e ciò ha permesso di ottenere una corretta trascrizione dei nomi dei prodotti commercializzati. 


Il parametro di Whisper _average log probability_ è stato utilizzato come indicatore dell’accuratezza della trascrizione poiché indica una misura di confidenza delle previsioni del modello. Ha valore negativo e più il valore è prossimo allo zero, più la trascrizione dovrebbe essere corretta. 
Dopo aver ottenuto le trascrizioni per il dataset completo, è  stata effettuata una seconda procedura di speech recognition per le pubblicità con _average log probability_ inferiore a -0,6 (circa 1200 spot). Questo valore era stato infatti  individuato come limite per poter considerare le trascrizioni come accurate. 
Si è passati poi a una fase di controllo e pulizia per la rimozione delle trascrizioni nulle, di quelle con caratteri non latini e delle frasi con allucinazioni del modello. 
In questo modo sono state ottenute 9400 trascrizioni adatte per l’analisi del testo. 

---

## Analisi delle trascrizioni

Ottenute le trascrizioni, abbiamo proseguito con le analisi dei testi.

### Analisi quantitative 
La prima analisi si è concentrata sul misurare la lunghezza media per lustro.
Dal grafico è possibile notare come ci sia un calo nel decennio 2000-2009. 

<p class="caption">
Lunghezza media delle trascrizioni per lustro
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_length_lustrum.json" style="width:100%"></vegachart> 

Le analisi sulla durata media degli spot confermano questo andamento. 
Anche in questo caso, infatti, si riscontra una riduzione della durata 
che coinvolge lo stesso decennio.

<p class="caption">
Durata media dei video per lustro
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/durata_media.json" style="width:100%"></vegachart> 

Adattandosi a un ritmo sempre più incalzante tipico degli ultimi quindici anni, 
il numero di parole per secondo aumenta a partire dal 2000, per poi diminuire negli ultimi cinque anni.
<p class="caption">
Numero di parole per secondo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/parole_secondo.json" style="width:100%"></vegachart> 

Anche il numero di scene per secondo aumenta nel corso dei lustri, la pubblicità sembra adattarsi a una società sempre più dinamica.
<p class="caption">
Numero di scene per secondo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/scene_sec.json" style="width:100%"></vegachart> 
Successivamente, la analisi sulla durata media delle trascrizioni è stata ripetuta ma considerando anche la classe di Nizza. In generale, sembra che la lunghezza media delle trascrizioni sia molto oscillante con picchi verso l'alto e verso il basso. Si può notare, inoltre, come ogni classe segua un proprio andamento indipendente.


<p class="caption">
Lunghezza media delle trascrizioni per lustro e classe di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_length.json" style="width:100%"></vegachart>  


### Topic
Come ulteriore analisi, sono stati ricercati i cosiddetti 'topic' più rilevanti divisi, ancora una volta, per lustro e classe di Nizza. 
Questa analisi permette di osservare l'eventuale insorgenza di parole chiave. 
Ad esempio, considerando la classe di Nizza 30, sotto la quale rientrano alcuni tipi di alimenti, è possibile notare come a partire dal 2020 emerge la parola 
'italiano'. Un simile aggettivo potrebbe essere emblematico della emergenza sanitaria dovuta al COVID.
Oppure, spostando l'attenzione sulla classe di Nizza 5 e sul lustro 2020-2024, si può evidenziare la comparsa del sostantivo 'ciclo'.
Questo topic diventa preponderante solo negli ultimi anni, in linea con i nuovi ideali e la maggiore sensibilità della società.
Un confronto fra le diverse classi di Nizza e i lustri mette, però, in evidenza la presenza quasi costante dell'aggettivo
'nuovo'.

<p class="caption">
Topic per lustro e classe di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_topic.json" style="width:100%"></vegachart>  


### Anglicismi
Infine, l'attenzione è stata rivolta all'eventuale presenza di anglicismi presenti negli spot pubblicitari. Dal grafico sembrerebbe emergere una tendenza altalenante fra periodi di apertura verso gli anglicismi, 
seguiti da periodi di maggiore chiusura. Inoltre, si nota come a partire dagli anni 2000
il numero di parole inglesi aumenti consistentemente, probabilmente anche per l'arrivo del canale MTV. 
Tuttavia, dal 2010 l'equilibrio cambia di nuovo, andando verso una diminuzione del numero di anglicismi per spot.

<p class="caption">
Numero di anglicismi per lustro
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_angl_lustrum.json" style="width:100%"></vegachart> 

# Clusterizzazione delle Trascrizioni
<p class="caption">
Metodo del gomito
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/cluster_charts_text/elbow_chart.json" style="width: 100%; height:640px;"></vegachart>

### Interpretazione
Osservando il grafico, si nota un significativo calo nella SSE inizialmente con l'aumento del numero di cluster, ma questo calo rallenta a un certo punto, creando una sorta di "gomito". In questo caso, il "gomito" appare chiaramente attorno al valore di 26 cluster. Questo punto rappresenta un buon compromesso tra la minimizzazione della SSE e l'evitare la sovrapartizione dei dati.
Il Silhouette Score aggiunge un ulteriore livello di comprensione, indicando la qualità del clustering. In generale, un Silhouette Score più alto indica cluster più distinti. Tuttavia, notiamo che il punteggio varia considerevolmente, suggerendo che la qualità dei cluster può variare.

<p class="caption">
Rappresentazione della Clusterizzazione delle Trascrizioni degli Spot con il t-SNE
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/cluster_charts_text/chart_cluster_text.json" style="width: 100%; height:640px;"></vegachart>

### Interpretazione

Il grafico sopra rappresenta la visualizzazione dei dati ridotti in due dimensioni usando il t-SNE. Ogni punto rappresenta un dato, con la posizione determinata dalle prime due componenti t-SNE.

Con 26 cluster, notiamo una distribuzione piuttosto dispersa dei punti. Alcuni cluster sono chiaramente distinti, mentre altri appaiono sovrapposti. Questo suggerisce che, mentre il numero di cluster scelto è ottimale secondo il Metodo dell'Elbow, la separabilità dei cluster potrebbe non essere perfetta.

La densità dei punti in alcune aree indica che ci sono gruppi ben definiti, ma la presenza di punti distanti suggerisce anche la presenza di cluster meno ben definiti.
Con 26 cluster, possiamo osservare una distribuzione abbastanza sparsa dei punti:

- Cluster Distinti: Alcuni cluster sono chiaramente separati, indicando gruppi di trascrizioni che condividono caratteristiche simili.
- Cluster Sovrapposti: In alcune regioni del grafico, i cluster appaiono sovrapposti, suggerendo che ci sono trascrizioni che potrebbero avere somiglianze con più di un cluster o che i confini tra i cluster non sono netti.
- Densità dei Punti: La densità varia tra le diverse aree del grafico. Aree con alta densità di punti indicano gruppi di trascrizioni molto simili tra loro, mentre le aree con punti più distanti possono indicare trascrizioni uniche o outliers.

### Conclusione 
 - In conclusione, il numero ottimale di cluster, come indicato dal Metodo dell'Elbow in questo esempio, è 26. Questa scelta bilancia efficacemente la riduzione degli errori e la qualità del clustering, fornendo una partizione ragionevole dei dati.
 - Il metodo di t-SNE fornisce una visione utile della struttura dei dati e dei risultati del clustering. Sebbene il numero di cluster scelto sia 26, è evidente che la qualità del clustering varia. Questo insight visivo è cruciale per comprendere meglio la distribuzione dei dati.
Alcuni cluster sono ben definiti, mentre altri potrebbero richiedere ulteriori dati per migliorare la distinzione.

