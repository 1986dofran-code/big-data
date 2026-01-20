Detección de Anomalías en Datos de Taxis NYC

De qué trata este proyecto?

Este es un proyecto personal que desarrollé para aprender Big Data y Machine Learning. Tomé datos reales de taxis amarillos de Nueva York (3.4 millones de viajes) y construí un sistema automático que detecta viajes sospechosos y anómalos.

Lo que hace el proyecto:

Lee archivos enormes de datos de viajes
Limpia los datos y se deshace de errores
Crea nuevas variables útiles (features)
Usa un algoritmo de Machine Learning para detectar anomalías
Analiza cuál es el impacto económico
Explica qué significa cada predicción

Cómo está organizado

trabajo.big data/
├── Data/
│   ├── Raw/
│   │   └── yellow_tripdata_2025-01.parquet
│   └── processed/
│       ├── trips_features_2025-01.parquet
│       └── trips_with_ml_risk.parquet
├── 02_big_data_eda.ipynb
├── 03_feature_engineering.ipynb
├── 04_modeling_ml.ipynb
├── 05_evaluation_business_impact.ipynb
├── 06_model_explainability.ipynb
├── reports/
└── README.md

Cómo funciona (paso a paso)

Paso 1: Exploración de Datos

Primero, exploré los datos para entender qué tenía:
- 3,475,226 viajes
- 7 columnas: fecha pickup, fecha dropoff, distancia, tarifa, monto total, pasajeros, tipo de pago
- Busqué datos faltantes, duplicados o raros

Resultado: Encontré 0 duplicados, pero había algunos registros con datos inconsistentes

Paso 2: Crear Nuevas Variables (Features)

Convertí los datos básicos en información más útil:

Variables de Tiempo:
- Cuánto tiempo duró el viaje (en minutos)
- A qué hora fue
- Qué día de la semana
- Si fue fin de semana

Variables de Costo:
- Cuánto costó por kilómetro
- Cuánto costó por minuto
- Qué porcentaje era tarifa vs otros cobros

Alertas de Riesgo (Flags):
- Viaje muy corto (< 0.5 km)
- Viaje muy largo (> 30 km)
- Viaje muy rápido (< 2 minutos)
- Muy corto pero muy caro (< 1 km pero > $50)
- Viaje muy largo (> 2 horas)
- Pago en efectivo

Score de Riesgo Personal:
Creé una puntuación de 0-10 para cada viaje:
- 0 puntos: base
- +1 por cada alerta activada
- +1 si es pago en efectivo
- +1 si es madrugada
- +2 si es fin de semana

Números finales:
- Entré con: 3,475,226 viajes
- Salí con: 3,328,229 viajes válidos
- Creé: 27 nuevas variables
- Eliminé: 147,997 viajes con datos inconsistentes (4.3%)

Paso 3: Entrenar el Modelo de IA

Usé un algoritmo llamado Isolation Forest (Bosque de Aislamiento):

Por qué este algoritmo?
- Es rápido para millones de datos
- No necesita "respuestas correctas" para aprender
- Busca lo que es diferente del patrón normal
- Maneja bien datos complejos

Cómo lo entrené:
- Usé 8 variables importantes: distancia, duración, monto total, costo/km, costo/minuto, ratio tarifa, pasajeros, score de riesgo
- Escalé los datos para que estuvieran en el mismo rango
- Pedí al modelo que busque ~3% de anomalías

Lo que predice:
- Viaje normal - 97% de los viajes
- Viaje anómalo - 3% de los viajes

Paso 4: Análisis de Impacto

Preguntas que respondí:
- Cuántos viajes eran anómalos?
- Cuánto dinero afectaban?
- A qué horas del día eran más comunes?
- Viernes/sábado vs resto de la semana?

Paso 5: Explicabilidad

Aquí expliqué por qué el modelo clasifica algo como anómalo

Lo que encontré

Números principales:
- Viajes analizados: 3,328,229
- Viajes normales: 3,228,383 (97%)
- Viajes anómalos: 99,846 (3%)

Ejemplos de anomalías detectadas:
1. Viajes de 5 minutos por $100+ (claramente raro)
2. Trayectos de 0 km pero cobrando dinero
3. Viajes de 2 minutos (no da tiempo para nada)
4. Patrones sospechosos en ciertos horarios

Información sobre los datos:
- Datos sin duplicados
- Tipos de datos correctos
- Errores corregidos
- Lógica validada

Tecnologías que usé

- Python - El lenguaje de programación
- Pandas - Para manipular y analizar datos
- NumPy - Para matemáticas rápidas
- Scikit-learn - Para Machine Learning
- Jupyter Notebooks - Para escribir código interactivo

Cómo ejecutar esto

1. Preparar el entorno

python -m venv .venv

.venv\Scripts\activate

pip install pandas numpy scikit-learn jupyter

2. Abrir y correr los notebooks

jupyter notebook

Luego abre en este orden:
1. 02_big_data_eda.ipynb
2. 03_feature_engineering.ipynb
3. 04_modeling_ml.ipynb
4. 05_evaluation_business_impact.ipynb
5. 06_model_explainability.ipynb

3. Archivos generados

- trips_features_2025-01.parquet - Datos con las nuevas variables
- trips_with_ml_risk.parquet - Datos finales con predicciones

Resultados Finales

Distribución de Riesgo:
- Bajo: Viajes normales sin alertas (mayoría)
- Medio: Algunos flags de riesgo pero no es urgente
- Alto: Múltiples alertas, requiere atención

Lo que se puede hacer con esto:
- Alertar al taxista si algo raro pasa
- Investigar si hay fraude
- Entender qué zonas y horas tienen más anomalías
- Entrenar conductores sobre viajes seguros
- Hacer reportes para la gerencia

Lo que aprendí

- Cómo trabajar con datos enormes
- Cómo limpiar datos "sucios"
- Cómo crear variables útiles
- Cómo entrenar un modelo de Machine Learning
- Cómo medir si funciona bien
- Cómo explicar predicciones de IA

Notas importantes

- El modelo busca ~3% de anomalías (pueden ajustarse)
- Los datos son de enero 2025
- Sería ideal actualizar el modelo cada mes con nuevos datos
- Algunas "anomalías" podrían ser casos legítimos (hay que revisar manualmente)

Preguntas?

Si hay algo que no entiendas, revisa los comentarios dentro de cada notebook - están explicados paso a paso.

Proyecto personal de Big Data & Machine Learning
