# CRITERIOS DE ACEPTACIÓN - HU: Filtrar Reporte Asignatura vs Criterios EURACE

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**C1: Facultad seleccionada**
- Estado: Sí / No
- Fuente: Campo de búsqueda "Facultad:" con autocompletado
- Valores observados: 
  - Estado inicial: "Buscar una facultad" (placeholder)
  - Texto intermedio: "Sis" (escribiendo)
  - Opciones desplegadas: "Sistemas", "Química y Agroindustria"
  - Valor seleccionado: "Sistemas"

**C2: Carrera seleccionada**
- Estado: Sí / No
- Fuente: Dropdown "Carrera:" dependiente de Facultad
- Valores observados:
  - Estado inicial: "Seleccionar una carrera" (deshabilitado)
  - Estado habilitado: "Seleccionar una carrera" (clickeable)
  - Opciones cuando Facultad="Sistemas": "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial"
  - Valor seleccionado: "Ingeniería de Software" o "Software"

**NOTA CRÍTICA:** Existe una **dependencia en cascada** donde Carrera solo puede seleccionarse si Facultad está seleccionada primero.

#### **Acciones del sistema identificadas:**

**A1: Mantener dropdown "Carrera:" deshabilitado**
- Condición: Facultad no seleccionada
- Observado en Imagen 4: Dropdown "Carrera:" en gris con texto "Seleccionar una carrera" no interactivo
- Resultado: Usuario no puede seleccionar carrera

**A2: Habilitar dropdown "Carrera:"**
- Condición: Facultad seleccionada
- Observado en transición entre imágenes 4→5→6
- Resultado: Dropdown cambia a estado activo, clickeable

**A3: Cargar opciones de carreras correspondientes a la facultad**
- Condición: Facultad seleccionada
- Observado en Imagen 6: Lista de carreras específicas de "Sistemas"
- Elementos: "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial"
- Resultado: Solo se muestran carreras que pertenecen a la facultad seleccionada

**A4: Actualizar valor del campo "Facultad:"**
- Condición: Usuario selecciona facultad del autocompletado
- Observado: Campo muestra "Sistemas" como valor final
- Resultado: Texto del campo se actualiza

**A5: Actualizar valor del dropdown "Carrera:"**
- Condición: Usuario selecciona carrera del dropdown
- Observado en Imagen 7: Dropdown muestra "Ingeniería de Software"
- Resultado: Texto del dropdown se actualiza con la selección

**A6: Resetear carrera cuando cambia facultad**
- Condición: Usuario cambia de facultad después de haber seleccionado una carrera
- Comportamiento esperado (no explícitamente visible pero inferido por lógica de dependencia)
- Resultado: Dropdown "Carrera:" vuelve a "Seleccionar una carrera" y se cargan nuevas opciones

**A7: Habilitar generación de reporte**
- Condición: Facultad Y Carrera seleccionadas (+ niveles de aporte)
- Observado en Imágenes 7-9: Matriz visible con datos
- Resultado: El sistema puede proceder a generar el reporte

**A8: Mostrar autocompletado de facultades**
- Condición: Usuario escribe en campo "Facultad:"
- Observado en Imagen 5: Al escribir "Sis" aparecen "Sistemas" y "Química y Agroindustria"
- Resultado: Lista filtrada de facultades

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 2 condiciones binarias: 2^2 = **4 reglas**

| Regla | C1: Facultad | C2: Carrera | Acción del Sistema |
|-------|--------------|-------------|-------------------|
| R1    | No           | No          | A1: Mantener Carrera deshabilitada |
| R2    | No           | Sí          | IMPOSIBLE* - Carrera no puede seleccionarse sin Facultad |
| R3    | Sí           | No          | A2 + A3 + A4: Habilitar Carrera + Cargar opciones + Actualizar Facultad |
| R4    | Sí           | Sí          | A2 + A3 + A4 + A5 + A7: Todos los filtros completos, habilitar reporte |

*Nota: R2 es técnicamente imposible debido a la dependencia en cascada implementada en la UI (Carrera está deshabilitada cuando no hay Facultad).

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Regla R1:** Estado inicial sin ningún filtro seleccionado. Carrera permanece deshabilitada. **Se mantiene como M1**.

2. **Regla R2:** Estado imposible por restricción de UI. La dependencia en cascada previene este estado. **Se elimina por ser imposible**.

3. **Regla R3:** Facultad seleccionada pero Carrera no. Momento crítico donde se habilita la cascada. **Se mantiene como M2**.

4. **Regla R4:** Ambos filtros completos, sistema listo para generar reporte (con niveles). **Se mantiene como M3** (HAPPY PATH).

#### **Tabla Minimizada:**

| Regla Min | C1: Facultad | C2: Carrera | Acción del Sistema |
|-----------|--------------|-------------|-------------------|
| **M1**    | No           | No          | A1: Mantener dropdown "Carrera:" deshabilitado |
| **M2**    | Sí           | No          | A2 + A3 + A4: Habilitar "Carrera:" + Cargar opciones + Actualizar campo Facultad |
| **M3**    | Sí           | Sí          | A2 + A3 + A4 + A5: Filtros completos listos para generar reporte |

**Resultado: 3 reglas minimizadas**

**Justificación:**
- M1: Estado inicial sin interacción
- M2: Estado intermedio con cascada habilitada (crítico para UX)
- M3: Estado completo con ambos filtros (prerequisito para reporte)
- R2 eliminada: Imposible por diseño de UI

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 3 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre estado inicial con Carrera deshabilitada
2. M2 → AC sobre habilitación de Carrera al seleccionar Facultad
3. M3 → AC sobre ambos filtros seleccionados (happy path)

**Análisis de criterios adicionales necesarios:**

Del análisis visual, identifico comportamientos críticos específicos de esta HU:

4. **Autocompletado de Facultad:** Imagen 5 muestra funcionalidad de búsqueda con "Sis" → "Sistemas", "Química y Agroindustria". Este es un componente clave para "facilitar la búsqueda" (objetivo de la HU).

5. **Desplegar opciones de Carrera:** Imagen 6 muestra dropdown desplegado con las 3 opciones. Validar que aparecen las carreras correctas.

6. **Cambio de facultad con reset de carrera:** Aunque no visible directamente, este comportamiento es crítico para mantener consistencia de datos (si usuario cambia Facultad después de seleccionar Carrera, debe resetear Carrera).

**Criterios a ELIMINAR por redundancia:**

Ninguno. Todos los criterios identificados son únicos y necesarios:
- M1, M2, M3 cubren la máquina de estados de los filtros
- Autocompletado (4) es funcionalidad específica observable
- Desplegar opciones (5) valida carga correcta de datos relacionados
- Reset en cambio (6) valida integridad de la relación jerárquica

**TOTAL FINAL: 6 Criterios de Aceptación**
- 3 de la tabla de decisión (M1, M2, M3)
- 3 adicionales por comportamientos específicos observados en prototipo

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

Aplicando la guía de estilo internalizada:

---

### **Escenario 1 – Estado inicial con carrera deshabilitada**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" **Y** soy un Coordinador de Carrera o CEI en el sistema,
**cuando** accedo al reporte sin haber seleccionado filtros,
**entonces** se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad" **Y** el campo está vacío y habilitado para escritura **Y** se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera" **Y** el dropdown "Carrera:" está en estado deshabilitado visualmente (color gris) **Y** el dropdown "Carrera:" no es clickeable **Y** no se puede abrir la lista de opciones de carrera **Y** es evidente que se debe seleccionar primero una facultad.

---

### **Escenario 2 – Buscar facultad con autocompletado**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" **Y** el campo "Facultad:" está vacío,
**cuando** escribo "Sis" en el campo de búsqueda "Facultad:",
**entonces** se despliega una lista de autocompletado debajo del campo **Y** la lista muestra opciones que coinciden con el texto ingresado: "Sistemas", "Química y Agroindustria" **Y** las opciones están ordenadas alfabéticamente o por relevancia **Y** puedo hacer clic en cualquiera de las opciones desplegadas **Y** el campo mantiene el texto "Sis" mientras se muestra el autocompletado **Y** la búsqueda es sensible a coincidencias parciales desde el inicio del nombre.

---

### **Escenario 3 – Seleccionar facultad y habilitar carrera**

**Dado que** he escrito en el campo "Facultad:" **Y** veo opciones en el autocompletado **Y** el dropdown "Carrera:" está deshabilitado,
**cuando** hago clic en la opción "Sistemas" del autocompletado,
**entonces** el campo "Facultad:" se actualiza con el valor "Sistemas" **Y** el autocompletado se cierra **Y** el dropdown "Carrera:" cambia a estado habilitado **Y** el dropdown "Carrera:" se vuelve clickeable con apariencia activa **Y** el texto del dropdown permanece como "Seleccionar una carrera" **Y** no se muestra contenido de matriz hasta completar todos los filtros requeridos.

---

### **Escenario 4 – Desplegar y visualizar opciones de carrera**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** el dropdown "Carrera:" está habilitado,
**cuando** hago clic en el dropdown "Carrera:",
**entonces** se despliega una lista con las carreras correspondientes a la facultad "Sistemas" **Y** la lista muestra las opciones: "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial" **Y** las opciones están claramente visibles y son clickeables **Y** cada opción está en una línea separada **Y** puedo desplazarme por la lista si hay más opciones que espacio visible **Y** solo se muestran carreras que pertenecen a la facultad seleccionada **Y** no aparecen carreras de otras facultades.

---

### **Escenario 5 – Seleccionar carrera completando filtros**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** el dropdown "Carrera:" está desplegado con opciones visibles,
**cuando** hago clic en la opción "Ingeniería de Software",
**entonces** el dropdown "Carrera:" se actualiza con el valor "Ingeniería de Software" o "Software" **Y** la lista de opciones se cierra **Y** el campo "Facultad:" mantiene el valor "Sistemas" **Y** ambos filtros (Facultad y Carrera) quedan configurados **Y** el sistema está listo para generar el reporte cuando se marquen los niveles de aporte **Y** los valores seleccionados permanecen visibles en los campos correspondientes.

---

### **Escenario 6 – Cambiar facultad con reseteo de carrera**

**Dado que** tengo la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas,
**cuando** cambio el valor del campo "Facultad:" borrando el texto **Y** escribo "Quí" **Y** selecciono "Química y Agroindustria" del autocompletado,
**entonces** el campo "Facultad:" se actualiza con "Química y Agroindustria" **Y** el dropdown "Carrera:" se resetea al estado "Seleccionar una carrera" **Y** el dropdown "Carrera:" permanece habilitado **Y** al hacer clic en "Carrera:" se despliegan las carreras correspondientes a "Química y Agroindustria" (diferentes a las de Sistemas) **Y** no se muestran las carreras de la facultad anterior **Y** debo seleccionar una nueva carrera de la nueva facultad para completar los filtros **Y** no se muestra contenido de matriz hasta reseleccionar la carrera.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 3 – Seleccionar facultad y habilitar carrera**

### **Justificación:**

Este criterio es el más crítico porque representa el **mecanismo core de la funcionalidad de filtrado en cascada** y valida directamente el objetivo de la HU: "facilitar la búsqueda del reporte". Las razones específicas son:

1. **Implementación de la dependencia jerárquica:** Este escenario valida el comportamiento fundamental de cascada Facultad→Carrera que es la esencia de esta HU. El sistema debe:
   - Reconocer que se seleccionó una Facultad
   - Cambiar el estado del dropdown Carrera de deshabilitado a habilitado
   - Cargar dinámicamente las opciones de carreras correspondientes
   - Mantener la consistencia de la relación jerárquica
   
   Sin este comportamiento funcionando, toda la lógica de filtrado por Facultad/Carrera falla.

2. **Punto crítico de transición de estados:** Este es el momento de cambio más importante en la máquina de estados de los filtros:
   - **Estado anterior:** M1 (Facultad=No, Carrera=No, Carrera deshabilitada)
   - **Estado posterior:** M2 (Facultad=Sí, Carrera=No, Carrera habilitada)
   - **Acción crítica:** Habilitar Carrera + Cargar opciones
   
   Si esta transición falla, el usuario queda bloqueado y no puede completar los filtros.

3. **Cumplimiento directo del valor de negocio:** El objetivo "facilitar la búsqueda del reporte" se materializa específicamente en:
   - Guiar al usuario paso a paso (primero Facultad, luego Carrera)
   - Prevenir errores (no permitir seleccionar Carrera sin Facultad)
   - Mostrar solo opciones relevantes (solo carreras de la facultad seleccionada)
   - Reducir carga cognitiva (no mostrar todas las carreras de todas las facultades)
   
   Este escenario valida que esta guía funciona correctamente.

4. **Validación de integración de datos crítica:** Este escenario confirma que:
   - Existe la relación Facultad→Carreras en la base de datos
   - Las queries de lookup funcionan correctamente
   - Las carreras se filtran por facultad_id
   - No hay carreras huérfanas o mal relacionadas
   - La carga de opciones es performante (no debería tardar >500ms)

5. **Punto de fallo de mayor impacto funcional:** Si este escenario falla:
   - El usuario no puede avanzar más allá de seleccionar Facultad
   - El filtrado por Carrera queda inoperativo
   - El reporte no puede generarse (requiere ambos filtros)
   - La funcionalidad completa de la HU se vuelve inútil
   - El usuario puede pensar que el sistema está roto (Carrera siempre deshabilitada)

6. **Punto de fallo de UX más crítico:** Los usuarios esperan que al seleccionar Facultad, el siguiente filtro se habilite inmediatamente. Si esto no ocurre:
   - Frustración del usuario (¿por qué no puedo seleccionar carrera?)
   - Confusión sobre qué hacer después
   - Posibles reportes de bug ("el dropdown de carrera no funciona")
   - Abandono de la funcionalidad

7. **Base para escenarios subsecuentes:** 
   - El Escenario 4 (desplegar opciones) depende de que Carrera esté habilitada
   - El Escenario 5 (seleccionar carrera) depende de que el Escenario 3 funcione
   - El Escenario 6 (cambio con reset) es una variación que también depende de esta lógica
   - Sin este escenario, los demás no tienen sentido

8. **Validación de lógica de negocio académica:** En el contexto universitario:
   - Las Facultades contienen múltiples Carreras
   - Una Carrera pertenece a una única Facultad
   - Esta jerarquía es fundamental para la estructura organizacional
   - El sistema debe respetar y reflejar esta jerarquía fielmente
   
   Este escenario valida que la implementación respeta el modelo organizacional real.

9. **Evidencia visual clara y específica:** Las imágenes documentan explícitamente esta transición:
   - Imagen 4: Carrera deshabilitada (antes)
   - Imagen 5: Usuario seleccionando Sistemas
   - Imagen 6: Carrera habilitada con opciones (después)
   
   Esta secuencia visual permite validación determinística del comportamiento.

10. **Patrón común en aplicaciones académicas:** El filtrado en cascada Facultad→Carrera es un patrón ubicuo en sistemas universitarios:
    - Matrícula de estudiantes
    - Gestión de programas académicos
    - Reportes de acreditación
    - Análisis curriculares
    
    Si falla aquí, probablemente falla en múltiples partes del sistema.

11. **Criticidad para accesibilidad:** El estado deshabilitado→habilitado debe ser:
    - Visualmente evidente (cambio de color, cursor)
    - Comunicado a lectores de pantalla (aria-disabled cambia a false)
    - Intuitivo para usuarios con diferentes habilidades
    
    Este escenario debe validar que la transición es accesible.

12. **Performance crítica:** La habilitación y carga de opciones debe ser:
    - Instantánea desde perspectiva del usuario (<200ms)
    - No bloquear la UI durante la carga
    - Manejar casos de lentitud de red
    - Mostrar feedback visual si tarda (spinner opcional)

**Recomendación de prueba prioritaria:**
- Automatizar verificación de estado deshabilitado→habilitado del dropdown
- Validar que el evento onChange de Facultad dispara la carga de Carreras
- Verificar que solo se cargan carreras de la facultad seleccionada (query con WHERE facultad_id)
- Probar con múltiples facultades para confirmar que cada una carga carreras diferentes
- Validar performance: tiempo desde selección de Facultad hasta Carrera habilitada
- Verificar accesibilidad: aria-disabled, estados focus, navegación por teclado
- Probar casos edge: facultad sin carreras, error de red durante carga
- Incluir en suite de regresión crítica (núcleo de funcionalidad)
- Validar en diferentes navegadores y dispositivos (comportamiento de dropdowns)

**Sin este escenario funcionando, la promesa de "facilitar la búsqueda del reporte" mediante filtrado estructurado no se cumple**, dejando al usuario sin forma de navegar eficientemente por la jerarquía Facultad→Carrera→Reporte. Este es el escenario que materializa la guía paso a paso que hace que el filtrado sea "fácil" en lugar de abrumador (mostrar todas las carreras sin contexto de facultad).