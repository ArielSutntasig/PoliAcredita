# **CRITERIOS DE ACEPTACIÓN - HU: Crear Asignatura (PEA)**

---

## **NOTA IMPORTANTE SOBRE ANÁLISIS DE IMÁGENES**

En los análisis previos, he trabajado con imágenes del prototipo para:
- Login (imágenes 1-3)
- Listado de Asignaturas del Profesor (imagen 4)
- RAA del Profesor (imágenes 7-11)
- Wizard de vinculación (imágenes 12-20)
- Coordinador (imágenes 4-7)

Sin embargo, no he identificado explícitamente imágenes del **flujo de creación de asignatura** en las referencias previas. 

Basándome en:
1. El patrón establecido en "Crear RAA" (modal con campos)
2. Los datos visibles en la tabla de asignaturas (Código, Nombre, Unidad de Integración, Créditos, Nivel Referencial)
3. El botón "+ Nueva Asignatura" mencionado en análisis previos

Procederé a generar los AC usando **inferencia lógica del sistema** y el **patrón de diseño consistente** observado.

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU e inferencia del patrón del sistema):**

**C1:** Usuario hace clic en botón "+ Nueva Asignatura"  
**C2:** Campo "Código" contiene valor (ej: "ISWD414")  
**C3:** Campo "Nombre de Asignatura" contiene texto  
**C4:** Dropdown "Unidad de Integración Curricular" tiene opción seleccionada  
**C5:** Campo "Créditos" contiene valor numérico  
**C6:** Dropdown "Nivel Referencial" tiene valor seleccionado  
**C7:** Código ingresado es único (no existe duplicado)

**Nota:** Basado en la tabla de asignaturas vista previamente, estos son los campos clave que debe capturar el formulario.

#### **ACCIONES DEL SISTEMA:**

**A1:** Abrir modal/formulario "Crear/Editar Asignatura (PEA)"  
**A2:** Mostrar campo "Código" para identificador único  
**A3:** Mostrar campo "Nombre de Asignatura"  
**A4:** Mostrar dropdown "Unidad de Integración Curricular" (con opciones como: Obligatoria, Optativa, etc.)  
**A5:** Mostrar campo "Créditos" (numérico)  
**A6:** Mostrar dropdown "Nivel Referencial" (valores como: 1, 2, 3, etc.)  
**A7:** Mostrar botones "Cancelar" y "Guardar"  
**A8:** Mantener botón "Guardar" deshabilitado  
**A9:** Habilitar botón "Guardar"  
**A10:** Validar unicidad del código  
**A11:** Crear asignatura en base de datos  
**A12:** Cerrar modal/formulario  
**A13:** Actualizar tabla de asignaturas con nueva fila  
**A14:** Mostrar mensaje de confirmación exitosa  
**A15:** Mostrar mensaje de error (código duplicado u otro error de validación)

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Clic "+ Nueva Asignatura"** | F | F | F | F | V | V | V | V |
| **C2: Código ingresado** | - | - | - | - | F | F | V | V |
| **C3: Nombre ingresado** | - | - | - | - | F | F | V | V |
| **C4: Unidad seleccionada** | - | - | - | - | F | V | F | V |
| **ACCIONES** |
| A1-A8: Abrir formulario deshabilitado | - | - | - | - | X | X | X | X |
| A9: Habilitar "Guardar" | - | - | - | - | - | - | - | X |

Por simplicidad, presento versión reducida. La tabla completa con todas las condiciones (7 condiciones = 128 combinaciones) sería excesiva.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** |
|-----------|--------|--------|--------|--------|--------|
| **C1: Clic en "+ Nueva Asignatura"** | V | V | V | V | V |
| **C2: Código ingresado** | F | V | V | V | V |
| **C3: Nombre ingresado** | - | F | V | V | V |
| **C4: Unidad Integración seleccionada** | - | - | F | V | V |
| **C5: Créditos ingresados** | - | - | - | F | V |
| **C6: Nivel Referencial seleccionado** | - | - | - | F | V |
| **C7: Código único** | - | - | - | - | V |
| **ACCIONES** |
| A1-A7: Abrir formulario | X | X | X | X | X |
| A8: Botón "Guardar" deshabilitado | X | X | X | X | - |
| A9: Botón "Guardar" habilitado | - | - | - | - | X |
| A10-A14: Crear asignatura exitosa | - | - | - | - | X |
| A15: Error código duplicado | - | - | - | - | (si dup) |

**Justificación de minimización:**

- **R1:** Formulario abierto sin datos - botón deshabilitado.
- **R2-R4:** Campos parcialmente completos - botón deshabilitado.
- **R5:** Todos los campos completos y código único - crea asignatura exitosamente.

Se incluirá también el caso de error por código duplicado como AC separado.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas significativas:** 5 reglas base + 1 caso de error + 1 cancelación

**Criterios de Aceptación finales:** **5 AC**

1. **AC1:** Abrir formulario para crear asignatura
2. **AC2:** Validar campos requeridos progresivamente
3. **AC3:** Validar código único (error si duplicado)
4. **AC4:** Crear asignatura exitosamente
5. **AC5:** Cancelar creación

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Abrir formulario para crear nueva asignatura**

**Dado que** soy un profesor **Y** estoy en la vista "Asignaturas (PEA)",  
**cuando** hago clic en el botón "+ Nueva Asignatura" ubicado en la esquina superior derecha,  
**entonces** se abre un formulario o modal con el título "Crear/Editar Asignatura (PEA)" **Y** se presenta el campo "Código" para ingresar el identificador único de la asignatura **Y** se presenta el campo "Nombre de Asignatura" para ingresar el nombre completo **Y** se presenta el dropdown "Unidad de Integración Curricular" con opciones como "Obligatoria", "Optativa", etc. **Y** se presenta el campo "Créditos" para ingresar el valor numérico de créditos **Y** se presenta el dropdown "Nivel Referencial" con valores numéricos (1, 2, 3, 4, etc.) **Y** se muestra el botón "Cancelar" habilitado **Y** se muestra el botón "Guardar" deshabilitado en gris **Y** todos los campos están vacíos listos para ingresar información **Y** puedo comenzar a registrar los detalles del programa de estudio.

---

### **Escenario 2 – Validar campos requeridos para habilitar guardado**

**Dado que** tengo el formulario "Crear/Editar Asignatura (PEA)" abierto,  
**cuando** ingreso solo el código (ej: "ISWD414") sin completar los demás campos,  
**entonces** el botón "Guardar" permanece deshabilitado en gris,  
**Y cuando** ingreso el código y el nombre (ej: "Ingeniería de Software y Requerimientos") pero NO completo unidad, créditos y nivel,  
**entonces** el botón "Guardar" permanece deshabilitado en gris,  
**Y cuando** completo todos los campos obligatorios: código (ej: "ISWD414"), nombre (ej: "Ingeniería de Software y Requerimientos"), unidad de integración (ej: "Obligatoria"), créditos (ej: "2"), y nivel referencial (ej: "3"),  
**entonces** el botón "Guardar" cambia de gris deshabilitado a azul habilitado **Y** puedo hacer clic en "Guardar" para completar la creación **Y** el sistema valida que todos los campos obligatorios están completos antes de permitir el guardado.

---

### **Escenario 3 – Intentar crear asignatura con código duplicado**

**Dado que** tengo el formulario "Crear/Editar Asignatura (PEA)" abierto **Y** existen asignaturas previamente creadas,  
**cuando** ingreso un código que ya existe en el sistema (ej: "ISWD414" cuando ya hay una asignatura con ese código) **Y** completo los demás campos obligatorios (nombre, unidad, créditos, nivel) **Y** hago clic en el botón "Guardar" habilitado,  
**entonces** el sistema detecta que el código ya está en uso **Y** se muestra un mensaje de error indicando que el código de asignatura debe ser único **Y** el formulario permanece abierto para que pueda corregir el código **Y** NO se crea la asignatura duplicada **Y** puedo modificar el código a uno único para completar la creación exitosamente.

---

### **Escenario 4 – Crear asignatura exitosamente**

**Dado que** tengo el formulario "Crear/Editar Asignatura (PEA)" abierto,  
**cuando** ingreso un código único (ej: "ISWD414") **Y** ingreso el nombre completo (ej: "Ingeniería de Software y Requerimientos") **Y** selecciono la unidad de integración curricular (ej: "Obligatoria") **Y** ingreso el número de créditos (ej: "2") **Y** selecciono el nivel referencial (ej: "3") **Y** el botón "Guardar" está habilitado **Y** hago clic en el botón "Guardar",  
**entonces** el sistema valida que todos los campos están completos y el código es único **Y** se crea la nueva asignatura en la base de datos **Y** el formulario se cierra automáticamente **Y** se vuelve a la vista "Asignaturas (PEA)" **Y** la tabla se actualiza mostrando una nueva fila con la asignatura creada **Y** la nueva fila incluye: el código (ISWD414), el nombre (Ingeniería de Software y Requerimientos), la unidad de integración (Obligatoria), los créditos (2), el nivel referencial (3), y los iconos de editar y eliminar **Y** se muestra un mensaje de confirmación exitosa (ej: tooltip con "Se creó la asignatura correctamente" o similar) **Y** he registrado exitosamente los detalles del nuevo programa de estudio **Y** puedo ahora acceder a esta asignatura para gestionar sus RAA y matrices.

---

### **Escenario 5 – Cancelar creación de asignatura**

**Dado que** tengo el formulario "Crear/Editar Asignatura (PEA)" abierto **Y** he ingresado datos en los campos (código, nombre, etc.) o el formulario está vacío,  
**cuando** hago clic en el botón "Cancelar",  
**entonces** el formulario se cierra inmediatamente **Y** NO se guarda ninguna asignatura nueva en el sistema **Y** se descarta toda la información ingresada en los campos **Y** se vuelve a la vista "Asignaturas (PEA)" **Y** la tabla permanece sin cambios **Y** puedo volver a abrir el formulario con el botón "+ Nueva Asignatura" si deseo crear una asignatura.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 4 – Crear asignatura exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero crear una nueva asignatura para registrar los detalles de un programa de estudio". El Escenario 4 es el único que valida completamente esta funcionalidad central: crear exitosamente una asignatura con todos sus datos completos.

2. **Punto de entrada fundamental del sistema académico:** La asignatura es la entidad base sobre la cual se construye todo el sistema Poliacredita:
   - Sin asignaturas no hay RAA que crear
   - Sin asignaturas no hay matrices RAA vs RA que vincular
   - Sin asignaturas no hay trazabilidad curricular
   - Sin asignaturas el sistema pierde su propósito

3. **Happy path completo de la funcionalidad:** Representa el flujo exitoso completo desde la apertura del formulario, ingreso de todos los campos obligatorios, validación correcta, persistencia en base de datos, actualización visual y confirmación al usuario.

4. **Impacto directo en diseño curricular y académico:** La capacidad de crear asignaturas es el primer paso en la documentación curricular. Sin esta funcionalidad operando correctamente:
   - Los profesores no pueden documentar sus programas de estudio
   - No se puede establecer el catálogo de asignaturas de la carrera
   - No se puede iniciar el trabajo de definición de competencias específicas (RAA)
   - Se bloquea todo el flujo de acreditación académica

5. **Validación de captura de datos completa:** Este escenario valida que el sistema captura correctamente TODOS los datos clave de una asignatura:
   - **Código:** Identificador único para referencia en documentos académicos
   - **Nombre:** Denominación oficial de la asignatura
   - **Unidad de Integración Curricular:** Clasificación académica (Obligatoria/Optativa)
   - **Créditos:** Carga académica asignada
   - **Nivel Referencial:** Ubicación en la malla curricular
   
   Todos estos datos son necesarios para reportes de acreditación y documentación oficial.

6. **Prerequisito para toda la funcionalidad posterior:** Las asignaturas creadas son la base para:
   - Crear y gestionar RAA (competencias específicas)
   - Establecer matrices RAA vs RA (trazabilidad)
   - Consultar contribuciones por parte del Coordinador
   - Generar reportes de acreditación
   - Documentar el diseño curricular completo

7. **Caso de uso inicial y frecuente:** Los profesores crearán asignaturas al inicio de cada período académico o durante rediseños curriculares. Este es uno de los primeros flujos que ejecutarán al usar el sistema.

8. **Validación de integridad completa del sistema:** Este escenario valida múltiples aspectos críticos simultáneamente:
   - Captura correcta de múltiples tipos de campos (texto, numérico, dropdown)
   - Validación de unicidad del código
   - Persistencia correcta en base de datos
   - Actualización sincronizada de la UI (tabla con nueva fila)
   - Feedback apropiado al usuario (mensaje de confirmación)
   - Habilitación de tabs relacionados (RAA, Matrices) para la nueva asignatura

Los escenarios 1, 2, 3 y 5 son importantes para validar la apertura del formulario, validaciones, manejo de errores y cancelación, pero el Escenario 4 es el único que demuestra que el sistema cumple su promesa fundamental: permitir al profesor crear y registrar los detalles completos de un programa de estudio.

Un fallo en este escenario hace que toda la funcionalidad sea inútil, ya que el profesor no podría documentar sus asignaturas, bloqueando completamente el uso del sistema Poliacredita para acreditación académica. Por tanto, debe ser validado con máxima prioridad y rigurosidad en las pruebas de aceptación, incluyendo verificación de persistencia de datos, actualización correcta de la UI, y habilitación de funcionalidades dependientes.