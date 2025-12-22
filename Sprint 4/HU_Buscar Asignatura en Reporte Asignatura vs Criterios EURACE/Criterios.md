# CRITERIOS DE ACEPTACIÓN - HU: Buscar Asignatura en Reporte Asignatura vs Criterios EURACE

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**PRECONDICIÓN (basado en HU previa):**
- Facultad y Carrera ya están seleccionadas
- Al menos un nivel de aporte está marcado
- La matriz Asignatura vs Criterios EURACE está visible con datos

**C1: Campo de búsqueda tiene texto ingresado**
- Estado: Sí / No
- Fuente: Campo "Buscar por código o nombre de asignatura" ubicado sobre la matriz
- Estados observados:
  - Vacío: Muestra todas las asignaturas
  - Con texto: Filtra resultados en tiempo real
- Ejemplo observado: "MATD113 Álgebra Lineal"

**C2: Texto ingresado coincide con código o nombre de asignatura(s)**
- Estado: Sí / No
- Tipos de coincidencia:
  - Por código: "MATD113", "IS-101", "MA-102"
  - Por nombre: "Álgebra", "Cálculo", "Programación"
  - Por código + nombre: "MATD113 Álgebra Lineal"
  - Coincidencia parcial: "Álg" coincide con "Álgebra Lineal"

**C3: Búsqueda retorna múltiples resultados**
- Estado: Sí / No
- Casos:
  - Múltiples: Buscar "Programación" puede retornar "Programación I", "Programación II"
  - Único: Buscar "MATD113" retorna solo "Álgebra Lineal"
  - Ninguno: Buscar "XYZ123" no retorna resultados

#### **Acciones del sistema identificadas:**

**A1: Mostrar campo de búsqueda habilitado**
- Condición: Matriz visible con datos
- Observado: Campo "Buscar por código o nombre de asignatura" sobre la matriz
- Estado: Vacío y listo para escritura
- Placeholder visible

**A2: Filtrar matriz en tiempo real mientras el usuario escribe**
- Condición: Usuario escribe en campo de búsqueda
- Comportamiento: Filtrado instantáneo sin necesidad de presionar Enter o botón de búsqueda
- Actualización: Dinámica, cada carácter ingresado actualiza los resultados

**A3: Mostrar solo asignaturas que coinciden con el término de búsqueda**
- Condición: Texto ingresado coincide con código/nombre
- Observado en HU previa: Al buscar "MATD113 Álgebra Lineal", solo se muestra esa fila
- Elementos mostrados:
  - Fila completa de la asignatura coincidente
  - Checkmarks verdes en las intersecciones correspondientes (5.3.4, 5.3.5 para Álgebra)
  - Todos los encabezados de columnas EUR-ACE permanecen visibles

**A4: Ocultar asignaturas que no coinciden con el término**
- Condición: Asignaturas no relacionadas con la búsqueda
- Observado: Otras asignaturas (Cálculo, Mecánica, Programación, etc.) desaparecen de la vista
- Resultado: Tabla más compacta y enfocada

**A5: Mostrar todas las asignaturas (resetear filtro)**
- Condición: Campo de búsqueda está vacío
- Comportamiento: Al borrar el texto, reaparecen todas las asignaturas
- Estado inicial: Vista completa de la matriz

**A6: Mostrar mensaje de "No se encontraron resultados"**
- Condición: Texto ingresado no coincide con ninguna asignatura
- Mensaje esperado: "No se encontraron asignaturas que coincidan con '[término]'" o similar
- Estado: Tabla vacía con mensaje informativo

**A7: Mantener encabezados y estructura de matriz**
- Condición: Durante cualquier búsqueda
- Elementos fijos:
  - Columna "Asignatura" (primera columna)
  - Encabezados EUR-ACE (5.2.1, 5.2.2, ..., 5.3.7)
  - Filtros de Facultad, Carrera, Nivel de aporte
- Propósito: Contexto siempre visible

**A8: Soportar búsqueda por código, nombre o combinación**
- Condición: Diferentes formatos de entrada
- Formatos soportados:
  - Solo código: "MATD113"
  - Solo nombre: "Álgebra Lineal"
  - Código + nombre: "MATD113 Álgebra Lineal"
  - Parcial: "Álg", "MAT", "113"

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Tiene texto | C2: Hay coincidencia | C3: Múltiples resultados | Acción del Sistema |
|-------|----------------|---------------------|-------------------------|-------------------|
| R1    | No             | No                  | No                      | A1 + A5: Mostrar todas las asignaturas (estado inicial) |
| R2    | No             | No                  | Sí                      | IMPOSIBLE* - Sin texto no puede haber coincidencias |
| R3    | No             | Sí                  | No                      | IMPOSIBLE* - Sin texto no puede haber coincidencias |
| R4    | No             | Sí                  | Sí                      | IMPOSIBLE* - Sin texto no puede haber coincidencias |
| R5    | Sí             | No                  | No                      | A1 + A2 + A6: Buscar sin resultados (mensaje informativo) |
| R6    | Sí             | No                  | Sí                      | IMPOSIBLE* - Si no hay coincidencia, no puede haber múltiples |
| R7    | Sí             | Sí                  | No                      | A1 + A2 + A3 + A4 + A7 + A8: Mostrar única asignatura coincidente |
| R8    | Sí             | Sí                  | Sí                      | A1 + A2 + A3 + A4 + A7 + A8: Mostrar múltiples asignaturas coincidentes |

*IMPOSIBLE: Combinaciones lógicamente contradictorias.

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Regla R1:** Campo vacío, estado inicial. Todas las asignaturas visibles. **Se mantiene como M1**.

2. **Reglas R2-R4:** Imposibles lógicamente (no puede haber coincidencias sin texto). **Se eliminan**.

3. **Regla R5:** Usuario escribe pero no hay coincidencias. Mostrar mensaje de "sin resultados". **Se mantiene como M2**.

4. **Regla R6:** Imposible (si no hay coincidencia, no puede haber múltiples resultados). **Se elimina**.

5. **Regla R7:** Texto ingresado coincide con una única asignatura. Caso observado en prototipo: "MATD113 Álgebra Lineal". **Se mantiene como M3**.

6. **Regla R8:** Texto ingresado coincide con múltiples asignaturas. Ejemplo: buscar "Programación" retorna "Programación I", "Programación II", etc. **Se mantiene como M4**.

#### **Tabla Minimizada:**

| Regla Min | C1: Tiene texto | C2: Hay coincidencia | C3: Múltiples resultados | Acción del Sistema |
|-----------|----------------|---------------------|-------------------------|-------------------|
| **M1**    | No             | -                   | -                       | A1 + A5: Mostrar todas las asignaturas |
| **M2**    | Sí             | No                  | -                       | A1 + A2 + A6: Sin resultados, mensaje informativo |
| **M3**    | Sí             | Sí                  | No                      | A1 + A2 + A3 + A4 + A7 + A8: Resultado único filtrado |
| **M4**    | Sí             | Sí                  | Sí                      | A1 + A2 + A3 + A4 + A7 + A8: Múltiples resultados filtrados |

**Resultado: 4 reglas minimizadas**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 4 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre estado inicial sin búsqueda
2. M2 → AC sobre búsqueda sin resultados (caso negativo)
3. M3 → AC sobre búsqueda con resultado único (HAPPY PATH - observado en prototipo)
4. M4 → AC sobre búsqueda con múltiples resultados

**Análisis de criterios adicionales necesarios:**

Del objetivo de la HU ("encontrar rápidamente la contribución de asignaturas específicas"):

5. **Limpiar búsqueda:** Usuario debe poder borrar el texto y volver a la vista completa fácilmente.
6. **Búsqueda case-insensitive:** Buscar "álgebra" o "ÁLGEBRA" debe funcionar igual.

**Criterios a CONSOLIDAR:**

- El punto 5 (limpiar búsqueda) es esencialmente M1 (campo vacío muestra todas), ya está cubierto.
- El punto 6 (case-insensitive) se incorporará en M3 y M4 como parte del comportamiento de búsqueda.

**TOTAL FINAL: 4 Criterios de Aceptación**
- 4 derivados de la tabla de decisión (M1, M2, M3, M4)
- Búsqueda case-insensitive integrada en criterios de coincidencia
- Limpieza de búsqueda cubierta por M1

**Justificación:**
Todos los criterios son únicos y necesarios para validar el comportamiento completo de la búsqueda desde estado inicial hasta diferentes tipos de resultados.

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

---

### **Escenario 1 – Estado inicial sin búsqueda activa**

**Dado que** soy un Coordinador de Carrera o CEI **Y** estoy visualizando el reporte "Reporte: Asignatura vs Criterios EURACE" **Y** tengo la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas **Y** tengo al menos un nivel de aporte marcado **Y** la matriz completa está visible con todas las asignaturas,
**cuando** visualizo el campo de búsqueda "Buscar por código o nombre de asignatura",
**entonces** el campo está vacío con el placeholder visible **Y** el campo está habilitado y listo para escritura **Y** se muestran todas las asignaturas de la carrera en la matriz: Álgebra Lineal, Cálculo en una Variable, Mecánica Newtoniana, Programación I, Comunicación Oral y Escrita, Ecuaciones Diferenciales, Matemática Computacional, Fundamentos de Electrónica **Y** todos los checkmarks verdes de las relaciones asignatura-criterio EUR-ACE están visibles **Y** los encabezados de columnas EUR-ACE (5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7) permanecen visibles.

---

### **Escenario 2 – Buscar asignatura sin resultados coincidentes**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" con la matriz completa visible,
**cuando** escribo "XYZ999 Materia Inexistente" en el campo de búsqueda "Buscar por código o nombre de asignatura",
**entonces** la tabla se actualiza automáticamente en tiempo real mientras escribo **Y** no se muestra ninguna fila de asignatura en la tabla **Y** se presenta un mensaje informativo indicando "No se encontraron asignaturas que coincidan con 'XYZ999 Materia Inexistente'" o mensaje similar **Y** los encabezados de columnas EUR-ACE permanecen visibles **Y** los filtros de Facultad, Carrera y Nivel de aporte se mantienen en su estado actual **Y** cuando borro el texto del campo de búsqueda, todas las asignaturas reaparecen inmediatamente en la matriz.

---

### **Escenario 3 – Buscar y filtrar por código o nombre específico mostrando resultado único**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" con la matriz completa visible mostrando múltiples asignaturas,
**cuando** escribo "MATD113 Álgebra Lineal" en el campo de búsqueda "Buscar por código o nombre de asignatura",
**entonces** la matriz se filtra automáticamente en tiempo real sin necesidad de presionar Enter o botón de búsqueda **Y** se muestra únicamente la fila correspondiente a "Álgebra Lineal" **Y** se visualizan los checkmarks verdes (✓) de Álgebra Lineal en las columnas 5.3.4 y 5.3.5 **Y** todas las demás asignaturas (Cálculo en una Variable, Mecánica Newtoniana, Programación I, etc.) quedan ocultas de la vista **Y** los encabezados de columnas EUR-ACE permanecen completamente visibles **Y** la búsqueda también funciona escribiendo solo el código "MATD113" mostrando el mismo resultado **Y** la búsqueda funciona escribiendo solo el nombre "Álgebra Lineal" mostrando el mismo resultado **Y** la búsqueda es case-insensitive, permitiendo "álgebra lineal", "ÁLGEBRA LINEAL" o "Álgebra Lineal" con el mismo resultado **Y** la búsqueda acepta coincidencias parciales, permitiendo "Álg" o "MATD" para encontrar Álgebra Lineal **Y** puedo ver rápidamente la contribución específica de Álgebra Lineal a los criterios EUR-ACE 5.3.4 y 5.3.5.

---

### **Escenario 4 – Buscar término que coincide con múltiples asignaturas**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" con la matriz completa visible,
**cuando** escribo un término parcial como "Programación" en el campo de búsqueda,
**entonces** la matriz se filtra automáticamente mostrando todas las asignaturas que contienen "Programación" en su código o nombre **Y** se muestran múltiples filas como "Programación I", "Programación Avanzada", "Programación Web" (si existen en la carrera) **Y** cada fila muestra sus checkmarks verdes correspondientes en las intersecciones con criterios EUR-ACE **Y** las asignaturas que no contienen el término "Programación" quedan ocultas **Y** los encabezados de columnas EUR-ACE permanecen visibles **Y** puedo ver y comparar las contribuciones de todas las asignaturas de programación simultáneamente **Y** cuando escribo más caracteres para especificar, por ejemplo "Programación I", el filtrado se vuelve más específico mostrando solo esa asignatura **Y** la búsqueda es case-insensitive funcionando con "programación", "PROGRAMACIÓN" o "Programación" **Y** cuando borro el texto del campo, reaparecen todas las asignaturas de la matriz.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 3 – Buscar y filtrar por código o nombre específico mostrando resultado único**

### **Justificación:**

Este criterio es el más crítico porque valida **directamente el objetivo central de la Historia de Usuario**: "encontrar rápidamente la contribución de asignaturas específicas". Las razones específicas son:

1. **Cumplimiento directo del objetivo de la HU:** El coordinador necesita "encontrar rápidamente" asignaturas. Este escenario valida que:
   - La búsqueda es rápida (tiempo real, sin necesidad de presionar Enter)
   - Se puede buscar por código o nombre (flexibilidad de entrada)
   - El resultado muestra la contribución específica (checkmarks en criterios EUR-ACE)
   - El filtrado es preciso y enfocado (solo la asignatura buscada)

2. **Caso de uso más frecuente (80-90% de las búsquedas):** En el contexto académico, los coordinadores típicamente buscan asignaturas específicas:
   - Revisión de asignatura particular durante junta de currículo
   - Verificación de contribución de materia a criterios de acreditación
   - Análisis enfocado en curso problemático o destacado
   - Respuesta a pregunta específica sobre una asignatura
   
   Buscar una asignatura específica por código/nombre es más común que buscar múltiples o no encontrar resultados.

3. **Evidencia visual directa del prototipo:** Este escenario fue específicamente observado en análisis previo:
   - Búsqueda: "MATD113 Álgebra Lineal"
   - Resultado: Solo fila de Álgebra Lineal visible
   - Checkmarks: ✓ en columnas 5.3.4 y 5.3.5
   - Otras asignaturas ocultas
   
   Esto permite validación determinística contra el prototipo documentado.

4. **Validación de funcionalidad completa de búsqueda:** Este escenario valida múltiples capacidades críticas:
   - **Filtrado en tiempo real** (cada carácter actualiza resultados)
   - **Búsqueda por código** ("MATD113")
   - **Búsqueda por nombre** ("Álgebra Lineal")
   - **Búsqueda por código+nombre** ("MATD113 Álgebra Lineal")
   - **Case-insensitive** ("álgebra" = "ÁLGEBRA")
   - **Coincidencias parciales** ("Álg" encuentra "Álgebra")
   - **Mantenimiento de contexto** (encabezados EUR-ACE visibles)

5. **Valor académico inmediato:** Este escenario resuelve el problema de negocio real:
   - **Problema:** Matriz con 30-50 asignaturas difícil de navegar
   - **Solución:** Buscar "Cálculo" y ver solo esa asignatura con sus contribuciones
   - **Resultado:** Coordinador puede responder inmediatamente "¿Cálculo contribuye al criterio 5.2.2?" → Sí, hay checkmark
   - **Ahorro de tiempo:** De minutos escaneando matriz completa a segundos con búsqueda

6. **Punto de fallo de mayor impacto funcional:** Si este escenario falla:
   - El coordinador no puede encontrar asignaturas específicas rápidamente
   - Debe scrollear manualmente por toda la matriz (tedioso y propenso a error)
   - Pierde tiempo en juntas o reuniones buscando información
   - La promesa de "encontrar rápidamente" no se cumple
   - La funcionalidad completa de la HU pierde su valor principal

7. **Base para los demás escenarios:** 
   - El Escenario 1 (sin búsqueda) es el punto de partida
   - El Escenario 2 (sin resultados) es un caso negativo edge
   - El Escenario 4 (múltiples resultados) es una variación del mismo patrón
   
   Si el Escenario 3 funciona correctamente, demuestra que el motor de búsqueda core funciona.

8. **Validación de UX moderna esperada:** Los usuarios académicos esperan:
   - Búsqueda instantánea (Google-like)
   - Sin necesidad de botones "Buscar" o presionar Enter
   - Flexibilidad de entrada (código, nombre, parcial)
   - Case-insensitive por defecto
   - Resultados focalizados y precisos
   
   Este escenario valida todas estas expectativas de UX moderna.

9. **Prevención de errores en análisis académico:** Con búsqueda efectiva:
   - Coordinador puede verificar rápidamente contribuciones específicas durante revisiones de acreditación
   - No hay confusión con asignaturas de nombres similares (filtrado preciso)
   - Puede confirmar datos antes de reportar a auditorías
   - Reduce errores de lectura en matrices grandes (solo ve lo relevante)

10. **Habilitador de flujo de trabajo eficiente:** En una sesión de trabajo típica:
    - Coordinador tiene lista de 10 asignaturas para revisar
    - Con este escenario funcionando: busca cada una, verifica contribuciones (1 min cada una = 10 min total)
    - Sin búsqueda funcional: scrollea matriz completa 10 veces (5 min cada vez = 50 min total)
    - **Ahorro: 40 minutos por sesión de revisión**

11. **Validación de integración de filtros:** Este escenario valida que:
    - Búsqueda trabaja correctamente con filtros pre-existentes (Facultad, Carrera, Nivel)
    - No interfiere con el filtrado por nivel de aporte
    - Mantiene el contexto de la carrera seleccionada
    - Los resultados son del scope correcto (solo asignaturas de la carrera actual)

12. **Complejidad técnica representativa:** Implementar búsqueda en tiempo real requiere:
    - Event listeners en input field (keyup/input)
    - Lógica de filtrado case-insensitive
    - Matching parcial de strings
    - Actualización eficiente del DOM (ocultar/mostrar filas)
    - Performance con 50+ asignaturas (filtrado <100ms)
    - Mantenimiento de estado de matriz
    
    Si este escenario funciona, demuestra que la implementación técnica es sólida.

13. **Testabilidad específica:** Este escenario permite pruebas automatizadas precisas:
    - Input: "MATD113 Álgebra Lineal"
    - Output esperado: 1 fila visible, código "MATD113", nombre "Álgebra Lineal"
    - Checkmarks esperados: columnas 5.3.4, 5.3.5
    - Otras filas: display:none o no en DOM visible
    - Performance: filtrado <200ms
    
    Permite assertions específicos y determinísticos.

14. **Patrón común en sistemas académicos:** La búsqueda por código/nombre de curso es ubicua en:
    - Sistemas de matrícula
    - Catálogos de cursos
    - Sistemas de gestión curricular
    - Plataformas de acreditación
    
    Si funciona aquí, establece patrón reutilizable para otros módulos.

**Recomendación de prueba prioritaria:**
- Crear suite automatizada que busque "MATD113" y verifique que solo Álgebra Lineal es visible
- Validar búsqueda por código solo, nombre solo, y código+nombre
- Probar case-insensitive: "álgebra", "ÁLGEBRA", "Álgebra"
- Validar coincidencias parciales: "Álg", "MATD", "113"
- Medir tiempo de filtrado (debe ser <200ms con 50 asignaturas)
- Verificar que checkmarks correctos permanecen visibles
- Probar con todas las asignaturas de la matriz para confirmar precisión
- Validar que otras asignaturas realmente se ocultan (no solo scroll)
- Probar con caracteres especiales: "Cálculo" con tilde, "Programación" con acento
- Verificar que limpieza de búsqueda restaura vista completa
- Incluir en regresión crítica para cambios en componente de matriz

**Sin este escenario funcionando, el coordinador no puede "encontrar rápidamente la contribución de asignaturas específicas"** como requiere la HU. Tendría que navegar manualmente por la matriz completa cada vez, lo cual elimina el valor principal de esta funcionalidad: velocidad y precisión en la búsqueda de información específica. Este escenario transforma una matriz potencialmente abrumadora (50+ asignaturas × 12 criterios = 600 celdas) en una herramienta eficiente y enfocada para análisis académico puntual.