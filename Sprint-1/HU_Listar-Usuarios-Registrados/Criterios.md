# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imágenes del prototipo):**

1. **C1:** Existen usuarios registrados en el sistema
2. **C2:** Se aplica filtro en dropdown "Todos los Roles" (valor diferente a "Todos los Roles")
3. **C3:** Se aplica filtro en dropdown "Todos los Estados" (valor diferente a "Todos los Estados")
4. **C4:** Se ingresa texto en el campo de búsqueda "Buscar usuario..."
5. **C5:** Los filtros/búsqueda aplicados tienen resultados coincidentes
6. **C6:** Se navega a una página diferente usando la paginación

### **Acciones del Sistema (observadas en las imágenes):**

1. **A1:** Mostrar tabla "Gestión de Usuarios" con columnas: "Email", "Nombre", "Rol", "Estado", "Acciones"
2. **A2:** Mostrar todos los usuarios registrados en filas de la tabla
3. **A3:** Mostrar información completa por usuario: email, nombre completo, rol(es) asignado(s), estado con etiqueta coloreada
4. **A4:** Mostrar etiquetas de estado: "Activo" (verde) o "Inactivo" (rojo)
5. **A5:** Mostrar iconos de acciones en la columna "Acciones": icono de editar (lápiz) e icono de eliminar (papelera)
6. **A6:** Filtrar y mostrar únicamente usuarios que coincidan con el rol seleccionado
7. **A7:** Filtrar y mostrar únicamente usuarios que coincidan con el estado seleccionado
8. **A8:** Filtrar y mostrar únicamente usuarios que coincidan con el texto de búsqueda
9. **A9:** Mostrar mensaje o tabla vacía cuando no hay resultados
10. **A10:** Mostrar controles de paginación: "< Previous 1 2 3 Next >"
11. **A11:** Actualizar contenido de la tabla según la página seleccionada
12. **A12:** Habilitar botón "+ Nuevo Usuario" en esquina superior derecha

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes para la funcionalidad de listar:

**Condiciones simplificadas:**
- **C1:** Existen usuarios en el sistema
- **C2:** Se aplican filtros (Rol y/o Estado)
- **C3:** Se ingresa búsqueda por texto
- **C4:** Hay resultados que coinciden con filtros/búsqueda

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Usuarios existen | C2: Filtros aplicados | C3: Búsqueda aplicada | C4: Hay coincidencias | Acción |
|-------|---------------------|----------------------|----------------------|---------------------|---------|
| R1 | N | N | N | N | A9: Mostrar tabla vacía o mensaje "No hay usuarios" |
| R2 | N | N | N | S | Imposible (no puede haber coincidencias sin usuarios) |
| R3 | N | N | S | N | A9: Mostrar mensaje "Sin resultados" |
| R4 | N | N | S | S | Imposible (no puede haber coincidencias sin usuarios) |
| R5 | N | S | N | N | A9: Mostrar tabla vacía o mensaje "No hay usuarios" |
| R6 | N | S | N | S | Imposible (no puede haber coincidencias sin usuarios) |
| R7 | N | S | S | N | A9: Mostrar mensaje "Sin resultados" |
| R8 | N | S | S | S | Imposible (no puede haber coincidencias sin usuarios) |
| R9 | S | N | N | N | Imposible (si hay usuarios, debe haber coincidencias) |
| R10 | S | N | N | S | A1, A2, A3, A4, A5, A10, A12: Mostrar todos los usuarios |
| R11 | S | N | S | N | A9: Mostrar mensaje "Sin resultados para la búsqueda" |
| R12 | S | N | S | S | A1, A3, A4, A5, A8, A10: Mostrar usuarios filtrados por búsqueda |
| R13 | S | S | N | N | A9: Mostrar mensaje "Sin resultados para los filtros" |
| R14 | S | S | N | S | A1, A3, A4, A5, A6/A7, A10: Mostrar usuarios filtrados |
| R15 | S | S | S | N | A9: Mostrar mensaje "Sin resultados" |
| R16 | S | S | S | S | A1, A3, A4, A5, A6/A7, A8, A10: Mostrar usuarios con filtros y búsqueda |

---

## **Tabla de Decisión Minimizada**

Después de eliminar reglas imposibles y fusionar reglas redundantes:

| Regla | Usuarios existen | Filtros/Búsqueda aplicados | Hay coincidencias | Acción |
|-------|-----------------|---------------------------|-------------------|---------|
| **R1** | N | - | - | Mostrar tabla vacía o mensaje "No hay usuarios registrados" |
| **R2** | S | N | S | Mostrar lista completa de todos los usuarios con paginación |
| **R3** | S | S | N | Mostrar mensaje "Sin resultados para los criterios aplicados" |
| **R4** | S | S | S | Mostrar lista filtrada de usuarios que coinciden |

**Justificación de la minimización:**
- **R1:** Si no hay usuarios, los filtros y búsquedas son irrelevantes (fusiona R1, R3, R5, R7)
- **R2:** Representa el caso estándar sin filtros donde se muestran todos los usuarios (R10)
- **R3:** Cualquier combinación de filtros/búsqueda sin resultados produce el mismo comportamiento (fusiona R11, R13, R15)
- **R4:** Cualquier combinación de filtros/búsqueda con resultados muestra la lista filtrada (fusiona R12, R14, R16)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 10 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios de listado)
- 6 escenarios adicionales para validar funcionalidades específicas observadas en el prototipo:
  - Filtrado por rol específico
  - Filtrado por estado específico
  - Combinación de filtros múltiples
  - Búsqueda por texto en campos
  - Navegación por paginación
  - Interacción con controles de UI (visualización de estados, acciones disponibles)

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Visualizar lista completa de usuarios registrados**

**Dado que** estoy autenticado como Administrador en el sistema **Y** existen usuarios registrados en la base de datos,  
**cuando** accedo a la sección "Usuarios" desde el menú lateral **O** navego directamente a "Gestión de Usuarios",  
**entonces** se muestra la pantalla "Gestión de Usuarios" con el título visible en la parte superior **Y** se presenta una tabla con cinco columnas: "Email", "Nombre", "Rol", "Estado", "Acciones" **Y** se muestran todos los usuarios registrados en filas de la tabla **Y** cada fila contiene el correo institucional del usuario en la columna "Email" **Y** cada fila contiene el nombre completo del usuario en la columna "Nombre" **Y** cada fila muestra el rol o roles asignados en la columna "Rol" (ej: "Administrador", "Coordinador de Carrera/Profesor", "CEI/Profesor") **Y** cada fila muestra el estado del usuario con una etiqueta coloreada en la columna "Estado": etiqueta verde con texto "Activo" para usuarios activos, etiqueta roja con texto "Inactivo" para usuarios inactivos **Y** cada fila contiene dos iconos en la columna "Acciones": icono de lápiz para editar e icono de papelera para eliminar **Y** se muestra el campo de búsqueda con placeholder "Buscar usuario..." en la parte superior **Y** se muestran dos dropdowns de filtro: "Todos los Roles" y "Todos los Estados" **Y** se muestra el botón "+ Nuevo Usuario" en la esquina superior derecha **Y** se presentan controles de paginación en la parte inferior con formato "< Previous 1 2 3 Next >".

---

**Escenario 2 – Visualizar tabla vacía cuando no hay usuarios registrados**

**Dado que** estoy autenticado como Administrador en el sistema **Y** no existen usuarios registrados en la base de datos,  
**cuando** accedo a la sección "Gestión de Usuarios",  
**entonces** se muestra la pantalla "Gestión de Usuarios" con todos los elementos de UI (campo de búsqueda, filtros, botón "+ Nuevo Usuario") **Y** se presenta la tabla con las cinco columnas: "Email", "Nombre", "Rol", "Estado", "Acciones" **Y** no se muestran filas de datos en la tabla **Y** se presenta un mensaje indicativo "No hay usuarios registrados" o la tabla aparece vacía **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 3 – Filtrar usuarios por rol específico**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados con diferentes roles,  
**cuando** hago clic en el dropdown "Todos los Roles",  
**entonces** se despliega una lista con las opciones de roles disponibles (ej: "Administrador", "Coordinador de Carrera", "CEI", "Profesor", "Autoridad Académica") **Y** puedo seleccionar un rol específico de la lista,  
**cuando** selecciono un rol específico (ej: "Administrador"),  
**entonces** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente los usuarios que tienen el rol "Administrador" asignado **Y** se ocultan todos los usuarios que no tienen ese rol **Y** el dropdown "Todos los Roles" se actualiza mostrando el rol seleccionado **Y** se mantienen visibles todos los demás controles de la interfaz.

---

**Escenario 4 – Filtrar usuarios por estado específico**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios con diferentes estados (Activo e Inactivo),  
**cuando** hago clic en el dropdown "Todos los Estados",  
**entonces** se despliega una lista con las opciones "Activo" e "Inactivo" **Y** puedo seleccionar un estado específico,  
**cuando** selecciono "Activo",  
**entonces** la tabla se actualiza automáticamente **Y** se muestran únicamente los usuarios con etiqueta verde "Activo" **Y** se ocultan todos los usuarios con estado "Inactivo" **Y** el dropdown se actualiza mostrando "Activo" **Y** la respuesta visual es inmediata al cambio de filtro.

---

**Escenario 5 – Aplicar múltiples filtros simultáneamente**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados,  
**cuando** selecciono un rol específico del dropdown "Todos los Roles" (ej: "Coordinador de Carrera") **Y** selecciono un estado del dropdown "Todos los Estados" (ej: "Activo"),  
**entonces** la tabla muestra únicamente los usuarios que cumplen ambas condiciones simultáneamente **Y** se presentan solo usuarios con rol "Coordinador de Carrera" Y estado "Activo" **Y** se excluyen todos los usuarios que no cumplan ambos criterios **Y** ambos dropdowns reflejan los filtros seleccionados **Y** la tabla se actualiza sin recargar la página.

---

**Escenario 6 – Buscar usuarios por texto**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen múltiples usuarios registrados,  
**cuando** ingreso texto en el campo de búsqueda "Buscar usuario..." (ej: "juan.perez"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestran únicamente los usuarios cuyo email, nombre o rol contienen el texto ingresado **Y** se ocultan todos los usuarios que no coinciden con el criterio de búsqueda **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** la búsqueda es case-insensitive (no distingue mayúsculas de minúsculas).

---

**Escenario 7 – Mostrar mensaje cuando no hay resultados de filtrado o búsqueda**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados en el sistema,  
**cuando** aplico un filtro de rol o estado **O** ingreso un término de búsqueda **Y** ningún usuario coincide con los criterios aplicados,  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron resultados" o "Sin resultados para los criterios aplicados" **Y** se mantienen visibles los controles de filtrado y búsqueda con los valores aplicados **Y** puedo modificar o limpiar los filtros para obtener nuevos resultados **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 8 – Navegar entre páginas de usuarios**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen más usuarios de los que se pueden mostrar en una página,  
**cuando** reviso los controles de paginación en la parte inferior,  
**entonces** se muestran los controles "< Previous", números de página (ej: "1 2 3"), y "Next >" **Y** la página actual está resaltada o marcada visualmente **Y** el botón "< Previous" está deshabilitado cuando estoy en la primera página,  
**cuando** hago clic en un número de página específico (ej: "2") **O** hago clic en "Next >",  
**entonces** la tabla se actualiza mostrando los usuarios correspondientes a esa página **Y** el número de página seleccionado se resalta **Y** se mantienen aplicados los filtros y búsquedas activos **Y** la transición es fluida sin recargar toda la página.

---

**Escenario 9 – Visualizar roles múltiples asignados a un usuario**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** un usuario tiene múltiples roles asignados,  
**cuando** visualizo la lista de usuarios en la tabla,  
**entonces** en la columna "Rol" se muestran todos los roles asignados al usuario separados por "/" (ej: "Coordinador de Carrera/Profesor", "CEI/Profesor", "Autoridad/Profesor") **Y** todos los roles son claramente legibles en la celda **Y** no se trunca la información de roles múltiples **Y** cada usuario muestra la combinación exacta de roles que tiene asignados.

---

**Escenario 10 – Limpiar filtros y búsqueda para ver lista completa**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** tengo filtros aplicados en "Todos los Roles" y/o "Todos los Estados" **Y** tengo texto ingresado en el campo de búsqueda,  
**cuando** cambio el dropdown "Todos los Roles" de vuelta a "Todos los Roles" **Y** cambio el dropdown "Todos los Estados" de vuelta a "Todos los Estados" **Y** borro el texto del campo de búsqueda,  
**entonces** la tabla se actualiza mostrando nuevamente todos los usuarios registrados sin filtros **Y** se restablece la vista completa con paginación según corresponda **Y** todos los controles vuelven a su estado inicial **Y** la tabla presenta la misma información que al acceder inicialmente a "Gestión de Usuarios".

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 1 – Visualizar lista completa de usuarios registrados**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones:

1. **Valida el propósito fundamental de la HU:** La Historia de Usuario establece que el Administrador quiere "listar los usuarios registrados para gestionar el acceso basado en roles". El Escenario 1 valida directamente este objetivo principal al verificar que efectivamente se puede visualizar la lista completa de usuarios con toda su información relevante.

2. **Representa el "happy path" principal:** Es el caso de uso más común y fundamental. Sin esta funcionalidad básica operando correctamente, ninguna de las capacidades avanzadas (filtrado, búsqueda, paginación) tiene sentido o valor.

3. **Valida la completitud de la información:** Verifica que se muestren todos los datos críticos para la gestión de acceso basado en roles:
   - Email institucional (identificador único)
   - Nombre completo (identificación del usuario)
   - Rol(es) asignado(s) (esencial para la gestión de acceso)
   - Estado activo/inactivo (control de acceso actual)
   - Acciones disponibles (editar/eliminar para gestión)

4. **Fundamento para todos los demás escenarios:** Los escenarios de filtrado (2-7), búsqueda (6), y paginación (8) son refinamientos o extensiones de esta funcionalidad base. Si el listado básico falla, todas las demás capacidades carecen de fundamento.

5. **Refleja fielmente el prototipo:** El escenario captura con precisión todos los elementos visuales críticos observados en la Imagen 14, incluyendo la estructura de la tabla, las etiquetas coloreadas de estado, los iconos de acción, y todos los controles de la interfaz.

6. **Habilita la gestión de acceso:** Solo con una lista completa y precisa de usuarios con sus roles y estados, el Administrador puede tomar decisiones informadas sobre la gestión de acceso, que es el valor de negocio declarado en la HU.

Los demás escenarios son importantes para la usabilidad y eficiencia del sistema (filtrado, búsqueda, paginación), pero el Escenario 1 es el que garantiza que el sistema cumple su propósito esencial: **proporcionar al Administrador visibilidad completa de todos los usuarios registrados y sus roles para gestionar efectivamente el acceso al sistema**.