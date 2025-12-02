🤖 DeepTweet — Modelos Entrenados (v1, v2, v3)

El proyecto utiliza un enfoque iterativo: cada modelo se basa en el anterior.

Todos los modelos completos (.h5) están en esta carpeta de Drive:

👉 Drive (Modelos entrenados):
https://drive.google.com/drive/folders/1f3kpO7VQNBeD3GcKodmALRMs7T8MIZUd?usp=sharing

En el repositorio local solo se incluyen versiones del segundo y el tercer modelo en .zip por si lo quieren ver.
No pude subir el primer modelo en .zip ya que era demsaido pesado por eso es que los modelos los pueden encontrar en la carpeya de Drive

A si mismo estos archivos son fundamenteles para que el notebook 07_Interface_deeptweet.ipynb pueda funcionar y correr todas las pruebas que quieran

```bash
models/
│
├── deeptweet_v1_base.h5          # Modelo base (2009)
├── deeptweet_v2_modern.h5        # Fine-tuning moderno
├── deeptweet_v3_final.h5         # Fine-tuning con tweets reales
│
└── tokenizer/
    ├── tokenizer_sentiment140.pkl

```
