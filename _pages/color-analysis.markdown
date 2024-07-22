---
layout: home
title: "Analisi del colore"
# subtitle: ""
show_sidetoc: true
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/miro_b.jpg
header_title: "Analisi del colore"
vega: true
---

A cura di Giorgio Bellante

## Metodo

Come raccogliere i colori da uno spot televisivo? Quanti raccoglierne? Come catalogarli in un dataset strutturato? A
queste domande è stato risposto in questa maniera.

Lo spot è un video di durata breve, in genere di 30 secondi, spesso con numerosi tagli di montaggio che conferiscono
dinamicità. L’idea iniziale è stata perciò quella di individuare questi tagli per poi dividere il video in **clip
separate**.

### Le scene

A questo scopo è stata utilizzata la libreria Python **PySceneDetect**, uno strumento in grado rilevare i
cambiamenti di ripresa nei video (sia bruschi, sia con dissolvenze basate su soglia) e dividere questo in clip separate,
che sono state chiamate _scene_.

L’individuazione delle scene è avvenuta utilizzando la funzione di PySceneDetect `detect`.
Dopo svariati esperimenti, è stato individuato il miglior set di parametri che potesse essere adeguato per
la grande maggioranza degli spot.

Innanzitutto il taglio delle scene inizia 12 frame dopo l’inizio del video e termina 12 frame prima della fine. Questo
è servito per eliminare possibili fotogrammi neri dovuti alla pausa tra uno spot e l’altro.

<p class="caption">
Esempio di spot (Campari, 1990) con fotogrammi neri presenti all’inizio e alla fine
</p>
![Esempio di flusso video]({{site.baseurl}}/assets/images/color/video-stream.png)

In qualità di `detector` delle scene è stato utilizzato `AdaptiveDetector()` al quale è stato applicato il parametro
riguardante la durata minima delle scene (15 frame).

Sulla base della rilevazione delle scene è stata poi effettuata la divisione del video in clip e da queste
l’estrapolazione del **fotogramma mediano** (rappresentativo per la scena in cui si trova).

<p class="caption">
Lo spot è stato suddiviso in 13 scene di cui questi sono i fotogrammi mediani
</p>
![Le 13 scene del video]({{site.baseurl}}/assets/images/color/scenes.png)

I dati ottenuti da questa prima procedura sono i seguenti:

- `scene`
    - il numero identificativo della scena
- `scene_size`
    - la lunghezza della scena, misurata in fotogrammi
- `start_frame`
    - il numero del fotogramma di inizio
- `end_frame`
    - il numero del fotogramma di fine

Oltre a questi dati è stata salvata anche una miniatura del fotogramma di altezza pari a 180px.

### La palette colori

Da ogni fotogramma mediano è stata poi estrapolata una palette di 5 colori utilizzando la libreria Python `Pylette` che
utilizza un algoritmo K-Means per la rilevazione dei colori predominanti di un’immagine.

I dati ottenuti da questa seconda procedura sono una serie di 5 record relativi ai 5 colori estratti:

- `hex_color`
    - il colore in codice esadecimale
- `frequency`
    - la quantità normalizzata del colore
- `hue`
    - la componente _tonalità_ del colore
- `lightness`
    - la componente _luminosità_ del colore
- `saturation`
    - la componente _saturazione_ del colore

Al termine di questa procedura per ciascuno spot è stato salvato un file con estensione `.pal.csv` contenente le
feature summenzionate.

Questa è la rappresentazione in un grafico _Marimekko_ della palette colori dello spot Campari.

<p class="caption">
Il grafico è composto da 13 colonne (una per scena) sistemate da sinistra verso destra secondo il loro ordine. La
larghezza è proporzionale alla loro durata. Ogni colonna è poi composta da 5 rettangoli (uno per colore estratto dalla
scena) sistemati in verticale dal basso verso l’alto. La loro altezza è proporzionale alla frequenza all’interno della
scena. Ciascun rettangolo assume il colore che rappresenta.
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/color_charts/campari.marimekko.json" style="width: 100%; height:400px;"></vegachart>

{% include big-numbers-cards.html data="palette-processing" number="value" description="label" %}

## Arricchimento colori

Il processo di arricchimento colori è stato eseguito utilizzando due approcci distinti che prevede l’approssimazione
a due scale di colore. Il primo metodo si basa sui _Color meanings_ di Jacob Olesen, che suddivide **550 colori in 11
gruppi distinti**, fornendo una varietà cromatica ampiamente rappresentativa. Il secondo metodo impiega i **138 colori
CSS3**, riconosciuti dagli standard web. Questi metodi consentono una classificazione significativa delle
tonalità presenti nei video, rendendo possibile un’analisi dettagliata e comparativa dei colori utilizzati negli spot.

<p class="caption">
I 550 colori nominati
</p>
![550 colori]({{site.baseurl}}/assets/images/color/toyota-yaris-letter-box_.png)

<p class="caption">
CSS3 named colors
</p>
![CSS3 named colors]({{site.baseurl}}/assets/images/color/toyota-yaris-letter-box_.png)

## Calcolo tf-idf

Le palette di tutti gli spot sono state unite in unico grande dataset.

Ogni colore è stato mappato con il colore CSS3 più vicino.

Successivamente, è stato applicato il calcolo tf-idf per determinare il peso di ciascun colore CSS3 in relazione ai
singoli spot e all’intero set di spot: ogni CSS3 color (_termine_) è stato pesato rispetto allo spot (_documento_) e
rispetto alla totalità degli spot (_collezione di documenti_).

> `tf * log10( N / df)`

- `tf` è la frequenza del colore nello spot,
- `N` è il numero totale di spot nella collezione,
- `df` è il numero di spot in cui il colore appare.

Questo approccio consente di stilare una classifica dei colori predominanti in ogni spot, tenendo conto della loro
frequenza complessiva nel dataset. Tale metodo riduce l’importanza dei colori comuni (‘stopwords’), come il nero, spesso
utilizzato per l’effetto letter box o pillar box, assegnando loro un peso minore. In questo modo, l’analisi diventa più
precisa, evidenziando i colori davvero distintivi di ciascuno spot pubblicitario.

<p class="caption">
Toyota Yaris, 2006. Formato TV 4:3. Effetto 16:9
</p>
![Toyota Yaris, 2006]({{site.baseurl}}/assets/images/color/toyota-yaris-letter-box.png)


<p class="caption">
Sky Glass, 2023. Formato TV 16:9. Effetto 4:3
</p>
![Sky Glass, 2023]({{site.baseurl}}/assets/images/color/sky-glass-pillar-box.jpg)