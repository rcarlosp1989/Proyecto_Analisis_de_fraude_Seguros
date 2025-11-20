
# ⏱️ Análisis Temporal de Reclamos de Seguros  

### Proyecto SafeClaim — Propuesta 1

Este repositorio contiene el análisis exploratorio, de calidad de datos y análisis temporal aplicado al dataset PFDA_fraud_car.csv, con el objetivo de identificar patrones de fraude en reclamos de seguros de autos.
El análisis fue desarrollado en el notebook:

📄 Entregable_Final_Analisis_Tempora.ipynb
---

## 🎯 Objetivo del Proyecto

El objetivo principal es entender el comportamiento temporal del fraude, usando variables como:

- Día del accidente

- Día de la reclamación

- Mes del accidente

- Mes de la reclamación

- Diferencia temporal entre accidente → reclamación

- Patrones por tipo de vehículo

- Datos históricos presentes en la póliza

## El análisis incluye:

- Exploración inicial
- Calidad de datos
- Outliers
- Distribuciones
- Patrones de fraude
- 5 preguntas temporales clave
- Construcción del Índice de Riesgo Temporal (IRT)
- Reglas de negocio basadas en evidencia

## 📝 Dataset Utilizado

El dataset contiene características relacionadas con:

------------

- Edad del asegurado

- Edad del vehículo

- Tipo de vehículo

- Historial de reclamos

- Días entre póliza–accidente

- Meses y días de accidente y reclamación

- Información del reporte policial

- Variable objetivo: FraudFound (1 = fraude, 0 = legítimo)

------------
# 🔍 Metodología del Análisis

1. Importación y exploración inicial

## Incluye:
------------
- Visualización de primeras filas

- Tipos de datos

- Conteo de filas y columnas

- Identificación de columnas numéricas

- Estadísticas descriptivas
------------
## 2. Evaluación de calidad de datos
------------

- Registros duplicados

- Valores nulos

- Detección de outliers usando el método IQR

- Columnas con inconsistencias (especialmente edades = 0)

------------


## 3. Análisis de distribución

- Se evaluaron las variables más relevantes:

- Distribución de casos de fraude

- Edad de asegurados

- Categoría de vehículo

- Diferencias entre casos legítimos y fraudulentos

- Ejemplos incluidos en el notebook:

- Gráfico de distribución del fraude

- Histogramas de edad

- Boxplots por tipo de fraude

- Barras por categoría de vehículo

## 4.  Análisis de patrones temporales

El corazón del análisis responde 5 preguntas clave:

# 🧠 PREGUNTA 1:
## PREGUNTA 1: ¿Hay meses del año con mayor incidencia de fraude?

![Pregunta 1](https://github.com/user-attachments/assets/5ba841f6-cc7d-4c35-812b-95440a177d37)

## **Interpretacion:**

Los datos revelan un patron estacional de fraude:

- **Primer semestre (Ene-Jun):** Concentra el 87% de los fraudes
  - Marzo pico maximo: 12.56% de tasa de fraude
  - Q1 y Q2 tienen tasas >10%

- **Segundo semestre (Jul-Dic):** Casi libre de fraude
  - Q3 solo 0.44% de fraude (24 veces MENOR que Q1)
  - Septiembre y Octubre: 0% de fraude

- **Patron de reclamacion:** Los defraudadores reclaman inmediatamente
  - El heatmap muestra concentracion en la diagonal (mismo mes)
  - No esperan para reclamar, actuan rapido

## **Implicacion de Negocio:**
   Este patron no puede ser coincidencia. Sugiere comportamiento deliberado
   y planificado.Se recomienda reforzar controles en el primer semestre
   del año, especialmente en marzo-mayo.

------------
------------

# 🧠 PREGUNTA 2:

## PREGUNTA 2: ¿Hay días de la semana con mayor proporción de casos fraudulentos?

![Pregunta 2](https://github.com/user-attachments/assets/70506557-d6ef-4425-b5bb-ea17a981398f)

## **Interpretacion:**

Los datos revelan comportamiento RACIONAL por parte de los defraudadores:

### - **Accidentes:** Prefieren el DOMINGO (8.44% de fraude, el más alto)
  - Fin de semana: 7.55% vs Días laborales: 6.22%
  - Jueves es el día más seguro (4.94%)

### - **Reclamaciones:** IMPOSIBLES en fin de semana (0% sábado y domingo)
  - Las oficinas solo operan días laborales
  - Martes es el pico (7.87%) - acumulación post-fin de semana
  - Viernes también alto (7.67%) - antes del cierre semanal

### - **Patron de timing:** Los defraudadores NO reclaman el mismo día de la semana
  - Diferentes días: 7.01% de fraude
  - Mismo día: 4.64% (51% MENOS fraude)
  - Sugiere intento de evitar patrones detectables

### **Implicacion de Negocio:**
El patrón semanal es MENOS dramático que el mensual, pero muestra que
los defraudadores entienden las restricciones operativas y actúan en
consecuencia. Se recomienda monitoreo especial de accidentes dominicales
y reclamaciones de los martes.



# 🧠 PREGUNTA 3:
## PREGUNTA 3: ¿Cuál es la diferencia temporal entre el accidente y la reclamación en casos de fraude?

![Pregunta 3](https://github.com/user-attachments/assets/c8485855-263e-4901-b911-db8e26fc5ac5)
**Interpretacion:**

Los datos revelan un patron CONTRAINTUITIVO sobre la velocidad de reclamacion:

### - **Los fraudulentos reclaman MAS LENTO:**
  - Promedio fraude: 0.59 meses
  - Promedio legitimo: 0.38 meses
  - Diferencia: 55% mas tiempo (p < 0.001)

### - **Mismo mes = Menor riesgo:**
  - Tasa de fraude: 5.37% (la mas baja)
  - Las victimas reales reclaman INMEDIATAMENTE

### - **Esperar 2-3 meses = Maximo riesgo:**
  - Tasa de fraude: 11.04% (mas del DOBLE que mismo mes)
  - Los defraudadores esperan estrategicamente

### - **Diferente mes vs Mismo mes:**
  - Diferente: 9.64% de fraude
  - Mismo: 5.37% de fraude (80% MENOS)

### **Implicacion de Negocio:**
Este hallazgo contradice el mito de que "reclamaciones rapidas son sospechosas".
La realidad es OPUESTA: las reclamaciones inmediatas son mas legitimas.
Los defraudadores muestran comportamiento calculado, esperando 1-3 meses
para evitar parecer urgentes. Se recomienda invertir la logica de alertas
y enfocar investigaciones en reclamaciones DIFERIDAS, no inmediatas.


# 🧠 PREGUNTA 4:
## PREGUNTA 4: ¿Los patrones temporales identifican banderas rojas para deteccion temprana?
![Pregunta 4](https://github.com/user-attachments/assets/3b39656d-6942-4c92-b551-8a865341d974)
**Interpretacion:**

El Indice de Riesgo Temporal (IRT) demuestra ser una herramienta
ALTAMENTE efectiva para deteccion temprana de fraude:

### - **Escalera de riesgo perfecta:**
  - Bajo: 1.28% (5x MENOS que promedio)
  - Muy Alto: 17.27% (2.6x MAS que promedio)
  - Contraste: 13.5x de diferencia

### - **Eficiencia comprobada:**
  - Con solo 22.9% de casos (Alto/Muy Alto)
  - Se captura 47.4% de todos los fraudes
  - ROI: 2x (el doble de rendimiento)

### - **Recall: 47%** - Capturamos casi la MITAD de fraudes
  revisando menos de la CUARTA PARTE de casos

### **Implicacion de Negocio:**
El IRT permite priorizar investigaciones de forma inteligente,
concentrando recursos donde realmente esta el fraude. Con solo
5 factores temporales simples, logramos identificar casos de
alto riesgo con precision suficiente para reducir workload en 77%
mientras mantenemos capacidad de deteccion del 47%.

Se recomienda implementacion inmediata del IRT como sistema de
scoring para clasificacion automatica de reclamaciones en:
- Verde (Bajo): Procesamiento automatico
- Amarillo (Medio): Validacion estandar
- Rojo (Alto/Muy Alto): Investigacion profunda prioritaria
  
# 🧠 PREGUNTA 5:
## PREGUNTA 5: ¿El tipo de vehículo también influye en el IRT?

![Pregunta 5](https://github.com/user-attachments/assets/b08fea36-5a1b-443e-bafa-fca3470ef354)

## **TOP 5 COMBINACIONES MAS RIESGOSAS (Vehiculo + IRT)**

| VehicleCategory | Risk_Category | Fraud_Count | Total | Fraud_Rate_Pct |
|-----------------|---------------|-------------|--------|-----------------|
| Sedan           | Muy Alto      | 36          | 157    | 22.929936       |
| Sedan           | Alto          | 88          | 528    | 16.666667       |
| Utility         | Medio         | 6           | 45     | 13.333333       |
| Utility         | Alto          | 2           | 18     | 11.111111       |
| Sedan           | Medio         | 108         | 1032   | 10.465116       |

## **TOP 5 COMBINACIONES MAS SEGURAS (Vehiculo + IRT)**

| VehicleCategory | Risk_Category | Fraud_Count | Total | Fraud_Rate_Pct |
|-----------------|---------------|-------------|--------|-----------------|
| Sport           | Bajo          | 0           | 633    | 0.000000        |
| Utility         | Muy Alto      | 0           | 3      | 0.000000        |
| Utility         | Bajo          | 1           | 55     | 1.818182        |
| Sedan           | Bajo          | 21          | 1032   | 2.034884        |
| Sport           | Medio         | 15          | 591    | 2.538071        |

## CONCLUSION: 
 - Hay RELACION significativa entre tipo de vehiculo e IRT
  (p < 0.05, rechazamos hipotesis de independencia)

## 📊 Conclusiones:

- El análisis temporal permitió identificar patrones claros asociados al fraude, mostrando que ciertos días,secuencias y tiempos inesperados elevansignificativamente el riesgo.
- El IRT sintetiza estas dimensiones temporales ydistingue con precisión los casos más sospechosos,permitiendo separar reclamos de bajo riesgo deaquellos que requieren 
  revisión inmediata.
- Integrar variables temporales con características delsiniestro y del vehículo mejora la detección temprana sinnecesidad de modelos complejos.

## **EST CHI-CUADRADO: INDEPENDENCIA VEHICULO vs IRT**

- Chi-cuadrado: 20.3703
- p-value: 0.002379
- Grados de libertad: 6
  
##   Recomendaciones:

- Usar el IRT para priorizar los reclamos conmayor riesgo.
- Automatizar la revisión de casos de bajoriesgo.
- Reforzar la investigación en reclamos conpatrones temporales sospechosos.
- Capacitar al equipo en detección tempranabasada en tiempos y secuencias.Mantener un monitoreo continuo de lospatrones temporales para ajustar estrategias.
