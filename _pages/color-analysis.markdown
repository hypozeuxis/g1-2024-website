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
Dopo svariati esperimenti, è stato individuaτο il miglior set di parametri che potesse essere adeguato per
la grande maggioranza degli spot.

