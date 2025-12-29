# **CRITERIOS DE ACEPTACIÓN - HU: Filtrar Asignaturas por Créditos**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imagen 4 del Profesor):**

**C1:** Usuario está en vista "Asignaturas (PEA)"  
**C2:** Dropdown "Créditos" tiene valor seleccionado  
**C3:** Valor de créditos seleccionado tiene asignaturas asociadas  
**C4:** Existen asignaturas creadas por el profesor

**Nota:** La imagen 4 muestra explícitamente el dropdown "Créditos" junto a "Nivel referencial". Los créditos representan la carga académica de cada asignatura (ej: 1, 2, 3, 4, 5 créditos).

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar dropdown "Créditos" visible y funcional  
**A2:** Mostrar opciones de créditos disponibles en dropdown (1, 2, 3, 4, 5, 6, etc.)  
**A3:** Mostrar todas las asignaturas sin filtrar (estado inicial)  
**A4:** Filtrar tabla mostrando solo asignaturas del valor de créditos seleccionado  
**A5:** Actualizar tabla automáticamente al seleccionar créditos  
**A6:** Ocultar asignaturas con diferente valor de créditos  
**A7:** Mantener iconos de acciones (editar/eliminar) en asignaturas filtradas  
**A8:** Combinar filtro con búsqueda por código/descripción si está activa  
**A9:** Combinar con otros filtros (Nivel referencial, Periodo académico) si están activos  
**A10:** Permitir cambiar valor de créditos o quitar filtro  
**A11:** Actualizar paginación según cantidad de resultados filtrados  
**A12:** Mantener estructura de tabla completa

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En vista Asignaturas** | F | F | F | F | V | V | V | V |
| **C2: Créditos seleccionados** | F | F | V | V | F | F | V | V |
| **C3: Créditos tienen asignaturas** | F | V | F | V | F | V | F | V |
| **C4: Existen asignaturas** | F | F | F | F | V | V | V | V |
| **ACCIONES** |
| A1-A3: Mostrar sin filtrar | - | - | - | - | - | X | - | - |
| A4-A7: Filtrar por créditos | - | - | - | - | - | - | - | X |

**Análisis:** R1-R4 son inválidas (fuera de vista o sin asignaturas base).

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** |
|-----------|--------|--------|--------|
| **C1: En vista "Asignaturas (PEA)"** | V | V | V |
| **C2: Dropdown créditos con selección** | F | V | V |
| **C3: Créditos tienen asignaturas** | - | F | V |
| **C4: Existen asignaturas creadas** | V | V | V |
| **ACCIONES** |
| A1-A2: Dropdown visible con opciones | X | X | X |
| A3: Mostrar todas las asignaturas (sin filtrar) | X | - | - |
| A4-A6: Filtrar por créditos seleccionados | - | - | X |
| A5: Actualizar tabla automáticamente | - | X | X |
| A7-A12: Mantener funcionalidad completa | X | X | X |
| Mostrar tabla vacía (créditos sin asignaturas) | - | X | - |

**Justificación de minimización:**

- **R1:** Estado inicial sin filtro - muestra todas las asignaturas.
- **R2:** Créditos seleccionados pero sin asignaturas con ese valor - tabla vacía.
- **R3:** Créditos seleccionados con asignaturas - muestra solo asignaturas de ese valor (happy path).

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 3 reglas

**Criterios de Aceptación finales:** **3 AC**

1. **AC1:** Visualizar dropdown de créditos sin filtro aplicado
2. **AC2:** Filtrar asignaturas por créditos exitosamente
3. **AC3:** Seleccionar créditos sin asignaturas asociadas

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar dropdown de créditos sin filtro aplicado**

**Dado que** soy un profesor **Y** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas,  
**cuando** visualizo la vista sin haber aplicado ningún filtro de créditos,  
**entonces** se muestra el dropdown "Créditos" visible en la parte superior junto al campo de búsqueda y otros filtros **Y** el dropdown está sin selección (mostrando placeholder o valor por defecto "Todos" o similar) **Y** al hacer clic en el dropdown se despliegan las opciones de créditos disponibles (ej: "1", "2", "3", "4", "5", "6") **Y** se presenta la tabla con TODAS mis asignaturas sin filtrado por créditos **Y** cada asignatura muestra su código, nombre, unidad de integración, créditos (pudiendo ser valores variados como 2, 3, 4), nivel referencial e iconos de acciones **Y** puedo ver asignaturas con diferentes valores de créditos mezcladas en la lista **Y** el campo de búsqueda y otros filtros (Nivel referencial, Periodo académico) permanecen visibles y funcionales **Y** puedo comenzar a filtrar por créditos cuando necesite acotar la búsqueda a asignaturas de carga académica específica.

---

### **Escenario 2 – Filtrar asignaturas por créditos exitosamente**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas con diferentes valores de créditos **Y** el dropdown "Créditos" está visible,  
**cuando** hago clic en el dropdown "Créditos" **Y** selecciono un valor específico de créditos (ej: "2" para asignaturas de 2 créditos),  
**entonces** el dropdown se cierra mostrando "2" como valor seleccionado **Y** la tabla se actualiza automáticamente mostrando únicamente las asignaturas que tienen 2 créditos asignados **Y** se ocultan todas las asignaturas con otros valores de créditos (1, 3, 4, 5, 6, etc.) **Y** cada asignatura filtrada mantiene su estructura completa con código, nombre, unidad de integración, créditos (mostrando "2"), nivel referencial, e iconos de editar y eliminar **Y** puedo ver claramente los programas que tienen la carga académica específica de 2 créditos **Y** la funcionalidad de búsqueda por código/descripción sigue disponible y se combina con este filtro **Y** los otros filtros (Nivel referencial, Periodo académico) permanecen disponibles y se pueden combinar con el filtro de créditos **Y** puedo cambiar a otro valor de créditos o quitar el filtro haciendo clic nuevamente en el dropdown y seleccionando otra opción **Y** la paginación se actualiza según la cantidad de asignaturas del valor de créditos seleccionado **Y** el botón "+ Nueva Asignatura" permanece visible y funcional **Y** he acotado exitosamente la búsqueda a asignaturas con un plan de estudios específico según su carga de créditos.

---

### **Escenario 3 – Seleccionar créditos sin asignaturas asociadas**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas **Y** existe un valor de créditos en el dropdown,  
**cuando** hago clic en el dropdown "Créditos" **Y** selecciono un valor de créditos en el que NO tengo asignaturas registradas (ej: "6" si no dicto asignaturas de 6 créditos),  
**entonces** el dropdown se cierra mostrando "6" como valor seleccionado **Y** la tabla se actualiza mostrando que no hay resultados **Y** se presenta una tabla vacía sin filas de asignaturas **Y** se mantienen visibles los encabezados de columnas de la tabla **Y** se indica claramente que no hay asignaturas con ese valor de créditos **Y** puedo seleccionar otro valor de créditos del dropdown para ver asignaturas con otra carga académica **Y** puedo quitar el filtro para volver a ver todas mis asignaturas **Y** el botón "+ Nueva Asignatura" permanece visible si deseo crear una asignatura con ese valor de créditos **Y** obtengo feedback claro de que no tengo programas con esa carga académica específica de créditos.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Filtrar asignaturas por créditos exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero filtrar las asignaturas por crédito para acotar la búsqueda a un plan de estudios específico". El Escenario 2 es el único que valida completamente esta funcionalidad: filtrar por créditos Y acotar efectivamente la búsqueda.

2. **Happy path de filtrado por carga académica:** Representa el caso de uso principal donde el filtro cumple su propósito: permitir al profesor enfocarse en asignaturas con un valor específico de créditos, que representa su peso en el plan de estudios.

3. **Evidencia directa en el prototipo:** La imagen 4 muestra explícitamente el dropdown "Créditos" junto a "Nivel referencial", y los datos de la tabla muestran asignaturas con valores de créditos (ej: "2"), confirmando que es una funcionalidad diseñada y esperada.

4. **Importancia de créditos en estructura académica:** Los créditos son fundamentales en educación superior porque:
   - **Definen carga de trabajo:** Un crédito ≈ horas de trabajo del estudiante
   - **Estructuran el plan:** Total de créditos = requisito de graduación
   - **Clasifican asignaturas:** Materias teóricas (2-3 créditos) vs prácticas/proyectos (4-6 créditos)
   - **Determinan horarios:** Más créditos = más horas semanales de clase

5. **Caso de uso frecuente en gestión académica:** El filtro por créditos será usado regularmente porque:
   - Profesores gestionan asignaturas de diferentes cargas
   - Necesitan identificar materias ligeras vs intensivas
   - Preparan diferente volumen de material según créditos
   - Coordinan disponibilidad según carga académica total
   - Verifican distribución equilibrada de su carga docente

6. **Facilitación de planificación docente:** El filtro permite al profesor:
   - Ver cuántas asignaturas de alta carga (4-5 créditos) tiene
   - Identificar materias de menor carga (2-3 créditos)
   - Planificar tiempo de preparación según créditos totales
   - Balancear esfuerzo entre asignaturas de diferente peso
   - Verificar coherencia de su carga docente con normativas

7. **Alineación con políticas institucionales:** Las instituciones frecuentemente tienen:
   - Límites de créditos por docente (ej: máximo 18-20 créditos/semestre)
   - Equivalencias créditos-horas de clase
   - Normas de carga académica balanceada
   - Reportes por distribución de créditos
   
   El filtro facilita verificar cumplimiento de estas políticas.

8. **Integración con análisis de carga docente:** Este escenario valida que el filtro:
   - Se combina con búsqueda por código/descripción
   - Se combina con filtros de Nivel referencial y Periodo
   - Permite identificar rápidamente asignaturas por peso académico
   - Facilita cálculo de carga total docente
   - No interfiere con otras funcionalidades

9. **Validación de coherencia de datos:** El filtro debe mostrar correctamente las asignaturas según el valor de créditos registrado, validando que:
   - Los créditos están asignados correctamente a cada asignatura
   - El filtrado refleja estos valores con precisión
   - No hay inconsistencias en la base de datos
   - La información académica es confiable

10. **Eficiencia operativa:** Un profesor con 10-12 asignaturas distribuidas en 2-5 créditos puede reducir su vista de 12 asignaturas a 3-4 del valor de créditos específico que está planificando, mejorando dramáticamente la eficiencia en la organización de su trabajo.

Los escenarios 1 y 3 son importantes para el estado inicial y casos sin datos, pero el Escenario 2 es el que demuestra el valor real: permitir al profesor filtrar y visualizar eficientemente solo los programas con una carga académica específica, facilitando gestión organizada según peso de las asignaturas en el plan de estudios.

Un fallo en este escenario comprometería la capacidad del profesor de organizar su trabajo por carga académica, obligándolo a identificar manualmente en listas mezcladas qué asignaturas tienen qué valor de créditos, complicando la planificación docente y verificación de carga académica total.

Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación, verificando que el filtrado refleja correctamente los valores de créditos definidos para cada asignatura.