# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: VISUALIZAR REPORTE OBJETIVOS DE CARRERA VS RESULTADOS DE APRENDIZAJE VS ASIGNATURAS**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Baja | HU: Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 1 – Estado inicial sin filtros aplicados | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera o CEI | Verificar visualización correcta del estado inicial del reporte sin filtros aplicados | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera / CEI | Paso1 | En el menú lateral izquierdo, dar clic en "OP vs RA vs Asignatura" ubicado en la sección "REPORTES" | *Se navega correctamente al reporte<br>*Se muestra el título "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas"<br>*Se presenta la descripción "Visualice la alineación entre objetivos, resultados y asignaturas del programa académico." | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar los campos de filtros en la parte superior del reporte | *Se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad"<br>*Se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera" en estado deshabilitado<br>*Se muestran los checkboxes "Alto", "Medio", "Bajo" desmarcados en la sección "Nivel de aporte" | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el área de contenido principal del reporte | *No se muestran los encabezados de tabla<br>*No se muestra contenido de trazabilidad<br>*El área de contenido principal permanece vacía | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 2 – Seleccionar facultad y habilitar carrera | *El usuario debe estar en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas"<br>*El dropdown "Carrera:" debe estar deshabilitado | Verificar habilitación del dropdown Carrera al seleccionar una facultad | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera / CEI | Paso1 | En el campo "Facultad:" escribir el texto necesario para filtrar y seleccionar "Sistemas" de las opciones desplegadas | *El campo "Facultad:" se actualiza con el valor "Sistemas"<br>*El dropdown "Carrera:" se habilita<br>*El dropdown "Carrera:" muestra el texto "Seleccionar una carrera" disponible para interacción | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el área de contenido principal | *No se muestra contenido de tabla<br>*El área de contenido principal permanece vacía hasta completar los filtros | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 3 – Seleccionar carrera sin marcar niveles de aporte | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El dropdown "Carrera:" debe estar habilitado | Verificar que no se muestra tabla al seleccionar carrera sin marcar niveles de aporte | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera / CEI | Paso1 | Dar clic en el dropdown "Carrera:" y seleccionar "Software" de las opciones disponibles | *El dropdown "Carrera:" se actualiza con el valor "Software" | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el área de contenido y los checkboxes de nivel de aporte | *No se muestra la tabla con datos<br>*Los checkboxes "Alto", "Medio", "Bajo" permanecen visibles y desmarcados<br>*El área de contenido principal permanece vacía<br>*Es evidente que se requiere marcar al menos un nivel de aporte para visualizar datos | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 4 – Generar tabla completa con todos los niveles de aporte | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El usuario debe tener la carrera "Software" seleccionada | Verificar generación correcta de tabla de trazabilidad con todos los niveles de aporte | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera / CEI | Paso1 | Marcar simultáneamente los checkboxes "Alto", "Medio" y "Bajo" en la sección "Nivel de aporte:" | *Los tres checkboxes se muestran marcados<br>*Se genera una tabla de trazabilidad con tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas"<br>*Se presentan múltiples filas de trazabilidad completa | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el contenido de la primera fila de la tabla | *En columna "Objetivos de carrera" se muestra el texto "OPP1: Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de software innovadores y eficientes, aplicando metodologías ágiles y estándares de calidad internacional."<br>*En columna "Resultados de Aprendizaje" se muestran con viñetas: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos.", "RE4: Diseña arquitecturas de software escalables y de alto rendimiento."<br>*En columna "Asignaturas" se muestran: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web", "MA-102: Álgebra Lineal", "IS-203: Bases de Datos" | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el contenido de las demás filas de la tabla | *Se presenta una segunda fila con OPP2 incluyendo RG1, RG3, RG4 y asignaturas GE-401, HU-301, IS-306<br>*Se presenta una tercera fila con OPP3 incluyendo RE1, RE2, RE3 y asignaturas IS-501, IS-402, MA-201<br>*Se presenta una cuarta fila con OPP5 incluyendo RG1, RG2, RE1 y asignaturas CO-101, HU-301, IS-403 | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Verificar la calidad general del contenido de la tabla | *Cada celda muestra el contenido completo y legible<br>*La tabla presenta la trazabilidad completa desde objetivos hasta asignaturas específicas | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 5 – Filtrar tabla por nivel de aporte específico | *El usuario debe tener la facultad "Sistemas" y carrera "Software" seleccionadas<br>*Los checkboxes de nivel de aporte deben estar desmarcados | Verificar filtrado correcto de tabla al seleccionar únicamente nivel de aporte Alto | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera / CEI | Paso1 | Marcar únicamente el checkbox "Alto" en "Nivel de aporte:" | *El checkbox "Alto" se muestra marcado<br>*Se genera una tabla de trazabilidad con las tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas"<br>*La tabla se actualiza automáticamente sin recargar la página | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el contenido filtrado de la primera fila | *Se muestra OPP1 con texto completo "Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de software innovadores y eficientes, aplicando metodologías ágiles y estándares de calidad internacional."<br>*En "Resultados de Aprendizaje" se muestran únicamente: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos." (sin RE4)<br>*En "Asignaturas" se muestran únicamente: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web" (sin MA-102 ni IS-203) | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el contenido filtrado de la segunda fila y verificar el comportamiento general | *La segunda fila muestra OPP2 con RG1, RG3 (sin RG4) y asignatura GE-401 únicamente<br>*Se ocultan los objetivos, resultados y asignaturas que corresponden exclusivamente a niveles medio y bajo<br>*El contenido mostrado es un subconjunto del contenido cuando todos los niveles están marcados | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas

**Total de Casos de Prueba**: 5 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 5 casos (100%)

**Distribución por Complejidad**:
- Baja: 1 caso (Escenario 1)
- Media: 2 casos (Escenarios 2, 3)
- Alta: 2 casos (Escenarios 4, 5)

**Roles Involucrados**: Coordinador de Carrera / CEI

**Módulos a Probar**: 
- Reportes - OP vs RA vs Asignatura

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   - Facultad: "Sistemas"
   - Carrera: "Software" (nombre corto de "Ingeniería de Software")
   - Objetivos de Carrera (OPP): OPP1, OPP2, OPP3, OPP5 con textos completos
   - Resultados de Aprendizaje (RG/RE): RG1, RG2, RG3, RG4, RE1, RE2, RE3, RE4
   - Asignaturas con códigos específicos: IS-101, IS-305, MA-102, IS-203, GE-401, HU-301, IS-306, IS-501, IS-402, MA-201, CO-101, IS-403
   - Relaciones predefinidas entre OPP → RA → Asignaturas para los tres niveles de aporte

2. **Consideraciones Especiales**:
   - Verificar que la tabla muestre estructura de tres columnas claramente delimitadas
   - Validar que los Resultados de Aprendizaje se presenten con viñetas/bullets
   - Confirmar que el filtrado por nivel de aporte funcione como subconjunto (nivel Alto debe mostrar menos datos que todos los niveles)
   - Verificar que la actualización sea automática sin necesidad de botón "Aplicar" o recarga de página
   - Validar que el Coordinador de Carrera solo vea datos de SU carrera (filtros pre-poblados)
   - Validar que el CEI pueda cambiar libremente entre facultades y carreras

3. **Defectos Potenciales a Detectar**:
   - Dropdown Carrera habilitado sin seleccionar Facultad
   - Tabla visible sin marcar niveles de aporte
   - Contenido de tabla idéntico entre nivel "Alto" solo vs "Todos los niveles" (debería ser subconjunto)
   - Resultados de Aprendizaje sin formato de viñetas/bullets
   - Códigos de asignaturas incorrectos o inconsistentes
   - Relaciones OPP-RA-Asignaturas incorrectas o incompletas
   - Actualización que requiere recarga de página
   - Contenido truncado o ilegible en celdas
   - Desalineación de columnas

4. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Base de datos con información completa de:
     - Objetivos de Carrera (OPP) por programa académico
     - Resultados de Aprendizaje (RA) de la carrera
     - Asignaturas con códigos y nombres
     - Relaciones de trazabilidad OPP → RA → Asignaturas clasificadas por nivel de aporte
   - Usuarios de prueba con roles Coordinador de Carrera y CEI correctamente configurados

5. **Validaciones Críticas de Contenido**:
   - **OPP1** debe incluir: RG1, RG3, RE4 en nivel Alto; datos adicionales en Medio/Bajo
   - **OPP2** debe incluir: RG1, RG3 en nivel Alto (sin RG4); RG4 solo en Medio/Bajo
   - **OPP3** debe incluir: RE1, RE2, RE3
   - **OPP5** debe incluir: RG1, RG2, RE1
   - Validar que asignaturas específicas correspondan a cada OPP según se especifica

6. **Comparación Entre Escenarios**:
   - **Escenario 4** (todos los niveles): Debe mostrar TODAS las relaciones
   - **Escenario 5** (solo Alto): Debe mostrar SUBCONJUNTO de Escenario 4
   - Verificar que Escenario 5 NO muestre datos exclusivos de nivel Medio/Bajo

7. **Dependencias**:
   - Esta HU es independiente de las HUs previas de reportes
   - Sin embargo, comparte la misma estructura de filtros (Facultad, Carrera, Nivel de aporte)
   - La lógica de habilitación/filtrado debe ser consistente con el reporte "Asignatura vs Criterios EURACE"

8. **Criterios de Éxito**:
   - Tabla de tres columnas claramente estructurada
   - Contenido completo y legible en todas las celdas
   - Trazabilidad clara desde OPP hasta asignaturas específicas
   - Filtrado por nivel de aporte funcional y preciso
   - Actualización reactiva sin recargas
   - Datos correctos según nivel de aporte seleccionado