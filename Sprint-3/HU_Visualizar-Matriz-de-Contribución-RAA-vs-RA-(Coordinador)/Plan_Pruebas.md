# HU: Visualizar Matriz de Contribución RAA vs RA (Coordinador)

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Matrices - RAA vs RA |
| **Rol** | Coordinador de Carrera |

---

## Escenario 1: Visualizar matriz con datos existentes

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Visualizar_Matriz_Con_Datos |
| **Pre-Condiciones** | El coordinador ha iniciado sesión correctamente. Existen RAA y RA con relaciones establecidas |
| **Descripción Caso** | Verificar que la matriz de contribución se muestra correctamente con las relaciones existentes entre RAA y RA |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe tener rol de Coordinador. Deben existir datos previos de relaciones |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Ingresar al sistema como Coordinador |
| 2 | Acceder al módulo de Matrices |
| 3 | Seleccionar la opción "Matriz RAA vs RA" |
| 4 | Seleccionar una asignatura con relaciones existentes |
| 5 | Esperar a que se cargue la matriz |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La matriz se muestra con los RAA en filas y los RA en columnas (o viceversa). Las celdas con relaciones muestran el nivel de contribución. Los colores o indicadores visuales reflejan el nivel de aporte |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Visualizar matriz sin relaciones

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Visualizar_Matriz_Sin_Relaciones |
| **Pre-Condiciones** | El coordinador ha iniciado sesión correctamente. Existe una asignatura sin relaciones RAA-RA establecidas |
| **Descripción Caso** | Verificar el comportamiento de la matriz cuando no hay relaciones establecidas |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder al módulo de Matrices como Coordinador |
| 2 | Seleccionar una asignatura sin relaciones establecidas |
| 3 | Observar la matriz generada |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | La matriz se muestra vacía o con indicadores de "sin relación". Se muestra un mensaje orientativo para establecer relaciones. Las opciones para crear relaciones están disponibles |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Verificar niveles de contribución en matriz

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Verificar_Niveles_Contribución |
| **Pre-Condiciones** | Existen relaciones con diferentes niveles de contribución (Alto, Medio, Bajo) |
| **Descripción Caso** | Verificar que los diferentes niveles de contribución se muestran correctamente diferenciados en la matriz |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Deben existir relaciones con diferentes niveles de aporte |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la matriz RAA vs RA |
| 2 | Seleccionar una asignatura con múltiples niveles de contribución |
| 3 | Revisar la representación visual de cada nivel |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | Cada nivel de contribución tiene una representación visual distintiva (colores diferentes, iconos, o valores numéricos). Existe una leyenda que explica los niveles. Los niveles son consistentes en toda la matriz |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Exportar o imprimir matriz de contribución

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Alta |
| **Nombre Testing** | CP_Exportar_Matriz_Contribución |
| **Pre-Condiciones** | La matriz está completamente cargada con datos |
| **Descripción Caso** | Verificar que el coordinador puede exportar o imprimir la matriz de contribución |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | La funcionalidad de exportación debe estar implementada |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Visualizar la matriz de contribución |
| 2 | Ubicar la opción de exportar/imprimir |
| 3 | Seleccionar el formato de exportación (PDF, Excel, etc.) |
| 4 | Esperar la generación del archivo |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema genera un archivo en el formato seleccionado. El archivo contiene toda la información de la matriz. El formato es legible y adecuado para documentación |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
