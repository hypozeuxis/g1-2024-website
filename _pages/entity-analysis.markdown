---
layout: home
title: "Analisi delle entità"
# subtitle: ""
header_type: hero #base, post, hero,image, splash
header_img: assets/images/hero/scacchiera.jpg
header_title: "Analisi delle entità"
vega: true
---


L'obiettivo dell'analisi delle entità è quello di individuare all'interno di un'immagine la presenza di una o più entità, ovvero oggetti, animali o persone, mettendola in relazione con diversi periodi storici, divisi in lustri.


## Analisi delle classi di YOLO

YOLO è un framework di intelligenza artificiale che permette di svolgere varie operazioni di computer vision; in questo caso ha classificato le scene in cui sono stati divisi i video analizzati.

<p class="caption">
Distribuzione classi nel tempo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/class_distribution_lustrum.json" style="width:100%;height:600px;"></vegachart>  





_Nell'immagine si osserva come la classe più rappresentata sia quella delle "persone", a indicare una componente umana fondamentale quando si tratta di mostrare prodotti o più semplicemente comunicare informazioni ad altri umani._


Per comprendere l'andamento dell'utilizzo di certe classi nei lustri di tempo, si possono prendere in considerazione le 10 classi più rappresentate, escludendo quella delle "persone", che avrebbe una presenza preponderante rispetto alle altre.

<p class="caption">
Evoluzione delle classi nel tempo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/top_classes_evolution_lustrum.json" style="width:100%;height:400px;"></vegachart>  



_Si osserva come, a un certo punto, la classe "macchine" abbia un'impennata di presenze all'interno degli spot pubblicitari, diventando dominante dagli anni 2000 in poi. Va inoltre notata una tendenza di aumento dell'utilizzo di elementi come "sedia" (potenzialmente indicando contesti casalinghi), come anche quello delle "bottiglie", spesso sfruttate in pubblicità basate su alcolici._


## Analisi delle classi di Nizza

Le stesse categorizzazioni precedentemente analizzate sono state trasformate in categorie di Nizza, per osservare l'andamento nel tempo delle tipologie merceologiche definite da questa particolare classificazione.

<p class="caption">
Evoluzione delle classi di Nizza nel tempo
</p>

<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/top_Nizza_evolution_lustrum.json" style="width:100%;height:600px;"></vegachart>  


_Anche in queste analisi la categoria "persona" non è stata inclusa, in quanto le avrebbe falsate. Nell'immagine si osserva come la classe di Nizza 21 (Utensili e recipienti per uso domestico o di cucina) abbia avuto un'impennata di rappresentazioni all'interno della pubblicità a partire dal lustro 2005-2009, arrivando a essere la più rappresentata per tutto il restante periodo preso in esame. Si osserva inoltre una generale superiorità rappresentativa per quanto riguarda la classe 12 (Veicoli e apparecchi di locomozione), così come anche un progressivo aumento della classe 20 (Mobili e loro parti) partendo dal lustro 1995-1999._

### Conclusioni
Questi risultati appaiono mutevoli a seconda di quale classificazione si usa (quella di YOLO piuttosto che quella di Nizza), ma sono comunque accomunati da una tendenza: la rappresentazione di elementi inerenti ai veicoli e al quotidiano ha riscontrato un aumento significativo partendo dagli anni 2000, assestandosi come più rappresentati nelle pubblicità italiane.
La rappresentazione di queste particolari categorie può significare una duplice natura in seno alla pubblicità odierna: la sua necessità di adattarsi a un pubblico bisognoso di stimoli rapidi, avanzati e improntati all'esperienza "del momento" (come veicoli e bottiglie), come anche il tentativo di allinearsi con il quotidiano e il casalingo, emblematico di una volontà di pace e tranquillità.

Sembra dunque esistano due tendenze: una improntata sull'accelerazione per cogliere un'attenzione sfuggente propria del pubblico, che ha dominato le pubblicità dagli anni 2000 in poi; e un'altra, ancora in ascesa, che richiama all'ordine e alla calma, concentrandosi maggiormente sulla costruzione di un nido sicuro.

### Descrizione tecnica

##### Fase 1: Dividere i video in scene
Per raggiungere questo scopo è stata utilizzata la libreria NOME_LIBRERIA_DIVISIONE_IN_SCENE, la quale ha suddiviso ciascun video in scene, sfruttando come criterio la diversità di contesto (con cambio di colore netto l'algoritmo della libreria assume che vi sia stato un cambio di scena). Per ciascuna scena è stato poi estratto il frame mediano.
Di fatto questa divisione permette di ridurre molto i tempi computazionali dell'analisi, non dovendo eseguire una classificazione su ogni singolo frame che compone ciascun video, ma eseguendolo su una ridotta parte accuratamente selezionata.
[INSERIRE EVENTUALI CODICI]

##### Fase 2: Applicare software di riconoscimento di entità
I frame mediani di ogni scena, salvati in cartelle con lo stesso nome dell'id identificativo di ciascun video, sono poi stati analizzati utilizzando YOLOv8 (versione yolov8n.pt). 
Questo framework di intelligenza artificiale è in grado di identificare le entità presenti all'interno di un'immagine o una sequenza di immagini: questo strumento è stato addestrato su COCO, un dataset di immagini che fanno riferimento a 80 categorie di oggetti e animali di uso comune.
L'output risultante è una cartella contenente file csv, ciascuno con il nome relativo al video analizzato, presentante tre colonne: 'Frame' che fa riferimento a quale scena sia stata classificata, 'Class' che indica quale è stata la classificazione prodotta e 'Probability' ovvero la probabilità con cui un entità viene riconosciuta. Va specificato che per ogni scena possono essere presenti più entità, ciascuna con una propria probabilità di riconoscimento.

```python
import os
import csv
import glob
from ultralytics import YOLO

# Carica il modello YOLOv8
model = YOLO('yolov8n.pt')  # Puoi usare il modello che preferisci

# Ottieni una lista di tutte le immagini nella cartella
image_paths = glob.glob(os.path.join(image_folder, '*.jpg'))  # Modifica l'estensione se necessario

# Funzione per ottenere il titolo della sequenza e il video dal nome del file
def get_video_info(image_path):
    base_name = os.path.basename(image_path)
    parts = base_name.split('.')
    sequence_title = parts[0]  # "_3siiuQ3kp0"
    video_title = parts[1]  # "s4"
    frame_name = base_name  # Nome completo del frame
    return sequence_title, video_title, frame_name

# Funzione per salvare i risultati in file CSV
def save_results_to_csv(results, output_folder='sceneDetect_output'):
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    for sequence_title, videos in results.items():
        for video_title, detections in videos.items():
            video_folder = os.path.join(output_folder, sequence_title, video_title)
            if not os.path.exists(video_folder):
                os.makedirs(video_folder)
            csv_file = os.path.join(video_folder, f'{video_title}.csv')
            with open(csv_file, 'w', newline='') as file:
                writer = csv.writer(file)
                writer.writerow(['Frame', 'Class', 'Probability'])
                for frame, dets in detections.items():
                    for det in dets:
                        writer.writerow([frame] + det)

# Itera attraverso tutte le immagini e applica il modello YOLOv8
results = {}
for image_path in image_paths:
    try:
        sequence_title, video_title, frame_name = get_video_info(image_path)
        # Applica il modello YOLOv8
        detections = model(image_path)  # Carica l'immagine direttamente tramite il modello
        # Estrai le informazioni rilevanti
        if sequence_title not in results:
            results[sequence_title] = {}
        if video_title not in results[sequence_title]:
            results[sequence_title][video_title] = {}
        results[sequence_title][video_title][frame_name] = []
        for det in detections:
            for bbox in det.boxes:
                class_id = int(bbox.cls[0].item())  # Indice della classe
                score = float(bbox.conf[0].item())  # Probabilità della classe
                class_name = det.names[class_id]  # Nome della classe
                results[sequence_title][video_title][frame_name].append([class_name, score])
        print(f"Elaborazione completata per: {frame_name}")
    except Exception as e:
        print(f"Errore durante l'elaborazione di {image_path}: {e}")

# Salva i risultati in file CSV
save_results_to_csv(results)
```


##### Fase 3: Pulizia e completamento dei dati
Le analisi vogliono tenere conto anche della dimensione temporale delle classificazioni (in particolare a quale lustro appartenesse ogni video), quindi è stato necessario implementarla: sfruttando un'altra cartella contenente file csv, ciascuno definito dal video_id e dall'anno a cui apparteneva tale video, è stata implementata la dimensione temporale (sotto forma di lustro) ai dati che abbiamo ottenuto dall'uso di YOLO.

```python
import os
import pandas as pd

def clean_video_name(file_name):
    # Rimuove eventuali ripetizioni ".csv" alla fine del nome del file
    if file_name.endswith('.csv.csv'):
        return file_name[:-4]  # Rimuove l'ultima '.csv'
    elif file_name.endswith('.csv'):
        return file_name[:-4]  # Rimuove l'ultima '.csv'
    else:
        return file_name

def aggiungi_colonna_anno_a_tutti(file_anni, cartella_video, output_cartella):
    # Carica i dati degli anni
    dati_anni = pd.read_csv(file_anni)

    # Crea la cartella di output se non esiste
    if not os.path.exists(output_cartella):
        os.makedirs(output_cartella)

    # Itera su ciascun file CSV nella cartella dei video
    for file in os.listdir(cartella_video):
        if file.endswith('.csv'):
            file_path = os.path.join(cartella_video, file)
            dati_video = pd.read_csv(file_path)
            
            # Pulisce il nome del video
            nome_video = clean_video_name(file)
            
            # Trova l'anno corrispondente
            anno = dati_anni.loc[dati_anni['commercial_id'] == nome_video, 'year'].values
            if len(anno) > 0:
                anno = anno[0]
            else:
                anno = None  # Gestisci il caso in cui non ci sia un anno corrispondente
            
            # Aggiungi la colonna 'year'
            dati_video['year'] = anno
            
            # Salva il DataFrame aggiornato in un nuovo file CSV nella cartella di output
            output_file_path = os.path.join(output_cartella, file)
            dati_video.to_csv(output_file_path, index=False)
            print(f"File '{file}' aggiornato con l'anno salvato come '{output_file_path}'.")

# Percorso del file con le informazioni sugli anni
file_anni = r"C:\Users\perin\PycharmProjects\pythonProject2\all_commercials_classified_filtered.csv"

# Percorso della cartella con i file CSV dei video
cartella_video = r"C:\Users\perin\PycharmProjects\pythonProject2\Dati_combinati"

# Percorso della cartella di output
output_cartella = r"Dati_finali"

aggiungi_colonna_anno_a_tutti(file_anni, cartella_video, output_cartella)
```

Sono state successivamente svolte altre due operazioni per la pulizia e ottimizzazione dei dati.
In primo luogo sono state rimosse le classificazioni con probabilità < 0.5, questo perchè non poteva essere utile in alcun modo effettuare delle analisi su elementi così ambigui per YOLO. 
Come seconda operazione ciascun video è stato definito dalle classi uniche che lo compongono: in altre parole, se una classe è stata riconosciuta all'interno di una delle scene appartenenti a un video con una probabilità superiore al 50%, allora ulteriori riconoscimenti sono stati ignorati. Il motivo è duplice: per le analisi svolte non è necessario conoscere con quale frequenza una classe viene riconosciuta all'interno di un video, ma piuttosto se tale classe è presente o meno, per poter affermare che quel video fa riferimento a tale classe. L'altro motivo è che le caratteristiche dei video rischiavano di falsare le analisi, in quanto la lunghezza di questi (o comunque il numero di scene in cui poteva essere suddiviso) avrebbero potuto creare una sovrarappresentazione di una classe ai danni di altre; si pensi a uno spot di 20 scene relativo a un'auto sportiva: verosimilmente verranno riconosciute almeno 20 classi "macchina" in quel video, mentre un altro spot, che si svolge con una sola scena e che fa riferimento a un video casalingo, avrebbe annoverato per una sola volta tutti gli elementi presenti in quella scena ("sedia", come anche "bottiglia" ecc.).

```python
import os
import pandas as pd
def load_and_filter_data(consolidated_folder, prob_threshold=0.5):
    all_data = pd.DataFrame()

    for file in os.listdir(consolidated_folder):
        if file.endswith('.csv'):
            file_path = os.path.join(consolidated_folder, file)
            data = pd.read_csv(file_path)
            filtered_data = data[data['Probability'] > prob_threshold]
            all_data = pd.concat([all_data, filtered_data], ignore_index=True)
    
    return all_data

def get_video_id_from_filename(filename):
    # Estrai il video_id dal filename assumendo il formato  'video_nomeFrame.jpg'
    video_id = filename.split('.')[0]  # Estrai 'video_nomeFrame' part
    return video_id

def get_classes_per_video(data):
    # Raggruppa per video ID e ottieni le classi uniche di ciascun video
    data['Video'] = data['Frame'].apply(get_video_id_from_filename)
    classes_per_video = data.groupby('Video').agg({'Class': lambda x: list(set(x)),
                                                   'year': 'first'}).reset_index()
    return classes_per_video

def save_classes_per_video(classes_per_video, output_folder):
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)
    
    for idx, row in classes_per_video.iterrows():
        video = row['Video']
        classes = row['Class']
        year = row['year']
        output_file = os.path.join(output_folder, f'{video}_classes.csv')
        df = pd.DataFrame({'Class': classes, 'year': [year] * len(classes)})
        df.to_csv(output_file, index=False)

# Percorso alla cartella con i file CSV consolidati
consolidated_folder = r"C:\Users\perin\PycharmProjects\pythonProject2\Dati_Finali"
output_folder = r"C:\Users\perin\PycharmProjects\pythonProject2\dati_finali_unici"

# Carica e filtra i dati
data = load_and_filter_data(consolidated_folder)

# Ottenere le classi per video
classes_per_video = get_classes_per_video(data)

# Salvare le classi e gli anni per video nella nuova cartella
save_classes_per_video(classes_per_video, output_folder)
```

##### Fase 4: Analisi Classi
L'obiettivo delle analisi è quello di mettere in relazione la dimensione temporale con le classi identificate.
I grafici risultanti da queste analisi sono stati creati con Altair, per permettere l'interazione.


**Analisi della distribuzione delle classi**: osservare come le classi identificate da YOLO si distribuiscono. E' un'analisi preliminare e non tiene conto della dimensione temporale.

```python
import altair as alt
def analyze_class_distribution(data):
    class_counts = data['Class'].value_counts().reset_index()
    class_counts.columns = ['Class', 'Occorrenze']
    
    chart = alt.Chart(class_counts).mark_bar().encode(
        x=alt.X('Occorrenze:Q', title='Occorrenze'),
        y=alt.Y('Class:N', sort='-x', title='Class'),
        color=alt.Color('Class:N', title='Classe',legend=None, scale=alt.Scale(scheme='blueorange',type='quantize') )
    ).properties(
        #title='Distribuzione delle Classi',
        width=800,
        height=600
    )
    
    return chart
```
_E' stata rimossa la legenda per favorire la leggibilità, come anche il titolo, che apparirà in markdown, inoltre è stato scelto un colore che rendesse la pagina "Entità" omogenea dal punto di vista stilistico rispetto alle altre._

**Analisi evoluzione delle classi**: successivamente è stata analizzata l'evoluzione nel tempo di tutte le classi identificate da YOLO. Quest'analisi non è riportata nel lavoro finale in quanto di difficile lettura.

```python
import altair as alt
import pandas as pd
def analyze_class_evolution(data):
    #data['year'] = pd.to_numeric(data['year'], errors='coerce')
    data.dropna(subset=['lustro', 'Class'], inplace=True)
    
    # Contare il numero di video per ogni anno
    videos_per_year = data.groupby('lustro')['video_id'].nunique().reset_index()
    videos_per_year.columns = ['lustro', 'num_videos']
    
    # Contare le occorrenze delle classi per anno
    class_distribution_by_year = data.groupby(['lustro', 'Class']).size().reset_index(name='counts')
    
    # Unire i dati di distribuzione delle classi con il numero di video per anno
    class_distribution_normalized = pd.merge(class_distribution_by_year, videos_per_year, on='lustro')
    class_distribution_normalized['normalized_counts'] = class_distribution_normalized['counts'] / class_distribution_normalized['num_videos']
    
    chart = alt.Chart(class_distribution_normalized).mark_line().encode(
        x=alt.X('lustro:O', title='Lustro'),
        y=alt.Y('normalized_counts:Q', title='Occorrenze per Video'),
        color=alt.Color('Class:N', title='Class')
    ).properties(
        title='Evoluzione delle Classi nel Tempo (Normalizzata per Numero di Video)',
        width=800,
        height=600
    )
    
    return chart
```

_La frequenza di ciascuna classe è stata normalizzata secondo il numero di video presenti in ogni anno, per evitare dei bias relativi alla quantità di dati reperiti per ciascun anno_

**Analisi delle top dieci classi**: in questa analisi vi è maggior chiarezza rispetto alla precedente, concentrandosi prevalentemente sulle categorie più rappresentate (i numeri delle successive diventano esigui). E' stata inoltre rimossa la classe più rappresentata in quanto si è osservata una sua preponderanza in ogni periodo storico: tale classe è quella delle "persone", per ragionevoli motivi si è optato di assumere che l'entità più utilizzata nella pubblicità rivolta agli umani siano altri esseri umani.

```python
import altair as alt
import pandas as pd
def analyze_top_classes_excluding_most_represented(data):
    # Calcola la frequenza delle classi
    total_class_frequency = data['Class'].value_counts()
    most_represented_class = total_class_frequency.idxmax()
    top_classes = total_class_frequency[total_class_frequency.index != most_represented_class].head(10).index
    
    

    # Filtra i dati per le top classi escludendo la più rappresentata
    filtered_data = data[data['Class'].isin(top_classes)]
    class_distribution_by_year = filtered_data.groupby(['lustro', 'Class']).size().reset_index(name='counts')
    
    # Calcola il numero di video per lustro
    videos_per_year = filtered_data.groupby('lustro')['video_id'].nunique().reset_index()
    videos_per_year.columns = ['lustro', 'num_videos']
    
    # Normalizza la distribuzione delle classi per il numero di video
    class_distribution_normalized = pd.merge(class_distribution_by_year, videos_per_year, on='lustro')
    class_distribution_normalized['normalized_counts'] = class_distribution_normalized['counts'] / class_distribution_normalized['num_videos']
    
    # Crea un selettore a discesa per le classi
    dropdown = alt.binding_select(options=top_classes.tolist(), name='Seleziona Classe: ')
    selector = alt.selection_point(fields=['Class'], bind=dropdown, value=top_classes[0])
    
    # Crea il grafico
    chart = alt.Chart(class_distribution_normalized).mark_line().encode(
        x=alt.X('lustro:O', title='Lustri'),
        y=alt.Y('normalized_counts:Q', title='Occorrenze per Video'),
        color=alt.Color('Class:N', title='Classe',scale=alt.Scale(scheme='blueorange',type='quantize')),
        opacity=alt.condition(selector, alt.value(1), alt.value(0.3))
    ).properties(
         width=800,
        height=600
    ).add_params(
        selector
    )
    
    # Salva il grafico in un file JSON
    chart_json = chart.to_json()
    with open('chart.json', 'w') as f:
        f.write(chart_json)
    
    return chart
```
_In questo grafico è stato inoltre creato un selettore a discesa, che permette di selezionare una singola classe per visualizzare con più facilità il suo andamento nel tempo_

**Salvataggio delle classi**: infine è stata definita una funzione che quando applicata alle precedenti permette il salvataggio del grafico in formato json con nome personalizzabile.

```python
def save_chart(chart, filename):
    chart.properties(width="container", height="container").save(filename)
```
_E' stato specificato che, tra le proprietà dei grafici, questi dovessero avere width e height = "container", in modo da permettere il ridimensionamento automatico del grafico nel caso in cui la finestra cambiasse le proprie dimensioni.

##### Fase 5: analisi classi di Nizza
Le analisi svolte si sono poi concentrate sull'utilizzo delle classi di Nizza, ovvero una classificazione universalmente riconosciuta che categorizza gli elementi in precise categorie merceologiche.

**Implementare la classificazione di Nizza nel dataset**: per farlo si è iterato sui file csv precedentemente salvati aggiungendo una colonna che identificasse ogni possibile classe del dataset COCO come appartenente a una precisa categoria di Nizza.

```python
coco_to_nizza = {
    "person": "45",
    "bicycle": "12",
    "car": "12",
    "motorcycle": "12",
    "airplane": "12",
    "bus": "12",
    "train": "12",
    "truck": "12",
    "boat": "12",
    "traffic light": "9",
    "fire hydrant": "9",
    "stop sign": "9",
    "parking meter": "9",
    "bench": "20",
    "bird": "31",
    "cat": "31",
    "dog": "31",
    "horse": "31",
    "sheep": "31",
    "cow": "31",
    "elephant": "31",
    "bear": "31",
    "zebra": "31",
    "giraffe": "31",
    "backpack": "18",
    "umbrella": "18",
    "handbag": "18",
    "tie": "25",
    "suitcase": "18",
    "frisbee": "28",
    "skis": "28",
    "snowboard": "28",
    "sports ball": "28",
    "kite": "28",
    "baseball bat": "28",
    "baseball glove": "28",
    "skateboard": "28",
    "surfboard": "28",
    "tennis racket": "28",
    "bottle": "21",
    "wine glass": "21",
    "cup": "21",
    "fork": "21",
    "knife": "21",
    "spoon": "21",
    "bowl": "21",
    "banana": "31",
    "apple": "31",
    "sandwich": "30",
    "orange": "31",
    "broccoli": "31",
    "carrot": "31",
    "hot dog": "30",
    "pizza": "30",
    "donut": "30",
    "cake": "30",
    "chair": "20",
    "couch": "20",
    "potted plant": "31",
    "bed": "20",
    "dining table": "20",
    "toilet": "11",
    "tv": "9",
    "laptop": "9",
    "mouse": "9",
    "remote": "9",
    "keyboard": "9",
    "cell phone": "9",
    "microwave": "11",
    "oven": "11",
    "toaster": "11",
    "sink": "11",
    "refrigerator": "11",
    "book": "16",
    "clock": "14",
    "vase": "21",
    "scissors": "8",
    "teddy bear": "28",
    "hair drier": "11",
    "toothbrush": "21"
}
```
_Inizialmente si crea una mappa che fa corrispondere a ciascuna classe una categoria di Nizza_

```python
import pandas as pd
import os
def aggiungi_colonna_nizza(file_csv):
    # Leggere il file CSV
    df = pd.read_csv(file_csv)
    
    # Aggiungere la colonna "Nizza" utilizzando la mappa
    df['Nizza'] = df['Class'].map(coco_to_nizza)
    
    # Salvare il file CSV aggiornato
    df.to_csv(file_csv, index=False)
    return df

def aggiorna_tutti_i_file(cartella):
    # Iterare attraverso tutti i file nella cartella
    for filename in os.listdir(cartella):
        # Verifica che il file sia un CSV
        if filename.endswith(".csv"):
            file_path = os.path.join(cartella, filename)
            try:
                # Aggiungi la colonna "Nizza" al file CSV
                df_aggiornato = aggiungi_colonna_nizza(file_path)
                print(f"File aggiornato: {filename}")
            except Exception as e:
                print(f"Errore nell'aggiornare il file {filename}: {e}")
```
_Successivamente si aggiunge la colonna "Nizza" a tutti i file, e si effettua la conversione classe -> Nizza_

**Analisi con classi di Nizza**: non ci sono differenze tecniche rispetto alle analisi precedenti, tranne quando vengono effettuate le analisi relative alle 10 categorie di Nizza più rappresentate (escludendo quella dove ricade la classe "persona" di YOLO).
Viene inizialmente definita una mappa per aggiungere una descrizione alle varie categorie di Nizza:

```python
nizza_descriptions = {
    1: 'prodotti chimici per uso industriale, scientifico e agricolo',
    2: 'vernici, coloranti e preparati usati per la protezione contro la corrosione',
    3: 'preparazioni per toelettatura non medicamentose',
    4: 'oli e grassi industriali, combustibili e illuminanti',
    5: 'prodotti farmaceutici e altre preparazioni per uso medico o veterinario',
    6: 'metalli comuni non lavorati e semilavorati',
    7: 'macchine e utensili meccanici, motori e motori',
    8: 'utensili e strumenti azionati a mano per eseguire compiti',
    9: 'apparecchi e strumenti per scopi scientifici o di ricerca, apparecchi audiovisivi e di tecnologia dell\'informazione, nonché attrezzature per la sicurezza e il salvataggio di vite',
    10: 'apparecchi chirurgici, medici, dentali e veterinari',
    11: 'apparecchi e installazioni per il controllo ambientale',
    12: 'veicoli e apparecchi per il trasporto di persone o merci via terra, aria o acqua',
    13: 'armi da fuoco e prodotti pirotecnici',
    14: 'metalli preziosi e alcuni beni fatti di metalli preziosi o rivestiti con essi',
    15: 'strumenti musicali, loro parti e accessori',
    16: 'carta, cartone e alcuni beni fatti di quei materiali, nonché requisiti per ufficio',
    17: 'materiali isolanti elettrici, termici e acustici e materie plastiche per uso manifatturiero sotto forma di fogli, blocchi e aste',
    18: 'pelle, imitazioni di pelle e alcuni beni fatti di quei materiali',
    19: 'materiali, non di metallo, per la costruzione e costruzione',
    20: 'mobili e loro parti',
    21: 'piccoli utensili e apparecchi a mano per uso domestico e da cucina',
    22: 'tela e altri materiali per la realizzazione di vele, corde, materiali per imbottitura, imbottitura e imbottitura e materie tessili grezze',
    23: 'fili e filati naturali o sintetici per uso tessile',
    24: 'tessuti e coperture di tessuti per uso domestico',
    25: 'abbigliamento, calzature e copricapi per esseri umani',
    26: 'articoli per sarte, capelli naturali o sintetici per essere indossati, e ornamenti per capelli',
    27: 'prodotti destinati ad essere aggiunti come coperture a pavimenti e pareti precedentemente costruiti',
    28: 'giocattoli, apparecchi per giocare, attrezzature sportive, articoli per il divertimento e la novità',
    29: 'alimenti di origine animale, nonché ortaggi e altri prodotti orticoli commestibili preparati o conservati per il consumo',
    30: 'alimenti di origine vegetale, ad eccezione di frutta e verdura, preparati o conservati per il consumo, nonché ausiliari destinati al miglioramento del sapore degli alimenti',
    31: 'prodotti terrestri e marini non sottoposti ad alcuna forma di preparazione per il consumo, animali vivi e piante, nonché alimenti per animali',
    32: 'bevande analcoliche, nonché birra',
    33: 'bevande alcoliche, essenze ed estratti',
    34: 'tabacco e articoli usati per fumare',
    35: 'servizi che coinvolgono la gestione aziendale, l\'operazione, l\'organizzazione e l\'amministrazione di un\'impresa commerciale o industriale',
    36: 'servizi relativi a operazioni bancarie e altre transazioni finanziarie',
    37: 'servizi nel campo della costruzione',
    38: 'servizi che consentono ad almeno una parte di comunicare con un\'altra',
    39: 'servizi per il trasporto di persone, animali o merci da un luogo all\'altro',
    40: 'servizi resi mediante lavorazioni meccaniche o chimiche',
    41: 'servizi costituiti da tutte le forme di istruzione o formazione, servizi aventi lo scopo principale di intrattenimento, divertimento o ricreazione delle persone',
    42: 'servizi forniti da persone in relazione agli aspetti teorici e pratici di campi complessi di attività',
    43: 'servizi forniti in relazione alla preparazione di cibi e bevande per il consumo',
    44: 'assistenza medica',
    45: 'servizi legali e di sicurezza'
}
```

Successivamente viene creato il grafico dell'evoluzione nel tempo delle classi di Nizza:
```python
import altair as alt
import pandas as pd
def analyze_top_classes_excluding_most_represented(data):
# Calcola la frequenza delle classi di Nizza
    total_class_frequency = data['Nizza'].value_counts()
    most_represented_class = total_class_frequency.idxmax()
    top_classes = total_class_frequency[total_class_frequency.index != most_represented_class].head(10).index

    # Aggiungi una colonna con le descrizioni delle classi di Nizza
    data['Description'] = data['Nizza'].map(nizza_descriptions)
    
    print(data)
    
    # Filtra i dati per le top classi escludendo la più rappresentata
    filtered_data = data[data['Nizza'].isin(top_classes)]
    class_distribution_by_year = filtered_data.groupby(['lustro', 'Nizza','Description']).size().reset_index(name='counts')
    
    # Calcola il numero di video per lustro
    videos_per_year = filtered_data.groupby('lustro')['video_id'].nunique().reset_index()
    videos_per_year.columns = ['lustro', 'num_videos']
    
    # Normalizza la distribuzione delle classi per il numero di video
    class_distribution_normalized = pd.merge(class_distribution_by_year, videos_per_year, on='lustro')
    class_distribution_normalized['normalized_counts'] = class_distribution_normalized['counts'] / class_distribution_normalized['num_videos']
    
    # Crea un selettore a discesa per le classi di Nizza
    dropdown = alt.binding_select(options=top_classes.tolist(), name='Seleziona Classe di Nizza: ')
    selector = alt.selection_point(fields=['Nizza'], bind=dropdown, value=top_classes[0])
    
    # Crea il grafico
    chart = alt.Chart(class_distribution_normalized).mark_line().encode(
        x=alt.X('lustro:O', title='Lustri'),
        y=alt.Y('normalized_counts:Q', title='Occorrenze per Video'),
        color=alt.Color('Nizza:N', title='Nizza',scale=alt.Scale(scheme='blueorange',type='quantize')),
        
        opacity=alt.condition(selector, alt.value(1), alt.value(0.3)),
        tooltip=[alt.Tooltip('Nizza:N', title='Classe di Nizza'),
                 alt.Tooltip('Description:N', title='Descrizione della Classe')
                 ]
    ).properties(
        #title='Evoluzione delle Top 10 classi di Nizza nel Tempo (Escludendo la Più Rappresentata, Normalizzata per Numero di Video)',
        width=800,
        height=600
    ).add_params(
        selector
    ).interactive(bind_x = False, bind_y = False)
    
    # Salva il grafico in un file JSON
    chart_json = chart.to_json()
    with open('chart.json', 'w') as f:
        f.write(chart_json)

    return chart
```
_Nel grafico è stato implementato un selettore a cascata (parametro "selector"), che permette di scegliere quale classe di Nizza visualizzare con più facilità. 
E' stato aggiunto un tooltip che visualizza (passandoci sopra con il cursore) le informazioni relative alla classe di Nizza a cui appartiene quel punto e la sua descrizione, per aumentare l'intelligibilità del grafico.
E' stato aggiunto l'elemento "interactive" dopo i parametri per poter visualizzare il tooltip, tuttavia con argomenti "bind_x" e "bind_y" = FALSE, in quanto altrimenti il grafico si sarebbe ridimensionato con lo srolling del cursore sopra di esso._

##### Fase 6: utilizzo di Jekyll per la creazione del sito web
Per l'implementazione dei grafici sono stati presi degli accorgimenti in quanto questi non venivano visualizzati correttamente.
```html
<vegachart schema-url="{{site.baseurl}}/assets/charts/entity_charts/top_classes_evolution_lustrum.json" style="width:100%;height:400px;"></vegachart>  

```
_Si sono dovute specificare le dimensioni di width e height, con quest'ultima avente una dimensione in pixel, per poter visualizzare i grafici.