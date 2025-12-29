# **CRITERIOS DE ACEPTACIÓN - HU: Listar Resultados de Aprendizaje de Carrera (RA) para Selección**

---

## **ACLARACIÓN IMPORTANTE**

He detectado una inconsistencia en la HU proporcionada:
- **Título:** "Listar Resultados de Aprendizaje de Asignatura (RAA) para selección"
- **Descripción:** "Quiero listar los resultados de aprendizaje **de la carrera**"

Basándome en:
1. El contexto del proceso de vinculación (vincular RAA con RA)
2. Las imágenes del wizard del Profesor (Paso 2) que muestran listado de RA de carrera
3. La lógica del flujo: primero se seleccionan RAA, luego RA de carrera

**Interpretaré esta HU como: Listar los RA (Resultados de Aprendizaje de la CARRERA) en el Paso 2 del wizard de vinculación, para que puedan ser seleccionados y vinculados con RAA.**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis del wizard similar al del Profesor - Paso 2):**

**C1:** Usuario (Coordinador) está en Paso 2 del wizard de vinculación  
**C2:** Se ha seleccionado al menos un RAA en Paso 1 (prerequisito)  
**C3:** Existen RA definidos en la carrera  
**C4:** Usuario aplica filtro por "Tipo de Aprendizaje" (Conocimientos, Destrezas, Valores)  
**C5:** Usuario escribe en campo de búsqueda "Buscar por código o descripción..."  
**C6:** Usuario selecciona al menos un RA de la lista

**Nota:** El Paso 2 del wizard muestra los RA disponibles de la carrera para ser seleccionados.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar título del wizard "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)"  
**A2:** Mostrar indicador de Paso 2 activo (círculo azul) con texto "Seleccionar Resultados de Aprendizaje (RA)"  
**A3:** Mostrar dropdown "Tipo de Aprendizaje" con opciones: Conocimientos, Destrezas, Valores y actitudes  
**A4:** Mostrar campo de búsqueda "Buscar por código o descripción..."  
**A5:** Mostrar tabla con columnas "Código" y "Descripción"  
**A6:** Mostrar filas con todos los RA de la carrera disponibles  
**A7:** Mostrar checkboxes para selección múltiple en cada fila  
**A8:** Mostrar datos completos de cada RA (código: RG1, RG2, RE1, etc. y descripción completa)  
**A9:** Filtrar RA dinámicamente según tipo seleccionado  
**A10:** Filtrar RA dinámicamente según búsqueda por código/descripción  
**A11:** Permitir selección múltiple de RA mediante checkboxes  
**A12:** Habilitar botón "Guardar" cuando se selecciona al menos un RA  
**A13:** Mantener botón "Guardar" deshabilitado si no hay selección

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard** | F | F | F | F | V | V | V | V |
| **C2: RAA seleccionado Paso 1** | F | F | V | V | F | F | V | V |
| **C3: Existen RA en carrera** | F | V | F | V | F | V | F | V |
| **C4: Filtro tipo aplicado** | - | - | - | - | - | - | - | F/V |
| **ACCIONES** |
| A1-A4: Mostrar estructura Paso 2 | - | - | - | - | - | - | - | X |
| A5-A8: Mostrar tabla con RA | - | - | - | - | - | - | - | X |
| A9-A10: Aplicar filtros si activos | - | - | - | - | - | - | - | X |
| A11-A13: Permitir selección | - | - | - | - | - | - | - | X |

**Análisis:** Solo R8 (todas las condiciones verdaderas) es válida para esta HU.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** |
|-----------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard de vinculación** | V | V | V | V |
| **C2: RAA seleccionado en Paso 1** | V | V | V | V |
| **C3: Existen RA en la carrera** | V | V | V | V |
| **C4: Filtro "Tipo de Aprendizaje" aplicado** | F | V | F | F |
| **C5: Búsqueda por código/descripción aplicada** | F | F | V | F |
| **C6: Al menos un RA seleccionado** | F | - | - | V |
| **ACCIONES** |
| A1-A4: Mostrar estructura Paso 2 | X | X | X | X |
| A5-A8: Mostrar tabla completa con todos los RA | X | - | - | X |
| A9: Filtrar por tipo | - | X | - | - |
| A10: Filtrar por búsqueda | - | - | X | - |
| A11: Permitir selección múltiple | X | X | X | X |
| A12: Habilitar botón "Guardar" | - | - | - | X |
| A13: Mantener botón deshabilitado | X | X | X | - |

**Justificación de minimización:**

- **R1:** Visualización inicial sin filtros - muestra todos los RA disponibles.
- **R2:** Aplicación de filtro por tipo - muestra solo RA del tipo seleccionado.
- **R3:** Aplicación de búsqueda - muestra solo RA que coinciden con término.
- **R4:** Selección de RA - habilita continuar al Paso 3.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 4 reglas

**Análisis:** Cada regla representa un aspecto diferente de la funcionalidad de listado:
1. Visualización completa inicial
2. Filtrado por tipo
3. Búsqueda por código/descripción
4. Selección para avanzar

**Criterios de Aceptación finales:** **4 AC**

No se detectaron AC redundantes. Cada uno valida funcionalidad específica del listado de RA para selección.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Listar todos los RA de la carrera para selección**

**Dado que** soy un coordinador de carrera **Y** estoy en el wizard de vinculación "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** he completado el Paso 1 seleccionando al menos un RAA **Y** he avanzado al Paso 2,  
**cuando** el sistema carga el Paso 2 "Seleccionar Resultados de Aprendizaje (RA)",  
**entonces** se muestra el indicador de progreso con el Paso 2 activo en círculo azul **Y** se presenta el título "Seleccionar Resultados de Aprendizaje (RA)" **Y** se visualiza el dropdown "Tipo de Aprendizaje" con las opciones: "Conocimientos", "Destrezas", "Valores y actitudes" **Y** se muestra el campo de búsqueda con placeholder "Buscar por código o descripción..." **Y** se presenta la tabla con las columnas "Código" y "Descripción" **Y** se muestran TODOS los RA (Resultados de Aprendizaje) definidos en la carrera en forma de filas **Y** cada fila incluye un checkbox para selección **Y** cada fila muestra el código del RA (ej: RG1, RG2, RG3, RG4, RG5, RE1, RE2, RE3, RE4, RE5, RE6) **Y** cada fila muestra la descripción completa del RA (ej: "Comprender los principios fundamentales de la ingeniería de software.") **Y** el botón "Guardar" está deshabilitado en gris hasta que seleccione al menos un RA **Y** puedo visualizar todos los resultados de aprendizaje de la carrera disponibles para vincular con los RAA previamente seleccionados.

---

### **Escenario 2 – Filtrar RA por tipo de aprendizaje**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la lista completa de RA de la carrera,  
**cuando** hago clic en el dropdown "Tipo de Aprendizaje" **Y** selecciono una opción específica (ej: "Conocimientos" o "Destrezas" o "Valores y actitudes"),  
**entonces** la tabla se actualiza automáticamente mostrando únicamente los RA que pertenecen al tipo seleccionado **Y** se filtran los resultados mientras mantengo la selección **Y** se ocultan los RA que no corresponden al tipo seleccionado **Y** se mantiene la estructura completa de la tabla con las columnas "Código" y "Descripción" **Y** cada RA filtrado mantiene su checkbox para selección **Y** puedo seleccionar RA específicos del tipo que me interesa **Y** puedo cambiar el filtro de tipo para ver RA de otras categorías **Y** la funcionalidad de búsqueda por código/descripción sigue disponible y se combina con este filtro **Y** encuentro más fácilmente los RA específicos que necesito seleccionar para el proceso de vinculación.

---

### **Escenario 3 – Buscar RA por código o descripción**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la lista de RA de la carrera,  
**cuando** hago clic en el campo de búsqueda "Buscar por código o descripción..." **Y** escribo un término de búsqueda (ej: "RG1" o "ingeniería" o "software"),  
**entonces** la tabla se actualiza dinámicamente mientras escribo **Y** se muestran únicamente los RA cuyo código coincide con el término de búsqueda **Y** se muestran únicamente los RA cuya descripción contiene el término de búsqueda **Y** los resultados se refinan progresivamente conforme escribo más caracteres **Y** la actualización ocurre en tiempo real sin necesidad de presionar Enter **Y** se mantienen los checkboxes para selección en cada resultado filtrado **Y** si no hay coincidencias, la tabla se muestra vacía **Y** si borro el texto, la tabla vuelve a mostrar todos los RA disponibles **Y** la funcionalidad de filtro por tipo permanece disponible y se puede combinar con la búsqueda **Y** encuentro rápidamente RA específicos por su código o por palabras clave en su descripción para poder seleccionarlos en el proceso de vinculación.

---

### **Escenario 4 – Seleccionar RA y avanzar al siguiente paso**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la lista de RA de la carrera (filtrada o completa),  
**cuando** hago clic en el checkbox de al menos un RA (ej: selecciono "RG1 - Comprender los principios fundamentales de la ingeniería de software."),  
**entonces** el checkbox se marca visualmente indicando selección **Y** puedo seleccionar múltiples RA haciendo clic en varios checkboxes **Y** puedo deseleccionar RA haciendo clic nuevamente en sus checkboxes marcados **Y** el botón "Guardar" cambia de gris deshabilitado a azul habilitado en cuanto selecciono al menos un RA **Y** si deselecciono todos los RA, el botón "Guardar" vuelve a deshabilitarse **Y** puedo hacer clic en el botón "Guardar" habilitado para avanzar al Paso 3 del wizard **Y** los RA seleccionados se pasan al siguiente paso para completar el proceso de vinculación **Y** he seleccionado exitosamente los resultados de aprendizaje de la carrera que serán vinculados con los RAA de la asignatura **Y** puedo continuar con la justificación de la relación en el Paso 3.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 1 – Listar todos los RA de la carrera para selección**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero listar los resultados de aprendizaje de la carrera para poder seleccionarlos en el proceso de vinculación". El Escenario 1 es el único que valida completamente el listado inicial y completo de RA, que es el prerequisito absoluto para cualquier selección posterior.

2. **Prerequisito obligatorio para toda la funcionalidad:** Sin un listado correcto y completo de RA, ninguno de los otros escenarios puede ejecutarse:
   - No se puede filtrar (Escenario 2) si no hay lista base
   - No se puede buscar (Escenario 3) si no hay datos que buscar
   - No se puede seleccionar (Escenario 4) si no hay RA visibles

3. **Validación de datos críticos de la carrera:** Este escenario valida que el sistema carga correctamente TODOS los RA definidos para la carrera. Los RA son el núcleo del perfil de egreso y las competencias que la institución promete desarrollar en sus estudiantes. Un error en el listado significaría:
   - RA faltantes que no pueden ser vinculados
   - Vinculaciones incompletas que comprometen la trazabilidad
   - Documentación de acreditación inválida
   - Pérdida de coherencia entre lo planificado y lo ejecutado

4. **Crítico para el proceso de vinculación completo:** El proceso de vinculación (Paso 1: RAA → Paso 2: RA → Paso 3: Justificación) depende críticamente de que el Paso 2 muestre correctamente todos los RA disponibles. Si faltan RA:
   - Los coordinadores no pueden establecer relaciones completas
   - Se pierden vinculaciones importantes entre asignaturas y competencias de carrera
   - El análisis de contribución de asignaturas queda incompleto
   - La matriz RAA vs RA no refleja la realidad curricular

5. **Impacto en acreditación académica:** En el contexto de acreditación EUR-ACE, demostrar la trazabilidad completa desde asignaturas hasta competencias de egreso es obligatorio. Este escenario asegura que:
   - Todos los RA están disponibles para vinculación
   - No hay "puntos ciegos" en la documentación
   - La cobertura de competencias puede evaluarse completamente
   - Los auditores pueden verificar trazabilidad integral

6. **Caso de uso inicial y más frecuente:** Cada vez que un coordinador inicia el proceso de vinculación para una asignatura:
   - Primero verá el listado completo (Escenario 1)
   - Opcionalmente aplicará filtros o búsqueda (Escenarios 2-3)
   - Finalmente seleccionará (Escenario 4)
   
   El Escenario 1 es el punto de entrada obligatorio que se ejecuta en el 100% de los casos.

7. **Validación de integridad de UI y datos:** Este escenario valida múltiples aspectos críticos simultáneamente:
   - Carga correcta de todos los RA desde base de datos
   - Renderizado apropiado de tabla con estructura correcta
   - Presentación de checkboxes funcionales para cada RA
   - Visualización completa de códigos y descripciones
   - Estado inicial correcto del botón "Guardar" (deshabilitado)

Los escenarios 2, 3 y 4 son importantes para la usabilidad (filtrado, búsqueda) y para completar el flujo (selección), pero el Escenario 1 es el fundamento sobre el cual todo lo demás se construye. Sin un listado completo y correcto de RA, el proceso de vinculación no puede cumplir su objetivo de establecer trazabilidad curricular confiable.

Un fallo en este escenario haría que RA críticos de la carrera queden "invisibles" en el proceso de vinculación, creando vacíos en la documentación académica que podrían comprometer evaluaciones de acreditación y la integridad del diseño curricular. Por tanto, debe ser validado con máxima prioridad y rigurosidad en las pruebas de aceptación.