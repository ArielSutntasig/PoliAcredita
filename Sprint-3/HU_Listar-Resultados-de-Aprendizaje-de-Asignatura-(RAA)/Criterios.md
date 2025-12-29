# **CRITERIOS DE ACEPTACIÓN - HU: Listar Resultados de Aprendizaje de Asignatura (RAA)**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imagen 7 del Profesor):**

**C1:** Usuario está en contexto de una asignatura (desde vista "Crear/Editar Asignatura (PEA)")  
**C2:** Usuario hace clic en el tab "Resultados de Aprendizaje (RAA)"  
**C3:** Existen RAA definidos para la asignatura  
**C4:** Cantidad de RAA excede límite por página (requiere paginación)

**Nota:** La imagen 7 muestra el tab activo con RAA listados en una tabla estructurada, con paginación visible.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar título "Crear/Editar Resultados de Aprendizaje Asignatura (RAA)"  
**A2:** Mantener visible el tab "Resultados de Aprendizaje (RAA)" activo (resaltado)  
**A3:** Mostrar botón "+ Nuevo RAA" en azul en esquina superior derecha  
**A4:** Mostrar tabla estructurada con columnas: "Código", "Tipo", "Descripción", "Acciones"  
**A5:** Mostrar filas con RAA existentes con todos sus datos completos  
**A6:** Mostrar código de cada RAA (ej: 1.1, 1.2, 2.1)  
**A7:** Mostrar tipo de cada RAA (ej: "De Conocimiento", "De Destrezas", "Valores y actitudes")  
**A8:** Mostrar descripción completa de cada RAA (ej: "Conocer los componentes, tecnología, información e impacto social de los sistemas de información")  
**A9:** Mostrar iconos de acciones por cada RAA: editar (lápiz) y eliminar (papelera roja)  
**A10:** Mostrar controles de paginación (Previous, 1, 2, 3, Next) si hay múltiples páginas  
**A11:** Mostrar botón "Cancelar" en la parte inferior derecha  
**A12:** Mostrar tabla vacía con estructura pero sin datos si no hay RAA  
**A13:** Permitir visualizar todas las competencias específicas de la asignatura

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En contexto de asignatura** | F | F | F | F | V | V | V | V |
| **C2: Clic en tab RAA** | F | F | V | V | F | F | V | V |
| **C3: Existen RAA** | F | V | F | V | F | V | F | V |
| **C4: Requiere paginación** | F | F | F | F | F | V | F | V |
| **ACCIONES** |
| A1-A4: Mostrar estructura base | - | - | - | - | - | - | X | X |
| A5-A9: Mostrar RAA en tabla | - | - | - | - | - | - | - | X |
| A10: Mostrar paginación | - | - | - | - | - | - | - | X |
| A11: Mostrar botón Cancelar | - | - | - | - | - | - | X | X |
| A12: Tabla vacía | - | - | - | - | - | - | X | - |
| A13: Visualizar competencias | - | - | - | - | - | - | - | X |

**Análisis:** R1-R6 son estados inválidos donde el usuario no está en contexto de asignatura o no ha accedido al tab RAA.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** |
|-----------|--------|--------|--------|
| **C1: En contexto de asignatura** | V | V | V |
| **C2: Accede a tab "Resultados de Aprendizaje (RAA)"** | V | V | V |
| **C3: Existen RAA definidos** | F | V | V |
| **C4: Requiere paginación (múltiples páginas)** | - | F | V |
| **ACCIONES** |
| A1: Mostrar título | X | X | X |
| A2: Tab RAA activo | X | X | X |
| A3: Mostrar botón "+ Nuevo RAA" | X | X | X |
| A4: Mostrar estructura de tabla (columnas) | X | X | X |
| A5-A9: Mostrar filas con RAA completos | - | X | X |
| A10: Mostrar paginación | - | - | X |
| A11: Mostrar botón "Cancelar" | X | X | X |
| A12: Tabla vacía (sin datos) | X | - | - |
| A13: Permitir visualizar competencias | - | X | X |

**Justificación de minimización:**

- **Eliminadas R1-R6:** Representan estados donde el usuario no está en el flujo correcto (sin contexto de asignatura o sin acceder al tab), lo cual está fuera del alcance de esta HU.
- **R1:** Usuario accede al tab RAA pero no hay RAA definidos - muestra estructura vacía.
- **R2:** Usuario accede al tab RAA con RAA existentes que caben en una página - lista completa visible.
- **R3:** Usuario accede al tab RAA con múltiples RAA que requieren paginación - lista con paginación.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 3 reglas

**Análisis:** Cada regla representa un escenario válido de visualización de la lista de RAA:
1. Lista vacía (sin RAA)
2. Lista con RAA (sin paginación)
3. Lista con RAA (con paginación)

**Criterios de Aceptación finales:** **3 AC**

No se detectaron AC redundantes. Cada uno valida un estado distinto de la funcionalidad de listado.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Listar RAA cuando no existen resultados definidos**

**Dado que** soy un profesor **Y** estoy en la vista "Crear/Editar Asignatura (PEA)" de una asignatura **Y** la asignatura NO tiene RAA definidos,  
**cuando** hago clic en el tab "Resultados de Aprendizaje (RAA)",  
**entonces** se muestra el título "Crear/Editar Resultados de Aprendizaje Asignatura (RAA)" en la parte superior **Y** el tab "Resultados de Aprendizaje (RAA)" se muestra activo y resaltado **Y** se visualiza el botón "+ Nuevo RAA" en azul en la esquina superior derecha **Y** se muestra la estructura de la tabla con los encabezados de columnas: "Código", "Tipo", "Descripción", "Acciones" **Y** la tabla NO contiene filas de datos **Y** se presenta una tabla vacía que indica claramente que no hay RAA definidos para esta asignatura **Y** el botón "Cancelar" está visible en la parte inferior derecha **Y** los controles de paginación NO se muestran (ya que no hay datos que paginar) **Y** puedo identificar que debo crear RAA usando el botón "+ Nuevo RAA" para definir las competencias específicas de la asignatura.

---

### **Escenario 2 – Listar RAA existentes en una sola página**

**Dado que** soy un profesor **Y** estoy en la vista "Crear/Editar Asignatura (PEA)" de una asignatura **Y** la asignatura tiene RAA definidos **Y** la cantidad de RAA NO excede el límite por página,  
**cuando** hago clic en el tab "Resultados de Aprendizaje (RAA)",  
**entonces** se muestra el título "Crear/Editar Resultados de Aprendizaje Asignatura (RAA)" **Y** el tab "Resultados de Aprendizaje (RAA)" está activo y resaltado **Y** se visualiza el botón "+ Nuevo RAA" en azul en la esquina superior derecha **Y** se muestra la tabla completa con las columnas "Código", "Tipo", "Descripción", "Acciones" **Y** se presentan todas las filas de RAA con sus datos completos **Y** cada fila muestra el código del RAA (ej: 1.1, 1.2, 1.3, 2.1, 2.2) **Y** cada fila muestra el tipo del RAA (ej: "De Conocimiento", "De Destrezas", "Valores y actitudes") **Y** cada fila muestra la descripción completa del RAA (ej: "Conocer los componentes, tecnología, información e impacto social de los sistemas de información") **Y** cada fila incluye iconos de acciones: editar (lápiz) y eliminar (papelera roja) **Y** el botón "Cancelar" está visible en la parte inferior derecha **Y** los controles de paginación NO se muestran (todos los RAA caben en una página) **Y** puedo visualizar todas las competencias específicas de la asignatura de forma clara y completa para entender qué conocimientos, destrezas y valores debe desarrollar el estudiante.

---

### **Escenario 3 – Listar RAA existentes con paginación múltiple**

**Dado que** soy un profesor **Y** estoy en la vista "Crear/Editar Asignatura (PEA)" de una asignatura **Y** la asignatura tiene múltiples RAA definidos **Y** la cantidad de RAA excede el límite de registros por página,  
**cuando** hago clic en el tab "Resultados de Aprendizaje (RAA)",  
**entonces** se muestra el título "Crear/Editar Resultados de Aprendizaje Asignatura (RAA)" **Y** el tab "Resultados de Aprendizaje (RAA)" está activo y resaltado **Y** se visualiza el botón "+ Nuevo RAA" en azul en la esquina superior derecha **Y** se muestra la tabla con las columnas "Código", "Tipo", "Descripción", "Acciones" **Y** se presentan las filas de RAA correspondientes a la página actual con todos sus datos completos **Y** cada fila muestra el código, tipo y descripción completa del RAA **Y** cada fila incluye iconos de acciones: editar (lápiz) y eliminar (papelera roja) **Y** se visualizan los controles de paginación en la parte inferior con "Previous, 1, 2, 3, Next" **Y** la página actual está resaltada visualmente **Y** puedo navegar entre páginas para ver todos los RAA usando los números de página o los botones "Previous" y "Next" **Y** el botón "Cancelar" está visible en la parte inferior derecha **Y** puedo visualizar todas las competencias específicas de la asignatura navegando por las diferentes páginas **Y** obtengo una vista completa de todos los resultados de aprendizaje que definen las capacidades que deben alcanzar los estudiantes en esta asignatura.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Listar RAA existentes en una sola página**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumple directamente el objetivo de la Historia de Usuario:** La HU establece "Quiero listar los resultados de aprendizaje de una asignatura para visualizar sus competencias específicas". El Escenario 2 valida el caso de uso principal: mostrar RAA existentes de forma completa y legible, permitiendo al profesor visualizar efectivamente las competencias.

2. **Happy path con datos reales:** Representa el caso de uso más común y frecuente en producción. La mayoría de las asignaturas tendrán RAA definidos (entre 3-10 típicamente), y estos cabrán en una sola página. Es el escenario que el profesor verá más frecuentemente en su trabajo diario.

3. **Evidencia directa en el prototipo:** La imagen 7 muestra específicamente este escenario con múltiples RAA listados (códigos 1.1, descripción completa visible), confirmando que es el caso de uso principal diseñado y esperado en el sistema.

4. **Validación de integridad de datos:** Este escenario es el único que valida que TODOS los componentes de un RAA se muestran correctamente:
   - Código (identificador único)
   - Tipo (categoría académica: Conocimiento, Destrezas, Valores)
   - Descripción completa (la competencia específica textual)
   - Acciones disponibles (editar/eliminar)

5. **Valor académico directo:** La capacidad de "visualizar competencias específicas" solo tiene valor real cuando hay RAA para visualizar. Un profesor accede a esta vista principalmente para:
   - Revisar qué competencias están definidas
   - Validar la completitud de RAA
   - Verificar la correcta redacción de competencias
   - Preparar documentación académica o para acreditación
   - Identificar qué RAA necesitan edición o actualización

6. **Base para otras funcionalidades:** Este escenario es prerequisito para funcionalidades relacionadas como:
   - Editar RAA (necesita ver la lista primero)
   - Crear matriz RAA vs RA (necesita confirmar qué RAA existen)
   - Evaluar cobertura de competencias de la asignatura

Los escenarios 1 y 3 son importantes para validar estados vacíos y paginación, pero el Escenario 2 es el que demuestra que el sistema cumple su propósito fundamental: permitir al profesor ver claramente las competencias específicas que define su asignatura. Sin esta visualización correcta, el profesor no puede cumplir su objetivo de "visualizar competencias específicas" que es el valor central de la HU.

Un fallo en este escenario comprometería la capacidad del profesor de revisar, validar y gestionar las competencias académicas de su asignatura, impactando directamente en la calidad del diseño curricular y la documentación de acreditación. Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación.