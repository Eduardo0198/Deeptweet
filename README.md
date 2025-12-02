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



