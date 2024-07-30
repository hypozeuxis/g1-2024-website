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

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(128px, 1fr)); gap: 0.5rem;">
    <img src="{{site.baseurl}}/assets/images/home/barilla-soggetto-gattino-1986.png" alt="Barilla, 1986">
    <img src="{{site.baseurl}}/assets/images/home/cinghiale.png" alt="Cinghiale, 1983">
    <img src="{{site.baseurl}}/assets/images/home/dash.png" alt="Dash, 1986">
    <img src="{{site.baseurl}}/assets/images/home/ferrero-rocher.png" alt="Ferrero Rocher, 1991">
</div>

## Da Carosello alla pubblicità moderna

In quegli anni la televisione passa da avere uno scopo pedagogico-didascalico tipico degli anni ’60 a quello di puro
intrattenimento che la ha caratterizzata fino agli anni 2000. Era una novità, sia per chi guardava la televisione, sia
per chi ideava queste sequenze di immagini: non vi erano molte regole e si potevano rappresentare scene narrative avendo
come unico limite (o quasi) l’immaginazione. Se però pensiamo a quanto fossero diverse le pubblicità di un tempo
rispetto a quelle che siamo abituati a vedere oggi, ci chiediamo cosa sia accaduto. «A cavallo fra gli anni 90 e gli anni 2000 c’è
un’inversione di rotta, si adotta lo stile MTV. La pubblicità si fa più ammiccante, caratterizzata da immagini
sovraesposte e dal ritmo sempre più incalzante \[…\] gli spot degli anni 2000 non suscitano le stesse emozioni dei
precedenti». Così commenta Michele Logrippo, fondatore del sito _Spot80_, quando gli chiediamo che cosa sia cambiato
rispetto agli anni ’80.

<div style="display: grid; grid-template-columns: 1fr 1fr 1fr 1fr; gap: 0.5rem;margin: 1rem 0;">
    <img src="{{site.baseurl}}/assets/images/home/bistefani.png" alt="Bistefani">
    <img src="{{site.baseurl}}/assets/images/home/mastro-lindo.png" alt="Mastro Lindo">
    <img src="{{site.baseurl}}/assets/images/home/mulino-bianco.png" alt="Mulino Bianco">
    <img src="{{site.baseurl}}/assets/images/home/tabu.jpg" alt="Tabù">
</div>

La nostra ricerca nasce dall’idea di indagare l’evoluzione della pubblicità televisiva andata in onda in Italia dagli
anni ’80 a oggi. Partendo dagli spunti di riflessione suggeriti da Logrippo durante l’intervista, abbiamo
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
risultata molto proficua, permettendoci di ottenere una distribuzione più consistente degli spot lungo l’asse temporale.
Un ulteriore raggruppamento è stato fatto sulla durata degli spot. I nostri spot infatti avevano una durata che andava
dai 3 ai 254 secondi, pertanto abbiamo deciso di suddividerli in intervalli. Le principali durate degli spot sono
10, 15, 20, 30 e 35 secondi. Come riportato nel grafico sottostante è possibile notare come inizialmente la durata degli
spot fosse tipicamente di 35 secondi, lunghezza che è andata man mano scemando nel tempo, facendo spazio a spot
della durata di 30 e 15 secondi. Infine negli ultimi quindici anni c’è stata una durata degli spot della durata
compresa tra i 18 e 27 secondi, accompagnata da una diminuzione degli spot di 30 secondi nel corso degli ultimi dieci
anni.
La scelta di utilizzare intervalli di tempo è dovuta al fatto che spesso gli spot avevano subito tagli non perfetti
durante i ricaricamenti da parte degli utenti e potevano dunque differire di pochi secondi rispetto alla lunghezza
degli spot orginali.
Una volta puliti e preparati i dati, abbiamo eseguito le analisi che presentiamo qui di seguito.

<p class="caption">
Distribuzione della durata degli spot per lustro
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/intervalli_lustro.json" style="width: 100%; height:400px"></vegachart>

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

Il genere pop risulta, in tutto l’arco temporale considerato, la scelta
predominante per diverse classi di [Nizza](music-analysis#analisi-per-classi-di-nizza) tra cui i prodotti farmaceutici,
i giocattoli, i generi alimentari e i servizi di telecomunicazione.

|     **Prodotto**      | **Percentuale di musica pop** |
|:---------------------:|:-----------------------------:|
| Prodotti farmaceutici |              48%              |      
|      Giocattoli       |              60%              | 
|   Generi alimentari   |              45%              |
|   Telecomunicazioni   |              55%              |

Per le pubblicità dei [veicoli](music-analysis#veicoli), in controtendenza con la diffusione del genere pop,
la musica elettronica sta tornando a essere la scelta più gettonata dopo aver raggiunto il minimo di occorrenze tra il
2005 e il 2009. In accordo con l’andamento generale, invece, è la progressiva scomparsa della musica classica.

<p class="caption">
Genere musicale per lustro per le pubblicità dei veicoli
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/music_charts/new_charts/nice12_f_22.json" style="width: 100%"></vegachart>

## Parole, parole, parole…

In questa sezione ci siamo concentrati sull’analizzare le trascrizioni estrapolate dai nostri dati.
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

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/scene_sec.json" style="width:100%; height:200px;"></vegachart>

<p class="caption">
Numero di parole per secondo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/parole_secondo.json" style="width:100%; height:200px;"></vegachart>

## Traducendo coi colori

Un aspetto importante per un video pubblicitario è il colore.

Ogni spot è stato suddiviso in **scene** e poi ‘tradotto’ in un grafico Marimekko che riassume a colpo d’occhio i
**colori** utilizzati, la loro **quantità** e la loro **frequenza**.

<p class="caption">
Le tavolozze colori (<em>Marimekko</em>) di 8 spot diversi
</p>
<div class="marimekko-grid">
    <div>
        <p class="marimekko-caption">Tabù, 1987</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-tabu-1987.png" alt="Tabù, 1987">
    </div>

    <div>
        <p class="marimekko-caption">Nutella, 1995</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-nutella-1995.png" alt="Nutella, 1995">
    </div>

    <div>
        <p class="marimekko-caption">Barilla, 2000</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-barilla-2000.png" alt="Barilla, 2000">
    </div>

    <div>
        <p class="marimekko-caption">Vodafone, 2003</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-vodafone-2003.png" alt="Vodafone, 2003">
    </div>

</div>

<div class="marimekko-grid">

    <div>
        <p class="marimekko-caption">Poste Italiane, 2003</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-poste-italiane-2003.png" alt="Poste Italiane, 2003">
    </div>

    <div>
        <p class="marimekko-caption">Riso Gallo, 2005</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-riso-gallo-2005.png" alt="Riso Gallo, 2005">
    </div>


    <div>
        <p class="marimekko-caption">Vanish, 2007</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-vanish-2007.png" alt="Vanish, 2007">
    </div>

    <div>
        <p class="marimekko-caption">Mercedes-Benz, 2023</p>
        <img src="{{site.baseurl}}/assets/images/home/marimekko-mercedes-benz-2023.png" alt="Mercedes-Benz, 2023">
    </div>

</div>

La collezione di tutte le palette ci ha poi permesso di ricalibrare il peso di ciascun colore e di applicarlo nelle
nostre analisi.

Ci teniamo a precisare che il nostro studio si è basato su video che provengono nella maggior parte dei casi da
registrazioni casalinghe e poi riversate in digitale: la qualità dei colori degli spot perciò non è quella originale ma
quella più vicina a quella esperita dall’utente finale attraverso i mezzi di ricezione di ciascuna epoca.

<p class="caption">
Distribuzione dei colori per classe di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/color_charts/nizza_colore.json" style="width: 100%; height:200px"></vegachart>

<p class="caption">
Andamento delle classi di Nizza nel tempo
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/color_charts/nizza_tempo.json" style="width: 100%; height:300px"></vegachart>

<p class="caption">
Andamento dei colori per lustro
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/color_charts/colori_lustro.json" style="width: 100%; height:300px;"></vegachart>

## Dagli anni 80 a oggi, chi sono i protagonisti

Ulteriore aspetto che è stato preso in considerazione in queste analisi è stato _chi_ e _cosa_ effettivamente comparisse
negli spot. Va infatti preso in considerazione anche chi sono i principali personaggi dei brevi sipari che ci fanno
compagnia
mentre guardiamo la televisione. Un elemento che spicca immediatamente è la pervasiva presenza
delle [persone](entity-analysis#analisi-delle-classi-di-yolo): benché
possa sembrare scontato infatti, la preponderanza di esseri umani è assoluta in ogni epoca analizzata.

| Classe     | Occorrenze |
|------------|-----------:|
| persona    |       8264 |
| bottiglia  |       1174 |
| automobile |       1102 |
| cravatta   |        791 |
| tazza      |        753 |

La spiegazione di questo è banale, in quanto se la pubblicità si prefigge di influenzare il comportamento delle persone,
è indubbio che
vedere altre persone come protagoniste ottenga un maggior effetto. Osserviamo trend particolari se invece si prendono in
considerazione altri elementi: analizzando le 10 categorie di oggetti più osservati, infatti, si nota come automobili e
bottiglie (prevalentemente di alcolici) conquistino le prime
posizioni, osservando le prime dominare la classifica a
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
ruolo creativo nell’ambito pubblicitario.

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
sono contraddistinti da aspetti mutevoli e difficili da definire, e
solo in rari casi siamo riusciti a individuare tendenze chiare e precise.
Eppure, non ci sentiamo di affermare di non aver raggiunto il nostro obiettivo.
Seppur con delle difficoltà, studiando i diversi livelli di comunicazione abbiamo trovato, almeno in parte,
elementi che distinguono la pubblicità contemporanea da quella passata. Sicuramente, la separazione fra
ieri e oggi non è così netta come ci aspettavamo, o meglio, così non appare dalle nostre analisi.
Tuttavia, non si può negare che ci sia un graduale cambiamento nel corso degli anni.
Infine, è doveroso sottolineare che le nostre conclusioni rimangono parziali,
pertanto non possono — e non vogliono — spiegare la totalità del fenomeno indagato.

## Next step

Abbiamo analizzato spot estraendo indicatori che nel loro insieme descrivono le caratteristiche percettive di
ciascun video, definendone il _mood_.
Questo tipo di analisi potrebbe essere esteso anche alle trasmissioni televisive (serie, varietà, film, talk show).

In questa maniera, parallelamente, si avrebbero gli stessi indicatori anche per gli show e
sarebbe quindi possibile calcolare l’affinità tra questi e gli spot che vanno a inserirsi in essi.

Tale operazione permetterebbe alle concessionarie di pubblicità di avere un nuovo strumento per caratterizzare gli spazi
pubblicitari da vendere.