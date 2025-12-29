# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imágenes 14 y 17 del prototipo):**

1. **C1:** El usuario seleccionado existe en el sistema
2. **C2:** El estado actual del usuario es "Activo" (etiqueta verde)
3. **C3:** El estado actual del usuario es "Inactivo" (etiqueta rojo)
4. **C4:** El Administrador confirma la acción de cambio de estado
5. **C5:** El Administrador cancela la acción de cambio de estado
6. **C6:** El usuario tiene sesiones activas en el sistema

### **Acciones del Sistema (observadas en Imágenes 14 y 17):**

1. **A1:** Identificar el estado actual del usuario en la columna "Estado" (etiqueta verde "Activo" o roja "Inactivo")
2. **A2:** Habilitar interacción con iconos de acción (lápiz de editar)
3. **A3:** Mostrar modal o diálogo de confirmación de cambio de estado
4. **A4:** Presentar información del usuario (nombre, email, rol) en el modal
5. **A5:** Mostrar el estado actual y el estado objetivo del cambio
6. **A6:** Cambiar el estado de "Activo" a "Inactivo"
7. **A7:** Actualizar la etiqueta en la tabla de verde "Activo" a rojo "Inactivo"
8. **A8:** Cambiar el estado de "Inactivo" a "Activo"
9. **A9:** Actualizar la etiqueta en la tabla de rojo "Inactivo" a verde "Activo"
10. **A10:** Revocar sesiones activas del usuario al desactivar
11. **A11:** Mostrar mensaje de confirmación de éxito del cambio
12. **A12:** Cancelar operación y mantener estado original
13. **A13:** Actualizar la tabla sin recargar la página completa
14. **A14:** Registrar el cambio en log de auditoría del sistema

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Usuario existe en el sistema
- **C2:** Estado actual es "Activo"
- **C3:** Administrador confirma el cambio
- **C4:** Usuario tiene sesiones activas

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Usuario existe | C2: Estado es Activo | C3: Confirma cambio | C4: Sesiones activas | Acción |
|-------|-------------------|---------------------|--------------------|--------------------|---------|
| R1 | N | N | N | N | Error: Usuario no encontrado |
| R2 | N | N | N | S | Imposible (no hay usuario) |
| R3 | N | N | S | N | Imposible (no hay usuario) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | Imposible (no hay usuario) |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | N | - | A12: Cancelar, mantener estado Inactivo |
| R10 | S | N | S | - | A8, A9, A11, A13: Activar usuario (Inactivo→Activo) |
| R11 | S | S | N | - | A12: Cancelar, mantener estado Activo |
| R12 | S | S | S | N | A6, A7, A11, A13: Desactivar usuario (Activo→Inactivo) |
| R13 | S | S | S | S | A6, A7, A10, A11, A13: Desactivar y cerrar sesiones |

---

## **Tabla de Decisión Minimizada**

| Regla | Usuario existe | Estado actual | Confirma cambio | Sesiones activas | Acción |
|-------|---------------|---------------|----------------|------------------|---------|
| **R1** | N | - | - | - | Mostrar error "Usuario no encontrado" |
| **R2** | S | Activo | N | - | Cancelar, mantener estado Activo |
| **R3** | S | Activo | S | N | Desactivar usuario (Activo→Inactivo) |
| **R4** | S | Activo | S | S | Desactivar usuario y cerrar sesiones activas |
| **R5** | S | Inactivo | N | - | Cancelar, mantener estado Inactivo |
| **R6** | S | Inactivo | S | - | Activar usuario (Inactivo→Activo) |

**Justificación de la minimización:**
- **R1:** Si el usuario no existe, las demás condiciones son irrelevantes (fusiona R1-R8)
- **R2:** Usuario activo pero Administrador cancela, no hay cambio (R11)
- **R3:** Usuario activo sin sesiones, se desactiva exitosamente (R12)
- **R4:** Usuario activo con sesiones, se desactiva y se cierran sesiones (R13)
- **R5:** Usuario inactivo pero Administrador cancela, no hay cambio (R9)
- **R6:** Usuario inactivo se activa, las sesiones no son relevantes al activar (R10)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de cambio de estado)
- 2 escenarios adicionales para validar funcionalidades específicas:
  - Acceso a la funcionalidad de cambio de estado desde la interfaz
  - Validación de permisos (solo Administrador puede cambiar estados)

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder a la funcionalidad de cambio de estado**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados en la tabla,  
**cuando** ubico un usuario específico en la tabla **Y** reviso la columna "Estado",  
**entonces** se muestra la etiqueta de estado del usuario: etiqueta verde con texto "Activo" para usuarios activos o etiqueta roja con texto "Inactivo" para usuarios inactivos **Y** se muestran los iconos de acción en la columna "Acciones" **Y** el icono de editar (lápiz) está habilitado para interacción **Y** puedo hacer clic en el icono de editar para gestionar el usuario incluyendo su estado.

---

**Escenario 2 – Desactivar usuario activo sin sesiones activas**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios" **Y** existe un usuario con estado "Activo" (etiqueta verde visible) **Y** el usuario no tiene sesiones activas en el sistema,  
**cuando** hago clic en el icono de editar (lápiz) del usuario **O** accedo a la opción de cambiar estado,  
**entonces** se muestra un modal o diálogo de confirmación **Y** se presenta la información del usuario: nombre completo, email, rol actual **Y** se muestra el estado actual "Activo" y el estado objetivo "Inactivo" **Y** se presenta el mensaje de confirmación "¿Está seguro que desea desactivar el acceso de este usuario?" **Y** se muestran dos botones: "Cancelar" y "Desactivar" o "Confirmar",  
**cuando** hago clic en el botón "Desactivar" o "Confirmar",  
**entonces** se actualiza el estado del usuario de "Activo" a "Inactivo" en la base de datos **Y** la etiqueta en la tabla cambia de verde "Activo" a roja "Inactivo" **Y** se cierra el modal de confirmación **Y** la tabla se actualiza automáticamente sin recargar la página completa **Y** se muestra un mensaje de éxito "El usuario ha sido desactivado exitosamente" o "Estado actualizado correctamente" **Y** el usuario ya no puede iniciar sesión en el sistema **Y** se registra el cambio en el log de auditoría del sistema.

---

**Escenario 3 – Desactivar usuario activo con sesiones activas**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios" **Y** existe un usuario con estado "Activo" (etiqueta verde) **Y** el usuario tiene una o más sesiones activas en el sistema,  
**cuando** accedo a la funcionalidad de cambiar estado del usuario **Y** se muestra el modal de confirmación,  
**entonces** se presenta un mensaje adicional advirtiendo "El usuario tiene sesiones activas. Al desactivarlo, todas sus sesiones serán cerradas inmediatamente" **Y** se muestran los botones "Cancelar" y "Desactivar",  
**cuando** hago clic en el botón "Desactivar",  
**entonces** se actualiza el estado del usuario de "Activo" a "Inactivo" **Y** se cierran inmediatamente todas las sesiones activas del usuario **Y** el usuario es deslogueado de todos sus dispositivos activos **Y** la etiqueta en la tabla cambia de verde "Activo" a roja "Inactivo" **Y** se muestra el mensaje de éxito confirmando la desactivación **Y** el usuario no puede iniciar sesión hasta ser reactivado **Y** se registra el cambio y el cierre de sesiones en el log de auditoría.

---

**Escenario 4 – Activar usuario inactivo**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios" **Y** existe un usuario con estado "Inactivo" (etiqueta roja visible),  
**cuando** hago clic en el icono de editar del usuario **O** accedo a la opción de cambiar estado,  
**entonces** se muestra un modal o diálogo de confirmación **Y** se presenta la información del usuario: nombre completo, email, rol actual **Y** se muestra el estado actual "Inactivo" y el estado objetivo "Activo" **Y** se presenta el mensaje de confirmación "¿Está seguro que desea activar el acceso de este usuario?" **Y** se muestran dos botones: "Cancelar" y "Activar" o "Confirmar",  
**cuando** hago clic en el botón "Activar" o "Confirmar",  
**entonces** se actualiza el estado del usuario de "Inactivo" a "Activo" en la base de datos **Y** la etiqueta en la tabla cambia de roja "Inactivo" a verde "Activo" **Y** se cierra el modal de confirmación **Y** la tabla se actualiza automáticamente sin recargar la página completa **Y** se muestra un mensaje de éxito "El usuario ha sido activado exitosamente" o "Estado actualizado correctamente" **Y** el usuario puede iniciar sesión nuevamente en el sistema **Y** se registra el cambio en el log de auditoría del sistema.

---

**Escenario 5 – Cancelar cambio de estado de usuario activo**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he iniciado el proceso de cambiar el estado de un usuario activo (etiqueta verde "Activo") **Y** se muestra el modal de confirmación,  
**cuando** hago clic en el botón "Cancelar" **O** cierro el modal sin confirmar,  
**entonces** se cierra el modal de confirmación **Y** no se realiza ningún cambio en el estado del usuario **Y** la etiqueta permanece verde "Activo" en la tabla **Y** el usuario mantiene su capacidad de acceso al sistema **Y** no se registra ningún cambio en el log de auditoría **Y** regreso a la vista normal de "Gestión de Usuarios".

---

**Escenario 6 – Cancelar cambio de estado de usuario inactivo**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he iniciado el proceso de cambiar el estado de un usuario inactivo (etiqueta roja "Inactivo") **Y** se muestra el modal de confirmación,  
**cuando** hago clic en el botón "Cancelar" **O** cierro el modal sin confirmar,  
**entonces** se cierra el modal de confirmación **Y** no se realiza ningún cambio en el estado del usuario **Y** la etiqueta permanece roja "Inactivo" en la tabla **Y** el usuario mantiene su estado de acceso bloqueado al sistema **Y** no se registra ningún cambio en el log de auditoría **Y** regreso a la vista normal de "Gestión de Usuarios".

---

**Escenario 7 – Intentar cambiar estado de usuario inexistente**

**Dado que** estoy autenticado como Administrador en el sistema,  
**cuando** intento cambiar el estado de un usuario que ha sido eliminado de la base de datos **O** intento acceder a un ID de usuario que no existe,  
**entonces** se muestra un mensaje de error "El usuario no fue encontrado" o "Usuario no existe" **Y** no se ejecuta ninguna acción de cambio de estado **Y** se mantiene la integridad de la tabla de usuarios **Y** puedo regresar a la lista de usuarios sin errores **Y** se registra el intento fallido en el log del sistema.

---

**Escenario 8 – Validar permisos de Administrador para cambiar estados**

**Dado que** estoy autenticado en el sistema con un rol diferente a Administrador (ej: Coordinador, Profesor, CEI),  
**cuando** accedo a una funcionalidad que intenta cambiar el estado de un usuario **O** intento ejecutar una acción de activar/desactivar usuario,  
**entonces** el sistema valida mis permisos **Y** se muestra un mensaje de error "No tiene permisos para realizar esta acción" o "Acceso denegado" **Y** no se ejecuta el cambio de estado **Y** el estado del usuario permanece sin modificaciones **Y** se registra el intento de acción no autorizada en el log de seguridad **Y** solo los usuarios con rol "Administrador" pueden cambiar estados de usuarios.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Desactivar usuario activo sin sesiones activas**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Administrador quiere "habilitar o deshabilitar el acceso de un usuario para controlar quién puede usar el sistema". El Escenario 2 valida directamente la funcionalidad principal de **desactivar acceso**, que es el caso de uso de control de seguridad más frecuente y crítico.

2. **Representa el "happy path" de control de acceso:** Es el escenario más común en la gestión de seguridad del sistema:
   - Empleados que dejan la organización
   - Usuarios temporales cuyo acceso debe ser revocado
   - Cuentas sospechosas que requieren suspensión inmediata
   - Usuarios que incumplen políticas de uso

3. **Impacto directo en seguridad del sistema:** La desactivación de usuarios es crítica para:
   - **Prevenir accesos no autorizados:** Revocar inmediatamente el acceso de usuarios que no deberían tener permisos
   - **Cumplimiento de seguridad:** Asegurar que solo personal autorizado actual puede acceder
   - **Gestión de riesgos:** Mitigar riesgos de seguridad al bloquear cuentas comprometidas o sospechosas
   - **Auditoría y compliance:** Demostrar control sobre quién tiene acceso al sistema

4. **Valida el flujo completo de desactivación:** Verifica todos los aspectos críticos del proceso:
   - Confirmación explícita del Administrador (previene acciones accidentales)
   - Cambio efectivo de estado en base de datos
   - Actualización visual inmediata (etiqueta verde→roja)
   - Bloqueo real de acceso (usuario no puede iniciar sesión)
   - Registro de auditoría para trazabilidad
   - Actualización de UI sin recarga completa

5. **Mayor frecuencia de uso que la activación:** En la práctica administrativa:
   - Desactivar usuarios es más frecuente que activarlos (escenario 4)
   - La mayoría de cambios de estado son de Activo→Inactivo (empleados que se van, cuentas temporales que expiran)
   - La activación generalmente ocurre una vez (al crear usuario), mientras la desactivación puede ocurrir múltiples veces

6. **Diferenciación del Escenario 3:** Aunque el Escenario 3 (con sesiones activas) es importante, el Escenario 2 representa el caso base más fundamental. El Escenario 3 es una variación que agrega complejidad (cierre de sesiones), pero el Escenario 2 valida el mecanismo esencial de desactivación que debe funcionar correctamente antes de abordar casos con sesiones activas.

7. **Precedencia en implementación:** Sin un mecanismo básico de desactivación funcionando (Escenario 2), el caso con sesiones activas (Escenario 3) no puede implementarse correctamente. El Escenario 2 es el fundamento sobre el cual se construye el 3.

8. **Impacto en gobernanza y cumplimiento:** La capacidad de desactivar usuarios es esencial para:
   - Cumplir con políticas de offboarding de personal
   - Responder a incidentes de seguridad
   - Gestionar contratos temporales o de consultoría
   - Mantener principio de "least privilege" (mínimo privilegio necesario)

Los demás escenarios complementan esta funcionalidad (activación, cancelación, validación de permisos), pero el Escenario 2 es el que garantiza que el sistema cumple su propósito crítico de seguridad declarado en la HU: **permitir al Administrador desactivar efectivamente el acceso de usuarios para controlar quién puede usar el sistema, que es la capacidad fundamental de control de acceso y seguridad**.