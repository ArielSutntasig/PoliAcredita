# **CRITERIOS DE ACEPTACIÓN - HU: Filtrar Asignaturas por Periodo Académico (PEA)**

---

## **NOTA IMPORTANTE SOBRE ANÁLISIS DE IMÁGENES**

En las imágenes del prototipo analizadas previamente (imagen 4 del Profesor que muestra la vista "Asignaturas (PEA)"), he observado:
- ✅ Campo de búsqueda "Buscar por código o descripción..."
- ✅ Dropdown "Nivel referencial"
- ✅ Dropdown "Créditos"
- ❌ NO he identificado explícitamente un dropdown "Periodo académico"

Sin embargo, dado que:
1. La HU lo solicita explícitamente
2. Es una funcionalidad lógica en sistemas académicos
3. Sigue el patrón de filtros del sistema observado

Procederé a generar los AC basándome en el **patrón consistente de filtros dropdown** observado en el sistema y la **lógica académica estándar**.

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU e inferencia del patrón del sistema):**

**C1:** Usuario está en vista "Asignaturas (PEA)"  
**C2:** Dropdown "Periodo académico" tiene periodo seleccionado  
**C3:** Periodo seleccionado tiene asignaturas asociadas  
**C4:** Existen asignaturas creadas por el profesor

**Nota:** Los periodos académicos típicamente son semestrales (ej: 2024-1, 2024-2, 2025-1).

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar dropdown "Periodo académico" visible y funcional  
**A2:** Mostrar opciones de periodos disponibles en dropdown  
**A3:** Mostrar todas las asignaturas sin filtrar (estado inicial)  
**A4:** Filtrar tabla mostrando solo asignaturas del periodo seleccionado  
**A5:** Actualizar tabla automáticamente al seleccionar periodo  
**A6:** Ocultar asignaturas que no pertenecen al periodo seleccionado  
**A7:** Mantener checkboxes y acciones (editar/eliminar) en asignaturas filtradas  
**A8:** Combinar filtro con búsqueda por código/descripción si está activa  
**A9:** Combinar con otros filtros (Nivel referencial, Créditos) si están activos  
**A10:** Permitir cambiar de periodo o quitar filtro  
**A11:** Actualizar paginación según cantidad de resultados filtrados  
**A12:** Mantener estructura de tabla completa

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En vista Asignaturas** | F | F | F | F | V | V | V | V |
| **C2: Periodo seleccionado** | F | F | V | V | F | F | V | V |
| **C3: Periodo tiene asignaturas** | F | V | F | V | F | V | F | V |
| **C4: Existen asignaturas** | F | F | F | F | V | V | V | V |
| **ACCIONES** |
| A1-A3: Mostrar sin filtrar | - | - | - | - | - | X | - | - |
| A4-A7: Filtrar por periodo | - | - | - | - | - | - | - | X |

**Análisis:** R1-R4 son inválidas (fuera de vista o sin asignaturas base).

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** |
|-----------|--------|--------|--------|
| **C1: En vista "Asignaturas (PEA)"** | V | V | V |
| **C2: Dropdown periodo con selección** | F | V | V |
| **C3: Periodo tiene asignaturas asociadas** | - | F | V |
| **C4: Existen asignaturas creadas** | V | V | V |
| **ACCIONES** |
| A1-A2: Dropdown visible con opciones | X | X | X |
| A3: Mostrar todas las asignaturas (sin filtrar) | X | - | - |
| A4-A6: Filtrar por periodo seleccionado | - | - | X |
| A5: Actualizar tabla automáticamente | - | X | X |
| A7-A12: Mantener funcionalidad completa | X | X | X |
| Mostrar tabla vacía (periodo sin asignaturas) | - | X | - |

**Justificación de minimización:**

- **R1:** Estado inicial sin filtro - muestra todas las asignaturas.
- **R2:** Periodo seleccionado pero sin asignaturas en ese periodo - tabla vacía o mensaje.
- **R3:** Periodo seleccionado con asignaturas - muestra solo asignaturas activas en ese ciclo (happy path).

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 3 reglas

**Criterios de Aceptación finales:** **3 AC**

1. **AC1:** Visualizar dropdown de periodo sin filtro aplicado
2. **AC2:** Filtrar asignaturas por periodo académico exitosamente
3. **AC3:** Seleccionar periodo sin asignaturas asociadas

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar dropdown de periodo sin filtro aplicado**

**Dado que** soy un profesor **Y** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas,  
**cuando** visualizo la vista sin haber aplicado ningún filtro de periodo académico,  
**entonces** se muestra el dropdown "Periodo académico" visible en la parte superior junto a los otros filtros **Y** el dropdown está sin selección (mostrando placeholder o valor por defecto "Todos" o similar) **Y** al hacer clic en el dropdown se despliegan las opciones de periodos académicos disponibles (ej: "2024-1", "2024-2", "2025-1") **Y** se presenta la tabla con TODAS mis asignaturas sin filtrado por periodo **Y** cada asignatura muestra su código, nombre, unidad de integración, créditos, nivel referencial e iconos de acciones **Y** puedo ver el listado completo de todas mis asignaturas independientemente del periodo en que se dictan **Y** los campos de búsqueda y otros filtros (Nivel referencial, Créditos) permanecen visibles y funcionales **Y** puedo comenzar a filtrar por periodo cuando necesite ver solo programas de un ciclo específico.

---

### **Escenario 2 – Filtrar asignaturas por periodo académico exitosamente**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas en diferentes periodos académicos **Y** el dropdown "Periodo académico" está visible,  
**cuando** hago clic en el dropdown "Periodo académico" **Y** selecciono un periodo específico (ej: "2025-1" para primer semestre de 2025),  
**entonces** el dropdown se cierra mostrando el periodo seleccionado como valor activo **Y** la tabla se actualiza automáticamente mostrando únicamente las asignaturas que están asociadas al periodo académico seleccionado **Y** se ocultan todas las asignaturas de otros periodos académicos **Y** cada asignatura filtrada mantiene su estructura completa con código, nombre, unidad de integración, créditos, nivel referencial e iconos de editar y eliminar **Y** puedo ver claramente los programas activos en ese ciclo específico **Y** la funcionalidad de búsqueda por código/descripción sigue disponible y se combina con este filtro **Y** los otros filtros (Nivel referencial, Créditos) permanecen disponibles y se pueden combinar con el filtro de periodo **Y** puedo cambiar a otro periodo o quitar el filtro haciendo clic nuevamente en el dropdown **Y** la paginación se actualiza según la cantidad de asignaturas del periodo seleccionado **Y** el botón "+ Nueva Asignatura" permanece visible y funcional **Y** he filtrado exitosamente mis asignaturas para ver solo los programas de estudio activos en el ciclo académico seleccionado.

---

### **Escenario 3 – Seleccionar periodo sin asignaturas asociadas**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** tengo asignaturas creadas **Y** existe un periodo académico en el dropdown,  
**cuando** hago clic en el dropdown "Periodo académico" **Y** selecciono un periodo en el que NO tengo asignaturas registradas (ej: "2023-2" si no dicté clases ese semestre),  
**entonces** el dropdown se cierra mostrando el periodo seleccionado **Y** la tabla se actualiza mostrando que no hay resultados **Y** se presenta una tabla vacía sin filas de asignaturas **Y** se mantienen visibles los encabezados de columnas de la tabla **Y** se indica claramente que no hay asignaturas asociadas a ese periodo académico **Y** puedo seleccionar otro periodo del dropdown para ver asignaturas de otro ciclo **Y** puedo quitar el filtro para volver a ver todas mis asignaturas **Y** el botón "+ Nueva Asignatura" permanece visible si deseo crear una asignatura para ese periodo **Y** obtengo feedback claro de que no tengo programas activos en ese ciclo específico.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Filtrar asignaturas por periodo académico exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero filtrar las asignaturas por periodo académico para ver los programas activos en un ciclo". El Escenario 2 es el único que valida completamente esta funcionalidad: filtrar por periodo Y visualizar los programas activos en ese ciclo específico.

2. **Happy path de la funcionalidad de filtrado temporal:** Representa el caso de uso principal donde el filtro cumple su propósito: permitir al profesor enfocarse en las asignaturas relevantes para un periodo académico específico, separándolas de las de otros semestres o años.

3. **Impacto crítico en organización del trabajo académico:** Los profesores típicamente trabajan con asignaturas de diferentes periodos:
   - **Periodo actual:** Asignaturas que están dictando AHORA
   - **Periodo anterior:** Asignaturas del semestre pasado (para referencia o reporte)
   - **Periodo futuro:** Asignaturas en planificación para próximo ciclo
   
   Sin filtrado por periodo, la lista se vuelve confusa y difícil de navegar.

4. **Caso de uso más frecuente en trabajo diario:** El filtro por periodo será usado constantemente porque:
   - Profesores trabajan principalmente con asignaturas del periodo actual
   - Necesitan actualizar RAA de asignaturas activas
   - Deben enfocarse en programas que están dictando HOY
   - Revisan asignaturas de periodos pasados ocasionalmente para referencia

5. **Validación de lógica temporal crítica:** Este escenario valida que el sistema:
   - Asocia correctamente asignaturas a periodos académicos
   - Filtra basándose en esa asociación temporal
   - Mantiene la integridad de datos entre periodos
   - No mezcla información de ciclos diferentes
   - Actualiza la vista automáticamente

6. **Prevención de errores por confusión temporal:** Sin este filtro funcionando correctamente:
   - Profesor puede editar asignatura del semestre pasado creyendo que es la actual
   - Puede crear RAA en versión incorrecta de la asignatura
   - Puede perder tiempo buscando entre asignaturas de múltiples años
   - Puede tomar decisiones basándose en información del periodo equivocado

7. **Alineación con calendario académico:** Los periodos académicos son fundamentales en educación:
   - Definen cuándo se dictan asignaturas
   - Determinan vigencia de programas
   - Marcan ciclos de evaluación y acreditación
   - Estructuran la planificación académica
   
   El filtro permite trabajar alineado con esta realidad temporal.

8. **Integración con otras funcionalidades:** Este escenario valida que el filtro:
   - Se combina correctamente con búsqueda por código/descripción
   - Se combina con otros filtros (Nivel referencial, Créditos)
   - No interfiere con creación de nuevas asignaturas
   - Mantiene iconos de edición y eliminación funcionales
   - Actualiza correctamente la paginación

9. **Eficiencia operativa:** Con asignaturas acumuladas de múltiples periodos (ej: un profesor con 3-5 años de historia podría tener 20-30 asignaturas totales), el filtro reduce listas de 30 asignaturas a 5-8 del periodo actual, mejorando dramáticamente la eficiencia.

10. **Preparación para reportes por periodo:** Los reportes académicos y de acreditación frecuentemente se organizan por periodo. Este filtro permite al profesor:
    - Verificar qué asignaturas dictó en periodo específico
    - Preparar documentación por ciclo académico
    - Analizar evolución de programas entre periodos

Los escenarios 1 y 3 son importantes para el estado inicial y casos sin datos, pero el Escenario 2 es el que demuestra el valor real: permitir al profesor filtrar y visualizar eficientemente solo los programas activos en un ciclo académico específico, eliminando el "ruido" de asignaturas de otros periodos.

Un fallo en este escenario comprometería severamente la usabilidad del sistema para profesores con historial académico, obligándolos a navegar manualmente por listas mezcladas de asignaturas de múltiples años, incrementando la probabilidad de trabajar con el periodo equivocado y perdiendo tiempo valioso en identificar qué asignaturas son las actualmente relevantes.

Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación, con especial énfasis en la correcta asociación temporal de asignaturas a periodos y la actualización precisa de la vista filtrada.