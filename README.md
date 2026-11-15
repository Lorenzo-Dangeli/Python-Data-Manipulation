# 📊 Analisi della spesa pubblica in istruzione e crescita del PIL

Un'indagine approfondita basata sui dati storici della **Banca Mondiale**, finalizzata a verificare se e come gli investimenti pubblici in istruzione (% del PIL) si traducano in crescita economica, esplorando dinamiche di lungo periodo, eterogeneità per fasce di reddito, volatilità della spesa e modelli econometrici a effetti fissi (*Panel Data*).

---

## 🎯 Obiettivi del progetto
* **Pulizia e preparazione dei dati:** Gestione di dataset macroeconomici eterogenei, standardizzazione dei tipi di dato e filtraggio di outlier macroscopici ed errori di inserimento storici.
* **Statistica Descrittiva e ranking:** Calcolo di indicatori di tendenza centrale, dispersione e percentili, con isolamento dei Top 10 paesi per spesa media in istruzione (filtrando per serie storiche con almeno 5 anni di rilevazioni).
* **Analisi di correlazione e Time-Lags ($T+5$ e $T+10$):** Valutazione dell'impatto ritardato del capitale umano sulla crescita economica.
* **Segmentazione per fasce di reddito:** Classificazione dei paesi in terzili (Low, Middle, High Income) tramite quantili per analizzare differenze strutturali nei rendimenti della spesa educativa.
* **Analisi di Volatilità e Resilienza:** Studio della deviazione standard della spesa in istruzione per valutare se la stabilità degli investimenti impatti la performance economica di lungo periodo.
* **Econometria Panel (Fixed Effects):** Rimozione dell'eterogeneità non osservabile tra paesi tramite trasformazione *Within-Group* (demeaning) e stima OLS per isolare l'effetto reale della spesa.

---

## 🛠️ Stack Tecnologico & Librerie
Il progetto è interamente sviluppato in **Python** all'interno di un ambiente Jupyter Notebook:
* **Pandas**: Manipolazione strutturata dei dataframe, merge e raggruppamenti.
* **NumPy**: Operazioni numeriche e supporto al calcolo statistico.
* **Matplotlib**: Personalizzazione e rendering dei grafici.
* **Seaborn**: Visualizzazioni statistiche avanzate (`histplot`, `barplot`, `regplot`, `lmplot` con facet grid).
* **Statsmodels**: Stima dei modelli econometrici e verifiche statistiche.

---

## 📈 Fasi e Moduli dell'analisi

### 1. Data Cleaning e Filtraggio
* Caricamento dei file CSV (PIL pro capite, crescita PIL, spesa in istruzione).
* Conversione rigorosa dei tipi (`year` int, `value` float) e rimozione dei valori nulli.
* Applicazione di filtri di validità economica per eliminare anomalie estreme ($0 < \text{valore} \le 30$).

### 2. Statistiche descrittive e Top 10 spender
* Analisi della distribuzione globale della spesa in istruzione (% del PIL) con calcolo di media, mediana, deviazione standard e percentili ($10^\circ, 25^\circ, 50^\circ, 75^\circ, 90^\circ$).
* Aggregazione per paese filtrando le serie storiche con almeno 5 rilevazioni per evitare distorsioni da singoli anni isolati.

### 3. Correlazione contemporanea e Time-Lags ($T+5$ e $T+10$)
* Calcolo della correlazione di Pearson bivariata contemporanea.
* Traslazione temporale della spesa educativa a $T+5$ e $T+10$ anni per testare l'ipotesi teorica secondo cui il capitale umano richiede tempo per generare produttività sistemica.

### 4. Segmentazione per fasce di reddito
* Divisione della platea in 3 gruppi omogenei (`pd.qcut`): *Low Income / Developing*, *Middle Income*, *High Income / Developed*.
* Confronto delle rette di regressione tramite `sns.lmplot` per evidenziare come varia la relazione spesa-crescita a seconda dello stadio di sviluppo economico.

### 5. Volatilità della spesa in istruzione e resilienza
* Calcolo della deviazione standard della spesa per ciascun paese per misurare la stabilità delle politiche di bilancio pubbliche nel tempo, mettendola in relazione con la crescita media del PIL.

### 6. Modello Panel ad Effetti Fissi (Within-Transformation)
* Applicazione della trasformazione *demeaned* ($X_{it} - \bar{X}_i$) per eliminare le differenze strutturali fisse tra nazioni (es. istituzioni, geografia).
* Stima OLS sui dati depurati per stimare l'effettivo coefficiente di impatto della spesa educativa, supportato da un'attenta interpretazione economica finale.

---

## 📊 Visualizzazioni chiave incluse nel Notebook
1. **Distribuzione Globale della Spesa (% PIL):** Istogramma con curva KDE e linee verticali per Media e Mediana.
2. **Top 10 Paesi Spender:** Grafico a barre orizzontali con palette cromatica `viridis`.
3. **Scatter Plot di Correlazione e Lag Temporali:** Analisi della dispersione con rette di regressione (`sns.regplot`).
4. **Confronto per Fasce di Reddito (FacetGrid):** Analisi multivariata divisa per terzili di PIL pro capite.
5. **Volatilità vs Crescita Economica:** Scatter plot con evidenza della stabilità degli investimenti.

---

