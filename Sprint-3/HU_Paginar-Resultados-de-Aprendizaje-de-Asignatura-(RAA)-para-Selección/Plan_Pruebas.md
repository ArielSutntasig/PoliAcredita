# HU: Paginar Resultados de Aprendizaje de Asignatura (RAA) para Selección

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Resultados de Aprendizaje (RAA) |
| **Rol** | Profesor |

---

## Escenario 1: Navegar a siguiente página de RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Paginar_RAA_Siguiente |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen más RAA de los que caben en una página |
| **Descripción Caso** | Verificar que la paginación permite navegar a la siguiente página de RAA |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Debe haber suficientes RAA para generar múltiples páginas |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de RAA para selección |
| 2 | Ubicar los controles de paginación |
| 3 | Hacer clic en "Siguiente" o en el número de la siguiente página |
| 4 | Esperar a que se carguen los nuevos resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Se muestran los RAA de la siguiente página. El indicador de página actual se actualiza. Los controles de navegación reflejan la posición actual |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Navegar a página anterior de RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Paginar_RAA_Anterior |
| **Pre-Condiciones** | El usuario está en una página posterior a la primera |
| **Descripción Caso** | Verificar que la paginación permite regresar a la página anterior |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | No estar en la primera página |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Estar en una página distinta a la primera |
| 2 | Hacer clic en "Anterior" |
| 3 | Esperar la actualización de la lista |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Se muestran los RAA de la página anterior. El indicador de página se actualiza correctamente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Ir a página específica de RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Paginar_RAA_Específica |
| **Pre-Condiciones** | Existen múltiples páginas de RAA |
| **Descripción Caso** | Verificar la navegación directa a una página específica |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | La página debe existir |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ubicar el selector de página o números de página |
| 2 | Seleccionar un número de página específico |
| 3 | Esperar la carga de resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La lista muestra los RAA de la página seleccionada. Los controles reflejan la página actual |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Paginación con una sola página de RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Paginar_RAA_Única_Página |
| **Pre-Condiciones** | Existen pocos RAA que caben en una sola página |
| **Descripción Caso** | Verificar el comportamiento cuando solo hay una página de resultados |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de RAA con pocos registros |
| 2 | Observar el estado de los controles de paginación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Los controles de navegación están deshabilitados o no visibles. Se indica que es la única página disponible |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
