---
layout: home
title: "Raccolta dati"
# subtitle: ""
show_sidetoc: true
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/miro_a.jpg
header_title: "Raccolta dati"
vega: true
---

## Individuazione delle fonti

Le nostre fonti per il recupero di spot televisivi andati in onda sulla TV italiana dal 1980 al 2024 sono state:

1. **Spot80**: un sito amatoriale che raccoglie spot italiani andati in onda dal 1977 al 1999.
    - 1.734 spot
2. Selezione da **YouTube** di spot pubblicitari dal 1983 a oggi:
    - **mDeplo**: 6.755 spot (raggruppati in sequenze)
    - **Engage.it**: 199 spot
    - altri account: 1.662 spot

In totale sono stati analizzati **10.350 spot**.

## Caratteristiche dei video

I video reperibili in rete erano suddivisi in

- spot singoli
- sequenze di spot (registrazioni di interruzioni pubblicitarie comprendenti, oltre agli spot, anche brevi sigle,
  bumper e i cosiddetti spot «inframe», cioè incorniciati dalla grafica identificativa dell’emittente)

Nel caso delle sequenze, è stato anche selezionato il timecode presente nella loro descrizione:
questo è stato utile successivamente per la suddivisione in spot singoli.

## Dati grezzi

Le librerie principalmente utilizzate per la raccolta dei dati sono state:

- `selenium`
    - per raccogliere informazioni testuali e gli ID dei video
- `pytube`
    - per il recupero dei video da YouTube
- `ffmpeg`
    - per la suddivisione delle sequenze in singoli spot
    - per il _crop_ e il ridimensionamento dei video (ripristinandone le proporzioni originali)

I dati sono stati sistemati in un dataframe con le seguenti proprietà:

- `commercial_id`
    - file name
    - YouTube video ID (when the video contains a single commercial)
    - concatenation of YouTube video ID and a progressive ID (when the video contains a sequence of commercials)
- `title`
    - titolo assegnato dall’account che ha caricato il video
- `description`
    - la didascalia presente appena dopo il video (Spot 80)
    - la descrizione (non sempre presente) del video su YouTube
- `duration_in_seconds`
    - durata in secondi
- `source`
    - la fonte del video

## Pulizia e preparazione dati

Il processo di _data cleaning and preparation_ ha avuto le seguenti fasi:

- sono stati eliminati i duplicati con medesimo titolo e medesimo anno di messa in onda
- è stato effettuato il _crop_ dei video caricati in formati errati (modalità _pillar_ o _letter box_)

<p class="caption">Video in formato <em>pillar box</em>, poi ripristinato</p>
![Formato pillar box]({{site.baseurl}}/assets/images/data/pillar-box.png)

<p class="caption">Video in formato <em>letter box</em>, poi ripristinato</p>
![Formato letter box]({{site.baseurl}}/assets/images/data/letter-box.png)

- Suddivisione in clip delle sequenze di spot
- Eliminazione video estranei dalle sequenze (sigle, bumper, spot _inframe_)

## Data enrichment

### Data di messa in onda

La data di messa in onda, `airing_date`, è stata estrapolata dal titolo o dalla descrizione mediante l’uso di
espressioni
regolari e solo in rarissimi casi (meno di 10) questa era assente: in questi casi è stata fatta una ricerca sul web per
recuperare la data più probabile.

### Marchio

Spesso la feature `title` (il titolo del video) funge da didascalia al video: oltre al nome del marchio, prodotto o
servizio essa presenta altre parole di descrizione. Da questa feature sono stati estrapolati (in maniera
semi-manuale) i nomi dei marchi e riportati nella colonna `brand`.

### Lustro

La distribuzione degli spot negli anni non ha un andamento canonico: per alcuni periodi ad esempio gli spot sono molto
scarsi: nel 1980, 1981 e 1998 gli spot sono meno di 20.

<p class="caption">
Distribuzione degli spot negli anni
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/data_charts/commercial_distribution_per_year.json" style="width: 100%; height:640px;"></vegachart>

Dal momento che il periodo temporale che abbiamo deciso di coprire era molto ampio abbiamo scelto di raggrupparli per
lustro. Questa operazione ci ha permesso di ottenere una distribuzione più consistente degli spot lungo l’asse
temporale. Di conseguenza, abbiamo associato a ciascuno spot un lustro, in riferimento all’anno di messa in onda.
I valori della colonna `lustrum` seguono questo pattern:

```
1980-1984
1985-1989
1990-1994
...
```

In questa maniera la distribuzione risulta più consistente e **il valore minimo di spot per lustro è 342** (2015–2019).

<p class="caption">Distribuzione degli spot nei lustri</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/data_charts/commercial_distribution_per_lustrum.json" style="width: 100%; height:320px;"></vegachart>

### Classificazione di Nizza

Con i dati in nostro possesso (titolo e descrizione), abbiamo tentato di clusterizzare gli spot in categorie, ma questo
ha portato a scarsi risultati.

Abbiamo così deciso di classificare gli spot in maniera manuale utilizzando la **Classificazione di Nizza**, un elenco
di 45 classi che descrivono «la natura di prodotti e servizi in termini generali, allo scopo di classificare i marchi
registrati in maniera univocamente riconosciuta ed accettata a livello
internazionale» [(Wikipedia)](https://it.wikipedia.org/wiki/Classificazione_di_Nizza).

<p class="caption">
Distribuzione degli spot rispetto alle classi di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/data_charts/nice_classification_distribution.json" style="width: 100%; height:600px;"></vegachart>

Notiamo come le 10 categorie di prodotti maggiormente pubblicizzati facciano parte di queste categorie:

| Classe di Nizza | Descrizione                           | Nº di spot |
|----------------:|---------------------------------------|-----------:|
|               3 | Prodotti per l’igiene                 |       1631 |
|              30 | Pasta, riso, caffè, prodotti da forno |       1600 |
|              12 | Veicoli                               |        924 |
|              29 | Carne, pesce, derivati del latte      |        815 |
|               5 | Prodotti farmaceutici                 |        645 |
|              16 | Articoli di cartoleria                |        582 |
|              38 | Telecomunicazioni                     |        436 |
|               9 | Apparecchi elettronici                |        411 |
|              32 | Acqua, birra, bevande                 |        406 |
|              28 | Giocattoli                            |        386 |

### Tipi di prodotto

Ciascuna classe di Nizza ha una serie di sotto-classi che identificano in maniera più precisa le categoria di un
prodotto. Ciascuno spot è stato così ulteriormente etichettato manualmente con queste sotto-categorie, consultando il
sito [TMclass](https://euipo.europa.eu/ec2/?lang=it).

I valori unici per il tipo di prodotto sono risultati 150: in questo grafico ne mostriamo i primi 40.

<p class="caption">
Distribuzione degli spot rispetto ai tipi di prodotto
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/data_charts/product_type_distribution.json" style="width: 100%; height:600px;"></vegachart>

Notiamo come, grazie a questa nuova etichettatura, nella top 10 dei prodotti maggiormente pubblicizzati compaiano le
_Bevande alcoliche (eccetto le birre)_ (classe di Nizza 33) e servizi di _Vendita al dettaglio ed all’ingrosso_ (classe
35), mentre spariscono _Articoli di cartoleria_ (classe 16) e Giocattoli (28).

| Tipo di prodotto                                                            | Classe di Nizza | Nº di spot | 
|-----------------------------------------------------------------------------|----------------:|-----------:|
| Veicoli e mezzi di trasporto terrestri                                      |              12 |        897 |
| Preparati per la pulizia del corpo e per la cura della bellezza             |               3 |        761 |
| Prodotti da forno, pasticceria, cioccolato e dolci                          |              30 |        723 |
| Prodotti per la pulizia e la profumazione, non per uso personale            |               3 |        590 |
| Libri, riviste, quotidiani stampati e altri mezzi di comunicazione su carta |              16 |        520 |
| Bevande alcoliche (eccetto le birre)                                        |              33 |        356 |
| Prodotti caseari e loro succedanei                                          |              29 |        341 |
| Medicamenti farmaceutici e naturali                                         |               5 |        312 |
| Bevande non alcoliche                                                       |              32 |        306 |
| Vendita al dettaglio ed all’ingrosso                                        |              35 |        299 |
