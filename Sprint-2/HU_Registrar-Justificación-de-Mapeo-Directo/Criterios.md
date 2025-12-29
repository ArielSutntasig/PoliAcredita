# **ANÁLISIS COMPLETO - HU: Registrar Justificación de Mapeo Directo**

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **PASO 1: LISTA DE CONDICIONES Y ACCIONES**

#### **📋 CONDICIONES IDENTIFICADAS:**

**C1:** Usuario tiene rol de Coordinador de Carrera (**V** = Sí, **F** = No)

**C2:** Existe una relación previamente creada en la celda de la matriz (**V** = Sí, **F** = No)

**C3:** La relación seleccionada ya tiene una justificación guardada (**V** = Sí, **F** = No)

**C4:** Campo de justificación está completo/modificado (**V** = Sí, **F** = No)

---

#### **⚙️ ACCIONES RESULTANTES:**

**A1:** Sistema permite abrir el formulario de justificación directa

**A2:** Sistema muestra mensaje de error "No tiene permisos para realizar esta acción"

**A3:** Sistema muestra mensaje "No existe una relación en esta celda. Debe crear la relación primero."

**A4:** Sistema muestra el formulario con la justificación existente cargada en el campo de texto

**A5:** Sistema muestra el formulario con el campo de justificación vacío

**A6:** Sistema guarda la nueva justificación y muestra notificación "Se guardó la justificación correctamente"

**A7:** Sistema actualiza la justificación existente y muestra notificación "Se actualizó la justificación correctamente"

**A8:** Sistema muestra mensaje de validación "Debe completar el campo de justificación"

---

#### **📸 ANÁLISIS VISUAL DE COMPONENTES DE UI (inferidos del patrón del sistema):**

Basándome en las imágenes de matrices (12, 16, 17) y el formulario de justificación del wizard (imagen 15), el flujo de "mapeo directo" funcionaría así:

**Acceso desde la Matriz:**
- Usuario hace clic en un checkmark verde (✓) existente en la matriz OPP vs RA o RA vs EUR-ACE
- Alternativamente, hace clic en el ícono de información (ℹ️) junto a una relación existente

**Formulario de Justificación Directa (modal o panel lateral):**
- **Título**: "Justificación de Relación"
- **Sección "Elementos Relacionados:"** (solo lectura)
  - Primer elemento: Código y descripción (ej: "OPP3: Aplicar metodologías ágiles...")
  - Segundo elemento: Código y descripción (ej: "RG3: Aplicar metodologías ágiles...")
- **Campo de texto multilínea**: "Justificación:"
  - Si existe justificación previa, se muestra el texto guardado
  - Si es nueva, el campo está vacío con placeholder
- **Botones**:
  - "Cancelar" (rojo, izquierda)
  - "Guardar" (azul, derecha)

**Diferencia clave con el wizard:**
- NO hay 3 pasos secuenciales
- Los elementos ya están relacionados (no se seleccionan)
- Solo se edita/añade la justificación
- Acceso inmediato desde la matriz

---

### **PASO 2: TABLA DE DECISIÓN COMPLETA (MAXIMIZADA)**

Con 4 condiciones, tenemos **2^4 = 16 reglas teóricas posibles**.

| **Regla** | **C1** | **C2** | **C3** | **C4** | **Acciones** |
|-----------|--------|--------|--------|--------|--------------|
| R1 | V | V | V | V | A1, A4, A7 ✅ **MODIFICAR (Happy Path)** |
| R2 | V | V | V | F | A1, A4, A8 |
| R3 | V | V | F | V | A1, A5, A6 ✅ **AÑADIR (Happy Path)** |
| R4 | V | V | F | F | A1, A5, A8 |
| R5 | V | F | V | V | A1, A3 |
| R6 | V | F | V | F | A1, A3 |
| R7 | V | F | F | V | A1, A3 |
| R8 | V | F | F | F | A1, A3 |
| R9 | F | V | V | V | A2 |
| R10 | F | V | V | F | A2 |
| R11 | F | V | F | V | A2 |
| R12 | F | V | F | F | A2 |
| R13 | F | F | V | V | A2 |
| R14 | F | F | V | F | A2 |
| R15 | F | F | F | V | A2 |
| R16 | F | F | F | F | A2 |

---

### **PASO 3: TABLA DE DECISIÓN MINIMIZADA**

#### **Análisis de Minimización:**

**Grupo 1 - Sin permisos (C1=F):**
Las reglas R9-R16 (8 reglas) producen la acción A2 independientemente de C2, C3 y C4.
**→ Se fusionan en R_MIN1**

**Grupo 2 - Sin relación existente (C1=V, C2=F):**
Las reglas R5-R8 (4 reglas) producen las acciones A1, A3 independientemente de C3 y C4.
Nota: C3 es técnicamente imposible si C2=F (no puede haber justificación sin relación).
**→ Se fusionan en R_MIN2**

**Grupo 3 - Justificación vacía al guardar (C1=V, C2=V, C4=F):**
Las reglas R2 y R4 producen las acciones A1, (A4 o A5), A8 independientemente de C3.
**→ Se fusionan en R_MIN3**

**Reglas únicas:**
- **R1** (Modificar justificación existente): C1=V, C2=V, C3=V, C4=V → Happy path para MODIFICAR
- **R3** (Añadir justificación nueva): C1=V, C2=V, C3=F, C4=V → Happy path para AÑADIR

#### **🎯 TABLA MINIMIZADA FINAL:**

| **Regla** | **C1** | **C2** | **C3** | **C4** | **Acciones** | **Descripción** |
|-----------|--------|--------|--------|--------|--------|--------------|
| **R_MIN1** | **F** | **-** | **-** | **-** | **A2** | Usuario sin permisos |
| **R_MIN2** | **V** | **F** | **-** | **-** | **A1, A3** | No existe relación en celda |
| **R_MIN3** | **V** | **V** | **-** | **F** | **A1, A4/A5, A8** | Campo justificación vacío |
| **R_MIN4** ✅ | **V** | **V** | **V** | **V** | **A1, A4, A7** | **Modificar justificación existente** |
| **R_MIN5** ✅ | **V** | **V** | **F** | **V** | **A1, A5, A6** | **Añadir nueva justificación** |

**Reducción: De 16 reglas → 5 reglas (68.75% de reducción)**

---

### **PASO 4: NÚMERO TOTAL DE CRITERIOS DE ACEPTACIÓN**

**Número final: 5 Criterios de Aceptación**

#### **Justificación:**

✅ **Se mantienen los 5 AC derivados de la tabla minimizada** porque cada uno valida un escenario único:

1. **R_MIN1**: Validación de seguridad/permisos
2. **R_MIN2**: Validación de prerequisito (debe existir relación)
3. **R_MIN3**: Validación de campo obligatorio
4. **R_MIN4**: Flujo de MODIFICACIÓN de justificación existente (CRÍTICO)
5. **R_MIN5**: Flujo de AÑADIR justificación nueva (CRÍTICO)

❌ **No se eliminan criterios** porque:
- Esta HU tiene un propósito específico: **edición directa desde matriz** (no wizard)
- Aunque usa componentes visuales similares (formulario de justificación), el **contexto y flujo son diferentes**
- Los criterios R_MIN4 y R_MIN5 son **complementarios** (modificar vs añadir) y ambos son casos de uso principales
- No hay redundancia con las HUs del wizard porque:
  - **Wizard**: Crea relación NUEVA con justificación (3 pasos: seleccionar elemento 1 → seleccionar elemento 2 → justificar)
  - **Esta HU**: Edita justificación de relación EXISTENTE (acceso directo: click en matriz → editar justificación)

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (FORMATO GHERKIN)**

### **AC1 - Modificar justificación de relación existente (HAPPY PATH - Modificar)**

**Dado que** soy un Coordinador de Carrera autenticado en el sistema

**Y** estoy visualizando la matriz "Objetivos de Carrera (OPP) y Resultados de Aprendizaje (RA)" o "Resultados de Aprendizaje (RA) y Criterios EUR-ACE"

**Y** existe una celda con un checkmark verde (✓) que representa una relación entre OPP3 y RG3

**Y** esta relación ya tiene una justificación guardada previamente

**Cuando** hago clic directamente sobre el checkmark verde (✓) o el ícono de información (ℹ️) de esa celda

**Entonces** se abre un formulario modal o panel lateral con título "Justificación de Relación"

**Y** se muestra la sección "Elementos Relacionados:" en modo solo lectura con:
   - Primer elemento con código y descripción completa (ej: "OPP3: Aplicar metodologías ágiles en la gestión de proyectos de software")
   - Segundo elemento con código y descripción completa (ej: "RG3: Aplicar metodologías ágiles en la gestión de proyectos de software")

**Y** se muestra el campo "Justificación:" con el texto de la justificación actual ya cargado

**Y** el cursor se posiciona automáticamente en el campo de texto

**Y** se muestran los botones "Cancelar" (rojo) y "Guardar" (azul).

**Cuando** modifico el texto de la justificación (añado, elimino o cambio contenido)

**Y** hago clic en el botón "Guardar"

**Entonces** el sistema guarda la justificación modificada

**Y** se cierra el formulario modal/panel

**Y** se muestra una notificación emergente con:
   - Ícono de check verde (✓)
   - Título "Completado"
   - Mensaje "Se actualizó la justificación correctamente"
   - Botón "X" para cerrar

**Y** el checkmark verde (✓) en la matriz permanece visible sin cambios

**Y** al hacer clic nuevamente en el checkmark, se muestra la justificación actualizada.

---

### **AC2 - Añadir justificación a relación existente sin justificación (HAPPY PATH - Añadir)**

**Dado que** soy un Coordinador de Carrera autenticado en el sistema

**Y** estoy visualizando una matriz con relaciones

**Y** existe una celda con un checkmark verde (✓) que representa una relación entre dos elementos

**Y** esta relación NO tiene una justificación guardada (fue creada sin justificación o la justificación fue eliminada)

**Cuando** hago clic directamente sobre el checkmark verde (✓) de esa celda

**Entonces** se abre el formulario "Justificación de Relación"

**Y** se muestra la sección "Elementos Relacionados:" con ambos elementos

**Y** se muestra el campo "Justificación:" completamente vacío

**Y** se muestra un placeholder en el campo: "Escribe tu justificación detallada aquí para la relación entre los elementos seleccionados."

**Y** se muestran los botones "Cancelar" y "Guardar".

**Cuando** escribo una justificación válida en el campo de texto (mínimo 10 caracteres)

**Y** hago clic en el botón "Guardar"

**Entonces** el sistema guarda la nueva justificación

**Y** se cierra el formulario

**Y** se muestra una notificación emergente con:
   - Ícono de check verde (✓)
   - Título "Completado"
   - Mensaje "Se guardó la justificación correctamente"

**Y** el checkmark en la matriz permanece visible

**Y** al hacer clic nuevamente en el checkmark, se muestra la justificación recién añadida.

---

### **AC3 - Intento de acceso sin permisos de Coordinador de Carrera**

**Dado que** estoy autenticado en el sistema

**Y** NO tengo asignado el rol de "Coordinador de Carrera"

**Y** estoy visualizando una matriz de relaciones (como observador o con rol diferente)

**Cuando** intento hacer clic en un checkmark verde (✓) de cualquier celda con relación

**Entonces** el sistema NO abre el formulario de justificación

**Y** se muestra un mensaje de error "No tiene permisos para realizar esta acción"

**Y** el checkmark permanece visible pero no es interactivo para mí

**Y** NO puedo modificar ni añadir justificaciones a ninguna relación.

---

### **AC4 - Intento de añadir justificación en celda sin relación**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** estoy visualizando la matriz de relaciones

**Cuando** hago clic en una celda vacía que NO tiene un checkmark verde (✓)

**O** intento interactuar con una celda sin relación establecida

**Entonces** el sistema NO abre el formulario de justificación

**Y** se muestra un mensaje informativo "No existe una relación en esta celda. Debe crear la relación primero."

**Y** se sugiere al usuario usar el botón "+ Nueva Relación" para crear la relación mediante el wizard

**Y** la celda permanece vacía sin cambios.

---

### **AC5 - Validación de campo justificación obligatorio**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** he abierto el formulario de justificación desde un checkmark en la matriz

**Y** el formulario muestra los elementos relacionados y el campo de justificación

**Cuando** dejo el campo "Justificación:" completamente vacío (sin texto)

**O** borro todo el contenido de una justificación existente dejándolo vacío

**Y** hago clic en el botón "Guardar"

**Entonces** el sistema NO guarda los cambios

**Y** se muestra un mensaje de validación "Debe completar el campo de justificación"

**Y** el campo de justificación se resalta visualmente con un borde rojo o indicador de error

**Y** el formulario permanece abierto

**Y** puedo escribir la justificación o hacer clic en "Cancelar" para cerrar sin guardar.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **🎯 CRITERIOS MÁS CRÍTICOS (EMPATE):**

**AC1 - Modificar justificación de relación existente (HAPPY PATH - Modificar)**

**AC2 - Añadir justificación a relación existente sin justificación (HAPPY PATH - Añadir)**

---

### **✅ JUSTIFICACIÓN DE CRITICIDAD (AMBOS CRITERIOS SON IGUALMENTE CRÍTICOS):**

#### **Por qué ambos AC1 y AC2 son críticos:**

1. **Ambos cumplen el propósito dual de la HU**: La Historia de Usuario especifica explícitamente dos funcionalidades: "**añadir o modificar** una justificación". Cada AC valida uno de estos dos casos de uso principales:
   - AC1: Validar "modificar"
   - AC2: Validar "añadir"

2. **Casos de uso principales complementarios**: Ambos son flujos happy path que los coordinadores usarán regularmente:
   - **AC1 (Modificar)**: Cuando revisan y mejoran justificaciones existentes durante procesos de revisión curricular o auditorías
   - **AC2 (Añadir)**: Cuando completan justificaciones faltantes de relaciones que fueron creadas sin documentación completa

3. **Diferenciador de "mapeo directo"**: Ambos AC validan la funcionalidad diferenciadora de esta HU: el **acceso directo desde la matriz** sin pasar por el wizard completo de 3 pasos. Esto es crucial para:
   - Eficiencia: Editar justificaciones rápidamente
   - Usabilidad: No forzar al usuario a repetir selecciones ya hechas
   - Mantenimiento: Facilitar la actualización continua de documentación

4. **Documentación de razonamiento académico**: Ambos AC permiten documentar el **razonamiento académico** que explica las relaciones curriculares, lo cual es fundamental para:
   - **Acreditación**: Demostrar coherencia curricular ante evaluadores
   - **Revisión curricular**: Facilitar análisis de alineación del programa
   - **Transparencia**: Explicar decisiones de diseño curricular
   - **Trazabilidad**: Mantener evidencia auditable de decisiones

5. **Impacto en procesos de acreditación**: Sin estas funcionalidades, los coordinadores no podrían:
   - Corregir justificaciones incompletas o inexactas
   - Mejorar la calidad de la documentación curricular
   - Responder a observaciones de auditores
   - Mantener actualizada la evidencia de alineación curricular

6. **Escenarios reales de uso frecuente**:
   - **AC1**: Durante preparación de acreditación, los coordinadores revisan justificaciones existentes y las mejoran con ejemplos concretos, referencias a contenidos de asignaturas, o evidencias de evaluación
   - **AC2**: Al migrar datos de sistemas anteriores o al identificar relaciones que fueron creadas sin justificación completa

7. **Validación del flujo directo completo**: Ambos AC prueban:
   - Acceso desde matriz (click en checkmark)
   - Apertura del formulario simplificado
   - Carga de contexto (elementos relacionados)
   - Edición/creación de justificación
   - Guardado y notificación
   - Persistencia de datos

8. **Casos de fallo críticos**: Si cualquiera de estos AC falla:
   - **AC1 falla**: No se pueden corregir justificaciones incorrectas o desactualizadas, comprometiendo la calidad de la documentación de acreditación
   - **AC2 falla**: No se pueden completar justificaciones faltantes, dejando vacíos en la evidencia curricular

9. **Complejidad técnica**: Ambos requieren:
   - Detección correcta del contexto (¿hay justificación previa?)
   - Carga de datos relacionados
   - Diferenciación entre INSERT (añadir) y UPDATE (modificar) en base de datos
   - Mensajes de éxito diferenciados ("guardó" vs "actualizó")
   - Actualización de estado de la relación

10. **Prerequisito para auditoría de calidad**: Ambos AC son necesarios para que los coordinadores puedan:
    - Mantener un nivel de calidad consistente en todas las justificaciones
    - Responder a feedback de revisores internos/externos
    - Demostrar mejora continua en la documentación curricular

---

### **🎯 SI SOLO SE PUEDE PRIORIZAR UNO: AC1 (Modificar)**

Si se debe forzar una priorización única, **AC1 es ligeramente más crítico** porque:

1. **Frecuencia de uso mayor**: En la práctica, es más común modificar justificaciones existentes (para mejorarlas, actualizarlas, corregirlas) que añadir justificaciones a relaciones sin documentación.

2. **Proceso de mejora continua**: La capacidad de modificar es fundamental para el ciclo de mejora continua de la calidad educativa. Las justificaciones evolucionan con el tiempo al incorporar:
   - Nuevas metodologías pedagógicas
   - Feedback de estudiantes/empleadores
   - Cambios en estándares de acreditación
   - Mejores prácticas identificadas

3. **Corrección de errores**: AC1 permite corregir justificaciones incorrectas o deficientes, mientras AC2 solo añade nuevas. La corrección de errores es más crítica que la adición de contenido nuevo.

---

**CONCLUSIÓN:**

**Ambos AC1 y AC2 son críticos** porque validan las dos funcionalidades principales de la HU ("añadir o modificar"). Sin embargo, si se requiere priorización absoluta, **AC1 (Modificar)** tiene una ligera ventaja por su mayor frecuencia de uso en procesos de mejora continua y revisión curricular para acreditación.

---

**FIN DEL ANÁLISIS** ✅