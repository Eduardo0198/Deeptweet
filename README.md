<img width="800" height="200" alt="image" src="https://github.com/user-attachments/assets/9dd03a0f-7631-46d6-9a0c-06db2bcffabb" />


# DeepTweet – Análisis de Sentimientos con LSTM

🐦 DeepTweet — Sentiment Analysis con LSTM (2009 → 2025)

DeepTweet es un sistema de análisis de sentimiento diseñado para clasificar tweets como positivos o negativos, utilizando una arquitectura LSTM Bidireccional y un enfoque iterativo basado en fine-tuning con datos de distintas épocas.

El objetivo central es demostrar cómo un modelo clásico (entrenado con tweets de 2009) puede evolucionar hasta interpretar lenguaje moderno y tweets reales de 2023–2025 mediante ciclos progresivos de actualización.

---

##  Estructura del Proyecto
```bash
DeepTweet/
│
├── notebooks/
│   ├── 01_ETL_sentiment140.ipynb        # Limpieza y preparación del dataset base (2009)
│   ├── 02_Model_LSTM_Base.ipynb         # Entrenamiento del modelo base (v1)
│   ├── 03_ETL_modern.ipynb              # ETL de TweetEval + Kaggle (2016–2022)
│   ├── 04_Model_FineTuning_Modern.ipynb # Fine-tuning con dataset moderno (v2)
│   ├── 05_ETL_Realtime_Tweets.ipynb     # Recolección/limpieza de tweets reales (2023–2025)
│   ├── 06_Model_FineTuning_Final.ipynb  # Entrenamiento final con tweets reales (v3)
│   ├── 07_Interface.ipynb               # Interfaz de predicción con el modelo final
│ 
DRIVE
https://drive.google.com/drive/folders/1f3kpO7VQNBeD3GcKodmALRMs7T8MIZUd?usp=sharing
|
├── models/
│   ├── deeptweet_v1_base.h5
│   ├── deeptweet_v2_modern.h5
│   ├── deeptweet_v3_final.h5
│
├── data/
│   ├── sentiment140/
│   ├── tweeteval/
│   ├── twitter_kaggle/
│   ├── realtime/
│   └── tensors_npy/
│
└── README.md   # (este documento)
```

Este documento explica **qué hace cada notebook**, qué **recibe**, qué **produce**, y cómo se conectan entre sí.  
Es una guía completa para entender el flujo del proyecto.
# 🧠 Pipeline General del Proyecto

* 01_ETL_sentiment140.ipynb → genera tensores para v1
* 02_Model_LSTM_Base.ipynb → entrena modelo v1
* 03_ETL_modern.ipynb → genera tensores para v2
* 04_Model_FineTuning_Modern.ipynb → entrena modelo v2 y usa el modelo v1
* 05_ETL_Realtime_Tweets.ipynb → genera tensores para v3
* 06_Model_FineTuning_Final.ipynb → entrena modelo v3 y usa el modelo v2
* 07_Interface.ipynb → carga modelos + pruebas

Todos los datasets, tensores y modelos generados por los ETLs  están organizados en:

 * MODELOS (.h5)
 * PROCESSED_DATA (tensores y un .pkl)
 * RAW_DATA (.csv)

📁 Drive:
https://drive.google.com/drive/folders/1f3kpO7VQNBeD3GcKodmALRMs7T8MIZUd?usp=sharing

---
# 🎯 Cumplimiento de Competencias

### ✅ 1. Uso de un framework de Deep Learning
El proyecto utiliza **TensorFlow/Keras** para construir, entrenar y ajustar los modelos (LSTM Bidireccional, capas Dense, Dropout, optimizador Adam y callbacks).

### ✅ 2. Evaluación y mejora del modelo
Se entrenaron tres versiones del modelo:
- **v1**: baseline con Sentiment140  
- **v2**: fine-tuning con TweetEval + Kaggle  
- **v3**: fine-tuning final con tweets reales  
Cada iteración incluye evaluación, métricas y ajustes para mejorar desempeño.

### ✅ 3. Uso de datos reales
Se emplearon datasets reales y externos:
- Sentiment140 (1.6M tweets)
- TweetEval (HuggingFace)
- Twitter Sentiment (Kaggle)
- Tweets reales 2023–2025 vía API  
Ninguno pertenece a ejemplos de clase.

### ✅ 4. Predicciones mediante interfaz
El notebook **07_Interface.ipynb** permite cargar los modelos, escribir textos y obtener predicciones en tiempo real, cumpliendo con el requisito de generar resultados desde una interfaz interactiva.


---

# 📓 01 — ETL Sentiment140 (Base)

**Archivo:** `01_ETL_sentiment140.ipynb`

### ✔ ¿Qué hace?
Prepara el dataset Sentiment140 de 2009 y genera los tensores para entrenar el modelo base.

### ✔ Recibe:
- CSV original de 1.6M tweets con ruido  
- etiquetas {0, 4}

### ✔ Procesa:
- Limpieza profunda:
  - menciones
  - URLs
  - hashtags
  - emojis
  - duplicados
- Tokenización **desde cero**
- Padding
- Train / val / test split

### ✔ Produce (guardado en `data_processed/v1_base/`):
- `tokenizer.pkl`
- `X_train.npy`, `X_val.npy`, `X_test.npy`
- `y_train.npy`, `y_val.npy`, `y_test.npy`

---

# 📓 02 — Modelo LSTM Base (v1)

**Archivo:** `02_Model_LSTM_Base.ipynb`

### ✔ ¿Qué hace?
Entrena la **versión 1** del modelo (baseline).

### ✔ Recibe:
- Tensores procesados (v1)
- Tokenizer

### ✔ Produce:
- `deeptweet_v1_base.h5`

### ✔ Usado por:
→ `04_Model_FineTuning_Modern.ipynb`

---

# 📓 03 — ETL Modern (TweetEval + Kaggle)

**Archivo:** `03_ETL_modern.ipynb`

### ✔ ¿Qué hace?
Prepara un dataset contemporáneo fusionando:

- TweetEval (HuggingFace)
- Twitter Sentiment (Kaggle)

### ✔ Recibe:
- datasets modernos (raw)

### ✔ Procesa:
- limpieza ligera  
- mapeo a 0/1  
- mezcla de datasets  
- tokenización **usando tokenizer v1**  
- padding  
- split 60/20/20  

### ✔ Produce (en `data_processed/v2_modern/`):
- `X_train.npy`, `X_val.npy`, `X_test.npy`
- `y_train.npy`, `y_val.npy`, `y_test.npy`

---

# 📓 04 — Fine-Tuning Moderno (v2)

**Archivo:** `04_Model_FineTuning_Modern.ipynb`

### ✔ ¿Qué hace?
Crea la **versión 2** del modelo ajustando el v1 con lenguaje moderno.

### ✔ Recibe:
- tensores v2  
- modelo v1  

### ✔ Procesa:
- congelamiento de capas profundas  
- fine-tuning suave  
- learning rate bajo  

### ✔ Produce:
- `deeptweet_v2_modern.h5`

### ✔ Usado por:
→ `06_Model_FineTuning_Final.ipynb`

---

# 📓 05 — ETL Tweets Reales (Live API)

**Archivo:** `05_ETL_Realtime_Tweets.ipynb`

### ✔ ¿Qué hace?
Procesa tweets reales 2023–2025 obtenidos vía API académica.

### ✔ Recibe:
- JSON con tweets reales

### ✔ Procesa:
- limpieza idéntica a v1  
- conserva estilo moderno  
- tokenización con tokenizer v1  
- padding  
- split 70/15/15  

### ✔ Produce (en `data_processed/v3_realtweets/`):
- `X_train_live.npy`, `X_val_live.npy`, `X_test_live.npy`
- `y_train_live.npy`, `y_val_live.npy`, `y_test_live.npy`

---

# 📓 06 — Fine-Tuning Final (v3)

**Archivo:** `06_Model_FineTuning_Final.ipynb`

### ✔ ¿Qué hace?
Crea la **versión final del modelo**, la más precisa y adaptada al lenguaje real.

### ✔ Recibe:
- tensores live (v3)
- modelo v2

### ✔ Procesa:
- early stopping  
- fine-tuning con datos reales  
- mezcla de capas congeladas + entrenables  

### ✔ Produce:
- `deeptweet_v3_final.h5`  
→ *modelo recomendado*

---

# 📓 07 — Interfaz / Demo de Predicción

**Archivo:** `07_Interface.ipynb`

### ✔ ¿Qué hace?
Notebook interactivo para **probar los modelos** (v1, v2 o v3).

### ✔ Recibe:
- cualquier modelo `.h5`
- tokenizer `.pkl`

### ✔ El usuario puede:
- cargar modelos manualmente  
- escribir tweets  
- obtener predicciones en tiempo real  

### ✔ Entrada:
Texto escrito por el usuario:




