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

## Raccolta dati

Le librerie principalmente utilizzate sono state:

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
- `airing_date`
    - data di messa in onda, estrapolata dal titolo o dalla descrizione
- `duration_in_seconds`
    - durata in secondi
- `source`
    - la fonte del video

## Pulizia e preparazione dati

Il processo di _data cleaning and preparation_ ha avuto le seguenti fasi:

- sono stati eliminati i duplicati con medesimo titolo e medesimo anno di messa in onda
- è stato effettuato il _crop_ dei video caricati in formati errati (modalità _pillar_ o _letter box_)

<p class="caption">Video in formato <em>pillar box</em>, poi ripristinato</p>
![Formato pillar box](assets/images/data/pillar-box.png)

<p class="caption">Video in formato <em>letter box</em>, poi ripristinato</p>
![Formato letter box](assets/images/data/letter-box.png)

- Suddivisione in clip delle sequenze di spot
- Eliminazione video estranei dalle sequenze (sigle, bumper, spot _inframe_)

## Data enrichment

### Lustro

La distribuzione degli spot negli anni non ha un andamento canonico: per alcuni periodi ad esempio gli spot sono molto
scarsi: nel 1980, 1981 e 1998 gli spot sono meno di 20.

<p class="caption">
Distribuzione degli spot negli anni
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/data_charts/commercial_distribution_per_year.json" style="width: 100%; height:640px;"></vegachart>

Dal momento che il periodo temporale che abbiamo deciso di coprire era molto ampio abbiamo scelto di raggrupparli per
lustro. Questa operazione ci ha permesso di ottenere una distribuzione più omogenea dei nostri dati lungo l’asse
temporale. Di conseguenza, abbiamo aggiunto la colonna `lustrum` al nostro set di dati secondo questa formula:

```python
df['lustrum'] = f'{year - year % 5}_{(year + 5) - (year + 5) % 5 - 1}'
```

<p class="caption">Distribuzione degli spot nei lustri</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/data_charts/commercial_distribution_per_lustrum.json" style="width: 100%; height:320px;"></vegachart>

### Classificazione di Nizza

Con i dati in nostro possesso (titolo e descrizione), abbiamo tentato di clusterizzare gli spot in categorie, ma questo
ha portato a scarsi risultati.

Abbiamo così deciso di classificare gli spot in maniera manuale utilizzando
la [Classificazione di Nizza](https://it.wikipedia.org/wiki/Classificazione_di_Nizza),

> un elenco che descrive la natura di prodotti e servizi in termini generali, allo scopo
> di classificare i marchi registrati in maniera univocamente riconosciuta ed accettata a livello internazionale.
> (Wikipedia)

<p class="caption">Distribuzione degli spot rispetto alle classi di Nizza</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/data_charts/nice_classification_count.json" style="width: 100%; height:600px;"></vegachart>

Notiamo come le categorie di spot maggiormente presenti facciano parte di queste categorie:

| Classe di Nizza | Descrizione                           | Nº di spot |
|----------------:|---------------------------------------|-----------:|
|               3 | Prodotti per l’igiene                 |       1630 |
|              30 | Pasta, riso, caffè, prodotti da forno |       1600 |
|              12 | Veicoli                               |        924 |
|              29 | Carne, pesce, derivati del latte      |        815 |
|               5 | Prodotti farmaceutici                 |        646 |
