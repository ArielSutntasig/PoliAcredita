# HU: Vincular RA con RAA

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Matrices - RAA vs RA |
| **Rol** | Profesor |

---

## Escenario 1: Vincular RA con RAA exitosamente

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Vincular_RA_RAA_Exitoso |
| **Pre-Condiciones** | El profesor ha iniciado sesión correctamente. Existen RA y RAA disponibles para vincular |
| **Descripción Caso** | Verificar que el sistema permite vincular un RA de carrera con un RAA de asignatura |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener permisos de profesor. El RA y RAA no deben tener vinculación previa |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al módulo de matrices o vinculación RA-RAA |
| 2 | Seleccionar la asignatura correspondiente |
| 3 | Ubicar un RAA para vincular |
| 4 | Seleccionar el RA de carrera a vincular |
| 5 | Establecer el nivel de contribución |
| 6 | Confirmar la vinculación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema confirma la vinculación exitosa. La relación se muestra en la matriz. El nivel de contribución se registra correctamente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Seleccionar nivel de contribución

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Seleccionar_Nivel_Contribución_RA_RAA |
| **Pre-Condiciones** | El usuario está en proceso de vinculación |
| **Descripción Caso** | Verificar que se pueden seleccionar diferentes niveles de contribución |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Los niveles de contribución deben estar definidos |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Iniciar el proceso de vinculación RA-RAA |
| 2 | Ubicar el selector de nivel de contribución |
| 3 | Verificar las opciones disponibles (Alto, Medio, Bajo) |
| 4 | Seleccionar un nivel |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El selector muestra todas las opciones de nivel disponibles. Se puede seleccionar cualquier nivel. La selección se refleja visualmente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Agregar justificación a vinculación RA-RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Agregar_Justificación_RA_RAA |
| **Pre-Condiciones** | El usuario está creando o editando una vinculación |
| **Descripción Caso** | Verificar que se puede agregar una justificación a la vinculación |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El campo de justificación debe estar disponible |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a crear o editar una vinculación |
| 2 | Ubicar el campo de justificación |
| 3 | Ingresar el texto de justificación |
| 4 | Guardar la vinculación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La justificación se guarda correctamente junto con la vinculación. Se puede consultar posteriormente. Se respeta el límite de caracteres permitido |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Modificar vinculación existente

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Modificar_Vinculación_RA_RAA |
| **Pre-Condiciones** | Existe una vinculación RA-RAA previa |
| **Descripción Caso** | Verificar que se puede modificar una vinculación existente |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Debe existir una vinculación previa |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la matriz con vinculaciones existentes |
| 2 | Seleccionar una celda con vinculación |
| 3 | Modificar el nivel de contribución o justificación |
| 4 | Guardar los cambios |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema actualiza la vinculación correctamente. Los cambios se reflejan en la matriz. Se muestra mensaje de confirmación |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 5: Eliminar vinculación RA-RAA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Eliminar_Vinculación_RA_RAA |
| **Pre-Condiciones** | Existe una vinculación RA-RAA |
| **Descripción Caso** | Verificar que se puede eliminar una vinculación existente |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la matriz con vinculaciones |
| 2 | Seleccionar una celda con vinculación |
| 3 | Seleccionar la opción de eliminar |
| 4 | Confirmar la eliminación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La vinculación se elimina correctamente. La celda de la matriz queda vacía. Se muestra mensaje de confirmación |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 6: Vincular sin seleccionar nivel de contribución

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Vincular_Sin_Nivel_Contribución |
| **Pre-Condiciones** | El usuario está creando una nueva vinculación |
| **Descripción Caso** | Verificar la validación cuando no se selecciona nivel de contribución |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Iniciar el proceso de vinculación |
| 2 | Seleccionar RA y RAA |
| 3 | No seleccionar nivel de contribución |
| 4 | Intentar guardar |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra mensaje de validación. No permite crear la vinculación sin nivel de contribución |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
