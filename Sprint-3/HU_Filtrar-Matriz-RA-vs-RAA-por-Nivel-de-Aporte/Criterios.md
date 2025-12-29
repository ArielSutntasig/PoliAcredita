# **CRITERIOS DE ACEPTACIÓN - HU: Filtrar Matriz RA vs RAA por Nivel de Aporte**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imágenes 6, 7 del Coordinador):**

**C1:** Filtro "Alto" seleccionado en dropdown "Filtrar por Nivel de Aporte"  
**C2:** Filtro "Medio" seleccionado en dropdown "Filtrar por Nivel de Aporte"  
**C3:** Filtro "Bajo" seleccionado en dropdown "Filtrar por Nivel de Aporte"

**Nota:** Estas condiciones son mutuamente excluyentes. El estado inicial es ningún filtro seleccionado (C1=F, C2=F, C3=F).

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar todas las relaciones RAA-RA en la matriz (sin filtrado)  
**A2:** Mostrar únicamente relaciones con nivel de aporte "Alto" (celdas verdes con checkmarks correspondientes)  
**A3:** Mostrar únicamente relaciones con nivel de aporte "Medio" (celdas verdes con checkmarks correspondientes)  
**A4:** Mostrar únicamente relaciones con nivel de aporte "Bajo" (celdas verdes con checkmarks correspondientes)  
**A5:** Ocultar todas las relaciones que no corresponden al nivel seleccionado  
**A6:** Mantener dropdown "Filtrar por Nivel de Aporte" visible y funcional  
**A7:** Mantener estructura de matriz (filas RAA y columnas RA) sin cambios

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Alto seleccionado** | F | F | F | F | V | V | V | V |
| **C2: Medio seleccionado** | F | F | V | V | F | F | V | V |
| **C3: Bajo seleccionado** | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1: Mostrar todas | X | - | - | - | - | - | - | - |
| A2: Mostrar solo Alto | - | - | - | - | X | - | - | - |
| A3: Mostrar solo Medio | - | - | X | - | - | - | - | - |
| A4: Mostrar solo Bajo | - | X | - | - | - | - | - | - |
| A5: Ocultar no coincidentes | - | X | X | X | X | X | X | X |
| A6: Mantener dropdown | X | X | X | X | X | X | X | X |
| A7: Mantener estructura | X | X | X | X | X | X | X | X |

**Análisis de reglas:** Las reglas R4, R5, R6, R7, R8 representan combinaciones imposibles (selección múltiple simultánea), ya que el dropdown solo permite una opción a la vez.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** |
|-----------|--------|--------|--------|--------|
| **C1: Alto seleccionado** | F | V | F | F |
| **C2: Medio seleccionado** | F | F | V | F |
| **C3: Bajo seleccionado** | F | F | F | V |
| **ACCIONES** |
| A1: Mostrar todas las relaciones RAA-RA | X | - | - | - |
| A2: Mostrar solo relaciones nivel "Alto" | - | X | - | - |
| A3: Mostrar solo relaciones nivel "Medio" | - | - | X | - |
| A4: Mostrar solo relaciones nivel "Bajo" | - | - | - | X |
| A5: Ocultar relaciones no coincidentes | - | X | X | X |
| A6: Mantener dropdown visible y funcional | X | X | X | X |
| A7: Mantener estructura de matriz intacta | X | X | X | X |

**Justificación de minimización:**
- **Eliminadas R4-R8:** Representan combinaciones imposibles donde múltiples opciones están seleccionadas simultáneamente. El comportamiento del dropdown (selección única) hace estas reglas inválidas.
- **R1:** Estado inicial o sin filtro aplicado (ninguna opción seleccionada).
- **R2-R4:** Estados válidos con un filtro específico aplicado.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 4 reglas

**Criterios de Aceptación finales:** **4 AC**

**Justificación:** Cada regla de la tabla minimizada representa un escenario único de interacción con el filtro:
1. Visualización sin filtro (estado inicial)
2. Filtrado por nivel "Alto"
3. Filtrado por nivel "Medio"
4. Filtrado por nivel "Bajo"

No se detectaron AC redundantes, ya que cada uno valida un comportamiento distinto del sistema.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar matriz sin filtro aplicado**

**Dado que** estoy en la vista "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** he seleccionado una materia (aplica para rol Coordinador) o estoy en contexto de una asignatura (aplica para rol Profesor),  
**cuando** accedo a la matriz sin aplicar ningún filtro en el dropdown "Filtrar por Nivel de Aporte",  
**entonces** se muestran todas las relaciones RAA-RA existentes en la matriz **Y** las celdas verdes con checkmarks (✓) indican todas las conexiones establecidas independientemente de su nivel de aporte **Y** se visualiza el dropdown "Filtrar por Nivel de Aporte" con su valor por defecto **Y** se mantienen visibles todas las filas (códigos RAA: 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1) **Y** se mantienen visibles todas las columnas (códigos RA: RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6) **Y** se presenta la vista panorámica completa de todas las relaciones sin restricciones.

---

### **Escenario 2 – Filtrar matriz por nivel de aporte "Alto"**

**Dado que** estoy en la matriz RAA vs RA con relaciones visibles **Y** tengo acceso al dropdown "Filtrar por Nivel de Aporte",  
**cuando** hago clic en el dropdown "Filtrar por Nivel de Aporte" **Y** selecciono la opción "Alto",  
**entonces** la matriz se actualiza automáticamente mostrando únicamente las relaciones con nivel de aporte "Alto" **Y** se muestran solo las celdas verdes con checkmarks (✓) correspondientes a nivel "Alto" **Y** se ocultan todas las celdas de relaciones con nivel "Medio" y "Bajo" **Y** se mantiene la estructura completa de la matriz con todas las filas RAA y columnas RA visibles **Y** el dropdown muestra "Alto" como opción seleccionada **Y** obtengo una vista enfocada en las materias que mayor valor aportan a los RA.

---

### **Escenario 3 – Filtrar matriz por nivel de aporte "Medio"**

**Dado que** estoy en la matriz RAA vs RA con relaciones visibles **Y** tengo acceso al dropdown "Filtrar por Nivel de Aporte",  
**cuando** hago clic en el dropdown "Filtrar por Nivel de Aporte" **Y** selecciono la opción "Medio",  
**entonces** la matriz se actualiza automáticamente mostrando únicamente las relaciones con nivel de aporte "Medio" **Y** se muestran solo las celdas verdes con checkmarks (✓) correspondientes a nivel "Medio" **Y** se ocultan todas las celdas de relaciones con nivel "Alto" y "Bajo" **Y** se mantiene la estructura completa de la matriz con todas las filas RAA y columnas RA visibles **Y** el dropdown muestra "Medio" como opción seleccionada **Y** obtengo una vista enfocada en las materias con aporte moderado a los RA.

---

### **Escenario 4 – Filtrar matriz por nivel de aporte "Bajo"**

**Dado que** estoy en la matriz RAA vs RA con relaciones visibles **Y** tengo acceso al dropdown "Filtrar por Nivel de Aporte",  
**cuando** hago clic en el dropdown "Filtrar por Nivel de Aporte" **Y** selecciono la opción "Bajo",  
**entonces** la matriz se actualiza automáticamente mostrando únicamente las relaciones con nivel de aporte "Bajo" **Y** se muestran solo las celdas verdes con checkmarks (✓) correspondientes a nivel "Bajo" **Y** se ocultan todas las celdas de relaciones con nivel "Alto" y "Medio" **Y** se mantiene la estructura completa de la matriz con todas las filas RAA y columnas RA visibles **Y** el dropdown muestra "Bajo" como opción seleccionado **Y** obtengo una vista enfocada en las materias con menor aporte relativo a los RA.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Filtrar matriz por nivel de aporte "Alto"**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Alineación directa con el valor de negocio:** La Historia de Usuario especifica explícitamente "para conocer las materias que más valor aportan a los RA". El filtro "Alto" es la implementación directa de este objetivo central, permitiendo a coordinadores y profesores identificar inmediatamente las asignaturas con mayor impacto académico.

2. **Caso de uso primario:** El escenario de filtrado por nivel "Alto" representa el "happy path" principal de la funcionalidad, ya que los usuarios (especialmente coordinadores) necesitan priorizar las relaciones más significativas para toma de decisiones académicas, evaluaciones de acreditación y optimización curricular.

3. **Mayor impacto en decisiones estratégicas:** Las relaciones de nivel "Alto" son las que determinan el cumplimiento efectivo de los resultados de aprendizaje de la carrera. Un error en este filtrado podría llevar a decisiones incorrectas sobre la estructura curricular o evaluaciones de acreditación (EUR-ACE).

4. **Evidencia en el prototipo:** Las imágenes del Coordinador (específicamente la imagen 7) muestran el dropdown desplegado con las tres opciones, destacando que esta funcionalidad es esencial y prioritaria en el diseño de la interfaz.

5. **Frecuencia de uso esperada:** Según el contexto de acreditación académica, es altamente probable que el filtro "Alto" sea el más utilizado, ya que las auditorías y evaluaciones se enfocan primero en verificar las relaciones de mayor impacto antes de analizar los niveles secundarios.

Por estas razones, el correcto funcionamiento del filtro "Alto" es crítico para el éxito de la funcionalidad completa y debe ser validado con máxima prioridad en las pruebas de aceptación.