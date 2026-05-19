# ðŸ“š Lezione 2 â€” Trasformare i dati

## ðŸŽ¯ Cosa imparerai oggi

Alla fine di questa lezione saprai:
- Come **pulire** un dataset (missing values, duplicati, tipi sbagliati)
- Come creare **colonne derivate** dai dati esistenti
- Come usare `groupby`, lo strumento piÃ¹ potente di pandas
- Come **unire** piÃ¹ DataFrame con `merge` e `concat`

---

## 1. Pulire i dati

Ricordi quanto detto ieri? Un data analyst passa il 70-80% del tempo a pulire i dati. Ecco perchÃ©.

### I dati reali sono sporchi

Nel mondo reale, i dataset arrivano con:
- **Valori mancanti** (NaN)
- **Duplicati**
- **Tipi di dato sbagliati** (numeri salvati come stringhe, date come testo)
- **Inconsistenze** â€” "Roma", "roma", "ROMA", " Roma " sono "valori diversi" per il computer
- **Outlier strani** â€” errori di battitura, sensori rotti, casi limite

Sistemarli prima di analizzare Ã¨ cruciale: dati sporchi â†’ conclusioni sbagliate.

### Missing values

In pandas i valori mancanti sono rappresentati da `NaN` (Not a Number). Li vedi sempre in:
- Celle vuote del CSV
- Valori come "N/D", "?", "-", "null" (se gestiti con `na_values=` durante il `read_csv`)

**Trovarli:**

```python
df.isna()                     # un DataFrame di True/False
df.isna().sum()               # conta i NaN per colonna
df.isna().any(axis=1).sum()   # quante righe hanno almeno un NaN
```

**Gestirli:** hai 3 strategie.

#### Strategia 1: rimuovere

```python
df.dropna()                       # elimina righe con almeno un NaN
df.dropna(subset=["prezzo"])      # solo se manca il prezzo (colonna chiave)
df.dropna(axis=1)                 # elimina colonne con NaN (raramente saggio)
```

**Quando**: i missing sono pochi e la riga senza quel dato Ã¨ inutile.

#### Strategia 2: riempire con un valore

```python
df["categoria"] = df["categoria"].fillna("Sconosciuta")
df["prezzo"] = df["prezzo"].fillna(0)
df["prezzo"] = df["prezzo"].fillna(df["prezzo"].mean())     # con la media
df["prezzo"] = df["prezzo"].fillna(df["prezzo"].median())   # con la mediana
```

**Quando**: i missing hanno un significato implicito, o vuoi mantenere la riga.

#### Strategia 3: lasciarli come sono

A volte i NaN sono **informativi**: dicono "questo dato non esiste". Esempio: nel dataset Netflix la colonna `director` Ã¨ spesso NaN per le serie TV (non ha senso "il regista" di una serie intera). Tenerli come NaN Ã¨ la scelta giusta.

> ðŸ§  **Importante**: per ogni operazione di pulizia, **giustifica la tua scelta nel notebook**. Non basta pulire, devi spiegare il "perchÃ©".

### Duplicati

```python
df.duplicated()                       # True per ogni riga duplicata
df.duplicated().sum()                 # quanti duplicati
df = df.drop_duplicates()             # rimuovi duplicati esatti
df = df.drop_duplicates(subset=["email"])  # rimuovi righe con stessa email
```

### Tipi sbagliati

Capita spesso che pandas legga male i tipi (perchÃ© il CSV non li specifica). I problemi tipici:

**Date salvate come stringhe:**

```python
df["data"] = pd.to_datetime(df["data"])
# Adesso puoi fare df["data"].dt.year, dt.month, dt.day_name(), ...
```

**Numeri salvati come stringhe** (capita se ci sono virgolette, "â‚¬" o spazi):

```python
df["prezzo"] = pd.to_numeric(df["prezzo"], errors="coerce")
# errors="coerce" â†’ i valori non convertibili diventano NaN (poi li gestisci)
```

**Cast forzato:**

```python
df["etÃ "] = df["etÃ "].astype(int)
df["voto"] = df["voto"].astype(float)
```

### Inconsistenze testuali

```python
df["cittÃ "] = df["cittÃ "].str.strip()    # rimuove spazi prima/dopo
df["cittÃ "] = df["cittÃ "].str.lower()    # tutto minuscolo
df["cittÃ "] = df["cittÃ "].str.title()    # Prima Lettera Maiuscola
```

---

## 2. Filtri e query avanzati

Ieri abbiamo visto i filtri booleani. Ne aggiungiamo qualcuno piÃ¹ sofisticato.

### `.query()` â€” sintassi piÃ¹ leggibile

```python
# Modo classico:
df[(df["categoria"] == "Elettronica") & (df["prezzo"] > 500)]

# Con query (piÃ¹ leggibile):
df.query("categoria == 'Elettronica' and prezzo > 500")
```

### `.isin()` â€” appartenenza a una lista

```python
df[df["cittÃ "].isin(["Roma", "Milano", "Napoli"])]
```

### `.str.contains()` â€” contiene una stringa

```python
df[df["titolo"].str.contains("Italia", na=False)]
```

> ðŸ§  Il `na=False` Ã¨ importante: dice "se Ã¨ NaN, considera come non-match" (altrimenti la funzione genera errore sui NaN).

### `.between()` â€” intervallo

```python
df[df["prezzo"].between(100, 500)]
```

---

## 3. Creare colonne derivate

Spesso la risposta a una domanda non Ã¨ in una colonna esistente, ma deriva dalla combinazione di altre.

### Calcoli vettoriali

```python
df["totale"] = df["prezzo"] * df["quantitÃ "]
df["sconto_percentuale"] = (df["prezzo_listino"] - df["prezzo_finale"]) / df["prezzo_listino"] * 100
```

Pandas applica le operazioni a tutta la colonna automaticamente. **Niente for loop**. Ãˆ sia piÃ¹ elegante che molto piÃ¹ veloce.

### Estrarre componenti da una data

```python
df["data"] = pd.to_datetime(df["data"])
df["anno"] = df["data"].dt.year
df["mese"] = df["data"].dt.month
df["giorno_settimana"] = df["data"].dt.day_name()
df["trimestre"] = df["data"].dt.quarter
```

### Operazioni su stringhe

```python
df["lunghezza_nome"] = df["nome"].str.len()
df["paese_maiuscolo"] = df["paese"].str.upper()
df["prima_parola"] = df["titolo"].str.split().str[0]
```

### Categorizzazione con `pd.cut`

```python
df["fascia_etÃ "] = pd.cut(
    df["etÃ "],
    bins=[0, 18, 35, 65, 100],
    labels=["Minorenne", "Giovane", "Adulto", "Senior"]
)
```

### `apply` per funzioni custom

Quando l'operazione Ã¨ complessa e non basta una formula:

```python
def categorizza_prezzo(p):
    if p < 50:
        return "Economico"
    elif p < 200:
        return "Medio"
    else:
        return "Premium"

df["fascia"] = df["prezzo"].apply(categorizza_prezzo)
```

> ðŸ§  `apply` Ã¨ flessibile ma **lento** rispetto alle operazioni vettoriali. Usalo solo quando proprio non puoi fare di meglio.

---

## 4. groupby â€” il cuore dell'analisi

`groupby` Ã¨ la singola funzione piÃ¹ importante di pandas per l'analisi.

### Cosa fa concettualmente

Il pattern Ã¨ **Split-Apply-Combine**:
1. **Split** â€” dividi il DataFrame in gruppi (es. uno per categoria)
2. **Apply** â€” applica una funzione a ciascun gruppo (es. somma, media)
3. **Combine** â€” rimetti insieme i risultati

### Esempio base

```python
# Vendite totali per categoria
df.groupby("categoria")["prezzo"].sum()
```

Output:
```
categoria
Accessori       1450.50
Elettronica    25690.00
Mobili         12300.00
```

### Aggregazioni comuni

```python
df.groupby("categoria")["prezzo"].mean()    # media per gruppo
df.groupby("categoria")["prezzo"].count()   # conteggio per gruppo
df.groupby("categoria")["prezzo"].max()     # massimo per gruppo
df.groupby("categoria").size()              # conteggio righe per gruppo
```

### PiÃ¹ aggregazioni insieme: `.agg()`

```python
df.groupby("categoria")["prezzo"].agg(["sum", "mean", "count"])
```

Output:
```
              sum     mean  count
categoria                        
Accessori    1450    15.79     92
Elettronica  25690   485.66    53
```

### Aggregazioni diverse su colonne diverse

```python
df.groupby("categoria").agg(
    vendite_totali=("prezzo", "sum"),
    quantita_media=("quantitÃ ", "mean"),
    numero_ordini=("id", "count")
)
```

### Groupby su piÃ¹ colonne

```python
df.groupby(["categoria", "cittÃ "])["prezzo"].sum()
```

### Resettare l'indice

Dopo groupby l'output ha le chiavi come **indice**. Se vuoi un DataFrame "piatto":

```python
risultato = df.groupby("categoria")["prezzo"].sum().reset_index()
```

### Analogia con SQL

GiÃ  conosci SQL, quindi:

```sql
SELECT categoria, SUM(prezzo)
FROM vendite
GROUP BY categoria
```

In pandas Ã¨ esattamente:

```python
df.groupby("categoria")["prezzo"].sum()
```

> ðŸ§  Il `GROUP BY` di SQL e il `groupby` di pandas fanno **la stessa cosa**, con sintassi diversa. Se sei a tuo agio con il primo, sei giÃ  a metÃ  strada con il secondo.

---

## 5. Unire piÃ¹ DataFrame: `merge` e `concat`

A volte i dati sono divisi su piÃ¹ file o tabelle e devi unirli prima di analizzarli.

### `concat` â€” impilare DataFrame con stessa struttura

Usalo quando hai piÃ¹ file con le stesse colonne (esempio classico: un CSV per ogni anno).

```python
df_2022 = pd.read_csv("vendite_2022.csv")
df_2023 = pd.read_csv("vendite_2023.csv")
df_2024 = pd.read_csv("vendite_2024.csv")

df_completo = pd.concat([df_2022, df_2023, df_2024], ignore_index=True)
```

`ignore_index=True` rinumera l'indice da 0 (altrimenti rimangono gli indici originali, con duplicati).

> ðŸ’¡ Se ti serve sapere da quale file viene ogni riga, aggiungi una colonna prima del concat:
> ```python
> df_2022["anno"] = 2022
> df_2023["anno"] = 2023
> ```

### `merge` â€” unire come fai con i JOIN SQL

Usalo quando hai DataFrame con **strutture diverse** che condividono una chiave (esempio: tabella ordini e tabella clienti che condividono `cliente_id`).

```python
df_completo = pd.merge(ordini, clienti, on="cliente_id")
```

I tipi di join sono i soliti di SQL:

```python
pd.merge(a, b, on="id", how="inner")  # solo righe presenti in entrambi (default)
pd.merge(a, b, on="id", how="left")   # tutte le righe di a, solo i match di b
pd.merge(a, b, on="id", how="right")  # tutte le righe di b
pd.merge(a, b, on="id", how="outer")  # tutte le righe di entrambi
```

Se le chiavi si chiamano diversamente:

```python
pd.merge(ordini, clienti, left_on="cliente_id", right_on="id")
```

> ðŸ§  Ãˆ identico ai JOIN SQL: stessa logica, sintassi diversa.

---

## ðŸŽ¯ Recap

- **Pulire** i dati prima di analizzarli Ã¨ non-negoziabile: missing (`isna`, `fillna`, `dropna`), duplicati (`drop_duplicates`), tipi (`to_datetime`, `to_numeric`)
- **Filtri avanzati**: `.query()`, `.isin()`, `.str.contains()`, `.between()`
- **Colonne derivate** con operazioni vettoriali (veloci) o `.apply()` (flessibile ma lento)
- **groupby** Ã¨ il cuore di pandas: **Split-Apply-Combine**. Stessa logica del `GROUP BY` in SQL.
- **`merge`** = JOIN tra DataFrame con strutture diverse
- **`concat`** = impilare DataFrame con stessa struttura

Domani arriva la parte piÃ¹ creativa: i grafici. ðŸŽ¨