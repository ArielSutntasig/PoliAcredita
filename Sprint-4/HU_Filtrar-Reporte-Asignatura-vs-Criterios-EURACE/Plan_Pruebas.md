# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: FILTRAR REPORTE ASIGNATURA VS CRITERIOS EURACE**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Baja | HU: Filtrar Reporte Asignatura vs Criterios EURACE - Escenario 1 – Estado inicial con carrera deshabilitada | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera o CEI | Verificar estado inicial correcto con campo Facultad habilitado y Carrera deshabilitada | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Acceder al reporte "Reporte: Asignatura vs Criterios EURACE" sin haber seleccionado filtros | *Se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad"<br>*El campo está vacío y habilitado para escritura | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el estado del dropdown "Carrera:" | *Se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera"<br>*El dropdown "Carrera:" está en estado deshabilitado visualmente (color gris)<br>*El dropdown "Carrera:" no es clickeable | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Intentar hacer clic en el dropdown "Carrera:" | *No se puede abrir la lista de opciones de carrera<br>*Es evidente que se debe seleccionar primero una facultad | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Filtrar Reporte Asignatura vs Criterios EURACE - Escenario 2 – Buscar facultad con autocompletado | *El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*El campo "Facultad:" debe estar vacío | Verificar funcionamiento correcto del autocompletado al escribir en campo Facultad | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | En el campo de búsqueda "Facultad:" escribir "Sis" | *El texto "Sis" se muestra en el campo<br>*Se despliega una lista de autocompletado debajo del campo<br>*El campo mantiene el texto "Sis" mientras se muestra el autocompletado | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar las opciones mostradas en el autocompletado | *La lista muestra opciones que coinciden con el texto ingresado: "Sistemas", "Química y Agroindustria"<br>*Las opciones están ordenadas alfabéticamente o por relevancia<br>*La búsqueda es sensible a coincidencias parciales desde el inicio del nombre | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar que las opciones son clickeables | *Puedo hacer clic en cualquiera de las opciones desplegadas | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Filtrar Reporte Asignatura vs Criterios EURACE - Escenario 3 – Seleccionar facultad y habilitar carrera | *El usuario debe haber escrito en el campo "Facultad:"<br>*Deben ser visibles opciones en el autocompletado<br>*El dropdown "Carrera:" debe estar deshabilitado | Verificar habilitación correcta del dropdown Carrera al seleccionar una facultad | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Hacer clic en la opción "Sistemas" del autocompletado | *El campo "Facultad:" se actualiza con el valor "Sistemas"<br>*El autocompletado se cierra | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el estado del dropdown "Carrera:" después de seleccionar facultad | *El dropdown "Carrera:" cambia a estado habilitado<br>*El dropdown "Carrera:" se vuelve clickeable con apariencia activa<br>*El texto del dropdown permanece como "Seleccionar una carrera" | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el área de contenido del reporte | *No se muestra contenido de matriz hasta completar todos los filtros requeridos | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Filtrar Reporte Asignatura vs Criterios EURACE - Escenario 4 – Desplegar y visualizar opciones de carrera | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El dropdown "Carrera:" debe estar habilitado | Verificar despliegue correcto de opciones de carrera correspondientes a la facultad seleccionada | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Hacer clic en el dropdown "Carrera:" | *Se despliega una lista con las carreras correspondientes a la facultad "Sistemas"<br>*La lista muestra las opciones: "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial" | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar las características de las opciones desplegadas | *Las opciones están claramente visibles y son clickeables<br>*Cada opción está en una línea separada<br>*Solo se muestran carreras que pertenecen a la facultad seleccionada<br>*No aparecen carreras de otras facultades | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar funcionalidad de scroll si aplica | *Puedo desplazarme por la lista si hay más opciones que espacio visible | ESTADO PRUEBA | Solo aplica si hay más de 3 opciones | | | |
| 28-10-2025 | Manual | Alta | Baja | HU: Filtrar Reporte Asignatura vs Criterios EURACE - Escenario 5 – Seleccionar carrera completando filtros | *El usuario debe tener la facultad "Sistemas" seleccionada<br>*El dropdown "Carrera:" debe estar desplegado con opciones visibles | Verificar actualización correcta del campo Carrera al seleccionar una opción | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Hacer clic en la opción "Ingeniería de Software" del dropdown | *El dropdown "Carrera:" se actualiza con el valor "Ingeniería de Software" o "Software"<br>*La lista de opciones se cierra | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar que los filtros quedan configurados correctamente | *El campo "Facultad:" mantiene el valor "Sistemas"<br>*Ambos filtros (Facultad y Carrera) quedan configurados<br>*Los valores seleccionados permanecen visibles en los campos correspondientes | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar estado del sistema | *El sistema está listo para generar el reporte cuando se marquen los niveles de aporte | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Filtrar Reporte Asignatura vs Criterios EURACE - Escenario 6 – Cambiar facultad con reseteo de carrera | *El usuario debe tener la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas | Verificar reseteo correcto del campo Carrera al cambiar de facultad | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Borrar el texto del campo "Facultad:", escribir "Quí" y seleccionar "Química y Agroindustria" del autocompletado | *El campo "Facultad:" se actualiza con "Química y Agroindustria"<br>*El dropdown "Carrera:" se resetea al estado "Seleccionar una carrera"<br>*El dropdown "Carrera:" permanece habilitado | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Hacer clic en el dropdown "Carrera:" después del cambio de facultad | *Se despliegan las carreras correspondientes a "Química y Agroindustria" (diferentes a las de Sistemas)<br>*No se muestran las carreras de la facultad anterior (Sistemas) | ESTADO PRUEBA | Validar que las carreras mostradas son diferentes | | | |
| | | | | | | | | | Paso3 | Verificar estado del sistema antes de seleccionar nueva carrera | *Debo seleccionar una nueva carrera de la nueva facultad para completar los filtros<br>*No se muestra contenido de matriz hasta reseleccionar la carrera | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Filtrar Reporte Asignatura vs Criterios EURACE

**Total de Casos de Prueba**: 6 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 6 casos (100%)

**Distribución por Complejidad**:
- Baja: 2 casos (Escenarios 1, 5)
- Media: 3 casos (Escenarios 2, 3, 4)
- Alta: 1 caso (Escenario 6)

**Roles Involucrados**: Coordinador de Carrera / CEI

**Módulos a Probar**: 
- Reportes - Asignatura vs EURACE

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   
   **Facultades en el sistema:**
   - Sistemas
   - Química y Agroindustria
   
   **Carreras por Facultad:**
   - **Sistemas**:
     - Ingeniería de Software
     - Ingeniería Ciencias de la Computación
     - Ingeniería en Inteligencia Artificial
   - **Química y Agroindustria**:
     - (Carreras diferentes a las de Sistemas)

2. **Consideraciones Especiales**:
   - Esta HU se enfoca en la **interacción con filtros** (Facultad y Carrera)
   - Es **independiente pero complementaria** a las HUs de visualización de reportes
   - El campo Facultad usa **autocompletado** (búsqueda en tiempo real)
   - El dropdown Carrera tiene **dependencia** del campo Facultad
   - Existe una **relación cascada**: cambiar Facultad resetea Carrera
   - Los estados visuales (habilitado/deshabilitado) deben ser claramente distinguibles

3. **Defectos Potenciales a Detectar**:
   - Dropdown Carrera habilitado sin seleccionar Facultad
   - Autocompletado no funciona al escribir en Facultad
   - Autocompletado muestra opciones que no coinciden con el texto escrito
   - Opciones de Carrera incorrectas (muestra carreras de otra facultad)
   - Carrera no se resetea al cambiar Facultad
   - Dropdown Carrera no cambia de estado visual al habilitarse/deshabilitarse
   - Se puede hacer clic en dropdown Carrera cuando está deshabilitado
   - Autocompletado no se cierra al seleccionar una opción
   - Valores seleccionados no persisten en los campos
   - Lista de Carrera muestra carreras de la facultad anterior después de cambiar

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Estado inicial):
   - ✓ Campo Facultad: vacío, habilitado, con placeholder
   - ✓ Dropdown Carrera: texto "Seleccionar una carrera", deshabilitado, color gris, no clickeable
   
   **Escenario 2** (Autocompletado):
   - ✓ Al escribir "Sis": muestra "Sistemas" y "Química y Agroindustria"
   - ✓ Texto permanece en campo mientras se muestra autocompletado
   - ✓ Opciones son clickeables
   - ✓ Búsqueda parcial desde inicio del nombre
   
   **Escenario 3** (Habilitar Carrera):
   - ✓ Al seleccionar "Sistemas": campo se actualiza
   - ✓ Autocompletado se cierra
   - ✓ Dropdown Carrera se habilita (cambio visual + clickeable)
   - ✓ Texto sigue siendo "Seleccionar una carrera"
   - ✓ NO se muestra matriz
   
   **Escenario 4** (Opciones Carrera):
   - ✓ Muestra SOLO 3 carreras: "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial"
   - ✓ NO aparecen carreras de otras facultades
   - ✓ Cada opción en línea separada
   - ✓ Opciones clickeables
   
   **Escenario 5** (Seleccionar Carrera):
   - ✓ Dropdown se actualiza con "Ingeniería de Software" o "Software"
   - ✓ Lista se cierra
   - ✓ Facultad mantiene "Sistemas"
   - ✓ Ambos filtros configurados
   - ✓ Sistema listo para generar reporte (con niveles de aporte)
   
   **Escenario 6** (Cambiar Facultad):
   - ✓ Al cambiar a "Química y Agroindustria": campo Facultad actualizado
   - ✓ Carrera se resetea a "Seleccionar una carrera"
   - ✓ Carrera permanece habilitada
   - ✓ Al hacer clic en Carrera: muestra carreras de Química (NO de Sistemas)
   - ✓ NO se muestra matriz hasta reseleccionar carrera

5. **Flujo de Estados del Dropdown Carrera**:
   
   | Situación | Estado Dropdown Carrera | Texto Mostrado | Clickeable | Color |
   |-----------|------------------------|----------------|------------|-------|
   | Estado inicial (sin Facultad) | Deshabilitado | "Seleccionar una carrera" | NO | Gris |
   | Después de seleccionar Facultad | Habilitado | "Seleccionar una carrera" | SÍ | Normal |
   | Después de seleccionar Carrera | Habilitado | "Ingeniería de Software" o "Software" | SÍ | Normal |
   | Después de cambiar Facultad | Habilitado (reseteado) | "Seleccionar una carrera" | SÍ | Normal |

6. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Base de datos con:
     - Listado de Facultades
     - Listado de Carreras con relación a Facultades
   - Componente de autocompletado funcional para campo Facultad
   - Lógica de habilitación/deshabilitación de Carrera basada en Facultad
   - Lógica de filtrado de Carreras según Facultad seleccionada
   - Lógica de reseteo de Carrera al cambiar Facultad

7. **Interacción con Otras Funcionalidades**:
   - Esta HU es **prerequisito** para generar cualquier reporte
   - Se combina con la funcionalidad de "Nivel de aporte" para mostrar datos
   - Secuencia completa: Seleccionar Facultad → Seleccionar Carrera → Marcar Nivel(es) de Aporte → Ver Reporte

8. **Diferencias entre Roles (Coordinador vs CEI)**:
   - **Coordinador de Carrera**: 
     - Filtros deben estar **pre-poblados** con su carrera asignada
     - Campos deben estar **bloqueados** (no editables)
     - Solo puede ver datos de SU carrera
   - **CEI**: 
     - Filtros **vacíos** al inicio
     - Campos **editables** y puede cambiar entre facultades/carreras
     - Puede ver datos de TODAS las carreras
   
   **CRÍTICO**: Validar esta diferencia según el rol del usuario

9. **Orden de Ejecución Recomendado**:
   1. **Escenario 1**: Estado inicial (establecer baseline)
   2. **Escenario 2**: Autocompletado de Facultad
   3. **Escenario 3**: Seleccionar Facultad y ver habilitación de Carrera
   4. **Escenario 4**: Desplegar opciones de Carrera
   5. **Escenario 5**: Completar filtros seleccionando Carrera
   6. **Escenario 6**: Cambiar Facultad y validar reseteo

10. **Criterios de Éxito**:
   - Campo Facultad con autocompletado funcional
   - Dropdown Carrera correctamente habilitado/deshabilitado según contexto
   - Relación cascada Facultad → Carrera funcional
   - Opciones de Carrera filtradas correctamente por Facultad
   - Reseteo de Carrera al cambiar Facultad
   - Estados visuales claros (habilitado vs deshabilitado)
   - Interacción fluida sin errores de UI
   - Valores persisten correctamente en los campos

11. **Dependencias con Otras HUs**:
   - Esta HU es la **base** para todas las HUs de reportes que usan filtros
   - Se debe ejecutar **antes** de validar las HUs de visualización de reportes
   - Los reportes dependen de que estos filtros funcionen correctamente