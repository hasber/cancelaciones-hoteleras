# Proyecto 1 · ¿Podemos anticipar las cancelaciones hoteleras?

Análisis y clasificación con la metodología CRISP-DM sobre el dataset público *Hotel Booking Demand* (119.390 reservas de dos hoteles, llegadas entre julio de 2015 y agosto de 2017).

Integrantes: Hasber Gonzalo Malpica · Carlos Andrés Restrepo · Juan Carlos Monterrosa

## Preguntas
1. ¿Qué tienen en común las reservas que más se cancelan?
2. ¿Podemos anticipar las cancelaciones?

Variable objetivo: `is_canceled` (1 = cancelada, 0 = no cancelada). Problema de clasificación binaria.

## Contenido

| Archivo | Qué es |
|---|---|
| `Notebook_Analisis_CRISP_DM_Hotel.ipynb` | Notebook ejecutado: comprensión del negocio, comprensión de los datos, preparación, modelado, evaluación y conclusiones |
| `resultados_crispdm/` | Tablas que exporta el notebook: particiones, comparación de modelos, evaluación en prueba, regla básica, escenarios de seguimiento, perfiles e importancias |
| `presentacion/Presentacion_CRISP_DM_Hotel.pptx` | Presentación de la sustentación (16 diapositivas, 20 minutos) |
| `hotel_bookings.csv` | Datos originales |

## Resultados en breve
- La tasa de cancelación crece con la anticipación: de 9,6 % en reservas hechas con 0–7 días a 67,7 % con más de 365 días. Es mucho mayor en clientes con cancelaciones previas (91,6 %), en el segmento Groups (61,1 %) y en el City Hotel (41,7 %). Son asociaciones observadas, no causas.
- Se separaron los datos por fecha prevista de llegada: entrenamiento hasta junio de 2016 (49.157 reservas), validación segundo semestre de 2016 (29.546) y prueba 2017 (40.687). Se compararon regresión logística, árbol de decisión y Random Forest; Random Forest obtuvo el mejor F1 de validación (0,611) con umbral 0,25.
- En prueba: F1 0,624, recall 89,25 %, precisión 47,99 %, ROC-AUC 0,699. Detecta 14.052 de 15.745 cancelaciones, pero genera 15.229 falsas alertas.
- Una regla básica que siempre predice "no se cancela" tiene más exactitud (61,3 % frente a 58,4 %) pero no detecta ninguna cancelación; por eso el modelo no se elige por exactitud.
- Si el hotel solo pudiera revisar el 10 % de reservas de mayor riesgo, encontraría el 17 % de las cancelaciones con una tasa de acierto del 67 %.

## Cómo ejecutar

```bash
pip install -r requirements.txt
```

Abrir `Notebook_Analisis_CRISP_DM_Hotel.ipynb` con Jupyter o VS Code y ejecutarlo desde la primera celda, con `hotel_bookings.csv` en la misma carpeta. Semilla 42; el notebook escribe las tablas en `resultados_crispdm/`.
