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
├── Lab6_Proyecciones.ipynb
├── nodos_bipartita.csv
├── aristas_bipartita.csv
├── comments_clean.csv
├── fase_5_proyecciones/
│   ├── aristas_autor_autor.csv
│   ├── aristas_video_video.csv
│   ├── nodos_autor_autor.csv
│   ├── nodos_video_video.csv
│   └── archivos de validación
├── fase_6_metricas/
│   ├── metricas_estructurales_basicas.csv
│   ├── estadisticas_grados_basicas.csv
│   ├── distribucion_grados_completa.csv
│   ├── componentes_analisis.csv
│   └── resumen_topologia_redes.csv
├── fase_7_comunidades/
│   ├── tamanos_comunidades.csv
│   ├── autores_comunidades.csv
│   ├── resumen_comunidades.csv
│   ├── top_autores_por_comunidad.csv
│   ├── top_videos_por_comunidad.csv
│   ├── top_canales_por_comunidad.csv
│   ├── temas_frecuentes_por_comunidad.csv
│   ├── sentimiento_comentarios.csv
│   └── sentimiento_por_comunidad.csv
└── graficos/
    ├── 05_red_autor_autor.png
    ├── 06_red_video_video.png
    ├── 06_distribucion_grados.png
    └── 07_red_comunidades_autor_autor.png
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

```bash
pip install networkx pysentimiento
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


## Cómo ejecutar las secciones 5 a 7

1. Asegurate de haber ejecutado previamente las secciones 1 a 4 y de tener disponibles:

   - `nodos_bipartita.csv`
   - `aristas_bipartita.csv`
   - `comments_clean.csv`

2. Abrí `Lab6_Proyecciones.ipynb`.

3. Ejecutá las celdas **en orden**, de arriba hacia abajo.

| Sección | Contenido |
|---|---|
| 5 | Construcción de las proyecciones autor–autor y video–video, validación de pesos y visualización |
| 6 | Métricas estructurales, distribución de grados, componentes conexos, cohesión, transitividad y análisis de nodos aislados/periféricos |
| 7 | Detección de comunidades con Louvain, modularidad, caracterización por autores, videos, canales, temas frecuentes y sentimiento  |