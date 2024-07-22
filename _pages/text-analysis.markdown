---
layout: home
title: "Analisi del testo"
# subtitle: ""
show_sidetoc: true
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/ghirigori.jpg
header_title: "Analisi del testo"
vega: true
---
A cura di: Denise Botrini e Oltiana Asllani

## Clusterizzazione delle Trascrizioni
Come primo task abbiamo tentato di raggruppare gli spot in base alle trascrizioni, scegliendo il numero
ideale di cluster secondo il cosiddetto metodo del 'gomito'. Il nostro intento era quello di trovare un numero di raggruppamenti 
inferiore alle quarantacinque classi di Nizza.
<p class="caption">
Metodo del gomito
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/cluster_charts_text/elbow_chart.json" style="width: 100%; height:300px;"></vegachart>

#### Interpretazione
Osservando il grafico, si nota un significativo calo nella SSE inizialmente con l'aumento del numero di cluster, ma questo calo rallenta a un certo punto, creando una sorta di "gomito". In questo caso, il "gomito" appare chiaramente attorno al valore di 26 cluster. Questo punto rappresenta un buon compromesso tra la minimizzazione della SSE e l'evitare la sovrapartizione dei dati.
Il Silhouette Score aggiunge un ulteriore livello di comprensione, indicando la qualità del clustering. In generale, un Silhouette Score più alto indica cluster più distinti. Tuttavia, notiamo che il punteggio varia considerevolmente, 
suggerendo che la qualità dei cluster può variare.

<p class="caption">
Rappresentazione della Clusterizzazione delle Trascrizioni degli Spot con il t-SNE
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/cluster_charts_text/chart_cluster_text.json" style="width: 100%; height:640px;"></vegachart>

#### Interpretazione

Il grafico sopra rappresenta la visualizzazione dei dati ridotti in due dimensioni usando il t-SNE. Ogni punto rappresenta un dato, con la posizione determinata dalle prime due componenti t-SNE.

Con 26 cluster, notiamo una distribuzione piuttosto dispersa dei punti. Alcuni cluster sono chiaramente distinti, mentre altri appaiono sovrapposti. Questo suggerisce che, mentre il numero di cluster scelto è ottimale secondo il Metodo dell'Elbow, la separabilità dei cluster potrebbe non essere perfetta.

La densità dei punti in alcune aree indica che ci sono gruppi ben definiti, ma la presenza di punti distanti suggerisce anche la presenza di cluster meno ben definiti.
Con 26 cluster, possiamo osservare una distribuzione abbastanza sparsa dei punti:

- Cluster Distinti: Alcuni cluster sono chiaramente separati, indicando gruppi di trascrizioni che condividono caratteristiche simili.
- Cluster Sovrapposti: In alcune regioni del grafico, i cluster appaiono sovrapposti, suggerendo che ci sono trascrizioni che potrebbero avere somiglianze con più di un cluster o che i confini tra i cluster non sono netti.
- Densità dei Punti: La densità varia tra le diverse aree del grafico. Aree con alta densità di punti indicano gruppi di trascrizioni molto simili tra loro, mentre le aree con punti più distanti possono indicare trascrizioni uniche o outliers.

#### Considerazioni
 - Il numero ottimale di cluster, come indicato dal Metodo del gomito in questo esempio, è 26. Questa scelta bilancia efficacemente la riduzione degli errori e la qualità del clustering, fornendo una partizione ragionevole dei dati.
 - Il metodo di t-SNE fornisce una visione utile della struttura dei dati e dei risultati del clustering. Sebbene il numero di cluster scelto sia 26, è evidente che la qualità del clustering varia. Questo insight visivo è cruciale per comprendere meglio la distribuzione dei dati.
   Alcuni cluster sono ben definiti, mentre altri potrebbero richiedere ulteriori dati per migliorare la distinzione.
 - Tuttavia, nonostante l'uso di modelli avanzati e del clustering basato su k-means, non abbiamo ottenuto i risultati sperati a causa del bias presente nelle classi. Questo suggerisce che le Classi di Nizza non sono sufficientemente rappresentative e che potrebbero essere necessari ulteriori dati per migliorare i risultati del clustering.
 - In conclusione, purtroppo, questa metodologia non ha funzionato come previsto, e abbiamo quindi deciso di utilizzare le Classi di Nizza. È importante considerare il bias nelle classi e l'importanza di dati adeguati per ottenere risultati di clustering più accurati.

## Analisi quantitative 
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

Adattandosi a un ritmo sempre più incalzante, 
il numero di parole per secondo aumenta a partire dal 2000, per poi diminuire negli ultimi cinque anni.
<p class="caption">
Numero di parole per secondo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/parole_secondo.json" style="width:100%"></vegachart> 

Successivamente, la analisi sulla durata media delle trascrizioni è stata ripetuta 
ma considerando anche la classe di Nizza ([Classificazione di Nizza](https://it.wikipedia.org/wiki/Classificazione_di_Nizza)). In generale, sembra che la lunghezza media delle trascrizioni sia molto oscillante con picchi verso l'alto e verso il basso. Si può notare, inoltre, come ogni classe segua un proprio andamento indipendente.


<p class="caption">
Lunghezza media delle trascrizioni per lustro e classe di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_length.json" style="width:100%"></vegachart>  


## Topic
Come ulteriore analisi, sono stati ricercati i cosiddetti 'topic' più rilevanti divisi, ancora una volta, 
per lustro e classe di Nizza ([Classificazione di Nizza](https://it.wikipedia.org/wiki/Classificazione_di_Nizza)). 
Questa analisi permette di osservare l'eventuale insorgenza di parole chiave. 
Ad esempio, considerando la classe di Nizza 30, sotto la quale rientrano alcuni tipi di alimenti, è possibile notare come a partire dal 2020 emerge la parola 
'italiano'. Un simile aggettivo potrebbe essere emblematico della emergenza sanitaria dovuta al COVID.
Oppure, spostando l'attenzione sulla classe di Nizza 5 e sul lustro 2020-2024, si può evidenziare la comparsa del sostantivo 'ciclo'.
Questo topic diventa preponderante solo negli ultimi anni, in linea con i nuovi ideali e la maggiore sensibilità della società.
Un confronto fra le diverse classi di Nizza e i lustri mette, però, in evidenza la presenza preponderante dell'aggettivo
'nuovo'.

<p class="caption">
Topic per lustro e classe di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_topic.json" style="width:100%"></vegachart>  


## Anglicismi
Infine, l'attenzione è stata rivolta all'eventuale presenza di anglicismi presenti negli spot pubblicitari. Dal grafico sembrerebbe emergere una tendenza altalenante fra periodi di apertura verso gli anglicismi, 
seguiti da periodi di maggiore chiusura. Inoltre, si nota come a partire dagli anni 2000
il numero di parole inglesi aumenti consistentemente rispetto al lustro precedente, probabilmente anche per l'arrivo del canale MTV. 
Tuttavia, dal 2010 l'equilibrio cambia di nuovo, andando verso una diminuzione del numero di anglicismi per spot.

<p class="caption">
Numero di anglicismi per lustro
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_angl_lustrum.json" style="width:100%"></vegachart> 


