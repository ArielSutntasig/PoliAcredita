# CRITERIOS DE ACEPTACIÓN - HU: Filtrar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**C1: Facultad seleccionada**
- Estado: Sí / No
- Fuente: Campo de búsqueda "Facultad:" con autocompletado
- Valores observados en imágenes 11-15 (Coordinador):
  - Estado inicial: "Buscar una facultad" (placeholder)
  - Valor seleccionado: "Sistemas"

**C2: Carrera seleccionada**
- Estado: Sí / No
- Fuente: Dropdown "Carrera:" dependiente de Facultad
- Valores observados:
  - Estado inicial: "Seleccionar una carrera" (deshabilitado)
  - Estado habilitado: "Seleccionar una carrera" (clickeable después de seleccionar Facultad)
  - Valor seleccionado: "Software"

**NOTA CRÍTICA:** Existe una **dependencia en cascada** donde Carrera solo puede seleccionarse si Facultad está seleccionada primero. Este es el patrón de filtrado jerárquico observado consistentemente en ambos reportes.

#### **Acciones del sistema identificadas:**

**A1: Mantener dropdown "Carrera:" deshabilitado**
- Condición: Facultad no seleccionada
- Observado en Imagen 11: Dropdown "Carrera:" en estado deshabilitado con texto "Seleccionar una carrera"
- Resultado: Usuario no puede interactuar con el dropdown

**A2: Habilitar dropdown "Carrera:"**
- Condición: Facultad seleccionada
- Comportamiento observado en secuencia de imágenes
- Resultado: Dropdown cambia a estado activo, puede desplegarse

**A3: Cargar opciones de carreras específicas de la facultad**
- Condición: Facultad seleccionada
- Opciones para "Sistemas": "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial"
- Resultado: Solo se muestran carreras que pertenecen a la facultad seleccionada

**A4: Actualizar valor del campo "Facultad:"**
- Condición: Usuario selecciona facultad del autocompletado
- Observado: Campo muestra "Sistemas"
- Resultado: Valor visible en el campo

**A5: Actualizar valor del dropdown "Carrera:"**
- Condición: Usuario selecciona carrera del dropdown
- Observado en Imágenes 12-15: Dropdown muestra "Software"
- Resultado: Valor visible en dropdown

**A6: Preparar sistema para generación de tabla**
- Condición: Facultad Y Carrera seleccionadas
- Observado: Con ambos filtros + niveles marcados, aparece la tabla de trazabilidad OP-RA-Asignaturas
- Resultado: Sistema tiene contexto completo para filtrar datos del reporte

**A7: Resetear carrera al cambiar facultad**
- Condición: Usuario cambia facultad después de haber seleccionado carrera
- Comportamiento esperado por lógica de dependencia
- Resultado: Dropdown "Carrera:" vuelve a "Seleccionar una carrera", se cargan nuevas opciones

**A8: Filtrar datos del reporte por carrera seleccionada**
- Condición: Carrera seleccionada + niveles marcados
- Observado en Imágenes 12-15: Tabla muestra datos específicos de "Software"
- Contenido: OPP1-OPP5 de Software, RA específicos, asignaturas específicas
- Resultado: Solo se muestran objetivos, resultados y asignaturas de la carrera filtrada

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 2 condiciones binarias: 2^2 = **4 reglas**

| Regla | C1: Facultad | C2: Carrera | Acción del Sistema |
|-------|--------------|-------------|-------------------|
| R1    | No           | No          | A1: Mantener Carrera deshabilitada |
| R2    | No           | Sí          | IMPOSIBLE* - Carrera no puede seleccionarse sin Facultad |
| R3    | Sí           | No          | A2 + A3 + A4: Habilitar Carrera + Cargar opciones + Actualizar Facultad |
| R4    | Sí           | Sí          | A2 + A3 + A4 + A5 + A6: Filtros completos, preparar tabla |

*Nota: R2 es técnicamente imposible debido a la dependencia en cascada implementada en la UI.

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Regla R1:** Estado inicial sin ningún filtro. Carrera deshabilitada. **Se mantiene como M1**.

2. **Regla R2:** Estado imposible por restricción de UI (dependencia en cascada). **Se elimina por imposibilidad técnica**.

3. **Regla R3:** Facultad seleccionada, Carrera aún no. Momento de habilitación de cascada. **Se mantiene como M2**.

4. **Regla R4:** Ambos filtros completos, sistema listo para generar reporte específico de la carrera. **Se mantiene como M3** (HAPPY PATH).

#### **Tabla Minimizada:**

| Regla Min | C1: Facultad | C2: Carrera | Acción del Sistema |
|-----------|--------------|-------------|-------------------|
| **M1**    | No           | No          | A1: Mantener dropdown "Carrera:" deshabilitado |
| **M2**    | Sí           | No          | A2 + A3 + A4: Habilitar "Carrera:" + Cargar opciones de carreras de la facultad |
| **M3**    | Sí           | Sí          | A2 + A3 + A4 + A5 + A6: Filtros completos, preparar generación de reporte por carrera |

**Resultado: 3 reglas minimizadas**

**Justificación:**
- M1: Estado inicial
- M2: Estado intermedio con cascada habilitada
- M3: Estado completo con ambos filtros (happy path)
- R2 eliminada: Imposible por diseño de UI

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 3 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre estado inicial con Carrera deshabilitada
2. M2 → AC sobre habilitación de Carrera al seleccionar Facultad (CRÍTICO para cascada)
3. M3 → AC sobre ambos filtros seleccionados preparando sistema para reporte filtrado (HAPPY PATH)

**Análisis de criterios adicionales necesarios:**

Del análisis visual y objetivo de la HU ("analizar la alineación de un programa de estudios específico"), identifico:

4. **Verificar que datos mostrados corresponden a la carrera:** Cuando se genera la tabla (con niveles), debe mostrar solo OP, RA y asignaturas de la carrera seleccionada. Esto valida el filtrado efectivo.

5. **Cambio de carrera dentro de la misma facultad:** Usuario puede cambiar de "Ingeniería de Software" a "Ingeniería Ciencias de la Computación" sin cambiar facultad. La tabla debe actualizarse con datos de la nueva carrera.

6. **Cambio de facultad con reset de carrera:** Al cambiar facultad, resetear carrera y cargar nuevas opciones. (Similar a HU anterior, pero aplicado a este reporte específico).

**Criterios a ELIMINAR por redundancia:**

- El criterio 6 (cambio de facultad con reset) es idéntico en comportamiento al Escenario 6 de la HU anterior. Si bien es importante, su comportamiento es genérico (mismo componente UI). **ELIMINADO para evitar redundancia entre HUs**, asumiendo que si funciona en un reporte, funciona en todos.

**Criterios consolidados:**

Los criterios 4 y 5 son específicos del objetivo "analizar alineación de programa específico":
- Criterio 4 valida que el filtrado por carrera realmente funciona en el contenido de la tabla
- Criterio 5 valida que el usuario puede comparar entre carreras de la misma facultad fácilmente

**TOTAL FINAL: 5 Criterios de Aceptación**
- 3 de la tabla de decisión (M1, M2, M3)
- 2 adicionales específicos del objetivo de análisis por carrera

**Justificación de eliminación:**
- **Cambio de facultad con reset:** Redundante con HU de "Filtrar Reporte Asignatura vs Criterios EURACE", ya que es el mismo comportamiento del componente UI. No aporta valor específico a esta HU.

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

Aplicando la guía de estilo internalizada:

---

### **Escenario 1 – Estado inicial con carrera deshabilitada**

**Dado que** estoy en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" **Y** soy un Coordinador de Carrera en el sistema,
**cuando** accedo al reporte sin haber seleccionado filtros,
**entonces** se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad" **Y** el campo está vacío y habilitado para escritura **Y** se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera" **Y** el dropdown "Carrera:" está en estado deshabilitado visualmente **Y** el dropdown "Carrera:" no es clickeable **Y** no se puede abrir la lista de opciones de carrera **Y** no se muestran encabezados de tabla ni contenido de trazabilidad **Y** es evidente que se debe seleccionar primero una facultad para continuar.

---

### **Escenario 2 – Seleccionar facultad y habilitar carrera**

**Dado que** estoy en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" **Y** el dropdown "Carrera:" está deshabilitado,
**cuando** escribo en el campo "Facultad:" **Y** selecciono "Sistemas" del autocompletado,
**entonces** el campo "Facultad:" se actualiza con el valor "Sistemas" **Y** el dropdown "Carrera:" cambia a estado habilitado **Y** el dropdown "Carrera:" se vuelve clickeable con apariencia activa **Y** al hacer clic en "Carrera:" se despliegan las opciones de carreras pertenecientes a "Sistemas": "Ingeniería de Software", "Ingeniería Ciencias de la Computación", "Ingeniería en Inteligencia Artificial" **Y** solo se muestran carreras que pertenecen a la facultad seleccionada **Y** el texto del dropdown permanece como "Seleccionar una carrera" hasta que se haga una selección **Y** no se muestra contenido de tabla hasta completar todos los filtros.

---

### **Escenario 3 – Seleccionar carrera completando filtros**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** el dropdown "Carrera:" está habilitado,
**cuando** hago clic en el dropdown "Carrera:" **Y** selecciono "Software" de las opciones disponibles,
**entonces** el dropdown "Carrera:" se actualiza con el valor "Software" **Y** la lista de opciones se cierra **Y** el campo "Facultad:" mantiene el valor "Sistemas" **Y** ambos filtros (Facultad y Carrera) quedan configurados **Y** el sistema está preparado para generar la tabla de trazabilidad cuando se marquen los niveles de aporte **Y** los valores seleccionados permanecen visibles y estables en los campos correspondientes.

---

### **Escenario 4 – Generar tabla filtrada por carrera específica**

**Dado que** tengo la facultad "Sistemas" y carrera "Software" seleccionadas **Y** marco al menos un checkbox de nivel de aporte (Alto, Medio o Bajo),
**cuando** se genera la tabla de trazabilidad,
**entonces** se muestran únicamente los objetivos de carrera (OP) que pertenecen a "Software" (OPP1, OPP2, OPP3, OPP5) **Y** se presentan únicamente los resultados de aprendizaje (RA) específicos de la carrera Software (RG1, RG3, RE4, RG4, RE1, RE2, RE3, RG2) **Y** se muestran únicamente las asignaturas correspondientes a la carrera Software (IS-101, IS-305, MA-102, IS-203, GE-401, HU-301, IS-306, IS-501, IS-402, MA-201, CO-101, IS-403) **Y** no se muestran objetivos de otras carreras de la facultad **Y** no se muestran asignaturas de otras carreras **Y** la tabla presenta la trazabilidad completa OP→RA→Asignaturas exclusivamente del programa de estudios "Software" **Y** el contenido permite analizar específicamente la alineación del programa seleccionado.

---

### **Escenario 5 – Cambiar carrera dentro de la misma facultad**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** tengo la carrera "Software" seleccionada **Y** la tabla de trazabilidad está visible con datos de Software,
**cuando** hago clic en el dropdown "Carrera:" **Y** selecciono "Ingeniería Ciencias de la Computación" de las opciones,
**entonces** el dropdown "Carrera:" se actualiza con "Ingeniería Ciencias de la Computación" **Y** el campo "Facultad:" mantiene el valor "Sistemas" **Y** la tabla de trazabilidad se actualiza automáticamente sin recargar la página **Y** se muestran únicamente los objetivos, resultados de aprendizaje y asignaturas correspondientes a "Ingeniería Ciencias de la Computación" **Y** se ocultan todos los datos de "Software" **Y** los checkboxes de nivel de aporte mantienen su estado de selección **Y** el sistema permite comparar fácilmente entre carreras de la misma facultad cambiando solo el filtro de carrera.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 4 – Generar tabla filtrada por carrera específica**

### **Justificación:**

Este criterio es el más crítico porque valida **el objetivo central de la Historia de Usuario**: "analizar la alineación de un programa de estudios específico". Es el punto donde el filtrado por carrera se materializa en contenido específico y útil. Las razones específicas son:

1. **Cumplimiento directo del valor de negocio:** El objetivo de esta HU es permitir que el Coordinador de Carrera analice la alineación curricular de **su** programa específico, no de toda la facultad. Este escenario valida que:
   - Solo se muestran OP del programa seleccionado (no de otras carreras)
   - Solo se muestran RA específicos de ese programa
   - Solo se muestran asignaturas del plan de estudios de esa carrera
   - El análisis es preciso y enfocado en el programa bajo responsabilidad del coordinador

2. **Validación de filtrado multinivel complejo:** Este escenario verifica que el sistema filtra correctamente en tres niveles de entidades académicas:
   - **Nivel 1 (OP):** Objetivos del Programa de Software (no de Computación ni IA)
   - **Nivel 2 (RA):** Resultados de Aprendizaje definidos para Software
   - **Nivel 3 (Asignaturas):** Cursos del plan de estudios de Software (IS-101, GE-401, etc.)
   
   Si cualquiera de estos filtros falla, se mostrarían datos incorrectos de otras carreras.

3. **Integridad de trazabilidad por carrera:** Valida que la cadena completa OP→RA→Asignatura mantiene coherencia:
   - Los RA mostrados realmente contribuyen a los OP de esa carrera
   - Las asignaturas mostradas realmente desarrollan esos RA
   - No hay "contaminación" de datos de otras carreras
   - La trazabilidad es auditablemente correcta para procesos de acreditación por programa

4. **Punto de fallo de mayor impacto académico:** Si este escenario falla:
   - El coordinador podría tomar decisiones basándose en datos de otra carrera (error crítico)
   - El análisis de alineación curricular sería inválido
   - Las evidencias para acreditación específica del programa serían incorrectas
   - Se podrían identificar incorrectamente fortalezas/debilidades del programa
   - Las decisiones de mejora curricular estarían mal fundamentadas

5. **Validación de modelo de datos académico:** Este escenario confirma que:
   - Las relaciones Carrera→OP están correctamente establecidas
   - Las relaciones OP→RA tienen el atributo carrera_id correcto
   - Las relaciones RA→Asignatura filtran por programa académico
   - Las queries SQL incluyen el WHERE carrera_id = [seleccionado]
   - No hay inconsistencias en la base de datos (ej: OP asignados a múltiples carreras incorrectamente)

6. **Diferenciación entre programas académicos:** En una facultad como Sistemas con 3 carreras:
   - Software: Enfoque en desarrollo de aplicaciones, metodologías ágiles
   - Computación: Enfoque más teórico, algoritmos, matemáticas
   - Inteligencia Artificial: Enfoque en ML, redes neuronales
   
   Cada carrera tiene objetivos, RA y asignaturas distintas. Este escenario valida que el sistema respeta y muestra estas diferencias correctamente.

7. **Base para análisis comparativo entre programas:** Este filtrado permite:
   - Comparar la estructura curricular entre Software vs Computación
   - Identificar asignaturas compartidas vs específicas de cada programa
   - Evaluar diferencias en la cobertura de objetivos entre carreras
   - Benchmark de alineación curricular entre programas similares

8. **Evidencia específica en prototipo:** Las Imágenes 12-15 muestran datos específicos de "Software":
   - OPP1: "Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de **software**..." (específico de Software, no de Computación)
   - Asignaturas como IS-101, IS-305 (Ingeniería de Software), GE-401 (Gestión)
   - Los códigos IS-xxx sugieren asignaturas de Ingeniería de Software
   
   Esto permite validación determinística del filtrado correcto.

9. **Dependencia crítica de escenarios previos:** 
   - Los Escenarios 1-3 son prerequisitos (seleccionar filtros)
   - El Escenario 5 (cambio de carrera) depende de que este escenario funcione
   - Sin este escenario funcionando, los filtros no tienen efecto real
   - Es el "momento de verdad" donde se demuestra que el filtrado realmente funciona

10. **Complejidad de consultas SQL:** Las queries para este reporte son complejas:
    ```sql
    SELECT op.*, ra.*, asig.*
    FROM objetivos_programa op
    JOIN resultados_aprendizaje ra ON ra.objetivo_id = op.id
    JOIN rel_ra_asignatura rel ON rel.ra_id = ra.id
    JOIN asignaturas asig ON asig.id = rel.asignatura_id
    WHERE op.carrera_id = ?
    AND rel.nivel_aporte IN (?)
    ```
    Este escenario valida que todas las JOINs y WHERE clauses son correctas.

11. **Impacto en procesos de acreditación:** Los procesos de acreditación evalúan programas específicos, no facultades completas:
    - Acreditación de Ingeniería de Software (CIP code específico)
    - Documentación de trazabilidad por programa
    - Evidencias específicas del plan de estudios acreditado
    
    Este escenario valida que el sistema puede generar evidencias correctas por programa.

12. **Validación de performance con datos reales:** Con facultades grandes:
    - Sistemas puede tener 50+ objetivos, 200+ RA, 100+ asignaturas **total**
    - Software específicamente: ~15 objetivos, ~60 RA, ~40 asignaturas
    
    El filtrado debe ser eficiente y mostrar solo el subset relevante (<500ms).

13. **Especificidad testeable:** El escenario especifica:
    - Qué objetivos deben aparecer (OPP1, OPP2, OPP3, OPP5)
    - Códigos específicos de asignaturas (IS-101, IS-305, GE-401, etc.)
    - Códigos de RA (RG1, RG3, RE4, etc.)
    - Qué NO debe aparecer (datos de otras carreras)
    
    Permite pruebas automatizadas con assertions exactos.

**Recomendación de prueba prioritaria:**
- Crear dataset de prueba con 3 carreras con datos distintos y verificar separación correcta
- Validar que al seleccionar Software solo aparecen OPs de Software
- Verificar que no hay "leak" de asignaturas de Computación o IA
- Probar con todas las carreras de la facultad para confirmar que cada una filtra correctamente
- Validar performance de query con filtro por carrera_id
- Verificar integridad referencial: cada asignatura mostrada debe realmente pertenecer a la carrera
- Incluir en regresión crítica para cambios en modelo de datos o lógica de filtrado
- Probar casos edge: carrera sin OP, carrera nueva sin asignaturas asignadas
- Validar con datos reales de múltiples facultades y carreras

**Sin este escenario funcionando, el coordinador no puede "analizar la alineación de un programa de estudios específico"** como requiere la HU, porque estaría viendo datos mezclados de múltiples programas, haciendo el análisis inútil y potencialmente peligroso (decisiones basadas en datos incorrectos). Este escenario valida que el filtrado jerárquico Facultad→Carrera realmente impacta el contenido mostrado, no solo la navegación de filtros.