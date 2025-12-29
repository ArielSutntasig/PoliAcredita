# **CRITERIOS DE ACEPTACIÓN - HU: Vincular RA con RAA**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imágenes 12-20 del Profesor):**

**C1:** Al menos un RAA seleccionado en Paso 1  
**C2:** Al menos un RA seleccionado en Paso 2  
**C3:** Nivel de aporte seleccionado en dropdown "Nivel de Aporte" (Paso 3)  
**C4:** Justificación escrita en textarea "Justifique la relación de RAA vs RA:" (Paso 3)

**Nota:** El wizard es secuencial, por lo que las condiciones tienen dependencias progresivas.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mantener botón "Guardar" deshabilitado (gris)  
**A2:** Habilitar botón "Guardar" (azul) en Paso 1  
**A3:** Avanzar al Paso 2 del wizard  
**A4:** Habilitar botón "Guardar" (azul) en Paso 2  
**A5:** Avanzar al Paso 3 del wizard  
**A6:** Mostrar elementos seleccionados en sección "Elementos Seleccionado:"  
**A7:** Habilitar botón "Guardar" (azul) final  
**A8:** Crear relación RAA-RA en base de datos  
**A9:** Actualizar matriz visual con nueva celda verde con checkmark (✓)  
**A10:** Mostrar tooltip azul "Información" con mensaje "Se agregó la relación correctamente"  
**A11:** Cerrar wizard y volver a vista de matriz

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** | **R9** | **R10** | **R11** | **R12** | **R13** | **R14** | **R15** | **R16** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|---------|---------|---------|---------|
| **C1: RAA seleccionado** | F | F | F | F | F | F | F | F | V | V | V | V | V | V | V | V |
| **C2: RA seleccionado** | F | F | F | F | V | V | V | V | F | F | F | F | V | V | V | V |
| **C3: Nivel aporte seleccionado** | F | F | V | V | F | F | V | V | F | F | V | V | F | F | V | V |
| **C4: Justificación escrita** | F | V | F | V | F | V | F | V | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1: Botón deshabilitado Paso 1 | X | X | X | X | X | X | X | X | - | - | - | - | - | - | - | - |
| A2: Botón habilitado Paso 1 | - | - | - | - | - | - | - | - | X | X | X | X | X | X | X | X |
| A3: Avanzar a Paso 2 | - | - | - | - | - | - | - | - | X | X | X | X | X | X | X | X |
| A4: Botón habilitado Paso 2 | - | - | - | - | - | - | - | - | - | - | - | - | X | X | X | X |
| A5: Avanzar a Paso 3 | - | - | - | - | - | - | - | - | - | - | - | - | X | X | X | X |
| A6: Mostrar elementos seleccionados | - | - | - | - | - | - | - | - | - | - | - | - | X | X | X | X |
| A7: Botón habilitado Paso 3 | - | - | - | - | - | - | - | - | - | - | - | - | - | - | X | X |
| A8-A11: Crear y confirmar relación | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | X |

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** |
|-----------|--------|--------|--------|--------|--------|--------|
| **C1: RAA seleccionado** | F | V | V | V | V | V |
| **C2: RA seleccionado** | - | F | V | V | V | V |
| **C3: Nivel aporte seleccionado** | - | - | F | V | V | V |
| **C4: Justificación escrita** | - | - | - | F | V | V |
| **ACCIONES** |
| A1: Botón "Guardar" deshabilitado (Paso 1) | X | - | - | - | - | - |
| A2: Botón "Guardar" habilitado (Paso 1) | - | X | X | X | X | X |
| A3: Avanzar a Paso 2 | - | X | X | X | X | X |
| A4: Botón "Guardar" deshabilitado (Paso 2) | - | X | - | - | - | - |
| A5: Botón "Guardar" habilitado (Paso 2) | - | - | X | X | X | X |
| A6: Avanzar a Paso 3 | - | - | X | X | X | X |
| A7: Mostrar elementos en "Elementos Seleccionado:" | - | - | X | X | X | X |
| A8: Botón "Guardar" deshabilitado (Paso 3) | - | - | X | X | - | - |
| A9: Botón "Guardar" habilitado (Paso 3) | - | - | - | - | X | X |
| A10-A14: Crear relación completa | - | - | - | - | - | X |

**Justificación de minimización:**

- **R1:** Estado inicial sin RAA seleccionado - botón deshabilitado
- **R2:** Solo RAA seleccionado - permite avanzar al Paso 2 pero botón Paso 2 deshabilitado
- **R3:** RAA y RA seleccionados - permite avanzar al Paso 3, muestra elementos
- **R4:** Paso 3 con nivel pero sin justificación - botón deshabilitado
- **R5:** Paso 3 con justificación pero sin nivel - botón deshabilitado (eliminada porque según imágenes, el nivel es requerido primero)
- **R6:** Paso 3 completo (nivel + justificación) - ejecuta creación exitosa

**Reglas eliminadas:** Las combinaciones donde C2, C3, C4 son verdaderas pero C1 es falsa son imposibles debido al flujo secuencial del wizard.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas significativas:** 6 reglas

**Criterios eliminados:**
- **Regla R5 (justificación sin nivel):** Si bien la tabla la incluye como posibilidad lógica, el análisis de las imágenes 16-17 muestra que el dropdown "Nivel de Aporte" debe ser completado. Por flujo lógico de UX, se espera que ambos campos sean requeridos. Sin embargo, para asegurar cobertura completa, mantendremos R4 y R5 como escenarios separados.

**Ajuste:** Mantendré 6 AC para cubrir todas las validaciones progresivas del wizard.

**Criterios de Aceptación finales:** **6 AC**

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Acceder al wizard sin selección de RAA**

**Dado que** estoy en la vista "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** tengo RAA creados para la asignatura **Y** soy un profesor en el sistema,  
**cuando** hago clic en el botón "+ Nueva Relación",  
**entonces** se abre el wizard con el título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** se muestra el Paso 1 activo con círculo azul y texto "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** se presentan los Pasos 2 y 3 en círculos grises e inactivos **Y** se muestra la tabla con columnas "Código", "Tipo", "Descripción" **Y** se visualiza el campo de búsqueda "Buscar por código o descripción..." **Y** se presenta la paginación "Previous, 1, 2, 3, Next" **Y** se muestra el botón "Cancelar" en rojo con icono X **Y** se muestra el botón "Guardar" deshabilitado en gris **Y** aparecen todos los RAA de la asignatura disponibles para selección.

---

### **Escenario 2 – Seleccionar RAA y avanzar al Paso 2**

**Dado que** estoy en el Paso 1 del wizard de vinculación **Y** tengo RAA visibles en la tabla,  
**cuando** selecciono al menos un RAA de la lista (ej: código "1.1", tipo "De Conocimiento"),  
**entonces** el botón "Guardar" cambia de gris deshabilitado a azul habilitado **Y** puedo hacer clic en el botón "Guardar" para avanzar **Y** se avanza automáticamente al Paso 2 **Y** el círculo del Paso 2 cambia a azul activo con texto "Seleccionar Resultados de Aprendizaje (RA)" **Y** el Paso 1 permanece completado **Y** se muestra la tabla con columnas "Código", "Descripción" **Y** se presenta el dropdown "Tipo de Aprendizaje" con opciones "Conocimientos", "Destrezas", "Valores y actitudes" **Y** se visualiza el campo de búsqueda "Buscar por código o descripción..." **Y** aparecen los RA disponibles de la carrera (RG1, RG2, RG3, RG4, RG5, etc.) **Y** el botón "Guardar" está deshabilitado en gris hasta seleccionar un RA.

---

### **Escenario 3 – Seleccionar RA y avanzar al Paso 3**

**Dado que** estoy en el Paso 2 del wizard **Y** tengo RA visibles en la tabla **Y** he seleccionado un RAA en el paso anterior,  
**cuando** selecciono al menos un RA de la lista (ej: código "RG1", descripción "Comprender los principios fundamentales de la ingeniería de software."),  
**entonces** el botón "Guardar" cambia de gris deshabilitado a azul habilitado **Y** puedo hacer clic en el botón "Guardar" para avanzar **Y** se avanza automáticamente al Paso 3 **Y** el círculo del Paso 3 cambia a azul activo con texto "Justificar Relación" **Y** se muestra la sección "Elementos Seleccionado:" con dos subsecciones **Y** se presenta la subsección "Resultados de Aprendizaje de Asignatura (RAA):" con la descripción completa del RAA seleccionado **Y** se presenta la subsección "Resultado de aprendizaje de carrera:" con la descripción completa del RA seleccionado **Y** se visualiza el dropdown "Seleccione el nivel de aporte:" con placeholder "Nivel de Aporte" **Y** se muestra el textarea "Justifique la relación de RAA vs RA:" con placeholder extenso **Y** el botón "Guardar" está deshabilitado en gris hasta completar nivel y justificación.

---

### **Escenario 4 – Intentar guardar con nivel seleccionado pero sin justificación**

**Dado que** estoy en el Paso 3 del wizard **Y** tengo RAA y RA seleccionados mostrados en "Elementos Seleccionado:" **Y** he seleccionado un nivel de aporte (ej: "Alto") en el dropdown,  
**cuando** intento guardar sin escribir texto en el textarea "Justifique la relación de RAA vs RA:",  
**entonces** el botón "Guardar" permanece deshabilitado en gris **Y** no se permite completar el proceso de vinculación **Y** debo escribir una justificación para poder continuar.

---

### **Escenario 5 – Intentar guardar con justificación escrita pero sin nivel seleccionado**

**Dado que** estoy en el Paso 3 del wizard **Y** tengo RAA y RA seleccionados mostrados en "Elementos Seleccionado:" **Y** he escrito una justificación en el textarea "Justifique la relación de RAA vs RA:",  
**cuando** intento guardar sin seleccionar un nivel de aporte en el dropdown "Seleccione el nivel de aporte:",  
**entonces** el botón "Guardar" permanece deshabilitado en gris **Y** no se permite completar el proceso de vinculación **Y** debo seleccionar un nivel de aporte (Alto, Medio o Bajo) para poder continuar.

---

### **Escenario 6 – Vincular RAA con RA exitosamente**

**Dado que** estoy en el Paso 3 del wizard **Y** tengo RAA y RA seleccionados mostrados en "Elementos Seleccionado:" **Y** he seleccionado un nivel de aporte (ej: "Alto", "Medio" o "Bajo") en el dropdown "Seleccione el nivel de aporte:" **Y** he escrito una justificación en el textarea "Justifique la relación de RAA vs RA:",  
**cuando** hago clic en el botón "Guardar" azul habilitado,  
**entonces** se crea la relación entre el RAA y el RA en el sistema **Y** se cierra el wizard automáticamente **Y** se vuelve a la vista de la matriz "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** se actualiza la matriz visual con una nueva celda verde con checkmark (✓) en la intersección correspondiente entre el RAA y RA vinculados **Y** se muestra un tooltip azul en la esquina superior derecha con icono ℹ️ **Y** el tooltip contiene el título "Información" **Y** el tooltip muestra el mensaje "Se agregó la relación correctamente" **Y** el tooltip tiene un botón X para cerrar **Y** puedo visualizar la nueva relación establecida en la matriz **Y** la vinculación queda registrada con su nivel de aporte y justificación asociada.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 6 – Vincular RAA con RA exitosamente**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumple el objetivo central de la Historia de Usuario:** La HU establece explícitamente "Quiero vincular un Resultado de Aprendizaje de Asignatura (RAA) de una asignatura a un Resultado de Aprendizaje (RA) de mi carrera". El Escenario 6 es el único que ejecuta completamente esta acción de vinculación exitosa, que es el valor principal que el usuario busca obtener.

2. **Happy path completo del flujo:** Representa el camino exitoso completo del wizard de 3 pasos, validando que toda la secuencia funciona correctamente: selección de RAA → selección de RA → justificación con nivel de aporte → creación exitosa → actualización visual → confirmación.

3. **Impacto académico directo:** La vinculación RAA-RA es fundamental para el sistema de acreditación académica. Establece la trazabilidad entre lo que se enseña en cada asignatura y las competencias globales de la carrera. Un error aquí compromete la integridad de todo el modelo de evaluación curricular.

4. **Validación de persistencia de datos:** Este escenario es el único que valida que la relación se guarda correctamente en la base de datos, se refleja visualmente en la matriz con la celda verde y checkmark, y el sistema confirma la operación con el mensaje exacto "Se agregó la relación correctamente".

5. **Completitud del valor de negocio:** Solo cuando este escenario funciona correctamente, el profesor puede "entender cómo cada asignatura contribuye a las competencias globales" (objetivo explícito en la HU), ya que la relación queda registrada, visible y documentada con su justificación y nivel de aporte.

6. **Evidencia visual en el prototipo:** Las imágenes 16-18 muestran específicamente este flujo completo exitoso, indicando que es el caso de uso principal diseñado y esperado por el sistema.

Los escenarios 1-5 son importantes para validar controles, navegación y validaciones del wizard, pero ninguno cumple con el objetivo principal de la HU. El Escenario 6 es el único que demuestra que el sistema permite efectivamente vincular RAA con RA de manera exitosa y visible, por lo que debe ser validado con máxima prioridad en las pruebas de aceptación.