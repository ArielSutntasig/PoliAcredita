# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: FILTRAR REPORTE OBJETIVOS DE CARRERA VS RESULTADOS DE APRENDIZAJE VS ASIGNATURAS**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Baja | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 1 – Estado inicial con carrera deshabilitada | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera | Verificar estado inicial correcto con campo Facultad habilitado y Carrera deshabilitada | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Acceder al reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" sin haber seleccionado filtros | *Se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad"<br>*El campo está vacío y habilitado para escritura | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el estado del dropdown "Carrera:" | *Se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera"<br>*El dropdown "Carrera:" está en estado deshabilitado visualmente<br>*El dropdown "Carrera:" no es clickeable<br>*No se puede abrir la lista de opciones de carrera | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el área de contenido del reporte | *No se muestran encabezados de tabla ni contenido de trazabilidad<br>*Es evidente que se debe seleccionar primero una facultad para continuar | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 2 – Seleccionar facultad y habilitar carrera | *El usuario debe estar en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas"<br>*El dropdown "Carrera:" debe estar deshabilitado | Verificar habilitación correcta del dropdown Carrera al seleccionar facultad y despliegue de opciones | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | En el campo "Facultad:" escribir el texto necesario y seleccionar "Sistemas" del autocompletado | *El campo "Facultad:" se actualiza con el valor "Sistemas"<br>*El dropdown "Carrera:" cambia a estado habilitado<br>*El dropdown "Carrera:" se vuelve clickeable con apariencia activa<br>*El texto del dropdown permanece como "Seleccionar una carrera" hasta que se haga una selección | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Hacer clic en el dropdown "Carrera:" | *Se despliegan las opciones de carreras pertenecientes a "Sistemas": "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial"<br>*Solo se muestran carreras que pertenecen a la facultad seleccionada | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el área de contenido del reporte | *No se muestra contenido de tabla hasta completar todos los filtros | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Baja | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 3 – Seleccionar carrera completando filtros | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El dropdown "Carrera:" debe estar habilitado | Verificar actualización correcta del campo Carrera al seleccionar una opción y configuración completa de filtros | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Hacer clic en el dropdown "Carrera:" y seleccionar "Software" de las opciones disponibles | *El dropdown "Carrera:" se actualiza con el valor "Software"<br>*La lista de opciones se cierra | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar que los filtros quedan configurados correctamente | *El campo "Facultad:" mantiene el valor "Sistemas"<br>*Ambos filtros (Facultad y Carrera) quedan configurados<br>*Los valores seleccionados permanecen visibles y estables en los campos correspondientes | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar estado del sistema | *El sistema está preparado para generar la tabla de trazabilidad cuando se marquen los niveles de aporte | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 4 – Generar tabla filtrada por carrera específica | *El usuario debe tener la facultad "Sistemas" y carrera "Software" seleccionadas | Verificar que la tabla generada muestre únicamente datos correspondientes a la carrera Software | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Marcar al menos un checkbox de nivel de aporte (Alto, Medio o Bajo) | *Se genera la tabla de trazabilidad con tres columnas | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar los objetivos de carrera mostrados en la tabla | *Se muestran únicamente los objetivos de carrera (OP) que pertenecen a "Software" (OPP1, OPP2, OPP3, OPP5)<br>*No se muestran objetivos de otras carreras de la facultad | ESTADO PRUEBA | Validar que SOLO aparecen OPP de Software | | | |
| | | | | | | | | | Paso3 | Verificar los resultados de aprendizaje mostrados en la tabla | *Se presentan únicamente los resultados de aprendizaje (RA) específicos de la carrera Software (RG1, RG3, RE4, RG4, RE1, RE2, RE3, RG2)<br>*No se muestran RA de otras carreras | ESTADO PRUEBA | Validar que SOLO aparecen RA de Software | | | |
| | | | | | | | | | Paso4 | Verificar las asignaturas mostradas en la tabla | *Se muestran únicamente las asignaturas correspondientes a la carrera Software (IS-101, IS-305, MA-102, IS-203, GE-401, HU-301, IS-306, IS-501, IS-402, MA-201, CO-101, IS-403)<br>*No se muestran asignaturas de otras carreras<br>*La tabla presenta la trazabilidad completa OP→RA→Asignaturas exclusivamente del programa de estudios "Software"<br>*El contenido permite analizar específicamente la alineación del programa seleccionado | ESTADO PRUEBA | Validar que SOLO aparecen asignaturas de Software | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas - Escenario 5 – Cambiar carrera dentro de la misma facultad | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El usuario debe tener la carrera "Software" seleccionada<br>*La tabla de trazabilidad debe estar visible con datos de Software | Verificar actualización automática y correcta de la tabla al cambiar de carrera dentro de la misma facultad | Reportes - OP vs RA vs Asignatura | Coordinador de Carrera | Paso1 | Hacer clic en el dropdown "Carrera:" y seleccionar "Ingeniería Ciencias de la Computación" de las opciones | *El dropdown "Carrera:" se actualiza con "Ingeniería Ciencias de la Computación"<br>*El campo "Facultad:" mantiene el valor "Sistemas"<br>*La tabla de trazabilidad se actualiza automáticamente sin recargar la página | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar el contenido actualizado de la tabla | *Se muestran únicamente los objetivos, resultados de aprendizaje y asignaturas correspondientes a "Ingeniería Ciencias de la Computación"<br>*Se ocultan todos los datos de "Software" | ESTADO PRUEBA | Comparar con datos anteriores de Software | | | |
| | | | | | | | | | Paso3 | Verificar el estado de los checkboxes de nivel de aporte | *Los checkboxes de nivel de aporte mantienen su estado de selección<br>*El sistema permite comparar fácilmente entre carreras de la misma facultad cambiando solo el filtro de carrera | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas

**Total de Casos de Prueba**: 5 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 5 casos (100%)

**Distribución por Complejidad**:
- Baja: 2 casos (Escenarios 1, 3)
- Media: 1 caso (Escenario 2)
- Alta: 2 casos (Escenarios 4, 5)

**Roles Involucrados**: Coordinador de Carrera

**Módulos a Probar**: 
- Reportes - OP vs RA vs Asignatura

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   
   **Facultades en el sistema:**
   - Sistemas
   
   **Carreras de la Facultad Sistemas:**
   - Ingeniería de Software (o "Software")
   - Ingeniería Ciencias de la Computación
   - Ingeniería en Inteligencia Artificial
   
   **Datos específicos de la carrera "Software":**
   - **Objetivos de Carrera (OPP)**: OPP1, OPP2, OPP3, OPP5
   - **Resultados de Aprendizaje (RA)**: RG1, RG3, RE4, RG4, RE1, RE2, RE3, RG2
   - **Asignaturas**: IS-101, IS-305, MA-102, IS-203, GE-401, HU-301, IS-306, IS-501, IS-402, MA-201, CO-101, IS-403
   
   **Datos específicos de la carrera "Ingeniería Ciencias de la Computación":**
   - Objetivos, RA y asignaturas DIFERENTES a los de Software

2. **Consideraciones Especiales**:
   - Esta HU se enfoca en el **filtrado por carrera** para mostrar datos específicos del programa
   - Es una **extensión** de la HU base de filtros (Facultad/Carrera)
   - El énfasis está en **validar que SOLO se muestran datos de la carrera seleccionada**
   - El cambio de carrera debe ser **reactivo** sin recarga de página
   - Los checkboxes de nivel de aporte deben **mantener su estado** al cambiar carrera
   - Solo aplica para rol **Coordinador de Carrera** (no CEI en esta HU)

3. **Defectos Potenciales a Detectar**:
   - Tabla muestra datos de múltiples carreras (no filtra correctamente)
   - Aparecen OPP de otras carreras en la tabla
   - Aparecen RA de otras carreras en la tabla
   - Aparecen asignaturas de otras carreras en la tabla
   - Al cambiar carrera no se actualiza la tabla
   - Al cambiar carrera se requiere recarga de página (no es automático)
   - Al cambiar carrera se pierden los checkboxes de nivel de aporte
   - Campo Facultad cambia al seleccionar otra carrera
   - Datos de la carrera anterior siguen visibles después del cambio

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Estado inicial):
   - ✓ Campo Facultad: vacío, habilitado, con placeholder
   - ✓ Dropdown Carrera: deshabilitado, no clickeable
   - ✓ Sin encabezados ni contenido de tabla
   
   **Escenario 2** (Habilitar Carrera):
   - ✓ Al seleccionar "Sistemas": Carrera se habilita
   - ✓ Al hacer clic en Carrera: muestra 3 opciones (Ingeniería de Software, Ingeniería Ciencias de la Computación, Ingeniería en Inteligencia Artificial)
   - ✓ SOLO carreras de Sistemas
   - ✓ Sin contenido de tabla
   
   **Escenario 3** (Completar filtros):
   - ✓ Seleccionar "Software": dropdown actualizado
   - ✓ Facultad mantiene "Sistemas"
   - ✓ Ambos filtros configurados
   - ✓ Sistema listo para generar tabla
   
   **Escenario 4** (Tabla filtrada por Software):
   - ✓ **CRÍTICO**: SOLO datos de Software
   - ✓ OPP: SOLO OPP1, OPP2, OPP3, OPP5 (de Software)
   - ✓ RA: SOLO RG1, RG3, RE4, RG4, RE1, RE2, RE3, RG2 (de Software)
   - ✓ Asignaturas: SOLO IS-101, IS-305, MA-102, IS-203, GE-401, HU-301, IS-306, IS-501, IS-402, MA-201, CO-101, IS-403 (de Software)
   - ✓ NO aparecen datos de otras carreras
   
   **Escenario 5** (Cambiar carrera):
   - ✓ Cambiar a "Ingeniería Ciencias de la Computación"
   - ✓ Facultad mantiene "Sistemas"
   - ✓ Tabla se actualiza automáticamente (sin recarga)
   - ✓ Muestra SOLO datos de Ciencias de la Computación
   - ✓ Oculta TODOS los datos de Software
   - ✓ Checkboxes mantienen estado

5. **Comparación Crítica: Software vs Ciencias de la Computación**:

   | Aspecto | Software | Ciencias de la Computación |
   |---------|----------|---------------------------|
   | **Objetivos (OPP)** | OPP1, OPP2, OPP3, OPP5 | Diferentes |
   | **RA** | RG1, RG3, RE4, RG4, RE1, RE2, RE3, RG2 | Diferentes |
   | **Asignaturas** | IS-101, IS-305, MA-102, IS-203, GE-401, HU-301, IS-306, IS-501, IS-402, MA-201, CO-101, IS-403 | Diferentes |
   | **Visualización** | Exclusiva de Software | Exclusiva de Ciencias de la Computación |

   **CRÍTICO**: Al cambiar de carrera, NINGÚN dato del anterior debe permanecer visible.

6. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Base de datos con:
     - Objetivos de Carrera por programa académico
     - Resultados de Aprendizaje por carrera
     - Asignaturas por carrera
     - Relaciones OPP→RA→Asignaturas por carrera
   - Lógica de filtrado que:
     - Habilita/deshabilita Carrera según Facultad
     - Filtra opciones de Carrera según Facultad
     - Filtra contenido de tabla según Carrera seleccionada
     - Actualiza tabla reactivamente al cambiar Carrera

7. **Flujo Completo de Filtrado**:
   ```
   1. Estado inicial → Facultad vacía, Carrera deshabilitada, Sin tabla
   2. Seleccionar Facultad → Carrera habilitada, Muestra opciones de carreras de esa facultad
   3. Seleccionar Carrera → Filtros completos, Sistema listo
   4. Marcar Nivel de Aporte → Tabla generada con datos SOLO de la carrera seleccionada
   5. Cambiar Carrera → Tabla actualizada con datos SOLO de la nueva carrera
   ```

8. **Interacción con Otras Funcionalidades**:
   - Esta HU **depende** de la HU base de filtros Facultad/Carrera
   - Se **combina** con la HU de filtrado por nivel de aporte
   - Es **prerequisito** para visualizar correctamente el reporte por carrera específica

9. **Diferencias vs HU de Filtros Base**:
   - **HU Base (anterior)**: Se enfoca en la interacción UI (habilitar/deshabilitar, autocompletado)
   - **Esta HU**: Se enfoca en el **filtrado de datos** según carrera seleccionada
   - Esta HU valida que el contenido mostrado corresponde exclusivamente a la carrera

10. **Orden de Ejecución Recomendado**:
    1. **Escenario 1**: Estado inicial
    2. **Escenario 2**: Habilitar y desplegar carreras
    3. **Escenario 3**: Completar filtros
    4. **Escenario 4**: Validar filtrado de datos por Software (documentar datos específicos)
    5. **Escenario 5**: Cambiar a Ciencias de la Computación y validar cambio de datos

11. **Criterios de Éxito**:
    - Tabla muestra EXCLUSIVAMENTE datos de la carrera seleccionada
    - Al cambiar carrera, datos se actualizan automáticamente
    - Sin mezcla de datos entre carreras
    - Checkboxes de nivel mantienen estado al cambiar carrera
    - Actualización reactiva sin recargas
    - Facultad permanece estable al cambiar carrera dentro de la misma facultad

12. **Dependencias con Otras HUs**:
    - **Dependencia**: HU "Filtrar Reporte Asignatura vs Criterios EURACE" (filtros base)
    - **Dependencia**: HU "Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" (tabla base)
    - **Dependencia**: HU de filtrado por nivel de aporte para este reporte
    - Se recomienda ejecutar DESPUÉS de validar las HUs de filtros base y visualización

13. **Casos Límite a Considerar**:
    - ¿Qué pasa si una carrera no tiene objetivos definidos?
    - ¿Qué pasa si una carrera no tiene asignaturas asociadas?
    - ¿La tabla muestra mensaje apropiado si no hay datos para la carrera?
    - ¿Qué pasa si se cambia rápidamente entre múltiples carreras?