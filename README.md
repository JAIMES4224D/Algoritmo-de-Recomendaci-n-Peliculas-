

<div align="center">

# 🎬 Algoritmo de Recomendación de Películas

### Solución de Machine Learning para la Mitigación de Sobrecarga de Información

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![AWS](https://img.shields.io/badge/Cloud-AWS-yellow?style=for-the-badge&logo=amazon-aws&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

<p align="center">
  <a href="#-descripción">Descripción</a> •
  <a href="#-características-principales">Características</a> •
  <a href="#-tecnologías-utilizadas">Tecnologías</a> •
  <a href="#-instalación">Instalación</a> •
  <a href="#-uso">Uso</a> •
  <a href="#-autores-y-créditos">Créditos</a>
</p>

</div>

---

## 📝 Descripción

Este proyecto implementa un **algoritmo de recomendación de películas basado en contenido (Content-Based Filtering)** utilizando técnicas de Procesamiento de Lenguaje Natural (NLP) y análisis de datos.

A diferencia de los sistemas tradicionales, esta solución no depende del historial de otros usuarios, resolviendo el problema del *Cold Start*. El sistema analiza la **similitud semántica** entre películas procesando atributos como tramas, directores, elenco y palabras clave para proporcionar recomendaciones personalizadas y mitigar la parálisis de elección en plataformas de streaming.

## ✨ Características Principales

- ✅ **Filtrado Basado en Contenido:** Recomendaciones puramente basadas en los metadatos de la película.
- ✅ **Ingeniería de Características ("Metadata Soup"):** Ponderación estratégica de atributos (Director x3, Elenco x3, Keywords x3) para capturar la "firma autoral".
- ✅ **NLP con TF-IDF:** Vectorización de texto para detectar términos únicos y relevantes.
- ✅ **Similitud del Coseno:** Cálculo matemático preciso de la distancia entre películas.
- ✅ **Manejo de Datos Faltantes:** Limpieza automática y parsing de estructuras JSON complejas.

## 🛠 Tecnologías Utilizadas

- **Python** - Lenguaje principal.
- **Pandas** - Manipulación y limpieza de datos (Data Wrangling).
- **NumPy** - Operaciones vectoriales.
- **Scikit-learn** - Implementación de TF-IDF y Cosine Similarity.
- **Joblib** - Serialización de modelos para despliegue.
- **FastAPI / AWS EC2** - Arquitectura de despliegue en la nube (Sugerida en documentación).

## 🚀 Instalación

Sigue estos pasos para configurar el proyecto en tu entorno local:

```bash
# 1. Clonar el repositorio
git clone [https://github.com/JAIMES4224D/Algoritmo-de-Recomendaci-n-Peliculas-.git](https://github.com/JAIMES4224D/Algoritmo-de-Recomendaci-n-Peliculas-.git)

# 2. Navegar al directorio
cd Algoritmo-de-Recomendaci-n-Peliculas-

# 3. Crear un entorno virtual (Opcional pero recomendado)
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# 4. Instalar dependencias
pip install -r requirements.txt

```

> **Nota:** Asegúrate de descargar los datasets `movies_metadata.csv`, `credits.csv` y `keywords.csv` desde [Kaggle](https://www.kaggle.com/rounakbanik/the-movies-dataset) y colocarlos en la raíz del proyecto, ya que no se incluyen por su tamaño.

## 💻 Uso

Para ejecutar el pipeline completo (limpieza, entrenamiento y validación), ejecuta el script maestro:

```bash
python scriptmaestro.py

```

### Ejemplo de código (Inferencia)

Si deseas usar el recomendador en tu propio script después de generar los modelos:

```python
import joblib
import pandas as pd

# Cargar el modelo y los datos
cosine_sim = joblib.load('cosine_sim_model.pkl')
df = pd.read_pickle('movie_data.pkl')
indices = pd.read_pickle('indices.pkl')

def recomendar(titulo, num_recs=5):
    idx = indices[titulo]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)
    top_indices = [i[0] for i in sim_scores[1:num_recs+1]]
    return df['title'].iloc[top_indices]

# Prueba
print(recomendar('The Dark Knight'))

```

## 📂 Estructura del Proyecto

```
├── README.md               # Documentación del proyecto
├── requirements.txt        # Dependencias (pandas, sklearn, etc.)
├── scriptmaestro.py        # Script principal de ETL y entrenamiento
├── cosine_sim_model.pkl    # Modelo entrenado (generado)
├── movie_data.pkl          # Data procesada (generado)
├── indices.pkl             # Mapeo de títulos (generado)
└── data/                   # Carpeta para los CSVs (ignorada en git)
    ├── movies_metadata.csv
    ├── credits.csv
    └── keywords.csv

```

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el repositorio.
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`).
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`).
4. Push a la rama (`git push origin feature/AmazingFeature`).
5. Abre un Pull Request.

## 📄 Licencia

Este proyecto está bajo la licencia MIT. Ver el archivo `LICENSE` para más detalles.

## 👥 Autores y Créditos

**Desarrollado por:**

* **JAIMES4224D** (Jaimes Passuni, Jeferson) - *Desarrollo inicial y Lógica del Algoritmo*



---

**Contacto:** Para preguntas o sugerencias, por favor abre un issue en el repositorio.
**Última actualización:** 2025-12-26
