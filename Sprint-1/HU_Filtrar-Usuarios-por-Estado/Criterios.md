# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 14 del prototipo):**

1. **C1:** Existen usuarios registrados en el sistema con estados asignados
2. **C2:** El dropdown "Todos los Estados" está en su estado por defecto (sin filtro aplicado)
3. **C3:** Se selecciona un estado específico del dropdown "Todos los Estados"
4. **C4:** Existen usuarios con el estado seleccionado (Activo o Inactivo) en la base de datos
5. **C5:** Hay otros filtros activos simultáneamente (ej: filtro de rol "Todos los Roles")
6. **C6:** Hay texto ingresado en el campo de búsqueda "Buscar usuario..."

### **Acciones del Sistema (observadas en Imagen 14):**

1. **A1:** Mostrar dropdown "Todos los Estados" con opciones disponibles: "Activo" e "Inactivo"
2. **A2:** Desplegar lista de estados al hacer clic en el dropdown
3. **A3:** Actualizar el valor del dropdown con el estado seleccionado
4. **A4:** Filtrar la tabla automáticamente sin recargar la página
5. **A5:** Mostrar únicamente las filas de usuarios con el estado seleccionado
6. **A6:** Ocultar todas las filas de usuarios con estado diferente al seleccionado
7. **A7:** Mantener visible la estructura completa de la tabla con columnas: "Email", "Nombre", "Rol", "Estado", "Acciones"
8. **A8:** Mostrar etiquetas coloreadas de estado correctamente: verde con texto "Activo" para usuarios activos, rojo con texto "Inactivo" para usuarios inactivos
9. **A9:** Mantener visibles los iconos de acciones (editar y eliminar) en las filas mostradas
10. **A10:** Mostrar mensaje o tabla vacía cuando no hay usuarios con el estado seleccionado
11. **A11:** Actualizar controles de paginación según cantidad de resultados filtrados
12. **A12:** Aplicar filtro de estado en combinación con otros filtros activos (rol, búsqueda)

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen usuarios con estados asignados
- **C2:** Se selecciona un estado específico del dropdown
- **C3:** Hay usuarios con el estado seleccionado
- **C4:** Hay otros filtros activos simultáneamente

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Usuarios existen | C2: Estado seleccionado | C3: Usuarios con ese estado | C4: Otros filtros activos | Acción |
|-------|---------------------|------------------------|----------------------------|--------------------------|---------|
| R1 | N | N | N | N | A1: Mostrar dropdown sin datos para filtrar |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber usuarios con estado si no hay usuarios) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A10: Mostrar tabla vacía |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A7: Mostrar todos los usuarios sin filtro de estado |
| R10 | S | N | - | S | A7, A12: Mostrar usuarios según otros filtros activos |
| R11 | S | S | N | N | A3, A4, A10: Mostrar mensaje "Sin resultados" |
| R12 | S | S | N | S | A3, A4, A10, A12: Sin resultados considerando múltiples filtros |
| R13 | S | S | S | N | A3, A4, A5, A6, A7, A8, A9, A11: Filtrar y mostrar usuarios |
| R14 | S | S | S | S | A3, A4, A5, A6, A7, A8, A9, A11, A12: Filtrar combinando múltiples criterios |

---

## **Tabla de Decisión Minimizada**

| Regla | Usuarios existen | Estado seleccionado | Usuarios con ese estado | Otros filtros | Acción |
|-------|-----------------|---------------------|------------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar dropdown pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todos los usuarios sin filtro de estado |
| **R3** | S | N | - | S | Mostrar usuarios según otros filtros, sin aplicar filtro de estado |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para el estado seleccionado" |
| **R5** | S | S | S | N | Filtrar y mostrar solo usuarios con el estado seleccionado |
| **R6** | S | S | S | S | Filtrar por estado Y combinar con otros filtros activos |

**Justificación de la minimización:**
- **R1:** Si no hay usuarios, el filtro no tiene datos sobre los cuales operar (fusiona R1, R5)
- **R2:** Estado inicial sin filtro de estado aplicado, sin otros filtros (R9)
- **R3:** Estado sin filtro de estado pero con otros filtros activos (R10)
- **R4:** Filtro aplicado pero sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: filtrar solo por estado (R13)
- **R6:** Caso avanzado: filtrar por estado en combinación con otros criterios (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de filtrado)
- 2 escenarios adicionales específicos observados en el prototipo:
  - Interacción con el dropdown (desplegar opciones de estado)
  - Cambio dinámico de filtro (alternar entre Activo e Inactivo)

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder y desplegar opciones del filtro de estados**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios",  
**cuando** ubico el dropdown "Todos los Estados" en la sección de filtros superior,  
**entonces** se muestra el dropdown con el texto por defecto "Todos los Estados" **Y** el dropdown está habilitado para interacción **Y** está posicionado junto al dropdown "Todos los Roles",  
**cuando** hago clic en el dropdown "Todos los Estados",  
**entonces** se despliega una lista con dos opciones de estado: "Activo" e "Inactivo" **Y** ambas opciones son claramente legibles **Y** puedo seleccionar cualquiera de las dos opciones.

---

**Escenario 2 – Filtrar usuarios por estado "Activo"**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados con diferentes estados (Activo e Inactivo) **Y** el dropdown "Todos los Estados" está en su estado por defecto,  
**cuando** hago clic en el dropdown "Todos los Estados" **Y** selecciono la opción "Activo" de la lista,  
**entonces** el dropdown se actualiza mostrando "Activo" como valor seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las filas de usuarios que tienen estado "Activo" **Y** se ocultan todas las filas de usuarios con estado "Inactivo" **Y** en la columna "Estado" de las filas mostradas aparece únicamente la etiqueta verde con el texto "Activo" **Y** no se muestra ninguna etiqueta roja con texto "Inactivo" **Y** se mantienen visibles todas las columnas: "Email", "Nombre", "Rol", "Estado", "Acciones" **Y** se conservan los iconos de editar (lápiz) y eliminar (papelera) en la columna "Acciones" **Y** los controles de paginación se actualizan según la cantidad de usuarios activos.

---

**Escenario 3 – Filtrar usuarios por estado "Inactivo"**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios con estado "Inactivo" en el sistema,  
**cuando** hago clic en el dropdown "Todos los Estados" **Y** selecciono la opción "Inactivo" de la lista,  
**entonces** el dropdown se actualiza mostrando "Inactivo" como valor seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las filas de usuarios que tienen estado "Inactivo" **Y** se ocultan todas las filas de usuarios con estado "Activo" **Y** en la columna "Estado" de las filas mostradas aparece únicamente la etiqueta roja con el texto "Inactivo" **Y** no se muestra ninguna etiqueta verde con texto "Activo" **Y** se mantiene la estructura completa de la tabla **Y** la respuesta visual es inmediata al cambio de filtro.

---

**Escenario 4 – Mostrar mensaje cuando no hay usuarios con el estado seleccionado**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados en el sistema,  
**cuando** selecciono un estado específico del dropdown "Todos los Estados" (ej: "Inactivo") **Y** todos los usuarios en la base de datos tienen el estado opuesto (ej: todos son "Activo"),  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron usuarios con el estado seleccionado" o "Sin resultados" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el dropdown "Todos los Estados" conserva el valor seleccionado ("Inactivo") **Y** los demás controles de filtrado permanecen disponibles para modificar los criterios **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 5 – Combinar filtro de estado con filtro de rol**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios con diversos roles y estados,  
**cuando** selecciono un estado específico del dropdown "Todos los Estados" (ej: "Activo") **Y** selecciono un rol del dropdown "Todos los Roles" (ej: "Coordinador de Carrera"),  
**entonces** la tabla muestra únicamente los usuarios que cumplen ambas condiciones simultáneamente **Y** se presentan solo usuarios con estado "Activo" (etiqueta verde) Y rol "Coordinador de Carrera" **Y** se excluyen los usuarios con estado "Activo" pero sin el rol "Coordinador de Carrera" **Y** se excluyen los usuarios con rol "Coordinador de Carrera" pero estado "Inactivo" **Y** ambos dropdowns reflejan los filtros seleccionados **Y** la tabla se actualiza sin recargar la página.

---

**Escenario 6 – Combinar filtro de estado con búsqueda por texto**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he seleccionado un estado del dropdown "Todos los Estados" (ej: "Activo"),  
**cuando** ingreso texto en el campo de búsqueda "Buscar usuario..." (ej: "juan.perez"),  
**entonces** la tabla muestra únicamente los usuarios que tienen estado "Activo" Y cuyo email, nombre o información coincide con "juan.perez" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** se excluyen los usuarios con estado "Activo" que no coinciden con la búsqueda **Y** se excluyen los usuarios que coinciden con la búsqueda pero tienen estado "Inactivo" **Y** solo se muestran usuarios con etiqueta verde "Activo" que cumplen el criterio de búsqueda **Y** el filtrado es dinámico mientras escribo en el campo de búsqueda.

---

**Escenario 7 – Quitar filtro de estado para visualizar todos los usuarios**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** tengo un estado específico seleccionado en el dropdown "Todos los Estados" (ej: "Activo") **Y** la tabla muestra usuarios filtrados por ese estado,  
**cuando** hago clic en el dropdown "Todos los Estados" **Y** selecciono nuevamente la opción "Todos los Estados",  
**entonces** el dropdown se actualiza mostrando "Todos los Estados" **Y** el filtro de estado se elimina **Y** la tabla se actualiza automáticamente mostrando todos los usuarios registrados sin filtro de estado **Y** se muestran filas con usuarios en ambos estados: etiquetas verdes "Activo" y etiquetas rojas "Inactivo" **Y** se restablecen las filas originales con todos los usuarios **Y** se mantienen activos cualquier otro filtro que esté aplicado (rol, búsqueda) **Y** los controles de paginación se actualizan según el total de usuarios sin filtrar.

---

**Escenario 8 – Cambiar dinámicamente entre diferentes estados**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** tengo aplicado un filtro de estado (ej: "Activo") **Y** la tabla muestra usuarios con etiquetas verdes "Activo",  
**cuando** cambio la selección del dropdown "Todos los Estados" al estado opuesto (ej: "Inactivo"),  
**entonces** el dropdown se actualiza inmediatamente con "Inactivo" **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se ocultan todas las filas con etiqueta verde "Activo" **Y** se muestran únicamente las filas con etiqueta roja "Inactivo" **Y** la transición entre filtros es fluida e inmediata **Y** no se requiere hacer clic en ningún botón adicional para aplicar el cambio **Y** se mantiene la consistencia visual de la tabla durante el cambio **Y** todas las etiquetas de estado mostradas tienen el color rojo correspondiente a "Inactivo".

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Filtrar usuarios por estado "Activo"**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Administrador quiere "filtrar usuarios por estado para gestionar el acceso y habilitación/deshabilitación de cuentas". El Escenario 2 valida directamente la capacidad de identificar usuarios con acceso habilitado (Activo), que es el caso de uso principal para la gestión de acceso.

2. **Representa el "happy path" más crítico para seguridad:** Filtrar por usuarios "Activo" es el escenario más frecuente y crítico porque:
   - Permite identificar qué cuentas tienen acceso activo al sistema
   - Es esencial para auditorías de seguridad
   - Facilita la revisión de quién tiene permisos habilitados actualmente
   - Es el caso de uso más común en operaciones diarias

3. **Valida comportamiento visual completo del filtro:** Verifica todos los aspectos críticos del filtrado con especial atención a la diferenciación visual:
   - Muestra exclusivamente etiquetas verdes "Activo"
   - Oculta completamente etiquetas rojas "Inactivo"
   - Actualización automática sin recarga
   - Preservación de estructura y funcionalidades

4. **Habilita gestión efectiva de acceso:** Solo con un filtrado efectivo por estado "Activo", el Administrador puede:
   - Identificar rápidamente todas las cuentas con acceso habilitado
   - Auditar usuarios activos por roles específicos
   - Gestionar deshabilitaciones masivas si es necesario
   - Verificar que solo usuarios autorizados tienen acceso activo

5. **Impacto directo en control de acceso y seguridad:** La capacidad de filtrar por estado "Activo" es crítica para:
   - **Auditorías de seguridad:** ¿Quiénes tienen acceso activo al sistema?
   - **Gestión de habilitaciones:** Identificar cuentas que requieren deshabilitación
   - **Control de acceso:** Verificar que ex-empleados o usuarios temporales no mantengan acceso activo
   - **Cumplimiento normativo:** Demostrar control sobre cuentas habilitadas

6. **Fundamento para escenarios de deshabilitación:** Sin la capacidad de identificar usuarios activos, el Administrador no puede gestionar efectivamente las deshabilitaciones de cuentas, que es el propósito declarado en la HU.

7. **Precedencia operativa:** En la práctica administrativa, es más frecuente revisar usuarios activos (para deshabilitarlos si es necesario) que revisar usuarios inactivos (para reactivarlos), haciendo este el caso de uso con mayor impacto operativo.

8. **Refleja fielmente el prototipo:** El escenario captura con precisión la diferenciación visual crítica observada en la Imagen 14: etiquetas verdes para usuarios activos vs. etiquetas rojas para usuarios inactivos.

Los demás escenarios complementan esta funcionalidad (filtrar inactivos, combinar filtros, cambio dinámico), pero el Escenario 2 es el que garantiza que el sistema cumple su propósito crítico de seguridad: **permitir al Administrador identificar y gestionar efectivamente todas las cuentas con acceso activo al sistema, que es fundamental para el control de acceso y la gestión de habilitación/deshabilitación de cuentas declarada en la Historia de Usuario**.