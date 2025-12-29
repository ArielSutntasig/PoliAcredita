# **CRITERIOS DE ACEPTACIÓN - HU: Visualizar Matriz de Relación RAA vs RA**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imagen 12 del Profesor):**

**C1:** Usuario accede al tab "Matriz RAA vs RA" desde la asignatura  
**C2:** Existen RAA definidos para la asignatura  
**C3:** Existen relaciones RAA-RA previamente establecidas

**Nota:** La HU se enfoca en la visualización/observación de la matriz, no en su creación o edición.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)"  
**A2:** Mostrar toggle buttons con "Resultados de Aprendizaje de Asignatura" activo (azul con checkbox) y "Resultados de Aprendizaje Carrera" inactivo (gris)  
**A3:** Mostrar dropdown "Filtrar por Nivel de Aporte"  
**A4:** Mostrar botón "+ Nueva Relación" en esquina superior derecha  
**A5:** Mostrar estructura completa de matriz con filas RAA (códigos: 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1) con iconos informativos ℹ️  
**A6:** Mostrar columnas RA (códigos: RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6) con iconos informativos ℹ️  
**A7:** Mostrar celdas verdes con checkmarks (✓) en intersecciones donde existen relaciones RAA-RA  
**A8:** Mostrar celdas vacías (sin color) en intersecciones donde no existen relaciones  
**A9:** Permitir identificar visualmente qué RAA aportan a qué RA

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Usuario accede al tab** | F | F | F | F | V | V | V | V |
| **C2: Existen RAA** | F | F | V | V | F | F | V | V |
| **C3: Existen relaciones RAA-RA** | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1: Mostrar título | - | - | - | - | - | - | X | X |
| A2-A6: Mostrar estructura completa | - | - | - | - | - | - | X | X |
| A7: Mostrar celdas verdes con relaciones | - | - | - | - | - | - | - | X |
| A8: Mostrar celdas vacías | - | - | - | - | - | - | X | X |

**Análisis:** Las reglas R1-R6 son inválidas porque representan estados donde el usuario no accede al tab (fuera de alcance de la HU) o no hay RAA (precondición no cumplida, ya que para llegar al tab "Matriz RAA vs RA" el profesor debe estar en contexto de una asignatura con RAA creados).

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** |
|-----------|--------|--------|
| **C1: Usuario accede al tab "Matriz RAA vs RA"** | V | V |
| **C2: Existen RAA definidos** | V | V |
| **C3: Existen relaciones RAA-RA establecidas** | F | V |
| **ACCIONES** |
| A1: Mostrar título de matriz | X | X |
| A2: Mostrar toggle buttons (RAA activo, RA inactivo) | X | X |
| A3: Mostrar dropdown "Filtrar por Nivel de Aporte" | X | X |
| A4: Mostrar botón "+ Nueva Relación" | X | X |
| A5: Mostrar filas RAA con códigos e iconos ℹ️ | X | X |
| A6: Mostrar columnas RA con códigos e iconos ℹ️ | X | X |
| A7: Mostrar estructura completa de matriz | X | X |
| A8: Mostrar celdas verdes con checkmarks (✓) | - | X |
| A9: Mostrar celdas vacías en todas las intersecciones | X | - |
| A10: Permitir identificar contribución de RAA a RA | - | X |

**Justificación de minimización:**

- **Eliminadas R1-R6:** Representan estados donde el usuario no ha accedido al tab o no hay RAA, lo cual está fuera del alcance de esta HU de visualización. El profesor solo puede acceder a este tab si ya está en contexto de una asignatura con RAA creados.
- **R1 (minimizada):** Usuario accede al tab, hay RAA pero no hay relaciones establecidas - muestra matriz con estructura completa pero todas las celdas vacías.
- **R2 (minimizada):** Usuario accede al tab, hay RAA y hay relaciones establecidas - muestra matriz completa con celdas verdes indicando relaciones (happy path principal).

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 2 reglas

**Análisis adicional:** La HU "observar la matriz" implica también poder interpretar visualmente los elementos de la matriz. Por tanto, agregaré un AC adicional para validar la capacidad de identificar y comprender los elementos visuales de la matriz.

**Criterios de Aceptación finales:** **3 AC**

**Justificación:**
1. **AC1:** Visualizar estructura completa de la matriz (elementos de UI, controles, filas, columnas)
2. **AC2:** Visualizar relaciones existentes RAA-RA (celdas verdes con checkmarks - happy path)
3. **AC3:** Identificar ausencia de relaciones RAA-RA (celdas vacías)

No se detectaron AC redundantes. Cada uno valida un aspecto distinto de la capacidad de "observar" y "entender cómo aporta a los RA".

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar estructura completa de la matriz RAA vs RA**

**Dado que** soy un profesor **Y** estoy en la vista "Crear/Editar Asignatura (PEA)" de una asignatura **Y** la asignatura tiene RAA definidos,  
**cuando** hago clic en el tab "Matriz RAA vs RA",  
**entonces** se muestra el título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** se visualizan los toggle buttons con "Resultados de Aprendizaje de Asignatura" activo en azul con checkbox marcado **Y** se visualiza "Resultados de Aprendizaje Carrera" inactivo en gris sin checkbox **Y** se muestra el dropdown "Filtrar por Nivel de Aporte" visible y funcional **Y** se presenta el botón "+ Nueva Relación" en azul en la esquina superior derecha **Y** se muestra la estructura completa de la matriz con filas correspondientes a los códigos RAA (1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1) en fondo azul **Y** cada fila RAA incluye un icono informativo ℹ️ **Y** se muestran las columnas correspondientes a los códigos RA (RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6) en fondo gris **Y** cada columna RA incluye un icono informativo ℹ️ **Y** se presenta una cuadrícula completa con todas las intersecciones entre RAA y RA visibles **Y** puedo visualizar toda la estructura para entender las posibles relaciones de aporte.

---

### **Escenario 2 – Visualizar relaciones RAA-RA existentes en la matriz**

**Dado que** estoy en la vista de matriz RAA vs RA **Y** existen relaciones previamente establecidas entre RAA y RA,  
**cuando** observo la matriz completa,  
**entonces** se muestran celdas verdes con checkmarks (✓) en las intersecciones donde existe una relación entre un RAA específico y un RA específico **Y** cada celda verde indica visualmente que ese RAA aporta al RA correspondiente **Y** puedo identificar claramente qué RAA (por ejemplo: 1.1, 1.3, 2.2) están vinculados a qué RA (por ejemplo: RE1, RG2, RE4) **Y** puedo visualizar la distribución de aportes a través de la matriz **Y** puedo entender cómo cada RAA de la asignatura contribuye a los resultados de aprendizaje de la carrera **Y** obtengo una vista panorámica de todas las relaciones establecidas para comprender el aporte global de la asignatura a las competencias de la carrera.

---

### **Escenario 3 – Identificar ausencia de relaciones RAA-RA en la matriz**

**Dado que** estoy visualizando la matriz RAA vs RA **Y** tengo RAA definidos para la asignatura,  
**cuando** observo las intersecciones de la matriz,  
**entonces** las celdas vacías (sin color de fondo verde ni checkmark) indican claramente que no existe relación entre ese RAA y ese RA específico **Y** puedo identificar visualmente qué RAA no aportan a determinados RA **Y** puedo detectar qué RA no reciben aporte de ningún RAA de esta asignatura **Y** puedo identificar oportunidades para establecer nuevas relaciones mediante el botón "+ Nueva Relación" **Y** obtengo información clara sobre las ausencias de vinculación entre los resultados de aprendizaje de la asignatura y los resultados de aprendizaje de la carrera.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Visualizar relaciones RAA-RA existentes en la matriz**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumple directamente el objetivo de la Historia de Usuario:** La HU establece "quiero observar la matriz de relación de RAA vs RA de una asignatura para entender cómo aporta a los RA". El Escenario 2 es el único que valida la capacidad de visualizar y comprender las relaciones de aporte existentes, que es el valor principal que el profesor busca obtener.

2. **Representa el happy path con datos reales:** La imagen 12 del prototipo muestra específicamente este escenario con múltiples relaciones establecidas (celdas verdes con checkmarks), indicando que es el caso de uso principal y más frecuente. Un profesor accede a esta matriz principalmente cuando hay relaciones que necesita revisar, analizar o validar.

3. **Impacto en comprensión académica:** La capacidad de "entender cómo aporta a los RA" solo es posible cuando existen relaciones visibles. Sin esta visualización correcta, el profesor no puede:
   - Evaluar si la asignatura está alineada con los objetivos de la carrera
   - Identificar si hay suficiente cobertura de RA
   - Tomar decisiones sobre ajustes curriculares
   - Documentar el aporte de la asignatura para procesos de acreditación

4. **Validación de la integración completa:** Este escenario valida que todo el sistema funciona correctamente: los RAA están creados, las relaciones están guardadas en base de datos, y la visualización refleja correctamente el estado persistido. Un error aquí compromete la confiabilidad de todo el módulo de trazabilidad académica.

5. **Valor para acreditación EUR-ACE:** En el contexto del sistema Poliacredita, la matriz RAA vs RA es fundamental para demostrar cómo cada asignatura contribuye a los criterios de acreditación. La correcta visualización de estas relaciones es crítica para auditorías y evaluaciones académicas.

6. **Base para otras funcionalidades:** Este escenario es prerequisito para funcionalidades relacionadas como el filtrado por nivel de aporte y la edición de relaciones. Si no se visualiza correctamente la matriz con relaciones, las demás funcionalidades pierden su valor.

Los escenarios 1 y 3 son importantes para validar la estructura y detectar ausencias, pero el Escenario 2 es el único que demuestra que el sistema cumple con el propósito principal: permitir al profesor observar y entender cómo su asignatura aporta a los resultados de aprendizaje de la carrera. Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación.