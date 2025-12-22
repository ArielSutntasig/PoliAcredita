# CRITERIOS DE ACEPTACIÓN - HU: Visualizar materia al relacionar RAA vs RA

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**C1: Asignatura seleccionada/activa**
- Estado: Sí / No
- Fuente: Contexto del sistema - la asignatura debe estar seleccionada para mostrar sus RAA
- Observado en imagen: "Ingeniería de Software y Requerimientos (ISWD414)" visible en encabezado principal
- Resultado: La materia es el contexto para mostrar la matriz RAA vs RA

**C2: Pestaña "Matriz RAA vs RA" activa**
- Estado: Sí / No
- Fuente: Sistema de pestañas en la parte superior
- Observado: Pestaña "Matriz RAA vs RA" con fondo azul oscuro (activa)
- Otras pestañas: "Asignatura (PEA)", "Resultados de Aprendizaje (RAA)"

**C3: Toggle en "Resultados de Aprendizaje de Asignatura"**
- Estado: Sí / No
- Fuente: Toggle switch debajo del título de la matriz
- Opciones: "Resultados de Aprendizaje de Asignatura" (azul - seleccionado) vs "Resultados de Aprendizaje Carrera" (gris)
- Observado: Posición izquierda (RAA) seleccionada

#### **Acciones del sistema identificadas:**

**A1: Mostrar nombre completo de la asignatura en encabezado**
- Condición: Asignatura seleccionada
- Observado: "Ingeniería de Software y Requerimientos (ISWD414)"
- Formato: Nombre completo + código entre paréntesis
- Resultado: Profesor sabe exactamente qué materia está analizando

**A2: Mostrar matriz RAA vs RA**
- Condición: Pestaña "Matriz RAA vs RA" activa
- Elementos observados:
  - Título: "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)"
  - Toggle para cambiar vista
  - Dropdown "Filtrar por Nivel de Aporte"
  - Botón "+ Nueva Relación"
  - Estructura de matriz con filas y columnas

**A3: Mostrar RAA de la asignatura en filas (eje Y)**
- Condición: Toggle en "Resultados de Aprendizaje de Asignatura"
- Observado: Filas con códigos 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1
- Cada RAA tiene:
  - Código numérico (formato X.Y)
  - Fondo azul
  - Icono de información (i) para ver detalles

**A4: Mostrar RA de carrera en columnas (eje X)**
- Condición: Siempre visible cuando matriz está activa
- Observado: Columnas con códigos RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6
- Cada RA tiene:
  - Código alfanumérico (RG# o RE#)
  - Icono de información (i) para ver detalles

**A5: Mostrar relaciones existentes RAA-RA**
- Condición: Existen relaciones previamente creadas
- Observado: Checkmarks (✓) en celdas con fondo verde/turquesa
- Relaciones visibles:
  - 1.1 ↔ RE1
  - 1.2 ↔ RE2
  - 1.3 ↔ RG2
  - 1.4 ↔ RG3
  - 2.1 ↔ RE3
  - 2.2 ↔ RG1
  - 2.2 ↔ RE4
  - 3.1 ↔ RE6

**A6: Habilitar funcionalidad de gestión de relaciones**
- Elementos:
  - Botón "+ Nueva Relación" para crear nuevas relaciones
  - Dropdown "Filtrar por Nivel de Aporte" para filtrar visualización
  - Iconos de información para ver detalles de RAA y RA

**A7: No mostrar matriz (vista alternativa)**
- Condición: Asignatura no seleccionada o pestaña diferente activa
- Resultado: Usuario no puede ver las relaciones RAA-RA

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Asignatura | C2: Pestaña RAA vs RA | C3: Toggle en RAA | Acción del Sistema |
|-------|----------------|----------------------|-------------------|-------------------|
| R1    | No             | No                   | No                | A7: No mostrar matriz |
| R2    | No             | No                   | Sí                | A7: No mostrar matriz (toggle irrelevante*) |
| R3    | No             | Sí                   | No                | A7: No mostrar matriz (estado imposible**) |
| R4    | No             | Sí                   | Sí                | A7: No mostrar matriz (estado imposible**) |
| R5    | Sí             | No                   | No                | A1: Mostrar nombre asignatura solamente |
| R6    | Sí             | No                   | Sí                | A1: Mostrar nombre asignatura solamente (toggle irrelevante*) |
| R7    | Sí             | Sí                   | No                | A1 + A2 + A4: Mostrar materia + matriz con RA en filas (vista alternativa) |
| R8    | Sí             | Sí                   | Sí                | A1 + A2 + A3 + A4 + A5 + A6: Vista completa con materia visible (HAPPY PATH) |

*Toggle irrelevante: El toggle solo tiene efecto cuando la matriz está visible
**Estado imposible: Si no hay asignatura, no se puede acceder a la pestaña de matriz RAA vs RA de esa asignatura

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Reglas R1-R4:** Todas resultan en no mostrar la matriz cuando Asignatura=No. Si no hay asignatura seleccionada, no tiene sentido mostrar sus RAA ni la matriz. El estado del toggle es irrelevante. **Se fusionan en M1**.

2. **Reglas R5-R6:** Cuando hay asignatura pero la pestaña de matriz no está activa, solo se muestra el nombre de la asignatura (posiblemente en otras pestañas como "Asignatura (PEA)" o "Resultados de Aprendizaje (RAA)"). El toggle es irrelevante. **Se fusionan en M2**.

3. **Regla R7:** Cuando la asignatura y pestaña están activas pero toggle está en "Resultados de Aprendizaje Carrera", se muestra una vista alternativa de la matriz (RA en filas en lugar de RAA). **Se mantiene como M3**.

4. **Regla R8:** Cuando todo está activo (asignatura, pestaña, toggle en RAA), se muestra la vista completa que permite al profesor "observar la materia al relacionar RAA con RA". **Se mantiene como M4 (HAPPY PATH)**.

#### **Tabla Minimizada:**

| Regla Min | C1: Asignatura | C2: Pestaña RAA vs RA | C3: Toggle en RAA | Acción del Sistema |
|-----------|----------------|----------------------|-------------------|-------------------|
| **M1**    | No             | -                    | -                 | A7: No mostrar matriz ni contexto de asignatura |
| **M2**    | Sí             | No                   | -                 | A1: Mostrar solo nombre de asignatura (otra vista) |
| **M3**    | Sí             | Sí                   | No                | A1 + A2 + A4: Mostrar materia + matriz con RA en filas |
| **M4**    | Sí             | Sí                   | Sí                | A1 + A2 + A3 + A4 + A5 + A6: Vista completa RAA vs RA |

**Resultado: 4 reglas minimizadas**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 4 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre ausencia de asignatura (caso negativo)
2. M2 → AC sobre asignatura seleccionada pero matriz no activa
3. M3 → AC sobre vista alternativa (toggle en RA)
4. M4 → AC sobre vista principal RAA vs RA (HAPPY PATH)

**Análisis de criterios adicionales necesarios:**

Del análisis visual y el objetivo de la HU ("observar la materia al relacionar un RAA con RA"), identifico:

5. **Ver detalles de RAA/RA con iconos de información:** Los iconos (i) permiten al profesor ver descripciones completas de cada RAA y RA para entender mejor las relaciones.

6. **Identificar relaciones existentes visualmente:** Los checkmarks verdes permiten al profesor ver rápidamente qué RAA están relacionados con qué RA de la materia actual.

**Criterios a ELIMINAR por redundancia:**

- **M1 (Sin asignatura):** Este es un caso negativo que no aporta valor a la funcionalidad principal de "observar la materia al relacionar RAA con RA". Es un prerequisito del sistema, no un criterio de aceptación de esta HU específica. **ELIMINADO por ser prerequisito del sistema**.

- **M2 (Asignatura pero otra pestaña):** Este escenario no cumple el objetivo de la HU. El profesor no está en la matriz RAA vs RA, por lo que no puede "relacionar RAA con RA". **ELIMINADO por no cumplir objetivo de la HU**.

- **Criterio adicional de ver detalles (punto 5):** Aunque importante, los iconos de información son auxiliares. El núcleo de "observar la materia al relacionar" es ver la matriz con el nombre de la asignatura y las relaciones, no los detalles individuales. **ELIMINADO por ser funcionalidad auxiliar, no core de la HU**.

**TOTAL FINAL: 3 Criterios de Aceptación**
- 1 de M3 (vista alternativa con RA en filas)
- 1 de M4 (happy path con RAA en filas)
- 1 adicional para identificación visual de relaciones existentes

**Justificación de eliminaciones:**
- **M1:** Prerequisito del sistema, no funcionalidad específica de esta HU
- **M2:** No cumple objetivo de "relacionar RAA con RA" ya que usuario no está en la matriz
- **Detalles de RAA/RA:** Funcionalidad auxiliar, no el core de "observar la materia al relacionar"

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

---

### **Escenario 1 – Visualizar materia con matriz RAA vs RA activa**

**Dado que** soy un profesor en el sistema **Y** he seleccionado la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" **Y** estoy en la sección "MATRICES" del menú lateral,
**cuando** hago clic en la pestaña "Matriz RAA vs RA",
**entonces** se muestra el nombre completo de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" en el encabezado principal de la página **Y** se presenta el título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** se muestra el toggle con las opciones "Resultados de Aprendizaje de Asignatura" y "Resultados de Aprendizaje Carrera" **Y** el toggle está posicionado en "Resultados de Aprendizaje de Asignatura" (opción izquierda en azul) **Y** se presenta la matriz con los RAA de la asignatura en las filas del eje Y: 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1 con fondo azul **Y** se muestran los RA de carrera en las columnas del eje X: RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6 **Y** cada código de RAA y RA incluye un icono de información (i) **Y** se muestra el dropdown "Filtrar por Nivel de Aporte" **Y** se presenta el botón "+ Nueva Relación" en la esquina superior derecha **Y** la materia es claramente visible permitiéndome identificar el contexto de las relaciones RAA-RA que estoy observando.

---

### **Escenario 2 – Visualizar relaciones existentes entre RAA y RA de la materia**

**Dado que** estoy visualizando la matriz RAA vs RA de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" **Y** el toggle está en "Resultados de Aprendizaje de Asignatura",
**cuando** observo el contenido de la matriz,
**entonces** se muestran checkmarks (✓) con fondo verde/turquesa en las intersecciones donde existe una relación entre un RAA y un RA **Y** específicamente veo las relaciones: RAA 1.1 con RE1, RAA 1.2 con RE2, RAA 1.3 con RG2, RAA 1.4 con RG3, RAA 2.1 con RE3, RAA 2.2 con RG1, RAA 2.2 con RE4, RAA 3.1 con RE6 **Y** las celdas sin relación permanecen vacías sin checkmark **Y** puedo identificar visualmente y de forma rápida qué resultados de aprendizaje de esta asignatura específica contribuyen a qué resultados de aprendizaje de la carrera **Y** el nombre de la asignatura permanece visible en el encabezado confirmando el contexto de las relaciones que estoy analizando.

---

### **Escenario 3 – Cambiar vista a Resultados de Aprendizaje de Carrera**

**Dado que** estoy visualizando la matriz RAA vs RA de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" **Y** el toggle está en "Resultados de Aprendizaje de Asignatura",
**cuando** hago clic en la opción "Resultados de Aprendizaje Carrera" del toggle,
**entonces** el toggle cambia de posición mostrando "Resultados de Aprendizaje Carrera" en azul (derecha) y "Resultados de Aprendizaje de Asignatura" en gris (izquierda) **Y** la matriz se reorganiza mostrando los RA de carrera (RG1, RG2, RG3, RE1, RE2, RE3, etc.) en las filas del eje Y **Y** los RAA de la asignatura (1.1, 1.2, 1.3, etc.) se muestran en las columnas del eje X **Y** las relaciones existentes se mantienen visibles con checkmarks verdes en las intersecciones correspondientes pero en la nueva orientación **Y** el nombre de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" permanece visible en el encabezado **Y** puedo alternar entre ambas vistas para analizar las relaciones desde diferentes perspectivas mientras siempre observo la materia que estoy analizando.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 1 – Visualizar materia con matriz RAA vs RA activa**

### **Justificación:**

Este criterio es el más crítico porque valida **directamente el objetivo central de la Historia de Usuario**: "observar la materia al relacionar un RAA con RA". Las razones específicas son:

1. **Cumplimiento literal del objetivo de la HU:** El profesor necesita **observar la materia** (nombre de la asignatura visible) **al relacionar** RAA con RA (matriz visible). Este escenario valida que:
   - El nombre completo de la asignatura es claramente visible: "Ingeniería de Software y Requerimientos (ISWD414)"
   - La matriz RAA vs RA está activa y visible
   - Los elementos están organizados para mostrar las relaciones
   - El profesor tiene el contexto completo para "definir correctamente el aporte de una asignatura"

2. **Provisión de contexto crítico:** Sin el nombre de la asignatura visible, el profesor podría estar trabajando con la matriz incorrecta. Este escenario garantiza que:
   - El profesor siempre sabe qué materia está analizando
   - No hay confusión entre diferentes asignaturas
   - Las decisiones sobre el aporte de la asignatura se toman con el contexto correcto
   - Se previenen errores de asignación de relaciones a la materia incorrecta

3. **Punto de entrada a la funcionalidad:** Este es el escenario que activa toda la funcionalidad. Sin este escenario funcionando:
   - El profesor no puede acceder a la matriz RAA vs RA
   - No se muestran los RAA de la asignatura
   - No se pueden visualizar las relaciones existentes
   - Los escenarios 2 y 3 no tienen sentido

4. **Validación de integración UI crítica:** Este escenario confirma que múltiples componentes trabajan juntos:
   - Sistema de navegación (menú lateral → RAA vs RA)
   - Sistema de pestañas (activación de "Matriz RAA vs RA")
   - Contexto de asignatura (nombre en encabezado)
   - Renderizado de matriz (estructura visual correcta)
   - Toggle de vista (estado inicial correcto)
   - Controles de gestión (botón Nueva Relación, dropdown de filtro)

5. **Prevención de errores académicos críticos:** En el contexto académico, trabajar con la asignatura incorrecta puede resultar en:
   - Relaciones RAA-RA asignadas a la materia equivocada
   - Análisis de aporte incorrecto de una asignatura
   - Documentación de acreditación errónea
   - Confusión en la trazabilidad curricular
   
   Este escenario previene estos errores al garantizar que el contexto (materia) siempre está visible.

6. **Base para toma de decisiones informadas:** El objetivo final es "definir correctamente el aporte de una asignatura". Para esto, el profesor necesita:
   - Ver qué materia está analizando (contexto)
   - Ver los RAA específicos de esa materia (filas)
   - Ver los RA de carrera disponibles (columnas)
   - Ver las relaciones existentes (checkmarks)
   - Tener herramientas para gestionar relaciones (botón Nueva Relación)
   
   Este escenario valida que todos estos elementos están presentes y visibles.

7. **Evidencia visual completa en prototipo:** La imagen muestra explícitamente este escenario completo:
   - Encabezado con "Ingeniería de Software y Requerimientos (ISWD414)"
   - Pestaña "Matriz RAA vs RA" activa (fondo azul)
   - Matriz completa visible con RAA en filas y RA en columnas
   - Toggle en posición correcta (RAA)
   - Todos los controles visibles y accesibles

8. **Patrón de usabilidad fundamental:** Mostrar el contexto (qué materia) junto con la acción (relacionar RAA-RA) es un patrón fundamental de usabilidad. Los usuarios necesitan saber "dónde están" en todo momento. Este escenario valida este principio.

9. **Punto de fallo de mayor impacto funcional:** Si este escenario falla:
   - El profesor no puede acceder a la matriz para la asignatura que necesita
   - No se muestra el nombre de la asignatura, causando confusión
   - La funcionalidad completa de la HU queda inoperativa
   - El profesor no puede cumplir su objetivo de definir el aporte de la asignatura

10. **Dependencia de escenarios subsecuentes:**
    - El Escenario 2 (ver relaciones) depende de que la matriz esté visible
    - El Escenario 3 (cambiar vista) depende de que el toggle esté disponible
    - Ambos requieren que el nombre de la asignatura esté visible para mantener contexto

**Recomendación de prueba prioritaria:**
- Validar que el nombre de la asignatura se muestra correctamente en el encabezado
- Verificar que al activar la pestaña "Matriz RAA vs RA", todos los elementos se cargan correctamente
- Confirmar que los RAA mostrados corresponden a la asignatura seleccionada
- Validar que el toggle inicia en la posición correcta (RAA)
- Probar con múltiples asignaturas para confirmar que el nombre se actualiza correctamente
- Verificar que todos los controles (Nueva Relación, Filtrar) están habilitados y visibles
- Incluir en regresión crítica para cambios en navegación o contexto de asignatura

**Sin este escenario funcionando, el profesor no puede "observar la materia al relacionar RAA con RA"** porque aunque pudiera ver una matriz, no sabría qué materia está analizando, haciendo imposible "definir correctamente el aporte de una asignatura". El contexto visual (nombre de la asignatura) es tan crítico como la matriz misma para cumplir el objetivo de esta HU.