# CRITERIOS DE ACEPTACIÓN - HU: Visualizar materia al crear RAA

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**C1: Asignatura seleccionada/activa**
- Estado: Sí / No
- Fuente: Contexto del sistema - la asignatura debe estar seleccionada para mostrar sus RAA
- Observado en imagen: "Ingeniería de Software y Requerimientos (ISWD414)" visible en encabezado principal
- Resultado: La materia es el contexto necesario para crear RAA

**C2: Pestaña "Resultados de Aprendizaje (RAA)" activa**
- Estado: Sí / No
- Fuente: Sistema de pestañas en la parte superior
- Observado: Pestaña "Resultados de Aprendizaje (RAA)" con fondo azul oscuro (activa)
- Otras pestañas disponibles: "Asignatura (PEA)", "Matriz RAA vs RA"

**C3: Usuario inicia creación de nuevo RAA**
- Estado: Sí / No
- Fuente: Click en botón "+ Nuevo RAA"
- Observado: Botón visible en esquina superior derecha
- Acción: Abre formulario/modal para crear un nuevo RAA

#### **Acciones del sistema identificadas:**

**A1: Mostrar nombre completo de la asignatura en encabezado**
- Condición: Asignatura seleccionada
- Observado: "Ingeniería de Software y Requerimientos (ISWD414)"
- Formato: Nombre completo + código entre paréntesis
- Ubicación: Encabezado principal de la página
- Resultado: Profesor sabe exactamente en qué materia está trabajando

**A2: Mostrar pestaña RAA activa con lista de RAA existentes**
- Condición: Pestaña "Resultados de Aprendizaje (RAA)" activa
- Elementos observados:
  - Tabla con columnas: Código, Tipo, Descripción, Acciones
  - Múltiples RAA existentes (todos con código 1.1 en la imagen)
  - Tipo: "De Conocimiento"
  - Descripciones completas visibles
  - Iconos de editar (lápiz) y eliminar (papelera)
  - Sistema de paginación (Previous, 1, 2, 3, Next)

**A3: Mostrar botón "+ Nuevo RAA" habilitado**
- Condición: Asignatura seleccionada y pestaña RAA activa
- Observado: Botón azul oscuro en esquina superior derecha
- Estado: Habilitado y clickeable
- Propósito: Permitir crear nuevos RAA para la asignatura

**A4: Abrir formulario de creación de RAA con contexto de materia**
- Condición: Usuario hace click en "+ Nuevo RAA"
- Comportamiento esperado: 
  - Abre modal o formulario de creación
  - Mantiene visible el nombre de la asignatura
  - Formulario incluye campos para código, tipo y descripción del RAA
- Resultado: Profesor puede crear RAA con contexto claro de la materia

**A5: No mostrar contexto de asignatura (caso negativo)**
- Condición: No hay asignatura seleccionada
- Resultado: Usuario no puede acceder a crear RAA sin contexto de materia

**A6: Mostrar solo nombre de asignatura sin acceso a creación**
- Condición: Asignatura seleccionada pero pestaña RAA no activa
- Resultado: Nombre visible pero sin funcionalidad de creación de RAA

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Asignatura | C2: Pestaña RAA | C3: Inicia creación | Acción del Sistema |
|-------|----------------|----------------|---------------------|-------------------|
| R1    | No             | No             | No                  | A5: No mostrar contexto de asignatura |
| R2    | No             | No             | Sí                  | A5: No mostrar contexto (imposible crear*) |
| R3    | No             | Sí             | No                  | A5: No mostrar contexto (estado imposible**) |
| R4    | No             | Sí             | Sí                  | A5: No mostrar contexto (estado imposible**) |
| R5    | Sí             | No             | No                  | A1 + A6: Mostrar nombre de asignatura sin acceso RAA |
| R6    | Sí             | No             | Sí                  | A1 + A6: Mostrar nombre sin acceso (click imposible***) |
| R7    | Sí             | Sí             | No                  | A1 + A2 + A3: Vista lista RAA con botón Nuevo RAA visible |
| R8    | Sí             | Sí             | Sí                  | A1 + A2 + A3 + A4: Abrir formulario con materia visible (HAPPY PATH) |

*Imposible crear: No se puede hacer click en "+ Nuevo RAA" sin tener asignatura
**Estado imposible: Si no hay asignatura, no se puede acceder a la pestaña RAA de esa asignatura
***Click imposible: Si no está en pestaña RAA, el botón "+ Nuevo RAA" no está visible

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Reglas R1-R4:** Todas resultan en no mostrar contexto de asignatura cuando Asignatura=No. Sin asignatura seleccionada, no tiene sentido acceder a sus RAA ni crear nuevos. Las otras condiciones son irrelevantes o imposibles. **Se fusionan en M1**.

2. **Reglas R5-R6:** Cuando hay asignatura pero la pestaña RAA no está activa (usuario puede estar en "Asignatura (PEA)" o "Matriz RAA vs RA"), solo se muestra el nombre pero no hay acceso a crear RAA. El intento de crear es imposible porque el botón no está visible. **Se fusionan en M2**.

3. **Regla R7:** Cuando asignatura y pestaña RAA están activas pero el usuario aún no ha iniciado la creación, se muestra la vista de lista con el botón "+ Nuevo RAA" visible. **Se mantiene como M3**.

4. **Regla R8:** Cuando el usuario hace click en "+ Nuevo RAA", se abre el formulario de creación manteniendo visible el nombre de la asignatura. Este es el escenario principal de la HU. **Se mantiene como M4 (HAPPY PATH)**.

#### **Tabla Minimizada:**

| Regla Min | C1: Asignatura | C2: Pestaña RAA | C3: Inicia creación | Acción del Sistema |
|-----------|----------------|----------------|---------------------|-------------------|
| **M1**    | No             | -              | -                   | A5: No mostrar contexto de asignatura |
| **M2**    | Sí             | No             | -                   | A1 + A6: Mostrar nombre en otra pestaña |
| **M3**    | Sí             | Sí             | No                  | A1 + A2 + A3: Vista lista RAA con materia visible |
| **M4**    | Sí             | Sí             | Sí                  | A1 + A2 + A3 + A4: Formulario creación con materia visible |

**Resultado: 4 reglas minimizadas**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 4 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre ausencia de asignatura (caso negativo)
2. M2 → AC sobre asignatura seleccionada pero otra pestaña activa
3. M3 → AC sobre vista lista RAA con materia visible (prerequisito del happy path)
4. M4 → AC sobre creación de RAA con materia visible (HAPPY PATH)

**Análisis de criterios adicionales necesarios:**

Del objetivo de la HU ("observar la materia al crear un RAA para definir correctamente el RAA de la materia"):

5. **Persistencia del nombre durante el proceso de creación:** El nombre de la asignatura debe mantenerse visible durante todo el flujo de creación del RAA, no solo al inicio.

**Criterios a ELIMINAR por redundancia:**

- **M1 (Sin asignatura):** Este es un caso negativo que no aporta valor a la funcionalidad principal de "observar la materia al crear RAA". Es un prerequisito del sistema (debe haber asignatura seleccionada), no un criterio de aceptación de esta HU específica. **ELIMINADO por ser prerequisito del sistema**.

- **M2 (Asignatura pero otra pestaña):** Este escenario no cumple el objetivo de la HU. El usuario no está creando RAA, está en otra funcionalidad. **ELIMINADO por no cumplir objetivo de la HU**.

- **Criterio adicional de persistencia (punto 5):** Este comportamiento se validará dentro del criterio M4 (happy path), no requiere un criterio separado. **CONSOLIDADO en M4**.

**TOTAL FINAL: 2 Criterios de Aceptación**
- 1 de M3 (vista lista RAA con materia visible - prerequisito)
- 1 de M4 (creación de RAA con materia visible - happy path)

**Justificación de eliminaciones:**
- **M1:** Prerequisito del sistema, no funcionalidad específica de esta HU
- **M2:** No cumple objetivo de "crear RAA", usuario está en otra pestaña
- **Persistencia durante creación:** Consolidado en M4, no requiere criterio separado

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

---

### **Escenario 1 – Visualizar materia en vista de lista de RAA antes de crear**

**Dado que** soy un profesor en el sistema **Y** he seleccionado la asignatura "Ingeniería de Software y Requerimientos (ISWD414)",
**cuando** hago clic en la pestaña "Resultados de Aprendizaje (RAA)" en el menú de navegación,
**entonces** se muestra el nombre completo de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" en el encabezado principal de la página **Y** la pestaña "Resultados de Aprendizaje (RAA)" se presenta con fondo azul oscuro indicando que está activa **Y** se muestra una tabla con los RAA existentes de la asignatura con las columnas: Código, Tipo, Descripción, Acciones **Y** se presenta el botón "+ Nuevo RAA" en la esquina superior derecha de color azul oscuro **Y** el botón está habilitado y es clickeable **Y** el nombre de la asignatura permanece claramente visible permitiéndome confirmar que estoy en el contexto correcto antes de crear un nuevo RAA.

---

### **Escenario 2 – Visualizar materia al iniciar creación de nuevo RAA**

**Dado que** estoy visualizando la lista de RAA de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" **Y** la pestaña "Resultados de Aprendizaje (RAA)" está activa **Y** el nombre de la asignatura es visible en el encabezado,
**cuando** hago clic en el botón "+ Nuevo RAA",
**entonces** se abre un formulario o modal para crear un nuevo RAA **Y** el nombre completo de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" permanece visible en el encabezado durante todo el proceso de creación **Y** el formulario incluye campos para definir el código, tipo y descripción del nuevo RAA **Y** el contexto de la materia está claro en todo momento permitiéndome definir correctamente el RAA de esta asignatura específica **Y** no hay ambigüedad sobre para qué materia estoy creando el RAA **Y** puedo proceder con confianza sabiendo que el RAA se asociará correctamente a "Ingeniería de Software y Requerimientos (ISWD414)".

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 2 – Visualizar materia al iniciar creación de nuevo RAA**

### **Justificación:**

Este criterio es el más crítico porque valida **directamente el objetivo central de la Historia de Usuario**: "observar la materia al crear un RAA para definir correctamente el RAA de la materia". Las razones específicas son:

1. **Cumplimiento literal del objetivo de la HU:** El profesor necesita **observar la materia al crear un RAA**. Este escenario valida que:
   - El nombre de la asignatura es visible cuando inicia la creación (click en "+ Nuevo RAA")
   - El nombre permanece visible durante el proceso de creación
   - El profesor tiene confirmación visual constante del contexto
   - No hay ambigüedad sobre para qué materia está creando el RAA

2. **Prevención de errores académicos críticos:** Sin la visibilidad del nombre de la asignatura durante la creación, el profesor podría:
   - Crear un RAA pensando que está en una materia diferente
   - Asignar incorrectamente el RAA a la asignatura equivocada
   - Perder tiempo creando RAA que luego debe reasignar o eliminar
   - Causar inconsistencias en la trazabilidad curricular
   - Afectar la documentación de acreditación
   
   Este escenario previene todos estos errores al garantizar contexto visual constante.

3. **Momento crítico de toma de decisión:** El momento de "crear RAA" es cuando el profesor:
   - Define los objetivos de aprendizaje de la asignatura
   - Estructura el contenido académico de la materia
   - Establece las bases para la evaluación
   - Crea documentación que será usada por años
   
   Un error en este momento tiene consecuencias a largo plazo. El contexto visual (nombre de materia) es la salvaguarda contra estos errores.

4. **Validación de persistencia del contexto:** No basta con mostrar el nombre de la asignatura en la lista de RAA (Escenario 1). El contexto debe **persistir** cuando se abre el formulario de creación. Este escenario valida que:
   - El nombre no desaparece al abrir el formulario
   - No hay transición que pierda el contexto
   - El encabezado se mantiene visible durante toda la interacción
   - El profesor nunca pierde de vista qué materia está editando

5. **Punto de no retorno en el flujo:** Una vez que el profesor empieza a llenar el formulario de creación de RAA:
   - Invierte tiempo pensando en el contenido del RAA
   - Escribe descripciones detalladas
   - Define el tipo de RAA (De Conocimiento, De Aplicación, etc.)
   
   Si en este punto descubre que está en la materia incorrecta, ha perdido tiempo valioso. Este escenario previene esta situación al mantener el contexto visible desde el inicio.

6. **Base para creación correcta de RAA:** Para "definir correctamente el RAA de la materia" (objetivo final de la HU), el profesor necesita:
   - Saber con certeza en qué materia está trabajando
   - Tener ese conocimiento visible, no solo en memoria
   - Poder verificar el contexto en cualquier momento durante la creación
   - Crear el RAA con confianza de que será asociado correctamente

7. **Evidencia de que alcanza el happy path:** El Escenario 1 es importante pero es solo el prerequisito. El Escenario 2 es el que valida la acción principal: **crear un RAA**. Sin este escenario funcionando:
   - El profesor puede ver la lista de RAA con contexto (Escenario 1)
   - Pero al intentar crear uno nuevo, podría perder el contexto
   - La funcionalidad principal de la HU quedaría incompleta

8. **Patrón de usabilidad crítico:** Mantener el contexto visible durante operaciones de creación/edición es un principio fundamental de UX. Los usuarios necesitan saber "dónde están y qué están haciendo" en todo momento. Este escenario valida este principio en el momento más crítico: cuando están creando contenido académico importante.

9. **Punto de fallo de mayor impacto funcional:** Si este escenario falla:
   - El profesor podría crear RAA sin saber para qué materia
   - Se podrían asignar RAA a asignaturas incorrectas
   - La integridad de datos académicos se vería comprometida
   - Los procesos de acreditación tendrían información errónea
   - La trazabilidad curricular sería incorrecta

10. **Diferenciador clave entre asignaturas:** En un sistema donde un profesor puede tener múltiples asignaturas:
    - "Ingeniería de Software y Requerimientos (ISWD414)"
    - "Programación Avanzada (ISWD312)"
    - "Bases de Datos (ISWD305)"
    
    Es fácil confundirse sobre en cuál está trabajando. El nombre visible constante es la única forma de prevenir esta confusión durante la creación de RAA.

11. **Dependencia del Escenario 1:** El Escenario 1 establece el contexto inicial, pero el Escenario 2 valida que ese contexto se **mantiene** durante la acción crítica. Sin ambos, la funcionalidad está incompleta, pero el Escenario 2 es más crítico porque:
    - Es donde ocurre la creación real del RAA
    - Es donde el error tendría más consecuencias
    - Es el punto de no retorno en el flujo

12. **Validación de integración UI durante transición:** Este escenario valida que la arquitectura UI mantiene el contexto cuando:
    - Se abre un modal/formulario (posible cambio de capa visual)
    - Se cambia de vista de lista a vista de creación
    - Se ejecutan acciones JavaScript/AJAX
    - Se actualiza el DOM sin reload de página
    
    Todas estas transiciones técnicas podrían "perder" el contexto si no están bien implementadas.

**Recomendación de prueba prioritaria:**
- Validar que el nombre de asignatura permanece visible al hacer click en "+ Nuevo RAA"
- Verificar que el nombre no desaparece durante el proceso de creación
- Confirmar que el nombre se muestra correctamente incluso con asignaturas de nombres largos
- Probar con múltiples asignaturas para confirmar que el nombre se actualiza correctamente
- Validar que si se cancela la creación y se selecciona otra asignatura, el contexto cambia correctamente
- Verificar que el formulario de creación incluye campos apropiados (código, tipo, descripción)
- Incluir en regresión crítica para cambios en navegación o contexto de asignatura
- Probar en diferentes tamaños de pantalla para confirmar que el nombre siempre es visible

**Sin este escenario funcionando, el profesor no puede "observar la materia al crear un RAA"** en el momento crítico de la creación, lo cual es el núcleo de esta HU. Podría ver la materia en la lista (Escenario 1), pero al iniciar la creación perdería ese contexto visual, haciendo imposible "definir correctamente el RAA de la materia" porque no tendría confirmación visual de para qué materia está creando el RAA. El contexto persistente durante la creación es lo que convierte esta funcionalidad de meramente técnica a genuinamente útil y segura para el usuario.