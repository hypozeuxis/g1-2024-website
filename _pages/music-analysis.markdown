---
layout: home
title: "Analisi della musica"
# subtitle: ""
header_type: hero #base, post, hero,image, splash
header_img: assets/images/fantasy.jpg
header_title: "Analisi della musica"
vega: true
---

# Analisi della musica


Durante gli anni, la proporzione tra spot pubblicitari in cui la musica rappresenta una componente fondamentale 
dell'audio e quelli in cui la sua presenza è limitata, è rimasta pressoché costante.

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/music_lustrum.json" style="width: 100%"></vegachart>


# Analisi del genere musicale

### Analisi temporale

Effettuando un'analisi temporale del genere musicale negli spot televisivi, si nota a partire dagli anni ottanta fino 
ad oggi una progressiva riduzione nell’utilizzo della musica classica e 
della musica elettronica a favore della musica pop, che diventa nell’ultimo decennio il genere caratterizzante per 
oltre la metà degli spot televisivi. 

Il rock invece rappresenta sempre una frazione trascurabile mentre la musica di background ha un andamento piuttosto 
costante, essendo presente in circa uno spot su dieci in tutto il dataset.
Unica eccezione il lustro 2010-2014 in cui la musica di background mostra un aumento piuttosto significativo. 
In questi stessi anni, la musica rock rappresenta una percentuale ancora minore delle pubblicità. 

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/streamgraph.json" style="width: 100%"></vegachart>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/lustrum3.json" style="width: 100%"></vegachart>

### Analisi per classi di Nizza
Considerando le dieci classi di Nizza più frequenti nel nostro dataset, invece, è possibile osservare la distribuzione
dei generi musicali in base alla tipologia merceologica. Si osserva che la musica elettronica è presente in oltre la 
metà delle pubblcità per le classi di Nizza relative ad apparecchi scientifici e informatici (9), veicoli (12) e 
prodotti realizzati in carta (16).

Il genere pop risulta quello predominante invece per i prodotti per l'igiene (3) e farmaceutici (5), 
per le pubblicità dei giocattoli (28), per i prodotti alimenteri (29,30) e per i servizi di telecomunicazione (38).

(rock maggiore in 32 e 12)

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice_top10.json" style="width: 100%"></vegachart>

#### Veicoli (12)
Per gli spot pubblicitari dei veicoli, si osserva che la musica classica, un tempo abbastanza diffusa, è andata via
via diminuendo. Il rock invece ha raggiunto un picco di presenza negli anni a inizio duemila, in corrispondenza di 
un minimo per la musica elettronica, che è poi tornata ad essere negli ultimi anni il genere preponderante nelle 
pubblicità delle automobili.


<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice12.json" style="width: 100%"></vegachart>

#### Giocattoli (28)
La classe di Nizza relativa ai giocattoli è quella con la proporzione maggiore di musica pop e come si osserva dal 
grafico il suo aumento è stato piuttosto costante. Anche in questo caso, la musica classica è pian piano diminuita 
fino a scomparire del tutto negli ultimi venti anni. 



<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice28.json" style="width: 100%"></vegachart>

#### Generi alimentari (29 e 30)
Per le pubblicità relativi ai generi alimentari (classi 29 e 30) l'andamento del genere musicale è piuttosto simile, 
con un progressivo aumento della musica pop a discapito di quella elettronica. Per entrambe le classi di Nizza, 
il lustro 2010-2014 vede un impiego più ridotto della musica pop con un aumento della musica classica per la classe 30 
e di background per la classe 29.


<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice29.json" style="width: 100%"></vegachart>


<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice30.json" style="width: 100%"></vegachart>

#### Telecomunicazioni (38)
Le pubblicità relativi ai servizi di telecomunicazioni hanno un andamento caratteristico rispetto alle altre classi 
di Nizza, con una proporzione tra generi molto variabile da un lustro all'altro e con l'unica costante dell'assenza 
di musica rock. Il genere pop infatti ha avuto un periodo di massima rappresentazione, seguito da un calo e da una 
ripresa negli ultimi anni.


<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/nice38.json" style="width: 100%"></vegachart>