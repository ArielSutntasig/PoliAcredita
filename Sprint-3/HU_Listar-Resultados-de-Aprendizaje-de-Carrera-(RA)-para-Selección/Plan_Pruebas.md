# HU: Listar Resultados de Aprendizaje de Carrera (RA) para Selección

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Resultados de Aprendizaje (RA) |
| **Rol** | Profesor |

---

## Escenario 1: Listar RA disponibles para selección

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Listar_RA_Para_Selección |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. Existen RA de carrera registrados en el sistema |
| **Descripción Caso** | Verificar que el sistema muestra correctamente la lista de RA de carrera disponibles para selección |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe estar en un contexto donde se requiera seleccionar RA |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al módulo que requiere selección de RA |
| 2 | Abrir el selector o lista de RA disponibles |
| 3 | Esperar a que se cargue la lista completa |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Se muestra una lista con todos los RA de carrera disponibles. Cada RA muestra su código y descripción. La lista permite la selección de uno o más RA |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Listar RA cuando no hay resultados

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Listar_RA_Sin_Resultados |
| **Pre-Condiciones** | El usuario ha iniciado sesión correctamente. No existen RA de carrera registrados |
| **Descripción Caso** | Verificar el comportamiento del sistema cuando no hay RA disponibles |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al selector de RA |
| 2 | Observar el estado de la lista |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra un mensaje indicando que no hay RA disponibles. Se sugiere contactar al administrador o crear RA si tiene permisos |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Verificar información mostrada de cada RA

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Verificar_Información_RA |
| **Pre-Condiciones** | Existen RA con información completa |
| **Descripción Caso** | Verificar que cada RA en la lista muestra la información necesaria para su selección |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de RA para selección |
| 2 | Revisar la información mostrada para cada RA |
| 3 | Verificar que se muestran todos los campos relevantes |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Cada RA muestra: código identificador, descripción completa del resultado de aprendizaje, tipo de RA (si aplica). La información es suficiente para tomar una decisión de selección |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Seleccionar múltiples RA de la lista

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Seleccionar_Múltiples_RA |
| **Pre-Condiciones** | Existen múltiples RA disponibles. El sistema permite selección múltiple |
| **Descripción Caso** | Verificar que el usuario puede seleccionar múltiples RA de la lista |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | La funcionalidad debe permitir selección múltiple |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la lista de RA |
| 2 | Seleccionar el primer RA |
| 3 | Seleccionar uno o más RA adicionales |
| 4 | Confirmar la selección |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema permite seleccionar múltiples RA simultáneamente. Las selecciones son visualmente indicadas. Se puede confirmar la selección múltiple |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
