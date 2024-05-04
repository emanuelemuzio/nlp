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

Per ricercare la combinazione migliore di iperparametri, sono state definite due griglie di iperparametri e svolti 8 addestramenti totali per task (4 per dati non preprocessati, 4 per dati preprocessati), randomizzando di volta in volta la configurazione, arrivando a risultati non particolarmente soddisfacenti per il task A e leggermente migliori per il task B.

A seguito della fase di addestramento, sono stati salvati i grafici dell'andamento per ogni task e ogni configurazione.

### Step 3: Classificazione

Ciascun task si è concluso con due test (uno su dati in-domain e l'altro su dati OOD) per valutare le reali capacità del classificatore usando ogni configurazione a disposizione, e generando dei report di classificazione grafici (visionabili all'interno dei notebook) con i risultati.

La metrica principale utilizzata per valutare le classificazione è l'F1 macro score, secondo cui la massima precisione raggiunta è stata ottenuta nel secondo task (circa 0.6).

## Task A: Sentiment Analysis

Il primo task ha avuto come obiettivo la classificazione binaria multilabel dei messaggi sulla base delle 8 emozioni base di Plutchik, più _Love_ e _Neutral_.

## Task B: Target Detection

Identificazione del target: i vari messaggi sono infatti indirizzati verso la direzione del programma, il topic (argomento), entrambi o nessuno dei due.

### Grafici

A seguire, una lista completa dei grafici riassuntivi dei risultati ottenuti e i link ai pesi:
- Task A:
  - [Addestramento no prep](https://drive.google.com/file/d/1iXBAbY43_Tw1WSnjK1D2mLcDbZCirxGb/view?usp=sharing)
  - [Addestramento prep](https://drive.google.com/file/d/1sPFlXhJvG9D3YKXhtPzdOCNJt7kT4ZMx/view?usp=sharing)
  - [Heatmap no prep](https://drive.google.com/file/d/19t0cPO_tcS9yg5R9i2XkHS_xo6__xQ8W/view?usp=sharing)
  - [Heatmap prep](https://drive.google.com/file/d/1nCmq7sZX9WUvkbqQxjJDAUm7608MJTok/view?usp=sharing)
  - [No prep recap csv](https://drive.google.com/file/d/1rjvX-wNjx3pZVlNe7cT4GTt_amX1M1UQ/view?usp=sharing)
  - [Prep recap csv](https://drive.google.com/file/d/18CiB5ZGjbt6g-E8cCbOg00xhep-jgamP/view?usp=sharing)
  - [Pesi prep OOD](https://drive.google.com/file/d/11_Mf4UOQ2oFRa1FHR8pDnExCAtw8peaZ/view?usp=sharing)
  - [Pesi prep in-domain](https://drive.google.com/file/d/1K2q7mmLVQUbuFwTNFe-OY9Rc9sDd1RQX/view?usp=sharing)
  - [Pesi no prep in-domain](https://drive.google.com/file/d/1tvUT4P9BCw19X1GjPO1GkHAG3EFy48g-/view?usp=sharing)
  - [Pesi no prep OOD](https://drive.google.com/file/d/1-sC-eECWFslCtICXQd1RGiZ00rtOxq-k/view?usp=sharing)
- Task B:
  - [Addestramento no prep](https://drive.google.com/file/d/10Tz5dwxsv1yLnUrWguV5a6dNzT9VoGhm/view?usp=sharing)
  - [Addestramento prep](https://drive.google.com/file/d/16iZlN-jenst9X6A00cxBJVFgYo9Zj9g-/view?usp=sharing)
  - [Heatmap no prep](https://drive.google.com/file/d/1-5EdY8vaCbN0qNaSi0MNpsH3i7wc9IA1/view?usp=sharing)
  - [Heatmap prep](https://drive.google.com/file/d/1-MW04xy7OkvnKjamJArcRqCvgNh1xDbT/view?usp=sharing)
  - [No prep recap csv](https://drive.google.com/file/d/1-2oxipWAx6vNos9558RKCiha3tvWFUDZ/view?usp=sharing)
  - [Prep recap csv](https://drive.google.com/file/d/1-IpSfiy-tKtsSjIBhT1iq05WaikJ7JXr/view?usp=sharing)
  - [Pesi prep OOD](https://drive.google.com/file/d/1-EcqhkihtM4fqXhw82kRRbq4w9QKBEVB/view?usp=sharing)
  - [Pesi prep in-domain](https://drive.google.com/file/d/1-640pOYr3y1DUhpe4NdA_QCXon176u8I/view?usp=sharing)
  - [Pesi no prep in-domain](https://drive.google.com/file/d/1-0R21vWj7mgPQt-G6CZ5UPewZZsyIdxb/view?usp=sharing)
  - [Pesi no prep OOD](https://drive.google.com/file/d/1-0hPGehAXt2vFRSlcR4QsguzB4S_iuiK/view?usp=sharing)
