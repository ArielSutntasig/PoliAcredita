# HU: Filtrar Asignaturas por créditos

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Asignaturas (PEA) |
| **Rol** | Profesor |

---

## Escenario 1: Filtrar asignaturas por número de créditos específico

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_Asignaturas_Por_Créditos_Específico |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente en la aplicación. Existe al menos una asignatura registrada con los créditos especificados |
| **Descripción Caso** | Verificar que la funcionalidad de filtrar asignaturas por un número de créditos específico funciona correctamente |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El selector de créditos debe estar habilitado en la interfaz. El usuario debe tener una carrera seleccionada previamente |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla principal de asignaturas |
| 2 | Ubicar el campo de filtro "Créditos" |
| 3 | Seleccionar un número de créditos válido |
| 4 | Esperar a que la lista se actualice automáticamente |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Solo se muestran las asignaturas que tienen el número exacto de créditos seleccionados. La lista se actualiza dinámicamente sin necesidad de recargar la página. Se muestra un mensaje indicando la cantidad de asignaturas encontradas o un mensaje si no hay coincidencias |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Filtrar asignaturas sin coincidencias

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_Asignaturas_Sin_Coincidencias |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. No existen asignaturas con cierto número de créditos seleccionado |
| **Descripción Caso** | Verificar que el sistema muestra un mensaje adecuado cuando no hay asignaturas con los créditos seleccionados |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar a la pantalla principal de asignaturas |
| 2 | Seleccionar un número de créditos sin registros asociados |
| 3 | Esperar la respuesta del sistema |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje informativo indicando que no se encontraron asignaturas con esos créditos. La tabla de asignaturas aparece vacía o con un indicador visual de "sin resultados" |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Restablecer filtro de créditos

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Restablecer_Filtro_Créditos |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existe un filtro de créditos activo |
| **Descripción Caso** | Verificar que el filtro de créditos puede ser restablecido para mostrar todas las asignaturas |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El sistema debe permitir la opción de "limpiar" o "restablecer" el filtro de créditos |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Aplicar un filtro de créditos |
| 2 | Ubicar la opción para restablecer el filtro |
| 3 | Seleccionar la opción de restablecimiento |
| 4 | Esperar a que la lista se actualice |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La lista de asignaturas muestra todas las asignaturas sin el filtro de créditos. El campo de filtro vuelve a su estado inicial (vacío o con valor por defecto) |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
