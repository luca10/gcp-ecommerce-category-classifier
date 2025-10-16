# 🛒 Progetto di Data Science: Classificatore di Categorie di Prodotti E-commerce su GCP


## 🎯 Obiettivo del Progetto

Questo progetto implementa una pipeline di Machine Learning completa su **Google Cloud Platform (GCP)** per la classificazione automatica dei prodotti e-commerce in categorie principali (`Apparel`, `Footwear`, `Accessories`, ecc.), basandosi sulle loro caratteristiche descrittive.

L'obiettivo è dimostrare la capacità di gestire un flusso di dati moderno, dalla fase di **storage grezzo** (GCS) all'**addestramento del modello** (Python) e alla **persistenza del Data Warehouse** (BigQuery).

## 🚀 Architettura della Soluzione (Data Pipeline)

La pipeline segue un'architettura Cloud standard:

1.  **Storage GCS (Data Lake):** Il dataset grezzo (`styles.csv`) è caricato e mantenuto in **Google Cloud Storage**.
2.  **Elaborazione & ML (Python/Workbench):** L'analisi, la pulizia dei dati e l'addestramento del modello avvengono su **Vertex AI Workbench** (Jupyter Notebook).
3.  **Data Warehouse (BigQuery):** Il dataset pulito e trasformato (le *feature* pronte per l'ML) viene caricato in **BigQuery** come fonte di verità per analisi future.
4.  **Artefatto ML:** Il modello addestrato (`category_classifier.joblib`) è salvato e persistito in **GCS** per il deployment.

---

## 💻 Stack Tecnologico e Feature Engineering

### Stack Tecnologico

| Area | Tecnologia | Librerie/Servizi Chiave |
| :--- | :--- | :--- |
| **Cloud** | **Google Cloud Platform (GCP)** | GCS, BigQuery, Vertex AI Workbench |
| **Core** | **Python 3.10+** | SQL |
| **Data Analysis** | Pandas, NumPy | Gestione Dati Malformati, EDA |
| **Machine Learning** | **Scikit-learn** | Random Forest Classifier, LabelEncoder, TfidfVectorizer |
| **Deployment** | **Joblib** | Salvataggio dell'artefatto ML in GCS |

### Dettagli del Feature Engineering

* **Dati Testuali:** La colonna `productDisplayName` (nome del prodotto) è stata vettorizzata utilizzando **TF-IDF (Term Frequency-Inverse Document Frequency)**, creando centinaia di feature numeriche.
* **Dati Categoriali:** Variabili come `gender`, `season`, `articleType`, ecc., sono state convertite tramite **One-Hot Encoding** per l'uso nel modello.
* **Pulizia:** È stata implementata una gestione avanzata del caricamento (`on_bad_lines='skip'`) per superare gli errori di tokenizzazione del CSV.

---

## 📊 Risultati e Performance del Modello

Il modello è stato addestrato su un set di training bilanciato e valutato su un set di testing separato (20% dei dati).

| Algoritmo | **Random Forest Classifier** |
| :--- | :--- |
| **Target (Y)** | `masterCategory` |
| **Accuracy Generale** | **99.98%** |

#### Report di Classificazione

La performance eccellente è confermata dai valori perfetti di Precision, Recall e F1-Score su tutte le classi principali:

| Categoria | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- |
| **Media Ponderata** | 1.00 | 1.00 | 1.00 |
| *Apparel, Accessories, Footwear* | *Performance perfetta* | *Performance perfetta* | *Performance perfetta* |

---

## 💡 Prossime Implementazioni Future

1.  **Deployment su Vertex AI:** Creazione di un **Vertex AI Endpoint** per ospitare il modello e renderlo accessibile per previsioni in tempo reale (API REST).
2.  **Orchestrazione ETL:** Automatizzazione della pipeline completa (da GCS a BigQuery) utilizzando **Cloud Dataflow** o **Cloud Composer**.
3.  **Validazione Avanzata:** Esecuzione della **K-Fold Cross-Validation** e ottimizzazione degli iper-parametri (`GridSearchCV`) per confermare la stabilità del modello.

---

## ⚙️ Istruzioni per l'Esecuzione

1.  **Clona il Repository:** `git clone https://github.com/luca10/gcp-ecommerce-category-classifier.git`
2.  **Autenticazione GCP:** Configura le credenziali di default: `gcloud auth application-default login`
3.  **Dependencies:** Installare le librerie richieste (Pandas, Scikit-learn, google-cloud-storage, google-cloud-bigquery).
4.  **Esecuzione:** Apri il file **`data_pipeline_ml.ipynb`** in JupyterLab e segui le celle in sequenza.