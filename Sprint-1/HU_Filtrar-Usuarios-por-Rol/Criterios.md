# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 14 del prototipo):**

1. **C1:** Existen usuarios registrados en el sistema con roles asignados
2. **C2:** El dropdown "Todos los Roles" está en su estado por defecto (sin filtro aplicado)
3. **C3:** Se selecciona un rol específico del dropdown "Todos los Roles"
4. **C4:** Existen usuarios con el rol seleccionado en la base de datos
5. **C5:** Hay otros filtros activos simultáneamente (ej: filtro de estado "Todos los Estados")
6. **C6:** Hay texto ingresado en el campo de búsqueda "Buscar usuario..."

### **Acciones del Sistema (observadas en Imagen 14):**

1. **A1:** Mostrar dropdown "Todos los Roles" con opciones disponibles de roles del sistema
2. **A2:** Desplegar lista de roles al hacer clic: "Administrador", "Coordinador de Carrera", "Cómite Evaluación Interna (CEI)", "Autoridad Académica", "Profesor"
3. **A3:** Actualizar el valor del dropdown con el rol seleccionado
4. **A4:** Filtrar la tabla automáticamente sin recargar la página
5. **A5:** Mostrar únicamente las filas de usuarios que tienen el rol seleccionado asignado
6. **A6:** Ocultar todas las filas de usuarios que no tienen el rol seleccionado
7. **A7:** Mantener visible la estructura completa de la tabla con columnas: "Email", "Nombre", "Rol", "Estado", "Acciones"
8. **A8:** Preservar las etiquetas de estado coloreadas (verde "Activo", rojo "Inactivo")
9. **A9:** Mantener visibles los iconos de acciones (editar y eliminar) en las filas mostradas
10. **A10:** Mostrar mensaje o tabla vacía "Sin resultados" cuando no hay usuarios con el rol seleccionado
11. **A11:** Actualizar controles de paginación según cantidad de resultados filtrados
12. **A12:** Aplicar filtro de rol en combinación con otros filtros activos (estado, búsqueda)

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen usuarios con roles asignados
- **C2:** Se selecciona un rol específico del dropdown
- **C3:** Hay usuarios con el rol seleccionado
- **C4:** Hay otros filtros activos simultáneamente

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Usuarios existen | C2: Rol seleccionado | C3: Usuarios con ese rol | C4: Otros filtros activos | Acción |
|-------|---------------------|---------------------|-------------------------|--------------------------|---------|
| R1 | N | N | N | N | A1: Mostrar dropdown sin datos para filtrar |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber usuarios con rol si no hay usuarios) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A10: Mostrar tabla vacía |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A7: Mostrar todos los usuarios sin filtro de rol |
| R10 | S | N | - | S | A7, A12: Mostrar usuarios según otros filtros activos |
| R11 | S | S | N | N | A3, A4, A10: Mostrar mensaje "Sin resultados" |
| R12 | S | S | N | S | A3, A4, A10, A12: Sin resultados considerando múltiples filtros |
| R13 | S | S | S | N | A3, A4, A5, A6, A7, A8, A9, A11: Filtrar y mostrar usuarios |
| R14 | S | S | S | S | A3, A4, A5, A6, A7, A8, A9, A11, A12: Filtrar combinando múltiples criterios |

---

## **Tabla de Decisión Minimizada**

| Regla | Usuarios existen | Rol seleccionado | Usuarios con ese rol | Otros filtros | Acción |
|-------|-----------------|------------------|---------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar dropdown pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todos los usuarios sin filtro de rol |
| **R3** | S | N | - | S | Mostrar usuarios según otros filtros, sin aplicar filtro de rol |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para el rol seleccionado" |
| **R5** | S | S | S | N | Filtrar y mostrar solo usuarios con el rol seleccionado |
| **R6** | S | S | S | S | Filtrar por rol Y combinar con otros filtros activos |

**Justificación de la minimización:**
- **R1:** Si no hay usuarios, el filtro no tiene datos sobre los cuales operar (fusiona R1, R5)
- **R2:** Estado inicial sin filtro de rol aplicado, sin otros filtros (R9)
- **R3:** Estado sin filtro de rol pero con otros filtros activos (R10)
- **R4:** Filtro aplicado pero sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: filtrar solo por rol (R13)
- **R6:** Caso avanzado: filtrar por rol en combinación con otros criterios (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de filtrado)
- 2 escenarios adicionales específicos observados en el prototipo:
  - Interacción con el dropdown (desplegar opciones)
  - Cambio dinámico de filtro (quitar filtro para volver a ver todos)

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder y desplegar opciones del filtro de roles**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios",  
**cuando** ubico el dropdown "Todos los Roles" en la sección de filtros superior,  
**entonces** se muestra el dropdown con el texto por defecto "Todos los Roles" **Y** el dropdown está habilitado para interacción,  
**cuando** hago clic en el dropdown "Todos los Roles",  
**entonces** se despliega una lista con las opciones de roles disponibles en el sistema **Y** la lista incluye las opciones: "Administrador", "Coordinador de Carrera", "Cómite Evaluación Interna (CEI)", "Autoridad Académica", "Profesor" **Y** todas las opciones son claramente legibles **Y** puedo seleccionar cualquier opción de la lista.

---

**Escenario 2 – Filtrar usuarios por rol "Administrador"**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados con diferentes roles asignados **Y** el dropdown "Todos los Roles" está en su estado por defecto,  
**cuando** hago clic en el dropdown "Todos los Roles" **Y** selecciono la opción "Administrador" de la lista,  
**entonces** el dropdown se actualiza mostrando "Administrador" como valor seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las filas de usuarios que tienen el rol "Administrador" asignado **Y** se ocultan todas las filas de usuarios que no tienen el rol "Administrador" **Y** en la columna "Rol" de las filas mostradas aparece "Administrador" **Y** se mantienen visibles todas las columnas: "Email", "Nombre", "Rol", "Estado", "Acciones" **Y** se conservan las etiquetas de estado coloreadas (verde "Activo", rojo "Inactivo") **Y** se mantienen visibles los iconos de editar (lápiz) y eliminar (papelera) en la columna "Acciones" **Y** los controles de paginación se actualizan según la cantidad de usuarios con rol "Administrador".

---

**Escenario 3 – Filtrar usuarios por rol "Coordinador de Carrera"**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios con el rol "Coordinador de Carrera" asignado,  
**cuando** selecciono "Coordinador de Carrera" del dropdown "Todos los Roles",  
**entonces** se muestran únicamente los usuarios que tienen "Coordinador de Carrera" como uno de sus roles asignados **Y** se incluyen usuarios con rol único "Coordinador de Carrera" **Y** se incluyen usuarios con roles múltiples que contienen "Coordinador de Carrera" (ej: "Coordinador de Carrera/Profesor") **Y** se excluyen todos los usuarios que no tienen "Coordinador de Carrera" en sus roles **Y** la respuesta visual es inmediata al cambio de filtro.

---

**Escenario 4 – Mostrar mensaje cuando no hay usuarios con el rol seleccionado**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados en el sistema,  
**cuando** selecciono un rol específico del dropdown "Todos los Roles" (ej: "Autoridad Académica") **Y** no existen usuarios con ese rol asignado en la base de datos,  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron usuarios con el rol seleccionado" o "Sin resultados" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el dropdown "Todos los Roles" conserva el valor seleccionado ("Autoridad Académica") **Y** los demás controles de filtrado permanecen disponibles para modificar los criterios **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 5 – Combinar filtro de rol con filtro de estado**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios con diversos roles y estados,  
**cuando** selecciono un rol específico del dropdown "Todos los Roles" (ej: "Profesor") **Y** selecciono un estado del dropdown "Todos los Estados" (ej: "Activo"),  
**entonces** la tabla muestra únicamente los usuarios que cumplen ambas condiciones simultáneamente **Y** se presentan solo usuarios con rol "Profesor" Y estado "Activo" (etiqueta verde) **Y** se excluyen los usuarios con rol "Profesor" pero estado "Inactivo" **Y** se excluyen los usuarios con estado "Activo" pero sin el rol "Profesor" **Y** ambos dropdowns reflejan los filtros seleccionados **Y** la tabla se actualiza sin recargar la página.

---

**Escenario 6 – Combinar filtro de rol con búsqueda por texto**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he seleccionado un rol del dropdown "Todos los Roles" (ej: "CEI"),  
**cuando** ingreso texto en el campo de búsqueda "Buscar usuario..." (ej: "juan"),  
**entonces** la tabla muestra únicamente los usuarios que tienen el rol "CEI" asignado Y cuyo email, nombre o información coincide con "juan" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** se excluyen los usuarios con rol "CEI" que no coinciden con la búsqueda **Y** se excluyen los usuarios que coinciden con la búsqueda pero no tienen rol "CEI" **Y** el filtrado es dinámico mientras escribo en el campo de búsqueda.

---

**Escenario 7 – Quitar filtro de rol para visualizar todos los usuarios**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** tengo un rol específico seleccionado en el dropdown "Todos los Roles" (ej: "Administrador") **Y** la tabla muestra usuarios filtrados por ese rol,  
**cuando** hago clic en el dropdown "Todos los Roles" **Y** selecciono nuevamente la opción "Todos los Roles",  
**entonces** el dropdown se actualiza mostrando "Todos los Roles" **Y** el filtro de rol se elimina **Y** la tabla se actualiza automáticamente mostrando todos los usuarios registrados sin filtro de rol **Y** se restablecen las filas originales con todos los usuarios **Y** se mantienen activos cualquier otro filtro que esté aplicado (estado, búsqueda) **Y** los controles de paginación se actualizan según el total de usuarios sin filtrar.

---

**Escenario 8 – Cambiar dinámicamente entre diferentes filtros de rol**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** tengo aplicado un filtro de rol (ej: "Coordinador de Carrera"),  
**cuando** cambio la selección del dropdown "Todos los Roles" a un rol diferente (ej: "Profesor"),  
**entonces** el dropdown se actualiza inmediatamente con "Profesor" **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se ocultan los usuarios con rol "Coordinador de Carrera" **Y** se muestran los usuarios con rol "Profesor" **Y** la transición entre filtros es fluida e inmediata **Y** no se requiere hacer clic en ningún botón adicional para aplicar el cambio **Y** se mantiene la consistencia visual de la tabla durante el cambio.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Filtrar usuarios por rol "Administrador"**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece explícitamente que el Administrador quiere "filtrar usuarios por rol para organizar la visualización y gestionar permisos por rol". El Escenario 2 valida directamente esta capacidad fundamental de filtrado por un rol específico.

2. **Representa el "happy path" principal:** Es el caso de uso más común y esencial. Demuestra que el mecanismo básico de filtrado funciona correctamente: seleccionar un rol → obtener solo usuarios con ese rol. Sin esta funcionalidad operando, los casos avanzados (combinación de filtros, roles múltiples) carecen de fundamento.

3. **Valida comportamiento completo del filtro:** Verifica todos los aspectos críticos del filtrado:
   - Interacción correcta con el dropdown
   - Actualización automática sin recarga de página
   - Visualización exclusiva de usuarios filtrados
   - Ocultación de usuarios no coincidentes
   - Preservación de la estructura visual de la tabla
   - Mantenimiento de funcionalidades adicionales (etiquetas de estado, iconos de acción)

4. **Habilita la gestión de permisos por rol:** Solo con un filtrado efectivo por rol, el Administrador puede:
   - Organizar visualmente a los usuarios según sus responsabilidades
   - Identificar rápidamente todos los usuarios con un rol específico
   - Gestionar permisos de manera eficiente (por ejemplo, revisar todos los Administradores)
   - Tomar decisiones sobre asignación o revocación de roles

5. **Fundamento para escenarios avanzados:** Los escenarios de combinación de filtros (5, 6), cambio dinámico (8), y gestión de roles múltiples (3) son extensiones de esta funcionalidad base. Si el filtrado simple por rol falla, las capacidades avanzadas no tienen sentido.

6. **Refleja fielmente el prototipo:** El escenario captura con precisión la interacción completa observada en la Imagen 14, incluyendo el dropdown, la actualización de la tabla, y la preservación de todos los elementos visuales.

7. **Impacto directo en el valor de negocio:** La capacidad de filtrar por rol es esencial para:
   - Auditorías de seguridad (¿quiénes son todos los Administradores?)
   - Gestión de acceso (¿qué usuarios tienen permisos específicos?)
   - Organización administrativa (agrupar usuarios por función)

Los demás escenarios complementan y refinan esta funcionalidad (combinación de filtros, manejo de casos sin resultados, cambio dinámico), pero el Escenario 2 es el que garantiza que el sistema cumple su propósito esencial: **permitir al Administrador filtrar efectivamente por rol para organizar la visualización y gestionar permisos, que es exactamente el valor declarado en la Historia de Usuario**.