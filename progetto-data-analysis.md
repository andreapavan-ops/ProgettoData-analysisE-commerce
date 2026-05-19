# ðŸ“Š Progetto Trasversale â€” Analizza un Dataset Reale

> **Progetto individuale** che attraversa tutti e 3 i giorni del corso di Data Analysis.
> Ogni giornata aggiunge un pezzo al tuo Jupyter notebook finale.

---

## ðŸŽ¯ Obiettivo

Nelle 12 ore del corso imparerai a usare **pandas** per esplorare, pulire e analizzare dati reali. Per consolidare ciÃ² che impari, sceglierai **un dataset** dalla lista qui sotto e lo analizzerai a fondo, costruendo un **Jupyter notebook** che alla fine racconterÃ  una piccola storia fatta di numeri, grafici e insight.

Alla fine del Giorno 3 ognuno presenterÃ  brevemente i propri **2-3 insight piÃ¹ interessanti** ai compagni: ci confronteremo su domini diversi (vendite, musica, cinema, dati sociali, sport) per vedere come gli stessi strumenti tirino fuori scoperte molto diverse.

---

## ðŸ› ï¸ Strumento di lavoro: Jupyter o Google Colab

Puoi lavorare con **qualunque dei due strumenti**, scegli quello con cui ti trovi meglio:

| Strumento | Quando sceglierlo |
|---|---|
| **Google Colab** (consigliato per neofiti) | Non vuoi installare nulla, lavori da PC diversi, hai un account Google. Tutto gira nel browser, le librerie sono giÃ  installate. |
| **Jupyter Notebook locale** | Hai giÃ  Python + Jupyter installato e preferisci lavorare offline. |

Entrambi gli strumenti producono lo stesso file `.ipynb`, quindi il **deliverable Ã¨ identico**.

> ðŸ“Ž **Starter notebook**: ti viene fornito un file `progetto_starter.ipynb` con la struttura del progetto giÃ  pronta, le librerie da importare e i tre modi di caricare il dataset spiegati. Aprilo, salvane una copia con il tuo nome, e parti da lÃ¬. Lo trovi in fondo al brief.

---

## ðŸ—“ï¸ Come si articola nei 3 giorni

| Giorno | Tema della lezione | Cosa fai sul progetto |
|---|---|---|
| **1** | Esplorare i dati | Scegli il dataset, lo carichi, lo esplori, rispondi alla **Q1** |
| **2** | Trasformare i dati | Pulisci il dataset e rispondi a **Q2, Q3, Q4** con `groupby` e analisi temporali |
| **3** | Visualizzare e raccontare | Crei i grafici, rispondi a **Q5**, finalizzi il notebook, prepari la presentazione |

---

## ðŸ—‚ï¸ Step 1 â€” Scegli il tuo dataset

Sono 5 opzioni. **Scegli quella che ti incuriosisce di piÃ¹**: l'analisi Ã¨ molto piÃ¹ piacevole quando l'argomento ti interessa davvero. Tutti i dataset sono su **Kaggle** (serve un account gratuito) e hanno un livello di difficoltÃ  comparabile.

### Opzione 1 â€” Sample Superstore (E-commerce) ðŸ›’

- **Link**: https://www.kaggle.com/datasets/vivek468/superstore-dataset-final
- **Cosa contiene**: ~10.000 ordini di una catena di negozi USA. Per ogni ordine hai data, cliente, segmento, regione, categoria di prodotto, vendite, sconto, profitto.
- **PerchÃ© Ã¨ interessante**: ci sono ordini in **perdita** â€” non tutto quello che vendi ti fa guadagnare. Scoprirai dove l'azienda perde soldi e perchÃ©.
- **A chi piace**: a chi vuole ragionare come un analista di business.

### Opzione 2 â€” Most Streamed Spotify Songs 2023 ðŸŽµ

- **Link**: https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023
- **Cosa contiene**: ~950 brani piÃ¹ ascoltati nel 2023, con artista, numero di stream, BPM, danceability, energia, valenza e presenza nelle playlist di Spotify, Apple Music e Deezer.
- **PerchÃ© Ã¨ interessante**: cosa rende una canzone una hit? Ãˆ una questione di ritmo, energia, o pura fortuna? Scoprilo.
- **A chi piace**: a chi ascolta musica e vuole capire cosa accomuna le canzoni di successo.

### Opzione 3 â€” Netflix Movies and TV Shows ðŸŽ¬

- **Link**: https://www.kaggle.com/datasets/shivamb/netflix-shows
- **Cosa contiene**: ~8.800 titoli del catalogo Netflix con tipo (film/serie), regista, cast, paese, anno di uscita, data di aggiunta su Netflix, rating, durata, generi.
- **PerchÃ© Ã¨ interessante**: Netflix sta diventando piÃ¹ "internazionale"? Cosa preferisce produrre o comprare? Si possono fare grafici sulla crescita esplosiva del catalogo.
- **A chi piace**: a chi Ã¨ curioso di capire la strategia di un colosso dello streaming.

### Opzione 4 â€” World Happiness Report ðŸŒ

- **Link**: https://www.kaggle.com/datasets/mathurinache/world-happiness-report
- **Cosa contiene**: il punteggio di felicitÃ  dei paesi del mondo dal 2015 al 2022, **un CSV per ogni anno**. Per ogni paese: PIL pro capite, supporto sociale, aspettativa di vita, libertÃ , generositÃ , fiducia nelle istituzioni.
- **PerchÃ© Ã¨ interessante**: che cosa rende felice un paese? I soldi? La libertÃ ? La sanitÃ ? E l'Italia dove si posiziona? Ottimo per ragionare su correlazioni e dati socio-economici reali.
- **A chi piace**: a chi vuole un tema "civico" e si trova bene a unire piÃ¹ file (servirÃ  `concat` per metterli insieme).

### Opzione 5 â€” International Football Results âš½

- **Link**: https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017 *(non farti confondere dall'URL: il dataset Ã¨ aggiornato fino al 2025)*
- **Cosa contiene**: ~49.000 partite internazionali di calcio dal 1872 ad oggi, con data, squadre, gol, torneo, cittÃ , paese, campo neutrale sÃ¬/no.
- **PerchÃ© Ã¨ interessante**: l'Italia Ã¨ davvero cosÃ¬ forte come dicono? Esiste il "fattore campo"? Il calcio Ã¨ diventato piÃ¹ offensivo nel tempo? Tante storie nascoste nei numeri.
- **A chi piace**: agli appassionati di calcio e a chi vuole lavorare con un dataset grande e storico.

---

## â“ Step 2 â€” Le domande di ricerca

Per ogni dataset trovi **5 domande obbligatorie** + **1 domanda bonus** opzionale per chi finisce in anticipo o vuole spingersi oltre.

Le domande hanno tutte la stessa struttura logica, indipendentemente dal dataset:
- **Q1** â†’ esplorativa: capire la forma del dataset
- **Q2** â†’ aggregazione con `groupby`
- **Q3** â†’ analisi temporale
- **Q4** â†’ segmentazione o confronto tra categorie
- **Q5** â†’ critica/aperta: trarre una conclusione, non solo calcolare un numero
- **Bonus** â†’ introduce una tecnica nuova

### ðŸ›’ Domande per chi sceglie Superstore

1. Quanti ordini, prodotti, clienti, regioni e categorie ci sono? Su che periodo si estendono i dati?
2. Quali categorie e sotto-categorie generano **piÃ¹ vendite** e quali **piÃ¹ profitti**? Ci sono sotto-categorie in perdita?
3. Come variano le vendite **mese per mese**? Si vede una stagionalitÃ ? Qual Ã¨ il mese migliore e quello peggiore?
4. I 3 segmenti di clienti (Consumer, Corporate, Home Office) sono ugualmente profittevoli? Chi compra di piÃ¹, chi rende di piÃ¹?
5. **Lo sconto fa bene o male all'azienda?** Esiste una soglia di sconto oltre la quale il profitto diventa negativo?

**Bonus â€” Principio di Pareto:** verifica se vale anche qui la regola dell'80/20. Quanti prodotti (in percentuale) generano l'80% del profitto totale? Visualizzalo con un grafico cumulativo.

### ðŸŽµ Domande per chi sceglie Spotify

1. Quanti brani e quanti artisti diversi ci sono? Da che anno di pubblicazione partono i brani in classifica?
2. Quali sono i **top 10 artisti** per numero di brani in top e per stream totali? Coincidono?
3. Le caratteristiche audio (BPM, danceability, energy, valence) **cambiano nel tempo**? I brani recenti sono piÃ¹ veloci o piÃ¹ lenti, piÃ¹ o meno "energici" di quelli vecchi?
4. I brani piÃ¹ ascoltati su Spotify sono presenti anche su **Apple Music e Deezer**? C'Ã¨ correlazione tra le piattaforme o esistono brani "monopiattaforma"?
5. **Quale ingrediente fa sfondare un brano nel 2023?** Esiste correlazione tra le metriche audio e il numero di stream, o il successo Ã¨ imprevedibile?

**Bonus â€” L'identikit della hit:** costruisci il "profilo audio medio" del top 10% di brani piÃ¹ ascoltati e confrontalo con il restante 90%. Esistono caratteristiche audio nettamente diverse? Mostralo con un grafico a barre comparativo.

### ðŸŽ¬ Domande per chi sceglie Netflix

1. Quanti titoli totali? Qual Ã¨ il rapporto film vs serie TV? Quanti paesi di produzione diversi?
2. Quali sono i **top 10 paesi** per numero di produzioni? Come si distribuiscono film vs serie tra questi paesi?
3. Come Ã¨ **cresciuto il catalogo** anno per anno (`date_added`)? E come si distribuiscono i titoli per `release_year`? C'Ã¨ uno scarto tra "quando un titolo Ã¨ uscito" e "quando Ã¨ arrivato su Netflix"?
4. Quali sono i **generi piÃ¹ frequenti** (`listed_in`)? I generi popolari nei film sono gli stessi delle serie TV?
5. **Esiste un "film tipo" su Netflix?** Qual Ã¨ la durata media dei film e il numero medio di stagioni delle serie? Quali rating sono i piÃ¹ frequenti? Ci sono outlier degni di nota?

**Bonus â€” I volti di Netflix:** il campo `cast` contiene una lista di attori in una singola stringa separata da virgole. Trasformala in righe separate e trova i **10 attori che compaiono in piÃ¹ titoli** del catalogo.

### ðŸŒ Domande per chi sceglie World Happiness

1. Nell'anno piÃ¹ recente disponibile, quali sono i **10 paesi piÃ¹ felici** e i 10 meno felici? Dove si posiziona l'Italia?
2. Quale fattore (PIL pro capite, supporto sociale, aspettativa di vita, libertÃ , generositÃ , fiducia nelle istituzioni) **correla di piÃ¹** con il punteggio di felicitÃ ?
3. Come Ã¨ cambiato il punteggio dell'**Italia** dal 2015 a oggi? Confrontalo con altri 3 paesi europei a tua scelta. *(Richiede di unire i CSV di piÃ¹ anni: ottima palestra per `concat`.)*
4. Mediamente, quale **regione del mondo** Ã¨ piÃ¹ felice? Ci sono differenze marcate tra continenti?
5. Esistono paesi **anomali** â€” con punteggio alto nonostante un PIL basso, o viceversa? Cosa potrebbe spiegarlo?

**Bonus â€” Chi Ã¨ salito, chi Ã¨ sceso:** confrontando il primo e l'ultimo anno disponibile, quali sono i **5 paesi che hanno guadagnato piÃ¹ posizioni** in classifica e i 5 che ne hanno perse di piÃ¹? Visualizzalo con un grafico "before-after".

### âš½ Domande per chi sceglie International Football Results

1. Quante partite totali, quante nazionali, quanti tornei diversi? In che anno Ã¨ la prima partita registrata?
2. Quali nazionali hanno **vinto piÃ¹ partite** di sempre? E con la piÃ¹ alta **percentuale di vittorie** (su almeno 100 partite giocate)?
3. Il record dell'**Italia**: quante partite, quante vittorie/pareggi/sconfitte, qual Ã¨ stato il decennio migliore e quello peggiore?
4. Esiste davvero il **"fattore campo"**? Le squadre di casa vincono piÃ¹ spesso? E nei tornei in campo neutrale come cambia?
5. Il calcio Ã¨ diventato **piÃ¹ offensivo o piÃ¹ difensivo** nel tempo? Come Ã¨ cambiato il numero medio di gol per partita dal 1900 a oggi?

**Bonus â€” Le grandi rivalitÃ :** trova le **10 coppie di nazionali** che si sono affrontate piÃ¹ volte nella storia. Per ognuna calcola il bilancio (vittorie squadra A, vittorie squadra B, pareggi). C'Ã¨ una squadra dominante o sono coppie equilibrate?

---

## ðŸ““ Step 3 â€” Il deliverable: il Jupyter Notebook

Il deliverable Ã¨ **un solo file** chiamato `progetto_NOME_COGNOME.ipynb`.

Deve avere queste **sezioni nell'ordine**:

### 1. Introduzione
- Titolo del progetto, nome e cognome
- Quale dataset hai scelto e perchÃ©
- Link al dataset su Kaggle
- Breve descrizione delle colonne piÃ¹ importanti
- Le 5 domande di ricerca che ti poni (copiate dal brief)

### 2. Caricamento ed esplorazione iniziale â†’ risponde alla **Q1**
- Carica il dataset con `pd.read_csv(...)` (e `pd.concat([...])` se sei sul World Happiness, che ha un file per anno)
- A seconda di dove lavori, scegli **una** di queste tre modalitÃ  (sono tutte giÃ  pronte nello starter notebook):
  - **Jupyter locale**: metti il CSV nella stessa cartella del notebook e usa `pd.read_csv("file.csv")`
  - **Colab + upload manuale**: usa `files.upload()` per caricare il file a ogni sessione
  - **Colab + Google Drive** (consigliato): monta Drive con `drive.mount(...)` e leggi da lÃ¬
- Esegui `head()`, `info()`, `describe()`, `shape`
- Prime osservazioni **commentate in testo Markdown**

### 3. Pulizia del dataset
- Gestione dei missing values (cosa fai con i NaN? Li elimini? Li riempi?)
- Conversione dei tipi sbagliati (es. date in `to_datetime`)
- Eventuali duplicati o anomalie
- **Spiega in testo le scelte fatte** â€” non basta pulire, bisogna giustificare il "perchÃ©"

### 4. Analisi â†’ risponde a **Q2, Q3, Q4, Q5**
- Una sotto-sezione Markdown per ogni domanda
- Per ogni domanda: codice + output + **commento testuale** che risponde
- Almeno un grafico per ogni domanda

### 5. Conclusioni e insight chiave
- 2-3 paragrafi che riassumono le scoperte piÃ¹ interessanti
- Cosa ti ha sorpreso? Cosa NON ti aspettavi?

### 6. (Opzionale) Bonus
- Se hai fatto la domanda bonus, mettila qui

### âœ… Regole di "buon notebook"

- **Ogni cella di codice ha un senso** e produce un output utile (no celle morte o di prova)
- Ogni risultato Ã¨ **commentato in testo Markdown** sotto la cella
- I grafici hanno **titolo**, **etichette degli assi** e legenda se serve
- Il notebook si puÃ² **eseguire dall'inizio alla fine senza errori** (controllo con `Kernel â†’ Restart & Run All`)
- Niente copia-incolla dai compagni: l'idea Ã¨ che TU analizzi il dataset

---

## ðŸŽ¤ Step 4 â€” La presentazione finale (3 minuti)

Alla fine del Giorno 3 ognuno presenta brevemente i propri risultati. **Non Ã¨ un report tecnico, Ã¨ il momento "wow, guardate cosa ho scoperto!"**.

Per il tuo turno prepara:

| Tempo | Contenuto |
|---|---|
| **30 secondi** | Quale dataset hai scelto e perchÃ© |
| **2 minuti** | **2-3 insight chiave** che hai trovato â€” le scoperte piÃ¹ sorprendenti, non un riassunto delle Q1-Q5 |
| **30 secondi** | Il tuo **grafico killer** â€” quello che racconta meglio i tuoi insight |

### Come prepararti
- Apri il tuo notebook sul grafico migliore in fullscreen
- **Non leggere il codice** ad alta voce
- Mostra **scoperte**, non procedure: dÃ¬ *"ho scoperto che le vendite di Tavoli sono in perdita del 40%"* invece di *"ho fatto un groupby per categoria e ho stampato il profitto medio"*
- Sii pronto a rispondere a 1-2 domande dei compagni

---

## ðŸ’¡ Consigli pratici per partire bene

1. **Scegli il dataset all'inizio del Giorno 1 e non cambiarlo.** Cambiare dataset a metÃ  significa rifare tutto da capo.
2. **Leggi attentamente la descrizione del dataset su Kaggle** prima di iniziare. Capire bene cosa significa ogni colonna ti farÃ  risparmiare ore.
3. **Lavora a piccoli passi.** Una cella, un risultato, un commento, avanti. Non scrivere 50 righe di codice tutte insieme.
4. **Salva spesso** e committa il notebook in una cartella personale (idealmente Git, se sei abituato).
5. **Quando sei in difficoltÃ **, prima rileggi le slides della lezione e poi cerca su Stack Overflow / docs di pandas. La documentazione di pandas Ã¨ eccellente.
6. **Confrontati con i compagni** sui concetti, non copiare il codice: chi sceglie il tuo stesso dataset farÃ  comunque scoperte diverse perchÃ© interpreterÃ  i numeri in modo diverso.

## âš ï¸ Errori comuni da evitare

- âŒ Generare 30 grafici a caso senza commentarli â€” meglio **5 grafici significativi** ben spiegati
- âŒ Lasciare colonne con NaN senza decidere come gestirli
- âŒ Usare numeri grezzi senza interpretarli: *"il valore Ã¨ 234.5"* non significa niente se non spieghi cosa rappresenta
- âŒ Confondere **correlazione** e **causalitÃ **: se A Ã¨ correlato a B, non significa che A causa B
- âŒ Aspettare il Giorno 3 per pensare alla presentazione: prendi appunti sugli insight man mano che li trovi

---

Buon lavoro! ðŸš€