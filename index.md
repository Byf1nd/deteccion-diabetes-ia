<style>
  :root {
    --sam-blue: #034EA2; 
    --tech-cyan: #00A9E0;
    --bg-light: #f8f9fa;
    --dark-text: #1c1c1c;
    --card-bg: #ffffff;
  }

  body { 
    font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif; 
    line-height: 1.7; 
    background-color: var(--bg-light);
    color: var(--dark-text);
    max-width: 1000px;
    margin: 0 auto;
    padding: 40px 20px;
  }

  /* Encabezado principal */
  .header-container {
    text-align: center;
    padding: 40px;
    background: var(--white);
    border-radius: 20px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.05);
    margin-bottom: 40px;
  }

  h1 { 
    font-size: 2.8rem;
    color: var(--sam-blue);
    margin-bottom: 10px;
    font-weight: 800;
  }

  .institution {
    font-size: 1.2rem;
    color: var(--tech-cyan);
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 2px;
  }

  /* Sección de colaboradores */
  .team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
    margin: 25px 0;
    text-align: center;
  }

  .member {
    background: var(--sam-blue);
    color: white;
    padding: 10px;
    border-radius: 8px;
    font-size: 0.9rem;
    font-weight: 500;
  }

  h2 { 
    color: var(--sam-blue);
    border-bottom: 3px solid var(--tech-cyan);
    display: inline-block;
    padding-bottom: 5px;
    margin-top: 50px;
  }

  /* Mejoras en tablas e imágenes */
  img {
    border-radius: 15px;
    border: 1px solid #e1e4e8;
    max-width: 100%;
    height: auto;
    display: block;
    margin: 30px auto;
  }

  table {
    border-radius: 10px;
    overflow: hidden;
    border: none;
    box-shadow: 0 5px 15px rgba(0,0,0,0.08);
  }

  th { background-color: var(--sam-blue) !important; color: white !important; }
</style>

<div class="header-container">
  <p class="institution">Samsung Innovation Campus</p>
  <h1>Signal Lab</h1>
  <p>Predicción de Riesgo de Diabetes Tipo 2 mediante Inteligencia Artificial</p>
  
  <div class="team-grid">
    <div class="member">Medina Mixtega Ángel Miguél</div>
    <div class="member">Plascencia Arevalo Alberto</div>
    <div class="member">Méndez Ortega Paula</div>
    <div class="member">Mota Barraza Moisés</div>
    <div class="member">Mendez Damián Brandon Efren</div>
  </div>

  <br>
  <a href="https://colab.research.google.com/drive/1nX9DHH1Ts1Y1LvaSJwoYT7Lzrs1dS6dc?usp=sharing">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab" style="box-shadow:none; margin:0; display:inline;">
  </a>
</div>

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
