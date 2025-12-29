# **CRITERIOS DE ACEPTACIÓN - HU: Buscar Resultados de Aprendizaje (RA) para Selección**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis del Paso 2 del wizard de vinculación):**

**C1:** Usuario está en Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)"  
**C2:** Campo de búsqueda "Buscar por código o descripción..." contiene texto  
**C3:** Texto ingresado coincide con código de RA existente (ej: "RG1", "RE2")  
**C4:** Texto ingresado coincide con descripción de RA existente (ej: "software", "ingeniería")  
**C5:** Existen RA en la carrera

**Nota:** Esta HU se enfoca específicamente en la funcionalidad de búsqueda dinámica dentro del listado de RA.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar campo de búsqueda "Buscar por código o descripción..." visible y activo  
**A2:** Mostrar todos los RA sin filtrar (estado inicial)  
**A3:** Activar búsqueda dinámica mientras el usuario escribe  
**A4:** Filtrar tabla mostrando solo RA cuyo código coincide con texto de búsqueda  
**A5:** Filtrar tabla mostrando solo RA cuya descripción contiene texto de búsqueda  
**A6:** Actualizar resultados automáticamente en tiempo real  
**A7:** Mostrar tabla vacía cuando no hay coincidencias  
**A8:** Mantener checkboxes para selección en resultados filtrados  
**A9:** Restaurar todos los RA si se borra el texto de búsqueda  
**A10:** Combinar búsqueda con filtro "Tipo de Aprendizaje" si está activo  
**A11:** Mantener estructura de tabla (columnas Código y Descripción)

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard** | F | F | F | F | V | V | V | V |
| **C2: Campo búsqueda con texto** | F | F | V | V | F | F | V | V |
| **C3: Coincide con código** | F | V | F | V | F | V | F | V |
| **C4: Coincide con descripción** | F | F | F | F | F | F | V | V |
| **C5: Existen RA** | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1-A2: Mostrar todos sin filtrar | - | - | - | - | - | X | - | - |
| A3-A6: Búsqueda dinámica activa | - | - | - | - | - | - | X | X |
| A4-A5: Mostrar resultados filtrados | - | - | - | - | - | - | - | X |
| A7: Tabla vacía sin coincidencias | - | - | - | - | - | - | X | - |

**Análisis:** R1-R4 son inválidas (fuera del contexto). Solo R5-R8 son relevantes para esta HU.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** |
|-----------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard vinculación** | V | V | V | V |
| **C2: Campo búsqueda con texto** | F | V | V | V |
| **C3: Coincide con código RA** | - | - | V | F |
| **C4: Coincide con descripción RA** | - | - | - | V |
| **C5: Existen RA en carrera** | V | V | V | V |
| **ACCIONES** |
| A1: Campo búsqueda visible y activo | X | X | X | X |
| A2: Mostrar todos los RA (sin filtrar) | X | - | - | - |
| A3: Búsqueda dinámica activada | - | X | X | X |
| A4: Filtrar y mostrar por código | - | - | X | - |
| A5: Filtrar y mostrar por descripción | - | - | - | X |
| A6: Actualizar en tiempo real | - | X | X | X |
| A7: Mostrar tabla vacía (sin coincidencias) | - | X (si no match) | - | - |
| A8-A11: Mantener funcionalidad selección | X | X | X | X |

**Justificación de minimización:**

- **R1:** Estado inicial sin búsqueda - muestra todos los RA disponibles.
- **R2:** Usuario escribe pero no hay coincidencias - tabla vacía o indica sin resultados.
- **R3:** Búsqueda coincide con código de RA - filtra por código (ej: "RG1", "RE2").
- **R4:** Búsqueda coincide con descripción de RA - filtra por contenido textual.

**Nota:** Un término puede coincidir tanto en código como descripción simultáneamente, pero para claridad los separo conceptualmente.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 4 reglas

**Análisis de consolidación:**
- R3 y R4 pueden consolidarse en un único AC de "búsqueda exitosa" ya que la acción del sistema es la misma (filtrar y mostrar coincidencias)
- La diferencia es solo en QUÉ campo coincide (código vs descripción)

**Criterios de Aceptación finales:** **3 AC**

1. **AC1:** Visualizar campo de búsqueda y todos los RA inicialmente
2. **AC2:** Buscar RA por código o descripción con resultados encontrados (happy path)
3. **AC3:** Buscar RA sin resultados coincidentes

No se detectaron AC redundantes adicionales.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar campo de búsqueda y listado completo de RA**

**Dado que** soy un coordinador de carrera **Y** estoy en el wizard de vinculación "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** he completado el Paso 1 seleccionando RAA **Y** estoy en el Paso 2 "Seleccionar Resultados de Aprendizaje (RA)",  
**cuando** visualizo el Paso 2 sin haber escrito nada en el campo de búsqueda,  
**entonces** se muestra el campo de búsqueda con el placeholder "Buscar por código o descripción..." visible y activo **Y** el campo de búsqueda está vacío listo para recibir texto **Y** se presenta la tabla con las columnas "Código" y "Descripción" **Y** se muestran TODOS los RA (Resultados de Aprendizaje) de la carrera sin filtrado **Y** cada fila muestra el código completo (ej: RG1, RG2, RG3, RE1, RE2, RE3) **Y** cada fila muestra la descripción completa del RA **Y** cada fila incluye checkbox para selección **Y** puedo visualizar la lista completa de RA disponibles antes de aplicar cualquier búsqueda **Y** puedo hacer clic en el campo de búsqueda para comenzar a buscar un RA específico.

---

### **Escenario 2 – Buscar RA por código o descripción exitosamente**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la lista completa de RA de la carrera,  
**cuando** hago clic en el campo de búsqueda "Buscar por código o descripción..." **Y** escribo un término que coincide con el código de un RA (ej: "RG1" o "RE2"),  
**entonces** la tabla se actualiza dinámicamente mientras escribo **Y** se muestran únicamente los RA cuyo código coincide con el término buscado **Y** los resultados se refinan progresivamente conforme escribo más caracteres **Y** cada RA filtrado mantiene su estructura completa (código, descripción, checkbox) **Y** la actualización ocurre en tiempo real sin necesidad de presionar Enter,  
**Y cuando** escribo un término que coincide con la descripción de un RA (ej: "software", "ingeniería", "principios"),  
**entonces** la tabla se actualiza dinámicamente mostrando únicamente los RA cuya descripción contiene el término buscado **Y** se muestran todos los RA relevantes que incluyen esa palabra clave en su descripción **Y** los resultados se actualizan en tiempo real mientras escribo **Y** cada RA filtrado mantiene visible su código, descripción completa y checkbox,  
**Y cuando** el término coincide tanto en código como en descripción (búsqueda amplia),  
**entonces** se muestran todos los RA que tienen coincidencias en cualquiera de los dos campos **Y** encuentro rápidamente el RA específico que busco para el proceso de vinculación **Y** puedo seleccionar el RA encontrado mediante su checkbox **Y** si borro el texto del campo de búsqueda, la tabla vuelve a mostrar todos los RA disponibles automáticamente **Y** la funcionalidad de filtro por "Tipo de Aprendizaje" permanece disponible y se puede combinar con la búsqueda.

---

### **Escenario 3 – Buscar RA sin resultados coincidentes**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** el campo de búsqueda está activo,  
**cuando** escribo un término de búsqueda que NO coincide con ningún código ni descripción de RA existente (ej: "XXXZZZ" o "TerminoInexistente"),  
**entonces** la búsqueda se ejecuta dinámicamente mientras escribo **Y** la tabla se actualiza mostrando que no hay resultados **Y** se presenta una tabla vacía sin filas de datos **Y** se mantienen visibles los encabezados de columnas "Código" y "Descripción" **Y** se indica claramente que no hay RA que coincidan con el criterio de búsqueda **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** puedo modificar el término de búsqueda para intentar una nueva búsqueda **Y** puedo borrar el texto para volver a ver todos los RA disponibles **Y** NO se deshabilita ninguna funcionalidad del wizard **Y** puedo continuar buscando hasta encontrar el RA específico que necesito para el proceso de vinculación.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Buscar RA por código o descripción exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero buscar resultados de aprendizaje por código o descripción para encontrar un RA específico en el proceso de vinculación". El Escenario 2 es el único que valida completamente esta funcionalidad: buscar por código O descripción Y encontrar exitosamente el RA.

2. **Happy path de la funcionalidad de búsqueda:** Representa el caso de uso principal donde la búsqueda cumple su propósito: ayudar al coordinador a localizar rápidamente un RA específico entre potencialmente decenas o cientos de opciones. Sin una búsqueda exitosa, el coordinador debe navegar manualmente por largas listas, comprometiendo la eficiencia del proceso.

3. **Validación de búsqueda dual (código Y descripción):** Este escenario es el único que valida que el sistema busca correctamente en AMBOS campos como promete el placeholder "Buscar por código o descripción...". Esta dualidad es crítica porque:
   - **Búsqueda por código:** Cuando el coordinador sabe el código exacto (ej: "RG1", "RE4")
   - **Búsqueda por descripción:** Cuando el coordinador recuerda palabras clave pero no el código (ej: "software", "ingeniería")

4. **Impacto directo en eficiencia del proceso de vinculación:** El proceso de vinculación requiere seleccionar RA específicos entre todos los RA de la carrera. En carreras con 20-50+ RA definidos, una búsqueda funcional es la diferencia entre:
   - **Con búsqueda exitosa:** Encontrar RA en segundos, completar vinculación eficientemente
   - **Sin búsqueda exitosa:** Scroll manual extenso, pérdida de tiempo, frustración, errores de selección

5. **Crítico para trazabilidad curricular precisa:** Los coordinadores vinculan RAA con RA específicos basándose en análisis curricular. Deben poder encontrar exactamente el RA correcto (no uno similar). Una búsqueda imprecisa o fallida podría llevar a:
   - Vincular RAA con RA incorrectos
   - Documentación de trazabilidad errónea
   - Problemas en evaluaciones de acreditación
   - Matrices RAA vs RA que no reflejan la realidad académica

6. **Caso de uso más frecuente en producción:** Cada vez que un coordinador establece una vinculación:
   - Primero listará los RA (Escenario 1)
   - Luego buscará RA específicos (Escenario 2) - **caso más común**
   - Raramente no encontrará nada (Escenario 3)
   
   El Escenario 2 será ejecutado cientos de veces durante la configuración inicial del sistema y actualizaciones curriculares.

7. **Validación de búsqueda dinámica en tiempo real:** Este escenario valida la experiencia de usuario moderna esperada:
   - Actualización instantánea mientras escribe
   - Sin necesidad de botones "Buscar" o Enter
   - Refinamiento progresivo de resultados
   - Respuesta inmediata del sistema
   
   Esta UX es estándar en sistemas modernos y los usuarios la esperan.

8. **Integración con otras funcionalidades:** Este escenario valida que la búsqueda:
   - Se combina correctamente con el filtro "Tipo de Aprendizaje"
   - Mantiene los checkboxes funcionales para selección
   - Preserva la capacidad de avanzar al Paso 3
   - No interfiere con otras operaciones del wizard

Los escenarios 1 y 3 son importantes para validar el estado inicial y casos sin resultados, pero el Escenario 2 es el que demuestra que el sistema cumple su propósito fundamental: permitir al coordinador buscar y encontrar rápidamente RA específicos por código o descripción durante el proceso crítico de vinculación curricular.

Un fallo en este escenario forzaría a los coordinadores a navegar manualmente por listas extensas de RA, incrementando dramáticamente el tiempo de vinculación, aumentando la probabilidad de errores de selección, y comprometiendo la eficiencia del proceso de acreditación académica. Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación.