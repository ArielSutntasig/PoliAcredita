# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imágenes 15, 16 y 17 del prototipo):**

1. **C1:** Se hace clic en el botón "+ Nuevo Usuario"
2. **C2:** El campo "Cédula*" está completo con un número de cédula válido
3. **C3:** El campo "Nombres*" está completo
4. **C4:** El campo "Apellidos*" está completo
5. **C5:** El campo "Email*" está completo con un email institucional válido
6. **C6:** El campo "Teléfono" está completo (opcional)
7. **C7:** Se ha seleccionado al menos un rol del dropdown "Rol*"
8. **C8:** Se ha seleccionado una facultad mediante el campo de búsqueda "Facultad*"
9. **C9:** El email ingresado ya existe en el sistema (duplicado)
10. **C10:** La cédula ingresada ya existe en el sistema (duplicada)
11. **C11:** Se hace clic en el botón "Guardar"
12. **C12:** Se hace clic en el botón "Cancelar"

### **Acciones del Sistema (observadas en Imágenes 15, 16 y 17):**

1. **A1:** Mostrar modal "Nuevo Usuario" sobre la vista de gestión de usuarios
2. **A2:** Presentar formulario con campos: "Cédula*", "Nombres*", "Apellidos*", "Email*", "Teléfono", "Rol*", "Facultad*"
3. **A3:** Mostrar campos obligatorios marcados con asterisco (*)
4. **A4:** Mostrar dropdown "Rol*" con opciones múltiples seleccionables
5. **A5:** Permitir seleccionar uno o múltiples roles (ej: "Profesor / Coordinador de Carrera")
6. **A6:** Mostrar campo "Facultad*" con funcionalidad de búsqueda (icono de lupa)
7. **A7:** Desplegar lista de facultades disponibles al buscar
8. **A8:** Permitir seleccionar una facultad de la lista
9. **A9:** Validar que todos los campos obligatorios estén completos
10. **A10:** Validar formato de email institucional
11. **A11:** Validar que la cédula no esté duplicada
12. **A12:** Validar que el email no esté duplicado
13. **A13:** Mostrar mensajes de error de validación si corresponde
14. **A14:** Guardar el nuevo usuario en la base de datos con estado "Activo" por defecto
15. **A15:** Cerrar el modal después de guardar exitosamente
16. **A16:** Actualizar la tabla de usuarios agregando la nueva fila
17. **A17:** Mostrar mensaje de éxito "Completado - El registro se ha creado exitosamente" (Imagen 17)
18. **A18:** Cerrar el modal sin guardar si se presiona "Cancelar"
19. **A19:** No realizar cambios en la base de datos si se cancela

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 6 condiciones principales más relevantes (simplificadas):

**Condiciones simplificadas:**
- **C1:** Campos obligatorios completos (Cédula, Nombres, Apellidos, Email, Rol, Facultad)
- **C2:** Email es válido (formato institucional)
- **C3:** Cédula es única (no duplicada)
- **C4:** Email es único (no duplicado)
- **C5:** Usuario hace clic en "Guardar"

Total combinaciones teóricas: 2^5 = 32 reglas (simplificadas a casos más relevantes)

| Regla | Campos obligatorios | Email válido | Cédula única | Email único | Clic Guardar | Acción |
|-------|---------------------|--------------|--------------|-------------|--------------|---------|
| R1 | N | - | - | - | N | Sin acción (espera) |
| R2 | N | - | - | - | S | A13: Error validación campos obligatorios |
| R3 | S | N | - | - | S | A13: Error formato email |
| R4 | S | S | N | - | S | A13: Error cédula duplicada |
| R5 | S | S | S | N | S | A13: Error email duplicado |
| R6 | S | S | S | S | N | Sin acción (espera) |
| R7 | S | S | S | S | S | A14-A17: Guardar usuario exitosamente |

---

## **Tabla de Decisión Minimizada**

| Regla | Campos obligatorios | Email válido | Cédula única | Email único | Clic Guardar | Acción |
|-------|---------------------|--------------|--------------|-------------|--------------|---------|
| **R1** | N | - | - | - | S | Mostrar error "Campos obligatorios requeridos" |
| **R2** | S | N | - | - | S | Mostrar error "Formato de email inválido" |
| **R3** | S | S | N | - | S | Mostrar error "La cédula ya está registrada" |
| **R4** | S | S | S | N | S | Mostrar error "El email ya está registrado" |
| **R5** | S | S | S | S | N | Sin acción, esperar interacción |
| **R6** | S | S | S | S | S | Guardar usuario, cerrar modal, mostrar éxito |

**Justificación de la minimización:**
- **R1:** Si faltan campos obligatorios, las demás validaciones son irrelevantes
- **R2:** Si el email no es válido, la unicidad es irrelevante
- **R3:** Si la cédula está duplicada, no se puede registrar
- **R4:** Si el email está duplicado, no se puede registrar
- **R5:** Usuario está llenando el formulario pero no ha intentado guardar
- **R6:** Caso exitoso: todos los requisitos cumplidos, se procede a guardar

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 10 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios principales)
- 4 escenarios adicionales para validar funcionalidades específicas:
  - Acceso al modal mediante botón "+ Nuevo Usuario"
  - Cancelar creación de usuario
  - Selección de múltiples roles
  - Búsqueda y selección de facultad

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder al formulario de nuevo usuario**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios",  
**cuando** hago clic en el botón "+ Nuevo Usuario" ubicado en la esquina superior derecha,  
**entonces** se muestra un modal con título "Nuevo Usuario" sobre la vista actual **Y** el modal contiene el texto descriptivo "Completa los detalles del usuario. Haz clic en guardar cuando hayas terminado." **Y** se presenta un formulario con los siguientes campos obligatorios marcados con asterisco (*): "Cédula*", "Nombres*", "Apellidos*", "Email*", "Rol*", "Facultad*" **Y** se incluye el campo opcional "Teléfono" sin asterisco **Y** se muestran dos botones en la parte inferior del modal: "Cancelar" y "Guardar" **Y** el botón "Guardar" tiene color azul oscuro **Y** todos los campos están vacíos listos para ingresar información **Y** el fondo detrás del modal se oscurece indicando que es una ventana modal.

---

**Escenario 2 – Registrar nuevo usuario con todos los datos completos**

**Dado que** estoy en el modal "Nuevo Usuario" **Y** todos los campos están vacíos,  
**cuando** ingreso un número de cédula válido en "Cédula*" (ej: "1726285040") **Y** ingreso nombres en "Nombres*" (ej: "Julio César") **Y** ingreso apellidos en "Apellidos*" (ej: "Sandobalín") **Y** ingreso un email institucional válido en "Email*" (ej: "julio.sandobalin@epn.edu.ec") **Y** ingreso un teléfono en "Teléfono" (ej: "0995498636") **Y** hago clic en el dropdown "Rol*" **Y** selecciono uno o más roles de la lista (ej: selecciono "Profesor" y "Coordinador de Carrera" resultando en "Profesor / Coordinador de Carrera") **Y** hago clic en el campo "Facultad*" con icono de lupa **Y** se despliega una lista de facultades disponibles **Y** selecciono una facultad (ej: "Facultad Ingeniería en Sistemas") **Y** hago clic en el botón "Guardar",  
**entonces** se validan todos los campos **Y** se guarda el nuevo usuario en la base de datos con estado "Activo" por defecto **Y** el modal "Nuevo Usuario" se cierra automáticamente **Y** regreso a la vista "Gestión de Usuarios" **Y** la tabla se actualiza mostrando el nuevo usuario agregado con: email "julio.sandobalin@epn.ed" en columna Email, "Julio Sandobalin" en columna Nombre, "Profesor / Coordinador de Carrera" o roles seleccionados en columna Rol, etiqueta verde "Activo" en columna Estado, iconos de editar y eliminar en columna Acciones **Y** se muestra un mensaje de notificación de éxito con ícono verde de verificación **Y** el mensaje indica "Completado" como título **Y** el mensaje contiene el texto "El registro se ha creado exitosamente" **Y** la notificación aparece en la esquina superior derecha temporalmente.

---

**Escenario 3 – Intentar guardar sin completar campos obligatorios**

**Dado que** estoy en el modal "Nuevo Usuario",  
**cuando** dejo vacío uno o más campos obligatorios (Cédula*, Nombres*, Apellidos*, Email*, Rol*, Facultad*) **Y** hago clic en el botón "Guardar",  
**entonces** no se cierra el modal **Y** no se guarda ninguna información en la base de datos **Y** se muestran mensajes de error de validación debajo o junto a los campos vacíos obligatorios **Y** los mensajes indican claramente qué campos son requeridos (ej: "La cédula es obligatoria", "El nombre es obligatorio", "Debe seleccionar al menos un rol", "Debe seleccionar una facultad") **Y** los campos con error se resaltan visualmente (ej: borde rojo) **Y** permanezco en el modal para corregir los errores **Y** puedo completar los campos faltantes y volver a intentar guardar.

---

**Escenario 4 – Intentar registrar usuario con email inválido**

**Dado que** estoy en el modal "Nuevo Usuario" **Y** he completado todos los campos obligatorios,  
**cuando** ingreso un email que no tiene formato institucional válido en "Email*" (ej: "usuario@gmail.com" en lugar de "@epn.edu.ec") **Y** hago clic en el botón "Guardar",  
**entonces** el sistema valida el formato del email **Y** detecta que no es un email institucional válido **Y** no se cierra el modal **Y** no se guarda la información en la base de datos **Y** se muestra un mensaje de error indicando "Debe ingresar un email institucional válido" o "El email debe tener el dominio @epn.edu.ec" **Y** el campo "Email*" se resalta visualmente como error **Y** permanezco en el modal para corregir el email **Y** puedo ingresar un email válido y volver a intentar guardar.

---

**Escenario 5 – Intentar registrar usuario con cédula duplicada**

**Dado que** estoy en el modal "Nuevo Usuario" **Y** existen usuarios registrados en el sistema con cédulas específicas,  
**cuando** ingreso una cédula que ya existe en el sistema en "Cédula*" (ej: una cédula ya registrada) **Y** completo todos los demás campos obligatorios correctamente **Y** hago clic en el botón "Guardar",  
**entonces** el sistema valida la unicidad de la cédula **Y** detecta que la cédula ya está registrada **Y** no se cierra el modal **Y** no se guarda la información en la base de datos **Y** se muestra un mensaje de error indicando "La cédula ya está registrada en el sistema" o "Esta cédula ya existe" **Y** el campo "Cédula*" se resalta visualmente como error **Y** permanezco en el modal para verificar o ingresar una cédula diferente.

---

**Escenario 6 – Intentar registrar usuario con email duplicado**

**Dado que** estoy en el modal "Nuevo Usuario" **Y** existen usuarios registrados en el sistema con emails específicos,  
**cuando** ingreso un email que ya existe en el sistema en "Email*" (ej: "juan.perez@epn.edu.ec" que ya está registrado) **Y** completo todos los demás campos obligatorios correctamente **Y** hago clic en el botón "Guardar",  
**entonces** el sistema valida la unicidad del email **Y** detecta que el email ya está registrado **Y** no se cierra el modal **Y** no se guarda la información en la base de datos **Y** se muestra un mensaje de error indicando "El email ya está registrado en el sistema" o "Este email ya existe" **Y** el campo "Email*" se resalta visualmente como error **Y** permanezco en el modal para ingresar un email diferente.

---

**Escenario 7 – Cancelar la creación de un nuevo usuario**

**Dado que** estoy en el modal "Nuevo Usuario" **Y** he ingresado información en uno o más campos,  
**cuando** hago clic en el botón "Cancelar",  
**entonces** el modal "Nuevo Usuario" se cierra inmediatamente **Y** regreso a la vista "Gestión de Usuarios" **Y** no se guarda ninguna información ingresada en la base de datos **Y** la tabla de usuarios permanece sin cambios **Y** no se crea ningún nuevo usuario **Y** no se muestra ningún mensaje de éxito ni error **Y** puedo volver a abrir el modal "+ Nuevo Usuario" con los campos vacíos si lo deseo.

---

**Escenario 8 – Seleccionar múltiples roles para el usuario**

**Dado que** estoy en el modal "Nuevo Usuario" **Y** estoy completando el formulario,  
**cuando** hago clic en el dropdown "Rol*",  
**entonces** se despliega una lista con roles disponibles que incluyen opciones como: "Administrador", "Coordinador de Carrera", "Cómite Evaluación Interna (CEI)", "Autoridad Académica", "Profesor" **Y** puedo seleccionar un solo rol haciendo clic en una opción **Y** puedo seleccionar múltiples roles haciendo clic en varias opciones (probablemente mediante checkboxes),  
**cuando** selecciono múltiples roles (ej: "Profesor" y "Coordinador de Carrera"),  
**entonces** el campo "Rol*" muestra los roles seleccionados separados por " / " (ej: "Profesor / Coordinador de Carrera") **Y** los roles quedan asignados al nuevo usuario **Y** puedo continuar completando otros campos o guardar el formulario **Y** al guardar, el usuario tendrá acceso a las funcionalidades de todos los roles asignados.

---

**Escenario 9 – Buscar y seleccionar facultad para el usuario**

**Dado que** estoy en el modal "Nuevo Usuario" **Y** estoy completando el formulario,  
**cuando** hago clic en el campo "Facultad*" que tiene un icono de lupa **O** comienzo a escribir en el campo "Facultad*",  
**entonces** se despliega una lista con nombres de facultades disponibles en el sistema **Y** la lista muestra nombres completos de facultades (ej: "Facultad Ingeniería en Sistemas", "Facultad de Ingeniería Eléctrica y Electrónica") **Y** puedo escribir para filtrar la lista en tiempo real **Y** al escribir "Ingeniería" se muestran todas las facultades que contienen "Ingeniería" **Y** puedo hacer clic en un nombre de la lista para seleccionarlo,  
**cuando** selecciono una facultad (ej: "Facultad Ingeniería en Sistemas"),  
**entonces** el campo "Facultad*" se completa con el nombre seleccionado **Y** la lista de opciones se cierra **Y** la facultad queda asignada al nuevo usuario **Y** puedo continuar completando otros campos o guardar el formulario.

---

**Escenario 10 – Validar que el nuevo usuario se crea con estado "Activo" por defecto**

**Dado que** he registrado exitosamente un nuevo usuario completando todos los campos obligatorios **Y** el modal se ha cerrado **Y** se ha mostrado el mensaje de éxito,  
**cuando** reviso la tabla en la pantalla "Gestión de Usuarios" **Y** ubico la fila del usuario recién creado,  
**entonces** el nuevo usuario aparece en la tabla con todos sus datos **Y** en la columna "Estado" se muestra una etiqueta verde con el texto "Activo" **Y** el usuario no tiene estado "Inactivo" por defecto **Y** el estado "Activo" significa que el usuario puede iniciar sesión inmediatamente en el sistema **Y** el usuario puede acceder a las funcionalidades correspondientes a sus roles asignados sin necesidad de activación adicional **Y** un Administrador puede posteriormente cambiar el estado a "Inactivo" si es necesario mediante la funcionalidad de edición.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Registrar nuevo usuario con todos los datos completos**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Administrador quiere "registrar un nuevo usuario para permitir que nuevas personas accedan a la plataforma". El Escenario 2 valida directamente la funcionalidad completa de creación exitosa de un usuario con todos sus datos necesarios.

2. **Representa el "happy path" completo del proceso:** Es el flujo ideal y más frecuente que los administradores ejecutarán cuando necesiten dar acceso a nuevos usuarios (profesores, coordinadores, personal académico) al sistema. Demuestra el valor completo de la funcionalidad de registro.

3. **Valida el flujo end-to-end completo:** Verifica todos los componentes críticos del proceso de registro:
   - Acceso al formulario mediante modal
   - Entrada de todos los campos obligatorios y opcionales
   - Selección de roles (incluyendo múltiples roles)
   - Búsqueda y asignación de facultad
   - Validaciones de datos
   - Persistencia en base de datos
   - Creación con estado "Activo" por defecto
   - Actualización automática de la UI
   - Retroalimentación mediante mensaje de éxito específico

4. **Impacto directo en el objetivo de la HU (permitir acceso):** Solo con un registro completo y exitoso:
   - Las nuevas personas pueden efectivamente acceder a la plataforma
   - Los usuarios quedan habilitados inmediatamente (estado "Activo")
   - Se asignan correctamente roles y permisos de acceso
   - Se establece la vinculación con facultades para contexto académico

5. **Valida componentes visuales y funcionales críticos observados en el prototipo:**
   - Modal completo con todos los campos obligatorios y opcionales (Imagen 15)
   - Selección de roles múltiples ("Profesor / Coordinador de Carrera") (Imagen 16)
   - Búsqueda de facultad ("Facultad Ingeniería en Sistemas") (Imagen 16)
   - Mensaje de éxito específico "Completado - El registro se ha creado exitosamente" (Imagen 17)
   - Actualización de tabla con nuevo usuario visible

6. **Fundamento para casos de validación y error:** Los escenarios de error (3-6) solo tienen sentido si primero se valida que el caso exitoso funciona correctamente. Sin un happy path operativo, las validaciones carecen de contexto y propósito.

7. **Mayor valor para gestión de acceso:** Un registro completo proporciona:
   - Información completa del usuario (identificación, contacto)
   - Roles claramente definidos (determina permisos de acceso)
   - Contexto académico (facultad asignada)
   - Habilitación inmediata (estado "Activo")
   - Trazabilidad y auditoría completa

8. **Validación de integración entre múltiples componentes:** El escenario verifica la integración correcta de:
   - Frontend (modal, formulario, dropdowns, búsqueda)
   - Backend (validaciones múltiples, lógica de negocio)
   - Base de datos (persistencia, unicidad)
   - Sistema de permisos (asignación de roles)
   - UI (actualización, notificaciones)

9. **Impacto en adopción y confianza del sistema:** Si el registro completo no funciona:
   - Los administradores no pueden incorporar nuevos usuarios
   - Se bloquea el crecimiento de la base de usuarios
   - Se pierde el valor fundamental de control de acceso
   - La promesa de "permitir que nuevas personas accedan" no se cumple

10. **Refleja el flujo completo del prototipo diseñado:** Las Imágenes 15-17 muestran específicamente este flujo completo:
    - Imagen 15: Modal vacío listo para ingresar datos
    - Imagen 16: Modal con datos completos listos para guardar
    - Imagen 17: Confirmación de éxito y usuario creado visible en tabla

Los demás escenarios son importantes para robustez (validaciones de campos, unicidad) y casos alternativos (cancelación), pero el Escenario 2 es el que garantiza que el sistema cumple su promesa fundamental: **permitir al Administrador registrar completamente un nuevo usuario con todos sus datos, roles y permisos para que efectivamente pueda acceder a la plataforma, que es el valor central y la razón de ser de esta funcionalidad crítica de gestión de acceso**.