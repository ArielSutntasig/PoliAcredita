# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: BUSCAR ASIGNATURA EN REPORTE ASIGNATURA VS CRITERIOS EURACE**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Baja | HU: Buscar Asignatura en Reporte Asignatura vs Criterios EURACE - Escenario 1 – Estado inicial sin búsqueda activa | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Coordinador de Carrera o CEI<br>*El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*Debe tener la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas<br>*Debe tener al menos un nivel de aporte marcado<br>*La matriz completa debe estar visible | Verificar estado inicial del campo de búsqueda vacío con todas las asignaturas visibles | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | Visualizar el campo de búsqueda "Buscar por código o nombre de asignatura" sin haber escrito nada | *El campo está vacío con el placeholder visible<br>*El campo está habilitado y listo para escritura | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar las asignaturas mostradas en la matriz | *Se muestran todas las asignaturas de la carrera en la matriz: Álgebra Lineal, Cálculo en una Variable, Mecánica Newtoniana, Programación I, Comunicación Oral y Escrita, Ecuaciones Diferenciales, Matemática Computacional, Fundamentos de Electrónica<br>*Todos los checkmarks verdes de las relaciones asignatura-criterio EUR-ACE están visibles | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar visibilidad de encabezados de columnas | *Los encabezados de columnas EUR-ACE (5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7) permanecen visibles | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Buscar Asignatura en Reporte Asignatura vs Criterios EURACE - Escenario 2 – Buscar asignatura sin resultados coincidentes | *El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*La matriz completa debe estar visible con todas las asignaturas | Verificar comportamiento correcto al buscar término que no existe y visualización de mensaje informativo | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | En el campo de búsqueda "Buscar por código o nombre de asignatura" escribir "XYZ999 Materia Inexistente" | *La tabla se actualiza automáticamente en tiempo real mientras se escribe<br>*No se muestra ninguna fila de asignatura en la tabla<br>*Se presenta un mensaje informativo indicando "No se encontraron asignaturas que coincidan con 'XYZ999 Materia Inexistente'" o mensaje similar | ESTADO PRUEBA | | Negativo | Funcional | |
| | | | | | | | | | Paso2 | Verificar que los elementos estructurales permanecen visibles | *Los encabezados de columnas EUR-ACE permanecen visibles<br>*Los filtros de Facultad, Carrera y Nivel de aporte se mantienen en su estado actual | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Borrar el texto del campo de búsqueda | *Todas las asignaturas reaparecen inmediatamente en la matriz | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Buscar Asignatura en Reporte Asignatura vs Criterios EURACE - Escenario 3 – Buscar y filtrar por código o nombre específico mostrando resultado único | *El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*La matriz completa debe estar visible mostrando múltiples asignaturas | Verificar filtrado en tiempo real con búsqueda específica mostrando resultado único y validar case-insensitive y coincidencias parciales | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | En el campo de búsqueda escribir "MATD113 Álgebra Lineal" | *La matriz se filtra automáticamente en tiempo real sin necesidad de presionar Enter o botón de búsqueda<br>*Se muestra únicamente la fila correspondiente a "Álgebra Lineal"<br>*Se visualizan los checkmarks verdes (✓) de Álgebra Lineal en las columnas 5.3.4 y 5.3.5 | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar que las demás asignaturas quedan ocultas | *Todas las demás asignaturas (Cálculo en una Variable, Mecánica Newtoniana, Programación I, etc.) quedan ocultas de la vista<br>*Los encabezados de columnas EUR-ACE permanecen completamente visibles<br>*Se puede ver rápidamente la contribución específica de Álgebra Lineal a los criterios EUR-ACE 5.3.4 y 5.3.5 | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Borrar el texto y buscar solo por código "MATD113" | *La búsqueda funciona escribiendo solo el código "MATD113" mostrando el mismo resultado (solo Álgebra Lineal) | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Borrar el texto y buscar solo por nombre "Álgebra Lineal" | *La búsqueda funciona escribiendo solo el nombre "Álgebra Lineal" mostrando el mismo resultado | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso5 | Probar búsqueda case-insensitive con diferentes variaciones | *La búsqueda es case-insensitive, permitiendo "álgebra lineal", "ÁLGEBRA LINEAL" o "Álgebra Lineal" con el mismo resultado | ESTADO PRUEBA | Probar las 3 variaciones | | | |
| | | | | | | | | | Paso6 | Probar búsqueda con coincidencias parciales como "Álg" o "MATD" | *La búsqueda acepta coincidencias parciales, permitiendo "Álg" o "MATD" para encontrar Álgebra Lineal | ESTADO PRUEBA | Probar ambas búsquedas parciales | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Buscar Asignatura en Reporte Asignatura vs Criterios EURACE - Escenario 4 – Buscar término que coincide con múltiples asignaturas | *El usuario debe estar en el reporte "Reporte: Asignatura vs Criterios EURACE"<br>*La matriz completa debe estar visible | Verificar filtrado con término parcial que muestra múltiples resultados coincidentes | Reportes - Asignatura vs EURACE | Coordinador de Carrera / CEI | Paso1 | En el campo de búsqueda escribir un término parcial como "Programación" | *La matriz se filtra automáticamente mostrando todas las asignaturas que contienen "Programación" en su código o nombre<br>*Se muestran múltiples filas como "Programación I", "Programación Avanzada", "Programación Web" (si existen en la carrera)<br>*Cada fila muestra sus checkmarks verdes correspondientes en las intersecciones con criterios EUR-ACE | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar ocultamiento de asignaturas no coincidentes | *Las asignaturas que no contienen el término "Programación" quedan ocultas<br>*Los encabezados de columnas EUR-ACE permanecen visibles<br>*Se pueden ver y comparar las contribuciones de todas las asignaturas de programación simultáneamente | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Escribir más caracteres para especificar, por ejemplo "Programación I" | *El filtrado se vuelve más específico mostrando solo esa asignatura | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Probar búsqueda case-insensitive con "programación", "PROGRAMACIÓN" | *La búsqueda es case-insensitive funcionando con "programación", "PROGRAMACIÓN" o "Programación" | ESTADO PRUEBA | Probar las 3 variaciones | | | |
| | | | | | | | | | Paso5 | Borrar el texto del campo de búsqueda | *Reaparecen todas las asignaturas de la matriz | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Buscar Asignatura en Reporte Asignatura vs Criterios EURACE

**Total de Casos de Prueba**: 4 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 4 casos (100%)

**Distribución por Complejidad**:
- Baja: 1 caso (Escenario 1)
- Media: 1 caso (Escenario 2)
- Alta: 2 casos (Escenarios 3, 4)

**Roles Involucrados**: Coordinador de Carrera / CEI

**Módulos a Probar**: 
- Reportes - Asignatura vs EURACE

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: 
- Positivo: 3 casos (Escenarios 1, 3, 4)
- Negativo: 1 caso (Escenario 2)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   
   **Asignaturas en la carrera "Ingeniería de Software"** (según prototipo):
   - MATD113 Álgebra Lineal
   - MATD123 Cálculo en una Variable
   - FISD134 Mecánica Newtoniana
   - ICCD144 Programación I
   - CSHD111 Comunicación Oral y Escrita
   - MATD213 Ecuaciones Diferenciales
   - ICCD224 Matemática Computacional
   - ICCD233 Fundamentos de Electrónica
   - Programación II (si existe)
   - Programación Avanzada (opcional para probar múltiples coincidencias)
   - Programación Web (opcional para probar múltiples coincidencias)
   
   **Relaciones específicas de prueba:**
   - Álgebra Lineal: checkmarks en 5.3.4 y 5.3.5

2. **Consideraciones Especiales**:
   - La búsqueda es **en tiempo real** (sin necesidad de presionar Enter o botón)
   - Busca tanto en **código** como en **nombre** de asignatura
   - Es **case-insensitive** (no distingue mayúsculas/minúsculas)
   - Acepta **coincidencias parciales** desde cualquier parte del código o nombre
   - El filtrado es **visual** (oculta filas, no las elimina)
   - Los **encabezados EUR-ACE** siempre permanecen visibles
   - Los **filtros de Facultad/Carrera/Nivel** mantienen su estado
   - Al **borrar** el texto, todas las asignaturas reaparecen **inmediatamente**

3. **Defectos Potenciales a Detectar**:
   - Campo de búsqueda no visible o deshabilitado
   - Búsqueda requiere presionar Enter o botón (no es en tiempo real)
   - Búsqueda solo funciona con código o solo con nombre (no ambos)
   - Búsqueda es case-sensitive (distingue mayúsculas/minúsculas)
   - No acepta coincidencias parciales (requiere término completo)
   - Encabezados EUR-ACE desaparecen al filtrar
   - Filtros de Facultad/Carrera/Nivel se resetean al buscar
   - Mensaje de "no encontrado" no aparece o es confuso
   - Asignaturas no reaparecen al borrar búsqueda
   - Performance lenta (lag) en búsqueda en tiempo real
   - Checkmarks no visibles en filas filtradas
   - Búsqueda afecta relaciones mostradas incorrectamente

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Estado inicial):
   - ✓ Campo de búsqueda vacío con placeholder visible
   - ✓ Campo habilitado para escritura
   - ✓ Todas las 8 asignaturas visibles
   - ✓ Todos los checkmarks verdes visibles
   - ✓ Encabezados EUR-ACE (12 columnas) visibles
   
   **Escenario 2** (Sin resultados):
   - ✓ Actualización en tiempo real mientras se escribe
   - ✓ Ninguna fila de asignatura visible
   - ✓ Mensaje "No se encontraron asignaturas que coincidan con..." visible
   - ✓ Encabezados EUR-ACE permanecen visibles
   - ✓ Filtros mantienen estado
   - ✓ Al borrar: todas las asignaturas reaparecen inmediatamente
   
   **Escenario 3** (Resultado único):
   - ✓ Filtrado automático en tiempo real (sin Enter/botón)
   - ✓ Solo "Álgebra Lineal" visible
   - ✓ Checkmarks en 5.3.4 y 5.3.5 visibles
   - ✓ Todas las demás asignaturas ocultas
   - ✓ Encabezados EUR-ACE visibles
   - ✓ Búsqueda por código completo ("MATD113") funciona
   - ✓ Búsqueda por nombre completo ("Álgebra Lineal") funciona
   - ✓ Case-insensitive: "álgebra lineal", "ÁLGEBRA LINEAL" funcionan
   - ✓ Coincidencias parciales: "Álg", "MATD" funcionan
   
   **Escenario 4** (Múltiples resultados):
   - ✓ Término "Programación" muestra múltiples asignaturas
   - ✓ "Programación I", "Programación Avanzada", "Programación Web" visibles
   - ✓ Cada fila con sus checkmarks correspondientes
   - ✓ Asignaturas sin "Programación" ocultas
   - ✓ Encabezados visibles
   - ✓ Comparación visual de múltiples asignaturas posible
   - ✓ Al especificar "Programación I": filtrado más específico
   - ✓ Case-insensitive: "programación", "PROGRAMACIÓN" funcionan
   - ✓ Al borrar: todas reaparecen

5. **Comportamiento de Búsqueda**:

   | Entrada | Tipo | Resultado Esperado |
   |---------|------|-------------------|
   | **"MATD113"** | Código completo | Solo Álgebra Lineal |
   | **"Álgebra Lineal"** | Nombre completo | Solo Álgebra Lineal |
   | **"MATD"** | Código parcial | Todas las asignaturas con código que inicie con MATD |
   | **"Álg"** | Nombre parcial | Álgebra Lineal |
   | **"Programación"** | Término común | Todas las asignaturas con "Programación" |
   | **"álgebra"** | Lowercase | Álgebra Lineal (case-insensitive) |
   | **"ÁLGEBRA"** | Uppercase | Álgebra Lineal (case-insensitive) |
   | **"XYZ999"** | No existe | Mensaje "No se encontraron asignaturas" |
   | **""** (vacío) | Sin término | Todas las asignaturas visibles |

6. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Usuarios con roles Coordinador de Carrera y CEI autenticados
   - Reporte "Asignatura vs Criterios EURACE" funcional
   - Filtros de Facultad, Carrera y Nivel de aporte funcionales
   - Matriz con al menos 8 asignaturas y relaciones con criterios EUR-ACE
   - Implementación de búsqueda en tiempo real (event listeners)
   - Lógica de filtrado de filas basada en búsqueda
   - Manejo de case-insensitive y coincidencias parciales

7. **Flujo Completo de Búsqueda**:
   ```
   1. Usuario en reporte con matriz visible (todas las asignaturas)
   2. Usuario escribe en campo de búsqueda
   3. Sistema filtra en tiempo real (cada carácter)
   4. Filas no coincidentes se ocultan
   5. Filas coincidentes permanecen visibles con checkmarks
   6. Encabezados EUR-ACE permanecen fijos
   7. Si no hay coincidencias: mensaje informativo
   8. Usuario borra texto: todas las asignaturas reaparecen
   ```

8. **Aspectos de Usabilidad a Validar**:
   - **Performance**: La búsqueda en tiempo real debe ser rápida (<200ms por carácter)
   - **Feedback visual**: Usuario debe ver inmediatamente los resultados del filtrado
   - **Claridad**: Mensaje de "no encontrado" debe ser claro y útil
   - **Persistencia**: Filtros de Facultad/Carrera/Nivel no deben afectarse
   - **Reversibilidad**: Fácil volver al estado completo (borrar texto)

9. **Interacción con Otras Funcionalidades**:
   - Esta HU **complementa** el reporte "Asignatura vs Criterios EURACE"
   - Funciona **en conjunto** con:
     - Filtros de Facultad/Carrera
     - Filtros de Nivel de aporte
     - Navegación a trazabilidad (clic en checkmark)
   - **NO afecta**:
     - Estado de filtros de Facultad/Carrera/Nivel
     - Relaciones subyacentes (solo visualización)
     - Datos persistidos en base de datos

10. **Orden de Ejecución Recomendado**:
    1. **Escenario 1**: Validar estado inicial sin búsqueda
    2. **Escenario 3**: Validar búsqueda con resultado único (caso más común)
    3. **Escenario 4**: Validar búsqueda con múltiples resultados
    4. **Escenario 2**: Validar búsqueda sin resultados (caso de error)

11. **Criterios de Éxito**:
    - Campo de búsqueda funcional y visible
    - Filtrado en tiempo real sin necesidad de botón/Enter
    - Búsqueda por código Y nombre funcional
    - Case-insensitive funcionando correctamente
    - Coincidencias parciales funcionando
    - Encabezados EUR-ACE siempre visibles
    - Filtros de Facultad/Carrera/Nivel mantienen estado
    - Mensaje de "no encontrado" claro
    - Checkmarks visibles en filas filtradas
    - Al borrar texto: todas las asignaturas reaparecen
    - Performance adecuada en búsqueda en tiempo real

12. **Dependencias con Otras HUs**:
    - **Dependencia CRÍTICA**: HU "Visualizar Reporte Asignatura vs Criterios EURACE"
    - Esta HU NO puede ejecutarse sin que la matriz base esté funcional
    - Es una **mejora de usabilidad** sobre el reporte base
    - Se recomienda ejecutar DESPUÉS de validar el reporte base

13. **Diferencias entre Roles** (No aplica en esta HU):
    - Coordinador de Carrera y CEI tienen el **mismo comportamiento** de búsqueda
    - No hay restricciones diferentes por rol
    - Ambos roles buscan de la misma manera

14. **Casos Límite a Considerar**:
    - ¿Qué pasa con caracteres especiales en búsqueda (ñ, á, ü)?
    - ¿Funciona con números en el código?
    - ¿Qué pasa si se pegan múltiples líneas de texto?
    - ¿Hay límite de caracteres en el campo de búsqueda?
    - ¿Qué pasa con espacios múltiples o al inicio/fin?
    - ¿Funciona con códigos que tienen guiones o puntos?