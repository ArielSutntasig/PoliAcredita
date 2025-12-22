# CRITERIOS DE ACEPTACIÓN - HU: Visualizar Trazabilidad detallada de Contribución Asignatura-Criterio

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**C1: Click válido en cruce de matriz**
- Estado: Sí / No
- Fuente: Usuario hace click en celda con checkmark verde en matriz Asignatura vs EURACE
- Contexto: Debe existir una relación documentada (checkmark visible)
- Observado: Click en "Cálculo en una Variable" intersección con criterio EUR-ACE

**C2: Asignatura tiene relaciones de nivel Alto**
- Estado: Sí / No
- Fuente: Datos de trazabilidad de la asignatura seleccionada
- Observado: Sección "Nivel de aporte: Alto" con fondo verde/turquesa visible en todas las imágenes de trazabilidad

**C3: Asignatura tiene relaciones de nivel Medio**
- Estado: Sí / No
- Fuente: Datos de trazabilidad de la asignatura seleccionada
- Observado: Sección "Nivel de aporte: Medio" con fondo amarillo visible en todas las imágenes de trazabilidad

**C4: Asignatura tiene relaciones de nivel Bajo**
- Estado: Sí / No
- Fuente: Datos de trazabilidad de la asignatura seleccionada
- Observado: Sección "Nivel de aporte: Bajo" con fondo rosa visible en todas las imágenes de trazabilidad

**C5: Click en botón "Regresar"**
- Estado: Sí / No
- Fuente: Botón ubicado en esquina superior derecha de vista de trazabilidad
- Acción: Navegación de regreso a matriz

#### **Acciones del sistema identificadas:**

**A1: Navegar a vista de trazabilidad**
- Condición: Click válido en cruce de matriz
- Elementos: Cambio de vista completo, carga de datos de trazabilidad

**A2: Mostrar encabezado de trazabilidad**
- Elementos observados:
  - Título: "Trazabilidad de [Nombre Asignatura]" (ej: "Trazabilidad de Cálculo en una Variable")
  - Botón "Regresar" en esquina superior derecha

**A3: Mostrar sección Nivel Alto**
- Condición: Existen relaciones de nivel Alto
- Elementos:
  - Encabezado: "Nivel de aporte: Alto"
  - Fondo: Verde/turquesa claro
  - 4 columnas: "R. de Aprendizaje Asignatura", "R. de Aprendizaje", "Justificación RA-EURACE", "Criterio EUR-ACE"
  - Flechas direccionales (→) entre columnas
  - Cards con bordes redondeados conteniendo:
    - RAA: Código (ej: "RAA 1.2: De conocimiento") + descripción
    - RA: Código (ej: "RA1:") + texto completo
    - Justificación: Título (ej: "RA1 - Criterio 5.2.1" o "RA1 - Criterio 5.2.2") + justificación académica
    - Criterio EUR-ACE: Código y nombre (ej: "Criterio 5.2.1: Conocimiento y Comprensión") + descripción

**A4: Mostrar sección Nivel Medio**
- Condición: Existen relaciones de nivel Medio
- Elementos: Estructura idéntica a A3 pero con fondo amarillo claro

**A5: Mostrar sección Nivel Bajo**
- Condición: Existen relaciones de nivel Bajo
- Elementos: Estructura idéntica a A3 pero con fondo rosa claro

**A6: Regresar a matriz**
- Condición: Click en botón "Regresar"
- Resultado: Volver a vista "Reporte: Asignatura vs Criterios EURACE" manteniendo filtros aplicados

**A7: No mostrar vista de trazabilidad**
- Condición: No hay click válido en cruce
- Resultado: Permanecer en vista de matriz

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 5 condiciones binarias: 2^5 = **32 reglas**

| Regla | C1: Click válido | C2: Nivel Alto | C3: Nivel Medio | C4: Nivel Bajo | C5: Click Regresar | Acción del Sistema |
|-------|------------------|----------------|-----------------|----------------|-------------------|-------------------|
| R1    | No               | No             | No              | No             | No                | A7: Permanecer en matriz |
| R2    | No               | No             | No              | No             | Sí                | A7: Permanecer en matriz (imposible*) |
| R3    | No               | No             | No              | Sí             | No                | A7: Permanecer en matriz |
| R4    | No               | No             | No              | Sí             | Sí                | A7: Permanecer en matriz (imposible*) |
| R5    | No               | No             | Sí              | No             | No                | A7: Permanecer en matriz |
| R6    | No               | No             | Sí              | No             | Sí                | A7: Permanecer en matriz (imposible*) |
| R7    | No               | No             | Sí              | Sí             | No                | A7: Permanecer en matriz |
| R8    | No               | No             | Sí              | Sí             | Sí                | A7: Permanecer en matriz (imposible*) |
| R9    | No               | Sí              | No              | No             | No                | A7: Permanecer en matriz |
| R10   | No               | Sí              | No              | No             | Sí                | A7: Permanecer en matriz (imposible*) |
| R11   | No               | Sí              | No              | Sí             | No                | A7: Permanecer en matriz |
| R12   | No               | Sí              | No              | Sí             | Sí                | A7: Permanecer en matriz (imposible*) |
| R13   | No               | Sí              | Sí              | No             | No                | A7: Permanecer en matriz |
| R14   | No               | Sí              | Sí              | No             | Sí                | A7: Permanecer en matriz (imposible*) |
| R15   | No               | Sí              | Sí              | Sí             | No                | A7: Permanecer en matriz |
| R16   | No               | Sí              | Sí              | Sí             | Sí                | A7: Permanecer en matriz (imposible*) |
| R17   | Sí               | No             | No              | No             | No                | A1 + A2: Mostrar encabezado sin secciones** |
| R18   | Sí               | No             | No              | No             | Sí                | A6: Regresar a matriz |
| R19   | Sí               | No             | No              | Sí             | No                | A1 + A2 + A5: Mostrar con solo nivel Bajo |
| R20   | Sí               | No             | No              | Sí             | Sí                | A6: Regresar a matriz |
| R21   | Sí               | No             | Sí              | No             | No                | A1 + A2 + A4: Mostrar con solo nivel Medio |
| R22   | Sí               | No             | Sí              | No             | Sí                | A6: Regresar a matriz |
| R23   | Sí               | No             | Sí              | Sí             | No                | A1 + A2 + A4 + A5: Mostrar niveles Medio y Bajo |
| R24   | Sí               | No             | Sí              | Sí             | Sí                | A6: Regresar a matriz |
| R25   | Sí               | Sí              | No              | No             | No                | A1 + A2 + A3: Mostrar con solo nivel Alto |
| R26   | Sí               | Sí              | No              | No             | Sí                | A6: Regresar a matriz |
| R27   | Sí               | Sí              | No              | Sí             | No                | A1 + A2 + A3 + A5: Mostrar niveles Alto y Bajo |
| R28   | Sí               | Sí              | No              | Sí             | Sí                | A6: Regresar a matriz |
| R29   | Sí               | Sí              | Sí              | No             | No                | A1 + A2 + A3 + A4: Mostrar niveles Alto y Medio |
| R30   | Sí               | Sí              | Sí              | No             | Sí                | A6: Regresar a matriz |
| R31   | Sí               | Sí              | Sí              | Sí             | No                | A1 + A2 + A3 + A4 + A5: Mostrar todos los niveles |
| R32   | Sí               | Sí              | Sí              | Sí             | Sí                | A6: Regresar a matriz |

*Imposible: No se puede hacer click en "Regresar" si no se está en la vista de trazabilidad
**Caso edge: Técnicamente imposible que una asignatura con checkmark no tenga ningún nivel

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Reglas R1-R16:** Todas con Click válido=No resultan en permanecer en matriz, sin importar los niveles de la asignatura (que son irrelevantes si no se accede). Click Regresar=Sí es imposible en este contexto. **Se fusionan en M1**.

2. **Regla R17:** Caso edge teóricamente imposible (checkmark sin niveles). **Se fusiona con M1 como caso inválido**.

3. **Reglas R18, R20, R22, R24, R26, R28, R30, R32:** Todas con Click Regresar=Sí ejecutan la misma acción (regresar a matriz), independientemente de los niveles. **Se fusionan en M2**.

4. **Reglas R19, R21, R23, R25, R27, R29, R31:** Con Click válido=Sí y Click Regresar=No, la acción depende de qué niveles existen. Sin embargo, desde la perspectiva de UX, el usuario verá **todas las secciones que existen**. Desde el análisis de imágenes, **siempre se muestran las 3 secciones** (Alto, Medio, Bajo), lo que sugiere que todas las asignaturas con trazabilidad tienen los 3 niveles. **Esto simplifica a una regla M3 para el caso completo**.

5. **Análisis de casos parciales:** Aunque teóricamente una asignatura podría tener solo algunos niveles, las imágenes muestran consistentemente los 3 niveles. Por completitud académica, incluiré reglas para casos donde solo existen algunos niveles.

#### **Tabla Minimizada:**

| Regla Min | C1: Click válido | C2: Nivel Alto | C3: Nivel Medio | C4: Nivel Bajo | C5: Click Regresar | Acción del Sistema |
|-----------|------------------|----------------|-----------------|----------------|--------------------|-------------------|
| **M1**    | No               | -              | -               | -              | -                  | A7: Permanecer en vista de matriz |
| **M2**    | Sí               | -              | -               | -              | Sí                 | A6: Regresar a matriz preservando filtros |
| **M3**    | Sí               | Sí             | No              | No             | No                 | A1 + A2 + A3: Mostrar trazabilidad con solo nivel Alto |
| **M4**    | Sí               | Sí             | Sí              | No             | No                 | A1 + A2 + A3 + A4: Mostrar trazabilidad con niveles Alto y Medio |
| **M5**    | Sí               | Sí             | Sí              | Sí             | No                 | A1 + A2 + A3 + A4 + A5: Mostrar trazabilidad completa (HAPPY PATH) |

**Resultado: 5 reglas minimizadas**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 5 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre estado sin navegación a trazabilidad (caso negativo básico - puede omitirse por ser implícito)
2. M2 → AC sobre funcionalidad del botón "Regresar"
3. M3 → AC sobre visualización parcial con solo nivel Alto
4. M4 → AC sobre visualización parcial con niveles Alto y Medio
5. M5 → AC sobre visualización completa con los 3 niveles (HAPPY PATH)

**Análisis de redundancias y necesidad:**

**Criterios a ELIMINAR:**
- **M1 (Permanecer en matriz):** Este es el comportamiento por defecto cuando no se accede a la funcionalidad. No es un criterio de aceptación de esta HU específica, sino del HU anterior (matriz). **ELIMINADO por redundancia con HU previa**.

- **M3 y M4 (casos parciales):** Tras revisar las imágenes nuevamente, **siempre se muestran las 3 secciones** (Alto, Medio, Bajo) en todos los ejemplos. Esto sugiere que todas las asignaturas con trazabilidad documentada tienen contribuciones en los 3 niveles. Incluir casos parciales sería especulación sin evidencia visual. **ELIMINADOS por falta de evidencia en prototipo**.

**Criterios adicionales necesarios del análisis visual:**

6. **Verificar estructura del flujo de 4 columnas:** Las imágenes muestran claramente el flujo RAA → RA → Justificación → Criterio EUR-ACE con flechas. Esto es fundamental para "entender la justificación completa" (objetivo de la HU).

7. **Verificar contenido específico en cards:** Las cards contienen códigos, títulos y descripciones específicas. Validar que se muestran correctamente es crítico.

8. **Scrolling vertical:** Las imágenes muestran que el contenido es scrollable para ver todas las secciones.

9. **Diferenciación visual por niveles:** Los códigos de color (verde/turquesa, amarillo, rosa) son críticos para distinguir niveles.

**TOTAL FINAL: 5 Criterios de Aceptación**
- 1 de M2 (Regresar)
- 1 de M5 (Happy path completo)
- 3 adicionales por elementos críticos de la visualización

**Justificación de eliminaciones:**
- **M1:** Redundante con HU de matriz, no es funcionalidad específica de esta HU
- **M3 y M4:** Sin evidencia visual en prototipo de casos parciales, todas las asignaturas muestran 3 niveles

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

Aplicando la guía de estilo internalizada:

---

### **Escenario 1 – Acceder a vista de trazabilidad desde matriz**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" **Y** veo la matriz con asignaturas y checkmarks verdes **Y** soy un Coordinador de Carrera o CEI en el sistema,
**cuando** hago clic en una celda con checkmark verde en la intersección de una asignatura con un criterio EUR-ACE (por ejemplo, "Cálculo en una Variable" con criterio "5.2.2"),
**entonces** se navega a una nueva vista de trazabilidad **Y** se muestra el título "Trazabilidad de Cálculo en una Variable" en la parte superior **Y** se presenta el botón "Regresar" en la esquina superior derecha **Y** se carga el contenido de trazabilidad completo de la asignatura **Y** la vista es scrollable verticalmente para visualizar todas las secciones.

---

### **Escenario 2 – Visualizar trazabilidad completa con los tres niveles de aporte**

**Dado que** he navegado a la vista de trazabilidad de una asignatura,
**cuando** se carga el contenido de la vista,
**entonces** se muestra la sección "Nivel de aporte: Alto" con fondo verde/turquesa claro **Y** se muestra la sección "Nivel de aporte: Medio" con fondo amarillo claro **Y** se muestra la sección "Nivel de aporte: Bajo" con fondo rosa claro **Y** cada sección mantiene su código de color distintivo **Y** las secciones se presentan en orden: Alto, Medio, Bajo de arriba hacia abajo **Y** todas las secciones son visibles mediante scroll vertical.

---

### **Escenario 3 – Visualizar flujo completo de trazabilidad por nivel**

**Dado que** estoy en la vista de trazabilidad **Y** veo una sección de nivel de aporte (Alto, Medio o Bajo),
**cuando** reviso el contenido de la sección,
**entonces** se presentan cuatro columnas horizontales con los encabezados: "R. de Aprendizaje Asignatura", "R. de Aprendizaje", "Justificación RA-EURACE", "Criterio EUR-ACE" **Y** se muestran flechas direccionales (→) entre cada columna indicando el flujo de trazabilidad **Y** la primera columna "R. de Aprendizaje Asignatura" contiene cards con código RAA (ej: "RAA 1.2: De conocimiento") y descripción completa del resultado de aprendizaje de la asignatura **Y** la segunda columna "R. de Aprendizaje" contiene cards con código RA (ej: "RA1:") y texto completo del resultado de aprendizaje de la carrera **Y** la tercera columna "Justificación RA-EURACE" contiene cards con título de relación (ej: "RA1 - Criterio 5.2.1") y texto de justificación académica explicando la conexión **Y** la cuarta columna "Criterio EUR-ACE" contiene cards con código y nombre del criterio (ej: "Criterio 5.2.1: Conocimiento y Comprensión") y descripción de la capacidad requerida **Y** todas las cards tienen bordes redondeados **Y** el flujo es legible de izquierda a derecha siguiendo las flechas.

---

### **Escenario 4 – Verificar contenido específico de cada nivel**

**Dado que** estoy visualizando la vista de trazabilidad completa,
**cuando** analizo el contenido de cada sección de nivel,
**entonces** en la sección "Nivel de aporte: Alto" se muestran las relaciones RAA-RA-Justificación-Criterio EUR-ACE correspondientes al aporte alto **Y** en la sección "Nivel de aporte: Medio" se muestran las relaciones correspondientes al aporte medio **Y** en la sección "Nivel de aporte: Bajo" se muestran las relaciones correspondientes al aporte bajo **Y** cada nivel puede contener múltiples cards de RAA si la asignatura tiene varios resultados de aprendizaje **Y** cada card muestra información completa y legible **Y** no hay solapamiento entre contenidos de diferentes niveles **Y** la información es comprensible para evaluación académica.

---

### **Escenario 5 – Regresar a matriz desde trazabilidad**

**Dado que** estoy en la vista "Trazabilidad de Cálculo en una Variable" **Y** veo el botón "Regresar" en la esquina superior derecha,
**cuando** hago clic en el botón "Regresar",
**entonces** se navega de regreso a la vista "Reporte: Asignatura vs Criterios EURACE" **Y** se mantiene visible la matriz completa con los mismos filtros aplicados antes de acceder a la trazabilidad **Y** se preserva el estado de selección de Facultad (ej: "Sistemas") **Y** se preserva el estado de selección de Carrera (ej: "Ingeniería de Software") **Y** se mantienen marcados los checkboxes de "Nivel de aporte" que estaban activos **Y** la matriz muestra los mismos checkmarks verdes de relaciones **Y** no se reinician los filtros ni se pierde el contexto de navegación.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 3 – Visualizar flujo completo de trazabilidad por nivel**

### **Justificación:**

Este criterio es el más crítico porque representa el **núcleo del valor de negocio** de esta Historia de Usuario y valida directamente su objetivo principal: "entender la justificación completa de una relación RAA-RA-EURACE". Las razones específicas son:

1. **Cumplimiento directo del objetivo de la HU:** El usuario (Coordinador de Carrera/CEI) necesita ver **el flujo completo de trazabilidad** para entender cómo un Resultado de Aprendizaje de Asignatura (RAA) se conecta con un Resultado de Aprendizaje de Carrera (RA), cómo esta conexión está justificada académicamente, y finalmente cómo se alinea con un Criterio EUR-ACE. Sin este flujo visible y comprensible, la funcionalidad no cumple su propósito.

2. **Complejidad de información crítica:** Este escenario valida la presentación correcta de **cuatro niveles de información académica interrelacionada**:
   - RAA (nivel asignatura)
   - RA (nivel carrera)
   - Justificación académica (enlace conceptual)
   - Criterio EUR-ACE (estándar de acreditación)
   
   Si cualquiera de estos elementos falta, está incompleto o no es legible, el análisis de acreditación se ve comprometido.

3. **Dependencia de elementos visuales críticos:** La comprensión del flujo depende de:
   - Flechas direccionales que guían la lectura
   - Organización en 4 columnas claramente diferenciadas
   - Cards con información completa (códigos + descripciones)
   - Estructura que permite seguir la lógica de trazabilidad
   
   Si estos elementos fallan, los usuarios no podrán "entender la justificación completa" como requiere la HU.

4. **Validación de reglas de negocio académicas:** Este escenario verifica que:
   - Los RAAs mostrados realmente pertenecen a la asignatura seleccionada
   - Los RAs están correctamente relacionados con los RAAs
   - Las justificaciones explican lógicamente la conexión RA-EUR-ACE
   - Los criterios EUR-ACE corresponden a las relaciones documentadas
   - La información es precisa y auditabable para procesos de acreditación

5. **Riesgo de impacto en acreditación:** Los Coordinadores de Carrera y CEI utilizan esta información para:
   - Evaluar la cobertura de criterios EUR-ACE
   - Identificar brechas en la alineación curricular
   - Preparar evidencias para auditorías de acreditación
   - Tomar decisiones estratégicas sobre programas de estudio
   
   Información incorrecta o ilegible podría resultar en decisiones erróneas con impacto directo en la acreditación institucional.

6. **Evidencia visual exhaustiva en prototipo:** Las imágenes 8-12 (ambos roles) documentan extensivamente este flujo, mostrando múltiples ejemplos con contenido real, lo que indica su importancia crítica desde el diseño.

7. **Patrón repetido por nivel:** Este escenario se aplica a las **tres secciones** (Alto, Medio, Bajo), multiplicando su criticidad. Si el flujo falla en cualquier nivel, toda esa sección pierde valor.

**Recomendación de prueba prioritaria:** 
- Automatizar validación del flujo de 4 columnas con datos reales
- Verificar presencia de todos los elementos (códigos, títulos, descripciones, flechas)
- Validar legibilidad y alineación visual
- Probar con múltiples asignaturas para verificar consistencia de estructura
- Incluir pruebas de regresión exhaustivas al modificar modelo de datos académicos

**Sin este escenario funcionando correctamente, los escenarios 1, 2, 4 y 5 carecen de valor real**, ya que el usuario podría acceder y navegar por la vista, pero no obtendría la información crítica que necesita para su análisis de acreditación.