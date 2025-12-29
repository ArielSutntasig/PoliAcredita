# **CRITERIOS DE ACEPTACIÓN - HU: Buscar Asignaturas (PEA)**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imagen 4 del Profesor):**

**C1:** Campo de búsqueda "Buscar por código o descripción..." contiene texto  
**C2:** Texto de búsqueda coincide con código de asignatura existente (ej: "ISWD414")  
**C3:** Texto de búsqueda coincide con descripción/nombre de asignatura existente (ej: "Ingeniería", "Software")  
**C4:** Existen asignaturas en el sistema del profesor

**Nota:** El campo de búsqueda en la imagen 4 muestra placeholder "Buscar por código o descripción...", indicando búsqueda en ambos campos simultáneamente.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar todas las asignaturas disponibles en la tabla  
**A2:** Filtrar dinámicamente la tabla mostrando solo asignaturas que coinciden con el término de búsqueda  
**A3:** Actualizar tabla automáticamente mientras el usuario escribe (búsqueda dinámica)  
**A4:** Mostrar columnas: Código, Nombre de Asignatura, Unidad de Integración Curricular, Créditos, Nivel Referencial, Acciones  
**A5:** Mostrar filas con datos completos de asignaturas coincidentes (ej: ISWD414, Ingeniería de Software y Requerimientos, Obligatoria, 2, 3)  
**A6:** Mostrar tabla vacía o mensaje indicando ausencia de resultados  
**A7:** Mantener funcionalidad de filtros adicionales (dropdowns "Nivel referencial" y "Créditos")  
**A8:** Mantener paginación visible (Previous, 1, 2, 3, Next)  
**A9:** Mantener botón "+ Nueva Asignatura" visible y funcional  
**A10:** Mantener iconos de acciones (editar y eliminar) en cada fila de resultados

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** | **R9** | **R10** | **R11** | **R12** | **R13** | **R14** | **R15** | **R16** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|---------|---------|---------|---------|
| **C1: Campo búsqueda con texto** | F | F | F | F | F | F | F | F | V | V | V | V | V | V | V | V |
| **C2: Coincide con código** | F | F | F | F | V | V | V | V | F | F | F | F | V | V | V | V |
| **C3: Coincide con descripción** | F | F | V | V | F | F | V | V | F | F | V | V | F | F | V | V |
| **C4: Existen asignaturas** | F | V | F | V | F | V | F | V | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1: Mostrar todas | - | X | - | X | - | X | - | X | - | - | - | - | - | - | - | - |
| A2: Mostrar filtradas | - | - | - | - | - | - | - | - | - | X | - | X | - | X | - | X |
| A6: Tabla vacía/sin resultados | X | - | X | - | X | - | X | - | X | - | X | - | X | - | X | - |
| A4-A5, A7-A10: Mantener UI completa | - | X | - | X | - | X | - | X | - | X | - | X | - | X | - | X |

**Análisis:** Muchas reglas representan estados imposibles o redundantes que serán simplificadas.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** |
|-----------|--------|--------|--------|--------|--------|
| **C1: Campo búsqueda con texto** | F | V | V | V | V |
| **C2: Coincide con código** | - | - | V | F | F |
| **C3: Coincide con descripción** | - | - | - | V | F |
| **C4: Existen asignaturas** | V | V | V | V | V |
| **ACCIONES** |
| A1: Mostrar todas las asignaturas | X | - | - | - | - |
| A2: Filtrar y mostrar asignaturas por código | - | - | X | - | - |
| A3: Filtrar y mostrar asignaturas por descripción | - | - | - | X | - |
| A4: Actualizar tabla dinámicamente | - | X | X | X | X |
| A5: Mostrar estructura completa de tabla | X | X | X | X | - |
| A6: Mostrar tabla vacía (sin coincidencias) | - | - | - | - | X |
| A7: Mantener filtros y controles disponibles | X | X | X | X | X |

**Justificación de minimización:**

- **Eliminadas reglas con C4=F:** Si no existen asignaturas en el sistema, la funcionalidad de búsqueda no tiene sentido. Este es un estado de base de datos vacía fuera del alcance normal de uso.
- **R1:** Estado inicial - campo vacío, mostrar todas las asignaturas disponibles.
- **R2:** Usuario comienza a escribir - el sistema debe responder dinámicamente aunque aún no haya coincidencia exacta.
- **R3:** Búsqueda coincide con código - filtrar por código (ej: "ISWD414").
- **R4:** Búsqueda coincide con descripción - filtrar por nombre/descripción (ej: "Ingeniería", "Software").
- **R5:** Búsqueda sin coincidencias - mostrar tabla vacía o mensaje.

**Nota importante:** C2 y C3 pueden ocurrir simultáneamente (una asignatura puede coincidir tanto en código como en descripción), pero para simplicidad de la tabla, las manejo como casos separados ya que la acción del sistema es la misma: mostrar las asignaturas coincidentes.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 5 reglas

**Análisis de consolidación:** 
- R2 puede integrarse con R3 y R4 ya que representa el comportamiento dinámico durante la búsqueda
- R3 y R4 pueden consolidarse en un único criterio "búsqueda exitosa" ya que ambos representan el happy path con coincidencias

**Criterios de Aceptación finales:** **4 AC**

1. **AC1:** Visualizar todas las asignaturas sin búsqueda (estado inicial)
2. **AC2:** Buscar asignatura por código o descripción con resultados encontrados (happy path)
3. **AC3:** Buscar asignatura sin resultados (búsqueda sin coincidencias)
4. **AC4:** Búsqueda dinámica en tiempo real (comportamiento de actualización)

**Consolidación R3 y R4:** Ambos representan búsqueda exitosa, la diferencia (código vs descripción) es solo el criterio de coincidencia, pero la acción del sistema es idéntica: mostrar resultados filtrados. Se consolidarán en AC2 que cubrirá ambos casos.

No se detectaron AC redundantes adicionales después de esta consolidación.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar lista completa de asignaturas sin aplicar búsqueda**

**Dado que** soy un profesor **Y** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas registradas en el sistema,  
**cuando** accedo a la vista sin ingresar ningún término en el campo de búsqueda "Buscar por código o descripción...",  
**entonces** se muestra el título "Asignaturas (PEA)" en la parte superior **Y** se visualiza el botón "+ Nueva Asignatura" en azul en la esquina superior derecha **Y** se presenta el campo de búsqueda con el placeholder "Buscar por código o descripción..." visible **Y** se muestran los dropdowns de filtros adicionales "Nivel referencial" y "Créditos" **Y** se visualiza la tabla completa con las columnas "Código", "Nombre de Asignatura", "Unidad de Integración Curricular", "Créditos", "Nivel Referencial", "Acciones" **Y** se presentan todas las asignaturas disponibles en la tabla sin filtrado **Y** cada fila muestra datos completos (ej: ISWD414, Ingeniería de Software y Requerimientos, Obligatoria, 2, 3) **Y** cada fila incluye iconos de acciones: editar (lápiz) y eliminar (papelera roja) **Y** se muestra la paginación "Previous, 1, 2, 3, Next" en la parte inferior **Y** obtengo una vista panorámica completa de todos los programas de estudio disponibles.

---

### **Escenario 2 – Buscar asignatura por código o descripción exitosamente**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas registradas en el sistema,  
**cuando** hago clic en el campo de búsqueda "Buscar por código o descripción..." **Y** escribo un término de búsqueda que coincide con el código de una asignatura (ej: "ISWD414") o con la descripción de una asignatura (ej: "Ingeniería", "Software", "Requerimientos"),  
**entonces** la tabla se actualiza automáticamente mostrando únicamente las asignaturas que coinciden con el término de búsqueda **Y** se filtran los resultados mientras escribo (búsqueda dinámica sin necesidad de presionar Enter) **Y** se muestran las filas de asignaturas cuyos códigos contienen el texto buscado **Y** se muestran las filas de asignaturas cuyos nombres/descripciones contienen el texto buscado **Y** cada resultado filtrado mantiene todas sus columnas visibles: Código, Nombre, Unidad de Integración, Créditos, Nivel, Acciones **Y** se mantienen los iconos de editar y eliminar en cada fila de resultado **Y** se actualiza la paginación según la cantidad de resultados encontrados **Y** los dropdowns "Nivel referencial" y "Créditos" permanecen disponibles para filtrado adicional **Y** el botón "+ Nueva Asignatura" permanece visible **Y** encuentro rápidamente el programa de estudio específico que busco.

---

### **Escenario 3 – Buscar asignatura sin resultados coincidentes**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo el campo de búsqueda visible,  
**cuando** escribo un término de búsqueda que NO coincide con ningún código ni descripción de asignaturas existentes (ej: "XXXZZZ" o "MateriaNonExistente"),  
**entonces** la tabla se actualiza automáticamente mostrando que no hay resultados **Y** se presenta una tabla vacía sin filas de datos **Y** se mantiene visible la estructura de la tabla con los encabezados de columnas **Y** se muestra claramente que no hay asignaturas que coincidan con el criterio de búsqueda **Y** los dropdowns "Nivel referencial" y "Créditos" permanecen disponibles **Y** el botón "+ Nueva Asignatura" permanece visible y funcional **Y** puedo modificar el término de búsqueda para intentar una nueva búsqueda **Y** el campo de búsqueda mantiene el texto ingresado visible para que pueda editarlo.

---

### **Escenario 4 – Búsqueda dinámica en tiempo real mientras se escribe**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas registradas en el sistema **Y** el campo de búsqueda está activo,  
**cuando** comienzo a escribir caracteres en el campo "Buscar por código o descripción..." (ej: escribo "I", luego "S", luego "W"),  
**entonces** la tabla se actualiza dinámicamente después de cada carácter ingresado **Y** los resultados se refinan progresivamente conforme escribo más caracteres **Y** no necesito presionar Enter ni hacer clic en ningún botón de búsqueda **Y** la actualización ocurre automáticamente en tiempo real **Y** la respuesta visual es inmediata sin recargar la página completa **Y** puedo ver cómo los resultados se van filtrando mientras continúo escribiendo **Y** si borro caracteres, la tabla vuelve a expandir los resultados automáticamente **Y** si borro todo el texto, la tabla vuelve a mostrar todas las asignaturas disponibles **Y** la experiencia de búsqueda es fluida y responsiva para encontrar rápidamente programas de estudio específicos.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Buscar asignatura por código o descripción exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece explícitamente "Quiero buscar asignaturas por código o descripción para encontrar rápidamente un programa de estudio específico". El Escenario 2 es el único que valida completamente esta funcionalidad central: buscar Y encontrar resultados exitosamente.

2. **Happy path principal de la funcionalidad:** Representa el flujo de uso más frecuente y esperado. Un profesor típicamente usa la búsqueda porque sabe que existe una asignatura específica y quiere localizarla rápidamente entre muchas otras. Este es el caso de uso que proporciona el valor principal.

3. **Validación de la lógica de búsqueda dual:** Este escenario es el único que valida que el sistema busca correctamente en AMBOS campos (código Y descripción) como promete el placeholder "Buscar por código o descripción...". Un error aquí significaría que la funcionalidad no cumple lo prometido en la interfaz.

4. **Impacto en productividad del usuario:** El objetivo explícito es "encontrar rápidamente". Si la búsqueda no funciona correctamente cuando hay coincidencias, el profesor pierde tiempo navegando manualmente por listas paginadas, lo cual contradice completamente el propósito de productividad de la funcionalidad.

5. **Caso más común en producción:** En un sistema académico con decenas o cientos de asignaturas, la búsqueda exitosa será el caso de uso ejecutado miles de veces. Los profesores confiarán en esta función diariamente para acceder a sus asignaturas para edición, consulta o gestión de RAA.

6. **Evidencia visual en el prototipo:** La imagen 4 muestra una tabla poblada con datos de asignaturas (ISWD414, etc.), indicando que el diseño contempla el escenario de búsqueda exitosa con resultados como el caso principal de uso.

Los escenarios 1, 3 y 4 son importantes para validar el estado inicial, casos sin resultados y la interactividad, pero el Escenario 2 es el único que demuestra que la funcionalidad cumple su promesa fundamental: permitir al profesor buscar y encontrar rápidamente un programa de estudio específico usando código o descripción. Un fallo en este escenario hace que toda la funcionalidad de búsqueda sea inútil, por lo que debe ser validado con máxima prioridad en las pruebas de aceptación.