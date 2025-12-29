# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: VISUALIZAR REPORTE ASIGNATURA VS CRITERIOS EURACE**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Baja | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 1 – Estado inicial sin filtros aplicados | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera o CEI | Verificar visualización correcta del estado inicial del reporte sin filtros aplicados | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | En el menú lateral izquierdo, dar clic en "Asignatura vs EURACE" ubicado en la sección "REPORTES" | *Se navega correctamente al reporte<br>*Se muestra el título "Reporte: Asignatura vs Criterios EURACE"<br>*Se presenta la descripción "Visualización detallada de la contribución de asignaturas a los criterios EUR-ACE." | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar los campos de filtros en la parte superior del reporte | *Se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad"<br>*Se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera" en estado deshabilitado<br>*Se muestran los checkboxes "Alto", "Medio", "Bajo" desmarcados en la sección "Nivel de aporte" | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el área de contenido principal del reporte | *No se muestra contenido de matriz<br>*No se muestra mensaje instructivo<br>*El área de contenido principal permanece vacía | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 2 – Seleccionar facultad y habilitar carrera | *El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*El dropdown "Carrera:" debe estar deshabilitado | Verificar habilitación del dropdown Carrera al seleccionar una facultad | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | En el campo "Facultad:" digitar "Sis" | *El texto "Sis" se muestra en el campo<br>*Se despliega una lista con opciones filtradas que contienen "Sis" (Sistemas, Química y Agroindustria) | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Seleccionar la opción "Sistemas" de la lista desplegada | *El campo "Facultad:" se actualiza con el valor "Sistemas"<br>*El dropdown "Carrera:" se habilita<br>*El dropdown "Carrera:" muestra el texto "Seleccionar una carrera" disponible para interacción | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el área de contenido principal | *No se muestra contenido de matriz<br>*El área de contenido principal permanece vacía hasta completar los filtros | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 3 – Seleccionar carrera sin marcar niveles de aporte | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El dropdown "Carrera:" debe estar habilitado | Verificar visualización del mensaje instructivo al seleccionar carrera sin marcar niveles | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Dar clic en el dropdown "Carrera:" | *Se despliega la lista de opciones mostrando "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial" | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Seleccionar "Ingeniería de Software" de las opciones disponibles | *El dropdown "Carrera:" se actualiza con el valor "Ingeniería de Software"<br>*Se muestra el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:" | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el área de la matriz y los checkboxes de nivel de aporte | *No se muestra la matriz con datos<br>*Los checkboxes "Alto", "Medio", "Bajo" permanecen visibles y desmarcados<br>*Es evidente que se requiere marcar al menos un nivel de aporte para visualizar datos | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 4 – Generar matriz completa con todos los filtros aplicados | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El usuario debe tener la carrera "Ingeniería de Software" seleccionada | Verificar generación correcta de la matriz al marcar nivel de aporte Alto | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Marcar el checkbox "Alto" en la sección "Nivel de aporte:" | *El checkbox "Alto" se muestra marcado<br>*Se mantiene el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:" | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar la estructura de la matriz generada | *Se genera la matriz completa con encabezados de columnas EUR-ACE (5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7) en fondo azul oscuro<br>*Se muestra la columna "Asignatura" como primera columna fija<br>*El campo de búsqueda "Buscar por código o nombre de asignatura" se muestra disponible sobre la matriz | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar las filas de asignaturas y sus relaciones | *Se presentan las filas de asignaturas (Álgebra Lineal, Cálculo en una Variable, Mecánica Newtoniana, Programación I, Comunicación Oral y Escrita, Ecuaciones Diferenciales, Matemática Computacional, Fundamentos de Electrónica)<br>*Se muestran checkmarks verdes (✓) en las intersecciones donde existe relación entre asignatura y criterio EUR-ACE<br>*Las celdas vacías indican ausencia de relación | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 5 – Visualizar matriz con múltiples niveles de aporte | *El usuario debe tener la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas<br>*El usuario debe tener al menos un nivel de aporte marcado | Verificar actualización dinámica de la matriz al seleccionar múltiples niveles de aporte | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Marcar adicionalmente los checkboxes "Medio" y "Bajo" en "Nivel de aporte:" | *Los checkboxes "Alto", "Medio" y "Bajo" se muestran marcados simultáneamente<br>*La matriz se actualiza automáticamente sin recargar la página | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar los cambios en la matriz | *Se muestran todas las relaciones de los tres niveles de aporte en la matriz<br>*Se presentan checkmarks verdes (✓) en todas las intersecciones que corresponden a cualquiera de los niveles seleccionados<br>*Se mantiene la estructura de encabezados y columnas<br>*Se incrementa la cantidad de checkmarks verdes visibles respecto a tener un solo nivel marcado<br>*La respuesta visual es inmediata al cambio de filtros | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 6 – Filtrar asignaturas mediante búsqueda | *El usuario debe tener la matriz completa visible con asignaturas y relaciones<br>*Deben existir múltiples asignaturas en la tabla | Verificar filtrado en tiempo real de asignaturas mediante campo de búsqueda | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | En el campo de búsqueda "Buscar por código o nombre de asignatura" digitar "MATD113 Álgebra Lineal" | *El texto "MATD113 Álgebra Lineal" se muestra en el campo de búsqueda<br>*La tabla se filtra automáticamente mostrando únicamente la fila correspondiente a "Álgebra Lineal"<br>*El filtrado ocurre en tiempo real sin necesidad de presionar botón de búsqueda | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar los resultados del filtrado | *Se muestran solo los checkmarks verdes (✓) en las columnas 5.3.4 y 5.3.5 para la asignatura "Álgebra Lineal"<br>*Se mantienen visibles todos los encabezados de columnas EUR-ACE<br>*Las demás filas de asignaturas desaparecen de la vista | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 7 – Navegar a vista de trazabilidad detallada | *El usuario debe tener la matriz completa visible con checkmarks verdes<br>*Debe existir la asignatura "Cálculo en una Variable" con checkmark en la intersección con criterio "5.2.2" | Verificar navegación correcta a la vista de trazabilidad detallada | Reportes - Trazabilidad | Coordinador de Carrera / CEI | Paso1 | Dar clic en la celda con checkmark verde de la intersección entre "Cálculo en una Variable" y criterio "5.2.2" | *Se navega a una nueva vista con título "Trazabilidad de Cálculo en una Variable"<br>*Se muestra el botón "Regresar" en la esquina superior derecha | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar la sección "Nivel de aporte: Alto" | *Se presenta la sección "Nivel de aporte: Alto" con fondo verde/turquesa claro<br>*Se muestra el flujo horizontal de 4 columnas: "R. de Aprendizaje Asignatura", "R. de Aprendizaje", "Justificación RA-EURACE", "Criterio EUR-ACE"<br>*Se presentan flechas direccionales (→) entre las columnas<br>*Se visualizan cards con bordes redondeados conteniendo RAA, RA, justificación y criterio EUR-ACE | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Hacer scroll vertical para observar las demás secciones | *Se muestra la sección "Nivel de aporte: Medio" con fondo amarillo claro<br>*Se muestra la sección "Nivel de aporte: Bajo" con fondo rosa claro<br>*Cada sección mantiene la misma estructura de 4 columnas con flujo completo | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Baja | HU: Visualizar Reporte Asignatura vs Criterios EURACE - Escenario 8 – Regresar de trazabilidad a matriz | *El usuario debe estar en la vista de trazabilidad detallada "Trazabilidad de Cálculo en una Variable"<br>*Debe ser visible el botón "Regresar" en la esquina superior derecha | Verificar retorno correcto a la matriz preservando el estado de los filtros | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Dar clic en el botón "Regresar" ubicado en la esquina superior derecha | *Se navega de regreso a la vista del reporte "Reporte: Asignatura vs Criterios EURACE"<br>*Se mantiene la matriz completa visible con los mismos filtros aplicados (Facultad: Sistemas, Carrera: Ingeniería de Software, Niveles de aporte previamente marcados) | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar el estado de los filtros y la matriz | *Se preserva el estado de los checkboxes de nivel de aporte<br>*Se mantiene visible la búsqueda y todos los checkmarks verdes de la matriz<br>*No se reinician los filtros aplicados | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Visualizar Reporte Asignatura vs Criterios EURACE

**Total de Casos de Prueba**: 8 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 8 casos (100%)

**Distribución por Complejidad**:
- Baja: 2 casos (Escenarios 1, 8)
- Media: 4 casos (Escenarios 2, 3, 5, 6)
- Alta: 2 casos (Escenarios 4, 7)

**Roles Involucrados**: Coordinador de Carrera / CEI

**Módulos a Probar**: 
- Reportes - Asignatura vs EURACE
- Reportes - Trazabilidad

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   - Facultad: "Sistemas"
   - Carrera: "Ingeniería de Software"
   - Asignaturas de prueba: Álgebra Lineal (MATD113), Cálculo en una Variable, Mecánica Newtoniana, Programación I, etc.
   - Relaciones predefinidas entre asignaturas y criterios EUR-ACE para los tres niveles de aporte

2. **Consideraciones Especiales**:
   - Verificar que el Coordinador de Carrera solo pueda ver datos de SU carrera asignada (filtros pre-poblados y bloqueados)
   - Verificar que el CEI pueda cambiar libremente entre facultades y carreras
   - Validar que el filtrado de búsqueda sea en tiempo real sin necesidad de botones adicionales
   - Confirmar que la navegación a trazabilidad y el retorno preserven el estado de los filtros

3. **Defectos Potenciales a Detectar**:
   - Dropdown Carrera habilitado sin seleccionar Facultad
   - Matriz visible sin marcar niveles de aporte
   - Filtros no preservados al regresar de trazabilidad
   - Búsqueda que requiera botón en lugar de ser en tiempo real
   - Colores incorrectos en niveles de aporte de trazabilidad
   - Botón "Regresar" no funcional

4. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Base de datos con información de facultades, carreras, asignaturas, criterios EUR-ACE y sus relaciones
   - Usuarios de prueba con roles Coordinador de Carrera y CEI correctamente configurados