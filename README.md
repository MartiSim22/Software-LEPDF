# Software-LEPDF

LEPDF - Lettore ed Estrattore_pdf

Autore : Martina Simonetti
Data : 13/04/2021


## Sommario

### Introduzione
### Audience
### Requisiti di sistema
### Descrizione del software:
- 3.1 Obiettivo
- 3.2 Componenti
- 3.3 Licenza
### Per iniziare
- 4.1 Installazione
- 4.2 Esecuzione del software




## Abstract
Il software consente di ricevere in input uno o più documenti in formato PDF e ricevere in output un unico documento CSV. Il documento CSV di output è composto da una singola tabella con al suo interno tutti i valori legati ad un argomento scelto presente in tutti i documenti che vengono inseriti in input. Inoltre, l’utente può scegliere quali pagine del documento,quali tabelle , righe o colonne da analizzare, per essere sicuro di ricevere in output solamente i valori di interesse.

## Introduzione
Il software nasce dall’idea di analizzare i cambiamenti inerenti ad alcuni campi del settore automobilistico durante il periodo della pandemia da COVID-19. Il primo passo è stato quello di ricavare i dati relativi all’immatricolazione di autoveicoli dal sito UNRAE e , dopo aver notato che la maggioranza dei dati forniti dal sito era racchiusa in documenti PDF, è nata l’idea di creare un programma che prenda in input tali file, uno per ogni data : ogni documento contiene delle righe rappresentanti le provincie italiane e delle colonne per diverse marche d’auto. Il risultato è un unico file CSV che mostra l’andamento dell’immatricolazione di autoveicoli per mese nel corso degli anni 2018-2021.

## Audience
L’utente dovrà apportare delle modifiche per rendere il programma idoneo ai propri fini, quindi sono opportune delle conoscenze pregresse del linguaggio di programmazione Python. Il software è consigliato a chiunque voglia effettuare un’analisi approfondita di un grande numero di documenti PDF trasformandoli in un unico file CSV. 


## Descrizione del software
### 4.1 Obiettivo
Il software LEPDF consente all’utente di leggere dei file con estensione PDF, organizzati per data, ed estrarre da essi degli argomenti selezionati relativi ad uno o più brand, che verranno proposti in output in un unico file di tipo CSV. Per brand si intende una singola riga del file in input, mentre per argomento si intende la singola colonna del file in input.


### 4.2 Componenti
Il software LEPDF è composto e da due moduli, organizzati in un unico notebook jupyter:

-Il modulo di Configurazione permette all’utente di personalizzare il software in modo da estrarre correttamente le informazioni dai propri file in input. Esso è formato da sei parti: la funzione configurazione(), che consente di associare determinati parametri ai documenti che sono riconosciuti dal programma grazie alla nomenclatura assegnatagli dall’utente, le variabili personalizzabili ‘colonna’ e ‘riga’;l’array colname che contiene le ridenominazioni delle colonne i cui nomi sono stati estratti in maniera errata; l’array indexname che contiene le ridenominazioni delle righe i cui nomi sono stati estratti in maniera errata; la lista subset contenente il nome/i delle colonne di cui voglio verificare i valori; e  la lista ‘date_toskip’, in cui l’utente inserisce i nomi dei file (senza estensione) che non vuole analizzare.

-Il modulo di Esecuzione si divide in due parti a seconda del numero di volte che si è eseguita la funzione. Se eseguo la funzione per la prima volta, il modulo di Esecuzione darà come risultato i dataframe delle mie tabelle, per controllare gli eventuali errori dell’analisi e per decidere i futuri parametri da utilizzare nella funzione camelot.read_pdf().  Invece, se il modulo esecuzione è stato eseguito per un numero di volte > 1 , il risultato sarà la lettura di ogni file in input con la produzione di un unico file di output.



### 4.3 Licenza
Il software è rilasciato con licenza MIT.


## Utilizzo del software
### 5.1 Installazione
E’ necessaria l’installazione di Jupyter-lab: https://jupyter.org 
E’ possibile scaricare il software da questo link github : https://github.com/MartiSim22/Software-LEPDF
E’ necessario rinominare i propri file con la nomenclatura seguente per favorire il corretto funzionamento del software: un file riferito al gennaio del 2018 dovrà essere rinominato 2018_1 e così tutti gli altri. Praticamente il nome di ogni file corrisponde alla sua data. 
Tutti i file dovranno essere inseriti in un'unica cartella chiamata DATI.

### 5.2 Esecuzione del software
E’ importante che prima di utilizzare il software il codice venga personalizzato secondo i propri interessi. Nello specifico:

Personalizzare la lista_anni e la lista_mesi in base al periodo di interesse: 
-	lista_anni = np.arange(2018,2022) - Inserire nella parentesi il periodo di tempo che coprono i file per quanto riguarda l’anno assicurandosi che il secondo numero sia avanti di un anno: in questo caso se i miei file vanno dal 2018 al 2021 inserisco 2018 e 2022.
-	lista_mesi = np.arange(1,13) - Inserire nella parentesi il periodo di tempo che coprono i file per quanto riguarda il mese assicurandosi che il secondo numero sia avanti di un mese: in questo caso se i miei file vanno da gennaio (1) a dicembre (12)  allora inserisco 1 e 13.

Personalizzare la funzione di configurazione in base agli anni e i mesi dei propri file e scegliere i parametri che si vogliono ricercare. 
Quelli utilizzati di default nel software sono:
-	ext , che indica l’estensione del file 
pages , che indica quali pagine analizzare del mio file (es. “2” - analizza solo la pagina numero 2 del mio file PDF ; “all” - analizza tutte le pagine del mio file). 
-	flavor , indica il metodo di analisi dei dati dal mio file. In questo caso il metodo utilizzato è “stream”,che viene utilizzato principalmente per tabelle che hanno spazi bianchi tra le celle per crearne la struttura.
-	row_tol,  avvicina le righe tra loro, arrivando anche a raggrupparle. Utile quando un valore che dovrebbe essere in un’unica riga, viene diviso in due righe consecutive.
-	strip_text,  serve per rimuovere eventuali caratteri indesiderati (spazi, punti, nuove righe) da una stringa.
-	splittext , serve per dividere tutte le stringhe che si trovano in celle diverse; ma che sono state assegnate ad una singola cella durante l’analisi dei dati.
-	table_areas, da utilizzare nei casi in cui l’area della tabella non è stata trovata correttamente. table_areas consiste in una stringa contenente le coordinate x,y top-left, 	x,y bottom-right della tabella. 
-	columns, da utilizzare nei casi in cui non tutti i separatori delle colonne della tabella sono state trovate correttamente in maniera automatica. columns consiste in una stringa contenente tutte le coordinate x per ogni separatore di colonna della mia tabella

Inserire i nomi dei file - senza estensione - da non analizzare nella lista date_toskip. Questi file da non analizzare potrebbero non esistere (tenendo in considerazione che la funzione prende in input i file anno per anno, per ogni mese, potrebbe capitare che non ho file per alcuni mesi-anni) o semplicemente sono file di cui non sono interessato a ricavare i dati. 

Rinominare i nomi delle colonne per ogni tabella nella lista colname, qualora siano stati estratti in maniera incorretta.  La lista colname viene richiamata successivamente dalla funzione df.rename

Rinominare i nomi delle righe per ogni tabella nella lista indexname, qualora siano stati estratti in maniera incorretta.  La lista indexname viene richiamata successivamente dalla funzione dftot.rename

Inserire nella variabile subset le colonne di cui voglio controllare i valori. La variabile subset viene richiamata nella funzione df.drop_duplicates che elimina le eventuali righe che hanno gli stessi valori per le colonne scelte.

Inserire il nome della riga/righe di interesse nella variabile riga 

Inserire il nome della colonna/e di interesse nella variabile colonna

Inserire il percorso dei propri file nella riga nel quale viene specificato:  file = "/"
Camelot accetta solamente il “path completo” di un file, ciò viene ricavato nel software utilizzando la libreria Os di Python.

Nella riga tables = camelot.read_pdf(file,....) personalizzare i parametri in base a quelli utilizzati nella funzione di configurazione facendo attenzione a lasciare nella parentesi file. Il parametro file viene definito dall’utente con il path completo dei file che vuole analizzare.

Nell’ultima riga del software inserire il nome che si desidera per il proprio documento csv.


