# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 18 del prototipo):**

1. **C1:** Se accede a la pantalla "Gestión de Roles"
2. **C2:** Se visualizan tarjetas de roles existentes con sus permisos actuales
3. **C3:** Se selecciona una tarjeta de rol para editar permisos (ej: "Coordinador de Carrera")
4. **C4:** Se abre interfaz de edición de permisos del rol
5. **C5:** Se modifica el estado de checkboxes de permisos (marcar/desmarcar)
6. **C6:** Se marcan permisos en diferentes módulos (Facultades, Carreras, Usuarios, Usuarios y Roles)
7. **C7:** Al menos un permiso está marcado para el rol
8. **C8:** Se hace clic en "Guardar" o "Actualizar"

### **Acciones del Sistema (observadas en Imagen 18):**

1. **A1:** Mostrar pantalla "Gestión de Roles" con título principal
2. **A2:** Mostrar tarjetas de roles en cuadrícula (2 filas x 3 columnas)
3. **A3:** Mostrar para cada rol: título, descripción, y permisos organizados por módulos
4. **A4:** Mostrar 4 módulos de permisos por rol: "Gestión de Facultades", "Gestión de Carreras", "Gestión de Usuarios", "Gestión de Usuarios y Roles"
5. **A5:** Mostrar checkboxes para cada permiso (marcado ■ o desmarcado □)
6. **A6:** Indicar visualmente permisos activos con checkbox marcado (■)
7. **A7:** Indicar visualmente permisos inactivos con checkbox desmarcado (□)
8. **A8:** Permitir editar permisos al seleccionar una tarjeta de rol
9. **A9:** Validar que al menos un permiso esté marcado
10. **A10:** Guardar cambios de permisos en base de datos
11. **A11:** Actualizar vista de la tarjeta con nuevos permisos
12. **A12:** Propagar cambios a todos los usuarios con ese rol
13. **A13:** Mostrar mensaje de éxito tras actualización

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Se selecciona rol para editar
- **C2:** Se modifican checkboxes de permisos
- **C3:** Al menos un permiso está marcado
- **C4:** Se guarda la configuración

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Rol seleccionado | C2: Permisos modificados | C3: Permisos marcados | C4: Guardar | Acción |
|-------|---------------------|------------------------|---------------------|------------|---------|
| R1 | N | N | - | N | A1-A7: Solo vista de tarjetas |
| R2 | N | N | - | S | Imposible |
| R3 | N | S | - | - | Imposible |
| R4 | N | S | - | - | Imposible |
| R5 | S | N | - | N | A8: Mostrar permisos actuales editables |
| R6 | S | N | - | S | Sin cambios, cerrar edición |
| R7 | S | S | N | N | En edición |
| R8 | S | S | N | S | Error "Debe marcar al menos un permiso" |
| R9 | S | S | S | N | En edición con cambios válidos |
| R10 | S | S | S | S | A10-A13: Guardar y actualizar |

---

## **Tabla de Decisión Minimizada**

| Regla | Rol seleccionado | Permisos modificados | Permisos marcados | Guardar | Acción |
|-------|-----------------|---------------------|------------------|---------|---------|
| **R1** | N | - | - | - | Mostrar vista de tarjetas con permisos actuales |
| **R2** | S | N | - | N | Abrir edición, mostrar permisos actuales |
| **R3** | S | N | - | S | Cerrar sin cambios |
| **R4** | S | S | N | S | Error "Debe seleccionar al menos un permiso" |
| **R5** | S | S | S | N | Edición en curso con cambios válidos |
| **R6** | S | S | S | S | Guardar, actualizar tarjeta, propagar a usuarios |

**Justificación de la minimización:**
- **R1:** Vista inicial mostrando todos los roles con sus permisos configurados
- **R2:** Modo edición abierto sin modificaciones
- **R3:** Usuario cancela o cierra sin hacer cambios
- **R4:** Validación: rol debe tener al menos un permiso
- **R5:** Usuario editando pero no ha guardado
- **R6:** Happy path: cambios válidos guardados exitosamente

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 11 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios principales)
- 5 escenarios adicionales para validar aspectos específicos:
  - Visualización inicial de tarjetas con estructura jerárquica
  - Edición de permisos de rol específico
  - Organización por módulos como muestra el prototipo
  - Permisos específicos observados (Ver, Crear, Editar, Eliminar)
  - Validación de estructura jerárquica académica

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin) - ACTUALIZADA**

**Escenario 1 – Visualizar pantalla de Gestión de Roles con tarjetas de roles**

**Dado que** estoy autenticado como Administrador en el sistema,  
**cuando** accedo a la opción "Roles" desde el menú lateral,  
**entonces** se muestra la pantalla con el título "Gestión de Roles" **Y** se presentan tarjetas de roles organizadas en cuadrícula (6 roles visibles: Administrador, CEI, Autoridad de facultad, Coordinador de Carrera, Personal Administrativo, Profesor) **Y** cada tarjeta muestra el nombre del rol en negrita (ej: "Administrador", "Coordinador de Carrera") **Y** cada tarjeta incluye una descripción breve del rol (ej: "Acceso total al sistema y gestión de todos los módulos y usuarios") **Y** cada tarjeta muestra permisos organizados en 4 módulos: "Gestión de Facultades", "Gestión de Carreras", "Gestión de Usuarios", "Gestión de Usuarios y Roles" **Y** cada permiso se presenta con checkbox (**✓ marcado con checkmark azul**, **☐ desmarcado vacío**) **Y** puedo visualizar la configuración actual de permisos de cada rol sin necesidad de abrir modales.

---

**Escenario 2 – Visualizar permisos organizados por módulos en cada rol** *(ACTUALIZADO)*

**Dado que** estoy en la pantalla "Gestión de Roles",  
**cuando** reviso cualquier tarjeta de rol (ej: "Autoridad de facultad"),  
**entonces** los permisos están organizados en 4 módulos claramente identificados **Y** bajo "Gestión de Facultades" se muestran: "**✓** Ver facultades", "**☐** Crear facultades", "**✓** Editar facultades", "**☐** Eliminar facultades" **Y** bajo "Gestión de Carreras" se muestran: "**✓** Ver carreras", "**✓** Crear carreras", "**✓** Editar carreras", "**☐** Eliminar carreras" **Y** bajo "Gestión de Usuarios" se muestran: "**✓** Ver profesores", "**✓** Crear profesores", "**✓** Editar profesores", "**☐** Eliminar profesores" **Y** bajo "Gestión de Usuarios y Roles" se muestran: "**☐** Ver usuarios", "**☐** Asignar roles", "**☐** Desactivar usuarios", "**☐** Ver roles", "**☐** Configurar permisos" **Y** los checkmarks azules (✓) indican permisos activos **Y** los checkboxes vacíos (☐) indican permisos inactivos **Y** la organización por módulos facilita la comprensión de capacidades del rol en cada área del sistema.

---

**Escenario 3 – Visualizar estructura jerárquica mediante permisos de rol Administrador** *(ACTUALIZADO)*

**Dado que** estoy en la pantalla "Gestión de Roles",  
**cuando** reviso la tarjeta del rol "Administrador",  
**entonces** el rol muestra la descripción "Acceso total al sistema y gestión de todos los módulos y usuarios" **Y** TODOS los checkboxes de permisos están marcados con checkmark azul (**✓**) en los 4 módulos **Y** bajo "Gestión de Facultades": **✓** Ver, **✓** Crear, **✓** Editar, **✓** Eliminar facultades **Y** bajo "Gestión de Carreras": **✓** Ver, **✓** Crear, **✓** Editar, **✓** Eliminar carreras **Y** bajo "Gestión de Usuarios": **✓** Ver, **✓** Crear, **✓** Editar, **✓** Eliminar profesores **Y** bajo "Gestión de Usuarios y Roles": **✓** Ver usuarios, **✓** Asignar roles, **✓** Desactivar usuarios, **✓** Ver roles, **✓** Configurar permisos **Y** esta configuración con todos los checkmarks activos refleja que Administrador está en el nivel jerárquico superior con control total del sistema.

---

**Escenario 4 – Visualizar estructura jerárquica mediante permisos de rol Profesor** *(ACTUALIZADO)*

**Dado que** estoy en la pantalla "Gestión de Roles",  
**cuando** reviso la tarjeta del rol "Profesor",  
**entonces** el rol muestra la descripción "Gestión de carreras específicas" **Y** tiene permisos muy limitados comparado con roles superiores **Y** bajo "Gestión de Facultades": **✓** Ver facultades, **☐** Crear, **☐** Editar, **☐** Eliminar facultades **Y** bajo "Gestión de Carreras": **✓** Ver carreras, **☐** Crear, **☐** Editar, **☐** Eliminar carreras **Y** bajo "Gestión de Usuarios": **✓** Ver profesores, **☐** Crear, **☐** Editar, **☐** Eliminar profesores **Y** bajo "Gestión de Usuarios y Roles": **☐** Ver usuarios, **☐** Asignar roles, **☐** Desactivar usuarios, **☐** Ver roles, **☐** Configurar permisos **Y** esta configuración con predominancia de checkboxes vacíos (☐) y solo algunos checkmarks (✓) en permisos de visualización refleja que Profesor está en nivel operativo con capacidades principalmente de lectura **Y** la diferencia con Administrador establece claramente la jerarquía académica.

---

**Escenario 5 – Editar permisos de un rol existente**

**Dado que** estoy en la pantalla "Gestión de Roles" **Y** deseo modificar permisos del rol "Coordinador de Carrera",  
**cuando** hago clic en la tarjeta de "Coordinador de Carrera" o en un botón de edición asociado,  
**entonces** se habilita el modo de edición para ese rol (mediante modal, panel expandido, o checkboxes editables en la tarjeta) **Y** puedo modificar los checkboxes haciendo clic para marcarlos (agregar ✓) o desmarcarlos (quitar ✓) **Y** por ejemplo, si deseo agregar el permiso "Crear carreras" hago clic en el checkbox y aparece el checkmark azul (✓) **Y** si deseo revocar "Editar profesores" hago clic en el checkbox marcado y el checkmark (✓) desaparece dejándolo vacío (☐) **Y** los cambios son visibles inmediatamente en la interfaz de edición **Y** se presenta un botón "Guardar" o "Actualizar Permisos" para confirmar cambios.

---

**Escenario 6 – Guardar permisos actualizados de un rol exitosamente** *(ACTUALIZADO)*

**Dado que** estoy editando permisos del rol "Coordinador de Carrera" **Y** he modificado algunos checkboxes (ej: agregué **✓** Crear carreras, **✓** Editar carreras donde antes estaban vacíos **☐**),  
**cuando** hago clic en el botón "Guardar" o "Actualizar Permisos",  
**entonces** el sistema valida que al menos un permiso esté marcado con checkmark (✓) **Y** se guardan los nuevos permisos en la base de datos asociados al rol "Coordinador de Carrera" **Y** se cierra el modo de edición (modal o panel) **Y** la tarjeta de "Coordinador de Carrera" se actualiza mostrando los nuevos checkmarks azules (✓) en los permisos recién activados **Y** se muestra un mensaje de notificación de éxito "Permisos actualizados exitosamente" o "Permisos del rol actualizados correctamente" **Y** todos los usuarios con rol "Coordinador de Carrera" obtienen automáticamente los nuevos permisos (ej: ahora pueden crear y editar carreras).

---

**Escenario 7 – Intentar guardar rol sin ningún permiso marcado**

**Dado que** estoy editando permisos del rol "Personal Administrativo" **Y** desmarcó todos los checkboxes quitando todos los checkmarks (✓) dejando el rol con todos los permisos vacíos (☐),  
**cuando** intento guardar haciendo clic en "Guardar" o "Actualizar Permisos",  
**entonces** el sistema valida que debe haber al menos un checkbox marcado con checkmark (✓) **Y** no se guardan los cambios en la base de datos **Y** se muestra un mensaje de error "Debe seleccionar al menos un permiso para el rol" o "Un rol requiere al menos un permiso activo" **Y** el mensaje se presenta de forma destacada (ej: texto rojo, icono de alerta) **Y** permanezco en el modo de edición para corregir la configuración **Y** puedo marcar al menos un permiso (agregar al menos un ✓) y volver a intentar guardar.

---

**Escenario 8 – Cancelar edición de permisos sin guardar cambios**

**Dado que** estoy editando permisos del rol "CEI (Comité de Evaluación Interna)" **Y** he modificado algunos checkboxes (agregando o quitando checkmarks ✓),  
**cuando** hago clic en el botón "Cancelar" o cierro el modal/panel de edición,  
**entonces** se cierra el modo de edición inmediatamente **Y** no se guardan los cambios realizados en la base de datos **Y** la tarjeta de "CEI" muestra los permisos en su estado original con los checkmarks (✓) y checkboxes vacíos (☐) como estaban antes de la edición **Y** no se muestra ningún mensaje de éxito ni error **Y** puedo volver a editar el rol si lo deseo y los checkboxes estarán en su estado original.

---

**Escenario 9 – Establecer permisos diferenciados para roles de nivel medio (Coordinador)** *(ACTUALIZADO)*

**Dado que** estoy configurando permisos para establecer la jerarquía académica **Y** el rol "Coordinador de Carrera" representa un nivel intermedio,  
**cuando** reviso o edito los permisos de "Coordinador de Carrera",  
**entonces** el rol tiene permisos enfocados en gestión de carreras y algunos sobre usuarios **Y** basado en el prototipo, tiene: **✓** Ver facultades, **☐** Crear facultades, **☐** Editar facultades, **☐** Eliminar facultades **Y** **✓** Ver carreras, **✓** Crear carreras, **✓** Editar carreras, **☐** Eliminar carreras **Y** **✓** Ver profesores, **☐** Crear profesores, **☐** Editar profesores, **☐** Eliminar profesores **Y** **☐** Ver usuarios, **☐** Asignar roles, **☐** Desactivar usuarios, **☐** Ver roles, **☐** Configurar permisos **Y** esta configuración con checkmarks (✓) enfocados en carreras y visualización, pero checkboxes vacíos (☐) en operaciones sensibles, refleja autoridad sobre carreras pero limitada sobre facultades y usuarios **Y** establece su posición intermedia en la jerarquía entre Administrador/Autoridad de facultad (superior) y Profesor (inferior).

---

**Escenario 10 – Validar propagación de cambios a usuarios con el rol modificado**

**Dado que** existen usuarios activos con el rol "Autoridad de facultad" (ej: 3 usuarios: Juan Pérez como Decano, María García como Decana, Pedro López como Decano) **Y** actualmente el rol tiene ciertos permisos limitados,  
**cuando** como Administrador edito el rol "Autoridad de facultad" **Y** agrego un nuevo permiso haciendo clic en el checkbox de "Eliminar carreras" para marcarlo con checkmark azul (**✓**) **Y** guardo los cambios exitosamente,  
**entonces** los 3 usuarios con rol "Autoridad de facultad" obtienen inmediatamente el permiso "Eliminar carreras" **Y** si alguno está activo en el sistema, puede ejecutar la nueva acción sin cerrar sesión **Y** al acceder a su perfil ("Mi Perfil") verán "Eliminar carreras" en su lista de permisos bajo "Ver Permisos Detallados" **Y** pueden usar el botón de eliminar (icono papelera) en la tabla de carreras inmediatamente **Y** el cambio en el rol afecta consistentemente a todos los usuarios con ese rol.

---

**Escenario 11 – Visualizar y validar la jerarquía académica completa mediante comparación de roles** *(ACTUALIZADO)*

**Dado que** estoy en la pantalla "Gestión de Roles" **Y** puedo ver las 6 tarjetas de roles simultáneamente,  
**cuando** comparo los permisos entre los diferentes roles observando los checkmarks azules (✓) y checkboxes vacíos (☐),  
**entonces** puedo identificar claramente la estructura jerárquica académica establecida **Y** **Nivel 1 (Superior):** "Administrador" tiene TODOS los permisos marcados con checkmark azul (**✓**) en todos los módulos (control total del sistema) **Y** **Nivel 2 (Autoridades):** "Autoridad de facultad" tiene muchos checkmarks (**✓**) en Facultades y Carreras pero algunos checkboxes vacíos (**☐**) en configuración de sistema **Y** **Nivel 3 (Coordinación):** "Coordinador de Carrera" tiene checkmarks (**✓**) enfocados en permisos de Carreras y visualización, con más checkboxes vacíos (**☐**) que Autoridad **Y** **Nivel 4 (Operativo):** "Profesor" tiene principalmente checkboxes vacíos (**☐**) con solo algunos checkmarks (**✓**) en permisos de visualización (Ver) **Y** **Roles Especiales:** "CEI" tiene checkmarks (**✓**) principalmente en permisos de lectura para auditoría, "Personal Administrativo" tiene checkmarks (**✓**) en permisos operativos específicos **Y** la densidad de checkmarks azules (✓) vs checkboxes vacíos (☐) refleja visualmente el nivel de autoridad **Y** la diferenciación de permisos refleja claramente niveles de autoridad y responsabilidad **Y** la estructura establece cadena de mando académica institucional mediante control de acceso basado en roles.

---

# **Cambios Realizados:**

1. **Reemplazo de notación:**
   - **■** → **✓** (checkmark azul) para permisos activos/marcados
   - **□** → **☐** (checkbox vacío) para permisos inactivos/desmarcados

2. **Énfasis agregado:** Se agregaron descripciones adicionales como "checkmark azul" y "checkbox vacío" para mayor claridad visual

3. **Escenarios actualizados:** 2, 3, 4, 6, 9, y 11 fueron modificados con la notación correcta

4. **Consistencia:** Todos los ejemplos de permisos ahora usan la notación de checkmarks (✓) como se observa en el prototipo real

La actualización mantiene toda la lógica, análisis y estructura original, solo corrige la representación visual exacta de los controles de checkbox según el prototipo de la Imagen 18.