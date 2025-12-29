# **CRITERIOS DE ACEPTACIÓN - HU: Buscar Asignatura para Matriz RAA vs RA**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imágenes 4-5 del Coordinador):**

**C1:** Usuario accede a vista "RAA vs RA" (menú lateral MATRICES)  
**C2:** Campo de búsqueda "Buscar una materia..." contiene texto  
**C3:** Texto ingresado coincide con nombres de asignaturas existentes  
**C4:** Usuario selecciona una materia del dropdown de resultados  
**C5:** Existen asignaturas en la carrera del coordinador

**Nota:** Esta HU se enfoca en la búsqueda específica que diferencia al Coordinador del Profesor, quien accede directamente desde el contexto de una asignatura.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)"  
**A2:** Mostrar campo obligatorio "Seleccione una materia:"  
**A3:** Mostrar campo de búsqueda con placeholder "Buscar una materia..." y icono de lupa  
**A4:** Activar búsqueda dinámica mientras el usuario escribe  
**A5:** Mostrar dropdown con sugerencias de materias que coinciden  
**A6:** Filtrar y actualizar lista de sugerencias en tiempo real  
**A7:** Resaltar/mostrar materias coincidentes (ej: "Ingeniería de Software y Requerimientos", "Fundamentos de Sistemas de Información.")  
**A8:** Permitir selección mediante clic en una sugerencia  
**A9:** Actualizar campo de búsqueda con materia seleccionada  
**A10:** Cargar matriz RAA vs RA de la materia seleccionada  
**A11:** Mostrar mensaje/estado cuando no hay coincidencias  
**A12:** Mantener campo de búsqueda activo para nueva búsqueda

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** | **R9** | **R10** | **R11** | **R12** | **R13** | **R14** | **R15** | **R16** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|---------|---------|---------|---------|
| **C1: Accede a vista RAA vs RA** | F | F | F | F | F | F | F | F | V | V | V | V | V | V | V | V |
| **C2: Campo búsqueda con texto** | F | F | F | F | V | V | V | V | F | F | F | F | V | V | V | V |
| **C3: Texto coincide con materias** | F | F | V | V | F | F | V | V | F | F | V | V | F | F | V | V |
| **C4: Selecciona materia** | F | V | F | V | F | V | F | V | F | V | F | V | F | V | F | V |
| **C5: Existen asignaturas** | F | F | F | F | F | F | F | F | V | V | V | V | V | V | V | V |
| **ACCIONES** |
| A1-A3: Mostrar vista inicial búsqueda | - | - | - | - | - | - | - | - | X | X | X | X | X | X | X | X |
| A4-A7: Búsqueda dinámica con resultados | - | - | - | - | - | - | - | - | - | - | - | - | - | - | X | X |
| A8-A10: Seleccionar y cargar matriz | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | X |
| A11: Sin coincidencias | - | - | - | - | - | - | - | - | - | - | - | - | X | X | - | - |

**Análisis:** R1-R8 son inválidas (sin acceso a vista), R9-R12 representan estados sin búsqueda activa o sin materias disponibles.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** |
|-----------|--------|--------|--------|--------|
| **C1: Accede a vista "RAA vs RA"** | V | V | V | V |
| **C2: Campo búsqueda con texto** | F | V | V | V |
| **C3: Texto coincide con materias** | - | F | V | V |
| **C4: Selecciona materia del dropdown** | - | - | F | V |
| **C5: Existen asignaturas en carrera** | V | V | V | V |
| **ACCIONES** |
| A1-A3: Mostrar campo búsqueda vacío | X | - | - | - |
| A4: Activar búsqueda dinámica | - | X | X | X |
| A5-A7: Mostrar dropdown con sugerencias | - | - | X | X |
| A8: Permitir selección de materia | - | - | X | X |
| A9-A10: Cargar matriz de materia seleccionada | - | - | - | X |
| A11: Indicar sin coincidencias | - | X | - | - |
| A12: Mantener búsqueda activa | X | X | X | - |

**Justificación de minimización:**

- **R1:** Vista inicial sin búsqueda - muestra campo vacío listo para escribir.
- **R2:** Usuario escribe pero no hay coincidencias - indica ausencia de resultados.
- **R3:** Usuario escribe y hay coincidencias - muestra dropdown con sugerencias.
- **R4:** Usuario selecciona materia del dropdown - carga matriz (happy path completo).

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 4 reglas

**Análisis:** Cada regla representa un paso válido en el flujo de búsqueda:
1. Estado inicial
2. Búsqueda sin resultados
3. Búsqueda con resultados
4. Selección y carga de matriz

**Criterios de Aceptación finales:** **4 AC**

No se detectaron AC redundantes. Cada uno valida un aspecto crítico de la funcionalidad de búsqueda del Coordinador.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar campo de búsqueda inicial para seleccionar materia**

**Dado que** soy un coordinador de carrera **Y** estoy autenticado en el sistema,  
**cuando** accedo al menú lateral en la sección "MATRICES" **Y** hago clic en la opción "RAA vs RA",  
**entonces** se muestra el título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" en la parte superior **Y** se presenta la sección "Seleccione una materia:" claramente identificada **Y** se visualiza el campo de búsqueda con el placeholder "Buscar una materia..." **Y** se muestra el icono de lupa junto al campo de búsqueda **Y** el campo de búsqueda está vacío y activo, listo para recibir texto **Y** NO se muestra ninguna matriz hasta que seleccione una materia específica **Y** puedo hacer clic en el campo para comenzar a buscar asignaturas de la carrera **Y** el cursor se posiciona automáticamente en el campo de búsqueda para facilitar la entrada de texto.

---

### **Escenario 2 – Buscar asignatura sin resultados coincidentes**

**Dado que** estoy en la vista "RAA vs RA" **Y** el campo de búsqueda está activo,  
**cuando** escribo un término de búsqueda que NO coincide con ninguna asignatura existente en la carrera (ej: "XXXZZZ" o "MateriaInexistente"),  
**entonces** la búsqueda se ejecuta dinámicamente mientras escribo **Y** NO se despliega ningún dropdown con sugerencias **Y** se indica claramente que no hay coincidencias (mediante ausencia de resultados o mensaje apropiado) **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** puedo modificar el término de búsqueda para intentar una nueva búsqueda **Y** el campo permanece activo para que pueda corregir mi búsqueda **Y** NO se carga ninguna matriz ya que no hay materia seleccionada.

---

### **Escenario 3 – Buscar asignatura con resultados coincidentes exitosamente**

**Dado que** estoy en la vista "RAA vs RA" **Y** el campo de búsqueda está activo **Y** existen asignaturas en la carrera,  
**cuando** escribo un término de búsqueda que coincide con nombres de asignaturas (ej: escribo "Ingeniería de"),  
**entonces** la búsqueda se ejecuta dinámicamente mientras escribo cada carácter **Y** se despliega automáticamente un dropdown debajo del campo de búsqueda **Y** el dropdown muestra una lista de asignaturas que coinciden con el texto ingresado **Y** se presentan sugerencias como "Ingeniería de Software y Requerimientos" y "Fundamentos de Sistemas de Información." **Y** los resultados se actualizan en tiempo real conforme continúo escribiendo más caracteres **Y** cada sugerencia en el dropdown es clickeable **Y** puedo ver claramente las opciones disponibles que coinciden con mi búsqueda **Y** la búsqueda es case-insensitive y busca coincidencias parciales en los nombres de las asignaturas **Y** encuentro rápidamente las asignaturas para consultar sus contribuciones.

---

### **Escenario 4 – Seleccionar asignatura y cargar su matriz de contribuciones**

**Dado que** estoy en la vista "RAA vs RA" **Y** he escrito en el campo de búsqueda (ej: "Ingeniería de") **Y** se muestra un dropdown con sugerencias de asignaturas coincidentes,  
**cuando** hago clic en una asignatura específica del dropdown (ej: hago clic en "Ingeniería de Software y Requerimientos"),  
**entonces** el dropdown se cierra automáticamente **Y** el campo de búsqueda se actualiza mostrando el nombre completo de la asignatura seleccionada ("Ingeniería de Software y Requerimientos") **Y** el sistema carga la matriz RAA vs RA específica de esa asignatura **Y** se muestra el texto explicativo "La tabla muestra la relación entre los Resultados de aprendizaje de Asignatura y los resultados de aprendizaje de una carrera." **Y** se visualizan los toggle buttons con "Resultados de Aprendizaje de Asignatura" activo **Y** se presenta el dropdown "Filtrar por Nivel de Aporte" **Y** se muestra el botón "+ Nueva Relación" **Y** se carga la estructura completa de la matriz con las filas RAA de la asignatura seleccionada y las columnas RA de la carrera **Y** se muestran las celdas verdes con checkmarks donde existen relaciones establecidas **Y** puedo visualizar todas las contribuciones de esta asignatura específica a los resultados de aprendizaje de la carrera **Y** he completado exitosamente la búsqueda y puedo ahora consultar las contribuciones de la asignatura seleccionada.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 4 – Seleccionar asignatura y cargar su matriz de contribuciones**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento completo del objetivo de la Historia de Usuario:** La HU establece "Quiero buscar una asignatura para la matriz RAA vs RA para consultar sus contribuciones". El Escenario 4 es el único que valida el flujo completo exitoso: buscar → encontrar → seleccionar → cargar matriz → consultar contribuciones.

2. **Happy path de la funcionalidad distintiva del Coordinador:** Este escenario representa el caso de uso principal que diferencia al Coordinador del Profesor. Mientras el Profesor accede directamente desde su asignatura, el Coordinador DEBE poder buscar y seleccionar CUALQUIER asignatura de la carrera. Esta es su función supervisora y analítica central.

3. **Evidencia directa en el prototipo:** Las imágenes 4-6 del Coordinador muestran específicamente este flujo completo:
   - Imagen 4: Estado inicial con campo de búsqueda
   - Imagen 5: Búsqueda activa con "Ingeniería de" mostrando sugerencias
   - Imagen 6: Matriz cargada con materia seleccionada visible

4. **Integración de múltiples componentes críticos:** Este escenario valida la correcta integración de:
   - Búsqueda dinámica funcional
   - Dropdown de sugerencias operativo
   - Selección mediante clic efectiva
   - Actualización del campo con materia seleccionada
   - Carga de datos específicos de la asignatura
   - Renderizado completo de la matriz
   - Sincronización entre búsqueda y visualización

5. **Impacto directo en supervisión curricular:** La capacidad del Coordinador de buscar y consultar contribuciones de cualquier asignatura es crítica para:
   - **Evaluación comparativa:** Analizar múltiples asignaturas para identificar patrones
   - **Auditorías académicas:** Revisar sistemáticamente todas las asignaturas de la carrera
   - **Identificación de problemas:** Detectar asignaturas sin relaciones o con bajo aporte
   - **Acreditación:** Verificar que todas las asignaturas contribuyen apropiadamente
   - **Toma de decisiones:** Basar decisiones curriculares en datos específicos de asignaturas

6. **Caso de uso más frecuente en gestión académica:** Los Coordinadores ejecutarán este flujo múltiples veces en cada sesión de trabajo cuando:
   - Preparan informes de autoevaluación
   - Revisan el portafolio de asignaturas
   - Analizan la distribución de competencias
   - Comparan contribuciones entre asignaturas similares
   - Validan la cobertura de RA por el conjunto de asignaturas

7. **Prerequisito para análisis de contribuciones:** Sin esta funcionalidad operando correctamente:
   - El Coordinador no puede acceder a matrices de asignaturas específicas
   - No puede cumplir su rol de supervisión curricular
   - Pierde la capacidad de análisis comparativo
   - No puede consultar contribuciones (objetivo explícito de la HU)
   - Se bloquea todo el flujo de evaluación y mejora curricular

Los escenarios 1, 2 y 3 son importantes para validar el estado inicial, casos sin resultados y búsqueda dinámica, pero el Escenario 4 es el que demuestra que el sistema cumple su propósito fundamental: permitir al Coordinador buscar exitosamente una asignatura específica y acceder inmediatamente a sus contribuciones documentadas.

Un fallo en este escenario hace que toda la funcionalidad de búsqueda sea inútil, ya que el Coordinador quedaría bloqueado sin poder consultar las contribuciones de asignaturas específicas, comprometiendo su capacidad de supervisión, análisis y toma de decisiones curriculares. Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación.