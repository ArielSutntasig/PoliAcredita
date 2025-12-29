# HU: Buscar Asignatura para Matriz RAA vs RA

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Matrices - RAA vs RA |
| **Rol** | Coordinador de Carrera |

---

## Escenario 1: Buscar asignatura por nombre exacto

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_Asignatura_Nombre_Exacto |
| **Pre-Condiciones** | El coordinador ha iniciado sesión correctamente. Existen asignaturas registradas en el sistema |
| **Descripción Caso** | Verificar que el sistema encuentra una asignatura al buscar por nombre exacto |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe estar en el módulo de matrices |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al módulo de Matrices RAA vs RA |
| 2 | Ubicar el campo de búsqueda de asignaturas |
| 3 | Ingresar el nombre exacto de una asignatura existente |
| 4 | Ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra la asignatura buscada en los resultados. Los datos de la asignatura son correctos. Se puede seleccionar la asignatura para ver su matriz |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Buscar asignatura con coincidencia parcial

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Buscar_Asignatura_Coincidencia_Parcial |
| **Pre-Condiciones** | El coordinador ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que el sistema encuentra asignaturas con coincidencias parciales en el nombre |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | La búsqueda debe soportar coincidencias parciales |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de asignaturas en el módulo de matrices |
| 2 | Ingresar parte del nombre de una asignatura |
| 3 | Ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra todas las asignaturas que contienen el texto buscado. Los resultados están ordenados por relevancia o alfabéticamente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Buscar asignatura inexistente

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_Asignatura_Inexistente |
| **Pre-Condiciones** | El coordinador ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento del sistema al buscar una asignatura que no existe |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de asignaturas |
| 2 | Ingresar un nombre de asignatura que no existe |
| 3 | Ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no se encontraron resultados. La interfaz permanece funcional para realizar nuevas búsquedas |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Buscar asignatura con campo vacío

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Buscar_Asignatura_Campo_Vacío |
| **Pre-Condiciones** | El coordinador ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento del sistema al intentar buscar con el campo de búsqueda vacío |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al buscador de asignaturas |
| 2 | Dejar el campo de búsqueda vacío |
| 3 | Intentar ejecutar la búsqueda |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra todas las asignaturas disponibles o solicita ingresar un término de búsqueda. No se produce un error |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
