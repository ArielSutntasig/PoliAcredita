# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imágenes 6, 7, 8 y 9 del prototipo):**

1. **C1:** Se hace clic en el botón "+ Nueva Facultad"
2. **C2:** El campo "Código" está completo con un código único
3. **C3:** El campo "Nombre" está completo
4. **C4:** El campo "Descripción" está completo
5. **C5:** Se ha seleccionado un Decano mediante el campo de búsqueda
6. **C6:** El código ingresado ya existe en el sistema (duplicado)
7. **C7:** Se hace clic en el botón "Guardar"
8. **C8:** Se hace clic en el botón "Cancelar"

### **Acciones del Sistema (observadas en Imágenes 6, 7, 8 y 9):**

1. **A1:** Mostrar modal "Nueva Facultad" sobre la vista de gestión de facultades
2. **A2:** Presentar formulario con campos: "Código:", "Nombre:", "Descripción", "Decano"
3. **A3:** Mostrar campo "Código:" como campo de texto obligatorio
4. **A4:** Mostrar campo "Nombre:" como campo de texto obligatorio
5. **A5:** Mostrar campo "Descripción" como área de texto multi-línea
6. **A6:** Mostrar campo "Decano" con funcionalidad de búsqueda (icono de lupa)
7. **A7:** Desplegar lista de decanos disponibles al buscar
8. **A8:** Permitir seleccionar un decano de la lista (ej: "Julio César Sandobalín")
9. **A9:** Validar que campos obligatorios estén completos
10. **A10:** Validar que el código no esté duplicado en el sistema
11. **A11:** Mostrar mensajes de error de validación si corresponde
12. **A12:** Guardar la nueva facultad en la base de datos
13. **A13:** Cerrar el modal después de guardar exitosamente
14. **A14:** Actualizar la tabla de facultades agregando la nueva fila
15. **A15:** Mostrar mensaje de éxito "Completado - El registro se ha creado exitosamente" (Imagen 9)
16. **A16:** Cerrar el modal sin guardar si se presiona "Cancelar"
17. **A17:** No realizar cambios en la base de datos si se cancela

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 5 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Campos obligatorios completos (Código, Nombre)
- **C2:** Campo Descripción completo
- **C3:** Decano seleccionado
- **C4:** Código es único (no duplicado)
- **C5:** Usuario hace clic en "Guardar"

Total combinaciones teóricas: 2^5 = 32 reglas (simplificadas a casos más relevantes)

| Regla | Campos obligatorios | Descripción | Decano | Código único | Clic Guardar | Acción |
|-------|---------------------|-------------|--------|--------------|--------------|---------|
| R1 | N | - | - | - | N | A11: Error de validación |
| R2 | N | - | - | - | S | A11: Error de validación |
| R3 | S | N | N | N | N | Sin acción (espera) |
| R4 | S | N | N | N | S | A11: Error código duplicado |
| R5 | S | N | N | S | N | Sin acción (espera) |
| R6 | S | N | N | S | S | A12-A15: Guardar sin descripción ni decano |
| R7 | S | N | S | N | S | A11: Error código duplicado |
| R8 | S | N | S | S | S | A12-A15: Guardar sin descripción |
| R9 | S | S | N | N | S | A11: Error código duplicado |
| R10 | S | S | N | S | S | A12-A15: Guardar sin decano |
| R11 | S | S | S | N | S | A11: Error código duplicado |
| R12 | S | S | S | S | S | A12-A15: Guardar completo (happy path) |

---

## **Tabla de Decisión Minimizada**

| Regla | Campos obligatorios | Código único | Clic Guardar | Acción |
|-------|---------------------|-------------|--------------|---------|
| **R1** | N | - | S | Mostrar error "Campos obligatorios requeridos" |
| **R2** | S | N | S | Mostrar error "El código ya existe" |
| **R3** | S | S | N | Sin acción, esperar interacción del usuario |
| **R4** | S | S | S | Guardar facultad, cerrar modal, mostrar éxito |

**Justificación de la minimización:**
- **R1:** Si faltan campos obligatorios, el código único es irrelevante (fusiona casos con campos incompletos)
- **R2:** Si el código está duplicado, no se puede guardar independiente de otros campos opcionales
- **R3:** Usuario está llenando el formulario pero no ha intentado guardar aún
- **R4:** Caso exitoso: todos los requisitos cumplidos, se procede a guardar
- **Nota:** Los campos Descripción y Decano se consideran opcionales basado en el análisis del prototipo

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios principales)
- 4 escenarios adicionales para validar funcionalidades específicas:
  - Acceso al modal mediante botón "+ Nueva Facultad"
  - Cancelar creación de facultad
  - Búsqueda y selección de decano
  - Validación de campos opcionales

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder al formulario de nueva facultad**

**Dado que** estoy autenticado como DGIP en el sistema **Y** estoy en la pantalla "Gestión de Facultades",  
**cuando** hago clic en el botón "+ Nueva Facultad" ubicado en la esquina superior derecha,  
**entonces** se muestra un modal con título "Nueva Facultad" sobre la vista actual **Y** el modal contiene el texto descriptivo "Cree una nueva facultad para el sistema." **Y** se presenta un formulario con los siguientes campos: "Código:" (campo de texto), "Nombre:" (campo de texto), "Descripción" (área de texto multi-línea), "Decano" (campo de búsqueda con icono de lupa) **Y** se muestran dos botones en la parte inferior del modal: "Cancelar" y "Guardar" **Y** el botón "Guardar" tiene color azul oscuro **Y** todos los campos están vacíos listos para ingresar información **Y** el fondo detrás del modal se oscurece indicando que es una ventana modal.

---

**Escenario 2 – Registrar nueva facultad con todos los datos completos**

**Dado que** estoy en el modal "Nueva Facultad" **Y** todos los campos están vacíos,  
**cuando** ingreso un código único en el campo "Código:" (ej: "FIS") **Y** ingreso un nombre en el campo "Nombre:" (ej: "Facultad de Ingeniería en Sistemas") **Y** ingreso texto en el campo "Descripción" (ej: "Facultad dedicada a la excelencia académica y la investigación.") **Y** hago clic en el campo "Decano" con icono de lupa **Y** se despliega una lista de decanos disponibles **Y** selecciono un decano de la lista (ej: "Julio César Sandobalín") **Y** el campo "Decano" muestra el nombre seleccionado **Y** hago clic en el botón "Guardar",  
**entonces** se validan todos los campos **Y** se guarda la nueva facultad en la base de datos **Y** el modal "Nueva Facultad" se cierra automáticamente **Y** regreso a la vista "Gestión de Facultades" **Y** la tabla se actualiza mostrando la nueva facultad agregada con: código "FIS", nombre "Facultad de Ingeniería en Sistemas", número de carreras asociadas inicial (0 o asignado), decano "Julio César Sandobalín", iconos de editar y eliminar **Y** se muestra un mensaje de notificación de éxito con ícono verde de verificación **Y** el mensaje indica "Completado" como título **Y** el mensaje contiene el texto "El registro se ha creado exitosamente" **Y** la notificación aparece en la esquina superior derecha temporalmente.

---

**Escenario 3 – Intentar guardar sin completar campos obligatorios**

**Dado que** estoy en el modal "Nueva Facultad",  
**cuando** dejo vacío el campo "Código:" **O** dejo vacío el campo "Nombre:" **Y** hago clic en el botón "Guardar",  
**entonces** no se cierra el modal **Y** no se guarda ninguna información en la base de datos **Y** se muestran mensajes de error de validación debajo o junto a los campos vacíos obligatorios **Y** los mensajes indican claramente qué campos son requeridos (ej: "El código es obligatorio", "El nombre es obligatorio") **Y** los campos con error se resaltan visualmente (ej: borde rojo) **Y** permanezco en el modal para corregir los errores **Y** puedo completar los campos faltantes y volver a intentar guardar.

---

**Escenario 4 – Intentar registrar facultad con código duplicado**

**Dado que** estoy en el modal "Nueva Facultad" **Y** existen facultades registradas en el sistema con códigos específicos (ej: "FIEE", "FICM", "FAD"),  
**cuando** ingreso un código que ya existe en el sistema en el campo "Código:" (ej: "FIEE") **Y** completo el campo "Nombre:" con cualquier valor **Y** hago clic en el botón "Guardar",  
**entonces** el sistema valida la unicidad del código **Y** detecta que el código "FIEE" ya está en uso **Y** no se cierra el modal **Y** no se guarda la información en la base de datos **Y** se muestra un mensaje de error indicando "El código ya existe en el sistema" o "Este código ya está registrado" **Y** el campo "Código:" se resalta visualmente como error **Y** permanezco en el modal para ingresar un código diferente **Y** puedo modificar el código a uno único y volver a intentar guardar.

---

**Escenario 5 – Registrar facultad solo con campos obligatorios (sin descripción ni decano)**

**Dado que** estoy en el modal "Nueva Facultad",  
**cuando** ingreso un código único en el campo "Código:" (ej: "FIS") **Y** ingreso un nombre en el campo "Nombre:" (ej: "Facultad de Ingeniería en Sistemas") **Y** dejo vacío el campo "Descripción" **Y** dejo sin seleccionar el campo "Decano" **Y** hago clic en el botón "Guardar",  
**entonces** se validan los campos obligatorios (Código y Nombre están completos) **Y** se acepta el registro con campos opcionales vacíos **Y** se guarda la nueva facultad en la base de datos **Y** el modal se cierra automáticamente **Y** la tabla se actualiza mostrando la nueva facultad con: código "FIS", nombre completo, carreras (valor inicial), decano vacío o con valor por defecto **Y** se muestra el mensaje de éxito "Completado - El registro se ha creado exitosamente" **Y** la facultad queda registrada y puede ser editada posteriormente para agregar descripción y decano.

---

**Escenario 6 – Cancelar la creación de una nueva facultad**

**Dado que** estoy en el modal "Nueva Facultad" **Y** he ingresado información en uno o más campos (ej: Código, Nombre, Descripción),  
**cuando** hago clic en el botón "Cancelar",  
**entonces** el modal "Nueva Facultad" se cierra inmediatamente **Y** regreso a la vista "Gestión de Facultades" **Y** no se guarda ninguna información ingresada en la base de datos **Y** la tabla de facultades permanece sin cambios **Y** no se crea ninguna nueva facultad **Y** no se muestra ningún mensaje de éxito ni error **Y** puedo volver a abrir el modal "+ Nueva Facultad" con los campos vacíos si lo deseo.

---

**Escenario 7 – Buscar y seleccionar decano para la facultad**

**Dado que** estoy en el modal "Nueva Facultad" **Y** estoy completando el formulario,  
**cuando** hago clic en el campo "Decano" que tiene un icono de lupa **O** comienzo a escribir en el campo "Decano",  
**entonces** se despliega una lista con nombres de decanos disponibles en el sistema **Y** la lista muestra nombres completos de personas con formato "Nombre Apellido" (ej: "Julio César Sandobalín", "Julio Enrique Soria", "Julio S") **Y** puedo escribir para filtrar la lista en tiempo real **Y** al escribir "Julio" se muestran todos los nombres que contienen "Julio" **Y** puedo hacer clic en un nombre de la lista para seleccionarlo,  
**cuando** selecciono un nombre (ej: "Julio César Sandobalín"),  
**entonces** el campo "Decano" se completa con el nombre seleccionado **Y** la lista de opciones se cierra **Y** el decano queda asignado a la nueva facultad **Y** puedo continuar completando otros campos o guardar el formulario.

---

**Escenario 8 – Validar actualización de tabla después de registrar facultad**

**Dado que** he registrado exitosamente una nueva facultad con código "FIS" y nombre "Facultad de Ingeniería en Sistemas" **Y** el modal se ha cerrado **Y** se ha mostrado el mensaje de éxito,  
**cuando** reviso la tabla en la pantalla "Gestión de Facultades",  
**entonces** se muestra una nueva fila en la tabla con los datos de la facultad recién creada **Y** la fila contiene: código "FIS" en columna Código, "Facultad de Ingeniería en Sistemas" en columna Nombre, número de carreras asociadas en columna Carreras, nombre del decano asignado en columna Decano (o vacío si no se asignó), iconos de lápiz (editar) y papelera (eliminar) en columna Acciones **Y** la nueva facultad aparece en la posición correspondiente según el orden de la tabla (alfabético, por fecha de creación, etc.) **Y** la tabla no requiere recarga manual de la página para mostrar el nuevo registro **Y** puedo interactuar inmediatamente con la nueva facultad (editar o eliminar) usando los iconos de acción.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Registrar nueva facultad con todos los datos completos**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el DGIP quiere "agregar una nueva facultad para mantener actualizada la estructura organizativa de la EPN". El Escenario 2 valida directamente la funcionalidad completa de creación exitosa de una facultad con todos sus datos.

2. **Representa el "happy path" completo del proceso:** Es el flujo ideal que los usuarios ejecutarán más frecuentemente cuando quieran registrar una nueva facultad con información completa y de calidad. Demuestra el valor completo de la funcionalidad.

3. **Valida el flujo end-to-end completo:** Verifica todos los componentes críticos del proceso de registro:
   - Acceso al formulario mediante modal
   - Entrada de todos los campos (obligatorios y opcionales)
   - Búsqueda y selección de decano
   - Validación de datos
   - Persistencia en base de datos
   - Actualización de la UI
   - Retroalimentación al usuario mediante mensaje de éxito

4. **Impacto directo en la estructura organizativa (objetivo de la HU):** Solo con un registro completo y exitoso, el DGIP puede:
   - Mantener actualizada la estructura organizativa real de la EPN
   - Asegurar que las facultades tienen toda su información necesaria
   - Facilitar la gestión posterior de carreras asociadas
   - Garantizar trazabilidad con decanos asignados

5. **Valida componentes visuales críticos observados en el prototipo:**
   - Modal completo con todos los campos (Imágenes 6, 7, 8)
   - Funcionalidad de búsqueda de decano (Imagen 7)
   - Mensaje de éxito específico "Completado - El registro se ha creado exitosamente" (Imagen 9)
   - Actualización automática de la tabla

6. **Fundamento para casos de error y validación:** Los escenarios de error (3, 4) solo tienen sentido si primero se valida que el caso exitoso funciona correctamente. Sin un happy path operativo, las validaciones carecen de contexto.

7. **Mayor valor para el usuario final:** Registrar una facultad completa (con código, nombre, descripción y decano) proporciona:
   - Información completa para gestión académica
   - Datos suficientes para reportes y análisis
   - Claridad sobre responsables (decano asignado)
   - Documentación adecuada (descripción)

8. **Validación de integración entre componentes:** El escenario verifica la integración correcta de:
   - Frontend (modal, formulario, búsqueda)
   - Backend (validación, persistencia)
   - UI actualización (tabla, notificaciones)
   - Base de datos (almacenamiento)

9. **Refleja el flujo completo del prototipo:** Las Imágenes 6-9 muestran específicamente este flujo completo desde modal vacío hasta mensaje de éxito, indicando que este es el flujo principal diseñado.

10. **Impacto en adopción del sistema:** Si el registro completo no funciona correctamente:
    - Los usuarios no confiarán en la funcionalidad
    - Se perderá el valor de mantener estructura actualizada
    - Habrá frustración por información incompleta
    - La promesa de la HU no se cumplirá

Los demás escenarios son importantes para robustez (validaciones, cancelación) y casos alternativos (solo obligatorios), pero el Escenario 2 es el que garantiza que el sistema cumple su promesa fundamental: **permitir al DGIP agregar una nueva facultad completa con toda su información para mantener efectivamente actualizada la estructura organizativa de la EPN, que es el valor central y el caso de uso principal de esta funcionalidad**.