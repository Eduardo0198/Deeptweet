🤖 DeepTweet — DATA 

### RAW_DATA

Contiene los 3 datasets que se usaron para los modelos 
* Modelo 1 - Sentiment_140.csv
* Modelo 2 - Tweets.csv + TweetEval (carpeta con train, val y test)
* Modelo 3 - real_tweets_tech.csv (se descargaron con una API en Google Colab)

Estos mismos datasest son los que procesados obtenemos las secuencias .npy que son las que basicamente le dan forma para que el modelo pueda entrenar

### PROCESSED_DATA

La carpeta DATA_PROCESSED almacena todos los tensores tokenizados y preprocesados generados por los ETLs de cada una de las tres iteraciones del proyecto DeepTweet.
Estos datos ya están listos para ser cargados directamente por los modelos (v1, v2, v3) sin necesidad de repetir el preprocesamiento.


👉 Drive (Datasets):
https://drive.google.com/drive/folders/1f3kpO7VQNBeD3GcKodmALRMs7T8MIZUd?usp=sharing

En el repositorio local solo se incluyen pues los archivos .csv son demasiado pesados

👉 A si mismo estos archivos son fundamenteles para que los notebook del modelo base y los dos Fine Tunning puedan funcionar (processed_data). 
👉 Por otro lado tambien puedes generar tu mismos los tensores tokenizados corriendo los ETLs con los datasets sin procesar (raw_data)

```bash
Drive (link)
|
RAW_DATA/
│
├── TweetEval/
│   ├── tweet_eval_sentiment_1.csv
│   ├── tweet_eval_sentiment_2.csv
│   ├── tweet_eval_sentiment_3.csv
│  
├── Sentiment_140.csv
├── Tweets.csv
├── real_tweets_tech.csv
│
│  
PROCESSED_DATA/
│
├── v1_base/
│   ├── tokenizer.pkl
│   ├── X_train.npy
│   ├── X_val.npy
│   ├── X_test.npy
│   ├── y_train.npy
│   ├── y_val.npy
│   └── y_test.npy
│
├── v2_modern/
│   ├── X_train.npy
│   ├── X_val.npy
│   ├── X_test.npy
│   ├── y_train.npy
│   ├── y_val.npy
│   └── y_test.npy
│
└── v3_realtweets/
    ├── X_train_live.npy
    ├── X_val_live.npy
    ├── X_test_live.npy
    ├── y_train_live.npy
    ├── y_val_live.npy
    └── y_test_live.npy
```
