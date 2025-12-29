# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de las Imágenes 2, 3, 4 y 5):**

**C1:** Campo "Código" contiene texto válido (Sí/No)  
**C2:** Campo "Descripción" contiene texto válido (Sí/No)  
**C3:** El código ingresado ya existe en el sistema (Sí/No)

**Acciones del sistema identificadas (observadas en Imágenes 3, 4 y 5):**

**A1:** Mostrar modal "Crear Objetivo de Programa" con campos vacíos  
**A2:** Habilitar botón "Guardar" para permitir el guardado  
**A3:** Deshabilitar botón "Guardar" por falta de datos obligatorios  
**A4:** Validar campos requeridos antes de intentar guardar  
**A5:** Guardar el nuevo Objetivo de Programa en el sistema  
**A6:** Cerrar el modal automáticamente tras guardado exitoso  
**A7:** Actualizar la tabla de "Gestión de Objetivos de Carrera (OPP)" mostrando el nuevo objetivo  
**A8:** Mostrar mensaje de confirmación "Completado - Se agregó el objetivo de programa correctamente" (observado en Imagen 5)  
**A9:** Mostrar mensaje de error de validación indicando campos faltantes  
**A10:** Mostrar mensaje de error indicando que el código ya existe  
**A11:** Mantener el modal abierto con los datos ingresados cuando hay errores  
**A12:** Permitir cancelar la operación y cerrar el modal sin guardar

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Código válido | C2: Descripción válida | C3: Código existe | Acciones |
|-------|------------------|------------------------|-------------------|----------|
| R1 | No | No | No | A1, A3, A9, A11, A12 |
| R2 | No | No | Sí | *Ilógico* |
| R3 | No | Sí | No | A1, A3, A9, A11, A12 |
| R4 | No | Sí | Sí | *Ilógico* |
| R5 | Sí | No | No | A1, A3, A9, A11, A12 |
| R6 | Sí | No | Sí | *Ilógico* |
| R7 | Sí | Sí | No | A1, A2, A4, A5, A6, A7, A8 |
| R8 | Sí | Sí | Sí | A1, A2, A4, A10, A11, A12 |

**Análisis de ilógicos:**
- R2, R4, R6: Si el código no es válido (vacío o inválido), no puede evaluarse si "ya existe" en el sistema, porque la verificación de duplicados requiere un código válido para buscar en la base de datos.

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Se eliminan R2, R4, R6 por ser lógicamente imposibles
- R1, R3, R5 se fusionan porque representan el mismo resultado: al menos un campo obligatorio falta
- Se mantienen separadas R1 y R2 minimizadas para distinguir claramente qué campo específico está vacío (mejor trazabilidad)
- R7 representa el happy path: todos los datos válidos y código único
- R8 representa el error de duplicado: datos válidos pero código ya existe

| Regla | C1: Código válido | C2: Descripción válida | C3: Código existe | Acciones |
|-------|------------------|------------------------|-------------------|----------|
| **R1** | No | - | - | A1, A3, A9, A11, A12 |
| **R2** | Sí | No | - | A1, A3, A9, A11, A12 |
| **R3** | Sí | Sí | No | A1, A2, A4, A5, A6, A7, A8 |
| **R4** | Sí | Sí | Sí | A1, A2, A4, A10, A11, A12 |

**Justificación de la minimización:**
Se eliminaron las reglas imposibles donde se evalúa existencia de un código inválido. Se mantuvieron separadas R1 y R2 para permitir mensajes de error específicos según el campo faltante. En R1 y R2, la condición C3 es irrelevante (marcada con "-") porque sin datos válidos completos no se llega a verificar duplicados. Las 4 reglas finales cubren exhaustivamente: código vacío, descripción vacía, guardado exitoso, y error por código duplicado.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **6 Criterios de Aceptación** en total.

**Justificación:** 
- Las 4 reglas de la tabla minimizada generan 4 criterios base (R1→AC1, R2→AC2, R3→AC3, R4→AC4)
- Se agregan 2 criterios adicionales para validar flujos completos observados en las imágenes:
  - Abrir modal de creación desde el botón "+ Nuevo OPP" (AC5) - observado en Imagen 2
  - Cancelar operación y cerrar modal sin guardar (AC6) - observado en Imagen 3

**Criterios NO eliminados - Justificación:** Aunque existe una HU similar "Agregar Criterio EUR-ACE" analizada anteriormente, los criterios NO son idénticos y deben conservarse debido a que:
1. **Los datos son diferentes:** Objetivos de Programa con códigos OPP1-OPP5 vs Criterios EUR-ACE con códigos 5.4.1-5.4.5
2. **El rol es diferente:** Coordinador de Carrera vs Miembro de la CEI
3. **El propósito es diferente:** Definir objetivos que guían la carrera vs Incorporar estándares de acreditación
4. **Las descripciones son diferentes:** "Comprender los principios fundamentales de la ingeniería de software" vs descripciones técnicas de estándares EUR-ACE
5. **El mensaje de confirmación es específico:** "Se agregó el objetivo de programa correctamente" vs "Se agregó exitosamente el Criterio EUR-ACE"

Por lo tanto, todos los criterios deben conservarse ya que validan comportamientos específicos de esta entidad con datos, roles y contextos únicos.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Intentar guardar sin ingresar código**

**Dado que** estoy en el modal "Crear Objetivo de Programa" **Y** soy un coordinador de carrera en el sistema, **cuando** dejo el campo "Código" vacío **Y** completo el campo "Descripción" con texto válido **Y** hago clic en el botón "Guardar", **entonces** el sistema NO guarda el Objetivo de Programa **Y** el botón "Guardar" permanece deshabilitado o muestra comportamiento que indica campos incompletos **Y** se muestra un mensaje de error indicando que el código es obligatorio **Y** el modal permanece abierto con los datos ingresados en el campo "Descripción" **Y** el campo "Código" se resalta visualmente indicando el error **Y** puedo corregir el campo "Código" o hacer clic en "Cancelar" para cerrar el modal.

### **Escenario 2 – Intentar guardar sin ingresar descripción**

**Dado que** estoy en el modal "Crear Objetivo de Programa" **Y** soy un coordinador de carrera en el sistema, **cuando** completo el campo "Código" con un código válido (ej: "OPP6") **Y** dejo el campo "Descripción" vacío **Y** hago clic en el botón "Guardar", **entonces** el sistema NO guarda el Objetivo de Programa **Y** el botón "Guardar" permanece deshabilitado o muestra comportamiento que indica campos incompletos **Y** se muestra un mensaje de error indicando que la descripción es obligatoria **Y** el modal permanece abierto con los datos ingresados en el campo "Código" **Y** el campo "Descripción" se resalta visualmente indicando el error **Y** puedo corregir el campo "Descripción" o hacer clic en "Cancelar" para cerrar el modal.

### **Escenario 3 – Guardar exitosamente un nuevo Objetivo de Programa con datos únicos**

**Dado que** estoy en el modal "Crear Objetivo de Programa" **Y** soy un coordinador de carrera en el sistema, **cuando** completo el campo "Código" con un código válido y único (ej: "OPP1" como se observa en la Imagen 4) **Y** completo el campo "Descripción" con texto válido (ej: "Comprender los principios fundamentales de la ingeniería de software." como se observa en la Imagen 4) **Y** hago clic en el botón "Guardar", **entonces** el sistema valida que todos los campos obligatorios están completos **Y** el sistema verifica que el código no existe previamente **Y** el sistema guarda el nuevo Objetivo de Programa exitosamente **Y** el modal se cierra automáticamente **Y** la tabla de "Gestión de Objetivos de Carrera (OPP)" se actualiza mostrando el nuevo objetivo con su código "OPP1" y descripción completa **Y** se muestra un mensaje de confirmación en la parte superior derecha con el texto "Completado" y el mensaje "Se agregó el objetivo de programa correctamente" como se observa en la Imagen 5 **Y** el nuevo objetivo aparece en la posición correspondiente de la tabla según el orden de los códigos.

### **Escenario 4 – Intentar guardar con código duplicado**

**Dado que** estoy en el modal "Crear Objetivo de Programa" **Y** soy un coordinador de carrera en el sistema **Y** existe un Objetivo de Programa con código "OPP1" en el sistema (como se observa en la Imagen 2), **cuando** completo el campo "Código" con un código que ya existe (ej: "OPP1") **Y** completo el campo "Descripción" con texto válido **Y** hago clic en el botón "Guardar", **entonces** el sistema valida que todos los campos obligatorios están completos **Y** el sistema detecta que el código "OPP1" ya existe en el sistema **Y** el sistema NO guarda el Objetivo de Programa **Y** se muestra un mensaje de error indicando que el código ya existe o está duplicado **Y** el modal permanece abierto con los datos ingresados **Y** el campo "Código" se resalta visualmente indicando el conflicto **Y** puedo modificar el código a uno único o hacer clic en "Cancelar" para cerrar el modal sin guardar.

### **Escenario 5 – Abrir modal para crear nuevo Objetivo de Programa**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** veo el listado de Objetivos de Programa existentes (OPP1, OPP2, OPP3, OPP4, OPP5 como se observa en la Imagen 2), **cuando** hago clic en el botón "+ Nuevo OPP" ubicado en la esquina superior derecha (observado en la Imagen 2), **entonces** se abre un modal con el título "Crear Objetivo de Programa" como se observa en la Imagen 3 **Y** el modal muestra el campo "Código" vacío con placeholder "OPPXXX" **Y** el modal muestra el campo "Descripción" vacío con placeholder "Descripción detallada del Objetivo de Programa..." **Y** se muestran los botones "Cancelar" y "Guardar" **Y** el botón "Guardar" está inicialmente deshabilitado o en estado que indica que faltan datos **Y** el fondo de la página principal se oscurece o se muestra overlay indicando modal activo **Y** puedo ingresar texto en ambos campos.

### **Escenario 6 – Cancelar creación de Objetivo de Programa**

**Dado que** estoy en el modal "Crear Objetivo de Programa" **Y** soy un coordinador de carrera en el sistema **Y** he ingresado datos en uno o ambos campos (Código: "OPP1", Descripción: "Comprender los principios fundamentales de la ingeniería de software."), **cuando** hago clic en el botón "Cancelar" ubicado en la parte inferior izquierda del modal o en el ícono de cerrar (X) del modal si existe, **entonces** el modal se cierra sin guardar ningún dato **Y** NO se crea ningún nuevo Objetivo de Programa en el sistema **Y** regreso a la vista "Gestión de Objetivos de Carrera (OPP)" con la tabla sin cambios mostrando los objetivos existentes (OPP1-OPP5) **Y** no se muestra ningún mensaje de confirmación o error **Y** los datos ingresados en el modal se descartan y no se conservan **Y** puedo volver a abrir el modal haciendo clic en "+ Nuevo OPP" y los campos aparecerán vacíos nuevamente.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Guardar exitosamente un nuevo Objetivo de Programa con datos únicos**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Validación Directa del Valor de la HU:** Este escenario demuestra explícitamente el objetivo central declarado en la Historia de Usuario: "registrar un nuevo Objetivo de Programa para definir nuevos objetivos que guiarán mi carrera". Sin este flujo exitoso, la HU completa carece de valor y propósito para el Coordinador de Carrera.

2. **Happy Path Esencial:** Representa el flujo principal y más importante de la funcionalidad. Es el escenario que los coordinadores de carrera ejecutarán cuando necesiten legítimamente definir nuevos objetivos para el programa académico que supervisan.

3. **Evidencia Visual Completa en el Prototipo:** Este es el único escenario que tiene evidencia visual completa en las imágenes adjuntas:
   - Imagen 3: Modal con campos vacíos y placeholders específicos
   - Imagen 4: Modal con datos completados (OPP1 y descripción)
   - Imagen 5: Mensaje de confirmación exacto "Completado - Se agregó el objetivo de programa correctamente"
   
   Esta trazabilidad visual lo hace verificable y auditable directamente contra el prototipo.

4. **Validación de Flujo Completo End-to-End:** Este escenario valida la cadena completa de acciones críticas observadas en las imágenes:
   - Entrada de datos válidos (A4)
   - Validación de unicidad de código
   - Persistencia correcta en base de datos (A5)
   - Cierre automático de modal (A6)
   - Actualización inmediata de la tabla (A7)
   - Confirmación visual específica al usuario (A8 con texto exacto)

5. **Impacto en Diseño Curricular:** Los Objetivos de Programa (OPP) son elementos fundamentales del diseño curricular y el perfil de egreso. Este escenario valida que:
   - El coordinador puede definir competencias que los graduados deben alcanzar
   - Se pueden agregar nuevos objetivos cuando el programa evoluciona
   - Los objetivos quedan disponibles inmediatamente para relacionarse con Resultados de Aprendizaje
   - Se preserva la coherencia del perfil profesional del programa

6. **Dependencia de Otros Escenarios:** Los escenarios de validación (AC1, AC2, AC4) solo tienen sentido si el escenario de éxito funciona correctamente. Sin un guardado exitoso funcional, las validaciones son accesorias e irrelevantes.

7. **Riesgo de Negocio Crítico:** Un fallo en este escenario tendría consecuencias graves para la gestión académica:
   - Imposibilidad de actualizar el perfil de egreso del programa
   - Bloqueo en procesos de rediseño o actualización curricular
   - Incumplimiento de planes de mejora continua
   - Impacto en procesos de autoevaluación y acreditación
   - Obsolescencia del perfil profesional frente a demandas del mercado laboral

8. **Contexto de Responsabilidad del Coordinador:** El Coordinador de Carrera es el responsable académico de:
   - Definir y actualizar el perfil de egreso
   - Asegurar la pertinencia del programa académico
   - Liderar procesos de diseño y rediseño curricular
   - Alinear el programa con estándares de acreditación
   
   Si no puede crear nuevos OPPs, su capacidad de gestión académica queda severamente limitada.

9. **Base de la Cadena de Trazabilidad Curricular:** Los OPPs son el punto de partida de la trazabilidad que conecta:
   - Objetivos de Programa (OPP) → Resultados de Aprendizaje (RA)
   - RA → Criterios EUR-ACE
   - RA → Asignaturas y actividades de aprendizaje
   
   Sin la capacidad de crear OPPs, toda la cadena de trazabilidad académica se bloquea desde su origen.

10. **Validación de Consistencia de Datos Específicos:** Este escenario valida elementos únicos observados en las imágenes:
    - Los códigos siguen el formato específico OPPXXX
    - Las descripciones son oraciones completas que definen competencias
    - El mensaje de confirmación es específico: "Se agregó el objetivo de programa correctamente"
    - La actualización de la tabla mantiene el orden correcto de los OPPs

11. **Experiencia del Usuario Completa:** Este escenario valida la retroalimentación completa observada en la Imagen 5:
    - Confirmación visual de éxito con ícono de check verde
    - Mensaje específico "Completado"
    - Texto descriptivo exacto del resultado
    - Evidencia inmediata del objetivo en la tabla
    - Cierre automático del modal (no requiere acción adicional del usuario)

12. **Punto de Referencia para Testing:** Este es el escenario base que debe funcionar perfectamente antes de probar casos límite o de error. Si el happy path falla, los tests de validación y casos de error son prematuros y carecen de contexto funcional.