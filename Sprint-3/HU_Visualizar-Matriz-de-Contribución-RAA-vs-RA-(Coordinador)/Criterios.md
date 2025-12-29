# **CRITERIOS DE ACEPTACIÓN - HU: Visualizar Matriz de Contribución RAA vs RA (Coordinador)**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imágenes 4-7 del Coordinador):**

**C1:** Usuario (Coordinador) accede al menú lateral "MATRICES → RAA vs RA"  
**C2:** Campo de búsqueda "Seleccione una materia:" tiene materia seleccionada  
**C3:** Materia seleccionada tiene RAA definidos  
**C4:** Existen relaciones RAA-RA establecidas para la materia  
**C5:** Usuario aplica filtro "Filtrar por Nivel de Aporte"

**Nota clave:** A diferencia del Profesor, el Coordinador debe PRIMERO seleccionar una materia antes de ver la matriz.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)"  
**A2:** Mostrar campo obligatorio "Seleccione una materia:" con buscador  
**A3:** Mostrar búsqueda dinámica con sugerencias de materias  
**A4:** Permitir selección de materia específica  
**A5:** Mostrar texto explicativo "La tabla muestra la relación entre los Resultados de aprendizaje de Asignatura y los resultados de aprendizaje de una carrera."  
**A6:** Mostrar toggle buttons con "Resultados de Aprendizaje de Asignatura" activo  
**A7:** Mostrar dropdown "Filtrar por Nivel de Aporte"  
**A8:** Mostrar botón "+ Nueva Relación"  
**A9:** Mostrar estructura completa de matriz con filas RAA e iconos ℹ️  
**A10:** Mostrar columnas RA con iconos informativos ℹ️  
**A11:** Mostrar celdas verdes con checkmarks (✓) donde existen relaciones  
**A12:** Permitir identificar visualmente cómo la asignatura aporta a la carrera  
**A13:** Filtrar matriz por nivel de aporte seleccionado

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** | **R9** | **R10** | **R11** | **R12** | **R13** | **R14** | **R15** | **R16** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|---------|---------|---------|---------|
| **C1: Accede a RAA vs RA** | F | F | F | F | F | F | F | F | V | V | V | V | V | V | V | V |
| **C2: Materia seleccionada** | F | F | F | F | V | V | V | V | F | F | F | F | V | V | V | V |
| **C3: Materia tiene RAA** | F | F | V | V | F | F | V | V | F | F | V | V | F | F | V | V |
| **C4: Existen relaciones** | F | V | F | V | F | V | F | V | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1-A2: Mostrar vista inicial | - | - | - | - | - | - | - | - | X | X | X | X | X | X | X | X |
| A5-A12: Mostrar matriz completa | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | X |

**Análisis:** Las reglas R1-R8 son inválidas porque el usuario no ha accedido a la vista. Solo las reglas donde C1=V y C2=V son relevantes.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** |
|-----------|--------|--------|--------|--------|
| **C1: Accede a menú "RAA vs RA"** | V | V | V | V |
| **C2: Materia seleccionada** | F | V | V | V |
| **C3: Materia tiene RAA** | - | - | V | V |
| **C4: Existen relaciones RAA-RA** | - | - | F | V |
| **ACCIONES** |
| A1-A2: Mostrar vista inicial con buscador | X | - | - | - |
| A3-A4: Permitir búsqueda y selección | X | X | X | X |
| A5: Mostrar texto explicativo | - | X | X | X |
| A6-A8: Mostrar controles (toggles, filtro, botón) | - | X | X | X |
| A9-A10: Mostrar estructura matriz (filas/columnas) | - | X | X | X |
| A11: Mostrar celdas verdes con relaciones | - | - | - | X |
| A12: Permitir comprender contribución | - | - | - | X |

**Justificación de minimización:**

- **R1:** Vista inicial sin materia seleccionada - muestra buscador obligatorio.
- **R2:** Materia seleccionada - carga y muestra matriz (puede estar vacía o con datos).
- **R3:** Materia con RAA pero sin relaciones - matriz con estructura pero celdas vacías.
- **R4:** Materia con RAA y relaciones - matriz completa con celdas verdes (happy path).

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 4 reglas

**Análisis de consolidación:**
- R2, R3, R4 pueden consolidarse parcialmente ya que todos muestran la matriz una vez seleccionada la materia
- Sin embargo, representan estados visuales distintos (sin RAA, con RAA sin relaciones, con relaciones)

**Criterios de Aceptación finales:** **4 AC**

1. **AC1:** Acceder a vista inicial y buscar materia
2. **AC2:** Seleccionar materia y visualizar estructura de matriz
3. **AC3:** Visualizar matriz con relaciones RAA-RA existentes (happy path)
4. **AC4:** Visualizar matriz sin relaciones establecidas

No se detectaron AC redundantes. Cada uno valida un aspecto crítico del flujo del Coordinador.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Acceder a vista inicial y buscar materia**

**Dado que** soy un coordinador de carrera **Y** estoy autenticado en el sistema,  
**cuando** accedo al menú lateral en la sección "MATRICES" **Y** hago clic en la opción "RAA vs RA",  
**entonces** se muestra el título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** se presenta la sección "Seleccione una materia:" como campo obligatorio **Y** se visualiza un campo de búsqueda con placeholder "Buscar una materia..." y un icono de lupa **Y** el campo de búsqueda está vacío y listo para recibir texto **Y** NO se muestra ninguna matriz hasta que seleccione una materia **Y** puedo comenzar a escribir para buscar asignaturas de la carrera,  
**Y cuando** comienzo a escribir en el campo de búsqueda (ej: "Ingeniería de"),  
**entonces** se despliega un dropdown con sugerencias de materias que coinciden con el texto ingresado **Y** se muestran opciones como "Ingeniería de Software y Requerimientos" y "Fundamentos de Sistemas de Información." **Y** la búsqueda es dinámica y se actualiza mientras escribo **Y** puedo seleccionar una materia específica de la lista de sugerencias.

---

### **Escenario 2 – Seleccionar materia y visualizar estructura de matriz**

**Dado que** estoy en la vista "RAA vs RA" **Y** el campo de búsqueda muestra sugerencias de materias,  
**cuando** hago clic en una materia específica de la lista (ej: "Ingeniería de Software y Requerimientos"),  
**entonces** el campo de búsqueda se actualiza mostrando la materia seleccionada **Y** se muestra el texto explicativo "La tabla muestra la relación entre los Resultados de aprendizaje de Asignatura y los resultados de aprendizaje de una carrera." **Y** se visualizan los toggle buttons con "Resultados de Aprendizaje de Asignatura" activo en azul con checkbox marcado **Y** se visualiza "Resultados de Aprendizaje Carrera" inactivo en gris **Y** se muestra el dropdown "Filtrar por Nivel de Aporte" visible y funcional **Y** se presenta el botón "+ Nueva Relación" en azul en la esquina superior derecha **Y** se carga y muestra la estructura completa de la matriz con filas correspondientes a los códigos RAA de la asignatura seleccionada (ej: 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1) en fondo azul **Y** cada fila RAA incluye un icono informativo ℹ️ **Y** se muestran las columnas correspondientes a los códigos RA de la carrera (ej: RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6) en fondo gris **Y** cada columna RA incluye un icono informativo ℹ️ **Y** se presenta una cuadrícula completa con todas las intersecciones entre RAA y RA visibles **Y** puedo visualizar cómo está estructurada la matriz de contribución de esta asignatura específica.

---

### **Escenario 3 – Visualizar matriz con relaciones RAA-RA existentes**

**Dado que** he seleccionado una materia (ej: "Ingeniería de Software y Requerimientos") **Y** la matriz está cargada **Y** existen relaciones previamente establecidas entre RAA y RA de esta asignatura,  
**cuando** observo la matriz completa,  
**entonces** se muestran celdas verdes con checkmarks (✓) en las intersecciones donde existe una relación entre un RAA específico de la asignatura y un RA de la carrera **Y** cada celda verde indica visualmente que ese RAA aporta al RA correspondiente **Y** puedo identificar claramente qué RAA de la asignatura (por ejemplo: 1.1, 1.3, 1.4, 2.1, 2.2) están vinculados a qué RA de la carrera (por ejemplo: RG1, RG2, RG3, RE1, RE2, RE3, RE4) **Y** puedo visualizar la distribución de aportes de la asignatura a través de la matriz **Y** puedo entender cómo cada RAA de esta asignatura específica contribuye a los resultados de aprendizaje globales de la carrera **Y** obtengo una vista panorámica completa de todas las relaciones establecidas **Y** puedo evaluar el nivel de contribución de esta asignatura al perfil de egreso de la carrera **Y** puedo identificar patrones de aporte para análisis curricular y acreditación.

---

### **Escenario 4 – Visualizar matriz sin relaciones establecidas**

**Dado que** he seleccionado una materia **Y** la matriz está cargada **Y** la asignatura tiene RAA definidos **Y** NO existen relaciones RAA-RA establecidas para esta asignatura,  
**cuando** observo la matriz,  
**entonces** se muestra la estructura completa de la matriz con todas las filas RAA y columnas RA **Y** todas las celdas de intersección están vacías (sin color de fondo verde ni checkmarks) **Y** puedo identificar visualmente que esta asignatura aún no tiene relaciones documentadas con los RA de la carrera **Y** puedo detectar que esta asignatura requiere vinculación de sus competencias específicas con las competencias globales **Y** puedo usar el botón "+ Nueva Relación" para comenzar a establecer las contribuciones **Y** obtengo información clara de que esta asignatura necesita trabajo de trazabilidad curricular **Y** puedo identificar oportunidades de mejora en la documentación de cómo esta asignatura aporta al perfil de egreso de la carrera.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 3 – Visualizar matriz con relaciones RAA-RA existentes**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumple directamente el objetivo de la Historia de Usuario:** La HU establece "Quiero visualizar la matriz de contribución RAA vs RA de una asignatura para entender cómo las asignaturas aportan a la carrera". El Escenario 3 es el único que valida completamente el valor principal: visualizar y comprender las contribuciones reales existentes.

2. **Rol diferenciador del Coordinador vs Profesor:** Este escenario valida la funcionalidad específica del Coordinador: poder revisar CUALQUIER asignatura de la carrera (no solo las propias), buscarla, seleccionarla y analizar su contribución al perfil de egreso. Esta capacidad es esencial para:
   - Supervisión curricular global de la carrera
   - Evaluación de coherencia entre asignaturas y objetivos de carrera
   - Identificación de asignaturas con mayor/menor contribución
   - Preparación de documentación para acreditación

3. **Happy path con datos reales evidenciado en el prototipo:** Las imágenes 6-7 del Coordinador muestran específicamente este escenario: matriz cargada con materia seleccionada ("Ingeniería de Software y Requerimientos") y múltiples celdas verdes indicando relaciones establecidas. Este es el caso de uso principal diseñado.

4. **Impacto en gestión académica estratégica:** Como Coordinador, la capacidad de visualizar matrices de contribución es crítica para:
   - **Evaluación curricular:** Identificar asignaturas clave vs asignaturas con bajo aporte
   - **Acreditación EUR-ACE:** Demostrar trazabilidad completa desde asignaturas hasta competencias de carrera
   - **Rediseño curricular:** Tomar decisiones informadas sobre qué asignaturas mantener, modificar o eliminar
   - **Balance de carrera:** Asegurar que todos los RA reciben aporte suficiente de múltiples asignaturas
   - **Calidad académica:** Verificar que las competencias prometidas se desarrollan efectivamente

5. **Validación de flujo completo específico del Coordinador:** Este escenario valida la secuencia única:
   - Búsqueda dinámica de materia (funcionalidad que NO tiene el Profesor)
   - Selección de materia específica
   - Carga de matriz con datos de esa materia
   - Visualización correcta de relaciones
   - Interpretación de contribución al perfil de egreso

6. **Prerequisito para análisis y toma de decisiones:** Solo cuando este escenario funciona correctamente, el Coordinador puede:
   - Comparar contribuciones entre diferentes asignaturas
   - Identificar gaps de cobertura en RA de la carrera
   - Priorizar asignaturas para revisión o actualización
   - Generar reportes para comités académicos
   - Justificar cambios curriculares con datos concretos

7. **Mayor frecuencia de uso en gestión académica:** Los Coordinadores revisarán matrices de múltiples asignaturas periódicamente durante:
   - Procesos de autoevaluación
   - Preparación de informes de acreditación
   - Reuniones de planificación curricular
   - Evaluaciones semestrales de la carrera

Los escenarios 1, 2 y 4 son importantes para validar la búsqueda, selección y casos sin datos, pero el Escenario 3 es el que demuestra que el sistema cumple su propósito estratégico: permitir al Coordinador entender y evaluar cómo cada asignatura de la carrera contribuye al perfil de egreso y a los objetivos académicos institucionales.

Un fallo en este escenario compromete la capacidad del Coordinador de ejercer supervisión curricular efectiva, preparar documentación de acreditación confiable, y tomar decisiones informadas sobre la estructura y contenido del programa académico. Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación.