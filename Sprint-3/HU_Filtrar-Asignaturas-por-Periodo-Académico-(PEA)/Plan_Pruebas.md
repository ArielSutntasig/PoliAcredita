# HU: Filtrar Asignaturas por Periodo Académico (PEA)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Asignaturas (PEA) |
| **Rol** | Profesor |

---

## Escenario 1: Filtrar asignaturas por periodo académico específico

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_Asignaturas_Periodo_Específico |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen asignaturas en diferentes periodos académicos |
| **Descripción Caso** | Verificar que el sistema filtra correctamente las asignaturas por periodo académico |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Deben existir periodos académicos definidos |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de asignaturas |
| 2 | Ubicar el filtro de periodo académico |
| 3 | Seleccionar un periodo específico |
| 4 | Esperar a que se actualice la lista |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Solo se muestran las asignaturas del periodo académico seleccionado. La lista se actualiza dinámicamente. Se indica el filtro activo |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Filtrar asignaturas sin coincidencias de periodo

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_Asignaturas_Periodo_Sin_Coincidencias |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento cuando no hay asignaturas del periodo seleccionado |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de asignaturas |
| 2 | Seleccionar un periodo académico sin asignaturas asociadas |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no hay asignaturas en ese periodo. La interfaz permite seleccionar otro periodo |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Restablecer filtro de periodo académico

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Restablecer_Filtro_Periodo |
| **Pre-Condiciones** | El usuario tiene un filtro de periodo activo |
| **Descripción Caso** | Verificar que el filtro de periodo puede ser restablecido |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Tener un filtro de periodo activo |
| 2 | Ubicar la opción para restablecer el filtro |
| 3 | Ejecutar el restablecimiento |
| 4 | Observar la lista de asignaturas |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El filtro se restablece a su estado inicial. Se muestran todas las asignaturas independientemente del periodo. El selector de periodo vuelve a su valor por defecto |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Combinar filtro de periodo con otros filtros

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Combinar_Filtro_Periodo_Otros |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que el filtro de periodo funciona en combinación con otros filtros |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Los filtros deben ser combinables |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Aplicar un filtro de periodo académico |
| 2 | Aplicar un filtro adicional (ej: créditos, nivel) |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Los resultados cumplen todos los criterios de filtrado aplicados. Ambos filtros están visiblemente activos. La lista refleja la intersección de los filtros |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
