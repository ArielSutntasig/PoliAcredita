# **CRITERIOS DE ACEPTACIÓN - HU: Filtrar Asignaturas por Nivel Referencial**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imagen 4 del Profesor):**

**C1:** Usuario está en vista "Asignaturas (PEA)"  
**C2:** Dropdown "Nivel referencial" tiene nivel seleccionado  
**C3:** Nivel seleccionado tiene asignaturas asociadas  
**C4:** Existen asignaturas creadas por el profesor

**Nota:** La imagen 4 muestra explícitamente el dropdown "Nivel referencial" junto al dropdown "Créditos". El nivel referencial indica en qué semestre/nivel de la malla curricular se dicta la asignatura (1, 2, 3, 4, 5, 6, etc.).

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar dropdown "Nivel referencial" visible y funcional  
**A2:** Mostrar opciones de niveles disponibles en dropdown (1, 2, 3, 4, 5, 6, etc.)  
**A3:** Mostrar todas las asignaturas sin filtrar (estado inicial)  
**A4:** Filtrar tabla mostrando solo asignaturas del nivel referencial seleccionado  
**A5:** Actualizar tabla automáticamente al seleccionar nivel  
**A6:** Ocultar asignaturas que no pertenecen al nivel seleccionado  
**A7:** Mantener iconos de acciones (editar/eliminar) en asignaturas filtradas  
**A8:** Combinar filtro con búsqueda por código/descripción si está activa  
**A9:** Combinar con otros filtros (Créditos, Periodo académico) si están activos  
**A10:** Permitir cambiar de nivel o quitar filtro  
**A11:** Actualizar paginación según cantidad de resultados filtrados  
**A12:** Mantener estructura de tabla completa

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En vista Asignaturas** | F | F | F | F | V | V | V | V |
| **C2: Nivel seleccionado** | F | F | V | V | F | F | V | V |
| **C3: Nivel tiene asignaturas** | F | V | F | V | F | V | F | V |
| **C4: Existen asignaturas** | F | F | F | F | V | V | V | V |
| **ACCIONES** |
| A1-A3: Mostrar sin filtrar | - | - | - | - | - | X | - | - |
| A4-A7: Filtrar por nivel | - | - | - | - | - | - | - | X |

**Análisis:** R1-R4 son inválidas (fuera de vista o sin asignaturas base).

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** |
|-----------|--------|--------|--------|
| **C1: En vista "Asignaturas (PEA)"** | V | V | V |
| **C2: Dropdown nivel con selección** | F | V | V |
| **C3: Nivel tiene asignaturas asociadas** | - | F | V |
| **C4: Existen asignaturas creadas** | V | V | V |
| **ACCIONES** |
| A1-A2: Dropdown visible con opciones | X | X | X |
| A3: Mostrar todas las asignaturas (sin filtrar) | X | - | - |
| A4-A6: Filtrar por nivel seleccionado | - | - | X |
| A5: Actualizar tabla automáticamente | - | X | X |
| A7-A12: Mantener funcionalidad completa | X | X | X |
| Mostrar tabla vacía (nivel sin asignaturas) | - | X | - |

**Justificación de minimización:**

- **R1:** Estado inicial sin filtro - muestra todas las asignaturas.
- **R2:** Nivel seleccionado pero sin asignaturas en ese nivel - tabla vacía.
- **R3:** Nivel seleccionado con asignaturas - muestra solo asignaturas de ese nivel (happy path).

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 3 reglas

**Criterios de Aceptación finales:** **3 AC**

1. **AC1:** Visualizar dropdown de nivel referencial sin filtro aplicado
2. **AC2:** Filtrar asignaturas por nivel referencial exitosamente
3. **AC3:** Seleccionar nivel sin asignaturas asociadas

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar dropdown de nivel referencial sin filtro aplicado**

**Dado que** soy un profesor **Y** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas,  
**cuando** visualizo la vista sin haber aplicado ningún filtro de nivel referencial,  
**entonces** se muestra el dropdown "Nivel referencial" visible en la parte superior junto al campo de búsqueda y otros filtros **Y** el dropdown está sin selección (mostrando placeholder o valor por defecto "Todos" o similar) **Y** al hacer clic en el dropdown se despliegan las opciones de niveles referenciales disponibles (ej: "1", "2", "3", "4", "5", "6") **Y** se presenta la tabla con TODAS mis asignaturas sin filtrado por nivel **Y** cada asignatura muestra su código, nombre, unidad de integración, créditos, nivel referencial e iconos de acciones **Y** puedo ver asignaturas de todos los niveles mezcladas en la lista (ej: nivel 1, nivel 2, nivel 3, etc.) **Y** el campo de búsqueda y otros filtros (Créditos, Periodo académico) permanecen visibles y funcionales **Y** puedo comenzar a filtrar por nivel cuando necesite ver solo programas de un nivel específico de la malla curricular.

---

### **Escenario 2 – Filtrar asignaturas por nivel referencial exitosamente**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas en diferentes niveles referenciales de la malla curricular **Y** el dropdown "Nivel referencial" está visible,  
**cuando** hago clic en el dropdown "Nivel referencial" **Y** selecciono un nivel específico (ej: "3" para tercer semestre/nivel),  
**entonces** el dropdown se cierra mostrando "3" como valor seleccionado **Y** la tabla se actualiza automáticamente mostrando únicamente las asignaturas que pertenecen al nivel referencial 3 **Y** se ocultan todas las asignaturas de otros niveles (1, 2, 4, 5, 6, etc.) **Y** cada asignatura filtrada mantiene su estructura completa con código (ej: ISWD414), nombre (ej: "Ingeniería de Software y Requerimientos"), unidad de integración, créditos, nivel referencial (mostrando "3"), e iconos de editar y eliminar **Y** puedo ver claramente los programas que se dictan en ese nivel específico de la malla curricular **Y** la funcionalidad de búsqueda por código/descripción sigue disponible y se combina con este filtro **Y** los otros filtros (Créditos, Periodo académico) permanecen disponibles y se pueden combinar con el filtro de nivel **Y** puedo cambiar a otro nivel o quitar el filtro haciendo clic nuevamente en el dropdown y seleccionando otra opción **Y** la paginación se actualiza según la cantidad de asignaturas del nivel seleccionado **Y** el botón "+ Nueva Asignatura" permanece visible y funcional **Y** he filtrado exitosamente mis asignaturas para ver solo los programas activos en un nivel específico de la estructura curricular.

---

### **Escenario 3 – Seleccionar nivel sin asignaturas asociadas**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas **Y** existe un nivel referencial en el dropdown,  
**cuando** hago clic en el dropdown "Nivel referencial" **Y** selecciono un nivel en el que NO tengo asignaturas registradas (ej: "6" si no dicto clases en sexto semestre),  
**entonces** el dropdown se cierra mostrando "6" como valor seleccionado **Y** la tabla se actualiza mostrando que no hay resultados **Y** se presenta una tabla vacía sin filas de asignaturas **Y** se mantienen visibles los encabezados de columnas de la tabla **Y** se indica claramente que no hay asignaturas asociadas a ese nivel referencial **Y** puedo seleccionar otro nivel del dropdown para ver asignaturas de otro nivel **Y** puedo quitar el filtro para volver a ver todas mis asignaturas **Y** el botón "+ Nueva Asignatura" permanece visible si deseo crear una asignatura para ese nivel **Y** obtengo feedback claro de que no tengo programas asignados en ese nivel específico de la malla curricular.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Filtrar asignaturas por nivel referencial exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero filtrar las asignaturas por Nivel referencial para ver los programas activos en un ciclo". El Escenario 2 es el único que valida completamente esta funcionalidad: filtrar por nivel referencial Y visualizar los programas específicos de ese nivel.

2. **Happy path de la funcionalidad de filtrado por ubicación curricular:** Representa el caso de uso principal donde el filtro cumple su propósito: permitir al profesor enfocarse en asignaturas de un nivel específico de la malla, separándolas de las de otros niveles o semestres.

3. **Evidencia directa en el prototipo:** La imagen 4 muestra explícitamente el dropdown "Nivel referencial" como uno de los filtros disponibles, confirmando que es una funcionalidad diseñada y esperada. El ejemplo visible muestra "3" como nivel referencial de una asignatura.

4. **Impacto en organización por estructura curricular:** Los profesores frecuentemente enseñan asignaturas en múltiples niveles de la malla curricular:
   - **Nivel 1-2:** Asignaturas de fundamentos (típicamente con más estudiantes)
   - **Nivel 3-4:** Asignaturas de formación profesional
   - **Nivel 5-6+:** Asignaturas de especialización o culminación
   
   El filtro permite enfocarse en asignaturas del nivel que actualmente están dictando.

5. **Caso de uso frecuente en planificación académica:** El filtro por nivel será usado regularmente porque:
   - Profesores preparan material diferente según nivel de madurez académica de estudiantes
   - RAA deben ajustarse a complejidad apropiada para cada nivel
   - Revisión de asignaturas se organiza por nivel curricular
   - Coordinación con colegas se facilita agrupando por nivel

6. **Validación de coherencia curricular:** Este escenario valida que el sistema:
   - Asocia correctamente asignaturas a niveles en la malla curricular
   - Filtra basándose en esa asociación estructural
   - Mantiene la integridad de la estructura curricular
   - No mezcla información de niveles diferentes
   - Refleja correctamente la organización del plan de estudios

7. **Facilitación de análisis de progresión curricular:** El filtro permite al profesor:
   - Ver cómo se distribuyen sus asignaturas en la malla
   - Identificar en qué niveles tiene mayor carga
   - Analizar progresión de complejidad entre niveles
   - Preparar documentación por nivel para acreditación
   - Coordinar con asignaturas prerequisito del nivel anterior

8. **Integración con lógica académica estándar:** El nivel referencial es un concepto fundamental en educación superior:
   - Define ubicación de asignatura en malla curricular
   - Determina prerequisitos y correquisitos
   - Indica nivel de complejidad esperado
   - Estructura la progresión del aprendizaje
   - Es requisito en reportes de acreditación

9. **Combinación con otros filtros para búsqueda precisa:** Este escenario valida que el filtro:
   - Se combina correctamente con búsqueda por código/descripción
   - Se combina con filtro por Créditos
   - Se combina con filtro por Periodo académico
   - Permite filtrado multidimensional (ej: "asignaturas de 2 créditos del nivel 3 del periodo 2025-1")
   - No interfiere con otras funcionalidades

10. **Eficiencia operativa para profesores con amplio portafolio:** Un profesor con 10-15 asignaturas distribuidas en 4-5 niveles puede reducir su vista de 15 asignaturas a 3-4 del nivel específico que está preparando, mejorando dramáticamente la eficiencia.

Los escenarios 1 y 3 son importantes para el estado inicial y casos sin datos, pero el Escenario 2 es el que demuestra el valor real: permitir al profesor filtrar y visualizar eficientemente solo los programas de un nivel específico de la malla curricular, facilitando trabajo organizado por estructura académica.

Un fallo en este escenario comprometería la capacidad del profesor de organizar su trabajo por niveles curriculares, obligándolo a navegar por listas mezcladas de asignaturas de todos los niveles, complicando la preparación de material apropiado para cada nivel de madurez académica de los estudiantes.

Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación, verificando que el filtrado refleja correctamente la estructura de la malla curricular y que las asignaturas se muestran según su nivel referencial definido.