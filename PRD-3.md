# ðŸ“š Lezione 3 â€” Visualizzare e raccontare

## ðŸŽ¯ Cosa imparerai oggi

Alla fine di questa lezione saprai:
- PerchÃ© **visualizzare** i dati non Ã¨ "estetica" ma una necessitÃ  analitica
- Quale **tipo di grafico** usare per quale tipo di dato
- Usare **matplotlib** e **seaborn** per creare grafici professionali
- Usare **Looker Studio** per costruire dashboard senza scrivere codice
- Trasformare i tuoi risultati in una **storia** che convince chi ti ascolta

---

## 1. PerchÃ© visualizzare?

I numeri da soli non parlano. I grafici sÃ¬.

### Il quartetto di Anscombe

Considera questi 4 dataset (Ã¨ un classico della statistica):

- Stessa media di X e Y
- Stessa varianza
- Stessa correlazione
- Stessa retta di regressione

Sembrano identici, vero? **In realtÃ  guardandoli graficamente sono completamente diversi**: uno Ã¨ una nuvola casuale, uno Ã¨ una curva, uno Ã¨ una linea con un outlier, uno Ã¨ una variabile costante con un punto perso.

La lezione Ã¨ chiara: i numeri statistici da soli **non bastano**. Visualizzare Ã¨ parte dell'analisi, non un'aggiunta cosmetica.

### Quando un grafico vince sui numeri

Confronta questi due output:

**Numeri:**
> Le vendite di gennaio sono state 12500, febbraio 13200, marzo 15800, aprile 9800, maggio 11200, giugno 14800, luglio 19200, agosto 21500, settembre 16700, ottobre 13900, novembre 14200, dicembre 22800.

**Grafico:** una linea che mostra in un secondo il picco estivo, la flessione di aprile e l'impennata di dicembre.

Quale comunica meglio?

---

## 2. Quale grafico per quale dato

Non tutti i grafici sono uguali. **Il tipo di dato suggerisce il tipo di grafico.**

### Confronti tra categorie â†’ grafico a barre

Quando confronti **quantitÃ  tra categorie discrete** (es. vendite per regione, popolazione per paese, brani per artista).

```python
import seaborn as sns
import matplotlib.pyplot as plt

vendite_per_categoria = df.groupby("categoria")["prezzo"].sum()
sns.barplot(x=vendite_per_categoria.index, y=vendite_per_categoria.values)
plt.title("Vendite totali per categoria")
plt.xlabel("Categoria")
plt.ylabel("Vendite (â‚¬)")
plt.show()
```

### Andamenti nel tempo â†’ grafico a linea

Per **serie temporali** (vendite mensili, temperatura settimanale, prezzo azione giornaliero).

```python
sns.lineplot(data=df, x="data", y="vendite")
plt.title("Vendite nel tempo")
plt.show()
```

### Distribuzione di una variabile continua â†’ istogramma

Per capire **come si distribuiscono i valori** di una variabile (etÃ  degli utenti, prezzi dei prodotti, gol per partita).

```python
sns.histplot(df["etÃ "], bins=20)
plt.title("Distribuzione delle etÃ ")
plt.show()
```

### Relazione tra due variabili numeriche â†’ scatter plot

Per vedere se due variabili sono **correlate** (es. prezzo vs profitto, BPM vs popolaritÃ , PIL vs felicitÃ ).

```python
sns.scatterplot(data=df, x="prezzo", y="profitto")
plt.title("Prezzo vs Profitto")
plt.show()
```

### Distribuzione + confronto â†’ boxplot

Per **confrontare distribuzioni** tra categorie. In un colpo solo ti mostra mediana, quartili e outlier.

```python
sns.boxplot(data=df, x="categoria", y="prezzo")
plt.title("Distribuzione prezzi per categoria")
plt.show()
```

### Correlazioni multiple â†’ heatmap

Per vedere correlazioni tra **tutte le coppie** di colonne numeriche, tutte insieme.

```python
correlazioni = df[["prezzo", "sconto", "profitto", "quantitÃ "]].corr()
sns.heatmap(correlazioni, annot=True, cmap="coolwarm", center=0)
plt.title("Matrice di correlazione")
plt.show()
```

### Pie chart? Quasi mai.

I grafici a torta sono brutti e quasi sempre sostituibili con un grafico a barre piÃ¹ chiaro. Evitali, o usali al massimo per **2-3 categorie con proporzioni molto diverse**. Gli analisti professionisti li snobbano.

---

## 3. Matplotlib e Seaborn

In Python ci sono due librerie principali per i grafici. Ti diciamo subito quale usare e quando.

### Matplotlib

Libreria storica, molto flessibile, sintassi piÃ¹ verbosa. Ãˆ il "motore" sotto a quasi tutte le altre librerie di grafici.

```python
import matplotlib.pyplot as plt

plt.plot(x, y)
plt.title("Titolo")
plt.xlabel("X")
plt.ylabel("Y")
plt.show()
```

### Seaborn

Libreria costruita **sopra** matplotlib. Sintassi piÃ¹ semplice, grafici di default piÃ¹ belli, integrata nativamente con pandas.

```python
import seaborn as sns
sns.barplot(data=df, x="categoria", y="vendite")
```

### Quale usare?

**Regola pratica**: usa **seaborn** per il 90% dei casi. Cadi su matplotlib quando hai bisogno di personalizzazioni avanzate o di funzioni che seaborn non ha.

Spesso si usano insieme: seaborn per il grafico, matplotlib per titolo, etichette e dimensioni.

```python
plt.figure(figsize=(12, 6))                            # dimensione (matplotlib)
sns.barplot(data=df, x="categoria", y="vendite")       # grafico (seaborn)
plt.title("Vendite per categoria", fontsize=16)        # titolo (matplotlib)
plt.xticks(rotation=45)                                # ruota etichette x
plt.tight_layout()                                     # margini automatici
plt.show()
```

### Personalizzazioni importanti

**Dimensioni del grafico:**
```python
plt.figure(figsize=(12, 6))  # larghezza, altezza in pollici
```

**Titoli ed etichette:**
```python
plt.title("Titolo del grafico")
plt.xlabel("Etichetta asse X")
plt.ylabel("Etichetta asse Y")
```

**Colori e palette:**
```python
sns.barplot(data=df, x="categoria", y="vendite", palette="viridis")
```

**Ruotare le etichette dell'asse X** (utile per nomi lunghi):
```python
plt.xticks(rotation=45)
```

**Salvare un grafico in un file:**
```python
plt.savefig("grafico.png", dpi=300, bbox_inches="tight")
```

### Subplots â€” piÃ¹ grafici in un'unica figura

```python
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

sns.histplot(df["etÃ "], ax=axes[0])
axes[0].set_title("Distribuzione etÃ ")

sns.boxplot(data=df, x="categoria", y="prezzo", ax=axes[1])
axes[1].set_title("Prezzi per categoria")

plt.tight_layout()
plt.show()
```

---

## 4. Looker Studio: dashboard senza codice

Tutto bello, ma a volte serve qualcosa di **diverso**: una dashboard interattiva che un manager o un cliente possa consultare senza aprire un notebook.

Qui entra **Looker Studio** (ex Google Data Studio), strumento gratuito di Google per creare dashboard.

### PerchÃ© esiste

Il notebook Ã¨ perfetto per **analizzare**. Ãˆ pessimo come **deliverable per non-tecnici**: nessuno fuori dal team data apre un file `.ipynb`.

Looker Studio risolve questo problema: colleghi una fonte dati (Google Sheets, CSV, database, ...), trascini i campi sui grafici, condividi un link. Chi lo riceve vede una pagina web pulita, interattiva, sempre aggiornata.

### Quando preferirlo al codice

| Usa Python (matplotlib/seaborn) quando... | Usa Looker Studio quando... |
|---|---|
| Esplori e analizzi (uso privato) | Mostri risultati a non-tecnici |
| Hai bisogno di trasformazioni complesse | I dati sono giÃ  puliti |
| Stai facendo un report una tantum | Vuoi una vista **live e interattiva** |
| Hai grafici molto custom | Bastano grafici standard |

### Workflow tipico

1. **Prepara i dati** in pandas e esportali (`df.to_csv("dati.csv")` o caricali in Google Sheets)
2. **Vai su** [lookerstudio.google.com](https://lookerstudio.google.com) e clicca "Crea â†’ Rapporto"
3. **Collega la fonte dati** (Google Sheets, file caricato, BigQuery, ecc.)
4. **Trascina i campi** sui grafici (scegliendo il tipo)
5. **Personalizza** colori, layout, filtri
6. **Condividi** il link (controllo permessi come su Drive)

> ðŸ’¡ In laboratorio oggi proveremo a costruire una dashboard di esempio. La cosa importante da capire: **stessi concetti** (groupby, filtri, aggregazioni) di pandas, ma con un'interfaccia **drag-and-drop** invece di codice.

---

## 5. Storytelling con i dati

L'ultimo passaggio. Non basta avere grafici belli: serve **raccontare una storia**.

### Avere una tesi

Ogni report dovrebbe rispondere a **una domanda principale** con una **risposta chiara**. Non "ecco i dati", ma "i dati ci dicono che X, e dovremmo fare Y".

### Scegliere gli insight giusti

Hai fatto 20 analisi nel notebook. Quante ne mostri in presentazione? **2 o 3**. Quelle piÃ¹ sorprendenti, piÃ¹ utili, piÃ¹ azionabili.

**Esempio**: nel progetto Spotify potresti aver scoperto 10 cose, ma per la presentazione scegli solo: *"i brani che sfondano nel 2023 hanno tutti un BPM tra 100 e 130"*. Quello Ã¨ il messaggio.

### La sequenza dei grafici

Un buon report ha un **ordine narrativo**:
1. **Contesto** â€” di cosa stiamo parlando? (1 grafico riassuntivo)
2. **Scoperta** â€” cosa ho trovato di nuovo o sorprendente? (2-3 grafici)
3. **Implicazione** â€” cosa significa? Cosa dovremmo fare adesso?

### Errori comuni da evitare

âŒ **Chart junk** â€” decorazioni inutili, 3D, gradienti, sfondi colorati: distraggono dai dati. *Less is more.*

âŒ **Asse Y troncato** per esagerare differenze: ingannevole, perdi credibilitÃ  con chi se ne accorge.

âŒ **Troppi colori** â€” usa massimo 5-6 colori, di solito gradazioni di pochi.

âŒ **Mancanza di titoli o etichette** â€” un grafico senza titolo Ã¨ quasi inutile.

âŒ **Mostrare il processo invece dei risultati** â€” al pubblico non interessa che hai fatto un `.merge()`. Interessa cosa hai **scoperto**.

### Esempio: 2 modi di dire la stessa cosa

âŒ *"Ho raggruppato il dataset per categoria con groupby, sommato i profitti, ordinato in modo decrescente e ho ottenuto questi numeri..."*

âœ… *"Tre sotto-categorie di Superstore sono in perdita. Insieme rappresentano il 6% delle vendite ma il -120% del profitto totale."*

Quale fa pensare al manager *"interessante!"*?

---

## ðŸŽ¯ Recap

- I **grafici** sono parte essenziale dell'analisi, non un'aggiunta estetica
- Tipo di dato â†’ tipo di grafico: **barre** (categorie), **linea** (tempo), **scatter** (relazione), **istogramma** (distribuzione), **boxplot** (confronto distribuzioni), **heatmap** (correlazioni)
- Usa **seaborn** come default, **matplotlib** per personalizzazioni avanzate
- Ogni grafico deve avere **titolo**, **etichette degli assi** e **dimensioni adeguate**
- **Looker Studio** Ã¨ la scelta per dashboard interattive destinate a non-tecnici
- Lo **storytelling** Ã¨ quello che trasforma un'analisi tecnica in una decisione: avere una tesi, scegliere pochi insight, raccontarli con ordine

Buon lavoro per il progetto finale! ðŸŽ¯ðŸ“Š