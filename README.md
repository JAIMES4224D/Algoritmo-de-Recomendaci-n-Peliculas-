
```markdown
<div align="center">

# 🎬 Sistema de Recomendación de Películas
### Mitigación de Sobrecarga de Información con Machine Learning

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)

<p align="center">
  <a href="#-descripción-del-proyecto">Descripción</a> •
  <a href="#-metodología">Metodología</a> •
  <a href="#-arquitectura">Arquitectura</a> •
  <a href="#-instalación-y-uso">Cómo Usar</a> •
  <a href="#-créditos">Créditos</a>
</p>

</div>

---

## 📖 Descripción del Proyecto

Este proyecto implementa un **Sistema de Recomendación Basado en Contenido** (Content-Based Filtering) diseñado para mitigar la "parálisis por análisis" que sufren los usuarios de plataformas de streaming como Netflix.

A diferencia de los sistemas colaborativos tradicionales, este algoritmo no requiere historial de usuario (solucionando el problema del *Cold Start*). En su lugar, utiliza **Procesamiento de Lenguaje Natural (NLP)** para analizar la similitud semántica entre películas basándose en su trama, género, director y actores.

## 📉 El Problema de Negocio

La gestión de catálogos masivos genera **"Sobrecarga de Información"**:
* **Paradoja de la elección:** El exceso de opciones bloquea la decisión del usuario.
* **Impacto Negativo:** Aumenta el tiempo de navegación improductiva y el riesgo de cancelación (*Churn Rate*).

**Objetivo:** Transformar el catálogo en una experiencia curada y personalizada.

---

## 🧠 Metodología y Algoritmo

El núcleo del sistema es un pipeline de Machine Learning desarrollado en Python:

### 1. Ingesta y Limpieza (Data Wrangling)
Se unificaron tres fuentes de datos (`movies_metadata`, `credits`, `keywords`) del dataset "The Movies Dataset". Se realizó un *parsing* de estructuras JSON complejas y limpieza de IDs para asegurar la integridad.

### 2. Feature Engineering: "Metadata Soup"
Se creó una variable sintética (`metadata_soup`) que combina todos los atributos textuales con una **ponderación estratégica** para capturar la "firma autoral":

```python
# Ponderación aplicada para mejorar la relevancia
metadata_soup = (
    overview + 
    (genres * 2) +      # Doble peso al género
    (keywords * 3) +    # Triple peso a temas de nicho
    (cast * 3) +        # Triple peso a protagonistas
    (director * 3)      # Triple peso al Director
)

```

### 3. Modelo Matemático

* **TF-IDF Vectorizer:** Convierte la sopa de texto en una matriz numérica, penalizando palabras comunes y resaltando términos únicos.
* **Similitud del Coseno:** Calcula el ángulo entre los vectores de las películas para determinar su grado de parentesco temático.

---

## ☁️ Arquitectura en la Nube (AWS)

El proyecto está diseñado para desplegarse como un microservicio:

| Componente | Tecnología | Función |
| --- | --- | --- |
| **Cómputo** | Amazon EC2 (t2.medium) | Alojamiento del servidor y la API |
| **Almacenamiento** | Amazon S3 | Resguardo de modelos serializados (`.pkl`) |
| **API** | FastAPI | Endpoint REST `/recommend` para consultas |
| **Serialización** | Joblib | Persistencia del modelo entrenado |

---

## 📊 Resultados y Validación

Dado que es un modelo no supervisado, se validó mediante **Pruebas de Coherencia Semántica**:

> **Prueba de Entrada:** *The Dark Knight* (Christopher Nolan)
> **Resultados del Modelo:**
> 1. *The Dark Knight Rises* (Secuela) ✅
> 2. *Batman Begins* (Precuela) ✅
> 3. *Inception* (Mismo Director/Estilo) ✅
> 
> 

El modelo demostró respetar géneros puros y detectar hibridaciones lógicas (ej. Acción + Ciencia Ficción).

---

## ⚙️ Instalación y Uso

### Prerrequisitos

* Python 3.8+
* Librerías: `pandas`, `numpy`, `scikit-learn`, `joblib`

### Pasos para ejecutar

1. **Clonar el repositorio:**
```bash
git clone [https://github.com/tu-usuario/recomendador-cine.git](https://github.com/tu-usuario/recomendador-cine.git)

```


2. **Instalar dependencias:**
```bash
pip install pandas numpy scikit-learn joblib

```


3. **Ejecutar el script maestro:**
```bash
python scriptmaestro.py

```


*Esto entrenará el modelo, generará las gráficas de análisis y guardará los archivos `.pkl`.*

---

## 🎓 Créditos

<div align="center">

**Universidad Privada Norbert Wiener** *Facultad de Ingeniería*

**Curso:** Gestión y Ciencias de Datos in Cloud

**Docente:** Rodriguez Ruiz, Wilmer Leoncio

**Desarrollado por:**

<h3>Jaimes Passuni, Jeferson</h3>

Lima, Perú - 2025

</div>

```

```
