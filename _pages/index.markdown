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
dolce bambina nella pubblicità della Barilla? A chi non è mai capitato di ricordare i famosi 'pennelli Cinghiale'?

## Da Carosello alla pubblicità moderna

In quegli anni la televisione passa da avere uno scopo pedagogico-didascalico tipico degli anni ’60 a quello di puro
intrattenimento che la ha caratterizzata fino agli anni 2000. Era una novità, sia per chi guardava la televisione, sia
per chi ideava queste sequenze di immagini: non vi erano molte regole e si potevano rappresentare scene narrative avendo
come unico limite (o quasi) l’immaginazione. Se però pensiamo a quanto fossero diverse le pubblicità di un tempo
rispetto a quelle che siamo abituati a vedere oggi, ci chiediamo cosa sia accaduto. «A partire dagli anni 2000 c’è
un’inversione di rotta, si adotta lo stile MTV. La pubblicità si fa più ammiccante, caratterizzata da immagini
sovraesposte e dal ritmo sempre più incalzante \[…\] gli spot degli anni 2000 non suscitano le stesse emozioni dei
precedenti». Così commenta Michele Logrippo, fondatore del sito Spot80, quando gli chiediamo che cosa sia cambiato
rispetto agli anni ’80.

La nostra ricerca nasce dall'idea di indagare l'evoluzione della comunicazione pubblicitaria 
televisiva dagli anni ’80 a oggi. A tale scopo, abbiamo raccolto gli spot reperibili da un sito dedicato, _Spot80_, e 
da diversi canali YouTube. I dati sono stati ordinati all'interno di un dataframe in base al loro id, al titolo, alla descrizione e all'anno di pubblicazione. 
Successivamente, gli stessi sono stati arricchiti. Abbiamo, quindi, aggiunto la cosiddetta classe di Nizza e raggruppato gli spot in base ai lustri.
Una volta puliti e preparati i dati, abbiamo eseguito le analisi che presentiamo qui di seguito.

## Evoluzione di musica e linguaggio

La pubblicità dimostra di sapersi adattare molto bene ai diversi equilibri della società e alle sue novità. Ad esempio, 
si nota a partire dagli anni Ottanta fino a oggi una progressiva
riduzione nell’utilizzo della musica classica e della musica elettronica a favore della musica pop che, ormai sempre più
in voga grazie a MTV, diventa nell’ultimo decennio il genere caratterizzante per oltre la metà degli spot televisivi.
Sulla scia di questa tendenza, si nota anche un progressivo aumento delle parole inglesi negli spot, dopo il calo registrato negli ultimi anni ’90. 
Tuttavia, la rivendicazione della nostra italianità continua a manifestarsi attraverso una seconda e rapida diminuzione di queste negli ultimi quindici anni.

<p class="caption">
Numero di anglicismi per lustro
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_angl_lustrum.json" style="width:70%"></vegachart> 


Anche le semplici parole sembrano non essere mai casuali. «Assistiamo a un ribaltamento di ciò che la società considera
scandaloso: negli anni Ottanta e Novanta erano facilmente concesse battutine sessuali e di genere, ma non si potevano
assolutamente pronunciare determinate parole. Se ci pensate, oggi, è esattamente il contrario», continua Logrippo.
Effettivamente, la nostra analisi dei testi mostra che nelle pubblicità sugli assorbenti, ad esempio, la parola ‘ciclo’
inizia a essere usata con una frequenza piuttosto elevata solo dal 2020. Oppure, risulta emblematico il caso
dell’aggettivo ‘italiano’ che, dal 2015, compare timidamente fra le parole più frequenti negli spot di prodotti alimentari, 
per poi rivelarsi il topic più rilevante a partire dal 2020.
Il _Made in Italy_ sembra diventare un requisito fondamentale proprio in questi anni successivi alla pandemia mondiale.

| **Prodotto**         | **Parola**     | **Lustro** |     **Rilevanza**     |
|:---------------------|:--------------:|-----------:|:---------------------:|
| Prodotti farmaceutici|     ciclo      |  2020-2024 |         8.43          |
| Generi alimentari    |    italiano    |  2015-2019 |         4.34         |
| Generi alimentari    |    italiano    |  2020-2024 |         13.39                   |


Una dimensione che, invece, risulta essere in continua crescita è il ritmo degli spot. Non solo quest'ultimo aumenta considerevolmente 
nel passaggio fra gi anni ’90 e i primi 2000, come ricordato anche dal nostro intervistato, ma la sua dinamicità continua 
ad aumentare fino agli ultimi cinque anni.

<p class="caption">
Numero di scene medio per secondo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/scene_sec.json" style="width:70%"></vegachart> 


## I colori

Per quanto riguarda i colori si nota come questi siano passati dall’essere molto saturi e ad alto contrasto negli anni
Ottanta e Novanta a esserlo invece meno dalla metà del 2000 in poi. Un motivo potrebbe essere quello tecnologico: la
trasmissione delle immagini da parte delle emittenti è passata da una tecnologia analogica (soggetta quindi a disturbo e
ad alterazione del segnale) a una digitale (in cui disturbo e alterazione non sussistono). Un altro motivo è poi dato
dal mezzo di ricezione e di quello di registrazione che hanno ulteriormente contribuito a deteriorare qualità e colore
dell’immagine.

Ci teniamo a precisare che in ogni caso il nostro studio si focalizza proprio sui colori percepiti dall’utente finale
attraverso i mezzi di ciascuna epoca (e non su quelli originali degli spot, cui non abbiamo accesso).

## Chi e cosa

Ulteriore aspetto che è stato preso in considerazione in queste analisi è stato _chi_ e _cosa_ effettivamente comparisse
negli spot. Va infatti preso in considerazione anche chi sono i protagonisti dei brevi sipari che ci fanno compagnia
mentre guardiamo la televisione. Un elemento che spicca immediatamente è la pervasiva presenza delle persone: benché
possa sembrare scontato infatti, la preponderanza di esseri umani è assoluta in ogni epoca analizzata. La spiegazione di
questo è banale, in quanto se la pubblicità si prefigge di influenzare il comportamento delle persone, è indubbio che
vedere altre persone come protagoniste ottenga un maggior effetto. Osserviamo trend particolari se invece si prendono in
considerazione altri elementi: analizzando le 10 categorie di oggetti più osservati, infatti, si nota come auto e
bottiglie (prevalentemente di alcolici) conquistino le prime posizioni, osservando le prime dominare la classifica a
partire dagli anni 2000 fino a oggi. Altri oggetti degni di nota sono le sedie (osservabili in svariati contesti), le
quali hanno avuto un progressivo aumento, arrivando a essere rappresentate con una frequenza sette volte più alta oggi,
rispetto al loro esordio.

Da ciò che la pubblicità mostra, si può cercare di inferire cosa essa stia cercando di proporre alla società. La
presenza di elementi come auto e bottiglie, infatti, è indicativa di uno stile pubblicitario consumistico e
avanzato, dove si sprona l’individuo a comportamenti più impulsivi, e di rimanere aggiornato sulle ultime novità
tecnologiche (almeno per quanto riguarda gli spostamenti). Le pubblicità delle automobili hanno inoltre uno stile
intrinsecamente dinamico, rappresentando rapidità e il movimento: aspetti che, come abbiamo visto, caratterizzano le
esigenze attentive del nostro pubblico odierno. Va comunque tenuto in considerazione un ultimo aspetto, perché quella
sedia che sempre più spesso appare (nonostante possa comparire in svariati contesti) è spesso associata alla casa, o
comunque a qualcosa di immobile, fermo; non è ancora ai livelli di rappresentazione di tutte le componenti dinamiche che
sono state osservate, tuttavia può rappresentare un futuro spunto, un segnale, che qualcuno cerchi di tornare alla calma
della propria dimora.

## Per concludere

In generale, dai nostri risultati, sembra che, nei primi anni 2000, per superare le difficoltà di un pubblico sempre
meno attento e interessato, la pubblicità abbia optato per essere più breve ma anche più dinamica e incisiva. Negli
ultimi anni, però, il ritmo delle pubblicità sembra essere rallentato nuovamente, per adattarsi, forse, a un nuovo
pubblico. Sicuramente, quella contemporanea, è una pubblicità che non mira a insegnare né tantomeno a emozionare ma,
piuttosto, a modellarsi e a plasmarsi alla società a cui si rivolge.