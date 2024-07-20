---
layout: home
title: "Analisi delle entità"
# subtitle: ""
header_type: hero #base, post, hero,image, splash
header_img: assets/images/folium_map.webp
header_title: "Analisi delle entità"
vega: true
---


L'obiettivo dell' analisi delle entità è quello di individuare all'interno di un'immagine la presenza di una o più entità, ovvero oggetti, animali o persone, mettendola in relazione con diversi periodi storici, divisi in lustri.


## Analisi delle classi di YOLO

YOLO è un framework di intelligenza artificiale che permette di svolgere varie operazioni di computer vision; in questo caso ha classificato le scene in cui sono stati divisi i video analizzati.

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/class_distribution_lustrum.json" style="width:100%"></vegachart>  





_Nell'immagine si osserva come la classe più rappresentata sia quella delle "persone", a indicare una componente umana fondamentale quando si tratta di mostrare prodotti o più semplicemente comunicare informazioni ad altri umani._


Per comprendere l'andamento dell'utilizzo di certe classi nei lustri di tempo, si possono prendere in considerazione le 10 classi più rappresentate, escludendo quella delle "persone", che avrebbe una presenza preponderante rispetto alle altre.

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/top_classes_evolution_lustrum.json" style="width:100%"></vegachart>  



_Si osserva come, a un certo punto, la classe "macchine" abbia un'impennata di presenze all'interno degli spot pubblicitari, diventando dominante dagli anni 2000 in poi. Va inoltre notata una tendenza di aumento dell'utilizzo di elementi come "sedia" (potenzialmente indicando contesti casalinghi), come anche quello delle "bottiglie", spesso sfruttate in pubblicità basate su alcolici._


## Analisi delle classi di Nizza

Le stesse categorizzazioni precedentemente analizzate sono state trasformate in categorie di Nizza, per osservare l'andamento nel tempo delle tipologie merceologiche definite da questa particolare classificazione.


<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/top_Nizza_evolution_lustrum.json" style="width:100%"></vegachart>  


_Anche in queste analisi la categoria "persona" non è stata inclusa, in quanto le avrebbe falsate. Nell'immagine si osserva come la classe di Nizza 21 (Utensili e recipienti per uso domestico o di cucina) abbia avuto un'impennata di rappresentazioni all'interno della pubblicità a partire dal lustro 2005-2009, arrivando a essere la più rappresentata per tutto il restante periodo preso in esame. Si osserva inoltre una generale superiorità rappresentativa per quanto riguarda la classe 12 (Veicoli e apparecchi di locomozione), così come anche un progressivo aumento della classe 20 (Mobili e loro parti) partendo dal lustro 1995-1999._

### Conclusioni
Questi risultati appaiono mutevoli a seconda di quale classificazione si usa (quella di YOLO piuttosto che quella di Nizza), ma sono comunque accomunati da una tendenza: la rappresentazione di elementi inerenti ai veicoli e al quotidiano ha riscontrato un aumento significativo partendo dagli anni 2000, assestandosi come più rappresentati nelle pubblicità italiane.
La rappresentazione di queste particolari categorie può significare una duplice natura in seno alla pubblicità odierna: la sua necessità di adattarsi a un pubblico bisognoso di stimoli rapidi, avanzati e improntati all'esperienza "del momento" (come veicoli e bottiglie), come anche il tentativo di allinearsi con il quotidiano e il casalingo, emblematico di una volontà di pace e tranquillità.

Sembra dunque esistano due tendenze: una improntata sull'accelerazione per cogliere un'attenzione sfuggente propria del pubblico, che ha dominato le pubblicità dagli anni 2000 in poi; e un'altra, ancora in ascesa, che richiama all'ordine e alla calma, concentrandosi maggiormente sulla costruzione di un nido sicuro.



