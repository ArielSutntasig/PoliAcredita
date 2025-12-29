# **CRITERIOS DE ACEPTACIÓN - HU: Crear Resultado de Aprendizaje de Asignatura (RAA)**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imágenes 7-11 del Profesor):**

**C1:** Usuario hace clic en botón "+ Nuevo RAA"  
**C2:** Campo "Código" contiene valor (ej: "1.X", "2.1")  
**C3:** Dropdown "Tipo" tiene opción seleccionada (Conocimientos, Destrezas, Valores y actitudes)  
**C4:** Textarea "Descripción" contiene texto  
**C5:** Código ingresado es único (no existe duplicado en la asignatura)

**Nota:** Las imágenes 8-10 muestran el flujo completo desde modal vacío hasta modal con datos completos.

#### **ACCIONES DEL SISTEMA:**

**A1:** Abrir modal centrado "Agregar Resultado de Aprendizaje de Asignatura (RAA)"  
**A2:** Mostrar subtítulo "Asegúrese de que el código sea único y la descripción clara."  
**A3:** Mostrar campo "Código" con placeholder "1.X"  
**A4:** Mostrar dropdown "Tipo" con placeholder "Tipo de RAA" y opciones: Conocimientos, Destrezas, Valores y actitudes  
**A5:** Mostrar textarea "Descripción" con placeholder "Descripción detallada del Resultado de Aprendizaje de Asignatura"  
**A6:** Mostrar botón "Cancelar" (gris)  
**A7:** Mantener botón "Guardar" deshabilitado (gris)  
**A8:** Habilitar botón "Guardar" (azul oscuro)  
**A9:** Validar unicidad del código  
**A10:** Crear RAA en base de datos  
**A11:** Cerrar modal automáticamente  
**A12:** Actualizar tabla de RAA con nueva fila  
**A13:** Mostrar tooltip azul con título "Información" y mensaje "Se agregó el Resultado de Aprendizaje de la Asignatura (RAA) correctamente"  
**A14:** Mostrar mensaje de error de validación (código duplicado)

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** | **R9** | **R10** | **R11** | **R12** | **R13** | **R14** | **R15** | **R16** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|---------|---------|---------|---------|
| **C1: Clic en "+ Nuevo RAA"** | F | F | F | F | F | F | F | F | V | V | V | V | V | V | V | V |
| **C2: Código ingresado** | F | F | F | F | V | V | V | V | F | F | F | F | V | V | V | V |
| **C3: Tipo seleccionado** | F | F | V | V | F | F | V | V | F | F | V | V | F | F | V | V |
| **C4: Descripción escrita** | F | V | F | V | F | V | F | V | F | V | F | V | F | V | F | V |
| **C5: Código único** | - | - | - | - | - | - | - | - | - | - | - | - | F | V | F | V |
| **ACCIONES** |
| A1-A7: Abrir modal deshabilitado | - | - | - | - | - | - | - | - | X | X | X | X | X | X | X | X |
| A8: Habilitar "Guardar" | - | - | - | - | - | - | - | - | - | - | - | - | - | X | - | X |
| A10-A13: Crear RAA exitoso | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | X |
| A14: Error código duplicado | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |

**Nota:** Las reglas R1-R8 son inválidas porque no hay clic en el botón, por lo que el modal no se abre. La validación de C5 solo es relevante cuando se intenta guardar.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** |
|-----------|--------|--------|--------|--------|--------|
| **C1: Hace clic en "+ Nuevo RAA"** | V | V | V | V | V |
| **C2: Código ingresado** | F | V | V | V | V |
| **C3: Tipo seleccionado** | - | F | V | V | V |
| **C4: Descripción escrita** | - | - | F | V | V |
| **C5: Código único** | - | - | - | - | V |
| **ACCIONES** |
| A1-A7: Abrir modal con botón deshabilitado | X | X | X | X | X |
| A8: Habilitar botón "Guardar" | - | - | - | X | X |
| A9: Validar unicidad | - | - | - | X | X |
| A10-A13: Crear RAA y confirmar | - | - | - | - | X |
| A14: Mostrar error código duplicado | - | - | - | X (si duplicado) | - |

**Justificación de minimización:**

- **R1:** Modal abierto sin datos - botón Guardar deshabilitado (estado inicial).
- **R2:** Solo código ingresado - botón Guardar deshabilitado (faltan tipo y descripción).
- **R3:** Código y tipo ingresados - botón Guardar deshabilitado (falta descripción).
- **R4:** Todos los campos completos - botón Guardar habilitado, valida unicidad al guardar.
- **R5:** Todos los campos completos y código único - crea RAA exitosamente.

**Nota:** R4 incluye tanto el caso de código único (que procede a R5) como código duplicado (que muestra error). Los separaré en AC distintos.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 5 reglas base + 1 caso de error = 6 escenarios

**Análisis de consolidación:**
- R1: Apertura de modal
- R2-R3: Validaciones progresivas (pueden consolidarse en un AC de "validación de campos requeridos")
- R4-R5: Creación exitosa y caso de error de código duplicado

**Criterios de Aceptación finales:** **5 AC**

1. **AC1:** Abrir modal para crear RAA
2. **AC2:** Validar campos requeridos (código, tipo, descripción)
3. **AC3:** Validar código único (error si duplicado)
4. **AC4:** Crear RAA exitosamente con todos los campos válidos
5. **AC5:** Cancelar creación de RAA

**Justificación:** R2 y R3 se consolidan en AC2 ya que ambos representan validación progresiva de campos requeridos.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Abrir modal para crear nuevo RAA**

**Dado que** soy un profesor **Y** estoy en la vista "Crear/Editar Resultados de Aprendizaje Asignatura (RAA)" de una asignatura,  
**cuando** hago clic en el botón "+ Nuevo RAA" ubicado en la esquina superior derecha,  
**entonces** se abre un modal centrado en la pantalla **Y** el modal tiene el título "Agregar Resultado de Aprendizaje de Asignatura (RAA)" **Y** se muestra el subtítulo "Asegúrese de que el código sea único y la descripción clara." **Y** se presenta el campo "Código" con placeholder "1.X" **Y** se presenta el dropdown "Tipo" con placeholder "Tipo de RAA" **Y** al hacer clic en el dropdown se despliegan las opciones: "Conocimientos", "Destrezas", "Valores y actitudes" **Y** se presenta el textarea "Descripción" con placeholder "Descripción detallada del Resultado de Aprendizaje de Asignatura" **Y** se muestra el botón "Cancelar" en gris a la izquierda **Y** se muestra el botón "Guardar" en gris deshabilitado a la derecha **Y** todos los campos están vacíos listos para ingresar información **Y** puedo comenzar a definir una nueva competencia específica para la asignatura.

---

### **Escenario 2 – Validar campos requeridos para habilitar guardado**

**Dado que** tengo el modal "Agregar Resultado de Aprendizaje de Asignatura (RAA)" abierto,  
**cuando** ingreso solo el código (ej: "2.1") sin seleccionar tipo ni escribir descripción,  
**entonces** el botón "Guardar" permanece deshabilitado en gris **Y** no puedo completar la creación,  
**Y cuando** ingreso el código (ej: "2.1") **Y** selecciono un tipo del dropdown (ej: "Destrezas") pero NO escribo descripción,  
**entonces** el botón "Guardar" permanece deshabilitado en gris **Y** no puedo completar la creación,  
**Y cuando** ingreso el código (ej: "2.1") **Y** selecciono un tipo del dropdown (ej: "Destrezas") **Y** escribo una descripción en el textarea (ej: "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo"),  
**entonces** el botón "Guardar" cambia de gris deshabilitado a azul oscuro habilitado **Y** puedo hacer clic en "Guardar" para completar la creación **Y** el sistema valida que todos los campos obligatorios están completos antes de permitir el guardado.

---

### **Escenario 3 – Intentar crear RAA con código duplicado**

**Dado que** tengo el modal "Agregar Resultado de Aprendizaje de Asignatura (RAA)" abierto **Y** existen RAA previamente creados en la asignatura,  
**cuando** ingreso un código que ya existe en la asignatura (ej: "1.1" cuando ya hay un RAA con código "1.1") **Y** selecciono un tipo (ej: "De Conocimiento") **Y** escribo una descripción **Y** hago clic en el botón "Guardar" habilitado,  
**entonces** el sistema detecta que el código ya está en uso **Y** se muestra un mensaje de error indicando que el código debe ser único **Y** el modal permanece abierto para que pueda corregir el código **Y** NO se crea el RAA duplicado **Y** puedo modificar el código a uno único (ej: "1.4") para completar la creación exitosamente.

---

### **Escenario 4 – Crear RAA exitosamente**

**Dado que** tengo el modal "Agregar Resultado de Aprendizaje de Asignatura (RAA)" abierto,  
**cuando** ingreso un código único (ej: "2.1") **Y** selecciono un tipo del dropdown (ej: "Destrezas") **Y** escribo una descripción detallada en el textarea (ej: "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo") **Y** el botón "Guardar" está habilitado en azul oscuro **Y** hago clic en el botón "Guardar",  
**entonces** el sistema valida que todos los campos están completos y el código es único **Y** se crea el nuevo RAA en la base de datos **Y** el modal se cierra automáticamente **Y** se vuelve a la vista "Crear/Editar Resultados de Aprendizaje Asignatura (RAA)" **Y** la tabla se actualiza mostrando una nueva fila con el RAA creado **Y** la nueva fila incluye: el código ingresado (2.1), el tipo seleccionado (Destrezas), la descripción completa, y los iconos de editar y eliminar **Y** se muestra un tooltip azul en la esquina superior derecha con icono ℹ️ **Y** el tooltip contiene el título "Información" **Y** el tooltip muestra el mensaje "Se agregó el Resultado de Aprendizaje de la Asignatura (RAA) correctamente" **Y** el tooltip tiene un botón X para cerrar **Y** he definido exitosamente una nueva competencia específica para la asignatura.

---

### **Escenario 5 – Cancelar creación de RAA**

**Dado que** tengo el modal "Agregar Resultado de Aprendizaje de Asignatura (RAA)" abierto **Y** he ingresado datos en los campos (código, tipo, descripción) o el modal está vacío,  
**cuando** hago clic en el botón "Cancelar",  
**entonces** el modal se cierra inmediatamente **Y** NO se guarda ningún RAA nuevo en el sistema **Y** se descarta toda la información ingresada en los campos **Y** se vuelve a la vista "Crear/Editar Resultados de Aprendizaje Asignatura (RAA)" **Y** la tabla permanece sin cambios **Y** puedo volver a abrir el modal con el botón "+ Nuevo RAA" si deseo crear un RAA.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 4 – Crear RAA exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece explícitamente "Quiero crear un nuevo resultado de aprendizaje de asignatura para definir las competencias específicas". El Escenario 4 es el único que valida completamente esta funcionalidad central: crear exitosamente un RAA con todos sus componentes.

2. **Happy path completo de la funcionalidad:** Representa el flujo de uso exitoso completo desde la apertura del modal, ingreso de datos válidos, validación correcta, persistencia en base de datos, actualización visual y confirmación al usuario. Es el caso de uso que proporciona el valor principal que el profesor busca obtener.

3. **Impacto directo en diseño curricular:** La capacidad de crear RAA es fundamental para el diseño curricular de la asignatura. Los RAA definen las competencias específicas que los estudiantes deben alcanzar. Sin esta funcionalidad operando correctamente:
   - No se pueden documentar las competencias de la asignatura
   - No se puede establecer la trazabilidad RAA → RA (requerida para acreditación)
   - No se puede completar el diseño del programa de estudios
   - Se compromete toda la documentación académica

4. **Validación de integridad completa:** Este escenario valida múltiples aspectos críticos simultáneamente:
   - Captura correcta de los tres campos obligatorios (código, tipo, descripción)
   - Validación de unicidad del código
   - Persistencia correcta en base de datos
   - Actualización sincronizada de la UI (tabla con nueva fila)
   - Feedback apropiado al usuario (tooltip de confirmación)
   - Mensaje exacto de confirmación para asegurar claridad

5. **Prerequisito para otras funcionalidades:** Los RAA creados son necesarios para:
   - Crear la matriz RAA vs RA (vincular asignatura con carrera)
   - Evaluar cobertura de competencias
   - Documentar para procesos de acreditación EUR-ACE
   - Comunicar objetivos de aprendizaje a estudiantes

6. **Evidencia visual completa en el prototipo:** Las imágenes 8-11 muestran el flujo completo exitoso específicamente:
   - Imagen 8: Modal vacío inicial
   - Imagen 9: Dropdown de tipo con opciones
   - Imagen 10: Modal con todos los campos completos
   - Imagen 11: Confirmación exitosa con mensaje exacto

7. **Caso de uso más frecuente:** Los profesores crearán RAA múltiples veces durante el diseño inicial de la asignatura y en actualizaciones curriculares. Este será el flujo ejecutado decenas o cientos de veces en producción.

Los escenarios 1, 2, 3 y 5 son importantes para validar la apertura del modal, validaciones, manejo de errores y cancelación, pero el Escenario 4 es el único que demuestra que el sistema cumple su promesa fundamental: permitir al profesor crear y definir competencias específicas para su asignatura. Un fallo en este escenario hace que toda la funcionalidad sea inútil, ya que el profesor no podría documentar las capacidades que espera desarrollar en sus estudiantes.

Por tanto, el Escenario 4 debe ser validado con máxima prioridad y rigurosidad en las pruebas de aceptación, incluyendo verificación de persistencia de datos, actualización correcta de la UI, y mensaje de confirmación exacto al usuario.