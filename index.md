<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;800&display=swap');

  :root {
    --sam-blue: #034EA2;
    --dark: #000000;
    --gray: #666666;
    --light-bg: #ffffff; 
  }

  body { 
    font-family: 'Inter', sans-serif; 
    background-color: var(--light-bg);
    color: var(--dark);
    max-width: 850px;
    margin: 0 auto;
    padding: 60px 20px;
  }

  .header-area {
    text-align: left;
    border-bottom: 2px solid #eee;
    padding-bottom: 40px;
    margin-bottom: 50px;
  }

  .campus-tag {
    color: var(--sam-blue);
    font-weight: 800;
    letter-spacing: 1.5px;
    font-size: 0.85rem;
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  h1 { 
    font-size: 3.5rem;
    font-weight: 800;
    line-height: 1;
    margin: 10px 0;
    letter-spacing: -2px;
  }

  .subtitle {
    font-size: 1.25rem;
    color: var(--gray);
    margin-bottom: 30px;
  }

  /* Lista de integrantes */
  .team-list {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    margin-bottom: 30px;
  }

  .team-item {
    font-size: 0.9rem;
    background: #f1f1f1;
    padding: 5px 12px;
    border-radius: 4px;
    font-weight: 600;
  }

  /* Botón de colab */
  .colab-link img {
    box-shadow: none !important;
    margin: 0 !important;
    transition: opacity 0.2s;
  }
  .colab-link img:hover { opacity: 0.8; }

  /* Ajustes de contenido */
  h2 { 
    font-size: 1.8rem;
    margin-top: 60px;
    border-bottom: 1px solid #eee;
    padding-bottom: 10px;
  }

  table {
    border-radius: 0;
    box-shadow: none;
    border: 1px solid #eee;
  }
  
  th { background-color: #fafafa !important; color: var(--dark) !important; border-bottom: 2px solid var(--sam-blue) !important; }

  /* Quita sombras de las imágenes */
  img {
    border-radius: 4px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
  }
</style>

<div class="header-area">
  <div class="campus-tag">Samsung Innovation Campus</div>
  <h1>Signal Lab.</h1>
  <p class="subtitle">Predicción de Riesgo de Diabetes Tipo 2 mediante Inteligencia Artificial aplicada a la ENSANUT 2024.</p>
  
  <div class="team-list">
    <span class="team-item">Medina Mixtega Ángel Miguél</span>
    <span class="team-item">Plascencia Arevalo Alberto</span>
    <span class="team-item">Méndez Ortega Paula</span>
    <span class="team-item">Mota Barraza Moisés</span>
    <span class="team-item">Méndez Damián Brandon Efren</span>
  </div>

  <a href="https://colab.research.google.com/drive/1nX9DHH1Ts1Y1LvaSJwoYT7Lzrs1dS6dc?usp=sharing" class="colab-link">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab">
  </a>
</div>

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
