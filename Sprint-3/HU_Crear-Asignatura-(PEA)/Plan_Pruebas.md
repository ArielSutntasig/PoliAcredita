# HU: Crear Asignatura (PEA)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Asignaturas (PEA) |
| **Rol** | Profesor |

---

## Escenario 1: Crear asignatura con datos válidos

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Crear_Asignatura_Datos_Válidos |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. El usuario tiene permisos para crear asignaturas |
| **Descripción Caso** | Verificar que el sistema permite crear una nueva asignatura con todos los campos completados correctamente |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener una carrera seleccionada previamente |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de gestión de asignaturas |
| 2 | Hacer clic en el botón "Nueva Asignatura" o equivalente |
| 3 | Completar todos los campos obligatorios (nombre, código, créditos, nivel, periodo) |
| 4 | Hacer clic en el botón "Guardar" |
| 5 | Esperar la confirmación del sistema |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje de éxito. La nueva asignatura aparece en la lista. Los datos guardados corresponden a los ingresados |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Crear asignatura con campos obligatorios vacíos

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Crear_Asignatura_Campos_Vacíos |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que el sistema valida los campos obligatorios antes de crear una asignatura |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de asignatura |
| 2 | Dejar uno o más campos obligatorios vacíos |
| 3 | Intentar guardar la asignatura |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra mensajes de validación indicando los campos requeridos. No se crea la asignatura hasta completar los campos obligatorios. Los campos con error están claramente identificados |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Crear asignatura con código duplicado

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Crear_Asignatura_Código_Duplicado |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existe una asignatura con el código que se intenta usar |
| **Descripción Caso** | Verificar que el sistema previene la creación de asignaturas con códigos duplicados |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Los códigos de asignatura deben ser únicos |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de asignatura |
| 2 | Ingresar un código que ya existe en el sistema |
| 3 | Completar los demás campos |
| 4 | Intentar guardar la asignatura |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema detecta el código duplicado y muestra un mensaje de error. No permite crear la asignatura con código duplicado. Sugiere usar un código diferente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Crear asignatura con créditos inválidos

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Crear_Asignatura_Créditos_Inválidos |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que el sistema valida que los créditos sean un valor válido |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Los créditos deben ser un número positivo dentro del rango permitido |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de asignatura |
| 2 | Ingresar un valor inválido en el campo de créditos (negativo, texto, fuera de rango) |
| 3 | Completar los demás campos correctamente |
| 4 | Intentar guardar la asignatura |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje de validación indicando que el valor de créditos es inválido. No permite crear la asignatura hasta corregir el valor |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 5: Cancelar creación de asignatura

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Cancelar_Creación_Asignatura |
| **Pre-Condiciones** | El usuario ha iniciado el proceso de creación de una asignatura |
| **Descripción Caso** | Verificar que el usuario puede cancelar la creación de una asignatura sin guardar cambios |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de asignatura |
| 2 | Completar algunos campos |
| 3 | Hacer clic en el botón "Cancelar" |
| 4 | Confirmar la cancelación si se solicita |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema cierra el formulario sin guardar datos. El usuario regresa a la lista de asignaturas. No se crea ningún registro nuevo |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
