# CRITERIOS DE ACEPTACIÓN - HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas por Nivel de Aporte

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**PRECONDICIÓN (siempre verdadera para esta HU):**
- Facultad y Carrera ya están seleccionadas
- El usuario está en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" con filtros básicos aplicados

**C1: Checkbox "Alto" marcado**
- Estado: Sí (☑) / No (□)
- Fuente: Checkbox en grupo "Nivel de aporte"
- Observado: 
  - Imagen 11 (Coordinador): Desmarcado
  - Imagen 12 (Coordinador): Marcado solo este
  - Imágenes 13-14 (Coordinador): Marcado junto con otros

**C2: Checkbox "Medio" marcado**
- Estado: Sí (☑) / No (□)
- Fuente: Checkbox en grupo "Nivel de aporte"
- Observado:
  - Imágenes 11-12: Desmarcado
  - Imágenes 13-14: Marcado

**C3: Checkbox "Bajo" marcado**
- Estado: Sí (☑) / No (□)
- Fuente: Checkbox en grupo "Nivel de aporte"
- Observado:
  - Imágenes 11-12: Desmarcado
  - Imágenes 13-14: Marcado

#### **Acciones del sistema identificadas:**

**A1: No mostrar tabla de trazabilidad**
- Condición: Ningún checkbox marcado
- Observado en Imagen 11: Área de contenido vacía, solo filtros visibles
- Resultado: Usuario ve estructura pero no datos de trazabilidad

**A2: Mostrar tabla con relaciones de nivel Alto únicamente**
- Condición: Solo checkbox "Alto" marcado
- Observado en Imagen 12: Tabla con contenido reducido
- Elementos específicos:
  - **Fila 1:** OPP1 completo → RG1 + RG3 (sin RE4) → IS-101 + IS-305 (2 asignaturas, sin MA-102 ni IS-203)
  - **Fila 2:** OPP2 completo → RG1 + RG3 (sin RG4) → GE-401 (1 asignatura, sin HU-301 ni IS-306)
  - Total: 2 filas visibles
  - Faltan: OPP3, OPP5 (no aparecen con solo nivel Alto)

**A3: Mostrar tabla con relaciones de nivel Medio únicamente**
- Condición: Solo checkbox "Medio" marcado
- No observado directamente en imágenes, comportamiento inferido

**A4: Mostrar tabla con relaciones de nivel Bajo únicamente**
- Condición: Solo checkbox "Bajo" marcado
- No observado directamente en imágenes, comportamiento inferido

**A5: Mostrar tabla con combinación de niveles seleccionados**
- Condición: Múltiples checkboxes marcados (no todos)
- Resultado: Unión de relaciones de los niveles marcados

**A6: Mostrar tabla completa con todas las relaciones**
- Condición: Todos los checkboxes marcados
- Observado en Imágenes 13-14: Tabla expandida con contenido completo
- Elementos específicos:
  - **Fila 1 EXPANDIDA:** OPP1 → RG1 + RG3 + RE4 (3 resultados) → IS-101 + IS-305 + MA-102 + IS-203 (4 asignaturas)
  - **Fila 2 EXPANDIDA:** OPP2 → RG1 + RG3 + RG4 (3 resultados) → GE-401 + HU-301 + IS-306 (3 asignaturas)
  - **Fila 3 NUEVA:** OPP3 → RE1 + RE2 + RE3 → IS-501 + IS-402 + MA-201
  - **Fila 4 NUEVA:** OPP5 → RG1 + RG2 + RE1 → CO-101 + HU-301 + IS-403
  - Total: 4+ filas visibles

**A7: Actualizar tabla dinámicamente sin recargar página**
- Condición: Cambio en cualquier checkbox
- Observado: Comportamiento esperado de SPA
- Resultado: Transición visual inmediata

**A8: Mostrar encabezados de tabla**
- Elementos: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas"
- Visible cuando hay al menos un nivel marcado

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Alto | C2: Medio | C3: Bajo | Acción del Sistema |
|-------|----------|-----------|----------|-------------------|
| R1    | No       | No        | No       | A1: No mostrar tabla con datos |
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

1. **Regla R1:** Estado sin ningún checkbox marcado. Caso especial documentado en Imagen 11. **Se mantiene como M1**.

2. **Regla R5:** Solo checkbox "Alto" marcado. Caso específico documentado en Imagen 12 con datos concretos. **Se mantiene como M2** por ser el caso de uso más común y tener evidencia visual específica.

3. **Reglas R2-R4, R6-R7:** Casos de selección parcial sin evidencia visual directa. Desde la perspectiva funcional, ejecutan la misma lógica: "mostrar relaciones de niveles seleccionados". Para evitar redundancia y enfocarnos en casos evidenciados, no los incluiremos como reglas separadas. **Se agrupan conceptualmente como variaciones de filtrado parcial**.

4. **Regla R8:** Todos los checkboxes marcados, documentado en Imágenes 13-14. **Se mantiene como M3** (HAPPY PATH).

#### **Tabla Minimizada:**

| Regla Min | C1: Alto | C2: Medio | C3: Bajo | Acción del Sistema |
|-----------|----------|-----------|----------|-------------------|
| **M1**    | No       | No        | No       | A1: No mostrar tabla con datos |
| **M2**    | Sí       | No        | No       | A2 + A8: Mostrar tabla filtrada con nivel Alto únicamente |
| **M3**    | Sí       | Sí        | Sí       | A6 + A8: Mostrar tabla completa con todos los niveles |

**Resultado: 3 reglas minimizadas**

**Justificación de minimización agresiva:**
- Solo se mantienen las reglas con **evidencia visual directa** en el prototipo
- M1: Observado en Imagen 11 (ningún checkbox)
- M2: Observado en Imagen 12 (solo Alto)
- M3: Observado en Imágenes 13-14 (todos los checkboxes)
- Las combinaciones intermedias (R2-R4, R6-R7) no aportan valor diferencial ya que la lógica es idéntica: "mostrar unión de relaciones de niveles marcados"

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 3 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre deselección de todos los niveles (caso límite)
2. M2 → AC sobre filtrado por nivel Alto únicamente (caso común, evidenciado)
3. M3 → AC sobre selección de todos los niveles (happy path, evidenciado)

**Análisis de criterios adicionales necesarios:**

Del análisis visual, identifico comportamiento crítico:

4. **Actualización dinámica entre filtros:** Cambiar de un estado de filtrado a otro debe actualizar la tabla sin recargar. Esto valida la transición entre estados M2 ↔ M3.

**Criterios a MANTENER:**

Todos los criterios identificados son únicos y aportan valor:
- M1 valida el caso límite sin datos
- M2 valida el filtrado específico más común (nivel Alto) con datos concretos observados
- M3 valida el caso completo con máxima información
- El criterio adicional valida la interactividad dinámica

**TOTAL FINAL: 4 Criterios de Aceptación**
- 3 de la tabla de decisión minimizada (M1, M2, M3)
- 1 adicional para cambio dinámico entre filtros

**Justificación de estructura conservadora:**
Dado que solo hay evidencia visual clara de 3 estados (ninguno, solo Alto, todos), es más riguroso crear ACs solo para lo que podemos validar contra el prototipo. Las combinaciones no documentadas quedarán para pruebas exploratorias o iteraciones futuras.

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

Aplicando la guía de estilo internalizada:

---

### **Escenario 1 – Deseleccionar todos los niveles de aporte**

**Dado que** estoy en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" **Y** tengo la facultad "Sistemas" y carrera "Software" seleccionadas **Y** soy un Coordinador de Carrera en el sistema,
**cuando** desmarco todos los checkboxes de "Nivel de aporte:" (Alto, Medio y Bajo quedan sin seleccionar),
**entonces** no se muestran los encabezados de tabla ("Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas") **Y** no se presenta ninguna fila de trazabilidad **Y** no se visualiza contenido de objetivos de programa **Y** no se muestran resultados de aprendizaje **Y** no aparecen códigos ni nombres de asignaturas **Y** el área de contenido principal debajo de los filtros permanece vacía **Y** los checkboxes permanecen visibles y disponibles para nueva selección **Y** queda claro que no se muestran datos por ausencia de filtros de nivel.

---

### **Escenario 2 – Filtrar por nivel "Alto" únicamente**

**Dado que** tengo el reporte visible con facultad "Sistemas" y carrera "Software" seleccionadas **Y** los checkboxes de nivel de aporte están desmarcados,
**cuando** marco únicamente el checkbox "Alto" en "Nivel de aporte:",
**entonces** se genera una tabla de trazabilidad con tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas" **Y** se muestran únicamente las filas correspondientes al nivel de aporte alto **Y** se presenta la primera fila con OPP1: "Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de software innovadores y eficientes, aplicando metodologías ágiles y estándares de calidad internacional." **Y** en columna "Resultados de Aprendizaje" se muestran únicamente: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos." (sin RE4) **Y** en columna "Asignaturas" se muestran únicamente: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web" (sin MA-102 ni IS-203) **Y** se presenta la segunda fila con OPP2 incluyendo RG1 y RG3 (sin RG4) y únicamente asignatura GE-401 (sin HU-301 ni IS-306) **Y** no se muestran las filas correspondientes a OPP3 ni OPP5 **Y** se ocultan todas las relaciones de nivel medio y bajo **Y** la tabla se actualiza sin recargar la página **Y** la respuesta visual es inmediata al marcar el checkbox.

---

### **Escenario 3 – Visualizar todos los niveles de aporte**

**Dado que** tengo el reporte visible con facultad "Sistemas" y carrera "Software" seleccionadas,
**cuando** marco todos los checkboxes "Alto", "Medio" y "Bajo" en "Nivel de aporte:",
**entonces** se genera una tabla de trazabilidad completa con las tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas" **Y** la primera fila presenta OPP1 expandido con resultados: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos.", "RE4: Diseña arquitecturas de software escalables y de alto rendimiento." (3 resultados) **Y** en columna "Asignaturas" se muestran: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web", "MA-102: Álgebra Lineal", "IS-203: Bases de Datos" (4 asignaturas) **Y** la segunda fila presenta OPP2 expandido con RG1, RG3 y RG4 (3 resultados) y asignaturas GE-401, HU-301, IS-306 (3 asignaturas) **Y** se presenta la tercera fila con OPP3: "Desarrollar habilidades críticas para la investigación y la adaptación continua a las nuevas tendencias y tecnologías en el ámbito de la ingeniería de software." con resultados RE1, RE2, RE3 y asignaturas IS-501, IS-402, MA-201 **Y** se presenta la cuarta fila con OPP5: "Fomentar la ética profesional, el compromiso social y la comunicación efectiva para interactuar en diversos contextos profesionales y comunitarios." con resultados RG1, RG2, RE1 y asignaturas CO-101, HU-301, IS-403 **Y** se visualizan todas las relaciones independientemente del nivel de intensidad **Y** la cantidad de filas y contenido por fila es mayor comparado con solo nivel "Alto" **Y** la tabla se actualiza automáticamente sin recargar la página.

---

### **Escenario 4 – Cambiar filtros de nivel dinámicamente**

**Dado que** tengo la tabla visible con solo el checkbox "Alto" marcado **Y** veo 2 filas con OPP1 y OPP2 con contenido parcial,
**cuando** marco los checkboxes "Medio" y "Bajo" adicionales manteniendo "Alto" marcado,
**entonces** la tabla se actualiza automáticamente sin recargar la página **Y** la fila de OPP1 se expande mostrando RE4 adicional en resultados de aprendizaje **Y** la fila de OPP1 muestra asignaturas adicionales MA-102 e IS-203 **Y** la fila de OPP2 se expande mostrando RG4 adicional y asignaturas HU-301 e IS-306 **Y** aparecen las filas nuevas de OPP3 y OPP5 que antes no estaban visibles **Y** la estructura de encabezados y columnas se mantiene intacta **Y** la respuesta visual es inmediata al cambio de checkboxes **Y** cuando desmarco "Medio" y "Bajo" dejando solo "Alto", la tabla retorna al estado anterior mostrando únicamente 2 filas con contenido reducido **Y** los cambios ocurren sin pérdida de información ni necesidad de recargar.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 2 – Filtrar por nivel "Alto" únicamente**

### **Justificación:**

Este criterio es el más crítico porque representa el **caso de uso principal y más frecuente** de la Historia de Usuario y valida directamente su objetivo: "identificar las relaciones por nivel de aporte". Las razones específicas son:

1. **Cumplimiento directo del valor de negocio:** El propósito de esta HU es permitir que el Coordinador de Carrera filtre y analice relaciones según su intensidad de contribución. El nivel "Alto" representa las relaciones más significativas en la alineación curricular, donde:
   - Las asignaturas contribuyen sustancialmente a los resultados de aprendizaje
   - Los resultados de aprendizaje aportan fuertemente a los objetivos del programa
   - El impacto en el perfil profesional es directo y medible
   
   Los coordinadores necesitan este filtrado para identificar las "columnas vertebrales" del currículo.

2. **Caso de uso más frecuente en análisis académico:** Basado en la evidencia del prototipo (Imagen 12 documenta específicamente este caso), este es el filtrado primario. En procesos de:
   - Revisión curricular: Se priorizan las contribuciones de alto impacto
   - Acreditación: Se destacan las relaciones más fuertes
   - Planificación: Se identifican asignaturas clave para cada objetivo
   - Evaluación: Se mide la fortaleza de la alineación curricular

3. **Validación de lógica de filtrado complejo:** Este escenario valida que el sistema puede:
   - Filtrar simultáneamente en tres dimensiones (OP, RA, Asignaturas)
   - Mantener coherencia de trazabilidad (solo mostrar OP que tienen RA de nivel Alto con asignaturas correspondientes)
   - Ocultar correctamente objetivos completos (OPP3, OPP5 no aparecen)
   - Reducir listas de RA por objetivo (RG1+RG3 sin RE4)
   - Reducir listas de asignaturas por relación (2 en lugar de 4)
   - Preservar integridad referencial en trazabilidad multinivel

4. **Evidencia visual específica y verificable:** Es el único caso de filtrado individual con datos concretos documentados (Imagen 12):
   - **Fila 1:** OPP1 → RG1 + RG3 → IS-101 + IS-305 (2 RA, 2 asignaturas)
   - **Fila 2:** OPP2 → RG1 + RG3 → GE-401 (2 RA, 1 asignatura)
   - **Ausentes:** OPP3, OPP5 completamente ocultos
   - **Contenido reducido:** Sin RE4, RG4, ni múltiples asignaturas
   
   Esta especificidad permite pruebas determinísticas con assertions exactos.

5. **Complejidad de reglas de negocio académicas:** Este filtrado no es simple exclusión de filas. Valida lógica compleja:
   - **Nivel 1:** ¿Qué objetivos de programa tienen al menos una relación de nivel Alto?
   - **Nivel 2:** Para cada objetivo, ¿qué resultados de aprendizaje tienen nivel Alto?
   - **Nivel 3:** Para cada RA de nivel Alto, ¿qué asignaturas contribuyen con nivel Alto?
   - **Resultado:** Solo mostrar la cadena completa OP→RA→Asignatura donde todo el camino tiene nivel Alto
   
   Si esta lógica falla, el análisis de trazabilidad será incorrecto.

6. **Punto de fallo de mayor impacto:** Si este escenario falla:
   - Los coordinadores no pueden identificar las relaciones principales del currículo
   - El análisis de fortalezas y debilidades será erróneo
   - Las decisiones sobre ajustes curriculares carecerán de base sólida
   - Los procesos de acreditación no podrán evidenciar las contribuciones más significativas
   - La funcionalidad principal de "identificar relaciones por nivel" quedará inoperativa
   - Podría mostrarse información incorrecta (ej: objetivos que no deberían aparecer)

7. **Base para análisis comparativo esencial:** Este filtrado permite a los coordinadores:
   - Comparar cantidad de relaciones Alto vs Medio vs Bajo
   - Identificar objetivos con pocas contribuciones altas (debilidad curricular)
   - Detectar asignaturas críticas que aportan a múltiples objetivos con nivel Alto
   - Evaluar si la distribución de niveles es equilibrada
   - Priorizar esfuerzos de mejora curricular en relaciones de bajo nivel

8. **Dependencia de otros escenarios:**
   - El Escenario 3 (todos los niveles) es la suma de Alto + Medio + Bajo
   - El Escenario 4 (cambio dinámico) depende de que el filtrado individual funcione
   - Si el filtrado por Alto falla, es muy probable que Medio y Bajo también fallen
   - Los otros escenarios son variaciones del mismo patrón de filtrado

9. **Validación de integridad de modelo de datos:** Este escenario confirma que:
   - Las relaciones OP→RA tienen nivel de aporte correctamente asignado
   - Las relaciones RA→Asignatura tienen nivel de aporte consistente
   - No hay inconsistencias donde RA tenga nivel Alto pero asignaturas solo Bajo
   - Las queries de filtrado en cascada funcionan correctamente
   - La base de datos mantiene integridad referencial en trazabilidad

10. **Complejidad de presentación:** A diferencia del reporte de matriz (checkmarks), este reporte presenta:
    - Textos largos de objetivos (párrafos completos)
    - Listas variables de resultados de aprendizaje con viñetas
    - Listas variables de asignaturas con código+nombre
    - Múltiples filas con estructura repetida pero contenido diferente
    - Necesidad de mantener legibilidad con contenido dinámico
    
    Este escenario valida que el filtrado no rompe la presentación visual.

11. **Criterio más específico y testeable:** Especifica:
    - Qué objetivos deben aparecer (OPP1, OPP2)
    - Qué objetivos NO deben aparecer (OPP3, OPP5)
    - Qué RA exactos por objetivo (RG1+RG3, sin RE4 ni RG4)
    - Qué asignaturas exactas (IS-101, IS-305, GE-401)
    - Qué asignaturas NO deben aparecer (MA-102, IS-203, HU-301, IS-306)
    
    Permite crear suite de pruebas automatizada con verificación completa.

12. **Patrón replicable por simetría:** Si funciona para "Alto", la misma lógica debe funcionar para "Medio" y "Bajo". Validar este caso cubre implícitamente el patrón para otros niveles individuales.

**Recomendación de prueba prioritaria:**
- Crear suite automatizada que verifique contenido exacto de tabla filtrada por Alto
- Validar que OPP3 y OPP5 NO aparecen cuando solo Alto está marcado
- Verificar que cada fila tiene el número correcto de RA y asignaturas
- Validar que no aparecen RE4, RG4 ni asignaturas de nivel Medio/Bajo
- Probar con múltiples carreras para verificar consistencia
- Validar performance (<1s para filtrado de 50+ objetivos)
- Verificar que el estado del filtro persiste durante la sesión
- Incluir en regresión crítica para cambios en modelo de datos o lógica de trazabilidad
- Probar casos edge: objetivos sin relaciones Alto, RA sin asignaturas de nivel Alto

**Sin este escenario funcionando correctamente, la promesa de "identificar relaciones por nivel de aporte" no se cumple**, haciendo que la funcionalidad sea inútil para su propósito de análisis curricular, gestión de calidad académica y procesos de acreditación. Este escenario valida el núcleo de la lógica de filtrado multinivel que es única y compleja en este tipo de reportes de trazabilidad académica.