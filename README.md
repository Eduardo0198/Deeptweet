# DeepTweet – Análisis de Sentimientos con LSTM

**DeepTweet** es un proyecto de *NLP (Procesamiento de Lenguaje Natural)* que utiliza redes neuronales **LSTM** para analizar sentimientos en tweets.  
A partir del dataset **Sentiment140**, el modelo aprende a reconocer emociones positivas y negativas, permitiendo observar tendencias emocionales en redes sociales.  
En futuras etapas, se integrará un dataset de **tweets políticos** para explorar la percepción social frente a eventos y figuras públicas.

---

##  Estructura del Proyecto

###  `01_ETL_deeptweet.ipynb`
> Carga, limpieza y análisis exploratorio de los datos.  
- Limpieza de texto (URLs, menciones, hashtags, símbolos).  
- Análisis de longitud de tweets y *wordclouds* por sentimiento.  
- Generación de dataset procesado para el modelado.

### `02_Model_deeptweet.ipynb`
> Modelado y entrenamiento con LSTM.  
- Tokenización y secuencias.  
- Entrenamiento del modelo y evaluación (Accuracy, F1, etc.).  
- Preparado para *fine-tuning* con tweets políticos.

###  `03_Interface_deeptweet.ipynb`
> Pruebas y visualización de resultados.  
- Carga del modelo entrenado.  
- Predicciones con nuevos textos.  
- (Opcional) Interfaz interactiva con Gradio o Streamlit.

---

## Datasets

- **Sentiment140:** Dataset con 1.6M tweets clasificados en positivo (4) y negativo (0).  
- **Tweets Políticos (pendiente):** Para especializar el modelo en análisis de percepción política.

---

## 🚀 Objetivo
Crear un modelo capaz de **analizar y entender emociones colectivas** expresadas en redes sociales, con potencial para el estudio de **tendencias políticas y sociales**.
