<style>
  :root {
    --primary: #2c3e50;
    --accent: #3498db;
    --bg: #f4f7f6;
    --text: #333;
    --white: #ffffff;
  }

  body { 
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif; 
    line-height: 1.6; 
    background-color: var(--bg);
    color: var(--text);
    max-width: 900px;
    margin: 0 auto;
    padding: 20px;
  }

  /* Título con gradiente */
  h1 { 
    font-size: 2.5rem;
    background: linear-gradient(120deg, #2c3e50, #3498db);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    border-bottom: 4px solid var(--accent);
    padding-bottom: 15px;
    text-align: center;
  }

  h2 { 
    color: var(--primary);
    border-left: 5px solid var(--accent);
    padding-left: 15px;
    margin-top: 50px;
    background: rgba(52, 152, 219, 0.05);
  }

  /* Estilo de tarjetas para imágenes y tablas */
  img, table {
    background: var(--white);
    border-radius: 12px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    transition: transform 0.3s ease;
    margin: 20px 0;
  }

  img:hover {
    transform: translateY(-5px);
  }

  /* Tabla */
  table {
    width: 100%;
    border-collapse: collapse;
    overflow: hidden;
  }

  th {
    background-color: var(--accent);
    color: white;
    padding: 12px;
  }

  td {
    padding: 12px;
    border-bottom: 1px solid #eee;
  }

  tr:hover { background-color: #f1f1f1; }

  /* Bloques resaltados para los objetivos */
  blockquote {
    background: #eef6fc;
    border-left: 8px solid var(--accent);
    margin: 1.5em 10px;
    padding: 1em 15px;
    border-radius: 0 15px 15px 0;
    font-style: italic;
  }

  /* Botones de navegación (índice) */
  ul {
    list-style: none;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }

  ul li a {
    text-decoration: none;
    background: var(--white);
    padding: 8px 16px;
    border-radius: 20px;
    border: 1px solid var(--accent);
    color: var(--accent);
    font-weight: bold;
    font-size: 0.9rem;
    transition: all 0.3s;
  }

  ul li a:hover {
    background: var(--accent);
    color: white;
  }
</style>

# Signal Lab: Predicción de Riesgo de Diabetes Tipo 2
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1nX9DHH1Ts1Y1LvaSJwoYT7Lzrs1dS6dc?usp=sharing)

### Inteligencia Artificial Aplicada a la Salud Pública en México (ENSANUT 2024)
## Tabla de Contenidos
- [Objetivo](#-emergencia-sanitaria-silenciosa)
- [Metodología](#️-metodología-y-arquitectura-de-datos)
- [Resultados](#-análisis-exploratorio-y-validación-biológica)
- [Modelado](#-resultados-torneo-de-algoritmos)
- [Perfiles de Riesgo](#-interpretabilidad-y-perfilamiento-k-means)

---

## 🇲🇽 Emergencia Sanitaria Silenciosa
México registra aproximadamente **169,425 nuevos diagnósticos** de DMT2 al año. El desafío de **Signal Lab** es transitar de una medicina *reactiva* a un tamizaje *preventivo predictivo* mediante métodos no invasivos.

> **Objetivo:** desarrollar modelos de Machine Learning que superen un **AUC-ROC de 0.70**, optimizando la detección en etapas preventivas sin depender de pruebas de laboratorio costosas.

---

## Metodología y Arquitectura de Datos
Nuestro pipeline integra cinco módulos fundamentales de la **ENSANUT Continua 2024**, logrando una visión holística del paciente.

### 1. Sincronización Multimodal (`FOLIO_I`)
Se diseñó una **Ingeniería de Identificadores Sintéticos** para resolver la disparidad de formatos entre módulos:
`FOLIO_I = UPM + VIV_SEL + NUM_REN`

### 2. Ingeniería de Características (Feature Engineering)
Trascendimos el uso de variables crudas creando indicadores biomédicos avanzados:
* **Presión de Pulso (PP):** `Sistólica - Diastólica` (Predictor de rigidez arterial).
* **Riesgo Combinado:** `Edad x IMC` (Captura el efecto multiplicador del envejecimiento y sobrepeso).

---

## Análisis Exploratorio y Validación Biológica

Para validar la integridad de los datos, realizamos un análisis de correlación de Pearson.

![Análisis de Correlación](correlacion.png)
**

**Hallazgo Clave:** La baja correlación lineal individual entre IMC y Diabetes justifica el uso de **Inteligencia Artificial**, capaz de detectar patrones no lineales y relaciones de alto orden que los métodos tradicionales omiten.

---

## Resultados: Torneo de Algoritmos
Evaluamos múltiples arquitecturas, seleccionando **Random Forest** por su equilibrio y superioridad en la sensibilidad clínica.

| Modelo | F1-Score | AUC-ROC | Recall (Sensibilidad) |
| :--- | :---: | :---: | :---: |
| **Random Forest** | **0.60** | **0.71** | **0.69** |
| Gradient Boosting | 0.61 | 0.70 | 0.65 |
| Regresión Logística | 0.58 | 0.69 | 0.63 |
| SVM (Linear) | 0.57 | 0.68 | 0.59 |

### Matriz de Confusión y Seguridad del Paciente
Nuestro modelo identifica correctamente a **7 de cada 10 individuos en riesgo**, priorizando la reducción de falsos negativos.

![Matriz de Confusión](matriz.png)
**

---

## Interpretabilidad y Perfilamiento (K-Means)
No solo predecimos; entendemos la lógica del riesgo. La **Presión Sistólica** se consolidó como el predictor más determinante.

![Importancia de Variables](importancia.png)
**

### Segmentación de Riesgo Poblacional
Identificamos tres fenotipos clínicos mediante **K-Means + PCA**:
* 🟢 **Bajo Riesgo:** Adultos jóvenes (Promedio 34.7 años).
* 🟠 **Riesgo Metabólico:** Mediana edad con el IMC más elevado (33.8).
* 🔴 **Riesgo Geriátrico:** Adultos mayores; el riesgo es dominado por el envejecimiento y la presión arterial.

![Clustering de Población](clusters.png)
**

---

##  Conclusiones y Estado del Arte
El sistema de **Signal Lab** alcanzó un **ROC-AUC de 0.7120**, situándose en el **límite superior de los estándares globales** para modelos de tamizaje no invasivos (Benchmarks internacionales NHANES establecen techos de 0.60 - 0.70).

---

## Referencias
* **American Diabetes Association.** (2023). *Standards of Care in Diabetes*.
* **Instituto Nacional de Salud Pública.** (2024). *ENSANUT Continua 2024*.
* **Zhang, L., et al.** (2014). *Predicting Type 2 Diabetes using non-invasive methods*. Scientific Reports.
