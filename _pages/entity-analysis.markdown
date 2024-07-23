---
layout: home
title: "Analisi delle entità"
# subtitle: ""
show_sidetoc: true
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/scacchiera.jpg
header_title: "Analisi delle entità"
vega: true
---
A cura di: Axel Perini



## Divisione dei video in scene
Per raggiungere questo scopo è stata utilizzata la libreria scenedetect, la quale ha suddiviso ciascun video in scene, sfruttando come criterio la diversità di contesto (con cambio di colore netto l'algoritmo della libreria assume che vi sia stato un cambio di scena). Per ciascuna scena è stato poi estratto il frame mediano.
Di fatto questa divisione permette di ridurre molto i tempi computazionali dell'analisi, non dovendo eseguire una classificazione su ogni singolo frame che compone ciascun video, ma eseguendolo su una ridotta parte accuratamente selezionata.


## Applicazione software di riconoscimento di entità
I frame mediani di ogni scena, salvati in cartelle con lo stesso nome dell'id identificativo di ciascun video, sono poi stati analizzati utilizzando YOLOv8 (versione yolov8n.pt). 
Questo framework di intelligenza artificiale è in grado di identificare le entità presenti all'interno di un'immagine o una sequenza di immagini: questo strumento è stato addestrato su COCO, un dataset di immagini che fanno riferimento a 80 categorie di oggetti e animali di uso comune.


L'output risultante è una cartella contenente file csv, ciascuno con il nome relativo al video analizzato, presentante tre colonne: 'Frame' che fa riferimento a quale scena sia stata classificata, 'Class' che indica quale è stata la classificazione prodotta e 'Probability' ovvero la probabilità con cui un' entità viene riconosciuta. Va specificato che per ogni scena possono essere presenti più entità, ciascuna con una propria probabilità di riconoscimento.




## Pulizia e completamento dei dati
Le analisi vogliono tenere conto anche della dimensione temporale delle classificazioni (in particolare a quale lustro appartenesse ogni video), quindi è stato necessario implementarla: sfruttando un'altra cartella contenente file csv, ciascuno definito dal video_id e dall'anno a cui apparteneva tale video, è stata implementata la dimensione temporale (sotto forma di lustro) ai dati che abbiamo ottenuto dall'uso di YOLO.
Sono state successivamente svolte altre due operazioni per la pulizia e ottimizzazione dei dati.


In primo luogo sono state rimosse le classificazioni con probabilità < 0.5, questo perchè non poteva essere utile in alcun modo effettuare delle analisi su elementi così ambigui per YOLO. 
Come seconda operazione ciascun video è stato definito dalle classi uniche che lo compongono: in altre parole, se una classe è stata riconosciuta all'interno di una delle scene appartenenti a un video con una probabilità superiore al 50%, allora ulteriori riconoscimenti sono stati ignorati. 


Il motivo è duplice: per le analisi svolte non è necessario conoscere con quale frequenza una classe viene riconosciuta all'interno di un video, ma piuttosto se tale classe è presente o meno, per poter affermare che quel video fa riferimento a tale classe. L'altro motivo è che le caratteristiche dei video rischiavano di falsare le analisi, in quanto la lunghezza di questi (o comunque il numero di scene in cui poteva essere suddiviso) avrebbero potuto creare una rappresentazione eccessiva di una classe rispetto ad altre; si pensi a uno spot di 20 scene relativo a un'auto sportiva: verosimilmente verranno riconosciute almeno 20 classi "macchina" in quel video, mentre un altro spot, che si svolge con una sola scena e che fa riferimento a un video casalingo, avrebbe annoverato per una sola volta tutti gli elementi presenti in quella scena ("sedia", come anche "bottiglia" ecc.).



## Classi di YOLOv8
L'obiettivo delle analisi è quello di mettere in relazione la dimensione temporale con le classi identificate.
I grafici risultanti da queste analisi sono stati creati con Altair, per permettere l'interattività.


### Distribuzione delle classi
In questa fase si osserva come le classi identificate da YOLO si distribuiscono. E' un'analisi preliminare e non tiene conto della dimensione temporale.
Il grafico è stato reso interattivo per poter visualizzare il numero di occorrenze effettive che ogni classe presenta.


### Evoluzione delle classi
Successivamente è stata analizzata l'evoluzione nel tempo di tutte le classi identificate da YOLO. Quest'analisi non è riportata nel lavoro finale in quanto di difficile lettura.
La frequenza di ciascuna classe è stata normalizzata secondo il numero di video presenti in ogni anno, per evitare dei bias relativi alla quantità di dati reperiti per ciascun anno.


### Top dieci classi
In questa analisi vi è maggior chiarezza rispetto alla precedente, concentrandosi prevalentemente sulle categorie più rappresentate (i numeri delle successive diventano esigui). 
E' stata inoltre rimossa la classe più rappresentata in quanto si è osservata una sua preponderanza in ogni periodo storico: tale classe è quella delle "persone", per ragionevoli motivi si è optato di assumere che l'entità più utilizzata nella pubblicità rivolta agli umani siano altri esseri umani.
Nel grafico è stato inoltre creato un selettore legato alla legenda, che permette di selezionare una singola classe per visualizzare con più facilità il suo andamento nel tempo.


### Salvataggio delle classi
Infine è stata definita una funzione che quando applicata alle precedenti permette il salvataggio del grafico in formato json con nome personalizzabile.
E' stato specificato che, tra le proprietà dei grafici, questi dovessero avere width e height = "container", in modo da permettere il ridimensionamento automatico del grafico nel caso in cui la finestra cambiasse le proprie dimensioni.


## Classi di Nizza
Le analisi svolte si sono poi concentrate sull'utilizzo delle classi di Nizza, ovvero una classificazione universalmente riconosciuta che categorizza gli elementi in precise categorie merceologiche.


### Implementazione della classificazione di Nizza
Per aggiungere le classi di Nizza nel dataset si è iterato sui file csv precedentemente salvati aggiungendo una colonna che identificasse ogni possibile classe del dataset COCO come appartenente a una precisa categoria di Nizza.
Inizialmente si crea una mappa che fa corrispondere a ciascuna classe una categoria di Nizza, successivamente si aggiunge la colonna "Nizza" a tutti i file, e si effettua la conversione classe -> Nizza


### Creazione grafici delle classi di Nizza
Viene inizialmente definita una mappa per aggiungere una descrizione alle varie categorie di Nizza.
Successivamente si esegue l'analisi delle prime dieci categorie di Nizza in base alla loro frequenza di comparsa nei video. 
Nel grafico risultante è stato implementato un selettore legato alla legenda, che permette di scegliere quale classe di Nizza visualizzare con più facilità. 


E' stato aggiunto un tooltip che visualizza (passandoci sopra con il cursore) le informazioni relative alla classe di Nizza a cui appartiene quel punto e la sua descrizione, per aumentare l'intelligibilità del grafico.
E' stato aggiunto l'elemento "interactive" dopo i parametri per poter visualizzare il tooltip, tuttavia con argomenti "bind_x" e "bind_y" = FALSE, in quanto altrimenti il grafico si sarebbe ridimensionato con lo scrolling del cursore sopra di esso.

## Utilizzo di Jekyll per la creazione del sito web
Per l'implementazione dei grafici sono stati presi degli accorgimenti in quanto questi non venivano visualizzati correttamente, infatti si sono dovute specificare le dimensioni di width e height, con quest'ultima avente una dimensione in pixel, per poter visualizzare i grafici.






## Analisi delle classi di YOLO

YOLO è un framework di intelligenza artificiale che permette di svolgere varie operazioni di computer vision; in questo caso ha classificato le scene in cui sono stati divisi i video analizzati.

<p class="caption">
Numero di occorrenze totali delle 50 classi più rappresentate
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/class_distribution_lustrum.json" style="width:100%;height:600px;"></vegachart>  





_Nell'immagine si osserva come la classe più rappresentata sia quella delle "persone", a indicare una componente umana fondamentale quando si tratta di mostrare prodotti o più semplicemente comunicare informazioni ad altri umani._


Per comprendere l'andamento dell'utilizzo di certe classi nei lustri di tempo, si possono prendere in considerazione le 10 classi più rappresentate, escludendo quella delle "persone", che avrebbe una presenza preponderante rispetto alle altre.

<p class="caption">
Frequenze di ciascuna classe rispetto al numero di video, distribuite nel tempo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/top_classes_evolution_lustrum.json" style="width:100%;height:400px;"></vegachart>  



_Si osserva come, a un certo punto, la classe "macchine" abbia un'impennata di presenze all'interno degli spot pubblicitari, diventando dominante dagli anni 2000 in poi. Va inoltre notata una tendenza di aumento dell'utilizzo di elementi come "sedia" (potenzialmente indicando contesti casalinghi), come anche quello delle "bottiglie", spesso sfruttate in pubblicità basate su alcolici._


## Analisi delle classi di Nizza

Le stesse categorizzazioni precedentemente analizzate sono state trasformate in categorie di Nizza, per osservare l'andamento nel tempo delle tipologie merceologiche definite da questa particolare classificazione.

<p class="caption">
Frequenze di ciascuna classe di Nizza rispetto al numero di video, distribuite nel tempo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/top_Nizza_evolution_lustrum.json" style="width:100%;height:600px;"></vegachart>  


_Anche in queste analisi la categoria "persona" non è stata inclusa, in quanto sovra rappresentata. Nell'immagine si osserva come la classe di Nizza 21 (piccoli utensili e apparecchi a mano per uso domestico e da cucina) abbia avuto un'impennata di rappresentazioni all'interno della pubblicità a partire dal lustro 2005-2009, arrivando a essere la più rappresentata per tutto il restante periodo preso in esame. Si osserva inoltre una generale superiorità rappresentativa per quanto riguarda la classe 12 (veicoli e apparecchi per il trasporto di persone o merci via terra, aria o acqua), così come anche un progressivo aumento della classe 20 (mobili e loro parti) partendo dal lustro 1995-1999._

## Conclusioni
Questi risultati appaiono mutevoli a seconda di quale classificazione si usa (quella di YOLO piuttosto che quella di Nizza), ma sono comunque accomunati da una tendenza: la rappresentazione di elementi inerenti ai veicoli e al quotidiano ha riscontrato un aumento significativo partendo dagli anni 2000, assestandosi come più rappresentati nelle pubblicità italiane.
Questo genere di conoscenza è utile considerando la necessità che ha la pubblicità di adattarsi a un mercato sempre più esigente (sono sempre più infatti le fonti pubblicitarie alle quali il pubblico viene esposto).


