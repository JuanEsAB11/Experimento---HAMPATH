# Estudio Experimental Comparativo de Algoritmos para el Problema del Camino Hamiltoniano

Este repositorio contiene las implementaciones, el arnés de experimentación y el informe final correspondientes al proyecto experimental de la materia **Análisis y Diseño de Algoritmos** (Universidad Nacional de Colombia, Sede Manizales, 2026).

El proyecto aborda el problema del **Camino Hamiltoniano (HAM-PATH)** —un conocido problema NP-completo— mediante cinco enfoques distintos: cuatro métodos exactos (Fuerza Bruta, Backtracking, Procedimiento de búsqueda de Rubin, Programación Dinámica) y uno heurístico/probabilístico (Monte Carlo con reinicios).

---

## 📂 Estructura del Proyecto

```text
proyecto-camino-hamiltoniano/
├── notebooks/
│   ├── Proyecto_Final_ADA.ipynb       # FASE 1: Implementaciones de algoritmos y suites de pruebas unitarias
│   └── Resultados_Experimento.ipynb   # FASE 2: Arnés experimental, recolección de métricas y graficación
├── resultados/
│   ├── resultados_crudos.csv          # Datos crudos recolectados de las 1155 corridas experimentales
│   ├── resumen_estadistico.csv        # Métricas agrupadas y procesadas estadísticamente con Pandas
│   └── entorno.json                   # Especificaciones de hardware y software del entorno experimental
├── figuras/                           # Figuras generadas por el análisis experimental (Formatos PNG/SVG)
├── informe/
│   └── informe_final.pdf              # Documento académico compilado en PDF
├── requirements.txt                   # Dependencias de Python necesarias para replicar el experimento
└── README.md                          # Instrucciones del procedimiento de experimentación y replicación
```

---

## 🛠️ Requisitos Previos e Instalación

El proyecto está diseñado y validado bajo **Python 3.13.3**. Para instalar todas las dependencias requeridas para la ejecución de los notebooks y la compilación del reporte, ejecute el siguiente comando en su terminal:

```bash
pip install -r requirements.txt
```

### Contenido de `requirements.txt`:
```text
networkx>=3.0
pandas>=2.0
matplotlib>=3.5
psutil>=5.9
numpy>=1.22
pytest>=7.0
ipytest>=0.13
weasyprint>=61.0
```

---

## ⚙️ Procedimiento de Experimentación y Replicación

Para replicar de manera exacta las mediciones, tablas y gráficas presentadas en el informe final, complete los siguientes pasos de manera secuencial:

### Paso 1: Validación de la Corrección (FASE 1)
1. Inicie su entorno de desarrollo (se recomienda **Visual Studio Code** con la extensión de Jupyter).
2. Abra el notebook `notebooks/Proyecto_Final_ADA.ipynb`.
3. Ejecute todas las celdas de este notebook. 
4. El notebook cargará los algoritmos y ejecutará automáticamente una suite de **pruebas unitarias** usando `pytest` e `ipytest` sobre grafos conocidos. La confirmación de que todas las pruebas pasaron con éxito garantiza que los algoritmos son lógicamente correctos antes de realizar las mediciones de rendimiento.

### Paso 2: Ejecución del Barrido Experimental (FASE 2)
1. Abra el notebook `notebooks/Resultados_Experimento.ipynb`.
2. Asegúrese de que el entorno sea un entorno local dedicado y estable (evite plataformas en la nube compartidas como Google Colab para medir tiempos reales estables).
3. Ejecute las celdas correspondientes a la **Fase de Generación de Datos** en orden:
   - Se registrará de forma automática la huella de hardware y software en `resultados/entorno.json`.
   - Se ejecutará el barrido experimental sobre el producto de: **5 Algoritmos** × **3 Tipos de Caso** (Mejor, Peor, Promedio) × **Tamaños de entrada $n$ crecientes** × **5 Réplicas independientes por tamaño**.
   - El arnés controlará el presupuesto mediante un límite automático de **5 segundos** de ejecución o topes de seguridad por algoritmo para evitar desbordes de memoria.
   - Las métricas de tiempo, operaciones básicas (consultas de adyacencia) y pico de memoria asignada (`tracemalloc`) se guardarán en `resultados/resultados_crudos.csv`.

### Paso 3: Análisis de Datos y Generación de Reportes
1. Continúe con la ejecución de las celdas finales de `notebooks/Resultados_Experimento.ipynb`.
2. El notebook leerá los datos crudos del CSV, computará agregaciones estadísticas (media, mediana, desviación estándar, modas) y los exportará a `resultados/resumen_estadistico.csv`.
3. Automáticamente se generarán y guardarán las **14 figuras comparativas** en la carpeta `figuras/`.

---

## 📊 Algoritmos Evaluados y Complejidad Teórica

| Algoritmo | Tipo de Enfoque | Complejidad Temporal (Peor Caso) | Complejidad Espacial (Peor Caso) | Recurso Limitante Práctico |
| :--- | :--- | :--- | :--- | :--- |
| **Fuerza Bruta** | Exacto Exhaustivo | $O(n \cdot n!)$ | $O(n)$ | Tiempo (Explosión factorial) |
| **Backtracking** | Exacto con Poda | $O(n \cdot n!)$ | $O(n)$ | Tiempo (En ausencia de solución) |
| **Procedimiento de Rubin** | Exacto Deductivo | $O((n+m) \cdot n!)$ | $O(n)$ | Tiempo (Sobrecarga de reglas) |
| **Held-Karp (Prog. Dinámica)** | Exacto con Memorización | $O(2^n \cdot n^2)$ | $O(2^n)$ | Espacio (Memoria Exponencial) |
| **Monte Carlo con Reinicios** | Probabilístico / Muestreo | $O(k(n+m))$ | $O(n)$ | Ninguno (Error de un solo lado) |

---

## 👥 Autores y Contacto
* **Juan Diego Ramírez Sánchez** - juaramirezs@unal.edu.co
* **Juan Esteban Agudelo Burgos** - juagudelobu@unal.edu.co
* **Profesor Guía:** Jairo Hernán Aponte Melo

*Universidad Nacional de Colombia, Sede Manizales — 2026*
