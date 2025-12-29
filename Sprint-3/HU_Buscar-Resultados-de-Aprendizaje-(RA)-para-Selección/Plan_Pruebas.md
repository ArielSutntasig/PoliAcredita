# HU: Buscar Resultados de Aprendizaje (RA) para Selección

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Resultados de Aprendizaje (RA) |
| **Rol** | Profesor |

---

## Escenario 1: Buscar RA por descripción

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_RA_Por_Descripción |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen RA registrados en el sistema |
| **Descripción Caso** | Verificar que el sistema permite buscar RA por su descripción |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe estar en un contexto de selección de RA |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al selector de RA |
| 2 | Ubicar el campo de búsqueda |
| 3 | Ingresar un texto que coincida con la descripción de un RA |
| 4 | Ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra los RA que coinciden con el texto buscado. Los resultados se actualizan dinámicamente. Se puede seleccionar un RA de los resultados |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Buscar RA sin coincidencias

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_RA_Sin_Coincidencias |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento cuando la búsqueda no encuentra RA coincidentes |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de RA |
| 2 | Ingresar un texto que no coincide con ningún RA |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no se encontraron resultados. La interfaz permite realizar una nueva búsqueda |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Búsqueda con caracteres especiales

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Buscar_RA_Caracteres_Especiales |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento del sistema al buscar con caracteres especiales |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de RA |
| 2 | Ingresar caracteres especiales en el campo de búsqueda |
| 3 | Ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema maneja correctamente los caracteres especiales. No se producen errores. Se muestra mensaje de sin resultados o resultados que contengan esos caracteres |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
