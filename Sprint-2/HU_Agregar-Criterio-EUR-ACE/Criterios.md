# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de la Imagen 11 + patrones observados en Imágenes 3-4, 6-8):**

**C1:** Campo "Código" contiene texto válido (Sí/No)  
**C2:** Campo "Descripción" contiene texto válido (Sí/No)  
**C3:** El código ingresado ya existe en el sistema (Sí/No)

**Acciones del sistema identificadas (basadas en patrones observados en modales de creación de las imágenes anteriores):**

**A1:** Mostrar modal "Crear Criterio EUR-ACE" con campos vacíos  
**A2:** Habilitar botón "Guardar" para permitir el guardado  
**A3:** Deshabilitar botón "Guardar" por falta de datos obligatorios  
**A4:** Validar campos requeridos antes de intentar guardar  
**A5:** Guardar el nuevo criterio EUR-ACE en el sistema  
**A6:** Cerrar el modal automáticamente tras guardado exitoso  
**A7:** Actualizar la tabla de "Criterios EUR-ACE" mostrando el nuevo criterio  
**A8:** Mostrar mensaje de confirmación exitosa (similar a "Completado - Se agregó exitosamente el Criterio EUR-ACE")  
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
- R2, R4, R6: Si el código no es válido (vacío o inválido), no puede evaluarse si "ya existe" en el sistema, porque la verificación de duplicados requiere un código válido para buscar.

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Se eliminan R2, R4, R6 por ser lógicamente imposibles
- R1, R3, R5 se fusionan en una sola regla porque representan el mismo resultado: al menos un campo obligatorio está vacío o inválido
- R7 representa el happy path: todos los datos válidos y código único
- R8 representa el caso de error de duplicado: datos válidos pero código ya existe

| Regla | C1: Código válido | C2: Descripción válida | C3: Código existe | Acciones |
|-------|------------------|------------------------|-------------------|----------|
| **R1** | No | - | - | A1, A3, A9, A11, A12 |
| **R2** | Sí | No | - | A1, A3, A9, A11, A12 |
| **R3** | Sí | Sí | No | A1, A2, A4, A5, A6, A7, A8 |
| **R4** | Sí | Sí | Sí | A1, A2, A4, A10, A11, A12 |

**Justificación de la minimización:**
Se eliminaron las reglas imposibles donde se evalúa existencia de un código inválido. Se separó R1 y R2 para distinguir claramente qué campo específico falta. En R1 y R2, la condición C3 es irrelevante (marcada con "-") porque sin datos válidos completos no se llega a verificar duplicados. Las 4 reglas finales cubren exhaustivamente: campo código vacío, campo descripción vacío, guardado exitoso, y error por duplicado.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **6 Criterios de Aceptación** en total.

**Justificación:** 
- Las 4 reglas de la tabla minimizada generan 4 criterios base (R1→AC1, R2→AC2, R3→AC3, R4→AC4)
- Se agregan 2 criterios adicionales para validar flujos completos observados en patrones del prototipo:
  - Abrir modal de creación desde la vista principal (AC5)
  - Cancelar operación y cerrar modal sin guardar (AC6)

**Criterios NO eliminados - Justificación:** Aunque existen HUs similares de creación (OPP, RA) observadas en las imágenes, los criterios NO son idénticos y deben conservarse debido a que:
1. **Los datos son diferentes:** Criterios EUR-ACE tienen códigos numéricos específicos (5.4.1, 5.4.2) vs códigos alfanuméricos (OPP1, RG1)
2. **El rol es diferente:** Miembro de la CEI (Comité de Evaluación Interna) vs Coordinador de Carrera
3. **El contexto es único:** Criterios EUR-ACE son estándares europeos de acreditación con formato y significado específico
4. **Las descripciones son diferentes:** Textos técnicos largos sobre estándares de ingeniería vs descripciones de objetivos o resultados
5. **La validación puede ser diferente:** Los códigos EUR-ACE tienen formato específico jerárquico (X.X.X)

Por lo tanto, todos los criterios deben conservarse ya que validan comportamientos específicos de esta entidad con reglas de negocio únicas.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Intentar guardar sin ingresar código**

**Dado que** estoy en el modal "Crear Criterio EUR-ACE" **Y** soy un miembro de la CEI en el sistema, **cuando** dejo el campo "Código" vacío **Y** completo el campo "Descripción" con texto válido **Y** hago clic en el botón "Guardar", **entonces** el sistema NO guarda el criterio EUR-ACE **Y** el botón "Guardar" permanece deshabilitado o muestra comportamiento que indica campos incompletos **Y** se muestra un mensaje de error indicando que el código es obligatorio **Y** el modal permanece abierto con los datos ingresados en el campo "Descripción" **Y** el campo "Código" se resalta visualmente indicando el error **Y** puedo corregir el campo "Código" o hacer clic en "Cancelar" para cerrar el modal.

### **Escenario 2 – Intentar guardar sin ingresar descripción**

**Dado que** estoy en el modal "Crear Criterio EUR-ACE" **Y** soy un miembro de la CEI en el sistema, **cuando** completo el campo "Código" con un código válido (ej: "5.4.6") **Y** dejo el campo "Descripción" vacío **Y** hago clic en el botón "Guardar", **entonces** el sistema NO guarda el criterio EUR-ACE **Y** el botón "Guardar" permanece deshabilitado o muestra comportamiento que indica campos incompletos **Y** se muestra un mensaje de error indicando que la descripción es obligatoria **Y** el modal permanece abierto con los datos ingresados en el campo "Código" **Y** el campo "Descripción" se resalta visualmente indicando el error **Y** puedo corregir el campo "Descripción" o hacer clic en "Cancelar" para cerrar el modal.

### **Escenario 3 – Guardar exitosamente un nuevo criterio EUR-ACE con datos únicos**

**Dado que** estoy en el modal "Crear Criterio EUR-ACE" **Y** soy un miembro de la CEI en el sistema, **cuando** completo el campo "Código" con un código válido y único (ej: "5.4.6") **Y** completo el campo "Descripción" con texto válido (ej: "Gestión de proyectos de ingeniería complejos aplicando metodologías modernas, considerando restricciones técnicas, económicas y de recursos humanos.") **Y** hago clic en el botón "Guardar", **entonces** el sistema valida que todos los campos obligatorios están completos **Y** el sistema verifica que el código no existe previamente **Y** el sistema guarda el nuevo criterio EUR-ACE exitosamente **Y** el modal se cierra automáticamente **Y** la tabla de "Criterios EUR-ACE" se actualiza mostrando el nuevo criterio con su código y descripción **Y** se muestra un mensaje de confirmación "Completado" con el texto "Se agregó exitosamente el Criterio EUR-ACE" o similar **Y** el nuevo criterio aparece en la posición correspondiente de la tabla según el orden de los códigos.

### **Escenario 4 – Intentar guardar con código duplicado**

**Dado que** estoy en el modal "Crear Criterio EUR-ACE" **Y** soy un miembro de la CEI en el sistema **Y** existe un criterio EUR-ACE con código "5.4.1" en el sistema, **cuando** completo el campo "Código" con un código que ya existe (ej: "5.4.1") **Y** completo el campo "Descripción" con texto válido **Y** hago clic en el botón "Guardar", **entonces** el sistema valida que todos los campos obligatorios están completos **Y** el sistema detecta que el código "5.4.1" ya existe **Y** el sistema NO guarda el criterio EUR-ACE **Y** se muestra un mensaje de error indicando que el código ya existe o está duplicado **Y** el modal permanece abierto con los datos ingresados **Y** el campo "Código" se resalta visualmente indicando el conflicto **Y** puedo modificar el código a uno único o hacer clic en "Cancelar" para cerrar el modal sin guardar.

### **Escenario 5 – Abrir modal para crear nuevo criterio EUR-ACE**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un miembro de la CEI en el sistema, **cuando** hago clic en el botón para agregar nuevo criterio (similar a "+ Nuevo OPP" o "+ Nuevo RA" observado en otras vistas), **entonces** se abre un modal con el título "Crear Criterio EUR-ACE" o similar **Y** el modal muestra el campo "Código" vacío con placeholder o etiqueta indicativa **Y** el modal muestra el campo "Descripción" vacío con placeholder o etiqueta indicativa (ej: "Descripción detallada del Criterio EUR-ACE") **Y** se muestran los botones "Cancelar" y "Guardar" **Y** el botón "Guardar" está inicialmente deshabilitado o en estado que indica que faltan datos **Y** el fondo de la página principal se oscurece o se muestra overlay indicando modal activo **Y** puedo ingresar texto en ambos campos.

### **Escenario 6 – Cancelar creación de criterio EUR-ACE**

**Dado que** estoy en el modal "Crear Criterio EUR-ACE" **Y** soy un miembro de la CEI en el sistema **Y** he ingresado datos en uno o ambos campos (Código, Descripción), **cuando** hago clic en el botón "Cancelar" o en el ícono de cerrar (X) del modal, **entonces** el modal se cierra sin guardar ningún dato **Y** NO se crea ningún nuevo criterio EUR-ACE en el sistema **Y** regreso a la vista "Criterios EUR-ACE" con la tabla sin cambios **Y** no se muestra ningún mensaje de confirmación o error **Y** los datos ingresados en el modal se descartan y no se conservan **Y** puedo volver a abrir el modal y los campos aparecerán vacíos nuevamente.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Guardar exitosamente un nuevo criterio EUR-ACE con datos únicos**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Validación Directa del Valor de la HU:** Este escenario demuestra explícitamente el objetivo central declarado en la Historia de Usuario: "registrar un nuevo Criterio EUR-ACE para incorporar nuevos estándares de acreditación al sistema". Sin este flujo exitoso, la HU completa carece de valor y propósito.

2. **Happy Path Esencial:** Representa el flujo principal y más importante de la funcionalidad. Es el escenario que los miembros de la CEI ejecutarán cuando necesiten agregar legítimamente nuevos estándares EUR-ACE al sistema de acreditación.

3. **Impacto en Procesos de Acreditación:** Los Criterios EUR-ACE son estándares europeos fundamentales para acreditación de programas de ingeniería. Este escenario valida que:
   - El sistema puede incorporar nuevos estándares cuando se actualizan
   - Los miembros de la CEI pueden mantener el catálogo actualizado
   - La institución puede adaptarse a cambios en requisitos de acreditación
   - Se preserva la integridad del sistema de estándares

4. **Validación de Flujo Completo End-to-End:** Este escenario valida la cadena completa de acciones críticas:
   - Entrada de datos válidos
   - Validación de campos obligatorios (A4)
   - Verificación de unicidad de código
   - Persistencia correcta en base de datos (A5)
   - Cierre automático de modal (A6)
   - Actualización inmediata de la vista (A7)
   - Confirmación visual al usuario (A8)

5. **Dependencia de Otros Escenarios:** Los escenarios de validación (AC1, AC2, AC4) solo tienen sentido si el escenario de éxito funciona correctamente. Sin un guardado exitoso funcional, las validaciones son irrelevantes.

6. **Riesgo de Negocio Crítico:** Un fallo en este escenario tendría consecuencias graves:
   - Imposibilidad de actualizar estándares de acreditación
   - Incumplimiento de requisitos regulatorios europeos
   - Bloqueo de procesos de evaluación de programas académicos
   - Impacto en certificación y reconocimiento internacional de títulos
   - Obsolescencia del sistema frente a actualizaciones de EUR-ACE

7. **Contexto Regulatorio y Normativo:** Los Criterios EUR-ACE son:
   - Estándares obligatorios para acreditación de programas de ingeniería en Europa
   - Requisitos para reconocimiento mutuo de títulos profesionales
   - Marco de referencia para evaluación de calidad educativa
   - Elemento clave para movilidad estudiantil y profesional en espacio europeo

8. **Responsabilidad del Rol CEI:** El Comité de Evaluación Interna (CEI) es el organismo responsable de:
   - Mantener actualizados los estándares institucionales
   - Asegurar alineación con marcos internacionales
   - Facilitar procesos de autoevaluación y mejora continua
   - Preparar evidencias para acreditación externa
   
   Si no pueden agregar criterios, su función esencial queda comprometida.

9. **Integridad del Sistema de Trazabilidad:** Los Criterios EUR-ACE son la capa superior de trazabilidad que conecta:
   - Criterios EUR-ACE → Resultados de Aprendizaje (RA)
   - RA → Objetivos de Programa (OPP)
   - OPP → Asignaturas
   
   Sin la capacidad de agregar nuevos criterios EUR-ACE, toda la cadena de trazabilidad curricular se vuelve estática e inadaptable.

10. **Validación de Consistencia de Datos:** Este escenario valida que:
    - Los códigos siguen el formato jerárquico correcto (X.X.X)
    - Las descripciones se guardan completas y legibles
    - Los nuevos criterios aparecen correctamente ordenados
    - La paginación se actualiza adecuadamente si es necesario
    - El criterio recién creado es inmediatamente utilizable en otros módulos del sistema

11. **Experiencia del Usuario Completa:** Este escenario valida la retroalimentación completa al usuario:
    - Confirmación visual de éxito (mensaje "Completado")
    - Evidencia inmediata del criterio en la tabla
    - Cierre automático del modal (no requiere acción adicional)
    - Estado limpio para siguiente operación

12. **Punto de Referencia para Testing:** Este es el escenario base que debe funcionar antes de probar casos límite o de error. Si el happy path falla, los tests de validación son prematuros.