# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de las Imágenes 9 y 10):**

**C1:** Campo de búsqueda contiene texto (Sí/No)  
**C2:** Existen Resultados de Aprendizaje que coinciden con el texto en el tab activo (Sí/No)  
**C3:** Tab activo es "Resultados Generales (RG)" o "Resultados Específicos (RE)" (RG/RE) - Esta condición determina el conjunto de datos sobre el cual se aplica la búsqueda

**Acciones del sistema identificadas (observadas en Imágenes 9 y 10):**

**A1:** Mostrar todos los RAs del tab activo sin filtrar  
**A2:** Filtrar y mostrar únicamente los RAs del tab activo que coinciden con el texto de búsqueda  
**A3:** Mantener visible la estructura de la tabla con columnas "Código" y "Descripción"  
**A4:** Actualizar los resultados dinámicamente sin recargar la página completa  
**A5:** Mostrar tabla vacía o mensaje indicativo cuando no hay resultados que coincidan  
**A6:** Mantener visible el campo de búsqueda "Buscar por código o descripción..."  
**A7:** Buscar coincidencias tanto en el campo "Código" como en "Descripción"  
**A8:** Actualizar controles de paginación según los resultados filtrados  
**A9:** Permitir búsqueda parcial (no requiere coincidencia exacta)  
**A10:** Mantener visible el botón "+ Nuevo RA" en la esquina superior derecha  
**A11:** Mantener visibles los tabs "Resultados Generales (RG)" y "Resultados Específicos (RE)"  
**A12:** Aplicar la búsqueda ÚNICAMENTE al tab activo (no buscar en el contenido del tab inactivo)  
**A13:** Mostrar códigos según el tab: RG1-RG5 para Generales, RE1-RE5 para Específicos

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Campo tiene texto | C2: Existen coincidencias en tab activo | Acciones |
|-------|----------------------|----------------------------------------|----------|
| R1 | No | No | A1, A3, A6, A8, A10, A11, A12, A13 |
| R2 | No | Sí | *Ilógico* |
| R3 | Sí | No | A5, A3, A6, A4, A7, A8, A10, A11, A12, A13 |
| R4 | Sí | Sí | A2, A3, A6, A4, A7, A8, A9, A10, A11, A12, A13 |

**Análisis de ilógicos:**
- R2: Si el campo de búsqueda está vacío, no puede haber una búsqueda activa que genere coincidencias. Esta regla es lógicamente imposible.

**Nota:** La condición C3 (tab activo) no genera combinaciones adicionales en la tabla porque determina el contexto (RG o RE) sobre el cual se aplican las reglas, pero la lógica de búsqueda es idéntica para ambos tabs.

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Se elimina R2 por ser lógicamente imposible
- R1 representa el estado inicial sin búsqueda activa (campo vacío)
- R3 representa búsqueda activa sin resultados en el tab activo
- R4 representa búsqueda activa con resultados en el tab activo
- La condición C3 no afecta la lógica, solo determina el conjunto de datos (RG o RE)

| Regla | C1: Campo tiene texto | C2: Existen coincidencias en tab activo | Acciones |
|-------|----------------------|----------------------------------------|----------|
| **R1** | No | - | A1, A3, A6, A8, A10, A11, A12, A13 |
| **R2** | Sí | No | A5, A3, A6, A4, A7, A8, A10, A11, A12, A13 |
| **R3** | Sí | Sí | A2, A3, A6, A4, A7, A8, A9, A10, A11, A12, A13 |

**Justificación de la minimización:**
Se eliminó la regla R2 de la tabla maximizada por ser lógicamente imposible. En R1 minimizada, la condición C2 es irrelevante (marcada con "-") porque sin texto de búsqueda no aplica la evaluación de coincidencias. Las 3 reglas finales cubren todos los estados válidos, y se aplican de manera idéntica tanto al tab de "Resultados Generales (RG)" como al de "Resultados Específicos (RE)".

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **6 Criterios de Aceptación** en total.

**Justificación:** 
- Las 3 reglas de la tabla minimizada generan 3 criterios base (R1→AC1, R2→AC2, R3→AC3)
- Se agregan 2 criterios adicionales para validar aspectos específicos:
  - Búsqueda específica por código de RA (AC4)
  - Búsqueda específica por descripción de RA (AC5)
- Se agrega 1 criterio crítico adicional para validar el comportamiento único de tabs:
  - Validar que la búsqueda se aplica solo al tab activo y no cruza datos entre tabs (AC6)

**Criterios NO eliminados - Justificación:** Aunque las HUs anteriores de búsqueda (EUR-ACE y OPP) tienen lógica similar, los criterios NO son idénticos y deben conservarse debido a que:
1. **Los datos son diferentes:** Resultados de Aprendizaje (RG1-RG5, RE1-RE5) vs OPPs vs Criterios EUR-ACE
2. **El contexto es único:** Esta vista tiene sistema de tabs (RG/RE) que otras vistas no tienen
3. **La búsqueda tiene alcance limitado:** La búsqueda se aplica SOLO al tab activo, característica única de esta vista
4. **Las descripciones son específicas:** Los RAs tienen descripciones académicas únicas del perfil de egreso
5. **Existe funcionalidad adicional:** AC6 valida comportamiento específico de tabs que no existe en otras HUs

Por lo tanto, todos los criterios deben conservarse ya que validan comportamientos específicos de esta vista con funcionalidad única.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar listado completo sin filtrar cuando campo de búsqueda está vacío en tab activo**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)", **cuando** el campo de búsqueda "Buscar por código o descripción..." está vacío o no contiene texto, **entonces** se muestra la tabla completa con las columnas "Código" y "Descripción" **Y** se muestran todos los Resultados de Aprendizaje disponibles del tab activo sin aplicar ningún filtro (ej: RG1, RG2, RG3, RG4, RG5 si estoy en tab RG, o RE1, RE2, RE3, RE4, RE5 si estoy en tab RE) **Y** se muestran las descripciones completas de cada resultado según el tab activo **Y** los controles de paginación funcionan normalmente mostrando todas las páginas disponibles del tab activo **Y** el campo de búsqueda permanece visible y disponible **Y** el botón "+ Nuevo RA" se muestra en la esquina superior derecha **Y** los tabs "Resultados Generales (RG)" y "Resultados Específicos (RE)" permanecen visibles.

### **Escenario 2 – Mostrar estado apropiado cuando no hay resultados que coincidan en el tab activo**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)", **cuando** ingreso texto en el campo de búsqueda "Buscar por código o descripción..." que no coincide con ningún código ni descripción de los RAs del tab activo (ej: "xyz999"), **entonces** la tabla se actualiza dinámicamente sin recargar la página **Y** se muestra la estructura de la tabla con las columnas "Código" y "Descripción" **Y** no se muestran filas de datos en la tabla **Y** se muestra un estado visual que indica que no hay resultados o la tabla aparece vacía **Y** el campo de búsqueda mantiene el texto ingresado **Y** los controles de paginación se ocultan o muestran solo página 1 sin resultados **Y** el botón "+ Nuevo RA" permanece visible **Y** los tabs permanecen visibles y accesibles.

### **Escenario 3 – Filtrar y mostrar solo RAs que coinciden con el texto de búsqueda en el tab activo**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" **Y** existen Resultados de Aprendizaje en el tab activo que contienen el texto buscado en su código o descripción, **cuando** ingreso texto en el campo de búsqueda "Buscar por código o descripción..." (ej: "RG1" o "software" en tab RG, o "RE2" o "escalables" en tab RE), **entonces** la tabla se actualiza dinámicamente sin recargar la página **Y** se filtran y muestran únicamente los RAs del tab activo que contienen el texto buscado en su código o descripción **Y** se mantiene la estructura de la tabla con columnas "Código" y "Descripción" **Y** cada RA filtrado muestra su código completo y descripción completa según el tab activo **Y** la búsqueda acepta coincidencias parciales (no requiere texto exacto completo) **Y** el campo de búsqueda mantiene el texto ingresado **Y** los controles de paginación se actualizan para reflejar solo las páginas de resultados filtrados del tab activo **Y** el botón "+ Nuevo RA" permanece visible **Y** los tabs permanecen visibles.

### **Escenario 4 – Buscar RAs específicos por código en el tab activo**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)", **cuando** ingreso un código específico o parte de un código en el campo de búsqueda (ej: "RG1" o "RG" en tab RG, o "RE3" o "RE" en tab RE), **entonces** se filtran y muestran únicamente los Resultados de Aprendizaje del tab activo cuyo código contiene el texto ingresado **Y** se muestra el RG1 "Comprender los principios fundamentales de la ingeniería de software." si estoy en tab RG y busco "RG1" **Y** se muestran todos los resultados generales (RG1, RG2, RG3, RG4, RG5) si estoy en tab RG y busco "RG" **Y** se muestra el RE3 con su descripción si estoy en tab RE y busco "RE3" **Y** la tabla se actualiza dinámicamente sin recargar la página **Y** se mantiene visible la estructura completa de cada resultado (código y descripción) **Y** el botón "+ Nuevo RA" y los tabs permanecen visibles.

### **Escenario 5 – Buscar RAs específicos por descripción en el tab activo**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)", **cuando** ingreso palabras o frases que aparecen en las descripciones de los RAs del tab activo (ej: "software", "metodologías ágiles" en tab RG, o "escalables", "seguridad" en tab RE), **entonces** se filtran y muestran únicamente los RAs del tab activo cuya descripción contiene el texto ingresado **Y** se muestra el RG1 si estoy en tab RG y busco "software" porque su descripción contiene esa palabra **Y** se muestra el RG3 si estoy en tab RG y busco "metodologías ágiles" porque su descripción contiene esa frase **Y** la búsqueda no distingue entre mayúsculas y minúsculas **Y** la búsqueda acepta coincidencias parciales de palabras **Y** la tabla se actualiza dinámicamente sin recargar la página **Y** cada RA filtrado muestra su código y descripción completa según el tab activo **Y** el botón "+ Nuevo RA" y los tabs permanecen visibles.

### **Escenario 6 – Validar que la búsqueda se aplica únicamente al tab activo**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)", **cuando** ingreso texto en el campo de búsqueda que solo coincide con RAs del tab "Resultados Específicos (RE)" pero no con RGs (ej: "RE1"), **entonces** la tabla se actualiza dinámicamente **Y** no se muestran resultados porque el texto no coincide con ningún RA del tab activo (RG) **Y** se muestra la tabla vacía o mensaje de sin resultados **Y** cuando cambio al tab "Resultados Específicos (RE)" sin modificar el texto de búsqueda, **entonces** se aplica automáticamente la búsqueda al nuevo tab activo **Y** se muestran los REs que coinciden con el texto (ej: RE1 si busqué "RE1") **Y** la búsqueda permanece activa pero se aplica independientemente a cada tab según cuál esté activo **Y** no se mezclan resultados de RG y RE en ningún momento.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 6 – Validar que la búsqueda se aplica únicamente al tab activo**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Funcionalidad Única y Diferenciadora:** Este escenario valida el comportamiento específico y único mencionado explícitamente en la HU: "Para encontrar resultados de aprendizaje específicos rápidamente **en la pestaña activa**". Este requisito distingue esta HU de las anteriores de búsqueda (EUR-ACE y OPP) que no tienen sistema de tabs.

2. **Riesgo Crítico de Confusión de Datos:** Si la búsqueda no respeta el alcance del tab activo, podría:
   - Mostrar mezclados RGs y REs en una misma búsqueda (violación conceptual grave)
   - Mostrar REs cuando el usuario está en tab RG (error de contexto)
   - Generar confusión sobre qué tipo de resultado está visualizando el coordinador
   - Comprometer la integridad de la clasificación entre Resultados Generales y Específicos

3. **Impacto en Decisiones Académicas:** Los Resultados de Aprendizaje Generales (RG) y Específicos (RE) tienen naturalezas y propósitos diferentes en el diseño curricular:
   - **RGs:** Competencias transversales y fundamentales del programa
   - **REs:** Competencias específicas de áreas o asignaturas particulares
   
   Mezclar o confundir estos tipos durante la búsqueda podría llevar a:
   - Errores en la documentación de acreditación
   - Asignación incorrecta de RAs a asignaturas
   - Confusión en mapas curriculares y matrices de trazabilidad

4. **Validación de Arquitectura de Componentes:** Este escenario valida que:
   - Los tabs funcionan como filtros de contexto correctamente
   - La búsqueda tiene scope limitado y controlado
   - El cambio de tabs reactiva la búsqueda sobre el nuevo conjunto de datos
   - No hay "bleeding" de datos entre contextos separados

5. **Caso de Uso Real y Frecuente:** Un coordinador trabajará típicamente:
   - Primero en RGs (diseño de competencias generales del programa)
   - Luego en REs (diseño de competencias específicas)
   - Necesitará buscar en cada contexto de forma independiente
   - No querrá ver resultados mezclados que contaminen su contexto de trabajo

6. **Complejidad Técnica Mayor:** Este escenario tiene la mayor complejidad técnica porque requiere:
   - Gestión de estado del tab activo
   - Filtrado dinámico por tab antes del filtrado por texto
   - Reactividad al cambio de tabs con búsqueda activa
   - Sincronización entre múltiples componentes (tabs + búsqueda + tabla)

7. **Punto de Fallo Silencioso:** Un bug en este escenario podría:
   - No ser inmediatamente obvio al usuario
   - Generar resultados "técnicamente correctos" pero contextualmente erróneos
   - Pasar desapercibido en pruebas superficiales
   - Causar errores acumulativos en trabajo posterior del coordinador

8. **Prerrequisito para Otros Escenarios:** Los escenarios 3, 4 y 5 asumen implícitamente que la búsqueda respeta el tab activo. Si este comportamiento falla, todos esos escenarios producirían resultados incorrectos o ambiguos, aunque técnicamente la búsqueda "funcione".

9. **Diferencia Crítica vs HUs Similares:** Mientras que "Buscar EUR-ACE" y "Buscar OPP" validan búsqueda en conjuntos de datos únicos, esta HU debe validar búsqueda en conjuntos de datos **múltiples mutuamente excluyentes** (RG vs RE) con cambio dinámico de contexto. Esta complejidad adicional la hace más crítica.

10. **Impacto en Experiencia del Usuario:** Una búsqueda que no respeta tabs:
    - Frustraría al coordinador con resultados irrelevantes
    - Obligaría a verificación manual adicional del tipo de RA
    - Reduciría la confianza en el sistema
    - Eliminaría el beneficio de productividad que justifica la funcionalidad