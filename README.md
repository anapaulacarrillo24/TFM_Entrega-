# Sistema de Gestión Predictiva y Dashboard Financiero de Activos Fijos (WMS)/
PythonFastAPIStreamlitMachine Learning

Este repositorio contiene el código fuente desarrollado para el Trabajo de Fin de Máster (TFM). El proyecto implementa un sistema predictivo impulsado por Inteligencia Artificial para el departamento de Skilled Trades del Austin Community College (ACC), permitiendo anticipar el fallo de equipos, calcular el riesgo financiero asociado y optimizar la logística del inventario.

## 1.- Arquitectura del Proyecto:
El sistema está diseñado bajo una arquitectura moderna y desacoplada, ideal para su despliegue en plataformas en la nube como Google Cloud Platform (GCP):

1.-Motor de Datos y Machine Learning: Limpieza de datos (Pandas), Entrenamiento del Modelo (Random Forest) y Segmentación (K-Means).
2.-Backend (API): Construido con FastAPI, actúa como el cerebro matemático que expone los endpoints de evaluación de riesgo.
3.-Frontend (Dashboard): Construido con Streamlit, ofrece una interfaz interactiva y visual para la toma de decisiones directivas sin requerir conocimientos técnicos. Estructura del Repositorio

## El flujo de trabajo técnico se divide en los siguientes scripts principales:
Archivo / Directorio	Descripción
etl_pipeline.py	Pipeline de Extracción, Transformación y Carga (ETL). Limpia los datos crudos y aplica Feature Engineering financiero.
ml_pipeline.py	Script de entrenamiento de los modelos predictivos (Random Forest y K-Means Clustering). Incluye prevención de Data Leakage.
api.py	Servidor backend en FastAPI. Procesa las solicitudes del cliente y devuelve cálculos de KPIs y semáforos de riesgo en formato JSON.
dashboard.py	Aplicación web interactiva en Streamlit. Es la "Cara" del sistema, mostrando métricas globales y la evaluación predictiva de equipos.
rf_model.pkl	Modelo de Random Forest entrenado y serializado, listo para usarse en producción.
wms_dataset_transformed.csv	Dataset procesado y codificado tras pasar por el pipeline ETL.

## Cómo ejecutar el proyecto localmente
Para revisar el funcionamiento del sistema en un entorno local, sigue estos pasos:

1. Requisitos Previos
Asegúrate de tener instaladas las siguientes librerías en tu entorno de Python
```bash
 pip install pandas scikit-learn fastapi uvicorn streamlit joblib

2. Iniciar el Backend (API Inteligente)
Abre una terminal, navega a la carpeta del repositorio y ejecuta el servidor de FastAPI:
*uvicorn api:app --host 0.0.0.0 --port 8000
(La API quedará corriendo en segundo plano, escuchando en el puerto 8000).

3. Iniciar el Frontend (Dashboard)
Abre una nueva terminal (sin cerrar la anterior), navega a la misma carpeta y ejecuta Streamlit
*streamlit run dashboard.py
Se abrirá automáticamente una ventana en tu navegador web mostrando el Dashboard Financiero.

Lógica de Negocio (El Semáforo Predictivo)
El sistema integra un algoritmo que evalúa cada activo basado en tres variables críticas:

##Probabilidad de Fallo (IA): Calculada en tiempo real.
Depreciación Consumida: Basada en la vida útil normativa (IRS/NIF).
Días Estancado: Días sin transferencia logística.
1.-ROJO (Crítico): Riesgo de fallo inminente (>70%) o vida útil agotada (>100%). Acción: Presupuestar reemplazo.
2.-AMARILLO (Alerta): Activo infrautilizado ("Zombi", >180 días estancado) o inicio de desgaste (>40%). Acción: Revisar o reasignar.
3.-VERDE (Saludable): Operación normal dentro de los márgenes óptimos de la institución
