# EMit - Emanuele Muzio 0766230

Repository del corso di NLP contenente i due notebook usati per svolgere i task A e B.

Entrambi i task hanno avuto come base la classificazione di un dataset contenente messaggi dai vari social sui programmi televisivi RAI (e non, detti OOD perchè Out-Of-Domain, ovvero fuori dal dominio principale rappresentato dei messaggi relativi all'emittente RAI).

## Dataset OOD e In-Domain

Per l'addestramento è stato fornito un dataset etichettato contenente tra i 5000 e i 6000 messaggi, per i test invece sono stati forniti due dataset diversi per mettere alla prova la capacità di classificazione:

- il primo contenente dati all'interno del già menzionato dominio dei messaggi sui programmi RAI in onda (In-Domain)
- il secondo contenente dati su materie fuori da questo dominio ristretto (OOD)

## Step

Per entrambi i task è stato adottato lo stesso procedimento e gli stessi test, variando però gli iperparametri utilizzati. Nel dettaglio, i tre step affrontati sono i seguenti:
- preprocessing del testo
- addestramento
- test

### Step 1: Preprocessing

Per valutare le capacità del classificatore (che sfrutta al suo interno un modello BERT-like multilingua, case sensitive e in grado di gestire le emoji/emoticons presenti nei dati) sono state effettuati dei test sia usando i dati raw, così come sono stati forniti, che dati testuali preprocessati.

In particolare, per il preprocessing sono state effettuate le seguenti operazioni:
- rimozione degli hashtag (la maggior parte sono relativi ai programmi televisivi menzionati)
- rimozione delle stopword
- rimozione degli hashtag
- rimozione dei collegamenti ipertestuali
- rimozione delle keyword relative al social X (RT, FAV)

### Step 2: Addestramento

Dopo aver effettuato la separazione e pulizia dei dati, è stata definita l'architettura del modello usato per la classificazione:
- BERT-like model per l'elaborazione degli input tokenizzati
- Dropout layer
- Layer dense
- Sigmoide

Per valutare l'accuracy del modello durante l'addestramento e la loss, sono state rispettivamente utilizzate la MultiLabelAccuracy e la BCELoss (Binary Cross-Entropy) da Pytorch.

Per la ricerca degli iperparametri migliori, sono state usate 4 configurazioni ed effettuati test su dati sia preprocessati che non.

A seguito della fase di addestramento, sono stati salvati i grafici dell'andamento per ogni task e ogni configurazione.

### Step 3: Classificazione

Ciascun task si è concluso con due test (uno su dati in-domain e l'altro su dati OOD) per valutare le reali capacità del classificatore usando ogni configurazione a disposizione, e generando dei report di classificazione grafici (visionabili all'interno dei notebook) con i risultati.

La metrica principale utilizzata per valutare le classificazione è l'F1 (average macro score).

## Task A: Sentiment Analysis

Il primo task ha avuto come obiettivo la classificazione binaria multilabel dei messaggi sulla base delle 8 emozioni base di Plutchik, più _Love_ e _Neutral_.

## Task B: Target Detection

Identificazione del target: i vari messaggi sono infatti indirizzati verso la direzione del programma, il topic (argomento), entrambi o nessuno dei due.

## File

I file di grandi dimensioni verranno conservati per un breve lasso di tempo sul mio PC per poi venire eliminati per fare spazio, tuttavia le configurazioni che hanno prodotto i risultati migliori, così come i grafici, verranno mantenuti su github.


