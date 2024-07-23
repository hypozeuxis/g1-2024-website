---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: "Home"
header_title: "Spot TV"
subtitle: "La comunicazione pubblicitaria televisiva dal 1980 a oggi"
show_sidetoc: true
header_type: hero #base, post, hero, image, splash
header_img: assets/images/hero/vangogh.jpg
vega: true
---

Giunta ormai la fine di ‘Carosello’ il primo gennaio 1977, la pubblicità televisiva italiana moderna ha conosciuto un
discreto successo, rivelandosi un efficace mezzo di comunicazione attraverso cui le aziende potevano mettersi
direttamente in contatto con i telespettatori. Non vi era tuttavia solo una dimensione economica, infatti ci possiamo
ricordare di spot divertenti o di quelli più toccanti, che rimanevano impressi non per quello che vendevano, ma per le
emozioni che ci facevano provare. Come dimenticare l’incontro sotto la pioggia fra un povero gattino smarrito e una
dolce bambina nella pubblicità della Barilla? A chi non è mai capitato di ricordare i famosi ‘Pennelli Cinghiale’?

## Da Carosello alla pubblicità moderna

In quegli anni la televisione passa da avere uno scopo pedagogico-didascalico tipico degli anni ’60 a quello di puro
intrattenimento che la ha caratterizzata fino agli anni 2000. Era una novità, sia per chi guardava la televisione, sia
per chi ideava queste sequenze di immagini: non vi erano molte regole e si potevano rappresentare scene narrative avendo
come unico limite (o quasi) l’immaginazione. Se però pensiamo a quanto fossero diverse le pubblicità di un tempo
rispetto a quelle che siamo abituati a vedere oggi, ci chiediamo cosa sia accaduto. «A partire dagli anni 2000 c’è
un’inversione di rotta, si adotta lo stile MTV. La pubblicità si fa più ammiccante, caratterizzata da immagini
sovraesposte e dal ritmo sempre più incalzante \[…\] gli spot degli anni 2000 non suscitano le stesse emozioni dei
precedenti». Così commenta Michele Logrippo, fondatore del sito _Spot80_, quando gli chiediamo che cosa sia cambiato
rispetto agli anni ’80.

La nostra ricerca nasce dall’idea di indagare l’evoluzione della pubblicità televisiva andata in onda in Italia dagli
anni ’80 a oggi. Partendo dagli spunti di riflessione suggeriti da Logrippo durante l'intervista, abbiamo
voluto ricercare gli elementi che caratterizzano la pubblicità degli anni 2000 e la differenziano dal passato.
A tale scopo, abbiamo raccolto gli spot dal sito sopra indicato, _Spot80_, e
da diversi canali YouTube. I dati sono stati ordinati all’interno di un dataset in base al loro id, al titolo, alla
descrizione e all’anno di pubblicazione.
Successivamente, gli stessi sono stati arricchiti. Basandoci sulla classificazione di Nizza, ovvero un sistema di
categorizzazione internazionale per la registrazione di prodotti e servizi,
abbiamo associato a ciascuno spot la relativa classe. In aggiunta, non avendo una distribuzione dei dati che riuscisse a
coprire in
maniera omogenea tutti gli anni della nostra ampia finestra temporale, abbiamo deciso di raggrupparli in base ai lustri.
Tale scelta è
risultata molto proficua, permettendoci di ottenere una distribuzione più consistente degli spot lungo l'asse temporale.
Una volta puliti e preparati i dati, abbiamo eseguito le analisi che presentiamo qui di seguito.

## Musica pop per spot popolari

La musica costituisce un aspetto fondamentale della comunicazione pubblicitaria televisiva e rappresenta uno dei canali
principali per rendere il messaggio dello spot efficace e accattivante.  
Analizzando l’[evoluzione temporale](music-analysis#analisi-temporale) della musica si osserva, a partire dagli anni
Ottanta fino a oggi, una progressiva riduzione nell’impiego della musica classica ed elettronica.
Il rock ha da sempre caratterizzato una frazione esigua degli spot mentre la musica di background ha un andamento
piuttosto costante, essendo presente in circa uno spot su dieci del nostro dataset.
Si nota anche come la musica pop aumenti progressivamente fino a diventare nell’ultimo decennio il genere
caratterizzante per oltre la metà degli spot televisivi.

<p class="caption">
Genere musicale per lustro
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/new_charts/lustrum_f_22.json" style="width: 100%"></vegachart>

Il genere pop risulta, in tutto l'arco temporale considerato, la scelta
predominante per diverse classi di [Nizza](music-analysis#analisi-per-classi-di-nizza) tra cui i prodotti farmaceutici,
i giocattoli, i generi alimentari e i servizi di telecomunicazione.

|     **Prodotto**      | **Percentuale di musica pop** |
|:---------------------:|:-----------------------------:|
| Prodotti farmaceutici |              48%              |      
|      Giocattoli       |              60%              | 
|   Generi alimentari   |              45%              |
|   Telecomunicazioni   |              55%              |

Per le pubblicità dei [veicoli](music-analysis#veicoli-12), in controtendenza con la diffusione del genere pop,
la musica elettronica sta tornando a essere la scelta più gettonata dopo aver raggiunto il minimo di occorrenze tra il
2005 e il 2009. In accordo con l'andamento generale, invece, la progressiva scomparsa della musica classica.

<p class="caption">
Genere musicale per lustro per le pubblicità dei veicoli
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/new_charts/nice12_f_22.json" style="width: 100%"></vegachart>

## Parole, parole, parole...

In questa sezione ci siamo concentrati sull'analizzare le trascrizioni estrapolate dai nostri dati.
Sulla scia delle nuove tendenze portate in auge da MTV, si nota, in primo luogo, un progressivo aumento delle parole
inglesi negli
spot, dopo il calo registrato verso la fine degli anni ’90.
Tuttavia, la rivendicazione della nostra italianità continua a manifestarsi attraverso una seconda e rapida diminuzione
di queste negli ultimi quindici anni.

<p class="caption">
Numero di anglicismi per lustro
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_angl_lustrum.json" style="width:100%"></vegachart> 


Anche le semplici parole sembrano non essere mai casuali. «Assistiamo a un ribaltamento di ciò che la società considera
scandaloso: negli anni Ottanta e Novanta erano facilmente concesse battutine sessuali e di genere, ma non si potevano
assolutamente pronunciare determinate parole. Se ci pensate, oggi, è esattamente il contrario», continua Logrippo.
Effettivamente, la nostra analisi dei testi mostra che nelle pubblicità sugli assorbenti, ad esempio, la parola ‘ciclo’
inizia a essere usata con una frequenza piuttosto elevata solo dal 2020. Oppure, risulta emblematico il caso
dell’aggettivo ‘italiano’ che, dal 2015, compare timidamente fra le parole più frequenti negli spot di prodotti
alimentari,
per poi rivelarsi il topic più rilevante a partire dal 2020.
Il _Made in Italy_ sembra diventare un requisito fondamentale proprio in questi anni successivi alla pandemia mondiale.

| **Prodotto**          | **Parola** | **Lustro** | **Rilevanza** |
|:----------------------|:----------:|-----------:|:-------------:|
| Prodotti farmaceutici |   ciclo    |  2020-2024 |     8.43      |
| Generi alimentari     |  italiano  |  2015-2019 |     4.34      |
| Generi alimentari     |  italiano  |  2020-2024 |     13.39     |

Una dimensione che, invece, risulta essere in continua crescita è il ritmo degli spot. Non solo quest’ultimo aumenta
considerevolmente
nel passaggio fra gi anni ’90 e i primi 2000, come ricordato anche dal nostro intervistato, ma la sua dinamicità
continua
ad aumentare fino agli ultimi cinque anni.
Infatti è possibile notare come il numero medio di scene per secondo aumenti ogni lustro, suggerendo spot
pubblicitari sempre più frenetici. Oltre a ciò anche il numero di parole per secondo aumenta nel corso dei lustri,
anche se negli ultimi cinque anni vi è stato un calo che ha riportato il numero di parole per secondo allo stesso
di dieci anni fa.

<p class="caption">
Numero di scene medio per secondo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/scene_sec.json" style="width:100%; height:400px;"></vegachart>

<p class="caption">
Numero di parole per secondo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/parole_secondo.json" style="width:100%; height:400px;"></vegachart>

## I colori

Per quanto riguarda i colori si nota come questi siano passati dall’essere molto saturi e ad alto contrasto negli anni
Ottanta e Novanta a esserlo invece meno dalla metà del 2000 in poi. Un motivo potrebbe essere quello tecnologico: la
trasmissione delle immagini da parte delle emittenti è passata da una tecnologia analogica (soggetta quindi a disturbo e
ad alterazione del segnale) a una digitale (in cui disturbo e alterazione non sussistono). Un altro motivo è poi dato
dal mezzo di ricezione e di quello di registrazione che hanno ulteriormente contribuito a deteriorare qualità e colore
dell’immagine.

Ci teniamo a precisare che in ogni caso il nostro studio si focalizza proprio sui colori percepiti dall’utente finale
attraverso i mezzi di ciascuna epoca (e non su quelli originali degli spot, cui non abbiamo accesso).

## Dagli anni 80 a oggi, chi sono i protagonisti

Ulteriore aspetto che è stato preso in considerazione in queste analisi è stato _chi_ e _cosa_ effettivamente comparisse
negli spot. Va infatti preso in considerazione anche chi sono i principali personaggi dei brevi sipari che ci fanno
compagnia
mentre guardiamo la televisione. Un elemento che spicca immediatamente è la pervasiva presenza delle persone: benché
possa sembrare scontato infatti, la preponderanza di esseri umani è assoluta in ogni epoca analizzata.

| Classe     | Occorrenze |
|------------|------------|
| persona    | 3845       |
| automobile | 762        |
| bottiglia  | 758        |
| tazza      | 565        |
| cravatta   | 534        |

La spiegazione di questo è banale, in quanto se la pubblicità si prefigge di influenzare il comportamento delle persone,
è indubbio che
vedere altre persone come protagoniste ottenga un maggior effetto. Osserviamo trend particolari se invece si prendono in
considerazione altri elementi: analizzando le 10 categorie di oggetti più osservati, infatti, si nota come automobili e
bottiglie (prevalentemente di alcolici) conquistino le prime
posizioni, [osservando](entity-analysis#analisi-delle-classi-di-yolo) le prime dominare la classifica a
partire dagli anni 2000 fino a oggi. Altri oggetti degni di nota sono le sedie (osservabili in svariati contesti), le
quali hanno avuto un progressivo aumento, arrivando a essere rappresentate con una frequenza sette volte più alta oggi,
rispetto al loro esordio.

Le analisi si sono inoltre concentrate sullo studio delle classi
di [Nizza](entity-analysis#analisi-delle-classi-di-nizza), valutando la loro rappresentazione nel tempo:
tra le classi più rappresentate si possono osservare la 12 (veicoli e apparecchi per il trasporto di persone o merci via
terra, aria o acqua) e la 21 (piccoli utensili e apparecchi a mano per uso domestico e da cucina).
Mostrare queste informazioni può essere utile per comprendere meglio l’evoluzione della pubblicità nel tempo, favorendo
lo sviluppo di nuovi sistemi comunicativi, che facciano maggior presa su di un pubblico più bisognoso di stimoli rapidi
e nuovi; va inoltre considerata l’utilità che queste informazioni possono avere per coloro che desiderano ricoprire un
ruolo competitivo nell’ambito pubblicitario, costretti a fronteggiare una concorrenza in continua evoluzione.

## Conclusioni

Il nostro progetto vuole diventare un utile strumento di supporto e di ricerca per un pubblico di esperti e di
appassionati. Più precisamente, fra i probabili interessati possono rientrare: professionisti della comunicazione,
pubblicitari, sociologi, video-maker, designer, ma anche i più curiosi. Il nostro strumento, infatti, può fornire una
analisi della pubblicità e della sua evoluzione nel tempo per i più esperti, migliorando l’efficacia delle campagne
pubblicitarie; ma, allo stesso tempo, può offrire, a chi volesse semplicemente saperne di più, la possibilità di
approfondire un tema facente parte della nostra cultura.

A valle della nostra analisi, inoltre, è stato progettato un [prototipo di motore di ricerca](search)
che consente di consultare un dataset di spot pubblicitari per marchio e tipologia di prodotto,
in modo da poter accelerare eventuali indagini mirate.

In generale, dalle nostre analisi, è emerso quanto la pubblicità sia un settore
dinamico e incostante. I nostri risultati, infatti, 
sono contraddistinti da aspetti mutevoli e difficili da inquadrare, e
solo in rari casi siamo riusciti a individuare tendenze chiare e precise. 
Eppure, non ci sentiamo di affermare di non aver raggiunto il nostro scopo.
Seppur con delle difficoltà, studiando i diversi livelli di comunicazione abbiamo trovato, almeno in parte,
elementi che distinguono la pubblicità contemporanea da quella passata. Sicuramente, la separazione fra
ieri e oggi non è così netta come ci aspettavamo, o meglio, così non appare dalle nostre analisi.
Tuttavia, non si può dire che non ci sia un graduale cambiamento nel corso degli anni.
Infine, è doveroso sottolineare che le nostre conclusioni rimangono parziali,
pertanto non possono, e non vogliono, spiegare la totalità del fenomeno indagato. 

