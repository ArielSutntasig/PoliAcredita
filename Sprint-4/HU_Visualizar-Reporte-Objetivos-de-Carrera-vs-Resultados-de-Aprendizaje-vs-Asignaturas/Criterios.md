# CRITERIOS DE ACEPTACIÓN - HU: Visualizar Reporte Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**C1: Facultad seleccionada**
- Estado: Sí / No
- Fuente: Campo de búsqueda "Facultad:" con autocompletado
- Valores observados: "Sistemas", estado vacío "Buscar una facultad"

**C2: Carrera seleccionada**
- Estado: Sí / No
- Fuente: Dropdown "Carrera:" dependiente de Facultad
- Valores observados: "Software", estado inicial "Seleccionar una carrera"

**C3: Al menos un nivel de aporte marcado**
- Estado: Sí / No
- Fuente: Checkboxes "Alto", "Medio", "Bajo"
- Estados observados en imágenes:
  - Imagen 11 (Coordinador): Ninguno marcado
  - Imagen 12 (Coordinador): Solo Alto marcado (☑ Alto, □ Medio, □ Bajo)
  - Imágenes 13-14 (Coordinador): Todos marcados (☑ Alto, ☑ Medio, ☑ Bajo)

#### **Acciones del sistema identificadas:**

**A1: Habilitar dropdown "Carrera:"**
- Condición: Cuando Facultad está seleccionada
- Observado: Dropdown cambia de estado deshabilitado a activo, muestra opciones

**A2: Mostrar estructura de tabla sin datos**
- Condición: Cuando Facultad y Carrera están seleccionadas pero ningún nivel marcado
- Elementos observados: Encabezados de las 3 columnas visibles pero sin filas de contenido

**A3: Generar y mostrar tabla con datos filtrados**
- Condición: Cuando Facultad, Carrera y al menos un nivel de aporte están seleccionados
- Elementos clave:
  - **Encabezados de tabla:** "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas"
  - **Fila tipo 1 (Imagen 12 - Solo Alto):**
    - Columna 1: OPP1 con texto completo
    - Columna 2: RG1 + RG3 (sin RE4)
    - Columna 3: IS-101, IS-305 (2 asignaturas)
    - Siguiente fila: OPP2 con RG1 + RG3, GE-401 (1 asignatura)
  - **Fila expandida (Imágenes 13-14 - Todos los niveles):**
    - Columna 1: OPP1 con texto completo
    - Columna 2: RG1 + RG3 + RE4 (3 resultados)
    - Columna 3: IS-101, IS-305, MA-102, IS-203 (4 asignaturas)
    - Siguiente fila: OPP2 con RG1 + RG3 + RG4, GE-401 + HU-301 + IS-306 (3 asignaturas)
    - Siguiente fila: OPP3 con RE1 + RE2 + RE3, IS-501 + IS-402 + MA-201
    - Siguiente fila: OPP5 con RG1 + RG2 + RE1, CO-101 + HU-301 + IS-403

**A4: Filtrar contenido según niveles marcados**
- Condición: Diferentes checkboxes afectan cantidad de información mostrada
- Observado: 
  - Solo Alto: 2 filas parciales
  - Todos los niveles: 4+ filas completas con más RA y asignaturas por objetivo

**A5: No mostrar contenido de tabla**
- Condición: Cuando no se cumplen todos los filtros requeridos
- Observado: Área de contenido vacía, solo panel de filtros visible

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Facultad | C2: Carrera | C3: Nivel aporte | Acción del Sistema |
|-------|--------------|-------------|------------------|-------------------|
| R1    | No           | No          | No               | A5: No mostrar contenido de tabla |
| R2    | No           | No          | Sí               | A5: No mostrar contenido de tabla |
| R3    | No           | Sí          | No               | A5: No mostrar contenido (estado imposible*) |
| R4    | No           | Sí          | Sí               | A5: No mostrar contenido (estado imposible*) |
| R5    | Sí           | No          | No               | A1: Habilitar Carrera + A5: No mostrar contenido |
| R6    | Sí           | No          | Sí               | A1: Habilitar Carrera + A5: No mostrar contenido |
| R7    | Sí           | Sí          | No               | A1 + A2: Habilitar Carrera + Mostrar estructura sin datos |
| R8    | Sí           | Sí          | Sí               | A1 + A2 + A3 + A4: Mostrar tabla completa con datos |

*Nota: Estado imposible porque Carrera solo se puede seleccionar si Facultad está seleccionada (dependencia en cascada).

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Reglas R1-R4:** Todas resultan en "No mostrar contenido" cuando Facultad=No, independientemente de otros valores. R3-R4 son imposibles por dependencia. **Se fusionan en Regla Minimizada M1**.

2. **Reglas R5-R6:** Cuando Facultad=Sí pero Carrera=No, el sistema habilita Carrera pero no muestra contenido. Nivel de aporte es irrelevante. **Se fusionan en Regla Minimizada M2**.

3. **Regla R7:** Cuando Facultad=Sí y Carrera=Sí pero Nivel=No, muestra estructura de tabla sin datos. **Regla Minimizada M3**.

4. **Regla R8:** Cuando todos los filtros están completos (Facultad=Sí, Carrera=Sí, Nivel=Sí), muestra tabla con datos. **Regla Minimizada M4 (HAPPY PATH)**.

#### **Tabla Minimizada:**

| Regla Min | C1: Facultad | C2: Carrera | C3: Nivel aporte | Acción del Sistema |
|-----------|--------------|-------------|------------------|-------------------|
| **M1**    | No           | -           | -                | A5: No mostrar contenido de tabla |
| **M2**    | Sí           | No          | -                | A1: Habilitar dropdown "Carrera:" + A5: No mostrar contenido |
| **M3**    | Sí           | Sí          | No               | A1 + A2: Habilitar Carrera + Mostrar encabezados sin datos |
| **M4**    | Sí           | Sí          | Sí               | A1 + A2 + A3 + A4: Mostrar tabla completa con trazabilidad OP-RA-Asignaturas |

**Resultado: 4 reglas minimizadas = 4 Criterios de Aceptación base**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 4 reglas minimizadas, procedo a evaluar si hay redundancias o si se requieren criterios adicionales:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre estado sin facultad seleccionada
2. M2 → AC sobre habilitación de carrera cuando facultad está seleccionada
3. M3 → AC sobre estado con facultad y carrera pero sin niveles marcados
4. M4 → AC sobre visualización de tabla completa (HAPPY PATH)

**Análisis de criterios adicionales necesarios:**

Del análisis visual, identifico comportamientos críticos NO cubiertos por la tabla base:

5. **Contenido específico de la tabla:** Las imágenes muestran estructura de 3 columnas con contenido académico específico (OPP con texto completo, múltiples RA por objetivo, múltiples asignaturas con códigos).

6. **Filtrado dinámico por niveles:** Comparación entre imagen 12 (solo Alto: 2 filas) vs imágenes 13-14 (todos: 4+ filas) demuestra que el contenido varía según niveles marcados.

7. **Cambio de carrera:** Similar al reporte anterior, comportamiento de cambiar entre carreras de la misma facultad.

**Criterios eliminados por redundancia:**
- ~~Cambio entre carreras de la misma facultad~~: Redundante con M2 y M4, es simplemente una repetición de la selección.
- ~~Estado inicial de página~~: M1 ya lo cubre.

**Criterios consolidados:**
- M4 debe incluir validación de contenido específico observado en imágenes
- El filtrado dinámico (nivel 5 adicional) se fusiona con validación de contenido en M4

**TOTAL FINAL: 5 Criterios de Aceptación**
- 4 de la tabla de decisión base
- 1 adicional para validar el comportamiento de filtrado dinámico por niveles (cambio entre solo Alto vs todos los niveles)

**Justificación de estructura:**
- M1: Caso base sin filtros
- M2: Habilitación en cascada
- M3: Estado intermedio sin datos
- M4: Happy path con contenido completo (todos los niveles)
- Adicional: Filtrado parcial (solo nivel Alto) para validar comportamiento diferencial

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

Aplicando la guía de estilo internalizada:

---

### **Escenario 1 – Estado inicial sin filtros aplicados**

**Dado que** estoy en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" **Y** soy un Coordinador de Carrera o CEI en el sistema,
**cuando** accedo al reporte sin haber seleccionado filtros,
**entonces** se muestra el título "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" **Y** se presenta la descripción "Visualice la alineación entre objetivos, resultados y asignaturas del programa académico." **Y** se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad" **Y** se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera" en estado deshabilitado **Y** se muestran los checkboxes "Alto", "Medio", "Bajo" desmarcados en la sección "Nivel de aporte" **Y** no se muestran los encabezados de tabla **Y** no se muestra contenido de trazabilidad **Y** el área de contenido principal permanece vacía.

---

### **Escenario 2 – Seleccionar facultad y habilitar carrera**

**Dado que** estoy en el reporte "Reporte: Objetivos de Carrera vs Resultados de Aprendizaje vs Asignaturas" **Y** el dropdown "Carrera:" está deshabilitado,
**cuando** escribo en el campo "Facultad:" **Y** selecciono "Sistemas" de las opciones desplegadas,
**entonces** el campo "Facultad:" se actualiza con el valor "Sistemas" **Y** el dropdown "Carrera:" se habilita **Y** el dropdown "Carrera:" muestra el texto "Seleccionar una carrera" disponible para interacción **Y** no se muestra contenido de tabla **Y** el área de contenido principal permanece vacía hasta completar los filtros.

---

### **Escenario 3 – Seleccionar carrera sin marcar niveles de aporte**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** el dropdown "Carrera:" está habilitado,
**cuando** hago clic en el dropdown "Carrera:" **Y** selecciono "Software" de las opciones disponibles,
**entonces** el dropdown "Carrera:" se actualiza con el valor "Software" **Y** no se muestra la tabla con datos **Y** los checkboxes "Alto", "Medio", "Bajo" permanecen visibles y desmarcados **Y** el área de contenido principal permanece vacía **Y** es evidente que se requiere marcar al menos un nivel de aporte para visualizar datos.

---

### **Escenario 4 – Generar tabla completa con todos los niveles de aporte**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** tengo la carrera "Software" seleccionada,
**cuando** marco los checkboxes "Alto", "Medio" y "Bajo" simultáneamente,
**entonces** se genera una tabla de trazabilidad con tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas" **Y** se presentan múltiples filas de trazabilidad completa **Y** la primera fila muestra en columna "Objetivos de carrera" el texto "OPP1: Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de software innovadores y eficientes, aplicando metodologías ágiles y estándares de calidad internacional." **Y** en columna "Resultados de Aprendizaje" se muestran múltiples resultados con viñetas: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos.", "RE4: Diseña arquitecturas de software escalables y de alto rendimiento." **Y** en columna "Asignaturas" se muestran: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web", "MA-102: Álgebra Lineal", "IS-203: Bases de Datos" **Y** se presenta una segunda fila con OPP2 incluyendo RG1, RG3, RG4 y asignaturas GE-401, HU-301, IS-306 **Y** se presenta una tercera fila con OPP3 incluyendo RE1, RE2, RE3 y asignaturas IS-501, IS-402, MA-201 **Y** se presenta una cuarta fila con OPP5 incluyendo RG1, RG2, RE1 y asignaturas CO-101, HU-301, IS-403 **Y** cada celda muestra el contenido completo y legible **Y** la tabla presenta la trazabilidad completa desde objetivos hasta asignaturas específicas.

---

### **Escenario 5 – Filtrar tabla por nivel de aporte específico**

**Dado que** tengo la facultad "Sistemas" y carrera "Software" seleccionadas **Y** los checkboxes de nivel de aporte están desmarcados,
**cuando** marco únicamente el checkbox "Alto" en "Nivel de aporte:",
**entonces** se genera una tabla de trazabilidad con las tres columnas: "Objetivos de carrera", "Resultados de Aprendizaje", "Asignaturas" **Y** se muestran únicamente las filas correspondientes al nivel de aporte alto **Y** la primera fila muestra OPP1 con texto completo "Formar profesionales capaces de analizar, diseñar, desarrollar y mantener sistemas de software innovadores y eficientes, aplicando metodologías ágiles y estándares de calidad internacional." **Y** en "Resultados de Aprendizaje" se muestran únicamente: "RG1: Identifica y aplica algoritmos de optimización para la mejora de sistemas.", "RG3: Modela sistemas complejos utilizando paradigmas de programación orientada a objetos." (sin RE4) **Y** en "Asignaturas" se muestran únicamente: "IS-101: Programación Avanzada", "IS-305: Desarrollo Web" (sin MA-102 ni IS-203) **Y** la segunda fila muestra OPP2 con RG1, RG3 (sin RG4) y asignatura GE-401 únicamente **Y** se ocultan los objetivos, resultados y asignaturas que corresponden exclusivamente a niveles medio y bajo **Y** el contenido mostrado es un subconjunto del contenido cuando todos los niveles están marcados **Y** la tabla se actualiza automáticamente sin recargar la página.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 4 – Generar tabla completa con todos los niveles de aporte**

### **Justificación:**

Este criterio representa el **happy path principal** y el núcleo de valor de la Historia de Usuario. Es el más crítico por las siguientes razones:

1. **Valor de negocio directo:** Cumple directamente con el objetivo de la HU "visualizar el reporte de alineación entre objetivos de carrera, resultados de aprendizaje y asignaturas para verificar el aporte de una asignatura al Perfil profesional". Sin esta visualización completa, el Coordinador de Carrera o CEI no puede realizar el análisis de alineación curricular.

2. **Validación de trazabilidad académica completa:** Este escenario valida la cadena completa de trazabilidad:
   - **Objetivos de Carrera (OPP)** → Define el perfil profesional esperado
   - **Resultados de Aprendizaje (RA)** → Especifica competencias que contribuyen al perfil
   - **Asignaturas** → Identifica cursos específicos que desarrollan esas competencias
   
   Esta trazabilidad es fundamental para demostrar cómo el currículo contribuye al perfil de egreso.

3. **Complejidad de integración de datos:** Integra información de tres dominios académicos distintos:
   - Base de datos de Objetivos de Programa
   - Repositorio de Resultados de Aprendizaje de Carrera
   - Catálogo de Asignaturas con sus códigos
   
   Si cualquiera de estas integraciones falla, el reporte pierde su valor.

4. **Dependencia de funcionalidades posteriores:** El Escenario 5 (filtrado parcial) solo tiene sentido si el Escenario 4 funciona correctamente, ya que el filtrado es una reducción del conjunto completo.

5. **Validación de relaciones múltiples:** Este escenario verifica que:
   - Un objetivo puede tener múltiples resultados de aprendizaje (OPP1 → RG1, RG3, RE4)
   - Un resultado puede estar asociado a múltiples asignaturas (RG1 → IS-101, IS-305, etc.)
   - Múltiples objetivos se muestran correctamente en filas separadas
   - La información se presenta en formato legible con viñetas para listas

6. **Evidencia de completitud académica:** Los datos específicos observados en las imágenes (OPP1-OPP5, múltiples RG/RE, códigos de asignaturas como IS-101, GE-401, MA-102) demuestran la complejidad y riqueza de información que debe manejarse. Este escenario valida que toda esta información se muestre correctamente.

7. **Punto de fallo más riesgoso:** Si la tabla no se genera con información completa:
   - Los coordinadores podrían concluir erróneamente que faltan relaciones
   - El análisis de cobertura del perfil profesional sería incompleto
   - Las decisiones curriculares se basarían en información parcial
   - El cumplimiento de estándares de acreditación no podría verificarse adecuadamente

8. **Validación de formato académico:** El escenario valida que:
   - Los OPP se muestran con su texto completo (descripción larga)
   - Los RA se listan con viñetas y códigos distintivos (RG1, RG3, RE4)
   - Las asignaturas incluyen código y nombre (IS-101: Programación Avanzada)
   - La estructura permite lectura clara de izquierda a derecha

9. **Base para análisis de brechas:** Los usuarios necesitan ver el panorama completo (todos los niveles) para:
   - Identificar qué objetivos tienen baja cobertura de asignaturas
   - Detectar asignaturas que aportan a múltiples objetivos (como HU-301)
   - Evaluar el balance de contribuciones Alto/Medio/Bajo
   - Planificar ajustes curriculares basados en análisis integral

10. **Evidencia visual exhaustiva en prototipo:** Las imágenes 13-14 (Coordinador) y equivalentes (CEI) muestran este escenario con datos reales y múltiples filas, indicando que es la vista principal y más importante del reporte.

**Recomendación de prueba prioritaria:**
- Validar con datos reales de múltiples carreras
- Verificar que todos los OPP de la carrera se muestran
- Confirmar que las relaciones OP-RA-Asignatura son correctas según modelo de datos
- Probar con casos de objetivos con muchos vs pocos RA
- Validar formato y legibilidad de textos largos en celdas
- Automatizar verificación de integridad de trazabilidad
- Incluir en suite de regresión para cada cambio en modelo académico

**Sin este escenario funcionando correctamente, el propósito fundamental de "verificar el aporte de una asignatura al Perfil profesional" no puede cumplirse**, haciendo que la funcionalidad completa carezca de valor para los procesos de gestión curricular y acreditación.