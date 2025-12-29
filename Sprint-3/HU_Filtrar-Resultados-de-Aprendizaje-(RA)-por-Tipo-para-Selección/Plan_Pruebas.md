# HU: Filtrar Resultados de Aprendizaje (RA) por Tipo para Selección

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Resultados de Aprendizaje (RA) |
| **Rol** | Profesor |

---

## Escenario 1: Filtrar RA por tipo específico

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_RA_Por_Tipo |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen RA de diferentes tipos |
| **Descripción Caso** | Verificar que el sistema permite filtrar RA por su tipo |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Deben existir tipos de RA definidos en el sistema |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de RA para selección |
| 2 | Ubicar el filtro de tipo de RA |
| 3 | Seleccionar un tipo específico |
| 4 | Esperar a que se actualice la lista |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Solo se muestran los RA del tipo seleccionado. La lista se actualiza dinámicamente. El filtro activo está claramente indicado |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Filtrar RA sin resultados para el tipo

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Filtrar_RA_Sin_Resultados_Tipo |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar el comportamiento cuando no hay RA del tipo seleccionado |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de RA |
| 2 | Seleccionar un tipo que no tiene RA asociados |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no hay RA de ese tipo. La interfaz permite seleccionar otro tipo |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Combinar filtro de tipo con búsqueda

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Combinar_Filtro_Tipo_Búsqueda |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente |
| **Descripción Caso** | Verificar que se puede combinar el filtro de tipo con una búsqueda de texto |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | La búsqueda debe respetar el filtro de tipo activo |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Aplicar un filtro de tipo de RA |
| 2 | Ingresar un término de búsqueda |
| 3 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Los resultados cumplen ambos criterios: son del tipo seleccionado Y coinciden con el texto buscado. Ambos filtros están visiblemente activos |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Limpiar filtro de tipo

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Limpiar_Filtro_Tipo_RA |
| **Pre-Condiciones** | El usuario tiene un filtro de tipo activo |
| **Descripción Caso** | Verificar que el filtro de tipo puede ser limpiado |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Tener un filtro de tipo activo |
| 2 | Ubicar la opción para limpiar el filtro |
| 3 | Ejecutar la limpieza |
| 4 | Observar los resultados |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El filtro de tipo se restablece. Se muestran todos los RA independientemente de su tipo. El selector de tipo vuelve a su estado inicial |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
