# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: OBSERVAR CARACTERES PERMITIDOS EN JUSTIFICACIONES EN MATRICES**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Baja | HU: Observar caracteres permitidos en justificaciones en Matrices - Escenario 1 – Estado inicial del campo de justificación vacío | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Profesor<br>*El usuario debe estar en el flujo de crear o editar una relación en cualquiera de las matrices (RA vs OP, RAA vs RA, o RA vs EUR-ACE) | Verificar visualización correcta del contador de caracteres en estado inicial vacío | Matrices - RA vs OP / RAA vs RA / RA vs EUR-ACE | Profesor | Paso1 | Visualizar el campo de "Justificación" sin haber escrito ningún contenido | *Se muestra el contador de caracteres con el texto "0/2000 caracteres" o formato equivalente<br>*El contador se presenta en color neutral (gris o negro)<br>*El campo está vacío y habilitado para escritura | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar visibilidad del límite de caracteres | *El límite de 2000 caracteres es claramente visible para planificar justificaciones concretas dentro de este límite | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Observar caracteres permitidos en justificaciones en Matrices - Escenario 2 – Escribir justificación dentro del rango normal | *El usuario debe estar en el campo de "Justificación" de cualquiera de las tres matrices<br>*El campo debe estar vacío mostrando "0/2000 caracteres" | Verificar actualización en tiempo real del contador y ausencia de restricciones en rango normal de caracteres | Matrices - RA vs OP / RAA vs RA / RA vs EUR-ACE | Profesor | Paso1 | En el campo de "Justificación" escribir texto hasta alcanzar 1500 caracteres (dentro del rango 1-1799) | *El contador se actualiza en tiempo real mostrando "1500/2000 caracteres"<br>*El contador mantiene el color neutral sin advertencias<br>*Se puede continuar escribiendo libremente<br>*Cada carácter adicional que se escribe incrementa el contador inmediatamente | ESTADO PRUEBA | Usar texto de prueba de exactamente 1500 caracteres | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Borrar varios caracteres del texto escrito | *El contador disminuye correspondientemente con cada carácter borrado<br>*El sistema no muestra ninguna restricción o advertencia en este rango | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar comportamiento consistente en las tres matrices | *Este comportamiento es idéntico en las matrices RA vs OP, RAA vs RA y RA vs EUR-ACE | ESTADO PRUEBA | Repetir en las 3 matrices | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Observar caracteres permitidos en justificaciones en Matrices - Escenario 3 – Advertencia al acercarse al límite de caracteres | *El usuario debe tener 1700 caracteres escritos en el campo de "Justificación" de cualquier matriz | Verificar cambio de color del contador y mensaje de advertencia al acercarse al límite | Matrices - RA vs OP / RAA vs RA / RA vs EUR-ACE | Profesor | Paso1 | Escribir caracteres adicionales hasta alcanzar el rango de 1800 a 1999 caracteres (por ejemplo, 1850 caracteres) | *El contador se actualiza mostrando el número actual de caracteres (ejemplo: "1850/2000 caracteres")<br>*El color del contador cambia a un color de advertencia (amarillo, naranja o similar)<br>*Opcionalmente se muestra un mensaje adicional como "Te acercas al límite de caracteres" o "Quedan X caracteres disponibles" | ESTADO PRUEBA | Usar texto de prueba de exactamente 1850 caracteres | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar que se puede continuar escribiendo en este rango | *Aún se puede continuar escribiendo hasta alcanzar los 2000 caracteres<br>*La advertencia visual permite tomar decisiones informadas sobre cómo redactar una justificación concreta dentro del límite | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar comportamiento consistente en las tres matrices | *Este comportamiento es consistente en las tres matrices del sistema | ESTADO PRUEBA | Repetir en las 3 matrices | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Observar caracteres permitidos en justificaciones en Matrices - Escenario 4 – Alcanzar el límite máximo y prevenir exceso | *El usuario debe tener 1995 caracteres escritos en el campo de "Justificación" de cualquier matriz | Verificar prevención de exceso al alcanzar límite máximo de 2000 caracteres y comportamiento de truncado | Matrices - RA vs OP / RAA vs RA / RA vs EUR-ACE | Profesor | Paso1 | Escribir 5 caracteres adicionales alcanzando exactamente 2000 caracteres | *El contador muestra "2000/2000 caracteres"<br>*El color del contador cambia a rojo o color de alerta máxima<br>*El sistema previene que se puedan escribir caracteres adicionales mediante teclado<br>*Las teclas de caracteres alfanuméricos, espacios y símbolos no insertan más texto | ESTADO PRUEBA | Usar texto de prueba de exactamente 2000 caracteres | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Intentar escribir caracteres adicionales y verificar que solo se permite edición | *No se pueden agregar más caracteres<br>*Aún se pueden usar las teclas Backspace, Delete y flechas de navegación para editar el texto existente<br>*Se muestra un mensaje informativo indicando "Has alcanzado el límite de 2000 caracteres" | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Intentar pegar texto que excedería el límite de 2000 caracteres | *El sistema trunca automáticamente el texto pegado a 2000 caracteres<br>*Se muestra un mensaje informativo indicando "Texto truncado al límite permitido" | ESTADO PRUEBA | Preparar texto de >2000 caracteres para pegar | | | |
| | | | | | | | | | Paso4 | Guardar la relación con exactamente 2000 caracteres | *Al intentar guardar la relación, la validación confirma que los 2000 caracteres están dentro del límite permitido<br>*La relación se guarda exitosamente | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso5 | Verificar comportamiento consistente en las tres matrices | *Este límite de 2000 caracteres y comportamiento es idéntico en las tres matrices (RA vs OP, RAA vs RA, RA vs EUR-ACE) para mantener consistencia en todo el sistema | ESTADO PRUEBA | Repetir en las 3 matrices | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Observar caracteres permitidos en justificaciones en Matrices (RA-OP, RAA-RA, RA-EUR-ACE)

**Total de Casos de Prueba**: 4 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 4 casos (100%)

**Distribución por Complejidad**:
- Baja: 1 caso (Escenario 1)
- Media: 2 casos (Escenarios 2, 3)
- Alta: 1 caso (Escenario 4)

**Roles Involucrados**: Profesor

**Módulos a Probar**: 
- Matrices - RA vs OP
- Matrices - RAA vs RA
- Matrices - RA vs EUR-ACE

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Límite de Caracteres y Rangos Críticos**:
   
   | Rango de Caracteres | Estado | Color Contador | Comportamiento |
   |---------------------|--------|----------------|----------------|
   | **0** | Inicial | Neutral (gris/negro) | Campo vacío, "0/2000 caracteres" |
   | **1 - 1799** | Normal | Neutral (gris/negro) | Escritura libre, sin restricciones |
   | **1800 - 1999** | Advertencia | Advertencia (amarillo/naranja) | Mensaje "Te acercas al límite", escritura permitida |
   | **2000** | Límite máximo | Alerta (rojo) | Prevención de escritura adicional, truncado en pegado |
   | **> 2000** | Bloqueado | Alerta (rojo) | No permite escritura, solo edición |

2. **Textos de Prueba Requeridos**:
   - **Texto de 1500 caracteres**: Para probar rango normal
   - **Texto de 1700 caracteres**: Estado inicial para prueba de advertencia
   - **Texto de 1850 caracteres**: Para probar estado de advertencia
   - **Texto de 1995 caracteres**: Estado inicial para prueba de límite máximo
   - **Texto de 2000 caracteres**: Para probar límite exacto
   - **Texto de >2000 caracteres** (ejemplo: 2500): Para probar truncado en pegado

3. **Consideraciones Especiales**:
   - Esta HU aplica a **TRES matrices diferentes**: RA vs OP, RAA vs RA, RA vs EUR-ACE
   - El comportamiento debe ser **idéntico** en las tres matrices
   - El contador debe actualizarse en **tiempo real** con cada carácter
   - El cambio de color debe ser **automático** según el rango
   - La prevención de escritura adicional debe ser **efectiva** al alcanzar 2000
   - El truncado de texto pegado debe ser **automático** y mostrar mensaje
   - No hay prototipo visual, por lo que los colores exactos pueden variar pero deben ser distinguibles

4. **Defectos Potenciales a Detectar**:
   - Contador no muestra "0/2000 caracteres" en estado inicial
   - Contador no se actualiza en tiempo real
   - Contador no cambia de color en rango de advertencia (1800-1999)
   - Contador no cambia a rojo al alcanzar 2000
   - Se pueden escribir más de 2000 caracteres por teclado
   - Texto pegado no se trunca a 2000 caracteres
   - Backspace/Delete no funcionan al alcanzar límite
   - Mensaje de advertencia no aparece o es confuso
   - Validación al guardar rechaza texto de 2000 caracteres exactos
   - Comportamiento inconsistente entre las tres matrices
   - Contador desincronizado con contenido real del campo

5. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Estado inicial):
   - ✓ Contador muestra "0/2000 caracteres"
   - ✓ Color neutral (gris/negro)
   - ✓ Campo vacío y habilitado
   - ✓ Límite claramente visible

   **Escenario 2** (Rango normal 1-1799):
   - ✓ Contador en tiempo real (ejemplo: 1500/2000)
   - ✓ Color neutral mantenido
   - ✓ Escritura libre sin restricciones
   - ✓ Contador incrementa/disminuye con cada carácter
   - ✓ Sin advertencias ni mensajes
   - ✓ Consistente en las 3 matrices

   **Escenario 3** (Advertencia 1800-1999):
   - ✓ Contador actualizado (ejemplo: 1850/2000)
   - ✓ Color cambió a advertencia (amarillo/naranja)
   - ✓ Mensaje opcional de advertencia visible
   - ✓ Escritura aún permitida
   - ✓ Consistente en las 3 matrices

   **Escenario 4** (Límite 2000):
   - ✓ Contador muestra "2000/2000"
   - ✓ Color cambió a rojo
   - ✓ Prevención de escritura adicional efectiva
   - ✓ Teclas alfanuméricas bloqueadas
   - ✓ Backspace/Delete/Flechas funcionan
   - ✓ Pegado trunca a 2000 caracteres
   - ✓ Mensaje de límite alcanzado visible
   - ✓ Mensaje de truncado visible (al pegar)
   - ✓ Validación al guardar exitosa
   - ✓ Consistente en las 3 matrices

6. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Usuario con rol Profesor autenticado
   - Acceso a las tres matrices:
     - RA vs OP (Resultados de Aprendizaje vs Objetivos de Programa)
     - RAA vs RA (Resultados de Aprendizaje de Asignatura vs Resultados de Aprendizaje)
     - RA vs EUR-ACE (Resultados de Aprendizaje vs Criterios EUR-ACE)
   - Flujo de crear/editar relación funcional
   - Campo de "Justificación" con contador de caracteres implementado
   - Validación de límite de caracteres en frontend y backend

7. **Casos de Borde a Probar**:
   - **Caracteres especiales**: ¿Cuentan igual que caracteres normales?
   - **Saltos de línea**: ¿Cuentan como 1 o 2 caracteres?
   - **Espacios múltiples**: ¿Se cuentan todos?
   - **Emojis**: ¿Cuentan como 1 o múltiples caracteres?
   - **Copiar/pegar con formato**: ¿Se mantiene el formato o solo texto plano?
   - **Pegar exactamente 2000 caracteres**: ¿Se permite sin truncar?
   - **Escribir hasta 1999 y pegar 2+ caracteres**: ¿Se trunca correctamente?

8. **Interacción con Teclas Especiales**:
   
   **Al alcanzar 2000 caracteres:**
   - ✓ **Bloqueadas**: A-Z, a-z, 0-9, símbolos, espacios, Enter
   - ✓ **Permitidas**: Backspace, Delete, Flechas (↑↓←→), Home, End, Ctrl+A, Ctrl+C, Ctrl+X
   - ✓ **Parcialmente**: Ctrl+V (pegar) - trunca a 2000

9. **Mensajes del Sistema**:
   
   **Mensajes esperados:**
   - Estado normal: Sin mensaje o contador solamente
   - Advertencia (1800-1999): "Te acercas al límite de caracteres" o "Quedan X caracteres disponibles"
   - Límite alcanzado (2000): "Has alcanzado el límite de 2000 caracteres"
   - Truncado por pegado: "Texto truncado al límite permitido"

10. **Orden de Ejecución Recomendado**:
    1. **Escenario 1**: Validar estado inicial en las 3 matrices
    2. **Escenario 2**: Validar rango normal (1-1799) en las 3 matrices
    3. **Escenario 3**: Validar advertencia (1800-1999) en las 3 matrices
    4. **Escenario 4**: Validar límite máximo (2000) y truncado en las 3 matrices

11. **Matrices a Probar (Validar en TODAS)**:
    
    | Matriz | Acrónimo | Entidades Relacionadas |
    |--------|----------|------------------------|
    | **RA vs OP** | Resultados de Aprendizaje vs Objetivos de Programa | RA ↔ OPP |
    | **RAA vs RA** | Resultados de Aprendizaje de Asignatura vs Resultados de Aprendizaje | RAA ↔ RA |
    | **RA vs EUR-ACE** | Resultados de Aprendizaje vs Criterios EUR-ACE | RA ↔ Criterio EUR-ACE |

12. **Criterios de Éxito**:
    - Contador visible y preciso en todo momento
    - Actualización en tiempo real con cada carácter
    - Cambios de color apropiados según rango
    - Mensajes de advertencia claros y oportunos
    - Prevención efectiva de exceso de caracteres
    - Truncado automático y correcto en pegado
    - Validación exitosa al guardar con 2000 caracteres
    - Comportamiento 100% consistente en las 3 matrices
    - Experiencia de usuario clara y predecible

13. **Dependencias con Otras HUs**:
    - Esta HU es **transversal** a todas las funcionalidades de crear/editar relaciones en matrices
    - Depende de las HUs de:
      - Crear relación en RA vs OP
      - Crear relación en RAA vs RA
      - Crear relación en RA vs EUR-ACE
    - Es una validación de **límite de entrada** aplicable a todas las matrices

14. **Diferencias vs Otras Validaciones**:
    - Esta HU no valida el contenido semántico de la justificación
    - Solo valida el **límite cuantitativo** de caracteres
    - Es una validación de **UI/UX** con feedback visual inmediato
    - No requiere backend validation hasta el guardado final