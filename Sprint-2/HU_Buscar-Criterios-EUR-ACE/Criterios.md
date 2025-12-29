# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de la Imagen 11):**

**C1:** Campo de búsqueda contiene texto (Sí/No)  
**C2:** Existen criterios EUR-ACE que coinciden con el texto de búsqueda (Sí/No)

**Acciones del sistema identificadas (observadas en Imagen 11):**

**A1:** Mostrar todos los criterios EUR-ACE disponibles sin filtrar  
**A2:** Filtrar y mostrar únicamente los criterios EUR-ACE que coinciden con el texto de búsqueda  
**A3:** Mantener visible la estructura de la tabla con columnas "Código" y "Descripción"  
**A4:** Actualizar los resultados dinámicamente sin recargar la página completa  
**A5:** Mostrar tabla vacía o mensaje indicativo cuando no hay resultados que coincidan  
**A6:** Mantener visible el campo de búsqueda "Buscar por código o descripción..."  
**A7:** Buscar coincidencias tanto en el campo "Código" como en "Descripción"  
**A8:** Actualizar controles de paginación según los resultados filtrados  
**A9:** Permitir búsqueda parcial (no requiere coincidencia exacta)

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Campo tiene texto | C2: Existen coincidencias | Acciones |
|-------|----------------------|---------------------------|----------|
| R1 | No | No | A1, A3, A6, A8 |
| R2 | No | Sí | *Ilógico* |
| R3 | Sí | No | A5, A3, A6, A4, A7, A8 |
| R4 | Sí | Sí | A2, A3, A6, A4, A7, A8, A9 |

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
| **R1** | No | - | A1, A3, A6, A8 |
| **R2** | Sí | No | A5, A3, A6, A4, A7, A8 |
| **R3** | Sí | Sí | A2, A3, A6, A4, A7, A8, A9 |

**Justificación de la minimización:**
Se eliminó la regla R2 de la tabla maximizada por ser lógicamente imposible (no puede haber coincidencias si no hay texto de búsqueda). En R1 minimizada, la condición C2 es irrelevante (marcada con "-") porque sin texto de búsqueda no aplica la evaluación de coincidencias. Las 3 reglas finales cubren exhaustivamente todos los estados válidos: sin búsqueda, búsqueda sin resultados, y búsqueda con resultados.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **5 Criterios de Aceptación** en total.

**Justificación:** 
- Las 3 reglas de la tabla minimizada generan 3 criterios base (R1→AC1, R2→AC2, R3→AC3)
- Se agregan 2 criterios adicionales para validar aspectos específicos observados en el prototipo y mencionados en la HU:
  - Búsqueda específica por código (AC4)
  - Búsqueda específica por descripción (AC5)

**Criterios eliminados:** Ninguno. Esta es una funcionalidad nueva (búsqueda/filtrado) que no se ha abordado en las HUs anteriores de paginación. Los datos de entrada son específicos (Criterios EUR-ACE con códigos como 5.4.1, 5.4.2, etc.) y el comportamiento es único para esta vista, por lo que no hay redundancia con otros criterios existentes.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar listado completo sin filtrar cuando campo de búsqueda está vacío**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema, **cuando** el campo de búsqueda "Buscar por código o descripción..." está vacío o no contiene texto, **entonces** se muestra la tabla completa con las columnas "Código" y "Descripción" **Y** se muestran todos los criterios EUR-ACE disponibles sin aplicar ningún filtro (ej: 5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5) **Y** se muestran las descripciones completas de cada criterio **Y** los controles de paginación funcionan normalmente mostrando todas las páginas disponibles **Y** el campo de búsqueda permanece visible y disponible para ingresar texto.

### **Escenario 2 – Mostrar estado apropiado cuando no hay resultados que coincidan**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema, **cuando** ingreso texto en el campo de búsqueda "Buscar por código o descripción..." que no coincide con ningún código ni descripción de los criterios EUR-ACE existentes (ej: "xyz123"), **entonces** la tabla se actualiza dinámicamente sin recargar la página **Y** se muestra la estructura de la tabla con las columnas "Código" y "Descripción" **Y** no se muestran filas de datos en la tabla **Y** se muestra un estado visual que indica que no hay resultados o la tabla aparece vacía **Y** el campo de búsqueda mantiene el texto ingresado **Y** los controles de paginación se ocultan o muestran solo página 1 sin resultados.

### **Escenario 3 – Filtrar y mostrar solo criterios que coinciden con el texto de búsqueda**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema **Y** existen criterios EUR-ACE que contienen el texto buscado en su código o descripción, **cuando** ingreso texto en el campo de búsqueda "Buscar por código o descripción..." (ej: "5.4.1" o "investigación"), **entonces** la tabla se actualiza dinámicamente sin recargar la página **Y** se filtran y muestran únicamente los criterios EUR-ACE que contienen el texto buscado en su código o en su descripción **Y** se mantiene la estructura de la tabla con columnas "Código" y "Descripción" **Y** cada criterio filtrado muestra su código completo y descripción completa **Y** la búsqueda acepta coincidencias parciales (no requiere texto exacto completo) **Y** el campo de búsqueda mantiene el texto ingresado **Y** los controles de paginación se actualizan para reflejar solo las páginas de resultados filtrados.

### **Escenario 4 – Buscar criterios específicos por código**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema, **cuando** ingreso un código específico o parte de un código en el campo de búsqueda (ej: "5.4.1" o "5.4"), **entonces** se filtran y muestran únicamente los criterios EUR-ACE cuyo código contiene el texto ingresado **Y** se muestra el criterio 5.4.1 "La investigación en la solución de problemas complejos de ingeniería en el campo de estudio pertinente..." si busco "5.4.1" **Y** se muestran todos los criterios con códigos 5.4.x (5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5) si busco "5.4" **Y** la tabla se actualiza dinámicamente sin recargar la página **Y** se mantiene visible la estructura completa de cada criterio (código y descripción).

### **Escenario 5 – Buscar criterios específicos por descripción**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema, **cuando** ingreso palabras o frases que aparecen en las descripciones de los criterios EUR-ACE (ej: "investigación", "ingeniería práctica", "especialización"), **entonces** se filtran y muestran únicamente los criterios EUR-ACE cuya descripción contiene el texto ingresado **Y** se muestra el criterio 5.4.1 si busco "investigación" porque su descripción contiene esa palabra **Y** se muestra el criterio 5.4.4 si busco "ingeniería práctica" porque su descripción contiene esa frase **Y** la búsqueda no distingue entre mayúsculas y minúsculas **Y** la búsqueda acepta coincidencias parciales de palabras **Y** la tabla se actualiza dinámicamente sin recargar la página **Y** cada criterio filtrado muestra su código y descripción completa.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Filtrar y mostrar solo criterios que coinciden con el texto de búsqueda**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Validación Directa del Valor de la HU:** Este escenario demuestra explícitamente el objetivo central declarado en la Historia de Usuario: "encontrar criterios específicos por código o descripción rápidamente". Sin esta funcionalidad básica de filtrado, la HU completa pierde su propósito y valor.

2. **Happy Path Principal:** Representa el flujo de uso más común y esperado por el usuario administrador: ingresar texto para buscar y obtener resultados relevantes filtrados. Es la razón principal por la que un administrador utilizaría esta funcionalidad.

3. **Dependencia de Otros Escenarios:** Los escenarios 4 y 5 (búsqueda específica por código y por descripción) son casos particulares o refinamientos de este escenario base. Si el filtrado general no funciona, los casos específicos tampoco funcionarán.

4. **Impacto en Productividad:** Los Criterios EUR-ACE son estándares europeos extensos y numerosos (como se observa en la Imagen 11 con códigos 5.4.1 hasta 5.4.5 y más). Sin una búsqueda funcional, el administrador tendría que revisar manualmente página por página, lo cual es ineficiente y contradice el objetivo de "encontrar rápidamente".

5. **Experiencia del Usuario:** Este escenario valida elementos críticos de UX observados en el prototipo:
   - Actualización dinámica sin recargas (fluidez)
   - Mantenimiento de estructura visual (consistencia)
   - Actualización de paginación según resultados (coherencia)
   - Búsqueda parcial flexible (usabilidad)

6. **Contexto de Acreditación Académica:** Los Criterios EUR-ACE son fundamentales para procesos de acreditación de programas de ingeniería en Europa. Un administrador necesita:
   - Localizar rápidamente criterios específicos al preparar documentación de acreditación
   - Verificar descripciones exactas para asegurar cumplimiento
   - Relacionar criterios con resultados de aprendizaje y asignaturas
   
   Una búsqueda disfuncional impactaría directamente la eficiencia en estos procesos críticos de aseguramiento de calidad académica.

7. **Riesgo de Abandono de Funcionalidad:** Si la búsqueda básica no funciona correctamente (resultados incorrectos, búsqueda muy restrictiva, actualizaciones lentas), los usuarios administradores evitarán usar esta funcionalidad y volverán a métodos manuales menos eficientes, reduciendo el ROI del desarrollo.

8. **Base para Validación de Precisión:** Este escenario establece el comportamiento correcto de filtrado que debe ser consistente en todos los demás casos. Si el filtrado general es impreciso o inconsistente, comprometería la confiabilidad de toda la funcionalidad de búsqueda.