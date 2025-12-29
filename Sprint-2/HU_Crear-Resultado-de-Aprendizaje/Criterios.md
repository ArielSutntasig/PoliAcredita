# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de las Imágenes 6, 7, 8 y 9):**

**C1:** Campo "Código" contiene texto válido (Sí/No)  
**C2:** Campo "Tipo" está seleccionado (General o Específico) (Sí/No)  
**C3:** Campo "Descripción" contiene texto válido (Sí/No)  
**C4:** El código ingresado ya existe en el sistema para el tipo seleccionado (Sí/No)

**Acciones del sistema identificadas (observadas en Imágenes 6, 7, 8 y 9):**

**A1:** Mostrar modal "Agregar Resultado de Aprendizaje" con campos vacíos  
**A2:** Mostrar dropdown "Tipo" con opciones "Específico" y "General" (observado en Imagen 7)  
**A3:** Habilitar botón "Guardar" para permitir el guardado  
**A4:** Deshabilitar botón "Guardar" por falta de datos obligatorios  
**A5:** Validar campos requeridos antes de intentar guardar  
**A6:** Guardar el nuevo Resultado de Aprendizaje en el sistema  
**A7:** Cerrar el modal automáticamente tras guardado exitoso  
**A8:** Actualizar la tabla del tab activo (RG o RE) mostrando el nuevo resultado  
**A9:** Mostrar mensaje de confirmación "Completado - Se agregó exitosamente el Resultado de Aprendizaje (RG1)" o similar según el código (observado en Imagen 9)  
**A10:** Mostrar mensaje de error de validación indicando campos faltantes  
**A11:** Mostrar mensaje de error indicando que el código ya existe  
**A12:** Mantener el modal abierto con los datos ingresados cuando hay errores  
**A13:** Permitir cancelar la operación y cerrar el modal sin guardar

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Código válido | C2: Tipo seleccionado | C3: Descripción válida | C4: Código existe | Acciones |
|-------|------------------|----------------------|------------------------|-------------------|----------|
| R1 | No | No | No | No | A1, A2, A4, A10, A12, A13 |
| R2 | No | No | No | Sí | *Ilógico* |
| R3 | No | No | Sí | No | A1, A2, A4, A10, A12, A13 |
| R4 | No | No | Sí | Sí | *Ilógico* |
| R5 | No | Sí | No | No | A1, A2, A4, A10, A12, A13 |
| R6 | No | Sí | No | Sí | *Ilógico* |
| R7 | No | Sí | Sí | No | A1, A2, A4, A10, A12, A13 |
| R8 | No | Sí | Sí | Sí | *Ilógico* |
| R9 | Sí | No | No | No | A1, A2, A4, A10, A12, A13 |
| R10 | Sí | No | No | Sí | *Ilógico* |
| R11 | Sí | No | Sí | No | A1, A2, A4, A10, A12, A13 |
| R12 | Sí | No | Sí | Sí | *Ilógico* |
| R13 | Sí | Sí | No | No | A1, A2, A4, A10, A12, A13 |
| R14 | Sí | Sí | No | Sí | *Ilógico* |
| R15 | Sí | Sí | Sí | No | A1, A2, A3, A5, A6, A7, A8, A9 |
| R16 | Sí | Sí | Sí | Sí | A1, A2, A3, A5, A11, A12, A13 |

**Análisis de ilógicos:**
- R2, R4, R6, R8, R10, R12, R14: Si el código no es válido (vacío o inválido), no puede evaluarse si "ya existe" en el sistema, porque la verificación de duplicados requiere un código válido para buscar.

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Se eliminan las 7 reglas ilógicas
- R1, R3, R5, R7, R9, R11, R13 se fusionan porque todas representan el mismo resultado: al menos un campo obligatorio falta
- Se mantienen separadas para distinguir claramente qué campo específico está vacío (mejor trazabilidad y mensajes de error específicos)
- R15 representa el happy path: todos los datos válidos, tipo seleccionado y código único
- R16 representa el error de duplicado: datos válidos pero código ya existe para ese tipo

| Regla | C1: Código válido | C2: Tipo seleccionado | C3: Descripción válida | C4: Código existe | Acciones |
|-------|------------------|----------------------|------------------------|-------------------|----------|
| **R1** | No | - | - | - | A1, A2, A4, A10, A12, A13 |
| **R2** | Sí | No | - | - | A1, A2, A4, A10, A12, A13 |
| **R3** | Sí | Sí | No | - | A1, A2, A4, A10, A12, A13 |
| **R4** | Sí | Sí | Sí | No | A1, A2, A3, A5, A6, A7, A8, A9 |
| **R5** | Sí | Sí | Sí | Sí | A1, A2, A3, A5, A11, A12, A13 |

**Justificación de la minimización:**
Se eliminaron las 7 reglas imposibles. Se mantuvieron separadas R1, R2 y R3 para permitir mensajes de error específicos según el campo faltante (código, tipo, o descripción). En R1, R2 y R3, la condición C4 es irrelevante (marcada con "-") porque sin datos válidos completos no se llega a verificar duplicados. Las 5 reglas finales cubren exhaustivamente: código vacío, tipo no seleccionado, descripción vacía, guardado exitoso, y error por código duplicado.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **7 Criterios de Aceptación** en total.

**Justificación:** 
- Las 5 reglas de la tabla minimizada generan 5 criterios base (R1→AC1, R2→AC2, R3→AC3, R4→AC4, R5→AC5)
- Se agregan 2 criterios adicionales para validar flujos completos observados en las imágenes:
  - Abrir modal de creación desde el botón "+ Nuevo RA" (AC6) - observado en contexto de Imágenes 6-9
  - Cancelar operación y cerrar modal sin guardar (AC7) - observado en Imagen 6

**Criterios NO eliminados - Justificación:** Aunque existen HUs similares "Agregar Criterio EUR-ACE" y "Crear Objetivo de Programa", los criterios NO son idénticos y deben conservarse debido a que:
1. **Los datos son diferentes:** Resultados de Aprendizaje con códigos RG1-RG5 o RE1-RE5 vs OPP1-OPP5 vs 5.4.1-5.4.5
2. **Campo adicional único:** Esta HU tiene el campo "Tipo" con dropdown (General/Específico) que no existe en las otras HUs
3. **Contexto de tabs:** Los RAs se crean dentro del contexto de tabs (RG/RE) que afecta la validación y visualización
4. **Mensaje de confirmación específico:** "Se agregó exitosamente el Resultado de Aprendizaje (RG1)" es único y específico
5. **Validación de duplicados por tipo:** El código puede repetirse entre General y Específico (RG1 y RE1 pueden coexistir)

Por lo tanto, todos los criterios deben conservarse ya que validan comportamientos específicos de esta entidad con campos, lógica y contextos únicos.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Intentar guardar sin ingresar código**

**Dado que** estoy en el modal "Agregar Resultado de Aprendizaje" **Y** soy un coordinador de carrera en el sistema, **cuando** dejo el campo "Código" vacío **Y** selecciono un tipo de aprendizaje del dropdown (ej: "General") **Y** completo el campo "Descripción" con texto válido **Y** hago clic en el botón "Guardar", **entonces** el sistema NO guarda el Resultado de Aprendizaje **Y** el botón "Guardar" permanece deshabilitado o muestra comportamiento que indica campos incompletos **Y** se muestra un mensaje de error indicando que el código es obligatorio **Y** el modal permanece abierto con los datos ingresados en los campos "Tipo" y "Descripción" **Y** el campo "Código" se resalta visualmente indicando el error **Y** puedo corregir el campo "Código" o hacer clic en "Cancelar" para cerrar el modal.

### **Escenario 2 – Intentar guardar sin seleccionar tipo de aprendizaje**

**Dado que** estoy en el modal "Agregar Resultado de Aprendizaje" como se observa en la Imagen 6 **Y** soy un coordinador de carrera en el sistema, **cuando** completo el campo "Código" con un código válido (ej: "RG1") **Y** NO selecciono ningún tipo del dropdown "Tipo de Aprendizaje" **Y** completo el campo "Descripción" con texto válido **Y** hago clic en el botón "Guardar", **entonces** el sistema NO guarda el Resultado de Aprendizaje **Y** el botón "Guardar" permanece deshabilitado o muestra comportamiento que indica campos incompletos **Y** se muestra un mensaje de error indicando que el tipo es obligatorio **Y** el modal permanece abierto con los datos ingresados en los campos "Código" y "Descripción" **Y** el campo "Tipo" se resalta visualmente indicando el error **Y** puedo abrir el dropdown y seleccionar "Específico" o "General" como se observa en la Imagen 7, o hacer clic en "Cancelar".

### **Escenario 3 – Intentar guardar sin ingresar descripción**

**Dado que** estoy en el modal "Agregar Resultado de Aprendizaje" **Y** soy un coordinador de carrera en el sistema, **cuando** completo el campo "Código" con un código válido (ej: "RG1") **Y** selecciono un tipo del dropdown "Tipo de Aprendizaje" (ej: "General") **Y** dejo el campo "Descripción" vacío **Y** hago clic en el botón "Guardar", **entonces** el sistema NO guarda el Resultado de Aprendizaje **Y** el botón "Guardar" permanece deshabilitado o muestra comportamiento que indica campos incompletos **Y** se muestra un mensaje de error indicando que la descripción es obligatoria **Y** el modal permanece abierto con los datos ingresados en los campos "Código" y "Tipo" **Y** el campo "Descripción" se resalta visualmente indicando el error **Y** puedo corregir el campo "Descripción" o hacer clic en "Cancelar" para cerrar el modal.

### **Escenario 4 – Guardar exitosamente un nuevo Resultado de Aprendizaje con datos únicos**

**Dado que** estoy en el modal "Agregar Resultado de Aprendizaje" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)", **cuando** completo el campo "Código" con un código válido y único (ej: "RG1" como se observa en la Imagen 8) **Y** selecciono el tipo "General" del dropdown "Tipo de Aprendizaje" **Y** completo el campo "Descripción" con texto válido (ej: "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo" como se observa en la Imagen 8) **Y** hago clic en el botón "Guardar", **entonces** el sistema valida que todos los campos obligatorios están completos **Y** el sistema verifica que el código no existe previamente para el tipo seleccionado **Y** el sistema guarda el nuevo Resultado de Aprendizaje exitosamente **Y** el modal se cierra automáticamente **Y** la tabla del tab correspondiente ("Resultados Generales (RG)" si seleccioné tipo "General") se actualiza mostrando el nuevo resultado con su código "RG1" y descripción completa **Y** se muestra un mensaje de confirmación en la parte superior derecha con el texto "Completado" y el mensaje "Se agregó exitosamente el Resultado de Aprendizaje (RG1)" como se observa en la Imagen 9 **Y** el nuevo resultado aparece en la posición correspondiente de la tabla según el orden de los códigos.

### **Escenario 5 – Intentar guardar con código duplicado para el mismo tipo**

**Dado que** estoy en el modal "Agregar Resultado de Aprendizaje" **Y** soy un coordinador de carrera en el sistema **Y** existe un Resultado de Aprendizaje General con código "RG1" en el sistema (como se observa en la Imagen 9), **cuando** completo el campo "Código" con un código que ya existe para el tipo seleccionado (ej: "RG1") **Y** selecciono el tipo "General" del dropdown **Y** completo el campo "Descripción" con texto válido **Y** hago clic en el botón "Guardar", **entonces** el sistema valida que todos los campos obligatorios están completos **Y** el sistema detecta que el código "RG1" ya existe para el tipo "General" **Y** el sistema NO guarda el Resultado de Aprendizaje **Y** se muestra un mensaje de error indicando que el código ya existe para ese tipo de resultado **Y** el modal permanece abierto con los datos ingresados **Y** el campo "Código" se resalta visualmente indicando el conflicto **Y** puedo modificar el código a uno único para el tipo seleccionado o hacer clic en "Cancelar" para cerrar el modal sin guardar.

### **Escenario 6 – Abrir modal para crear nuevo Resultado de Aprendizaje**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)", **cuando** hago clic en el botón "+ Nuevo RA" ubicado en la esquina superior derecha, **entonces** se abre un modal con el título "Agregar Resultado de Aprendizaje" como se observa en la Imagen 6 **Y** el modal muestra el campo "Código" vacío con placeholder "REXXX" **Y** el modal muestra el dropdown "Tipo" con placeholder o etiqueta "Tipo de Aprendizaje" **Y** el modal muestra el campo "Descripción" vacío con placeholder "Descripción detallada del Resultado de Aprendizaje" **Y** se muestran los botones "Cancelar" y "Guardar" **Y** el botón "Guardar" está inicialmente deshabilitado o en estado que indica que faltan datos **Y** el fondo de la página principal se oscurece o se muestra overlay indicando modal activo **Y** puedo hacer clic en el dropdown "Tipo" para ver las opciones "Específico" y "General" como se observa en la Imagen 7.

### **Escenario 7 – Cancelar creación de Resultado de Aprendizaje**

**Dado que** estoy en el modal "Agregar Resultado de Aprendizaje" **Y** soy un coordinador de carrera en el sistema **Y** he ingresado datos en uno o más campos (Código: "RG1", Tipo: "General", Descripción: "Integrar herramientas y tecnologías modernas..."), **cuando** hago clic en el botón "Cancelar" ubicado en la parte inferior del modal o en el ícono de cerrar (X) del modal si existe, **entonces** el modal se cierra sin guardar ningún dato **Y** NO se crea ningún nuevo Resultado de Aprendizaje en el sistema **Y** regreso a la vista "Gestión de Resultados de Aprendizaje (RA)" con la tabla sin cambios en el tab activo **Y** no se muestra ningún mensaje de confirmación o error **Y** los datos ingresados en el modal se descartan y no se conservan **Y** puedo volver a abrir el modal haciendo clic en "+ Nuevo RA" y los campos aparecerán vacíos nuevamente.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 4 – Guardar exitosamente un nuevo Resultado de Aprendizaje con datos únicos**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Validación Directa del Valor de la HU:** Este escenario demuestra explícitamente el objetivo central declarado en la Historia de Usuario: "registrar un nuevo Resultado de Aprendizaje (General o Específico) para definir los resultados que los estudiantes deben alcanzar". Sin este flujo exitoso, la HU completa carece de valor para el Coordinador de Carrera.

2. **Happy Path con Evidencia Visual Completa:** Este es el único escenario que tiene evidencia visual completa y secuencial en las imágenes adjuntas:
   - Imagen 6: Modal inicial con estructura de campos
   - Imagen 7: Dropdown de tipo mostrando opciones "Específico" y "General"
   - Imagen 8: Modal completado con datos reales (RG1, tipo General, descripción completa)
   - Imagen 9: Mensaje de confirmación exacto "Completado - Se agregó exitosamente el Resultado de Aprendizaje (RG1)"
   
   Esta trazabilidad visual completa lo hace totalmente verificable y auditable.

3. **Elemento Diferenciador Crítico - Campo "Tipo":** Este escenario valida el campo único y diferenciador de esta funcionalidad: la selección de "Tipo" (General o Específico). Este campo:
   - No existe en las HUs similares (OPP, Criterios EUR-ACE)
   - Determina en qué tab se mostrará el resultado (RG o RE)
   - Afecta la validación de duplicados (RG1 y RE1 pueden coexistir)
   - Es fundamental para la clasificación pedagógica de los resultados

4. **Impacto en Diseño Curricular y Evaluación:** Los Resultados de Aprendizaje son elementos centrales del diseño curricular moderno. Este escenario valida que:
   - Se pueden definir competencias generales (transversales del programa)
   - Se pueden definir competencias específicas (de áreas o asignaturas)
   - Los RAs quedan inmediatamente disponibles para mapeo con OPPs y Criterios EUR-ACE
   - Se mantiene la diferenciación conceptual entre RGs y REs

5. **Validación de Flujo Completo End-to-End Único:** Este escenario valida una cadena de acciones más compleja que las HUs similares:
   - Entrada de datos en tres campos obligatorios (vs dos en OPP/EUR-ACE)
   - Selección de tipo mediante dropdown (interacción adicional)
   - Validación de unicidad por tipo (lógica más compleja)
   - Actualización del tab correcto según tipo seleccionado (A8)
   - Mensaje de confirmación con código específico en el texto (A9)

6. **Riesgo de Negocio y Acreditación Crítico:** Un fallo en este escenario tendría consecuencias graves:
   - Imposibilidad de definir competencias del perfil de egreso
   - Bloqueo de procesos de diseño curricular basado en competencias
   - Incumplimiento de metodologías educativas modernas (Tuning, Bolonia)
   - Impacto en preparación para acreditación internacional
   - Imposibilidad de evidenciar logro de aprendizajes de estudiantes

7. **Base de Trazabilidad Curricular Bidireccional:** Los RAs son el elemento central de la trazabilidad que conecta:
   - Hacia arriba: RA → Objetivos de Programa (OPP) → Criterios EUR-ACE
   - Hacia abajo: RA → Asignaturas → Actividades de aprendizaje → Instrumentos de evaluación
   
   Sin la capacidad de crear RAs, toda la estructura de trazabilidad curricular colapsa en ambas direcciones.

8. **Diferenciación Pedagógica Fundamental:** Este escenario valida la distinción crítica entre:
   - **Resultados Generales (RG):** Competencias transversales, habilidades blandas, competencias de programa completo
   - **Resultados Específicos (RE):** Competencias técnicas, conocimientos disciplinares, habilidades de áreas específicas
   
   Esta diferenciación es fundamental en modelos educativos modernos y acreditación internacional.

9. **Contexto del Sistema de Tabs Único:** A diferencia de otras HUs, este escenario valida que:
   - El tipo seleccionado determina en qué tab aparecerá el resultado
   - La validación de duplicados se hace dentro del tipo, no globalmente
   - La tabla del tab correcto se actualiza (no ambas)
   - El usuario puede crear RG1 y RE1 sin conflicto

10. **Responsabilidad del Coordinador en Marco Competencias:** El Coordinador de Carrera es responsable de:
    - Definir el perfil de egreso basado en competencias
    - Establecer RAs medibles y evaluables
    - Asegurar coherencia entre RGs (perfil general) y REs (especializaciones)
    - Facilitar evaluación del logro de aprendizajes
    
    Sin este escenario funcionando, el coordinador no puede cumplir su rol estratégico.

11. **Validación de Consistencia de Datos Específicos:** Este escenario valida elementos únicos observados:
    - Códigos siguen formato específico RGX o REX según tipo
    - Descripciones son competencias redactadas en forma de logros de aprendizaje
    - Mensaje incluye el código exacto: "...Resultado de Aprendizaje (RG1)"
    - La tabla correcta se actualiza según el tipo seleccionado

12. **Complejidad Técnica Mayor:** Este escenario tiene mayor complejidad que las HUs similares porque requiere:
    - Gestión de tres campos obligatorios
    - Lógica de dropdown con dos opciones
    - Validación condicional por tipo
    - Enrutamiento a tab correcto
    - Actualización selectiva de tabla según tipo
    - Mensaje dinámico con código interpolado

Por todas estas razones, este escenario es el más crítico y debe validarse exhaustivamente antes de cualquier otro, ya que representa no solo el valor central de la HU, sino también la funcionalidad diferenciadora y más compleja de toda la familia de HUs de creación.