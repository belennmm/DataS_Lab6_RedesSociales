# Laboratorio 6 — Análisis de redes sociales (YouTube)
**CC3084 – Data Science | Universidad del Valle de Guatemala**
Melisa Mendizabal · Belén Monterroso · Renato Rojas

Este README cubre el **avance** entregado (secciones 1 a 4 del laboratorio):
carga e integración de datos, calidad y limpieza, análisis exploratorio, y
construcción de la red bipartita autor–video.

## Contenido del repositorio

```
├── Lab6_Analisis_Limpieza.ipynb   # Notebook principal (secciones 1-4)
├── youtube_videos.csv             # Dataset original (293 videos, 20 variables)
├── youtube_comments.csv           # Dataset original (406 comentarios, 17 variables)
├── videos_clean.csv               # Dataset de videos ya limpio (generado por el notebook)
├── comments_clean.csv             # Dataset de comentarios ya limpio (generado por el notebook)
└── README.md
```

`videos_clean.csv` y `comments_clean.csv` se generan al correr la sección 2
del notebook; no es necesario crearlos manualmente.

## Requisitos

- Python 3.9 o superior
- Jupyter Notebook / JupyterLab

### Dependencias de Python

```bash
pip install pandas numpy matplotlib networkx wordcloud emoji py3langid nltk spacy
```

Adicionalmente se requieren dos recursos que no se instalan con `pip install`:

```bash
# Modelo de español para spaCy (lematización, sección 2.6)
python -m spacy download es_core_news_sm

# Lista de stopwords en español para NLTK (sección 2.6)
python -c "import nltk; nltk.download('stopwords')"
```

## Cómo ejecutar el análisis

1. Cloná el repositorio y colocá `youtube_videos.csv` y `youtube_comments.csv`
   en la misma carpeta que el notebook.
2. Instalá las dependencias (sección anterior).
3. Abrí `Lab6_Analisis_Limpieza.ipynb` y ejecutá las celdas **en orden**, de
   arriba hacia abajo. El notebook está dividido en las siguientes secciones:

   | Sección | Contenido |
   |---|---|
   | 1 | Carga e integración de `youtube_videos.csv` y `youtube_comments.csv` mediante `video_id` |
   | 2 | Diagnóstico de calidad, limpieza de identificadores y conteos, generación de `texto_original` / `texto_limpio`, y exportación de `videos_clean.csv` / `comments_clean.csv` |
   | 3 | Análisis exploratorio: estadísticas descriptivas, concentración de participación, popularidad vs. participación, nube de palabras y preguntas de análisis |
   | 4 | Construcción de la red bipartita autor–video (nodos, aristas, visualización e interpretación) |

4. A partir de la sección 3, el notebook vuelve a leer los datos desde
   `videos_clean.csv` y `comments_clean.csv` (ya no desde los CSV originales),
   así que la sección 2 debe correrse al menos una vez antes.

## Notas importantes

- La columna `reply_count` **no** identifica autores de respuestas ni el
  contenido de las mismas; por esa razón no se usa como arista entre
  usuarios en la red del punto 4.
- Las aristas de la red autor–video representan **co-participación
  observada** (un autor comentó en un video), no relación social,
  conversación directa ni aprobación del contenido — ver la justificación
  completa en la sección 4.5 del notebook.
- Los resultados descriptivos y de red corresponden a la muestra recolectada
  (293 videos / 406 comentarios, sesgada por las consultas de búsqueda
  usadas) y no deben generalizarse a la población total de usuarios de
  YouTube en Guatemala.
