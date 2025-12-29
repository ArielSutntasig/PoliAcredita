# HU: Listar Asignaturas (PEA)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Asignaturas (PEA) |
| **Rol** | Profesor |

---

## Escenario 1: Listar asignaturas con resultados

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Listar_Asignaturas_Con_Resultados |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen asignaturas registradas para la carrera seleccionada |
| **Descripción Caso** | Verificar que el sistema muestra correctamente la lista de asignaturas |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener una carrera seleccionada |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla principal de asignaturas |
| 2 | Verificar que se carga la lista automáticamente |
| 3 | Observar las asignaturas mostradas |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Se muestra una lista con todas las asignaturas de la carrera. Cada asignatura muestra su código, nombre, créditos y nivel. La lista está ordenada de forma coherente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Listar asignaturas sin resultados

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Listar_Asignaturas_Sin_Resultados |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. No existen asignaturas para la carrera seleccionada |
| **Descripción Caso** | Verificar el comportamiento del sistema cuando no hay asignaturas |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de asignaturas |
| 2 | Observar el estado de la lista |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no hay asignaturas registradas. Se ofrece la opción de crear una nueva asignatura |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Verificar información de cada asignatura

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Verificar_Información_Asignatura |
| **Pre-Condiciones** | Existen asignaturas con información completa |
| **Descripción Caso** | Verificar que cada asignatura muestra toda la información necesaria |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de asignaturas |
| 2 | Revisar la información mostrada para cada asignatura |
| 3 | Verificar que se muestran todos los campos relevantes |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Cada asignatura muestra: código, nombre completo, número de créditos, nivel referencial, periodo académico. Existen opciones para ver detalles, editar y eliminar |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
