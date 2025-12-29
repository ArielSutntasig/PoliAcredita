# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 10 y patrón de registro observado):**

1. **C1:** Se hace clic en el botón "+ Nueva Carrera"
2. **C2:** El campo "Código*" está completo con un código único
3. **C3:** El campo "Nombre*" está completo
4. **C4:** El campo "Descripción" está completo (opcional)
5. **C5:** Se ha seleccionado una Facultad mediante el campo de búsqueda "Facultad*"
6. **C6:** Se ha seleccionado un Coordinador mediante el campo de búsqueda "Coordinador*"
7. **C7:** El código ingresado ya existe en el sistema (duplicado)
8. **C8:** Se hace clic en el botón "Guardar"
9. **C9:** Se hace clic en el botón "Cancelar"

### **Acciones del Sistema (inferidas del patrón de prototipos observados):**

1. **A1:** Mostrar modal "Nueva Carrera" sobre la vista de gestión de carreras
2. **A2:** Presentar formulario con campos: "Código*", "Nombre*", "Descripción", "Facultad*", "Coordinador*"
3. **A3:** Mostrar campos obligatorios marcados con asterisco (*)
4. **A4:** Mostrar campo "Facultad*" con funcionalidad de búsqueda (icono de lupa)
5. **A5:** Desplegar lista de facultades disponibles al buscar
6. **A6:** Permitir seleccionar una facultad de la lista
7. **A7:** Mostrar campo "Coordinador*" con funcionalidad de búsqueda
8. **A8:** Desplegar lista de coordinadores disponibles al buscar
9. **A9:** Permitir seleccionar un coordinador de la lista
10. **A10:** Validar que campos obligatorios estén completos
11. **A11:** Validar que el código no esté duplicado en el sistema
12. **A12:** Mostrar mensajes de error de validación si corresponde
13. **A13:** Guardar la nueva carrera en la base de datos
14. **A14:** Cerrar el modal después de guardar exitosamente
15. **A15:** Actualizar la tabla de carreras agregando la nueva fila
16. **A16:** Mostrar mensaje de éxito "Completado - El registro se ha creado exitosamente"
17. **A17:** Cerrar el modal sin guardar si se presiona "Cancelar"
18. **A18:** No realizar cambios en la base de datos si se cancela

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 5 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Campos obligatorios completos (Código, Nombre, Facultad, Coordinador)
- **C2:** Campo Descripción completo
- **C3:** Código es único (no duplicado)
- **C4:** Usuario hace clic en "Guardar"

Total combinaciones teóricas: 2^4 = 16 reglas (simplificadas)

| Regla | Campos obligatorios | Descripción | Código único | Clic Guardar | Acción |
|-------|---------------------|-------------|--------------|--------------|---------|
| R1 | N | - | - | N | Sin acción (espera) |
| R2 | N | - | - | S | A12: Error de validación |
| R3 | S | N | N | S | A12: Error código duplicado |
| R4 | S | N | S | N | Sin acción (espera) |
| R5 | S | N | S | S | A13-A16: Guardar sin descripción |
| R6 | S | S | N | S | A12: Error código duplicado |
| R7 | S | S | S | N | Sin acción (espera) |
| R8 | S | S | S | S | A13-A16: Guardar completo (happy path) |

---

## **Tabla de Decisión Minimizada**

| Regla | Campos obligatorios | Código único | Clic Guardar | Acción |
|-------|---------------------|-------------|--------------|---------|
| **R1** | N | - | S | Mostrar error "Campos obligatorios requeridos" |
| **R2** | S | N | S | Mostrar error "El código ya existe" |
| **R3** | S | S | N | Sin acción, esperar interacción del usuario |
| **R4** | S | S | S | Guardar carrera, cerrar modal, mostrar éxito |

**Justificación de la minimización:**
- **R1:** Si faltan campos obligatorios, el código único es irrelevante (fusiona casos con campos incompletos)
- **R2:** Si el código está duplicado, no se puede guardar independiente de otros campos opcionales
- **R3:** Usuario está llenando el formulario pero no ha intentado guardar aún
- **R4:** Caso exitoso: todos los requisitos cumplidos, se procede a guardar
- **Nota:** El campo Descripción se considera opcional basado en el patrón observado

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios principales)
- 5 escenarios adicionales para validar funcionalidades específicas:
  - Acceso al modal mediante botón "+ Nueva Carrera"
  - Cancelar creación de carrera
  - Búsqueda y selección de facultad
  - Búsqueda y selección de coordinador
  - Validación de actualización de tabla

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder al formulario de nueva carrera**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** estoy en la pantalla "Gestión de Carreras",  
**cuando** hago clic en el botón "+ Nueva Carrera" ubicado en la esquina superior derecha,  
**entonces** se muestra un modal con título "Nueva Carrera" sobre la vista actual **Y** el modal contiene texto descriptivo como "Cree una nueva carrera para el sistema." **Y** se presenta un formulario con los siguientes campos obligatorios marcados con asterisco (*): "Código*", "Nombre*", "Facultad*", "Coordinador*" **Y** se incluye el campo opcional "Descripción" (área de texto multi-línea) **Y** se muestran dos botones en la parte inferior del modal: "Cancelar" y "Guardar" **Y** el botón "Guardar" tiene color azul oscuro **Y** todos los campos están vacíos listos para ingresar información **Y** el fondo detrás del modal se oscurece indicando que es una ventana modal.

---

**Escenario 2 – Registrar nueva carrera con todos los datos completos**

**Dado que** estoy en el modal "Nueva Carrera" **Y** todos los campos están vacíos,  
**cuando** ingreso un código único en el campo "Código*" (ej: "IS-SW") **Y** ingreso un nombre en el campo "Nombre*" (ej: "Ingeniería de Software") **Y** ingreso texto en el campo "Descripción" (ej: "Carrera enfocada en desarrollo de software y gestión de proyectos tecnológicos.") **Y** hago clic en el campo "Facultad*" con icono de lupa **Y** se despliega una lista de facultades disponibles **Y** selecciono una facultad de la lista (ej: "Facultad de Ingeniería de Sistemas") **Y** el campo "Facultad*" muestra el nombre seleccionado **Y** hago clic en el campo "Coordinador*" con icono de lupa **Y** se despliega una lista de coordinadores disponibles **Y** selecciono un coordinador de la lista (ej: "Dr. Juan Pérez") **Y** el campo "Coordinador*" muestra el nombre seleccionado **Y** hago clic en el botón "Guardar",  
**entonces** se validan todos los campos **Y** se guarda la nueva carrera en la base de datos **Y** el modal "Nueva Carrera" se cierra automáticamente **Y** regreso a la vista "Gestión de Carreras" **Y** la tabla se actualiza mostrando la nueva carrera agregada con: código "IS-SW" en columna Código, "Ingeniería de Software" en columna Nombre, "Facultad de Ingeniería de Sistemas" en columna Facultad, "Dr. Juan Pérez" en columna Coordinador, iconos de editar (lápiz) y eliminar (papelera) en columna Acciones **Y** se muestra un mensaje de notificación de éxito con ícono verde de verificación **Y** el mensaje indica "Completado" como título **Y** el mensaje contiene el texto "El registro se ha creado exitosamente" **Y** la notificación aparece en la esquina superior derecha temporalmente.

---

**Escenario 3 – Intentar guardar sin completar campos obligatorios**

**Dado que** estoy en el modal "Nueva Carrera",  
**cuando** dejo vacío uno o más campos obligatorios (Código*, Nombre*, Facultad*, Coordinador*) **Y** hago clic en el botón "Guardar",  
**entonces** no se cierra el modal **Y** no se guarda ninguna información en la base de datos **Y** se muestran mensajes de error de validación debajo o junto a los campos vacíos obligatorios **Y** los mensajes indican claramente qué campos son requeridos (ej: "El código es obligatorio", "El nombre es obligatorio", "Debe seleccionar una facultad", "Debe seleccionar un coordinador") **Y** los campos con error se resaltan visualmente (ej: borde rojo) **Y** permanezco en el modal para corregir los errores **Y** puedo completar los campos faltantes y volver a intentar guardar.

---

**Escenario 4 – Intentar registrar carrera con código duplicado**

**Dado que** estoy en el modal "Nueva Carrera" **Y** existen carreras registradas en el sistema con códigos específicos (ej: "IS-ING", "ADM-NEG", "IC-CIV"),  
**cuando** ingreso un código que ya existe en el sistema en el campo "Código*" (ej: "IS-ING") **Y** completo todos los demás campos obligatorios correctamente (Nombre, Facultad, Coordinador) **Y** hago clic en el botón "Guardar",  
**entonces** el sistema valida la unicidad del código **Y** detecta que el código "IS-ING" ya está en uso **Y** no se cierra el modal **Y** no se guarda la información en la base de datos **Y** se muestra un mensaje de error indicando "El código ya existe en el sistema" o "Este código ya está registrado" **Y** el campo "Código*" se resalta visualmente como error **Y** permanezco en el modal para ingresar un código diferente **Y** puedo modificar el código a uno único y volver a intentar guardar.

---

**Escenario 5 – Registrar carrera solo con campos obligatorios (sin descripción)**

**Dado que** estoy en el modal "Nueva Carrera",  
**cuando** ingreso un código único en el campo "Código*" (ej: "IS-SW") **Y** ingreso un nombre en el campo "Nombre*" (ej: "Ingeniería de Software") **Y** dejo vacío el campo "Descripción" **Y** selecciono una facultad en el campo "Facultad*" (ej: "Facultad de Ingeniería de Sistemas") **Y** selecciono un coordinador en el campo "Coordinador*" (ej: "Dr. Juan Pérez") **Y** hago clic en el botón "Guardar",  
**entonces** se validan los campos obligatorios (Código, Nombre, Facultad y Coordinador están completos) **Y** se acepta el registro con el campo opcional Descripción vacío **Y** se guarda la nueva carrera en la base de datos **Y** el modal se cierra automáticamente **Y** la tabla se actualiza mostrando la nueva carrera con todos sus datos excepto descripción **Y** se muestra el mensaje de éxito "Completado - El registro se ha creado exitosamente" **Y** la carrera queda registrada y puede ser editada posteriormente para agregar descripción.

---

**Escenario 6 – Cancelar la creación de una nueva carrera**

**Dado que** estoy en el modal "Nueva Carrera" **Y** he ingresado información en uno o más campos (ej: Código, Nombre, Facultad),  
**cuando** hago clic en el botón "Cancelar",  
**entonces** el modal "Nueva Carrera" se cierra inmediatamente **Y** regreso a la vista "Gestión de Carreras" **Y** no se guarda ninguna información ingresada en la base de datos **Y** la tabla de carreras permanece sin cambios **Y** no se crea ninguna nueva carrera **Y** no se muestra ningún mensaje de éxito ni error **Y** puedo volver a abrir el modal "+ Nueva Carrera" con los campos vacíos si lo deseo.

---

**Escenario 7 – Buscar y seleccionar facultad para la carrera**

**Dado que** estoy en el modal "Nueva Carrera" **Y** estoy completando el formulario,  
**cuando** hago clic en el campo "Facultad*" que tiene un icono de lupa **O** comienzo a escribir en el campo "Facultad*",  
**entonces** se despliega una lista con nombres de facultades disponibles en el sistema **Y** la lista muestra nombres completos de facultades (ej: "Facultad de Ingeniería de Sistemas", "Facultad de Ingeniería Civil", "Facultad de Ciencias Administrativas") **Y** puedo escribir para filtrar la lista en tiempo real **Y** al escribir "Sistemas" se muestran todas las facultades que contienen "Sistemas" **Y** puedo hacer clic en un nombre de la lista para seleccionarlo,  
**cuando** selecciono una facultad (ej: "Facultad de Ingeniería de Sistemas"),  
**entonces** el campo "Facultad*" se completa con el nombre seleccionado **Y** la lista de opciones se cierra **Y** la facultad queda asignada a la nueva carrera **Y** puedo continuar completando otros campos o guardar el formulario.

---

**Escenario 8 – Buscar y seleccionar coordinador para la carrera**

**Dado que** estoy en el modal "Nueva Carrera" **Y** estoy completando el formulario,  
**cuando** hago clic en el campo "Coordinador*" que tiene un icono de lupa **O** comienzo a escribir en el campo "Coordinador*",  
**entonces** se despliega una lista con nombres de coordinadores disponibles en el sistema **Y** la lista muestra nombres completos de personas (ej: "Dr. Juan Pérez", "Dra. Ana García", "Ing. Luis Martínez") **Y** puedo escribir para filtrar la lista en tiempo real **Y** al escribir "Juan" se muestran todos los nombres que contienen "Juan" **Y** puedo hacer clic en un nombre de la lista para seleccionarlo,  
**cuando** selecciono un coordinador (ej: "Dr. Juan Pérez"),  
**entonces** el campo "Coordinador*" se completa con el nombre seleccionado **Y** la lista de opciones se cierra **Y** el coordinador queda asignado a la nueva carrera **Y** puedo continuar completando otros campos o guardar el formulario.

---

**Escenario 9 – Validar actualización de tabla después de registrar carrera**

**Dado que** he registrado exitosamente una nueva carrera con código "IS-SW" y nombre "Ingeniería de Software" **Y** el modal se ha cerrado **Y** se ha mostrado el mensaje de éxito,  
**cuando** reviso la tabla en la pantalla "Gestión de Carreras",  
**entonces** se muestra una nueva fila en la tabla con los datos de la carrera recién creada **Y** la fila contiene: código "IS-SW" en columna Código, "Ingeniería de Software" en columna Nombre, "Facultad de Ingeniería de Sistemas" en columna Facultad, "Dr. Juan Pérez" en columna Coordinador, iconos de lápiz (editar) y papelera (eliminar) en columna Acciones **Y** la nueva carrera aparece en la posición correspondiente según el orden de la tabla **Y** la tabla no requiere recarga manual de la página para mostrar el nuevo registro **Y** puedo interactuar inmediatamente con la nueva carrera (editar o eliminar) usando los iconos de acción **Y** la carrera queda disponible para asignación de estudiantes y gestión académica.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Registrar nueva carrera con todos los datos completos**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que la Autoridad quiere "registrar una carrera para agregar una oferta académica". El Escenario 2 valida directamente la funcionalidad completa de creación exitosa de una carrera con toda su información necesaria, cumpliendo el objetivo de agregar oferta académica.

2. **Representa el "happy path" completo del proceso:** Es el flujo ideal que las autoridades académicas ejecutarán cuando necesiten ampliar la oferta académica de la institución con una nueva carrera. Demuestra el valor completo de la funcionalidad con información rica y completa.

3. **Valida el flujo end-to-end completo:** Verifica todos los componentes críticos del proceso de registro:
   - Acceso al formulario mediante modal
   - Entrada de todos los campos (obligatorios y opcionales)
   - Búsqueda y selección de facultad (vinculación organizacional)
   - Búsqueda y selección de coordinador (asignación de responsable)
   - Validación de datos
   - Persistencia en base de datos
   - Actualización automática de la UI
   - Retroalimentación mediante mensaje de éxito

4. **Impacto directo en la oferta académica (objetivo de la HU):** Solo con un registro completo y exitoso, la Autoridad puede:
   - Agregar efectivamente una nueva carrera a la oferta académica de la EPN
   - Establecer la estructura organizacional (facultad asociada)
   - Asignar responsabilidad académica (coordinador)
   - Documentar la carrera adecuadamente (descripción)
   - Habilitar la carrera para admisión de estudiantes

5. **Valida componentes académicos críticos:** El escenario verifica la captura de información esencial:
   - **Código:** Identificador único institucional de la carrera
   - **Nombre:** Denominación oficial de la carrera
   - **Facultad:** Vinculación a unidad académica organizacional
   - **Coordinador:** Responsable académico-administrativo asignado
   - **Descripción:** Documentación del alcance y enfoque de la carrera

6. **Fundamento para casos de error y validación:** Los escenarios de error (3, 4) solo tienen sentido si primero se valida que el caso exitoso funciona correctamente. Sin un happy path operativo, las validaciones carecen de contexto y propósito.

7. **Mayor valor para ampliación de oferta académica:** Un registro completo proporciona:
   - Información completa para publicación en portales institucionales
   - Datos suficientes para trámites regulatorios y acreditación
   - Claridad sobre responsables (coordinador asignado desde el inicio)
   - Documentación adecuada para estudiantes potenciales (descripción)
   - Vinculación organizacional clara (facultad)

8. **Validación de integración entre componentes:** El escenario verifica la integración correcta de:
   - Frontend (modal, formulario, búsquedas con lupa)
   - Backend (validación, persistencia, relaciones)
   - Base de datos (almacenamiento, unicidad, relaciones FK con facultades y coordinadores)
   - UI (actualización de tabla, notificaciones)

9. **Impacto en crecimiento institucional:** Si el registro completo no funciona:
   - La institución no puede ampliar su oferta académica
   - Se bloquea el crecimiento estratégico de la EPN
   - No se pueden crear nuevas carreras para responder a demanda del mercado
   - La promesa de "agregar oferta académica" no se cumple

10. **Precedencia estratégica:** En instituciones académicas:
    - Agregar carreras es una decisión estratégica importante
    - Requiere información completa desde el inicio
    - Debe tener responsable asignado inmediatamente
    - Debe estar vinculada organizacionalmente (facultad)
    - La calidad del registro inicial determina la gestión posterior

Los demás escenarios son importantes para robustez (validaciones, cancelación) y casos alternativos (solo obligatorios), pero el Escenario 2 es el que garantiza que el sistema cumple su promesa fundamental: **permitir a la Autoridad registrar completamente una nueva carrera con toda su información académica y organizacional para agregar efectivamente oferta académica a la EPN, que es el valor central y el caso de uso principal de esta funcionalidad crítica para el crecimiento institucional**.