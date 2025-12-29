# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: FILTRAR REPORTE ASIGNATURA VS CRITERIOS EURACE POR NIVEL DE APORTE**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Media | HU: Filtrar Reporte Asignatura vs Criterios EURACE por Nivel de Aporte - Escenario 1 – Deseleccionar todos los niveles de aporte | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera<br>*El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*Debe tener la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas | Verificar comportamiento correcto al deseleccionar todos los checkboxes de nivel de aporte | Reportes - Asignatura vs EURACE | Coordinador de Carrera | Paso1 | Desmarcar todos los checkboxes de "Nivel de aporte:" (Alto, Medio y Bajo deben quedar sin seleccionar) | *Todos los checkboxes se muestran desmarcados<br>*Se mantiene visible el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:" | ESTADO PRUEBA | | Negativo | Funcional | |
| | | | | | | | | | Paso2 | Observar el área de contenido principal del reporte | *No se muestra la matriz con datos<br>*No se muestran encabezados de columnas EUR-ACE<br>*No se presentan filas de asignaturas<br>*No aparecen checkmarks verdes en ninguna intersección<br>*El área de contenido principal debajo de los filtros permanece vacía | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar disponibilidad de los checkboxes | *Los checkboxes permanecen visibles y disponibles para nueva selección<br>*Es evidente que no hay contenido mostrado por ausencia de filtros de nivel | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Asignatura vs Criterios EURACE por Nivel de Aporte - Escenario 2 – Filtrar por nivel "Alto" únicamente | *El usuario debe tener el reporte visible con facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas<br>*Los checkboxes de nivel de aporte deben estar desmarcados | Verificar visualización correcta de la matriz con únicamente relaciones de nivel Alto | Reportes - Asignatura vs EURACE | Coordinador de Carrera | Paso1 | Marcar únicamente el checkbox "Alto" en "Nivel de aporte:" | *El checkbox "Alto" se muestra marcado<br>*Se mantiene el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:"<br>*Se genera la matriz completa con encabezados de columnas EUR-ACE (5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7) en fondo azul oscuro<br>*La matriz se actualiza sin recargar la página<br>*La respuesta visual es inmediata al marcar el checkbox | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar las filas de asignaturas presentadas | *Se presentan las filas de asignaturas (Álgebra Lineal, Cálculo en una Variable, Mecánica Newtoniana, Programación I, Comunicación Oral y Escrita, Ecuaciones Diferenciales, Matemática Computacional, Fundamentos de Electrónica) | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar los checkmarks verdes específicos mostrados en la matriz | *Se muestran únicamente los checkmarks verdes (✓) correspondientes a relaciones de nivel de aporte alto<br>*Se muestran checkmarks en: Álgebra Lineal (5.3.4, 5.3.5), Cálculo en una Variable (5.2.2, 5.2.4, 5.3.3), Mecánica Newtoniana (5.2.5, 5.3.1, 5.3.2), Programación I (5.2.5)<br>*Se ocultan todas las relaciones de nivel medio y bajo | ESTADO PRUEBA | Debe validarse la ubicación exacta de cada checkmark | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Asignatura vs Criterios EURACE por Nivel de Aporte - Escenario 3 – Visualizar todos los niveles de aporte | *El usuario debe tener el reporte visible con facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas | Verificar visualización completa de matriz con todos los niveles de aporte combinados | Reportes - Asignatura vs EURACE | Coordinador de Carrera | Paso1 | Marcar todos los checkboxes "Alto", "Medio" y "Bajo" en "Nivel de aporte:" | *Los tres checkboxes se muestran marcados<br>*Se genera la matriz completa con encabezados de columnas EUR-ACE<br>*Se presentan todas las filas de asignaturas<br>*La matriz se actualiza automáticamente sin recargar la página | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar todos los checkmarks verdes mostrados | *Se muestran todos los checkmarks verdes (✓) de los tres niveles de aporte combinados<br>*La densidad de checkmarks verdes en la matriz es mayor que con solo un nivel seleccionado | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar checkmarks adicionales comparado con solo nivel "Alto" | *Se visualizan relaciones adicionales comparado con solo nivel "Alto": Cálculo en una Variable muestra checkmarks adicionales en 5.2.4, 5.3.7; Comunicación Oral y Escrita muestra checkmarks en 5.3.3, 5.3.5; Ecuaciones Diferenciales muestra checkmarks en 5.2.1, 5.2.5, 5.3.2, 5.3.4, 5.3.5<br>*Se presenta una vista panorámica completa de todas las contribuciones de las asignaturas a criterios EUR-ACE independientemente del nivel de intensidad | ESTADO PRUEBA | Comparar con resultado del Escenario 2 | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Asignatura vs Criterios EURACE por Nivel de Aporte - Escenario 4 – Cambiar filtros de nivel dinámicamente | *El usuario debe tener la matriz visible con todos los niveles de aporte marcados (Alto, Medio, Bajo)<br>*Deben ser visibles checkmarks verdes en múltiples intersecciones | Verificar actualización dinámica de matriz al cambiar selección de checkboxes de nivel | Reportes - Asignatura vs EURACE | Coordinador de Carrera | Paso1 | Desmarcar el checkbox "Medio" manteniendo "Alto" y "Bajo" marcados | *El checkbox "Medio" se muestra desmarcado<br>*Los checkboxes "Alto" y "Bajo" permanecen marcados<br>*La matriz se actualiza automáticamente sin recargar la página<br>*Se ocultan los checkmarks verdes correspondientes exclusivamente al nivel medio<br>*Se mantienen visibles los checkmarks de nivel alto y bajo<br>*La respuesta visual es inmediata al cambio de checkbox | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar cambios en la matriz tras desmarcar "Medio" | *La cantidad de checkmarks verdes disminuye en la matriz<br>*La estructura de encabezados y columnas EUR-ACE se mantiene intacta<br>*Las filas de asignaturas permanecen visibles | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Volver a marcar el checkbox "Medio" | *El checkbox "Medio" se muestra marcado nuevamente<br>*Los checkmarks correspondientes al nivel medio reaparecen automáticamente<br>*La matriz restaura la visualización previa sin pérdida de información<br>*La respuesta visual es inmediata | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Filtrar Reporte Asignatura vs Criterios EURACE por Nivel de Aporte

**Total de Casos de Prueba**: 4 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 4 casos (100%)

**Distribución por Complejidad**:
- Media: 1 caso (Escenario 1)
- Alta: 3 casos (Escenarios 2, 3, 4)

**Roles Involucrados**: Coordinador de Carrera

**Módulos a Probar**: 
- Reportes - Asignatura vs EURACE

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: 
- Positivo: 3 casos (Escenarios 2, 3, 4)
- Negativo: 1 caso (Escenario 1)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   - Facultad: "Sistemas"
   - Carrera: "Ingeniería de Software"
   - Asignaturas: Álgebra Lineal, Cálculo en una Variable, Mecánica Newtoniana, Programación I, Comunicación Oral y Escrita, Ecuaciones Diferenciales, Matemática Computacional, Fundamentos de Electrónica
   - Criterios EUR-ACE: 5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7
   - **Relaciones específicas de nivel Alto**:
     - Álgebra Lineal: 5.3.4, 5.3.5
     - Cálculo en una Variable: 5.2.2, 5.2.4, 5.3.3
     - Mecánica Newtoniana: 5.2.5, 5.3.1, 5.3.2
     - Programación I: 5.2.5
   - **Relaciones adicionales para niveles Medio/Bajo** (aparecen cuando todos los niveles están marcados):
     - Cálculo en una Variable: 5.2.4, 5.3.7 (adicionales)
     - Comunicación Oral y Escrita: 5.3.3, 5.3.5
     - Ecuaciones Diferenciales: 5.2.1, 5.2.5, 5.3.2, 5.3.4, 5.3.5

2. **Consideraciones Especiales**:
   - Esta HU se enfoca específicamente en el **filtrado reactivo** de la matriz ya generada
   - Es una funcionalidad **dependiente** de la HU "Visualizar Reporte Asignatura vs Criterios EURACE"
   - Debe validarse la **ubicación exacta** de cada checkmark según el nivel de aporte
   - El comportamiento debe ser **reactivo e inmediato** sin recargas de página
   - Validar que el Coordinador de Carrera solo vea datos de SU carrera (filtros pre-poblados de Facultad y Carrera)

3. **Defectos Potenciales a Detectar**:
   - Matriz visible con todos los checkboxes desmarcados (Escenario 1)
   - Checkmarks incorrectos para nivel Alto (no coinciden con ubicaciones especificadas)
   - Todos los niveles muestran los mismos checkmarks (no hay diferencia entre niveles)
   - Actualización requiere recarga de página (no es reactiva)
   - Checkmarks de nivel Medio no desaparecen al desmarcar ese checkbox
   - Checkmarks no reaparecen al volver a marcar un checkbox
   - Pérdida de información al cambiar filtros dinámicamente
   - Estructura de matriz se rompe al cambiar checkboxes
   - Lag o delay excesivo en la actualización
   - Checkmarks aparecen en ubicaciones incorrectas según nivel

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Todos desmarcados):
   - ✓ Área vacía sin matriz
   - ✓ Mensaje instructivo visible
   - ✓ Checkboxes disponibles
   
   **Escenario 2** (Solo Alto):
   - ✓ Álgebra Lineal: SOLO 5.3.4, 5.3.5
   - ✓ Cálculo en una Variable: SOLO 5.2.2, 5.2.4, 5.3.3
   - ✓ Mecánica Newtoniana: SOLO 5.2.5, 5.3.1, 5.3.2
   - ✓ Programación I: SOLO 5.2.5
   - ✓ NO deben aparecer checkmarks en otras asignaturas para nivel Alto
   
   **Escenario 3** (Todos los niveles):
   - ✓ Incluye TODOS los checkmarks del Escenario 2 MÁS checkmarks adicionales
   - ✓ Cálculo en una Variable: checkmarks adicionales en 5.2.4, 5.3.7
   - ✓ Comunicación Oral y Escrita: checkmarks en 5.3.3, 5.3.5
   - ✓ Ecuaciones Diferenciales: checkmarks en 5.2.1, 5.2.5, 5.3.2, 5.3.4, 5.3.5
   - ✓ Mayor densidad visual de checkmarks
   
   **Escenario 4** (Dinámico):
   - ✓ Desmarcar Medio: checkmarks disminuyen pero estructura permanece
   - ✓ Remarcar Medio: checkmarks reaparecen exactamente igual
   - ✓ Sin pérdida de información
   - ✓ Actualización inmediata

5. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Base de datos con relaciones Asignatura-Criterio clasificadas por nivel de aporte (Alto, Medio, Bajo)
   - Matriz de "Asignatura vs Criterios EURACE" funcional
   - Usuario Coordinador de Carrera con carrera "Ingeniería de Software" asignada
   - JavaScript funcional para actualización reactiva

6. **Orden de Ejecución Recomendado**:
   1. **Escenario 1**: Validar estado vacío (todos desmarcados)
   2. **Escenario 2**: Validar nivel Alto solo (documentar ubicaciones exactas)
   3. **Escenario 3**: Validar todos los niveles (documentar checkmarks adicionales)
   4. **Escenario 4**: Validar cambio dinámico (usar datos de Escenarios 2 y 3 como referencia)

7. **Criterios de Éxito**:
   - Filtrado reactivo sin recargas de página
   - Checkmarks correctos según nivel de aporte seleccionado
   - Diferencias claras entre niveles (Alto ≠ Alto+Medio+Bajo)
   - Comportamiento consistente al marcar/desmarcar dinámicamente
   - Sin pérdida de información al cambiar filtros
   - Estructura de matriz preservada en todos los casos
   - Actualización visual inmediata (< 500ms)

8. **Dependencias con Otras HUs**:
   - **Dependencia CRÍTICA**: HU "Visualizar Reporte Asignatura vs Criterios EURACE"
   - Esta HU NO puede ejecutarse sin que la matriz base esté funcional
   - Los checkboxes de nivel de aporte son el mecanismo de filtrado de la matriz ya generada
   - Se recomienda ejecutar esta HU DESPUÉS de validar completamente la HU de visualización base