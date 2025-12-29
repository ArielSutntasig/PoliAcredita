# HU: Listar Resultados de Aprendizaje de Asignatura (RAA)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Resultados de Aprendizaje (RAA) |
| **Rol** | Profesor |

---

## Escenario 1: Listar RAA de una asignatura con resultados

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Listar_RAA_Con_Resultados |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existe al menos una asignatura con RAA registrados |
| **Descripción Caso** | Verificar que el sistema muestra correctamente la lista de RAA para una asignatura seleccionada |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener una asignatura seleccionada |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de gestión de asignaturas |
| 2 | Seleccionar una asignatura con RAA registrados |
| 3 | Acceder a la sección de Resultados de Aprendizaje de la asignatura |
| 4 | Esperar a que se cargue la lista de RAA |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Se muestra una lista con todos los RAA asociados a la asignatura. Cada RAA muestra su código, descripción y nivel de contribución. La lista está ordenada de forma coherente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Listar RAA de una asignatura sin resultados

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Listar_RAA_Sin_Resultados |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existe una asignatura sin RAA registrados |
| **Descripción Caso** | Verificar que el sistema muestra un mensaje adecuado cuando no hay RAA para una asignatura |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de gestión de asignaturas |
| 2 | Seleccionar una asignatura sin RAA |
| 3 | Acceder a la sección de Resultados de Aprendizaje |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no hay RAA registrados para esta asignatura. Se ofrece la opción de crear un nuevo RAA |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Verificar información mostrada en cada RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Verificar_Información_RAA |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen RAA registrados con información completa |
| **Descripción Caso** | Verificar que cada RAA en la lista muestra toda la información necesaria |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de RAA de una asignatura |
| 2 | Revisar la información mostrada para cada RAA |
| 3 | Verificar que se muestran todos los campos relevantes |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Cada RAA muestra: código identificador, descripción del resultado de aprendizaje, nivel de contribución (si aplica), opciones de edición y eliminación. La información es legible y está bien formateada |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
