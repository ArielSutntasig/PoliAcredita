# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: FILTRAR REPORTE OBJETIVOS DE CARRERA VS RESULTADOS DE APRENDIZAJE VS ASIGNATURAS POR NIVEL DE APORTE**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Media | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas por Nivel de Aporte - Escenario 1 – Deseleccionar todos los niveles de aporte | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera<br>*El usuario debe estar en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas"<br>*Debe tener la facultad "Sistemas" y carrera "Software" seleccionadas | Verificar comportamiento correcto al deseleccionar todos los checkboxes de nivel de aporte | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Desmarcar todos los checkboxes de "Nivel de aporte:" (Alto, Medio y Bajo deben quedar sin seleccionar) | *Todos los checkboxes se muestran desmarcados<br>*No se muestran los encabezados de tabla ("Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas")<br>*No se presenta ninguna fila de trazabilidad | ESTADO PRUEBA | | Negativo | Funcional | |
| | | | | | | | | | Paso2 | Observar el área de contenido principal del reporte | *No se visualiza contenido de objetivos de programa<br>*No se muestran resultados de aprendizaje<br>*No aparecen códigos ni nombres de asignaturas<br>*El área de contenido principal debajo de los filtros permanece vacía | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar disponibilidad de los checkboxes | *Los checkboxes permanecen visibles y disponibles para nueva selección<br>*Queda claro que no se muestran datos por ausencia de filtros de nivel | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas por Nivel de Aporte - Escenario 2 – Filtrar por nivel "Alto" únicamente | *El usuario debe tener el reporte visible con facultad "Sistemas" y carrera "Software" seleccionadas<br>*Los checkboxes de nivel de aporte deben estar desmarcados | Verificar visualización correcta de tabla con únicamente relaciones de nivel Alto | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Marcar únicamente el checkbox "Alto" en "Nivel de aporte:" | *El checkbox "Alto" se muestra marcado<br>*Se genera una tabla de trazabilidad con tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas"<br>*Se muestran únicamente las filas correspondientes al nivel de aporte alto<br>*La tabla se actualiza sin recargar la página<br>*La respuesta visual es inmediata al marcar el checkbox | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el contenido de la primera fila de la tabla | *Se presenta la primera fila con OPP1: "Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de software innovadores y eficientes, aplicando metodologías ágiles y estándares de calidad internacional."<br>*En columna "Resultados de Aprendizaje" se muestran únicamente: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos." (sin RE4)<br>*En columna "Asignaturas" se muestran únicamente: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web" (sin MA-102 ni IS-203) | ESTADO PRUEBA | No debe aparecer RE4, MA-102 ni IS-203 en esta fila | | | |
| | | | | | | | | | Paso3 | Observar el contenido de la segunda fila y verificar ausencia de OPP3 y OPP5 | *Se presenta la segunda fila con OPP2 incluyendo RG1 y RG3 (sin RG4) y únicamente asignatura GE-401 (sin HU-301 ni IS-306)<br>*No se muestran las filas correspondientes a OPP3 ni OPP5<br>*Se ocultan todas las relaciones de nivel medio y bajo | ESTADO PRUEBA | Solo deben aparecer 2 filas: OPP1 y OPP2 | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas por Nivel de Aporte - Escenario 3 – Visualizar todos los niveles de aporte | *El usuario debe tener el reporte visible con facultad "Sistemas" y carrera "Software" seleccionadas | Verificar visualización completa de tabla con todos los niveles de aporte combinados | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Marcar todos los checkboxes "Alto", "Medio" y "Bajo" en "Nivel de aporte:" | *Los tres checkboxes se muestran marcados<br>*Se genera una tabla de trazabilidad completa con las tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas"<br>*La tabla se actualiza automáticamente sin recargar la página | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el contenido expandido de la primera fila | *La primera fila presenta OPP1 expandido con resultados: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos.", "RE4: Diseña arquitecturas de software escalables y de alto rendimiento." (3 resultados)<br>*En columna "Asignaturas" se muestran: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web", "MA-102: Álgebra Lineal", "IS-203: Bases de Datos" (4 asignaturas) | ESTADO PRUEBA | Comparar con Escenario 2: ahora incluye RE4, MA-102 e IS-203 | | | |
| | | | | | | | | | Paso3 | Observar el contenido de las demás filas | *La segunda fila presenta OPP2 expandido con RG1, RG3 y RG4 (3 resultados) y asignaturas GE-401, HU-301, IS-306 (3 asignaturas)<br>*Se presenta la tercera fila con OPP3: "Desarrollar habilidades críticas para la investigación y la adaptación continua a las nuevas tendencias y tecnologías en el ámbito de la ingeniería de software." con resultados RE1, RE2, RE3 y asignaturas IS-501, IS-402, MA-201<br>*Se presenta la cuarta fila con OPP5: "Fomentar la ética profesional, el compromiso social y la comunicación efectiva para interactuar en diversos contextos profesionales y comunitarios." con resultados RG1, RG2, RE1 y asignaturas CO-101, HU-301, IS-403 | ESTADO PRUEBA | Deben aparecer 4 filas en total | | | |
| | | | | | | | | | Paso4 | Verificar la completitud del contenido | *Se visualizan todas las relaciones independientemente del nivel de intensidad<br>*La cantidad de filas y contenido por fila es mayor comparado con solo nivel "Alto" | ESTADO PRUEBA | 4 filas vs 2 filas del Escenario 2 | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas por Nivel de Aporte - Escenario 4 – Cambiar filtros de nivel dinámicamente | *El usuario debe tener la tabla visible con solo el checkbox "Alto" marcado<br>*Deben ser visibles 2 filas con OPP1 y OPP2 con contenido parcial | Verificar expansión y contracción dinámica de filas al cambiar checkboxes de nivel | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Marcar los checkboxes "Medio" y "Bajo" adicionales manteniendo "Alto" marcado | *Los tres checkboxes se muestran marcados<br>*La tabla se actualiza automáticamente sin recargar la página<br>*La respuesta visual es inmediata al cambio de checkboxes | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar la expansión de las filas existentes OPP1 y OPP2 | *La fila de OPP1 se expande mostrando RE4 adicional en resultados de aprendizaje<br>*La fila de OPP1 muestra asignaturas adicionales MA-102 e IS-203<br>*La fila de OPP2 se expande mostrando RG4 adicional y asignaturas HU-301 e IS-306 | ESTADO PRUEBA | Comparar con contenido antes de marcar Medio y Bajo | | | |
| | | | | | | | | | Paso3 | Observar la aparición de nuevas filas | *Aparecen las filas nuevas de OPP3 y OPP5 que antes no estaban visibles<br>*La estructura de encabezados y columnas se mantiene intacta | ESTADO PRUEBA | Total de filas pasa de 2 a 4 | | | |
| | | | | | | | | | Paso4 | Desmarcar "Medio" y "Bajo" dejando solo "Alto" marcado | *La tabla retorna al estado anterior mostrando únicamente 2 filas con contenido reducido<br>*Los cambios ocurren sin pérdida de información ni necesidad de recargar<br>*La respuesta visual es inmediata | ESTADO PRUEBA | Debe volver exactamente al estado del Paso1 | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas por Nivel de Aporte

**Total de Casos de Prueba**: 4 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 4 casos (100%)

**Distribución por Complejidad**:
- Media: 1 caso (Escenario 1)
- Alta: 3 casos (Escenarios 2, 3, 4)

**Roles Involucrados**: Coordinador de Carrera

**Módulos a Probar**: 
- Reportes - OP vs RA vs Asignatura

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: 
- Positivo: 3 casos (Escenarios 2, 3, 4)
- Negativo: 1 caso (Escenario 1)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   - Facultad: "Sistemas"
   - Carrera: "Software"
   
   **Contenido específico por nivel:**
   
   **Nivel Alto (2 filas):**
   - **OPP1**: "Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de software innovadores y eficientes, aplicando metodologías ágiles y estándares de calidad internacional."
     - RA: RG1, RG3 (NO incluye RE4)
     - Asignaturas: IS-101, IS-305 (NO incluye MA-102, IS-203)
   - **OPP2**: 
     - RA: RG1, RG3 (NO incluye RG4)
     - Asignaturas: GE-401 (NO incluye HU-301, IS-306)
   - **NO aparecen**: OPP3, OPP5
   
   **Todos los niveles (4 filas):**
   - **OPP1**: [Texto completo]
     - RA: RG1, RG3, RE4 (3 resultados)
     - Asignaturas: IS-101, IS-305, MA-102, IS-203 (4 asignaturas)
   - **OPP2**:
     - RA: RG1, RG3, RG4 (3 resultados)
     - Asignaturas: GE-401, HU-301, IS-306 (3 asignaturas)
   - **OPP3**: "Desarrollar habilidades críticas para la investigación y la adaptación continua a las nuevas tendencias y tecnologías en el ámbito de la ingeniería de software."
     - RA: RE1, RE2, RE3
     - Asignaturas: IS-501, IS-402, MA-201
   - **OPP5**: "Fomentar la ética profesional, el compromiso social y la comunicación efectiva para interactuar en diversos contextos profesionales y comunitarios."
     - RA: RG1, RG2, RE1
     - Asignaturas: CO-101, HU-301, IS-403

2. **Consideraciones Especiales**:
   - Esta HU se enfoca en el **filtrado reactivo** de la tabla de tres columnas ya generada
   - Es una funcionalidad **dependiente** de la HU "Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas"
   - A diferencia del reporte matricial, aquí las filas completas aparecen/desaparecen y se expanden/contraen
   - El nivel Alto muestra un **subconjunto** del contenido total (2 filas vs 4 filas)
   - Debe validarse la **expansión/contracción** de filas existentes (OPP1, OPP2)
   - Debe validarse la **aparición/desaparición** de filas completas (OPP3, OPP5)

3. **Defectos Potenciales a Detectar**:
   - Tabla visible con todos los checkboxes desmarcados (Escenario 1)
   - Contenido idéntico entre nivel Alto y todos los niveles (no hay diferenciación)
   - Aparecen OPP3 y OPP5 en nivel Alto (deberían solo aparecer con Medio/Bajo)
   - Aparece RE4 en OPP1 con solo nivel Alto (no debería)
   - Aparecen MA-102, IS-203 en OPP1 con solo nivel Alto (no deberían)
   - Aparecen RG4, HU-301, IS-306 en OPP2 con solo nivel Alto (no deberían)
   - Actualización requiere recarga de página (no es reactiva)
   - Filas no se expanden al agregar niveles Medio/Bajo
   - Filas no se contraen al quitar niveles Medio/Bajo
   - Pérdida de información al cambiar filtros dinámicamente
   - Estructura de tabla se rompe al cambiar checkboxes

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Todos desmarcados):
   - ✓ Área completamente vacía
   - ✓ Sin encabezados de tabla
   - ✓ Sin filas
   - ✓ Checkboxes disponibles
   
   **Escenario 2** (Solo Alto):
   - ✓ SOLO 2 filas: OPP1 y OPP2
   - ✓ OPP1: SOLO RG1, RG3 (sin RE4)
   - ✓ OPP1: SOLO IS-101, IS-305 (sin MA-102, IS-203)
   - ✓ OPP2: SOLO RG1, RG3 (sin RG4)
   - ✓ OPP2: SOLO GE-401 (sin HU-301, IS-306)
   - ✓ NO deben aparecer OPP3 ni OPP5
   
   **Escenario 3** (Todos los niveles):
   - ✓ 4 filas totales: OPP1, OPP2, OPP3, OPP5
   - ✓ OPP1: RG1, RG3, RE4 (incluye RE4 adicional)
   - ✓ OPP1: IS-101, IS-305, MA-102, IS-203 (incluye MA-102, IS-203 adicionales)
   - ✓ OPP2: RG1, RG3, RG4 (incluye RG4 adicional)
   - ✓ OPP2: GE-401, HU-301, IS-306 (incluye HU-301, IS-306 adicionales)
   - ✓ OPP3 completo: RE1, RE2, RE3 + IS-501, IS-402, MA-201
   - ✓ OPP5 completo: RG1, RG2, RE1 + CO-101, HU-301, IS-403
   
   **Escenario 4** (Dinámico):
   - ✓ Estado inicial: 2 filas (Alto solo)
   - ✓ Al agregar Medio+Bajo: 4 filas (expansión + nuevas filas)
   - ✓ Al quitar Medio+Bajo: regresa a 2 filas (contracción + desaparición)
   - ✓ Sin pérdida de información
   - ✓ Actualización inmediata

5. **Comparación Entre Escenarios (CRÍTICO)**:

   | Aspecto | Escenario 2 (Alto) | Escenario 3 (Todos) | Diferencia |
   |---------|-------------------|---------------------|------------|
   | **Número de filas** | 2 (OPP1, OPP2) | 4 (OPP1, OPP2, OPP3, OPP5) | +2 filas nuevas |
   | **OPP1 - RA** | RG1, RG3 | RG1, RG3, RE4 | +RE4 |
   | **OPP1 - Asig** | IS-101, IS-305 | IS-101, IS-305, MA-102, IS-203 | +MA-102, IS-203 |
   | **OPP2 - RA** | RG1, RG3 | RG1, RG3, RG4 | +RG4 |
   | **OPP2 - Asig** | GE-401 | GE-401, HU-301, IS-306 | +HU-301, IS-306 |

6. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Base de datos con relaciones OPP-RA-Asignaturas clasificadas por nivel de aporte (Alto, Medio, Bajo)
   - Tabla de "OP vs RA vs Asignatura" funcional
   - Usuario Coordinador de Carrera con carrera "Software" asignada
   - JavaScript funcional para actualización reactiva de tabla

7. **Orden de Ejecución Recomendado**:
   1. **Escenario 1**: Validar estado vacío (documentar que NO aparece nada)
   2. **Escenario 2**: Validar nivel Alto solo (documentar 2 filas con contenido específico)
   3. **Escenario 3**: Validar todos los niveles (documentar 4 filas con contenido completo)
   4. **Escenario 4**: Validar cambio dinámico (usar datos de Escenarios 2 y 3 como referencia de estados)

8. **Criterios de Éxito**:
   - Diferenciación clara entre nivel Alto (2 filas) y todos los niveles (4 filas)
   - Expansión/contracción correcta de filas OPP1 y OPP2
   - Aparición/desaparición correcta de filas OPP3 y OPP5
   - Contenido específico correcto según nivel de aporte
   - Actualización reactiva sin recargas
   - Sin pérdida de información al cambiar filtros
   - Cambios visuales inmediatos (< 500ms)

9. **Dependencias con Otras HUs**:
   - **Dependencia CRÍTICA**: HU "Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas"
   - Esta HU NO puede ejecutarse sin que la tabla base esté funcional
   - Se recomienda ejecutar DESPUÉS de validar la HU de visualización base