---
layout: home
title: "Analisi del testo"
# subtitle: ""
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/ghirigori.jpg
header_title: "Analisi del testo"
vega: true
---

## Dettagli tecnici
L’obiettivo del task di speech recognition è la trascrizione dei dialoghi e dei voiceover presenti negli spot televisivi in modo da poter effettuare la text analysis. Per il riconoscimento vocale abbiamo quindi testato diverse librerie. Whisper è emerso come il modello più adatto in quanto ha fornito le trascrizioni più accurate. 

**Whisper** è un’architettura transformer (encoder-decoder) sequence-to-sequence che estrae feature dall’ audio da cui genera il testo. È sviluppato da OpenAI ed è stato addestrato su vari task di elaborazione vocale tra cui il riconoscimento vocale multilingue, la traduzione vocale e l’identificazione della lingua. È dotato di cinque diversi modelli con precisione crescente nella trascrizione ma con un costo computazionale più elevato. Abbiamo testato in particolare i modelli small, medium e large e abbiamo individuato nel modello medium il compromesso ottimale tra efficienza e accuratezza. 


Uno dei problemi riscontrati è stato rappresentato dal fatto che Whisper può trascrivere erroneamente nomi propri non comuni come nomi di prodotti, aziende o persone. Il problema dell'errata trascrizione è stato risolto con l'aggiunta del parametro _initial_prompt_, che consente di fornire una lista di parole che verranno pronunciate, scritte con la giusta grafia. Come valore di questo parametro è stato quindi impostato il titolo dello spot televisivo e ciò ha permesso di ottenere una corretta trascrizione dei nomi dei prodotti commercializzati. 


Il parametro di Whisper _average log probability_ è stato utilizzato come indicatore dell’accuratezza della trascrizione poiché indica una misura di confidenza delle previsioni del modello. Ha valore negativo e più il valore è prossimo allo zero, più la trascrizione dovrebbe essere corretta. 
Dopo aver ottenuto le trascrizioni per il dataset completo, è  stata effettuata una seconda procedura di speech recognition per le pubblicità con _average log probability_ inferiore a -0,6 (circa 1200 spot). Questo valore era stato infatti  individuato come limite per poter considerare le trascrizioni come accurate. 
Si è passati poi a una fase di controllo e pulizia per la rimozione delle trascrizioni nulle, di quelle con caratteri non latini e delle frasi con allucinazioni del modello. 
In questo modo sono state ottenute 9400 trascrizioni adatte per l’analisi del testo. 

---

## Analisi delle trascrizioni


Una volta ottenute le trascrizioni, una prima analisi si è concentrata sul misurare la lunghezza media per lustro.
Dal grafico è possibile notare come ci sia un calo della lunghezza media delle trascrizioni nel decennio 2000-2009. 
Le analisi sulla durata media degli spot confermano questo andamento. 
Anche in quel caso, infatti, si nota una riduzione della durata che coinvolge lo stesso decennio.

<p class="caption">
Lunghezza media delle trascrizioni per lustro
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_length_lustrum.json" style="width:100%"></vegachart> 

Successivamente, la stessa analisi è stata ripetuta ma considerando anche la classe di Nizza. In generale, sembra che la lunghezza media delle trascrizioni sia molto oscillante con picchi verso l'alto e verso il basso. Si può notre, inoltre, come ogni classe segua un proprio andamento indipendente.


<p class="caption">
Lunghezza media delle trascrizioni per lustro e classe di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_length.json" style="width:100%"></vegachart>  

Come ulteriore analisi, sono stati ricercati i cosiddetti 'topic' più rilevanti divisi, ancora una volta, per lustro e classe di Nizza. 
Questa analisi permette di osservare l'eventuale insorgenza di parole chiave. 
Ad esempio, considerando la classe di Nizza 30, sotto la quale rientrano alcuni tipi di alimenti, è possibile notare come a partire dal 2020 emerge la parola 
'italiano'. Un simile aggettivo potrebbe essere emblematico della emergenza sanitaria dovuta al COVID.
Oppure, spostando l'attenzione sulla classe di Nizza 5 e sul lustro 2020-2024, è possibile notare la comparsa del sostantivo 'ciclo'.
Questo topic diventa preponderante solo negli ultimi anni, in linea con i nuovi ideali e la maggiore sensibilità della società.
Un confronto fra le diverse classi di Nizza e i lustri mette, però, in evidenza la presenza quasi costante dell'aggettivo
'nuovo'.

<p class="caption">
Topic per lustro e classe di Nizza
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_topic.json" style="width:100%"></vegachart>  

Infine, l'attenzione è stata rivolta all'eventuale presenza di anglicismi presenti negli spot pubblicitari. Dal grafico sembrerebbe emergere una tendenza altalenante fra periodi di apertura verso gli anglicismi, 
seguiti da periodi di maggiore chiusura. Inoltre, si nota come, a partire dagli anni 2000 
la presenza di anglicismi aumenti consistentemente probabilmente anche per l'arrivo del canale MTV. 
Tuttavia, a partire dal 2010 l'equilibrio cambia di nuovo, andando verso una situazione di maggiore chiusura 
verso gli anglicismi.

<p class="caption">
Numero di anglicismi per lustro
</p>
<vegachart schema-url="{{site.baseurl}}/assets/charts/text_charts/chart_angl_lustrum.json" style="width:100%"></vegachart> 


