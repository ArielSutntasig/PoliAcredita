# HU: Buscar Resultados de Aprendizaje de Asignatura (RAA) para Selección

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Resultados de Aprendizaje (RAA) |
| **Rol** | Profesor |

---

## Escenario 1: Buscar RAA por descripción

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_RAA_Por_Descripción |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen RAA registrados en el sistema |
| **Descripción Caso** | Verificar que el sistema permite buscar RAA por su descripción |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe estar en un contexto de selección de RAA |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al selector de RAA |
| 2 | Ubicar el campo de búsqueda |
| 3 | Ingresar un texto que coincida con la descripción de un RAA |
| 4 | Ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra los RAA que coinciden con el texto buscado. Los resultados se actualizan dinámicamente. Se puede seleccionar un RAA de los resultados |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Buscar RAA sin coincidencias

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_RAA_Sin_Coincidencias |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento cuando la búsqueda no encuentra RAA coincidentes |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de RAA |
| 2 | Ingresar un texto que no coincide con ningún RAA |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no se encontraron resultados. La interfaz permite realizar una nueva búsqueda |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Limpiar búsqueda de RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Limpiar_Búsqueda_RAA |
| **Pre-Condiciones** | El usuario tiene una búsqueda activa de RAA |
| **Descripción Caso** | Verificar que el usuario puede limpiar la búsqueda y ver todos los RAA |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Tener una búsqueda de RAA activa |
| 2 | Ubicar la opción para limpiar la búsqueda |
| 3 | Ejecutar la limpieza |
| 4 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El campo de búsqueda se vacía. Se muestran todos los RAA disponibles. La lista vuelve a su estado inicial |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
