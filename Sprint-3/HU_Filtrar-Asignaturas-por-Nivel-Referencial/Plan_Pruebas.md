# HU: Filtrar Asignaturas por Nivel Referencial

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Asignaturas (PEA) |
| **Rol** | Profesor |

---

## Escenario 1: Filtrar asignaturas por nivel referencial específico

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_Asignaturas_Nivel_Específico |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen asignaturas con diferentes niveles referenciales |
| **Descripción Caso** | Verificar que el sistema filtra correctamente las asignaturas por nivel referencial |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Deben existir niveles referenciales definidos |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de asignaturas |
| 2 | Ubicar el filtro de nivel referencial |
| 3 | Seleccionar un nivel específico |
| 4 | Esperar a que se actualice la lista |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Solo se muestran las asignaturas del nivel referencial seleccionado. La lista se actualiza dinámicamente. Se indica el filtro activo |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Filtrar asignaturas sin coincidencias de nivel

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_Asignaturas_Nivel_Sin_Coincidencias |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento cuando no hay asignaturas del nivel seleccionado |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de asignaturas |
| 2 | Seleccionar un nivel referencial sin asignaturas asociadas |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no hay asignaturas de ese nivel. La interfaz permite seleccionar otro nivel |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Restablecer filtro de nivel referencial

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Restablecer_Filtro_Nivel |
| **Pre-Condiciones** | El usuario tiene un filtro de nivel activo |
| **Descripción Caso** | Verificar que el filtro de nivel puede ser restablecido |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Tener un filtro de nivel activo |
| 2 | Ubicar la opción para restablecer el filtro |
| 3 | Ejecutar el restablecimiento |
| 4 | Observar la lista de asignaturas |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El filtro se restablece a su estado inicial. Se muestran todas las asignaturas independientemente del nivel. El selector de nivel vuelve a su valor por defecto |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
