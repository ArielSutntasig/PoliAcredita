# HU: Visualizar Matriz de Relación RAA vs RA

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Matrices - RAA vs RA |
| **Rol** | Profesor |

---

## Escenario 1: Visualizar matriz con relaciones existentes

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Visualizar_Matriz_Con_Relaciones |
| **Pre-Condiciones** | El profesor ha iniciado sesión correctamente. Existen relaciones RAA-RA establecidas |
| **Descripción Caso** | Verificar que la matriz muestra correctamente las relaciones entre RAA y RA |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Deben existir datos previos de relaciones |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar al sistema como Profesor |
| 2 | Acceder al módulo de Matrices |
| 3 | Seleccionar la opción "Matriz RAA vs RA" |
| 4 | Esperar a que se cargue la matriz |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La matriz se muestra con los RAA en filas y los RA en columnas. Las celdas con relaciones muestran el nivel de contribución. Los colores o indicadores visuales son claros y distintivos |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Visualizar matriz sin relaciones

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Visualizar_Matriz_Sin_Relaciones |
| **Pre-Condiciones** | El profesor ha iniciado sesión correctamente. No existen relaciones RAA-RA |
| **Descripción Caso** | Verificar el comportamiento de la matriz cuando no hay relaciones establecidas |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al módulo de matrices |
| 2 | Seleccionar una asignatura sin relaciones |
| 3 | Observar la matriz generada |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La matriz se muestra vacía o con indicadores de "sin relación". Se muestra un mensaje orientativo. Las opciones para crear relaciones están disponibles |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Verificar leyenda de niveles de contribución

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Verificar_Leyenda_Niveles |
| **Pre-Condiciones** | La matriz está cargada con datos |
| **Descripción Caso** | Verificar que existe una leyenda que explica los niveles de contribución |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la matriz RAA vs RA |
| 2 | Ubicar la leyenda o guía de colores/niveles |
| 3 | Verificar que corresponde a los valores mostrados en la matriz |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La leyenda está visible y accesible. Muestra todos los niveles de contribución (Alto, Medio, Bajo). Los colores/indicadores coinciden con los usados en la matriz |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Interactuar con celdas de la matriz

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Interactuar_Celdas_Matriz |
| **Pre-Condiciones** | La matriz está cargada |
| **Descripción Caso** | Verificar que las celdas de la matriz son interactivas |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener permisos de edición |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la matriz RAA vs RA |
| 2 | Hacer clic en una celda de la matriz |
| 3 | Observar la respuesta del sistema |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Al hacer clic en una celda, se muestra información detallada o un diálogo de edición. Se puede ver la justificación si existe. Las opciones de edición/eliminación están disponibles según permisos |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 5: Verificar scroll horizontal y vertical

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Verificar_Scroll_Matriz |
| **Pre-Condiciones** | La matriz tiene muchas filas y columnas |
| **Descripción Caso** | Verificar que la matriz permite desplazamiento cuando hay muchos datos |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Debe haber suficientes RAA y RA para requerir scroll |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a una matriz con muchos datos |
| 2 | Intentar desplazarse horizontal y verticalmente |
| 3 | Verificar la funcionalidad de scroll |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El scroll funciona correctamente en ambas direcciones. Los encabezados permanecen visibles al desplazarse. No hay pérdida de datos ni errores visuales |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
