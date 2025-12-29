# HU: Paginar Asignaturas (PEA)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Asignaturas (PEA) |
| **Rol** | Profesor |

---

## Escenario 1: Navegar a la siguiente página de asignaturas

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Paginar_Asignaturas_Siguiente_Página |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen más asignaturas de las que se pueden mostrar en una sola página |
| **Descripción Caso** | Verificar que la paginación permite navegar a la siguiente página de asignaturas |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Debe existir más de una página de resultados |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de listado de asignaturas |
| 2 | Ubicar los controles de paginación |
| 3 | Hacer clic en el botón "Siguiente" o en el número de la siguiente página |
| 4 | Esperar a que se carguen los nuevos resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Se muestran las asignaturas de la siguiente página. El indicador de página actual se actualiza. Los botones de paginación reflejan la nueva posición |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Navegar a la página anterior de asignaturas

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Paginar_Asignaturas_Página_Anterior |
| **Pre-Condiciones** | El usuario ha navegado previamente a una página distinta a la primera |
| **Descripción Caso** | Verificar que la paginación permite regresar a la página anterior |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario no debe estar en la primera página |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Estar en una página distinta a la primera |
| 2 | Hacer clic en el botón "Anterior" o seleccionar la página anterior |
| 3 | Esperar a que se actualice la lista |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Se muestran las asignaturas de la página anterior. El indicador de página se actualiza correctamente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Ir a una página específica de asignaturas

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Paginar_Asignaturas_Página_Específica |
| **Pre-Condiciones** | Existen múltiples páginas de asignaturas |
| **Descripción Caso** | Verificar que el usuario puede navegar directamente a una página específica |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | La página seleccionada debe existir dentro del rango de páginas disponibles |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ubicar el selector de página o los números de página |
| 2 | Seleccionar un número de página específico |
| 3 | Esperar a que se carguen los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La lista muestra las asignaturas correspondientes a la página seleccionada. Los controles de paginación reflejan la página actual |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Intentar paginar cuando hay una sola página

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Paginar_Asignaturas_Única_Página |
| **Pre-Condiciones** | Existen pocas asignaturas que caben en una sola página |
| **Descripción Caso** | Verificar el comportamiento del sistema cuando solo existe una página de resultados |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de listado de asignaturas con pocos registros |
| 2 | Observar el estado de los controles de paginación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Los controles de navegación están deshabilitados o no visibles. Se muestra que es la única página disponible |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
