---
layout: home
title: "Analisi della musica"
# subtitle: ""
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/fantasy.jpg
header_title: "Analisi della musica"
vega: true
---

## Dettagli tecnici

Tutti gli spot televisivi sono stati analizzati con **YAMNet**, una deep neural network che predice 521 classi di 
eventi audio. Dopo un campionamento a 16 KHz, per ogni video sono state memorizzate le cinque classi predette con 
maggiore confidenza dal modello. 

Un problema riscontrato consiste nel fatto che YAMNet è maggiormente efficiente nel riconoscimento di segmenti audio 
di breve durata. Avendo noi spot pubblicitari di lunghezza variabile spesso dava evidenti errori nei primi due 
risultati, garantendo tuttavia risultati attendibili per quelli successivi. Da qui la decisione di utilizzare le cinque classi predette con maggiore confidenza. 

Per la successiva analisi della musica, sono stati selezionati solo gli spot in cui una delle cinque classi predette 
era relativa a un genere o a uno strumento musicale.


L’analisi del genere musicale è stata effettuata con il modello **Musicnn**, che ha mostrato un’accuratezza migliore 
di YAMNet nella predizione. 
Musicnn è una rete neurale convoluzionale per la classificazione di eventi musicali. Predice cinquanta possibili classi,
comprendenti generi musicali (_classical_, _techno_, _rock_, ...), strumenti musicali (_piano_, _violin_, _electric 
guitar_, ...) e caratteristiche della musica (_slow_, _quiet_, _vocal_, ...). Questi tag sono stati raggruppati in 
cinque generi musicali: **classical, background, pop, rock** ed **electronic**. 

Musicnn è dotata di due modelli, MTT e MSD, allenati su due dataset differenti. Per l’analisi della musica negli spot 
televisivi, è stato preferito il modello MTT che ha fornito predizioni più accurate. 

Ogni video per cui YAMNet aveva rilevato suoni riconducibili a musica è stato quindi analizzato con Musicnn e sono
state salvate le tre classi con punteggio più elevato e per ogni spot è stato individuato il genere musicale 
predominante.

---

## Analisi dell'audio
La musica costituisce un aspetto fondamentale della comunicazione pubblicitaria televisiva e rappresenta uno dei canali 
principali per rendere il messaggio dello spot efficace e accattivante.  
Analizzare l’evoluzione temporale della musica della pubblicità italiana permette quindi di comprendere come le 
strategie di marketing siano cambiate.

Nel corso degli anni, il rapporto tra spot pubblicitari in cui la musica rappresenta una componente fondamentale 
dell'audio e quelli in cui la sua presenza è limitata, è rimasto pressoché costante.

<p class="caption">
Presenza di musica per lustro
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/music_lustrum_f.json" style="width: 100%"></vegachart>


## Analisi del genere musicale
### Analisi temporale

Effettuando un'analisi temporale del genere musicale negli spot televisivi, si nota a partire dagli anni Ottanta fino 
ad oggi una progressiva riduzione nell’utilizzo della musica classica e 
della musica elettronica a favore della musica pop, che diventa nell’ultimo decennio il genere caratterizzante per 
oltre la metà degli spot televisivi. 

Il rock invece rappresenta sempre una frazione trascurabile mentre la musica di background ha un andamento piuttosto 
costante, essendo presente in circa uno spot su dieci in tutto il dataset.
Unica eccezione il lustro 2010-2014 in cui la musica di background mostra un aumento piuttosto significativo. 
In questi stessi anni, la musica rock rappresenta una percentuale ancora minore delle pubblicità. 


<p class="caption">
Genere musicale per anno (grafico non normalizzato)
</p>


<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/streamgraph_f.json" style="width: 100%"></vegachart>

<p class="caption">
Genere musicale per lustro
</p>


<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/lustrum_f.json" style="width: 100%"></vegachart>

### Analisi per classi di Nizza


Considerando le dieci classi di Nizza più frequenti nel nostro dataset è possibile osservare la distribuzione
dei generi musicali in base alla tipologia merceologica. Si osserva che la musica elettronica è presente in oltre la 
metà delle pubblcità per le classi di Nizza relative ad apparecchi scientifici e informatici (classe 9), veicoli (12) e 
prodotti realizzati in carta (16).

Il genere pop risulta quello predominante per i prodotti per l'igiene (3) e farmaceutici (5), 
per le pubblicità dei giocattoli (28), per i prodotti alimentari (29,30) e per i servizi di telecomunicazione (38).

La musica rock invece rappresenta una frazione molto bassa degli spot televisivi e le classi per cui ha un valore 
maggiore sono quelle relative ai veicoli (12) e alle birre (32).

<p class="caption">
Genere musicale per Classe di Nizza
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice_top10_f.json" style="width: 100%"></vegachart>

Per completezza, si riporta la distribuzione dei generi musicali per tutte le classi di Nizza.

<p class="caption">
Genere musicale per Classe di Nizza
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice_all_f_2.json" style="width: 100%"></vegachart>



Si analizza nei grafici seguenti l'andamento dei generi musicali nel tempo per cinque classi di Nizza.



#### Veicoli (12)
Per gli spot pubblicitari dei veicoli, si osserva che la musica classica, un tempo abbastanza diffusa, è andata via
via diminuendo. Il rock ha raggiunto un picco di presenza a inizio duemila. Nello stesso periodo si nota 
un minimo per la musica elettronica, che è tornata ad essere negli ultimi anni il genere preponderante nelle 
pubblicità delle automobili.

<p class="caption">
Genere musicale per lustro per Classe di Nizza 12
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice12_f.json" style="width: 100%"></vegachart>

#### Giocattoli (28)
La classe di Nizza relativa ai giocattoli è quella con la proporzione maggiore di musica pop e come si osserva dal 
grafico il suo aumento è stato piuttosto costante. Anche in questo caso, la musica classica è pian piano diminuita 
fino a scomparire del tutto negli ultimi venti anni. 

<p class="caption">
Genere musicale per lustro per Classe di Nizza 28
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice28_f.json" style="width: 100%"></vegachart>

#### Generi alimentari (29 e 30)
Per le pubblicità relative ai generi alimentari (classi 29 e 30) l'andamento della musica è piuttosto simile, 
con un progressivo aumento della musica pop a discapito di quella elettronica. Per entrambe le classi di Nizza, 
il lustro 2010-2014 vede un impiego più ridotto della musica pop con un aumento della musica classica per la classe 30 
e di background per la classe 29.

<p class="caption">
Genere musicale per lustro per Classe di Nizza 29
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice29_f.json" style="width: 100%"></vegachart>

<p class="caption">
Genere musicale per lustro per Classe di Nizza 30
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice30_f.json" style="width: 100%"></vegachart>

#### Telecomunicazioni (38)
Le pubblicità dei servizi di telecomunicazioni hanno un andamento caratteristico rispetto alle altre classi 
di Nizza, con una proporzione tra generi molto variabile da un lustro all'altro e con l'unica costante dell'assenza 
di musica rock. Il genere pop infatti ha avuto un periodo di massima rappresentazione, seguito da un calo e da una 
ripresa negli ultimi anni.

<p class="caption">
Genere musicale per lustro per Classe di Nizza 38
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice38_f.json" style="width: 100%"></vegachart>


