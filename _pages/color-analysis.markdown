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
