# HU: Vincular RAA con RA (Coordinador)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Matrices - RAA vs RA |
| **Rol** | Coordinador de Carrera |

---

## Escenario 1: Vincular RAA con RA exitosamente

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Vincular_RAA_RA_Exitoso |
| **Pre-Condiciones** | El coordinador ha iniciado sesión correctamente. Existen RAA y RA disponibles para vincular |
| **Descripción Caso** | Verificar que el sistema permite vincular un RAA con un RA estableciendo el nivel de contribución |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener rol de Coordinador. El RAA y RA no deben tener vinculación previa |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al módulo de matrices RAA vs RA |
| 2 | Seleccionar una asignatura |
| 3 | Ubicar un RAA sin vincular |
| 4 | Seleccionar el RA a vincular |
| 5 | Establecer el nivel de contribución (Alto, Medio, Bajo) |
| 6 | Confirmar la vinculación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema confirma la vinculación exitosa. La matriz se actualiza mostrando la nueva relación. El nivel de contribución se muestra correctamente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Modificar nivel de contribución existente

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Modificar_Nivel_Contribución |
| **Pre-Condiciones** | Existe una vinculación RAA-RA previa |
| **Descripción Caso** | Verificar que se puede modificar el nivel de contribución de una vinculación existente |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Debe existir una vinculación previa |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la matriz RAA vs RA |
| 2 | Ubicar una celda con vinculación existente |
| 3 | Seleccionar la celda para editar |
| 4 | Cambiar el nivel de contribución |
| 5 | Guardar los cambios |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema actualiza el nivel de contribución. La matriz refleja el nuevo valor. Se muestra mensaje de confirmación |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Eliminar vinculación RAA-RA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Eliminar_Vinculación_RAA_RA |
| **Pre-Condiciones** | Existe una vinculación RAA-RA |
| **Descripción Caso** | Verificar que se puede eliminar una vinculación existente |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la matriz RAA vs RA |
| 2 | Ubicar una celda con vinculación |
| 3 | Seleccionar la opción para eliminar la vinculación |
| 4 | Confirmar la eliminación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La vinculación se elimina correctamente. La celda de la matriz queda vacía. Se muestra mensaje de confirmación |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Agregar justificación a la vinculación

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Agregar_Justificación_Vinculación |
| **Pre-Condiciones** | El coordinador está creando o editando una vinculación |
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
| 4 | Guardar los cambios |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La justificación se guarda correctamente. Se puede consultar la justificación posteriormente. El sistema respeta el límite de caracteres |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 5: Intentar vincular sin seleccionar nivel de contribución

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Vincular_Sin_Nivel_Contribución |
| **Pre-Condiciones** | El coordinador está creando una nueva vinculación |
| **Descripción Caso** | Verificar la validación cuando no se selecciona nivel de contribución |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Iniciar el proceso de vinculación RAA-RA |
| 2 | Seleccionar RAA y RA |
| 3 | No seleccionar nivel de contribución |
| 4 | Intentar guardar la vinculación |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje de validación indicando que es necesario seleccionar el nivel de contribución. No se crea la vinculación |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 6: Vincular RAA con múltiples RA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Alta |
| **Nombre Testing** | CP_Vincular_RAA_Múltiples_RA |
| **Pre-Condiciones** | Existen múltiples RA disponibles |
| **Descripción Caso** | Verificar que un RAA puede vincularse con múltiples RA |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Depende de las reglas de negocio |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Seleccionar un RAA |
| 2 | Vincularlo con un primer RA |
| 3 | Vincular el mismo RAA con un segundo RA |
| 4 | Verificar ambas vinculaciones |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema permite múltiples vinculaciones para un RAA. La matriz muestra todas las relaciones correctamente. Cada vinculación puede tener diferente nivel de contribución |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 7: Visualizar historial de cambios en vinculación

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Alta |
| **Nombre Testing** | CP_Visualizar_Historial_Vinculación |
| **Pre-Condiciones** | Existen vinculaciones con modificaciones previas |
| **Descripción Caso** | Verificar que se puede consultar el historial de cambios de una vinculación |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | La funcionalidad de historial debe estar implementada |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a una vinculación con historial |
| 2 | Seleccionar la opción de ver historial |
| 3 | Revisar los cambios registrados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra el historial de cambios con fechas, usuarios y valores anteriores/nuevos. La información está ordenada cronológicamente |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
