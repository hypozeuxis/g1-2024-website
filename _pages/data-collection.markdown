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

Librerie principali utilizzate

- `selenium`
- `pytube`
- `ffmpeg`

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

