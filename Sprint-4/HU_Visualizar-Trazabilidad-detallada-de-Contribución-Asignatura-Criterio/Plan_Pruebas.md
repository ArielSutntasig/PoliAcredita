# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: VISUALIZAR TRAZABILIDAD DETALLADA DE CONTRIBUCIÓN ASIGNATURA-CRITERIO**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Alta | HU: Visualizar Trazabilidad detallada de Contribución Asignatura-Criterio - Escenario 1 – Acceder a vista de trazabilidad desde matriz | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera o CEI<br>*El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*Debe existir la matriz visible con asignaturas y checkmarks verdes | Verificar navegación correcta a la vista de trazabilidad al hacer clic en checkmark verde | Reportes - Trazabilidad | Coordinador de Carrera / CEI | Paso1 | En la matriz, dar clic en la celda con checkmark verde ubicada en la intersección de "Cálculo en una Variable" con criterio "5.2.2" | *Se navega a una nueva vista de trazabilidad<br>*Se muestra el título "Trazabilidad de Cálculo en una Variable" en la parte superior<br>*Se presenta el botón "Regresar" en la esquina superior derecha | ESTADO PRUEBA | El checkmark debe existir en esa intersección específica | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el contenido de la vista de trazabilidad | *Se carga el contenido de trazabilidad completo de la asignatura<br>*La vista es scrollable verticalmente para visualizar todas las secciones | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Trazabilidad detallada de Contribución Asignatura-Criterio - Escenario 2 – Visualizar trazabilidad completa con los tres niveles de aporte | *El usuario debe haber navegado a la vista de trazabilidad de una asignatura<br>*La vista de trazabilidad debe estar completamente cargada | Verificar visualización correcta de las tres secciones de nivel de aporte con sus colores distintivos | Reportes - Trazabilidad | Coordinador de Carrera / CEI | Paso1 | Observar la primera sección visible en la vista de trazabilidad | *Se muestra la sección "Nivel de aporte: Alto" con fondo verde/turquesa claro<br>*El código de color es distintivo y visible | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Hacer scroll vertical hacia abajo para visualizar las demás secciones | *Se muestra la sección "Nivel de aporte: Medio" con fondo amarillo claro<br>*Se muestra la sección "Nivel de aporte: Bajo" con fondo rosa claro<br>*Cada sección mantiene su código de color distintivo | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar el orden de presentación de las secciones | *Las secciones se presentan en orden: Alto, Medio, Bajo de arriba hacia abajo<br>*Todas las secciones son visibles mediante scroll vertical | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Visualizar Trazabilidad detallada de Contribución Asignatura-Criterio - Escenario 3 – Visualizar flujo completo de trazabilidad por nivel | *El usuario debe estar en la vista de trazabilidad<br>*Debe ser visible al menos una sección de nivel de aporte (Alto, Medio o Bajo) | Verificar estructura correcta del flujo de trazabilidad con cuatro columnas y contenido completo | Reportes - Trazabilidad | Coordinador de Carrera / CEI | Paso1 | Revisar el contenido de una sección de nivel de aporte | *Se presentan cuatro columnas horizontales con los encabezados: "R. de Aprendizaje Asignatura", "R. de Aprendizaje", "Justificación RA-EURACE", "Criterio EUR-ACE"<br>*Se muestran flechas direccionales (→) entre cada columna indicando el flujo de trazabilidad | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el contenido de la primera columna "R. de Aprendizaje Asignatura" | *Contiene cards con código RAA (ej: "RAA 1.2: De conocimiento")<br>*Muestra descripción completa del resultado de aprendizaje de la asignatura<br>*Las cards tienen bordes redondeados | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el contenido de la segunda columna "R. de Aprendizaje" | *Contiene cards con código RA (ej: "RA1:")<br>*Muestra texto completo del resultado de aprendizaje de la carrera<br>*Las cards tienen bordes redondeados | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Observar el contenido de la tercera columna "Justificación RA-EURACE" | *Contiene cards con título de relación (ej: "RA1 - Criterio 5.2.1")<br>*Muestra texto de justificación académica explicando la conexión<br>*Las cards tienen bordes redondeados | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso5 | Observar el contenido de la cuarta columna "Criterio EUR-ACE" | *Contiene cards con código y nombre del criterio (ej: "Criterio 5.2.1: Conocimiento y Comprensión")<br>*Muestra descripción de la capacidad requerida<br>*Las cards tienen bordes redondeados<br>*El flujo es legible de izquierda a derecha siguiendo las flechas | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Trazabilidad detallada de Contribución Asignatura-Criterio - Escenario 4 – Verificar contenido específico de cada nivel | *El usuario debe estar visualizando la vista de trazabilidad completa<br>*Deben ser visibles las tres secciones de nivel de aporte mediante scroll | Verificar contenido específico y correcto de cada nivel de aporte sin solapamientos | Reportes - Trazabilidad | Coordinador de Carrera / CEI | Paso1 | Analizar el contenido de la sección "Nivel de aporte: Alto" | *Se muestran las relaciones RAA-RA-Justificación-Criterio EUR-ACE correspondientes al aporte alto<br>*Cada card muestra información completa y legible<br>*Puede contener múltiples cards de RAA si la asignatura tiene varios resultados de aprendizaje | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Hacer scroll y analizar el contenido de la sección "Nivel de aporte: Medio" | *Se muestran las relaciones correspondientes al aporte medio<br>*Cada card muestra información completa y legible<br>*Puede contener múltiples cards de RAA si aplica | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Hacer scroll y analizar el contenido de la sección "Nivel de aporte: Bajo" | *Se muestran las relaciones correspondientes al aporte bajo<br>*Cada card muestra información completa y legible<br>*Puede contener múltiples cards de RAA si aplica | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Verificar la calidad general del contenido en todas las secciones | *No hay solapamiento entre contenidos de diferentes niveles<br>*La información es comprensible para evaluación académica<br>*Todas las cards son legibles y bien formateadas | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar Trazabilidad detallada de Contribución Asignatura-Criterio - Escenario 5 – Regresar a matriz desde trazabilidad | *El usuario debe estar en la vista "Trazabilidad de Cálculo en una Variable"<br>*Debe ser visible el botón "Regresar" en la esquina superior derecha<br>*El usuario debe haber accedido desde la matriz con filtros específicos aplicados | Verificar retorno correcto a la matriz preservando todos los filtros y el contexto de navegación | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Dar clic en el botón "Regresar" ubicado en la esquina superior derecha | *Se navega de regreso a la vista "Reporte: Asignatura vs Criterios EURACE"<br>*Se mantiene visible la matriz completa con los mismos filtros aplicados antes de acceder a la trazabilidad | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar el estado de los filtros de Facultad y Carrera | *Se preserva el estado de selección de Facultad (ej: "Sistemas")<br>*Se preserva el estado de selección de Carrera (ej: "Ingeniería de Software") | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar el estado de los checkboxes de Nivel de aporte y la matriz | *Se mantienen marcados los checkboxes de "Nivel de aporte" que estaban activos<br>*La matriz muestra los mismos checkmarks verdes de relaciones<br>*No se reinician los filtros ni se pierde el contexto de navegación | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Visualizar Trazabilidad detallada de Contribución Asignatura-Criterio

**Total de Casos de Prueba**: 5 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 5 casos (100%)

**Distribución por Complejidad**:
- Media: 3 casos (Escenarios 2, 4, 5)
- Alta: 2 casos (Escenarios 1, 3)

**Roles Involucrados**: Coordinador de Carrera / CEI

**Módulos a Probar**: 
- Reportes - Trazabilidad
- Reportes - Asignatura vs EURACE

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   - Asignatura de prueba: "Cálculo en una Variable"
   - Criterio EUR-ACE de prueba: "5.2.2"
   - Relación predefinida entre la asignatura y el criterio con checkmark verde
   - RAAs asociados a la asignatura para cada nivel (Alto, Medio, Bajo)
   - RAs de la carrera relacionados
   - Justificaciones académicas documentadas
   - Criterios EUR-ACE completos con descripciones

2. **Consideraciones Especiales**:
   - Validar que el clic en checkmark verde navegue correctamente (no en celdas vacías)
   - Verificar que los colores de fondo de cada nivel sean distintos y correctos (verde/turquesa para Alto, amarillo para Medio, rosa para Bajo)
   - Confirmar que las flechas direccionales (→) estén correctamente posicionadas entre columnas
   - Validar que todas las cards tengan bordes redondeados según el diseño
   - Asegurar que el botón "Regresar" preserve el estado completo de los filtros

3. **Defectos Potenciales a Detectar**:
   - Clic en checkmark no navega a trazabilidad
   - Título de trazabilidad incorrecto o no muestra nombre de asignatura
   - Botón "Regresar" no visible o no funcional
   - Colores de fondo incorrectos en niveles de aporte
   - Secciones en orden incorrecto (no Alto → Medio → Bajo)
   - Flechas direccionales faltantes o mal posicionadas
   - Cards sin bordes redondeados
   - Contenido truncado o ilegible
   - Solapamiento de información entre niveles
   - Pérdida de filtros al regresar de trazabilidad
   - Scroll vertical no funcional

4. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Base de datos con trazabilidad completa documentada (RAA → RA → Justificación → Criterio EUR-ACE)
   - Relaciones configuradas para los tres niveles de aporte
   - Matriz de "Asignatura vs Criterios EURACE" funcional como punto de partida
   - Navegación entre vistas funcionando correctamente

5. **Dependencias con Otras HUs**:
   - Esta HU depende de la HU "Visualizar Reporte Asignatura vs Criterios EURACE" (HU previa)
   - Se debe ejecutar después de validar la matriz principal
   - Los casos de prueba requieren que la matriz esté funcional y con datos

6. **Criterios de Éxito**:
   - Navegación fluida desde matriz a trazabilidad y viceversa
   - Preservación completa del contexto de filtros
   - Visualización clara y legible de la trazabilidad completa
   - Diferenciación visual correcta entre los tres niveles de aporte
   - Flujo de información comprensible de izquierda a derecha
   - Sin pérdida de datos ni errores de navegación