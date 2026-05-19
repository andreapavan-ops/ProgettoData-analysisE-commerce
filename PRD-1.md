# ðŸ“š Lezione 1 â€” Esplorare i dati con pandas

## ðŸŽ¯ Cosa imparerai oggi

Alla fine di questa lezione saprai:
- Cos'Ã¨ il **data analysis** e dove si inserisce nel mondo del lavoro reale
- Da dove vengono i dati (file, database, API)
- Cos'Ã¨ **pandas** e perchÃ© Ã¨ lo strumento standard per analizzare dati in Python
- Come **caricare** un dataset, vedere cosa contiene e fare le **prime selezioni**

---

## 1. Cos'Ã¨ il data analysis?

Il data analysis Ã¨ il processo di **trasformare numeri grezzi in decisioni informate**.

Pensa a Netflix che ti suggerisce film, a Spotify che ti prepara il Wrapped di fine anno, a un manager che decide su quali prodotti puntare l'anno prossimo, a un comune che decide dove costruire una pista ciclabile: dietro tutte queste decisioni ci sono **dati** analizzati da qualcuno.

### La pipeline tipica

Quasi tutti i progetti di analisi seguono lo stesso schema in 5 fasi:

```
RACCOLTA â†’ PULIZIA â†’ ESPLORAZIONE â†’ VISUALIZZAZIONE â†’ COMUNICAZIONE
```

1. **Raccolta** â€” da dove arrivano i dati? File CSV, database aziendale, API di un servizio web, sensore IoT...
2. **Pulizia** â€” i dati reali sono sporchi. Valori mancanti, date in formato sbagliato, duplicati. Va sistemato tutto.
3. **Esplorazione** â€” prima di analizzare, devi *conoscere* i dati. Quante righe? Quali colonne? Distribuzioni? Outlier?
4. **Visualizzazione** â€” i grafici raccontano una storia che i numeri da soli non riescono a dire.
5. **Comunicazione** â€” il deliverable finale non Ã¨ il grafico, Ã¨ la **decisione** che il destinatario prende grazie al tuo lavoro.

> ðŸ’¡ Le statistiche di settore dicono che un data analyst passa **circa il 70-80% del tempo nelle fasi 1-2** (raccolta e pulizia). Solo il 20-30% nell'analisi vera e propria. SÃ¬, Ã¨ strano. No, non puoi saltarle: dati sporchi = conclusioni sbagliate.

### Data analyst vs Data scientist

Termini spesso confusi. Per semplificare:

| Data Analyst | Data Scientist |
|---|---|
| Risponde a domande sul **passato** e sul **presente** | Costruisce modelli che predicono il **futuro** |
| Strumenti: pandas, SQL, Excel, Looker Studio | Strumenti: pandas, scikit-learn, TensorFlow, ML |
| Risultato: report, dashboard, decisione | Risultato: modello predittivo, sistema di raccomandazione |

In questo corso facciamo **data analysis**. Niente machine learning, niente reti neurali: capiamo cosa Ã¨ successo nei dati, e perchÃ©.

---

## 2. Le fonti di dati

I dati non escono dal nulla. Vengono da qualche parte. Ãˆ importante conoscere le principali fonti perchÃ© in un lavoro reale non ti danno sempre un CSV pulito su WhatsApp.

### File di testo strutturato

**CSV** (Comma Separated Values) â€” il piÃ¹ comune in assoluto. Un file di testo dove ogni riga Ã¨ un record e i campi sono separati da virgole (o punti e virgola).

```csv
data,prodotto,prezzo
2024-01-15,Laptop,899.00
2024-01-15,Mouse,15.50
```

**Excel** (.xlsx) â€” molto usato in azienda. Ha piÃ¹ fogli e formattazione, ma Ã¨ meno "machine-friendly" del CSV.

**JSON** â€” usato da API e applicazioni web. Annidato (nested), perfetto per dati gerarchici.

```json
{
  "ordini": [
    {"data": "2024-01-15", "prodotto": "Laptop", "prezzo": 899.00}
  ]
}
```

### Database

Quando i dati sono troppi per stare in un file, vivono in un **database**. In pandas usi `pd.read_sql()` per interrogare con SQL un database e ricevere direttamente un DataFrame.

```python
import sqlite3
conn = sqlite3.connect("azienda.db")
df = pd.read_sql("SELECT * FROM ordini WHERE anno = 2024", conn)
```

> ðŸ§  Hai giÃ  fatto SQL: ora sai che puoi prendere i risultati di una query e analizzarli in Python. Le due cose si parlano benissimo.

### API esterne

I servizi online (Twitter, Spotify, OpenWeatherMap, ISTAT) espongono **API**: tu fai una richiesta HTTP, loro ti rispondono con JSON. In Python si usa la libreria `requests`.

```python
import requests
risposta = requests.get("https://api.esempio.it/dati")
dati = risposta.json()
df = pd.DataFrame(dati)
```

### Quale fonte scegliere?

Nessuna scelta libera, di solito: usi quella che hai a disposizione. Ma se tocca a te scegliere:

- **CSV** â†’ semplice, portabile, leggibile da umani. Default per piccoli progetti.
- **Excel** â†’ solo se devi consegnare a non-tecnici che lavorano con quello.
- **JSON** â†’ se i dati sono naturalmente annidati o vieni da un'API.
- **Database** â†’ quando i dati sono tanti, condivisi, o servono query complesse.

---

## 3. Pandas: il coltellino svizzero del data analyst

**Pandas** Ã¨ la libreria Python standard per il data analysis. Quasi tutto il lavoro che vedrai in questo corso passa da qui.

### PerchÃ© pandas e non Python "puro"?

Potresti fare tutto con liste e dizionari, ma sarebbe lento e doloroso. Pandas ti dÃ :
- **Strutture dati ottimizzate** (DataFrame, Series)
- **Funzioni di alto livello** giÃ  pronte (read_csv, groupby, merge)
- **Vettorizzazione**: le operazioni sono velocissime (lavora in C dietro le quinte)

### Series e DataFrame

Le due strutture fondamentali di pandas:

**Series** = una colonna. Una sequenza di valori con un indice.

```python
import pandas as pd

prezzi = pd.Series([899, 15.50, 1200, 35])
print(prezzi)
# 0     899.00
# 1      15.50
# 2    1200.00
# 3      35.00
```

**DataFrame** = una tabella. PiÃ¹ Series messe insieme, con righe e colonne.

```python
df = pd.DataFrame({
    "prodotto": ["Laptop", "Mouse", "Monitor", "Tastiera"],
    "prezzo": [899, 15.50, 1200, 35],
    "categoria": ["Elettronica", "Accessori", "Elettronica", "Accessori"]
})
```

### Analogie utili

Se stai pensando *"ma Ã¨ come..."*, probabilmente hai ragione:

| pandas | SQL | Excel | Python puro |
|---|---|---|---|
| DataFrame | Tabella | Foglio di calcolo | Lista di dict |
| Series | Colonna | Colonna | Lista |
| Indice | Chiave primaria | Numero di riga | Indice della lista |
| `df['col']` | `SELECT col FROM ...` | Selezione colonna | `lista[i]['col']` |

> ðŸ§  **Importante**: un DataFrame ha un **indice** (a sinistra) e poi le **colonne**. L'indice serve a etichettare le righe. Di default Ã¨ 0, 1, 2, ..., ma puÃ² essere personalizzato (es. usare la data come indice).

---

## 4. Caricare un dataset

In quasi ogni progetto la prima riga di codice "vera" Ã¨ il `read_csv`.

### CSV

```python
df = pd.read_csv("vendite.csv")
```

Parametri utili quando il file ha qualche stranezza:

```python
df = pd.read_csv(
    "vendite.csv",
    sep=";",                 # separatore diverso (italiano: spesso ;)
    encoding="utf-8",        # encoding del file
    na_values=["N/D", "?"],  # valori da considerare come "mancante"
    parse_dates=["data"],    # parsa subito le colonne data
)
```

### Excel

```python
df = pd.read_excel("vendite.xlsx", sheet_name="2024")
```

### JSON

```python
df = pd.read_json("vendite.json")
# Se Ã¨ annidato, si lavora con json_normalize
```

### Database SQLite

```python
import sqlite3
conn = sqlite3.connect("azienda.db")
df = pd.read_sql("SELECT * FROM ordini", conn)
```

### URL diretto

Puoi anche dare un URL al posto del path:

```python
df = pd.read_csv("https://example.com/dati.csv")
```

### Su Google Colab

Se lavori su Colab, il file deve arrivare in qualche modo. Tre opzioni:
1. Caricarlo manualmente con il pannello "File" o `files.upload()`
2. Montare Google Drive e leggere da lÃ¬
3. Usare un URL diretto (se il file Ã¨ online)

---

## 5. Esplorare un DataFrame

Hai caricato i dati. Ora cosa? **Mai analizzare alla cieca**. Prima si **esplora**: si guarda cosa c'Ã¨ dentro.

### Le prime righe

```python
df.head()       # prime 5 righe
df.head(10)     # prime 10
df.tail()       # ultime 5
df.sample(5)    # 5 righe casuali
```

> ðŸ§  `head()` Ã¨ la prima cosa che fa SEMPRE qualunque data analyst dopo aver caricato un dataset. Sempre.

### Forma e struttura

```python
df.shape       # (righe, colonne) â€” es. (10000, 13)
df.columns     # i nomi delle colonne
df.dtypes      # i tipi di dato per colonna
df.info()      # riepilogo completo: tipi, count, memoria usata
```

`df.info()` Ã¨ particolarmente potente: in un colpo solo vedi quante righe ci sono, quante non-null per ogni colonna (=> se ci sono missing!), il tipo di dato e la memoria occupata.

### Statistiche descrittive

```python
df.describe()              # statistiche delle colonne numeriche
df.describe(include="all") # anche le colonne testuali
```

Output di `describe()` per una colonna numerica:
- **count** â€” quanti valori non nulli
- **mean** â€” media
- **std** â€” deviazione standard
- **min** / **max** â€” minimo / massimo
- **25% / 50% / 75%** â€” i tre quartili (50% = mediana)

### Conteggi su colonne categoriche

```python
df["categoria"].value_counts()
# Elettronica    523
# Accessori      311
# Mobili         150
```

Versione percentuale:

```python
df["categoria"].value_counts(normalize=True)
```

### Quanti valori unici?

```python
df["cittÃ "].nunique()    # numero di valori unici
df["cittÃ "].unique()     # i valori unici (array)
```

---

## 6. Selezionare e filtrare

Hai un DataFrame ma raramente ti interessano tutte le righe e tutte le colonne. Devi **selezionare** la fetta giusta.

### Selezionare colonne

```python
df["prodotto"]                # una colonna (Series)
df[["prodotto", "prezzo"]]    # piÃ¹ colonne (DataFrame)
```

### Selezionare righe per posizione: `.iloc`

```python
df.iloc[0]          # prima riga
df.iloc[0:5]        # prime 5 righe
df.iloc[0:5, 0:2]   # prime 5 righe, prime 2 colonne
```

### Selezionare righe per etichetta: `.loc`

```python
df.loc[0, "prodotto"]                # riga 0, colonna "prodotto"
df.loc[0:5, ["prodotto", "prezzo"]]  # righe 0-5, due colonne
```

### Filtri booleani

Qui sta il vero potere di pandas. Crei una "maschera" booleana e selezioni solo le righe dove la condizione Ã¨ vera.

```python
# Solo le righe dove il prezzo Ã¨ > 100
df[df["prezzo"] > 100]

# Solo elettronica
df[df["categoria"] == "Elettronica"]
```

### Filtri multipli

`&` (AND), `|` (OR), `~` (NOT). **Importante**: parentesi obbligatorie attorno a ogni condizione!

```python
# Elettronica E prezzo > 500
df[(df["categoria"] == "Elettronica") & (df["prezzo"] > 500)]

# Elettronica O Accessori
df[df["categoria"].isin(["Elettronica", "Accessori"])]
```

> âš ï¸ **Errore classico**: dimenticare le parentesi nei filtri multipli. `df[df["a"] > 1 & df["b"] < 2]` non funziona â€” Python interpreta male l'ordine degli operatori. Devono essere `(df["a"] > 1) & (df["b"] < 2)`.

---

## 7. Ripasso veloce di statistica

Per "leggere" i numeri che pandas ti restituisce, serve un ripasso veloce dei concetti base.

### Media, mediana, moda

- **Media** (`mean`) â€” somma di tutti i valori diviso il numero di valori. **Sensibile agli outlier**.
- **Mediana** (`median`) â€” il valore "in mezzo" quando ordini tutto. **Robusta agli outlier**.
- **Moda** (`mode`) â€” il valore piÃ¹ frequente. Utile per dati categorici.

**Esempio classico**: stipendi di 5 persone â€” 1500, 1600, 1700, 1800, 50000.
- Media: **11320** (distorta dall'outlier)
- Mediana: **1700** (rappresenta meglio il "tipico")

> ðŸ§  **Regola pratica**: quando una distribuzione Ã¨ asimmetrica (es. stipendi, prezzi, popolazioni di cittÃ ), la **mediana** Ã¨ piÃ¹ rappresentativa della media.

### Deviazione standard

Misura **quanto i valori si discostano** dalla media. Se Ã¨ piccola, i dati sono concentrati attorno alla media; se Ã¨ grande, sono sparsi.

### Quartili e percentili

Dividono i dati ordinati in 4 (quartili) o 100 (percentili) gruppi uguali.
- **1Â° quartile (25%)** â€” sotto questo valore c'Ã¨ il 25% dei dati
- **2Â° quartile (50%)** â€” la mediana, divide a metÃ 
- **3Â° quartile (75%)** â€” sopra questo valore c'Ã¨ il 25% dei dati

Conoscere i quartili ti dÃ  un'idea della **forma della distribuzione** dei dati senza nemmeno guardare un grafico.

### Outlier

Valori "anomali", molto distanti dal resto. Esistono tecniche statistiche per identificarli (regola del 1.5Ã—IQR, z-score). Per ora basti sapere che li **sospetti** quando vedi `max` molto diverso da `75%`, o `min` molto diverso da `25%`.

---

## ðŸŽ¯ Recap

- Il **data analysis** Ã¨ una pipeline: **raccolta â†’ pulizia â†’ esplorazione â†’ visualizzazione â†’ comunicazione**
- I dati arrivano da fonti diverse: **file** (CSV/Excel/JSON), **database** (SQL), **API**
- **pandas** Ã¨ la libreria standard per analizzare dati in Python. Le sue strutture chiave sono **Series** (colonna) e **DataFrame** (tabella)
- Le prime operazioni dopo aver caricato un dataset sono SEMPRE le stesse: `head()`, `info()`, `describe()`, `shape`
- Si seleziona con `[]`, `.loc[]`, `.iloc[]` e **filtri booleani**
- Per leggere i numeri serve un minimo di **statistica**: media (sensibile a outlier), mediana (robusta), quartili (forma della distribuzione)

## ðŸ› ï¸ Cosa serve avere installato

- **Su Google Colab** â€” nulla, tutto giÃ  pronto
- **Su Jupyter locale** â€” `pip install pandas numpy matplotlib seaborn jupyter`

Pronti per il laboratorio? ðŸš€