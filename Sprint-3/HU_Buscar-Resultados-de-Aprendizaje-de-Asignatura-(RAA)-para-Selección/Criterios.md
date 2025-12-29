# **CRITERIOS DE ACEPTACIÓN - HU: Buscar Resultados de Aprendizaje de Asignatura (RAA) para Selección**

---

## **ACLARACIÓN IMPORTANTE SOBRE LA HU**

He detectado una inconsistencia en la HU proporcionada:
- **Título:** "Buscar Resultados de Aprendizaje (RAA) para selección"
- **Descripción:** "...buscar resultados de aprendizaje de una asignatura... para encontrar un RA específico"

La descripción mezcla "RAA" (Resultados de Aprendizaje de Asignatura) con "RA" (Resultados de Aprendizaje de Carrera).

**Interpretación basada en contexto:**
Dado que el título especifica "RAA" y la descripción menciona "de una asignatura", interpretaré esta HU como:
- **Contexto:** Paso 1 del wizard de vinculación
- **Funcionalidad:** Buscar RAA (de la asignatura seleccionada) por palabra clave
- **Usuario:** Coordinador que vincula una asignatura específica

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis del Paso 1 del wizard):**

**C1:** Usuario (Coordinador) está en Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)"  
**C2:** Campo de búsqueda "Buscar por código o descripción..." contiene texto  
**C3:** Texto ingresado coincide con código de RAA existente (ej: "1.1", "2.1")  
**C4:** Texto ingresado coincide con descripción/palabra clave de RAA existente (ej: "conocimiento", "software")  
**C5:** Existen RAA definidos para la asignatura seleccionada

**Nota:** El Paso 1 del wizard muestra RAA de la asignatura que fue seleccionada previamente por el Coordinador.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar campo de búsqueda "Buscar por código o descripción..." visible y activo  
**A2:** Mostrar todos los RAA sin filtrar (estado inicial)  
**A3:** Activar búsqueda dinámica mientras el usuario escribe  
**A4:** Filtrar tabla mostrando solo RAA cuyo código coincide con texto de búsqueda  
**A5:** Filtrar tabla mostrando solo RAA cuya descripción contiene palabra clave buscada  
**A6:** Actualizar resultados automáticamente en tiempo real  
**A7:** Mostrar tabla vacía cuando no hay coincidencias  
**A8:** Mantener checkboxes para selección en resultados filtrados  
**A9:** Restaurar todos los RAA si se borra el texto de búsqueda  
**A10:** Mantener estructura de tabla (columnas Código, Tipo, Descripción)  
**A11:** Mantener paginación funcional si aplica

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En Paso 1 wizard** | F | F | F | F | V | V | V | V |
| **C2: Campo búsqueda con texto** | F | F | V | V | F | F | V | V |
| **C3: Coincide con código** | F | V | F | V | F | V | F | V |
| **C4: Coincide con descripción** | F | F | F | F | F | F | V | V |
| **C5: Existen RAA** | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1-A2: Mostrar todos sin filtrar | - | - | - | - | - | X | - | - |
| A3-A6: Búsqueda dinámica activa | - | - | - | - | - | - | X | X |
| A4-A5: Mostrar resultados filtrados | - | - | - | - | - | - | - | X |
| A7: Tabla vacía sin coincidencias | - | - | - | - | - | - | X (si no) | - |

**Análisis:** R1-R4 son inválidas (fuera del contexto). Solo R5-R8 son relevantes.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** |
|-----------|--------|--------|--------|--------|
| **C1: En Paso 1 wizard vinculación** | V | V | V | V |
| **C2: Campo búsqueda con texto** | F | V | V | V |
| **C3: Coincide con código RAA** | - | - | V | F |
| **C4: Coincide con descripción/palabra clave** | - | - | - | V |
| **C5: Existen RAA en asignatura** | V | V | V | V |
| **ACCIONES** |
| A1: Campo búsqueda visible y activo | X | X | X | X |
| A2: Mostrar todos los RAA (sin filtrar) | X | - | - | - |
| A3: Búsqueda dinámica activada | - | X | X | X |
| A4: Filtrar y mostrar por código | - | - | X | - |
| A5: Filtrar y mostrar por palabra clave | - | - | - | X |
| A6: Actualizar en tiempo real | - | X | X | X |
| A7: Mostrar tabla vacía (sin coincidencias) | - | X (si no match) | - | - |
| A8-A11: Mantener funcionalidad selección | X | X | X | X |

**Justificación de minimización:**

- **R1:** Estado inicial sin búsqueda - muestra todos los RAA de la asignatura.
- **R2:** Usuario escribe pero no hay coincidencias - tabla vacía.
- **R3:** Búsqueda coincide con código de RAA - filtra por código (ej: "1.1", "2.1").
- **R4:** Búsqueda coincide con palabra clave en descripción - filtra por contenido.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 4 reglas

**Análisis de consolidación:**
- R3 y R4 pueden consolidarse en un AC de "búsqueda exitosa" ya que la acción del sistema es idéntica (filtrar y mostrar)

**Criterios de Aceptación finales:** **3 AC**

1. **AC1:** Visualizar campo de búsqueda y todos los RAA inicialmente
2. **AC2:** Buscar RAA por código o palabra clave con resultados encontrados (happy path)
3. **AC3:** Buscar RAA sin resultados coincidentes

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar campo de búsqueda y listado completo de RAA**

**Dado que** soy un coordinador de carrera **Y** estoy en el wizard de vinculación "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** he seleccionado una asignatura específica **Y** estoy en el Paso 1 "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)",  
**cuando** visualizo el Paso 1 sin haber escrito nada en el campo de búsqueda,  
**entonces** se muestra el campo de búsqueda con el placeholder "Buscar por código o descripción..." visible y activo **Y** el campo de búsqueda está vacío listo para recibir texto **Y** se presenta la tabla con las columnas "Código", "Tipo", "Descripción" **Y** se muestran TODOS los RAA de la asignatura seleccionada sin filtrado **Y** cada fila muestra el código del RAA (ej: 1.1, 1.2, 1.3, 2.1, 2.2) **Y** cada fila muestra el tipo del RAA (ej: "De Conocimiento", "De Destrezas", "Valores y actitudes") **Y** cada fila muestra la descripción completa del RAA **Y** cada fila incluye checkbox para selección **Y** puedo visualizar la lista completa de RAA de la asignatura antes de aplicar cualquier búsqueda **Y** puedo hacer clic en el campo para comenzar a buscar un RAA específico por palabra clave.

---

### **Escenario 2 – Buscar RAA por código o palabra clave exitosamente**

**Dado que** estoy en el Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** se muestra la lista completa de RAA de la asignatura,  
**cuando** hago clic en el campo de búsqueda "Buscar por código o descripción..." **Y** escribo un término que coincide con el código de un RAA (ej: "1.1" o "2.1"),  
**entonces** la tabla se actualiza dinámicamente mientras escribo **Y** se muestran únicamente los RAA cuyo código coincide con el término buscado **Y** los resultados se refinan progresivamente conforme escribo más caracteres **Y** cada RAA filtrado mantiene su estructura completa (código, tipo, descripción, checkbox) **Y** la actualización ocurre en tiempo real sin necesidad de presionar Enter,  
**Y cuando** escribo una palabra clave que coincide con la descripción de un RAA (ej: "conocimiento", "software", "integrar", "tecnología"),  
**entonces** la tabla se actualiza dinámicamente mostrando únicamente los RAA cuya descripción contiene la palabra clave buscada **Y** se muestran todos los RAA relevantes que incluyen esa palabra en su descripción **Y** los resultados se actualizan en tiempo real mientras escribo **Y** cada RAA filtrado mantiene visible su código, tipo, descripción completa y checkbox,  
**Y cuando** la palabra clave coincide en múltiples RAA (búsqueda amplia),  
**entonces** se muestran todos los RAA que tienen coincidencias **Y** encuentro rápidamente el RAA específico que busco para el proceso de vinculación **Y** puedo seleccionar el RAA encontrado mediante su checkbox **Y** si borro el texto del campo de búsqueda, la tabla vuelve a mostrar todos los RAA disponibles automáticamente **Y** la funcionalidad de paginación permanece disponible si hay muchos RAA **Y** puedo continuar con la selección de RAA para avanzar al Paso 2.

---

### **Escenario 3 – Buscar RAA sin resultados coincidentes**

**Dado que** estoy en el Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** el campo de búsqueda está activo,  
**cuando** escribo una palabra clave que NO coincide con ningún código ni descripción de RAA existente (ej: "XXXZZZ" o "PalabraInexistente"),  
**entonces** la búsqueda se ejecuta dinámicamente mientras escribo **Y** la tabla se actualiza mostrando que no hay resultados **Y** se presenta una tabla vacía sin filas de datos **Y** se mantienen visibles los encabezados de columnas "Código", "Tipo", "Descripción" **Y** se indica claramente que no hay RAA que coincidan con la palabra clave buscada **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** puedo modificar la palabra clave para intentar una nueva búsqueda **Y** puedo borrar el texto para volver a ver todos los RAA disponibles **Y** NO se deshabilita ninguna funcionalidad del wizard **Y** puedo continuar buscando con diferentes palabras clave hasta encontrar el RAA específico que necesito para el proceso de vinculación.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Buscar RAA por código o palabra clave exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero buscar resultados de aprendizaje de una asignatura por una palabra clave para encontrar un RA específico en el proceso de vinculación". El Escenario 2 es el único que valida completamente esta funcionalidad: buscar por palabra clave Y encontrar exitosamente el RAA.

2. **Happy path de la búsqueda por palabra clave:** Representa el caso de uso principal donde la búsqueda cumple su propósito: ayudar al coordinador a localizar rápidamente un RAA específico usando términos descriptivos (no solo códigos). Esta es una funcionalidad más potente que la búsqueda simple por código.

3. **Crítico para la usabilidad del Coordinador:** A diferencia del Profesor (que conoce bien sus propios RAA), el Coordinador está revisando asignaturas de otros profesores. La búsqueda por palabra clave es esencial porque:
   - Puede no conocer los códigos exactos de RAA
   - Puede recordar conceptos clave pero no códigos
   - Busca por temas o competencias (ej: "software", "integrar", "tecnología")
   - Necesita encontrar RAA relacionados con temas específicos

4. **Impacto en eficiencia del proceso de vinculación:** En asignaturas con 10-15+ RAA:
   - **Con búsqueda por palabra clave exitosa:** Encuentra RAA en segundos usando términos conceptuales
   - **Sin búsqueda por palabra clave:** Debe leer manualmente todas las descripciones largas de RAA, proceso tedioso y propenso a errores

5. **Validación de búsqueda semántica potente:** Este escenario valida que el sistema:
   - Busca en el CONTENIDO de las descripciones (no solo códigos)
   - Encuentra coincidencias parciales de palabras
   - Soporta búsqueda por términos técnicos y académicos
   - Actualiza resultados dinámicamente mientras se escribe
   - Permite refinamiento progresivo de búsqueda

6. **Crítico para análisis curricular del Coordinador:** Los coordinadores usan esta búsqueda para:
   - Identificar RAA que cubren competencias específicas (ej: buscar "software" para ver todos los RAA relacionados)
   - Analizar distribución de competencias en asignaturas
   - Verificar que ciertos temas están cubiertos
   - Comparar enfoques entre diferentes asignaturas
   - Preparar reportes de cobertura curricular

7. **Diferenciador clave del rol Coordinador:** Mientras el Profesor puede navegar sus propios RAA fácilmente, el Coordinador necesita búsqueda por palabra clave porque:
   - Revisa múltiples asignaturas de diferentes profesores
   - No memoriza códigos de RAA de todas las asignaturas
   - Necesita encontrar RAA por conceptos, no por estructura
   - Realiza análisis temáticos cross-asignatura

8. **Caso de uso frecuente en gestión académica:** Los coordinadores ejecutarán búsquedas por palabra clave constantemente cuando:
   - Vinculan asignaturas con RA de carrera
   - Buscan RAA que aportan a competencias específicas
   - Preparan matrices de trazabilidad
   - Analizan cobertura de temas en el currículo
   - Generan reportes de acreditación

Los escenarios 1 y 3 son importantes para el estado inicial y casos sin resultados, pero el Escenario 2 es el que demuestra la funcionalidad más potente y diferenciadora: permitir al coordinador buscar RAA usando palabras clave conceptuales, no solo códigos numéricos.

Un fallo en este escenario forzaría a los coordinadores a leer manualmente largas listas de descripciones de RAA para encontrar competencias específicas, incrementando dramáticamente el tiempo de análisis y vinculación, y aumentando la probabilidad de omitir RAA relevantes en el proceso de documentación curricular.

Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación, con especial énfasis en la búsqueda dentro de descripciones textuales y actualización dinámica de resultados.