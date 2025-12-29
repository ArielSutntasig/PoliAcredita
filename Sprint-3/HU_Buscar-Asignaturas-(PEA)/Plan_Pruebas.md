# HU: Buscar Asignaturas (PEA)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Asignaturas (PEA) |
| **Rol** | Profesor |

---

## Escenario 1: Buscar asignatura por nombre

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_Asignatura_Por_Nombre |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen asignaturas registradas |
| **Descripción Caso** | Verificar que el sistema permite buscar asignaturas por nombre |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de asignaturas |
| 2 | Ubicar el campo de búsqueda |
| 3 | Ingresar el nombre o parte del nombre de una asignatura |
| 4 | Ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra las asignaturas que coinciden con el texto buscado. Los resultados se actualizan dinámicamente. Se resaltan las coincidencias |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Buscar asignatura por código

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_Asignatura_Por_Código |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que el sistema permite buscar asignaturas por código |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de asignaturas |
| 2 | Ingresar el código de una asignatura |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra la asignatura con el código buscado. La búsqueda es precisa para códigos exactos |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Buscar asignatura sin coincidencias

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_Asignatura_Sin_Coincidencias |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento cuando no hay asignaturas que coincidan |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de asignaturas |
| 2 | Ingresar un texto que no coincide con ninguna asignatura |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no se encontraron resultados. La interfaz permite realizar una nueva búsqueda |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Limpiar búsqueda de asignaturas

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Limpiar_Búsqueda_Asignaturas |
| **Pre-Condiciones** | El usuario tiene una búsqueda activa |
| **Descripción Caso** | Verificar que el usuario puede limpiar la búsqueda |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Tener una búsqueda de asignaturas activa |
| 2 | Ubicar la opción para limpiar la búsqueda |
| 3 | Ejecutar la limpieza |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El campo de búsqueda se vacía. Se muestran todas las asignaturas disponibles. La lista vuelve a su estado inicial |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
