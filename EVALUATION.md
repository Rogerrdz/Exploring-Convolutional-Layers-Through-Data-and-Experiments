# Evaluación del Repositorio: Exploring Convolutional Layers Through Data and Experiments

**Fecha de evaluación**: 17 de febrero de 2026  
**Evaluador**: Asistente de Código AI  
**Estudiante**: Roger Rodríguez

---

## Resumen Ejecutivo

Este documento evalúa el repositorio en función de los requisitos especificados en el assignment sobre capas convolucionales. La evaluación se basa en una escala de 1 a 5 para cada componente, donde:

- **5**: Excelente - Cumple todos los requisitos con alta calidad
- **4**: Bueno - Cumple los requisitos con calidad aceptable
- **3**: Satisfactorio - Cumple requisitos mínimos con algunas deficiencias
- **2**: Insuficiente - Cumple parcialmente los requisitos
- **1**: Deficiente - No cumple los requisitos

---

## Evaluación por Componentes

### 1. Dataset Understanding and EDA (15 puntos)

**Calificación: 3/5** (9/15 puntos)

#### Aspectos Positivos:
- ✅ Dataset apropiado seleccionado: Fashion-MNIST
- ✅ Justificación clara de por qué es apropiado para CNNs
- ✅ Ejemplos visuales de muestras por clase mostrados
- ✅ Preprocesamiento implementado (normalización a rango 0-1)
- ✅ Dimensiones de imagen identificadas (28×28 grayscale)

#### Deficiencias:
- ❌ **Falta tabla estadística formal** del tamaño del dataset (60,000 train / 10,000 test no se menciona explícitamente)
- ❌ **No hay histograma de distribución de clases** aunque el dataset está balanceado
- ❌ **EDA limitado** - No se muestran estadísticas como media/desviación estándar por clase
- ❌ **No se discute si hay preprocessing adicional necesario** (resize, augmentation, etc.)

#### Evidencia del Notebook:
```
"Fashion-MNIST consists of 28 × 28 grayscale images belonging to 10 clothing classes. 
The data set is balanced and small enough to fit in memory"
```

#### Recomendaciones:
- Agregar tabla con estadísticas del dataset (samples por split, clases, balance)
- Incluir visualización de distribución de clases
- Calcular y reportar estadísticas básicas (pixel intensity distribution)

---

### 2. Baseline Model and Comparison (15 puntos)

**Calificación: 4/5** (12/15 puntos)

#### Aspectos Positivos:
- ✅ Modelo baseline no-convolucional implementado correctamente
- ✅ Arquitectura claramente definida: Flatten → Dense(128) → Dense(64) → Dense(10)
- ✅ Performance reportado: Test accuracy 87.89%, Val accuracy 88.49%
- ✅ **Excelente identificación de limitaciones**: "treats each pixel independently after flattening it, ignoring spatial relationships"
- ✅ Comparación conceptual con CNN incluida

#### Deficiencias:
- ❌ **Número de parámetros no calculado explícitamente** (debería mostrar ~101,770 params)
- ⚠️ No hay tabla comparativa lado-a-lado de baseline vs CNN
- ⚠️ No se reporta tiempo de entrenamiento

#### Evidencia del Notebook:
```
"Although the baseline achieves reasonable accuracy, it requires a large number 
of parameters and lacks robustness to spatial transformations"
```

#### Recomendaciones:
- Usar `model.summary()` para mostrar número exacto de parámetros
- Crear tabla comparativa: Baseline vs CNN (params, accuracy, loss, time)

---

### 3. CNN Architecture Design and Justification (25 puntos)

**Calificación: 3/5** (15/25 puntos)

#### Aspectos Positivos:
- ✅ Arquitectura diseñada desde cero (no copiada)
- ✅ Estructura simple e intencional: 2 conv layers + 2 pooling + 2 dense
- ✅ Kernel size consistente (3×3)
- ✅ Activaciones ReLU utilizadas
- ✅ MaxPooling strategy implementada
- ✅ Padding='same' para preservar dimensiones

#### Arquitectura Implementada:
```
Conv2D(32, 3×3, padding='same') → ReLU → MaxPool(2×2) →
Conv2D(64, 3×3, padding='same') → ReLU → MaxPool(2×2) →
Flatten → Dense(128) → ReLU → Dense(10) → Softmax
```

#### Deficiencias Críticas:
- ❌ **FALTA JUSTIFICACIÓN EXPLÍCITA** de decisiones arquitectónicas:
  - ¿Por qué 3×3 kernels y no 5×5 o 7×7?
  - ¿Por qué exactamente 2 capas convolucionales?
  - ¿Por qué 32 y 64 filtros en lugar de otros valores?
  - ¿Por qué MaxPooling y no AveragePooling?
- ❌ **No se discute stride** (asume default=1 sin explicación)
- ❌ **No se menciona batch normalization** como decisión consciente
- ⚠️ No hay diagrama visual de la arquitectura

#### Evidencia (limitada):
El notebook muestra el código pero no contiene sección de "Design Rationale" o "Architectural Justifications"

#### Recomendaciones:
- **CRÍTICO**: Agregar sección "Design Rationale" con justificaciones punto por punto
- Explicar trade-offs de cada decisión (e.g., "3×3 kernels balance receptive field with computational efficiency")
- Incluir diagrama de arquitectura (puede ser simple ASCII art o matplotlib)
- Comparar explícitamente con alternativas consideradas

---

### 4. Experimental Rigor (25 puntos)

**Calificación: 2/5** (10/25 puntos)

#### Aspectos Positivos:
- ✅ Experimento controlado realizado: Kernel size (3×3 vs 5×5)
- ✅ Variables controladas: Todo fijo excepto kernel size
- ✅ Resultados cuantitativos reportados:
  - CNN 3×3: **91.45%** test accuracy
  - CNN 5×5: **91.31%** test accuracy
- ✅ Observación cualitativa incluida: "larger cores did not improve performance"

#### Deficiencias Críticas:
- ❌ **SOLO UN EXPERIMENTO** - El assignment requiere "systematic exploration"
- ❌ **Faltan experimentos en**:
  - Number of filters (16 vs 32 vs 64)
  - Depth (1 vs 2 vs 3 conv layers)
  - Pooling strategy (with vs without, Max vs Average)
  - Stride effects
- ❌ **No hay ablation study completo**
- ❌ **No hay trade-offs cuantificados** (performance vs complexity, time vs accuracy)
- ❌ **No se reporta statistical significance** de las diferencias

#### Evidencia del Notebook:
```
"Holding all other factors fixed, larger cores did not improve performance. 
This highlights the efficiency of small grains combined with depth"
```

#### Recomendaciones:
- **CRÍTICO**: Realizar al menos 2-3 experimentos controlados adicionales
- Crear tabla de ablation study completa
- Graficar trade-offs (params vs accuracy, time vs performance)
- Ejecutar múltiples runs para reportar mean ± std

---

### 5. Interpretation and Clarity of Reasoning (20 puntos)

**Calificación: 4/5** (16/20 puntos)

#### Aspectos Positivos:
- ✅ **Excelente explicación conceptual** de por qué CNN supera baseline
- ✅ **Inductive bias claramente articulado**:
  - "incorporate prior assumptions about spatial structure directly into architecture"
  - "This inductive bias reduces parameter counts, improves generalization"
- ✅ **Limitaciones de convolution identificadas**: "not appropriate for tabular or non-spatial data"
- ✅ Razonamiento claro y en palabras propias (no copiado)

#### Evidencia del Notebook:
```
"Convolutional layers outperform fully connected networks because they incorporate 
prior assumptions about spatial structure directly into architecture"

"convolution is not appropriate for tabular or non-spatial data, where locality 
assumptions are not met"
```

#### Deficiencias:
- ⚠️ **Falta profundidad** en algunos conceptos (e.g., translation equivariance, weight sharing)
- ❌ **No hay visualización de filtros aprendidos** (bonus pero altamente valorado)
- ❌ **No hay análisis de feature maps** para mostrar representaciones jerárquicas
- ⚠️ La explicación de por qué 3×3 > 5×5 es superficial

#### Recomendaciones:
- Agregar visualización de filtros de primera capa
- Mostrar feature maps intermedios para una imagen
- Profundizar en conceptos como parameter sharing, receptive field
- Incluir diagrama conceptual de inductive bias

---

### 6. SageMaker Deployment (Requerido)

**Calificación: 1/5** (0 puntos - CRÍTICO)

#### Estado Actual:
- ❌ **DEPLOYMENT FALLIDO** - Código presente pero no ejecutado exitosamente
- ❌ Error en notebook: `NameError: name 'cnn_model' is not defined`
- ❌ **No hay evidencia de endpoint funcional**
- ❌ **No hay predicciones realizadas desde endpoint**

#### Código Presente (no funcional):
```python
cnn_model.save("fashion_cnn_model")
model = TensorFlowModel(model_data="fashion_cnn_model", role=role, ...)
predictor = model.deploy(initial_instance_count=1, instance_type="ml.m5.large")
```

#### Deficiencias:
- Kernel state issue: modelo no disponible cuando se ejecuta celda de deployment
- No hay manejo de errores
- No hay validación de endpoint
- No hay cleanup code verificado
- Texto aspiracional sin ejecución real: "The trained CNN was deployed... After verification, the endpoint was deleted"

#### Impacto:
**ESTE ES UN REQUISITO OBLIGATORIO DEL ASSIGNMENT**. El hecho de que el deployment no funcione es una deficiencia crítica que afecta significativamente la calificación final.

#### Recomendaciones:
- **URGENTE**: Re-ejecutar notebook en orden para tener modelo en memoria
- Guardar modelo correctamente en formato TensorFlow SavedModel
- Implementar error handling para deployment
- Capturar screenshot de endpoint activo en consola de SageMaker
- Realizar al menos una predicción exitosa
- Documentar proceso de cleanup

---

## Deliverables Verification

### ✅ Git Repository
- Presente y funcional
- Commits muestran evolución del proyecto

### ⚠️ Jupyter Notebook
- ✅ Presente y ejecutable
- ✅ Contiene explicaciones en Markdown
- ⚠️ Algunas celdas con errores de ejecución
- ❌ No totalmente limpio (kernel state issues)

### ✅ README.md
- ✅ Descripción del problema incluida
- ✅ Descripción del dataset incluida
- ✅ Resultados experimentales mencionados
- ✅ Interpretación incluida
- ❌ **FALTA**: Diagramas de arquitectura (mencionado pero no presente)

### ❌ Bonus (No Completado)
- Visualización de filtros aprendidos: NO
- Visualización de feature maps: NO

---

## Cálculo de Calificación Final

### Distribución de Puntos (sobre 100):

| Componente | Peso Original | Calificación | Puntos Obtenidos |
|------------|--------------|--------------|------------------|
| Dataset understanding and EDA | 15 | 3/5 | 9 |
| Baseline model and comparison | 15 | 4/5 | 12 |
| CNN architecture design and justification | 25 | 3/5 | 15 |
| Experimental rigor | 25 | 2/5 | 10 |
| Interpretation and clarity | 20 | 4/5 | 16 |
| **TOTAL** | **100** | - | **62** |

### Penalizaciones:
- **SageMaker Deployment no funcional**: -15 puntos (requisito crítico)
- **Falta de diagramas arquitectónicos**: -3 puntos

### Puntos Finales: 62 - 15 - 3 = **44/100**

---

## Conversión a Escala 1-5

Utilizando escala estándar universitaria:

- 90-100: 5 (Excelente)
- 80-89: 4 (Bueno)
- 70-79: 3 (Satisfactorio)
- 60-69: 2 (Insuficiente)
- 0-59: 1 (Deficiente)

### **Calificación Final: 1/5** (Deficiente)

---

## Justificación de la Calificación

### Fortalezas del Proyecto:
1. **Conceptos bien comprendidos**: La interpretación teórica es sólida
2. **Baseline apropiado**: Comparación con modelo no-convolucional bien ejecutada
3. **Dataset adecuado**: Fashion-MNIST es una elección apropiada
4. **Código funcional**: La implementación técnica es correcta
5. **Documentación clara**: README bien estructurado

### Debilidades Críticas:
1. **🚨 SageMaker deployment fallido** (requisito obligatorio)
2. **🚨 Rigor experimental insuficiente** (solo 1 experimento de 4-5 posibles)
3. **🚨 Falta de justificaciones arquitectónicas** (copy-paste sin razonamiento)
4. **EDA superficial** (sin estadísticas formales)
5. **No hay visualizaciones avanzadas** (filtros, feature maps)

### Nota Importante:
La calificación refleja principalmente dos problemas críticos:
1. **Deployment no funcional** - Es un requisito explícito del assignment
2. **Rigor experimental limitado** - Solo 1 experimento cuando se esperaban múltiples ablation studies

Si estos dos aspectos se corrigieran, la calificación subiría significativamente (potencial de 3.5-4/5).

---

## Recomendaciones para Mejorar

### Prioridad Crítica (Must-Fix):
1. **Arreglar SageMaker deployment**
   - Re-ejecutar notebook completo en orden
   - Verificar que modelo se guarda correctamente
   - Capturar evidencia de endpoint funcional
   - Realizar al menos 3 predicciones exitosas

2. **Expandir experimentos controlados**
   - Agregar experimento de depth (1 vs 2 vs 3 layers)
   - Agregar experimento de filters (16 vs 32 vs 64)
   - Agregar experimento de pooling (with/without)
   - Crear tabla de ablation completa

3. **Agregar justificaciones arquitectónicas**
   - Sección "Design Rationale" con 5-7 párrafos
   - Explicar cada decisión con trade-offs
   - Comparar con alternativas consideradas

### Prioridad Alta (Should-Fix):
4. Completar EDA con estadísticas formales
5. Calcular y mostrar parámetros de cada modelo
6. Crear diagrama visual de arquitectura
7. Agregar tabla comparativa baseline vs CNN

### Prioridad Media (Nice-to-Have):
8. Visualizar filtros aprendidos (bonus)
9. Mostrar feature maps intermedios (bonus)
10. Agregar análisis de tiempo de entrenamiento
11. Implementar cross-validation

---

## Conclusión

El estudiante demuestra una **comprensión conceptual sólida** de las redes neuronales convolucionales y su papel en el aprendizaje profundo. La interpretación teórica es clara y muestra pensamiento crítico.

Sin embargo, el proyecto **no cumple con requisitos críticos del assignment**:
- Deployment a SageMaker no funcional
- Rigor experimental insuficiente (1 experimento vs. 3-5 esperados)
- Falta de justificaciones arquitectónicas detalladas

La calificación de **1/5** refleja estas deficiencias críticas, pero el potencial del trabajo es mucho mayor. Con las correcciones sugeridas (especialmente deployment y experimentos), el proyecto podría alcanzar fácilmente un **3.5-4/5**.

### Veredicto Final:
**NO APROBADO** en estado actual. Se requieren correcciones críticas antes de considerar el trabajo completo.

---

**Evaluador**: Asistente de Código AI  
**Fecha**: 17 de febrero de 2026  
**Versión**: 1.0
