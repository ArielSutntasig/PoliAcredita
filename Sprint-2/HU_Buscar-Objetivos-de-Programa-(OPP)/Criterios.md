# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de las Imágenes 2 y 5):**

**C1:** Campo de búsqueda contiene texto (Sí/No)  
**C2:** Existen Objetivos de Programa que coinciden con el texto de búsqueda (Sí/No)

**Acciones del sistema identificadas (observadas en Imágenes 2 y 5):**

**A1:** Mostrar todos los Objetivos de Programa (OPP) disponibles sin filtrar  
**A2:** Filtrar y mostrar únicamente los OPPs que coinciden con el texto de búsqueda  
**A3:** Mantener visible la estructura de la tabla con columnas "Código" y "Descripción"  
**A4:** Actualizar los resultados dinámicamente sin recargar la página completa  
**A5:** Mostrar tabla vacía o mensaje indicativo cuando no hay resultados que coincidan  
**A6:** Mantener visible el campo de búsqueda "Buscar por código o descripción..."  
**A7:** Buscar coincidencias tanto en el campo "Código" como en "Descripción"  
**A8:** Actualizar controles de paginación según los resultados filtrados  
**A9:** Permitir búsqueda parcial (no requiere coincidencia exacta)  
**A10:** Mantener visible el botón "+ Nuevo OPP" en la esquina superior derecha

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Campo tiene texto | C2: Existen coincidencias | Acciones |
|-------|----------------------|---------------------------|----------|
| R1 | No | No | A1, A3, A6, A8, A10 |
| R2 | No | Sí | *Ilógico* |
| R3 | Sí | No | A5, A3, A6, A4, A7, A8, A10 |
| R4 | Sí | Sí | A2, A3, A6, A4, A7, A8, A9, A10 |

**Análisis de ilógicos:**
- R2: Si el campo de búsqueda está vacío, no puede haber una búsqueda activa que genere coincidencias. Esta regla es lógicamente imposible.

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Se elimina R2 por ser lógicamente imposible
- R1 representa el estado inicial sin búsqueda activa (campo vacío)
- R3 representa búsqueda activa sin resultados encontrados
- R4 representa búsqueda activa con resultados encontrados

| Regla | C1: Campo tiene texto | C2: Existen coincidencias | Acciones |
|-------|----------------------|---------------------------|----------|
| **R1** | No | - | A1, A3, A6, A8, A10 |
| **R2** | Sí | No | A5, A3, A6, A4, A7, A8, A10 |
| **R3** | Sí | Sí | A2, A3, A6, A4, A7, A8, A9, A10 |

**Justificación de la minimización:**
Se eliminó la regla R2 de la tabla maximizada por ser lógicamente imposible (no puede haber coincidencias sin texto de búsqueda). En R1 minimizada, la condición C2 es irrelevante (marcada con "-") porque sin texto de búsqueda no aplica la evaluación de coincidencias. Las 3 reglas finales cubren exhaustivamente todos los estados válidos: sin búsqueda, búsqueda sin resultados, y búsqueda con resultados.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **5 Criterios de Aceptación** en total.

**Justificación:** 
- Las 3 reglas de la tabla minimizada generan 3 criterios base (R1→AC1, R2→AC2, R3→AC3)
- Se agregan 2 criterios adicionales para validar aspectos específicos observados en el prototipo y mencionados en la HU:
  - Búsqueda específica por código de OPP (AC4)
  - Búsqueda específica por descripción de OPP (AC5)

**Criterios NO eliminados - Justificación:** Aunque la HU anterior "Buscar Criterios EUR-ACE" tiene una lógica de búsqueda similar, los criterios NO son idénticos y deben conservarse debido a que:
1. **Los datos de entrada son diferentes:** Objetivos de Programa (OPP1, OPP2, OPP3, etc.) vs Criterios EUR-ACE (5.4.1, 5.4.2, etc.)
2. **El rol del usuario es diferente:** Coordinador de Carrera vs Administrador
3. **La vista es diferente:** "Gestión de Objetivos de Carrera (OPP)" vs "Criterios EUR-ACE"
4. **Las descripciones son diferentes:** "Comprender los principios fundamentales de la ingeniería de software" vs "La investigación en la solución de problemas complejos..."
5. **El contexto de uso es diferente:** Los OPPs son parte del perfil de egreso de una carrera académica, mientras que los Criterios EUR-ACE son estándares de acreditación

Por lo tanto, todos los criterios deben conservarse ya que validan comportamientos específicos de esta vista con datos únicos.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar listado completo sin filtrar cuando campo de búsqueda está vacío**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema, **cuando** el campo de búsqueda "Buscar por código o descripción..." está vacío o no contiene texto, **entonces** se muestra la tabla completa con las columnas "Código" y "Descripción" **Y** se muestran todos los Objetivos de Programa disponibles sin aplicar ningún filtro (ej: OPP1, OPP2, OPP3, OPP4, OPP5) **Y** se muestran las descripciones completas de cada objetivo (ej: "Comprender los principios fundamentales de la ingeniería de software.", "Diseñar y desarrollar sistemas de software escalables y seguros.", etc.) **Y** los controles de paginación funcionan normalmente mostrando todas las páginas disponibles **Y** el campo de búsqueda permanece visible y disponible para ingresar texto **Y** el botón "+ Nuevo OPP" se muestra en la esquina superior derecha.

### **Escenario 2 – Mostrar estado apropiado cuando no hay resultados que coincidan**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema, **cuando** ingreso texto en el campo de búsqueda "Buscar por código o descripción..." que no coincide con ningún código ni descripción de los Objetivos de Programa existentes (ej: "xyz789"), **entonces** la tabla se actualiza dinámicamente sin recargar la página **Y** se muestra la estructura de la tabla con las columnas "Código" y "Descripción" **Y** no se muestran filas de datos en la tabla **Y** se muestra un estado visual que indica que no hay resultados o la tabla aparece vacía **Y** el campo de búsqueda mantiene el texto ingresado **Y** los controles de paginación se ocultan o muestran solo página 1 sin resultados **Y** el botón "+ Nuevo OPP" permanece visible en la esquina superior derecha.

### **Escenario 3 – Filtrar y mostrar solo OPPs que coinciden con el texto de búsqueda**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** existen Objetivos de Programa que contienen el texto buscado en su código o descripción, **cuando** ingreso texto en el campo de búsqueda "Buscar por código o descripción..." (ej: "OPP1" o "software"), **entonces** la tabla se actualiza dinámicamente sin recargar la página **Y** se filtran y muestran únicamente los OPPs que contienen el texto buscado en su código o en su descripción **Y** se mantiene la estructura de la tabla con columnas "Código" y "Descripción" **Y** cada OPP filtrado muestra su código completo y descripción completa **Y** la búsqueda acepta coincidencias parciales (no requiere texto exacto completo) **Y** el campo de búsqueda mantiene el texto ingresado **Y** los controles de paginación se actualizan para reflejar solo las páginas de resultados filtrados **Y** el botón "+ Nuevo OPP" permanece visible en la esquina superior derecha.

### **Escenario 4 – Buscar OPPs específicos por código**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema, **cuando** ingreso un código específico o parte de un código en el campo de búsqueda (ej: "OPP1" o "OPP"), **entonces** se filtran y muestran únicamente los Objetivos de Programa cuyo código contiene el texto ingresado **Y** se muestra el OPP1 "Comprender los principios fundamentales de la ingeniería de software." si busco "OPP1" **Y** se muestran todos los objetivos con códigos que contienen "OPP" (OPP1, OPP2, OPP3, OPP4, OPP5) si busco "OPP" **Y** la tabla se actualiza dinámicamente sin recargar la página **Y** se mantiene visible la estructura completa de cada objetivo (código y descripción) **Y** el botón "+ Nuevo OPP" permanece visible.

### **Escenario 5 – Buscar OPPs específicos por descripción**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema, **cuando** ingreso palabras o frases que aparecen en las descripciones de los Objetivos de Programa (ej: "software", "metodologías ágiles", "herramientas"), **entonces** se filtran y muestran únicamente los OPPs cuya descripción contiene el texto ingresado **Y** se muestra el OPP1 si busco "software" porque su descripción contiene esa palabra **Y** se muestra el OPP3 si busco "metodologías ágiles" porque su descripción contiene esa frase **Y** la búsqueda no distingue entre mayúsculas y minúsculas **Y** la búsqueda acepta coincidencias parciales de palabras **Y** la tabla se actualiza dinámicamente sin recargar la página **Y** cada OPP filtrado muestra su código y descripción completa **Y** el botón "+ Nuevo OPP" permanece visible en la esquina superior derecha.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Filtrar y mostrar solo OPPs que coinciden con el texto de búsqueda**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Validación Directa del Valor de la HU:** Este escenario demuestra explícitamente el objetivo central declarado en la Historia de Usuario: "encontrar objetivos específicos por código o descripción rápidamente". Sin esta funcionalidad básica de filtrado, la HU completa pierde su propósito y valor para el coordinador de carrera.

2. **Happy Path Principal:** Representa el flujo de uso más común y esperado: un coordinador de carrera ingresa texto para buscar OPPs específicos y obtiene resultados relevantes filtrados. Es la razón principal por la que un coordinador utilizaría esta funcionalidad en su trabajo diario.

3. **Dependencia de Otros Escenarios:** Los escenarios 4 y 5 (búsqueda específica por código y por descripción) son casos particulares o refinamientos de este escenario base. Si el filtrado general no funciona correctamente, los casos específicos tampoco funcionarán.

4. **Impacto en Productividad del Coordinador:** Los Objetivos de Programa son elementos centrales del diseño curricular. Un coordinador de carrera necesita acceder frecuentemente a OPPs específicos para:
   - Revisar y actualizar objetivos
   - Relacionar OPPs con Resultados de Aprendizaje
   - Preparar documentación de acreditación
   - Verificar alineación con criterios EUR-ACE
   
   Sin una búsqueda funcional, tendría que navegar manualmente página por página, lo cual es altamente ineficiente.

5. **Experiencia del Usuario y Elementos Críticos de UX:** Este escenario valida elementos esenciales observados en las imágenes 2 y 5:
   - Actualización dinámica sin recargas (fluidez y rapidez)
   - Mantenimiento de estructura visual (consistencia)
   - Actualización inteligente de paginación según resultados (coherencia)
   - Búsqueda parcial flexible (usabilidad y tolerancia a errores)
   - Persistencia del botón "+ Nuevo OPP" (acceso constante a funcionalidad clave)

6. **Contexto Académico Crítico:** Los Objetivos de Programa (OPP) son el corazón del perfil de egreso de una carrera académica y definen las competencias que los graduados deben alcanzar. Un coordinador de carrera necesita:
   - Localizar rápidamente objetivos específicos al trabajar en diseño curricular
   - Verificar redacciones exactas para documentos oficiales
   - Relacionar objetivos con asignaturas del plan de estudios
   - Validar alineación con estándares de acreditación

7. **Riesgo de Negocio y Calidad Académica:** Una búsqueda disfuncional tendría impactos negativos directos:
   - Retrasos en procesos de revisión curricular
   - Errores en documentación de acreditación por no localizar objetivos correctos
   - Frustración del coordinador que impactaría la adopción del sistema
   - Retorno a métodos manuales menos eficientes (spreadsheets, documentos Word)

8. **Base para Validación de Precisión:** Este escenario establece el comportamiento correcto de filtrado que debe ser consistente con los demás criterios. Si el filtrado general es impreciso, ambiguo o inconsistente, comprometería la confiabilidad de toda la funcionalidad de búsqueda y la confianza del usuario en el sistema.

9. **Frecuencia de Uso:** Este es el escenario que se ejecutará con mayor frecuencia en el uso real del sistema. Los coordinadores buscarán OPPs regularmente (múltiples veces al día), mientras que los casos de "sin resultados" o "campo vacío" son situaciones transitorias o menos frecuentes.