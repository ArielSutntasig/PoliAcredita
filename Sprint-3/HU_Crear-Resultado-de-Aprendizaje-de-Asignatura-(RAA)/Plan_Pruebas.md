# HU: Crear Resultado de Aprendizaje de Asignatura (RAA)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Resultados de Aprendizaje (RAA) |
| **Rol** | Profesor |

---

## Escenario 1: Crear RAA con datos válidos

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Crear_RAA_Datos_Válidos |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existe al menos una asignatura donde crear el RAA |
| **Descripción Caso** | Verificar que el sistema permite crear un nuevo RAA con todos los campos completados correctamente |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener permisos para crear RAA. La asignatura debe estar activa |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla de gestión de RAA de una asignatura |
| 2 | Hacer clic en el botón "Crear nuevo RAA" o equivalente |
| 3 | Completar todos los campos obligatorios (descripción, nivel de contribución) |
| 4 | Hacer clic en el botón "Guardar" o "Crear" |
| 5 | Esperar la confirmación del sistema |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje de éxito. El nuevo RAA aparece en la lista de resultados de aprendizaje. Los datos guardados corresponden a los ingresados |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Crear RAA con campos obligatorios vacíos

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Crear_RAA_Campos_Vacíos |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que el sistema valida los campos obligatorios antes de crear un RAA |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de RAA |
| 2 | Dejar campos obligatorios vacíos |
| 3 | Intentar guardar el RAA |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra mensajes de validación indicando los campos requeridos. No se crea el RAA hasta completar los campos obligatorios |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Crear RAA duplicado

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Crear_RAA_Duplicado |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existe un RAA con la misma descripción en la asignatura |
| **Descripción Caso** | Verificar el comportamiento del sistema al intentar crear un RAA con descripción duplicada |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Depende de las reglas de negocio sobre duplicados |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de RAA |
| 2 | Ingresar una descripción idéntica a un RAA existente |
| 3 | Completar los demás campos |
| 4 | Intentar guardar el RAA |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema detecta la duplicidad y muestra un mensaje de advertencia o error. No permite crear RAA duplicados o solicita confirmación |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Cancelar creación de RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Cancelar_Creación_RAA |
| **Pre-Condiciones** | El usuario ha iniciado el proceso de creación de un RAA |
| **Descripción Caso** | Verificar que el usuario puede cancelar la creación de un RAA sin guardar cambios |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de RAA |
| 2 | Completar algunos campos |
| 3 | Hacer clic en el botón "Cancelar" |
| 4 | Confirmar la cancelación si se solicita |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema cierra el formulario sin guardar datos. El usuario regresa a la lista de RAA. No se crea ningún registro nuevo |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 5: Validar longitud máxima de descripción RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Validar_Longitud_Descripción_RAA |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que el sistema valida la longitud máxima permitida para la descripción del RAA |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Debe existir un límite de caracteres definido |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al formulario de creación de RAA |
| 2 | Ingresar una descripción que exceda el límite permitido |
| 3 | Intentar guardar el RAA |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema impide ingresar más caracteres del límite permitido o muestra un mensaje de validación. El contador de caracteres (si existe) indica el límite alcanzado |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
