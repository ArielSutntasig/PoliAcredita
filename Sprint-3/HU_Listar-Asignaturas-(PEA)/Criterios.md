# **CRITERIOS DE ACEPTACIÓN - HU: Listar Asignaturas (PEA)**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imagen 4 del Profesor):**

**C1:** Usuario (Profesor) accede a la vista "Asignaturas (PEA)"  
**C2:** Existen asignaturas creadas por el profesor  
**C3:** Cantidad de asignaturas excede límite por página (requiere paginación)

**Nota:** Esta HU se enfoca en la funcionalidad base de listar/visualizar asignaturas, no en búsqueda o paginación específicas (que son HU separadas).

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar título "Asignaturas (PEA)"  
**A2:** Mostrar botón "+ Nueva Asignatura" en esquina superior derecha  
**A3:** Mostrar campo de búsqueda "Buscar por código o descripción..."  
**A4:** Mostrar dropdowns de filtros: "Nivel referencial" y "Créditos"  
**A5:** Mostrar tabla estructurada con columnas definidas  
**A6:** Mostrar columnas: "Código", "Nombre de Asignatura", "Unidad de Integración Curricular", "Créditos", "Nivel Referencial", "Acciones"  
**A7:** Mostrar filas con asignaturas completas con todos sus datos  
**A8:** Mostrar iconos de acciones por cada asignatura: editar (lápiz) y eliminar (papelera roja)  
**A9:** Mostrar controles de paginación (Previous, 1, 2, 3, Next) si hay múltiples páginas  
**A10:** Mostrar tabla vacía con estructura si no hay asignaturas  
**A11:** Permitir visualizar todos los programas de estudio del profesor

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Accede a vista Asignaturas** | F | F | F | F | V | V | V | V |
| **C2: Existen asignaturas** | F | F | V | V | F | F | V | V |
| **C3: Requiere paginación** | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1-A6: Mostrar estructura base | - | - | - | - | X | X | X | X |
| A7-A8: Mostrar asignaturas en tabla | - | - | - | - | - | - | X | X |
| A9: Mostrar paginación | - | - | - | - | - | - | - | X |
| A10: Tabla vacía | - | - | - | - | X | X | - | - |

**Análisis:** R1-R4 son inválidas (usuario no accede a vista).

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** |
|-----------|--------|--------|--------|
| **C1: Accede a vista "Asignaturas (PEA)"** | V | V | V |
| **C2: Existen asignaturas creadas** | F | V | V |
| **C3: Requiere paginación** | - | F | V |
| **ACCIONES** |
| A1-A6: Mostrar estructura completa vista | X | X | X |
| A7-A8: Mostrar filas con asignaturas | - | X | X |
| A9: Mostrar controles paginación | - | - | X |
| A10: Tabla vacía (sin datos) | X | - | - |
| A11: Permitir visualizar programas | - | X | X |

**Justificación de minimización:**

- **R1:** Vista inicial sin asignaturas - muestra estructura vacía.
- **R2:** Vista con asignaturas que caben en una página - lista completa visible.
- **R3:** Vista con múltiples asignaturas - lista con paginación.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 3 reglas

**Criterios de Aceptación finales:** **3 AC**

1. **AC1:** Listar asignaturas cuando no existen programas creados
2. **AC2:** Listar asignaturas existentes en una sola página
3. **AC3:** Listar asignaturas con paginación múltiple

No se detectaron AC redundantes. Cada uno valida un estado distinto de la vista.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Listar asignaturas cuando no existen programas creados**

**Dado que** soy un profesor **Y** estoy autenticado en el sistema **Y** NO tengo asignaturas creadas,  
**cuando** accedo a la vista "Asignaturas (PEA)" desde el menú lateral en la sección "CARRERA",  
**entonces** se muestra el título "Asignaturas (PEA)" en la parte superior **Y** se visualiza el botón "+ Nueva Asignatura" en azul en la esquina superior derecha **Y** se presenta el campo de búsqueda con placeholder "Buscar por código o descripción..." **Y** se muestran los dropdowns de filtros "Nivel referencial" y "Créditos" **Y** se visualiza la estructura de la tabla con los encabezados de columnas: "Código", "Nombre de Asignatura", "Unidad de Integración Curricular", "Créditos", "Nivel Referencial", "Acciones" **Y** la tabla NO contiene filas de datos **Y** se presenta una tabla vacía que indica claramente que no hay asignaturas creadas **Y** los controles de paginación NO se muestran (ya que no hay datos que paginar) **Y** puedo identificar que debo crear asignaturas usando el botón "+ Nueva Asignatura" **Y** la interfaz está lista para que comience a registrar programas de estudio.

---

### **Escenario 2 – Listar asignaturas existentes en una sola página**

**Dado que** soy un profesor **Y** estoy autenticado en el sistema **Y** tengo asignaturas creadas **Y** la cantidad de asignaturas NO excede el límite por página,  
**cuando** accedo a la vista "Asignaturas (PEA)",  
**entonces** se muestra el título "Asignaturas (PEA)" en la parte superior **Y** se visualiza el botón "+ Nueva Asignatura" en azul en la esquina superior derecha **Y** se presenta el campo de búsqueda "Buscar por código o descripción..." visible y funcional **Y** se muestran los dropdowns de filtros "Nivel referencial" y "Créditos" **Y** se visualiza la tabla completa con las columnas "Código", "Nombre de Asignatura", "Unidad de Integración Curricular", "Créditos", "Nivel Referencial", "Acciones" **Y** se presentan todas las filas de asignaturas con sus datos completos **Y** cada fila muestra el código de la asignatura (ej: ISWD414) **Y** cada fila muestra el nombre completo de la asignatura (ej: "Ingeniería de Software y Requerimientos") **Y** cada fila muestra la unidad de integración curricular (ej: "Obligatoria") **Y** cada fila muestra el número de créditos (ej: "2") **Y** cada fila muestra el nivel referencial (ej: "3") **Y** cada fila incluye iconos de acciones: editar (lápiz azul) y eliminar (papelera roja) **Y** los controles de paginación NO se muestran (todas las asignaturas caben en una página) **Y** puedo visualizar todos mis programas de estudio de forma clara y completa **Y** puedo hacer clic en el icono de editar para modificar una asignatura **Y** puedo hacer clic en el icono de eliminar para eliminar una asignatura **Y** puedo usar el botón "+ Nueva Asignatura" para crear nuevos programas.

---

### **Escenario 3 – Listar asignaturas con paginación múltiple**

**Dado que** soy un profesor **Y** estoy autenticado en el sistema **Y** tengo múltiples asignaturas creadas **Y** la cantidad de asignaturas excede el límite de registros por página,  
**cuando** accedo a la vista "Asignaturas (PEA)",  
**entonces** se muestra el título "Asignaturas (PEA)" en la parte superior **Y** se visualiza el botón "+ Nueva Asignatura" en azul en la esquina superior derecha **Y** se presenta el campo de búsqueda "Buscar por código o descripción..." visible y funcional **Y** se muestran los dropdowns de filtros "Nivel referencial" y "Créditos" **Y** se visualiza la tabla con las columnas "Código", "Nombre de Asignatura", "Unidad de Integración Curricular", "Créditos", "Nivel Referencial", "Acciones" **Y** se presentan las filas de asignaturas correspondientes a la página actual con todos sus datos completos **Y** cada fila muestra el código, nombre, unidad de integración, créditos, nivel referencial, e iconos de acciones **Y** se visualizan los controles de paginación en la parte inferior con "Previous, 1, 2, 3, Next" **Y** la página actual está resaltada visualmente **Y** puedo navegar entre páginas para ver todas mis asignaturas usando los números de página o los botones "Previous" y "Next" **Y** puedo visualizar todos mis programas de estudio navegando por las diferentes páginas **Y** obtengo una vista completa de todas las asignaturas que he creado **Y** puedo acceder a las funcionalidades de edición, eliminación y creación desde cualquier página.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Listar asignaturas existentes en una sola página**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero listar las asignaturas para visualizar los programas de estudio". El Escenario 2 valida el caso de uso principal: mostrar asignaturas existentes de forma completa y legible, permitiendo al profesor visualizar efectivamente sus programas.

2. **Happy path con datos reales:** Representa el caso de uso más común y frecuente. La mayoría de los profesores tendrán entre 3-10 asignaturas típicamente, que cabrán en una sola página. Es el escenario que el profesor verá más frecuentemente en su trabajo diario.

3. **Evidencia directa en el prototipo:** La imagen 4 del Profesor muestra específicamente este escenario con asignaturas listadas (ISWD414 visible con datos completos), confirmando que es el caso de uso principal diseñado y esperado.

4. **Punto de entrada fundamental para todas las operaciones:** La vista de listado de asignaturas es el punto de partida para:
   - Acceder a una asignatura para gestionar sus RAA
   - Editar datos de asignaturas existentes
   - Eliminar asignaturas obsoletas
   - Navegar a matrices RAA vs RA
   - Comprender el panorama completo de programas a cargo

5. **Validación de integridad de datos completa:** Este escenario es el único que valida que TODOS los campos de una asignatura se muestran correctamente:
   - **Código:** Identificador único y referencia
   - **Nombre:** Denominación oficial del programa
   - **Unidad de Integración Curricular:** Clasificación académica
   - **Créditos:** Carga académica
   - **Nivel Referencial:** Ubicación curricular
   - **Acciones:** Operaciones disponibles (editar/eliminar)

6. **Valor académico y operativo directo:** La capacidad de "visualizar programas de estudio" solo tiene valor real cuando hay asignaturas para visualizar. Un profesor accede a esta vista principalmente para:
   - Revisar qué programas tiene a cargo
   - Seleccionar una asignatura para trabajar en sus RAA
   - Verificar datos de sus asignaturas
   - Identificar asignaturas que necesitan actualización
   - Obtener una vista panorámica de su carga académica

7. **Base para funcionalidades dependientes:** Este escenario es prerequisito para:
   - Acceder a gestión de RAA de cada asignatura
   - Editar asignaturas (necesita ver la lista primero)
   - Crear matrices RAA vs RA (necesita identificar asignaturas)
   - Usar búsqueda y filtros (necesita datos base para filtrar)

8. **Caso de uso más frecuente en producción:** Los profesores accederán a esta vista constantemente:
   - Al inicio de cada sesión para orientarse
   - Para seleccionar asignatura con la que trabajar
   - Para verificar datos de programas
   - Para acceder a funcionalidades de cada asignatura

Los escenarios 1 y 3 son importantes para validar estados vacíos y paginación, pero el Escenario 2 es el que demuestra que el sistema cumple su propósito fundamental: permitir al profesor listar y visualizar claramente sus programas de estudio con toda la información relevante.

Sin esta visualización correcta, el profesor no puede:
- Identificar qué asignaturas tiene
- Acceder a gestionar RAA de asignaturas específicas
- Verificar la información de sus programas
- Navegar eficientemente por su carga académica

Un fallo en este escenario comprometería la capacidad del profesor de orientarse en el sistema, acceder a sus asignaturas, y realizar su trabajo de documentación curricular. Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación, verificando que todos los datos se muestran completos, correctos y accesibles.