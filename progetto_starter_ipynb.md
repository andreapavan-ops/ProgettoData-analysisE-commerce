{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "e6280805",
   "metadata": {},
   "source": [
    "# 📊 Progetto Trasversale — Data Analysis\n",
    "\n",
    "**Nome e cognome**: _[scrivi qui]_  \n",
    "**Dataset scelto**: _[Superstore / Spotify / Netflix / World Happiness / International Football]_  \n",
    "**Link Kaggle**: _[incolla qui]_  \n",
    "**Perché ho scelto questo dataset**: _[1-2 righe]_\n",
    "\n",
    "---\n",
    "\n",
    "### 📋 Le 5 domande di ricerca\n",
    "\n",
    "Incolla qui le 5 domande del tuo dataset (le trovi nel brief del progetto).\n",
    "\n",
    "1. **Q1** — _[copia qui]_\n",
    "2. **Q2** — _[copia qui]_\n",
    "3. **Q3** — _[copia qui]_\n",
    "4. **Q4** — _[copia qui]_\n",
    "5. **Q5** — _[copia qui]_\n",
    "\n",
    "**Bonus (opzionale):** _[copia qui]_\n",
    "\n",
    "---\n",
    "\n",
    "> 💡 **Come usare questo notebook**: scorri dall'alto al basso, leggi i commenti nelle celle, compila le parti `[scrivi qui]` e scrivi il codice nelle celle vuote. Le sezioni sono già nell'ordine giusto per il deliverable finale."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c9613f42",
   "metadata": {},
   "source": [
    "## ⚙️ Setup\n",
    "\n",
    "Eseguendo la cella sotto importi tutte le librerie che servono per il progetto."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "7018b3e7",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Librerie standard per data analysis\n",
    "import pandas as pd\n",
    "import numpy as np\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "\n",
    "# Stile dei grafici (rende i plot più puliti automaticamente)\n",
    "sns.set_style(\"whitegrid\")\n",
    "plt.rcParams[\"figure.figsize\"] = (10, 5)\n",
    "plt.rcParams[\"font.size\"] = 11\n",
    "\n",
    "print(\"Setup completato ✓\")"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "015ebc11",
   "metadata": {},
   "source": [
    "## 📥 Caricamento del dataset\n",
    "\n",
    "Hai **tre modi** di caricare il file, a seconda di dove stai lavorando. Decommenta l'opzione che fa al caso tuo (eliminando i `#` davanti alle righe), poi esegui la cella.\n",
    "\n",
    "> ⚠️ **Se hai scelto World Happiness Report**: il dataset ha un CSV per ogni anno. Dovrai caricarli tutti e unirli con `pd.concat([...])`. Trovi un esempio in fondo alla cella."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "cab18c6c",
   "metadata": {},
   "outputs": [],
   "source": [
    "# === OPZIONE A — Jupyter LOCALE ===\n",
    "# Metti il file CSV nella stessa cartella di questo notebook\n",
    "# df = pd.read_csv(\"nome_del_file.csv\")\n",
    "\n",
    "\n",
    "# === OPZIONE B — Google Colab con upload manuale ===\n",
    "# Il file va caricato a ogni nuova sessione\n",
    "# from google.colab import files\n",
    "# uploaded = files.upload()  # apre il selettore di file\n",
    "# df = pd.read_csv(\"nome_del_file.csv\")\n",
    "\n",
    "\n",
    "# === OPZIONE C — Google Colab con Google Drive (consigliato) ===\n",
    "# Carica una volta il file su Drive e poi rileggilo da lì in ogni sessione\n",
    "# from google.colab import drive\n",
    "# drive.mount('/content/drive')\n",
    "# df = pd.read_csv('/content/drive/MyDrive/data-analysis/nome_del_file.csv')\n",
    "\n",
    "\n",
    "# === ESEMPIO per World Happiness (più file da unire) ===\n",
    "# anni = [2018, 2019, 2020, 2021, 2022]\n",
    "# lista_df = []\n",
    "# for anno in anni:\n",
    "#     df_anno = pd.read_csv(f\"{anno}.csv\")\n",
    "#     df_anno['anno'] = anno   # aggiungi una colonna per sapere a che anno appartiene la riga\n",
    "#     lista_df.append(df_anno)\n",
    "# df = pd.concat(lista_df, ignore_index=True)\n",
    "\n",
    "\n",
    "# ---- LASCIA SOLO LA TUA OPZIONE ATTIVA ----\n",
    "df = None   # <-- sostituisci con il read_csv giusto\n",
    "\n",
    "# Verifica veloce che il caricamento sia andato bene\n",
    "if df is not None:\n",
    "    print(f\"Dataset caricato: {df.shape[0]} righe × {df.shape[1]} colonne\")\n",
    "    print(f\"Colonne: {list(df.columns)}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "913d9dee",
   "metadata": {},
   "source": [
    "## 🔍 Q1 — Esplorazione iniziale del dataset\n",
    "\n",
    "> **Domanda Q1 del tuo dataset:** _[incolla qui il testo esatto della domanda]_\n",
    "\n",
    "Esegui le celle sotto per capire cosa c'è dentro il tuo dataset."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "d0a00b20",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Le prime 5 righe per vedere come sono fatti i dati\n",
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "22620e93",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Numero di righe e colonne, tipi di dato, valori non nulli\n",
    "df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "da6a22d4",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Statistiche descrittive sulle colonne numeriche\n",
    "df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "d89e99d3",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Quante righe e quante colonne in totale\n",
    "print(f\"Righe: {df.shape[0]}\")\n",
    "print(f\"Colonne: {df.shape[1]}\")\n",
    "\n",
    "# Eventuali altri conteggi utili per la Q1 (es. quanti valori unici in una colonna)\n",
    "# print(df['colonna'].nunique())"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2b6d1777",
   "metadata": {},
   "source": [
    "**📝 Osservazioni iniziali (risposta alla Q1):**\n",
    "\n",
    "_Scrivi qui in 3-5 righe cosa hai notato. Esempi: quante righe e colonne, che tipo di colonne ci sono, ci sono valori mancanti evidenti?, su che periodo temporale si estendono i dati (se applicabile), quante categorie / paesi / artisti diversi ci sono, ecc._"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e3be4d40",
   "metadata": {},
   "source": [
    "## 🧹 Pulizia del dataset\n",
    "\n",
    "Prima di analizzare seriamente, sistemiamo il dataset. Per ogni operazione di pulizia che fai, **spiega in testo cosa hai deciso e perché**."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "1a19f160",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Quanti valori mancanti ci sono per ogni colonna?\n",
    "df.isna().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "fe648abe",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Eventuali duplicati\n",
    "duplicati = df.duplicated().sum()\n",
    "print(f\"Righe duplicate: {duplicati}\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "174ef6bc",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Applica qui le pulizie che servono al TUO dataset.\n",
    "# Esempi (decommenta e adatta):\n",
    "\n",
    "# Conversione di una colonna in formato data\n",
    "# df['data'] = pd.to_datetime(df['data'])\n",
    "\n",
    "# Rimuovere righe duplicate\n",
    "# df = df.drop_duplicates()\n",
    "\n",
    "# Riempire i NaN con un valore di default\n",
    "# df['categoria'] = df['categoria'].fillna('Sconosciuta')\n",
    "\n",
    "# Eliminare righe con NaN in una colonna fondamentale\n",
    "# df = df.dropna(subset=['colonna_essenziale'])\n",
    "\n",
    "# Convertire un numero salvato come testo\n",
    "# df['prezzo'] = pd.to_numeric(df['prezzo'], errors='coerce')\n",
    "\n",
    "# Verifica dopo la pulizia\n",
    "print(f\"Righe dopo la pulizia: {df.shape[0]}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "55be55d9",
   "metadata": {},
   "source": [
    "**📝 Pulizie effettuate (giustifica le scelte):**\n",
    "\n",
    "_Elenca cosa hai pulito e perché. Esempi:_\n",
    "- _Convertita la colonna `date_added` in `datetime` perché era una stringa_\n",
    "- _Rimossi 23 duplicati esatti_\n",
    "- _Mantenuti i NaN su `director` perché informativi: significa che il regista non è registrato_\n",
    "- _Riempiti i NaN su `country` con `'Unknown'` per non perdere ~800 righe_"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "266e404b",
   "metadata": {},
   "source": [
    "## 📊 Q2 — Aggregazione\n",
    "\n",
    "> **Domanda Q2 del tuo dataset:** _[incolla qui il testo esatto della domanda]_\n",
    "\n",
    "💡 *Suggerimento: per questa domanda di solito serve `groupby` seguito da `.sum()`, `.mean()`, `.count()` o `.agg()`.*"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "97d83074",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Il tuo codice per rispondere alla Q2\n",
    "# Esempio generico (adattalo):\n",
    "# df.groupby('colonna_da_raggruppare')['colonna_da_calcolare'].sum().sort_values(ascending=False)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "cea5292d",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Grafico che supporta la risposta alla Q2\n",
    "# Esempio: un grafico a barre con seaborn\n",
    "# sns.barplot(data=..., x='colonna_x', y='colonna_y')\n",
    "# plt.title(\"Titolo del grafico\")\n",
    "# plt.xlabel(\"Etichetta X\")\n",
    "# plt.ylabel(\"Etichetta Y\")\n",
    "# plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f5218e82",
   "metadata": {},
   "source": [
    "**💡 Risposta alla Q2:**\n",
    "\n",
    "_Scrivi qui in 2-4 righe la risposta, riferendoti ai numeri e/o al grafico sopra._"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a3772121",
   "metadata": {},
   "source": [
    "## 📈 Q3 — Analisi temporale\n",
    "\n",
    "> **Domanda Q3 del tuo dataset:** _[incolla qui il testo esatto della domanda]_\n",
    "\n",
    "💡 *Suggerimento: se hai una colonna data, puoi estrarre anno o mese con `df['data'].dt.year` e `df['data'].dt.month`, poi raggruppare.*"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "631c4aaa",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Il tuo codice per rispondere alla Q3\n",
    "# Esempio: estrazione dell'anno + groupby\n",
    "# df['anno'] = df['data'].dt.year\n",
    "# df.groupby('anno')['valore'].sum()\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "590a401d",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Grafico che supporta la risposta alla Q3 (per le serie temporali, di solito un grafico a linea)\n",
    "# sns.lineplot(data=..., x='anno', y='valore')\n",
    "# plt.title(\"Titolo\")\n",
    "# plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3cf471f6",
   "metadata": {},
   "source": [
    "**💡 Risposta alla Q3:**\n",
    "\n",
    "_Scrivi qui la risposta._"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "867b65a8",
   "metadata": {},
   "source": [
    "## 🔀 Q4 — Confronto tra segmenti/categorie\n",
    "\n",
    "> **Domanda Q4 del tuo dataset:** _[incolla qui il testo esatto della domanda]_\n",
    "\n",
    "💡 *Suggerimento: anche qui di solito serve `groupby`, oppure filtri (`df[df['colonna'] == valore]`) per confrontare sotto-insiemi.*"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "9db9c053",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Il tuo codice per rispondere alla Q4\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "5ee95790",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Grafico che supporta la risposta alla Q4\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "eac39f84",
   "metadata": {},
   "source": [
    "**💡 Risposta alla Q4:**\n",
    "\n",
    "_Scrivi qui la risposta._"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1e099420",
   "metadata": {},
   "source": [
    "## 🤔 Q5 — Domanda critica/aperta\n",
    "\n",
    "> **Domanda Q5 del tuo dataset:** _[incolla qui il testo esatto della domanda]_\n",
    "\n",
    "💡 *Questa è la domanda più \"aperta\": non basta calcolare un numero, devi **interpretare** i dati e formulare una conclusione. Possono servire correlazioni (`df.corr()`), filtri condizionali, o confronti tra gruppi.*"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "1311dd04",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Il tuo codice per rispondere alla Q5\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "c88d9973",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Grafico che supporta la risposta alla Q5\n",
    "# Per le correlazioni, sns.scatterplot o sns.heatmap sono molto utili\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c10baa0b",
   "metadata": {},
   "source": [
    "**💡 Risposta alla Q5:**\n",
    "\n",
    "_Scrivi qui la tua interpretazione, non solo il numero. Questa è la domanda dove dimostri di saper \"leggere\" i dati._\n",
    "\n",
    "> ⚠️ **Attenzione**: correlazione non significa causalità. Se A è correlato a B, non vuol dire automaticamente che A causa B."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b2473ea3",
   "metadata": {},
   "source": [
    "## 🎯 Conclusioni e insight chiave\n",
    "\n",
    "_Scrivi 2-3 paragrafi che riassumono cosa hai scoperto analizzando questo dataset._\n",
    "\n",
    "_Cosa ti ha **sorpreso**? Cosa **non ti aspettavi**? Quali sono le scoperte che presenterai ai compagni alla fine del Giorno 3? Annotale qui: saranno la base della tua presentazione finale._\n",
    "\n",
    "---\n",
    "\n",
    "**🥇 Insight 1:** _Il più sorprendente. Spiegalo in 2-3 righe._\n",
    "\n",
    "**🥈 Insight 2:** _Il secondo più interessante._\n",
    "\n",
    "**🥉 Insight 3:** _Il terzo (opzionale ma consigliato per la presentazione)._\n",
    "\n",
    "---\n",
    "\n",
    "**Grafico \"killer\" da mostrare nella presentazione:** _segnati qui qual è il grafico migliore del notebook (es. \"il grafico della Q3 sulle vendite mensili\"), così lo trovi subito al momento della presentazione._"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "8100aaba",
   "metadata": {},
   "source": [
    "## 🏆 Bonus (opzionale)\n",
    "\n",
    "> **Domanda bonus del tuo dataset:** _[incolla qui]_\n",
    "\n",
    "_Questa parte è opzionale: falla se finisci in anticipo o vuoi spingerti oltre._"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "61158597",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Codice della domanda bonus\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "3925823e",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Grafico del bonus\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d2a9b45f",
   "metadata": {},
   "source": [
    "**💡 Risposta al bonus:**\n",
    "\n",
    "_..._\n",
    "\n",
    "---\n",
    "\n",
    "🎉 **Fine del progetto!** Prima di consegnare, controlla che:\n",
    "- ☐ Nome e cognome compilati in cima al notebook\n",
    "- ☐ Tutte le 5 domande hanno una risposta in testo (non solo codice)\n",
    "- ☐ Ogni grafico ha titolo ed etichette sugli assi\n",
    "- ☐ Il notebook si esegue dall'inizio alla fine senza errori (`Kernel → Restart & Run All` su Jupyter, oppure `Runtime → Esegui tutto` su Colab)\n",
    "- ☐ Hai scelto i 2-3 insight per la presentazione finale"
   ]
  }
 ],
 "metadata": {},
 "nbformat": 4,
 "nbformat_minor": 5
}