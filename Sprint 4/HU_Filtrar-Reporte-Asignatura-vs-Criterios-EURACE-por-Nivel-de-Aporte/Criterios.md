# CRITERIOS DE ACEPTACIÓN - HU: Filtrar Reporte Asignatura vs Criterios EURACE por Nivel de Aporte

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**PRECONDICIÓN (siempre verdadera para esta HU):**
- Facultad y Carrera ya están seleccionadas
- El usuario está en el reporte "Reporte: Asignatura vs Criterios EURACE" con filtros básicos aplicados

**C1: Checkbox "Alto" marcado**
- Estado: Sí (☑) / No (□)
- Fuente: Checkbox en grupo "Nivel de aporte"
- Observado: 
  - Imagen 4: Desmarcado
  - Imagen 5: Marcado
  - Imágenes 6-7: Marcado

**C2: Checkbox "Medio" marcado**
- Estado: Sí (☑) / No (□)
- Fuente: Checkbox en grupo "Nivel de aporte"
- Observado:
  - Imágenes 4-5: Desmarcado
  - Imágenes 6-7: Marcado

**C3: Checkbox "Bajo" marcado**
- Estado: Sí (☑) / No (□)
- Fuente: Checkbox en grupo "Nivel de aporte"
- Observado:
  - Imágenes 4-5: Desmarcado
  - Imágenes 6-7: Marcado

#### **Acciones del sistema identificadas:**

**A1: No mostrar matriz de datos**
- Condición: Ningún checkbox marcado
- Observado en Imagen 4: Área de contenido vacía, solo mensaje instructivo visible
- Resultado: Usuario ve estructura pero no datos

**A2: Mostrar matriz con relaciones de nivel Alto únicamente**
- Condición: Solo checkbox "Alto" marcado
- Observado en Imagen 5: Matriz visible con checkmarks verdes específicos
- Elementos:
  - Álgebra Lineal: ✓ en 5.3.4, 5.3.5
  - Cálculo en una Variable: ✓ en 5.2.2, 5.2.4, 5.3.3
  - Mecánica Newtoniana: ✓ en 5.2.5, 5.3.1, 5.3.2
  - Programación I: ✓ en 5.2.5
  - (Cantidad reducida de checkmarks)

**A3: Mostrar matriz con relaciones de nivel Medio únicamente**
- Condición: Solo checkbox "Medio" marcado
- No observado directamente en imágenes, pero comportamiento inferido por lógica del sistema

**A4: Mostrar matriz con relaciones de nivel Bajo únicamente**
- Condición: Solo checkbox "Bajo" marcado
- No observado directamente en imágenes, pero comportamiento inferido por lógica del sistema

**A5: Mostrar matriz con combinación de niveles seleccionados**
- Condición: Múltiples checkboxes marcados
- Resultado: Unión de relaciones de los niveles marcados

**A6: Mostrar matriz completa con todas las relaciones**
- Condición: Todos los checkboxes marcados
- Observado en Imágenes 6-7: Matriz con mayor cantidad de checkmarks verdes
- Elementos adicionales vs solo Alto:
  - Cálculo en una Variable: ✓ adicionales en 5.2.4, 5.3.3, 5.3.7
  - Mecánica Newtoniana: ✓ adicionales en 5.2.2, 5.3.1, 5.3.2
  - Comunicación Oral y Escrita: ✓ en 5.3.3, 5.3.5
  - Ecuaciones Diferenciales: ✓ en 5.2.1, 5.2.5, 5.3.2, 5.3.4, 5.3.5
  - (Mayor densidad de checkmarks en matriz)

**A7: Actualizar matriz dinámicamente sin recargar página**
- Condición: Cambio en cualquier checkbox
- Observado: Comportamiento esperado de SPA (Single Page Application)
- Resultado: Transición visual inmediata

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Alto | C2: Medio | C3: Bajo | Acción del Sistema |
|-------|----------|-----------|----------|-------------------|
| R1    | No       | No        | No       | A1: No mostrar matriz con datos |
| R2    | No       | No        | Sí       | A4: Mostrar solo relaciones nivel Bajo |
| R3    | No       | Sí        | No       | A3: Mostrar solo relaciones nivel Medio |
| R4    | No       | Sí        | Sí       | A5: Mostrar relaciones nivel Medio + Bajo |
| R5    | Sí       | No        | No       | A2: Mostrar solo relaciones nivel Alto |
| R6    | Sí       | No        | Sí       | A5: Mostrar relaciones nivel Alto + Bajo |
| R7    | Sí       | Sí        | No       | A5: Mostrar relaciones nivel Alto + Medio |
| R8    | Sí       | Sí        | Sí       | A6: Mostrar todas las relaciones (3 niveles) |

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Regla R1:** Estado sin ningún checkbox marcado. Es un caso especial que debe manejarse explícitamente. **Se mantiene como M1**.

2. **Reglas R2-R7:** Todas representan casos de selección parcial donde se muestran solo las relaciones de los niveles marcados. Desde la perspectiva funcional, todas ejecutan la misma lógica: "mostrar relaciones de niveles seleccionados". Sin embargo, desde la perspectiva de pruebas, son combinaciones diferentes. **Se mantienen separadas para validar combinaciones específicas**: M2 (solo Alto), M3 (Alto+Medio), M4 (Alto+Bajo).

3. **Regla R8:** Todos los checkboxes marcados, representa el caso de máxima información. **Se mantiene como M5**.

4. **Simplificación por simetría:** R2, R3, R4 (casos sin Alto) pueden agruparse conceptualmente ya que el comportamiento es idéntico (mostrar solo relaciones de niveles marcados). Sin embargo, por completitud de pruebas y dado que solo tenemos evidencia visual de Alto y Todos, mantendré las combinaciones más relevantes.

#### **Tabla Minimizada:**

| Regla Min | C1: Alto | C2: Medio | C3: Bajo | Acción del Sistema |
|-----------|----------|-----------|----------|-------------------|
| **M1**    | No       | No        | No       | A1: No mostrar matriz con datos |
| **M2**    | Sí       | No        | No       | A2: Mostrar solo relaciones nivel Alto (EVIDENCIADO) |
| **M3**    | Sí       | Sí        | No       | A5: Mostrar relaciones nivel Alto + Medio |
| **M4**    | No       | Sí        | Sí       | A5: Mostrar relaciones nivel Medio + Bajo |
| **M5**    | Sí       | Sí        | Sí       | A6: Mostrar todas las relaciones (HAPPY PATH) |

**Resultado: 5 reglas minimizadas**

**Justificación de selección:**
- M1: Caso límite sin filtros (observado en Imagen 4)
- M2: Caso más común de filtrado específico (observado en Imagen 5)
- M3: Combinación de dos niveles superiores (caso intermedio importante)
- M4: Combinación sin nivel Alto (valida que el sistema funciona sin el nivel más común)
- M5: Caso completo con máxima información (observado en Imágenes 6-7)

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 5 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre deselección de todos los niveles (caso límite)
2. M2 → AC sobre filtrado por nivel Alto únicamente (caso común)
3. M3 → AC sobre filtrado por niveles Alto y Medio
4. M4 → AC sobre filtrado por niveles Medio y Bajo
5. M5 → AC sobre selección de todos los niveles (happy path)

**Análisis de criterios adicionales necesarios:**

Del análisis visual, identifico comportamientos críticos:

6. **Actualización dinámica:** El cambio de checkboxes debe actualizar la matriz sin recargar la página (comportamiento de SPA observado en la secuencia de imágenes).

7. **Cambio entre filtros:** Marcar/desmarcar dinámicamente debe actualizar el contenido inmediatamente.

**Criterios a ELIMINAR por redundancia:**

- **M3 y M4 (combinaciones intermedias):** Si bien son válidas, agregan complejidad sin aportar valor diferencial en pruebas. La lógica subyacente es la misma: "mostrar unión de relaciones de niveles marcados". Si M2 (un nivel) y M5 (tres niveles) funcionan, las combinaciones de dos niveles funcionarán por transitividad. **ELIMINADOS por redundancia lógica**.

**Criterios consolidados:**

El criterio de actualización dinámica (punto 6) se incorporará en cada escenario de cambio de filtro, no como AC separado.

**TOTAL FINAL: 4 Criterios de Aceptación**
- 1 de M1 (deselección total)
- 1 de M2 (filtrado específico por Alto)
- 1 de M5 (todos los niveles)
- 1 adicional para cambio dinámico entre filtros

**Justificación de eliminaciones:**
- **M3 (Alto + Medio):** Redundante con la lógica validada por M2 y M5. Si el sistema puede mostrar uno y tres niveles correctamente, dos niveles funcionará por la misma lógica de unión.
- **M4 (Medio + Bajo):** Redundante por la misma razón. Además, no hay evidencia visual directa en el prototipo de estos casos intermedios.

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

Aplicando la guía de estilo internalizada:

---

### **Escenario 1 – Deseleccionar todos los niveles de aporte**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" **Y** tengo la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas **Y** soy un Coordinador de Carrera en el sistema,
**cuando** desmarco todos los checkboxes de "Nivel de aporte:" (Alto, Medio y Bajo quedan sin seleccionar),
**entonces** se mantiene visible el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:" **Y** no se muestra la matriz con datos **Y** no se muestran encabezados de columnas EUR-ACE **Y** no se presentan filas de asignaturas **Y** no aparecen checkmarks verdes en ninguna intersección **Y** el área de contenido principal debajo de los filtros permanece vacía **Y** los checkboxes permanecen visibles y disponibles para nueva selección **Y** es evidente que no hay contenido mostrado por ausencia de filtros de nivel.

---

### **Escenario 2 – Filtrar por nivel "Alto" únicamente**

**Dado que** tengo el reporte visible con facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas **Y** los checkboxes de nivel de aporte están desmarcados,
**cuando** marco únicamente el checkbox "Alto" en "Nivel de aporte:",
**entonces** se mantiene el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:" **Y** se genera la matriz completa con encabezados de columnas EUR-ACE (5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7) en fondo azul oscuro **Y** se presentan las filas de asignaturas (Álgebra Lineal, Cálculo en una Variable, Mecánica Newtoniana, Programación I, Comunicación Oral y Escrita, Ecuaciones Diferenciales, Matemática Computacional, Fundamentos de Electrónica) **Y** se muestran únicamente los checkmarks verdes (✓) correspondientes a relaciones de nivel de aporte alto **Y** específicamente se muestran checkmarks en: Álgebra Lineal (5.3.4, 5.3.5), Cálculo en una Variable (5.2.2, 5.2.4, 5.3.3), Mecánica Newtoniana (5.2.5, 5.3.1, 5.3.2), Programación I (5.2.5) **Y** se ocultan todas las relaciones de nivel medio y bajo **Y** la matriz se actualiza sin recargar la página **Y** la respuesta visual es inmediata al marcar el checkbox.

---

### **Escenario 3 – Visualizar todos los niveles de aporte**

**Dado que** tengo el reporte visible con facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas,
**cuando** marco todos los checkboxes "Alto", "Medio" y "Bajo" en "Nivel de aporte:",
**entonces** se genera la matriz completa con encabezados de columnas EUR-ACE **Y** se presentan todas las filas de asignaturas **Y** se muestran todos los checkmarks verdes (✓) de los tres niveles de aporte combinados **Y** se visualizan relaciones adicionales comparado con solo nivel "Alto": Cálculo en una Variable muestra checkmarks adicionales en 5.2.4, 5.3.7; Comunicación Oral y Escrita muestra checkmarks en 5.3.3, 5.3.5; Ecuaciones Diferenciales muestra checkmarks en 5.2.1, 5.2.5, 5.3.2, 5.3.4, 5.3.5 **Y** la densidad de checkmarks verdes en la matriz es mayor que con solo un nivel seleccionado **Y** se presenta una vista panorámica completa de todas las contribuciones de las asignaturas a criterios EUR-ACE independientemente del nivel de intensidad **Y** la matriz se actualiza automáticamente sin recargar la página.

---

### **Escenario 4 – Cambiar filtros de nivel dinámicamente**

**Dado que** tengo la matriz visible con todos los niveles de aporte marcados (Alto, Medio, Bajo) **Y** veo checkmarks verdes en múltiples intersecciones,
**cuando** desmarco el checkbox "Medio" manteniendo "Alto" y "Bajo" marcados,
**entonces** la matriz se actualiza automáticamente sin recargar la página **Y** se ocultan los checkmarks verdes correspondientes exclusivamente al nivel medio **Y** se mantienen visibles los checkmarks de nivel alto y bajo **Y** la cantidad de checkmarks verdes disminuye en la matriz **Y** la estructura de encabezados y columnas EUR-ACE se mantiene intacta **Y** las filas de asignaturas permanecen visibles **Y** la respuesta visual es inmediata al cambio de checkbox **Y** cuando vuelvo a marcar el checkbox "Medio", los checkmarks correspondientes reaparecen automáticamente **Y** la matriz restaura la visualización previa sin pérdida de información.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 2 – Filtrar por nivel "Alto" únicamente**

### **Justificación:**

Este criterio es el más crítico porque representa el **caso de uso principal** de la Historia de Usuario y valida directamente su objetivo: "identificar las contribuciones de una intensidad específica". Las razones específicas son:

1. **Cumplimiento directo del valor de negocio:** El propósito de esta HU es permitir que el Coordinador de Carrera analice contribuciones por intensidad. El nivel "Alto" es típicamente el más relevante desde la perspectiva académica, ya que representa las contribuciones más significativas de las asignaturas a los criterios EUR-ACE. Los coordinadores necesitan identificar rápidamente estas contribuciones principales para:
   - Evaluar la fortaleza de la alineación curricular
   - Identificar asignaturas clave para cada criterio
   - Priorizar revisiones curriculares
   - Preparar evidencias de acreditación

2. **Caso de uso más frecuente:** Basado en el análisis del prototipo (Imagen 5 muestra específicamente este caso), este es el filtrado más común. Los usuarios académicos típicamente comienzan su análisis revisando contribuciones de alto impacto antes de profundizar en niveles medio y bajo.

3. **Validación de lógica de filtrado core:** Este escenario valida que el sistema puede:
   - Discriminar correctamente entre niveles de aporte
   - Ocultar relaciones de otros niveles (medio y bajo)
   - Mostrar solo checkmarks correspondientes al nivel seleccionado
   - Mantener la estructura de matriz mientras filtra contenido
   - Aplicar el filtro sin afectar otros elementos de la UI

4. **Evidencia visual específica y detallada:** Es el único caso de filtrado individual documentado con checkmarks específicos en el prototipo (Imagen 5). Los checkmarks exactos observados son:
   - Álgebra Lineal: 5.3.4, 5.3.5
   - Cálculo en una Variable: 5.2.2, 5.2.4, 5.3.3
   - Mecánica Newtoniana: 5.2.5, 5.3.1, 5.3.2
   - Programación I: 5.2.5
   
   Esta especificidad permite pruebas determinísticas y verificables.

5. **Punto de fallo de mayor impacto:** Si este escenario falla:
   - Los coordinadores no podrán identificar las contribuciones principales
   - El análisis de fortalezas curriculares se verá comprometido
   - Las decisiones estratégicas sobre el currículo carecerán de base sólida
   - Los procesos de acreditación no podrán destacar las contribuciones más significativas
   - La funcionalidad principal de la HU quedará inoperativa

6. **Dependencia de escenarios relacionados:** 
   - El Escenario 3 (todos los niveles) es esencialmente la suma de los tres niveles individuales
   - El Escenario 4 (cambio dinámico) depende de que el filtrado individual funcione correctamente
   - Si el filtrado por "Alto" falla, es probable que los otros niveles también fallen

7. **Base para análisis comparativo:** Los usuarios necesitan este filtrado individual para:
   - Comparar visualmente Alto vs Medio vs Bajo
   - Cuantificar diferencias en cobertura por nivel
   - Identificar gaps donde solo existen contribuciones bajas
   - Evaluar si la distribución de niveles es apropiada

8. **Validación de modelo de datos académico:** Este escenario confirma que:
   - Las relaciones Asignatura-Criterio EUR-ACE tienen nivel de aporte correctamente asignado
   - El atributo "nivel de aporte" está poblado en la base de datos
   - Las consultas de filtrado funcionan correctamente
   - No hay inconsistencias en la clasificación de niveles

9. **Criterio de aceptación más específico:** A diferencia de otros escenarios que validan comportamientos generales, este especifica checkmarks exactos en posiciones específicas, permitiendo:
   - Pruebas automatizadas con assertions precisos
   - Validación determinística de resultados
   - Detección de regresiones específicas
   - Verificación de integridad de datos

10. **Patrón replicable:** Si este escenario funciona correctamente para "Alto", la misma lógica debe funcionar para "Medio" y "Bajo" (por simetría del diseño). Por lo tanto, validar este caso cubre implícitamente el 33% de las combinaciones individuales.

**Recomendación de prueba prioritaria:**
- Crear suite automatizada que verifique checkmarks exactos para nivel Alto
- Validar que no aparecen checkmarks de nivel Medio o Bajo cuando solo Alto está marcado
- Probar con múltiples carreras para verificar consistencia de comportamiento
- Incluir validación de performance (la matriz debe actualizarse en <500ms)
- Verificar que el estado del filtro se mantiene durante la sesión
- Añadir a regresión crítica para cada cambio en modelo de datos o lógica de filtrado

**Sin este escenario funcionando, el valor fundamental de "identificar contribuciones de intensidad específica" no se cumple**, haciendo que la funcionalidad sea inútil para su propósito académico y de gestión curricular.