# Instrucciones para la Clase Práctica de Data Science
## Neurodiplomatura - Análisis de Estrés en Estudiantes

### Materiales Creados

📁 **Archivos disponibles:**
- `Clase_Practica_DataScience_EJERCICIOS.ipynb` - Notebook para estudiantes con ejercicios a completar
- `Clase_Practica_DataScience_SOLUCIONES.ipynb` - Notebook completo con todas las soluciones
- `INSTRUCCIONES_CLASE_PRACTICA.md` - Este documento

---

## 🎯 Objetivos de la Clase (3 horas)

Los estudiantes aprenderán a:
1. **Cargar y explorar** un dataset real de Kaggle
2. **Analizar datos descriptivamente** usando pandas
3. **Crear visualizaciones** informativas con matplotlib/seaborn
4. **Calcular correlaciones** entre variables psicológicas
5. **Aplicar pruebas estadísticas** básicas (t-test)
6. **Construir modelos predictivos** de regresión múltiple
7. **Identificar predictores** clave del estrés estudiantil
8. **Interpretar resultados** y extraer conclusiones prácticas

---

## 📋 Estructura de la Clase

### **BLOQUE 1: Configuración inicial (20 min)**
- Abrir Google Colab o Jupyter
- Cargar el notebook de ejercicios
- Ejecutar las celdas de importación de librerías
- Descargar el dataset usando kagglehub

### **BLOQUE 2: Exploración de datos (40 min)**
- **Ejercicios 1-4**: Carga, exploración inicial, estadísticas descriptivas
- **Puntos clave a remarcar:**
  - Importancia de entender los datos antes de analizarlos
  - Verificación de valores faltantes
  - Interpretación de variables psicológicas (estrés, GPA, horas de sueño)

### **BLOQUE 3: Visualización (40 min)**
- **Ejercicios 5-6**: Boxplots comparativos y matriz de correlación
- **Puntos clave a remarcar:**
  - Cómo los gráficos revelan patrones no visibles en tablas
  - Interpretación de boxplots para comparar grupos
  - Importancia de la visualización en psicología

### **BLOQUE 4: Estadística inferencial (40 min)**
- **Ejercicios 7-8**: Prueba t y regresión simple
- **Puntos clave a remarcar:**
  - Diferencia entre correlación y causalidad
  - Interpretación de valores p
  - Relevancia clínica vs. significancia estadística

### **BLOQUE 5: Modelado predictivo (60 min)**
- **Ejercicios 9-11**: Regresión múltiple para predecir estrés
- **Puntos clave a remarcar:**
  - Conversión de variables categóricas a numéricas
  - Interpretación de coeficientes de regresión
  - R² como medida de ajuste del modelo
  - Identificación de predictores más importantes

### **BLOQUE 6: Reflexión y conclusiones (20 min)**
- **Ejercicio 12**: Síntesis e interpretación de resultados
- **Puntos clave a remarcar:**
  - Integración de todos los análisis realizados
  - Aplicación práctica de los hallazgos
  - Limitaciones y próximos pasos

---

## 🔧 Configuración Técnica

### **Opción 1: Google Colab (Recomendada)**
```python
# Los estudiantes deben ejecutar esto primero:
!pip install kagglehub
```

### **Opción 2: Entorno local**
```bash
pip install pandas matplotlib seaborn scipy statsmodels kagglehub
```

---

## 📚 Dataset: Student Lifestyle & Stress

**Variables incluidas:**
- `Study_Hours_Per_Day`: Horas de estudio diarias
- `Sleep_Hours_Per_Day`: Horas de sueño diarias
- `Physical_Activity_Hours_Per_Day`: Horas de ejercicio diarias
- `Social_Hours_Per_Day`: Horas sociales diarias
- `Extracurricular_Hours_Per_Day`: Horas de actividades extra
- `GPA`: Promedio académico (1.0-4.0)
- `Stress_Level`: Nivel de estrés (Low, Moderate, High)

**¿Por qué este dataset?**
- Variables relevantes para psicólogos
- Tamaño manejable (2000 observaciones)
- Conceptos aplicables a bienestar estudiantil
- Resultados interpretables clínicamente

---

## 🎓 Estrategias Pedagógicas

### **Para estudiantes con dificultades:**
1. **Emparéjalos** con estudiantes más avanzados
2. **Enfócate en interpretación** más que en código
3. **Usa analogías** psicológicas para conceptos estadísticos
4. **Permite copiar código** pero exige explicación de resultados

### **Para estudiantes avanzados:**
1. **Propón análisis adicionales:** 
   - ANOVA entre los 3 grupos de estrés
   - Regresión logística ordinal
   - Análisis de subgrupos (ej: por género si estuviera disponible)
   - Validación cruzada del modelo predictivo
2. **Interpretación crítica:** Limitaciones del estudio
3. **Aplicación clínica:** ¿Cómo usarían estos resultados?

### **Gestión del tiempo:**
- **Flexibilidad:** Algunos grupos irán más rápido
- **Puntos de control:** Cada 30 min, verificar progreso general
- **Ayuda focalizada:** Circular por el aula constantemente
- **Prioridades:** Si van lento, asegurar que lleguen al modelo predictivo

---

## 🔍 Respuestas Esperadas a los Ejercicios

### **Ejercicio 1:** 
```python
df = pd.read_csv(path + '/student_lifestyle_dataset.csv')
```

### **Ejercicio 2:**
```python
df.head()
df.info()
print(f"El dataset tiene {df.shape[0]} filas y {df.shape[1]} columnas")
```

### **Ejercicio 3:**
```python
df.describe()
df['Stress_Level'].value_counts()
```

### **Ejercicio 4:**
```python
df.groupby('Stress_Level').mean().round(2)
```

### **Ejercicio 5:**
```python
sns.boxplot(data=df, x='Stress_Level', y='Study_Hours_Per_Day', ax=axes[0])
sns.boxplot(data=df, x='Stress_Level', y='Sleep_Hours_Per_Day', ax=axes[1])
```

### **Ejercicio 6:**
```python
correlation_matrix = df[numeric_vars].corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
```

### **Ejercicio 7:**
```python
high_stress = df[df['Stress_Level'] == 'High']['Study_Hours_Per_Day']
low_stress = df[df['Stress_Level'] == 'Low']['Study_Hours_Per_Day']
t_stat, p_value = stats.ttest_ind(high_stress, low_stress)
```

### **Ejercicio 8:**
```python
sns.regplot(data=df, x='Study_Hours_Per_Day', y='GPA')
correlation = df['Study_Hours_Per_Day'].corr(df['GPA'])
```

### **Ejercicio 9:** 
```python
stress_mapping = {'Low': 1, 'Moderate': 2, 'High': 3}
df['Stress_Score'] = df['Stress_Level'].map(stress_mapping)
```

### **Ejercicio 10:**
```python
formula = "Stress_Score ~ Study_Hours_Per_Day + Sleep_Hours_Per_Day + Physical_Activity_Hours_Per_Day + Social_Hours_Per_Day + Extracurricular_Hours_Per_Day + GPA"
stress_model = ols(formula, data=df).fit()
```

---

## 🧠 Conceptos Clave para Reforzar

### **Estadística Descriptiva:**
- Media vs. mediana en datos psicológicos
- Desviación estándar como medida de variabilidad
- Percentiles y su interpretación clínica

### **Visualización:**
- Boxplots: mediana, cuartiles, outliers
- Scatterplots: relaciones lineales
- Heatmaps: matrices de correlación

### **Inferencia Estadística:**
- Valor p: probabilidad de error tipo I
- Tamaño del efecto vs. significancia estadística
- Limitaciones de las pruebas estadísticas

### **Regresión Múltiple:**
- Interpretación de coeficientes
- R² como medida de ajuste
- Variables predictoras vs. variables confusoras
- Importancia relativa de predictores

### **Interpretación Psicológica:**
- Correlación ≠ causalidad
- Variables confusoras en estudios observacionales
- Relevancia clínica de los hallazgos
- Aplicación práctica de modelos predictivos

---

## ⚠️ Problemas Comunes y Soluciones

### **Error técnico:** Kagglehub no funciona
**Solución:** Subir el CSV manualmente a Colab

### **Error conceptual:** "¿Un coeficiente positivo significa que la variable es buena o mala?"
**Explicación:** Depende de la variable dependiente. En este caso, coeficiente positivo = aumenta el estrés

### **Error de interpretación:** "El modelo explica el 60% del estrés, ¿qué pasa con el otro 40%?"
**Explicación:** Hay otros factores no medidos (genética, personalidad, eventos externos, etc.)

### **Error de código:** Estudiantes confundidos con la conversión categórica
**Estrategia:** Mostrar ejemplo paso a paso, explicar el mapeo

### **Ritmo muy lento**
**Adaptación:** Priorizar llegar al modelo predictivo, saltar análisis intermedios si es necesario

---

## 📝 Evaluación Formativa

### **Preguntas para verificar comprensión:**

1. **Descriptiva:** "¿Qué nos dice la media de horas de estudio por grupo de estrés?"
2. **Visualización:** "¿Qué patrón ven en este boxplot?"
3. **Correlación:** "Esta correlación de 0.3, ¿es fuerte o débil? ¿Qué significa?"
4. **Estadística:** "El valor p es 0.02, ¿qué concluimos?"
5. **Regresión:** "Este coeficiente es -0.15 para horas de sueño, ¿cómo lo interpretamos?"
6. **Modelo:** "El R² es 0.65, ¿qué nos dice sobre nuestro modelo?"
7. **Aplicación:** "¿Cómo usarían estos resultados para aconsejar a un estudiante estresado?"

### **Indicadores de éxito:**
- Estudiantes pueden interpretar gráficos básicos
- Comprenden diferencia entre correlación y causalidad  
- Pueden explicar coeficientes de regresión en términos psicológicos
- Entienden el concepto de modelo predictivo
- Muestran curiosidad por explorar más datos

---

## 🚀 Extensiones Avanzadas (si hay tiempo)

1. **Validación del modelo:** División train/test para evaluar predicciones
2. **Regresión logística ordinal:** Modelar directamente las categorías de estrés
3. **Análisis de residuos:** Verificar supuestos del modelo
4. **Variables de interacción:** ¿El efecto del estudio depende del sueño?
5. **Análisis de clusters:** ¿Hay perfiles típicos de estudiantes?

---

## 📞 Contacto y Soporte

**Durante la clase:**
- Circular constantemente por el aula
- Usar el notebook de soluciones como referencia
- No dudar en simplificar si el grupo va lento
- **PRIORIDAD:** Que entiendan el modelo predictivo y su interpretación

**Después de la clase:**
- Los estudiantes pueden contactar por email para dudas
- Subir ambos notebooks a la plataforma del curso
- Considerar tarea opcional de análisis adicional con otros predictores

---

## ✅ Checklist Pre-Clase

- [ ] Verificar que Google Colab está disponible
- [ ] Probar descarga del dataset con kagglehub
- [ ] Revisar el notebook de ejercicios
- [ ] Preparar ejemplos de interpretación de coeficientes
- [ ] Tener datos alternativos por si falla la descarga
- [ ] Repasar conceptos de regresión múltiple
- [ ] Preparar respuestas sobre interpretación de R²
- [ ] Revisar cómo explicar la conversión de variables categóricas

## 🎯 Mensajes Clave de la Clase

1. **Los datos nos permiten entender patrones complejos** que no son obvios a simple vista
2. **Los modelos predictivos nos ayudan a identificar** qué factores son más importantes
3. **En psicología, el equilibrio es clave** - rara vez hay una sola causa de un problema
4. **La data science es una herramienta poderosa** para la investigación y práctica psicológica
5. **Los resultados deben interpretarse con cuidado** considerando limitaciones y contexto

¡Que tengas una excelente clase! 🎓📊🧠 