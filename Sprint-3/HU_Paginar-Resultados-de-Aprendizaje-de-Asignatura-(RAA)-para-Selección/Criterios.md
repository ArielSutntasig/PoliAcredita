# **CRITERIOS DE ACEPTACIÓN - HU: Paginar Resultados de Aprendizaje de Asignatura (RAA) para Selección**

---

## **CONFIRMACIÓN: RAA (NO RA)**

Esta HU se refiere específicamente a:
- ✅ **RAA (Resultados de Aprendizaje de ASIGNATURA)** - Competencias de una asignatura específica
- ❌ NO son RA (Resultados de Aprendizaje de CARRERA) - Competencias globales
- 📍 **Contexto:** Paso 1 del wizard de vinculación (Coordinador selecciona RAA de una asignatura)
- 🎯 **Códigos de RAA:** 1.1, 1.2, 1.3, 2.1, 2.2, 3.1 (de la ASIGNATURA)

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y Paso 1 del wizard):**

**C1:** Usuario (Coordinador) está en Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)"  
**C2:** Ha seleccionado una asignatura específica previamente  
**C3:** Cantidad total de RAA de la asignatura excede el límite por página (requiere paginación)  
**C4:** Usuario está en la primera página  
**C5:** Usuario está en una página intermedia (ni primera ni última)  
**C6:** Usuario está en la última página  
**C7:** Usuario hace clic en botón "Next"  
**C8:** Usuario hace clic en botón "Previous"  
**C9:** Usuario hace clic en número de página específico (ej: 1, 2, 3)

**Nota:** La paginación sigue el patrón estándar observado: "Previous, 1, 2, 3, Next".

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar controles de paginación en la parte inferior de la tabla de RAA  
**A2:** Mostrar botón "Previous" habilitado  
**A3:** Mostrar botón "Previous" deshabilitado (en página 1)  
**A4:** Mostrar números de página disponibles (1, 2, 3, etc.)  
**A5:** Resaltar visualmente la página actual  
**A6:** Mostrar botón "Next" habilitado  
**A7:** Mostrar botón "Next" deshabilitado (en última página)  
**A8:** Cargar y mostrar RAA de la página seleccionada en la tabla  
**A9:** Actualizar tabla sin recargar el wizard completo  
**A10:** Mantener selecciones previas de RAA (checkboxes marcados persisten)  
**A11:** Mantener filtros y búsqueda aplicados al cambiar de página  
**A12:** Mantener estructura del wizard y botón "Guardar"

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** |
|-----------|--------|--------|--------|--------|--------|--------|
| **C1: En Paso 1 wizard vinculación** | V | V | V | V | V | V |
| **C2: Asignatura seleccionada** | V | V | V | V | V | V |
| **C3: Requiere paginación (múltiples páginas)** | F | V | V | V | V | V |
| **C4: En primera página** | - | V | - | - | V | - |
| **C6: En última página** | - | - | V | - | - | V |
| **Acción de navegación** | - | Inicial | Inicial | Número | Next | Previous |
| **ACCIONES** |
| A1: Mostrar controles de paginación | - | X | X | X | X | X |
| A2: Botón "Previous" habilitado | - | - | X | X | X | X |
| A3: Botón "Previous" deshabilitado | - | X | - | - | X | - |
| A4-A5: Números y resaltar actual | - | X | X | X | X | X |
| A6: Botón "Next" habilitado | - | X | X | X | X | - |
| A7: Botón "Next" deshabilitado | - | - | X | - | - | X |
| A8-A12: Cargar página y mantener contexto | - | X | X | X | X | X |

**Justificación de minimización:**

- **R1:** Sin paginación necesaria - pocos RAA en la asignatura.
- **R2:** Visualización inicial página 1 - "Previous" deshabilitado, "Next" habilitado.
- **R3:** Visualización última página - "Previous" habilitado, "Next" deshabilitado.
- **R4:** Navegación por número de página - carga página específica.
- **R5:** Navegación con "Next" - avanza a siguiente página.
- **R6:** Navegación con "Previous" - retrocede a página anterior.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 5 reglas (excluyendo R1)

**Criterios de Aceptación finales:** **4 AC**

1. **AC1:** Visualizar controles de paginación con múltiples páginas de RAA
2. **AC2:** Navegar a página específica haciendo clic en número
3. **AC3:** Navegar a página siguiente con botón "Next"
4. **AC4:** Navegar a página anterior con botón "Previous"

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar controles de paginación con múltiples páginas de RAA**

**Dado que** soy un coordinador de carrera **Y** he seleccionado una asignatura específica para vincular **Y** estoy en el Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** la cantidad total de RAA de la asignatura seleccionada excede el límite de registros por página,  
**cuando** visualizo la lista de RAA de la asignatura,  
**entonces** se muestran los controles de paginación en la parte inferior de la tabla **Y** se visualiza el botón "Previous" a la izquierda **Y** se muestran los números de página disponibles en el centro (ej: 1, 2, 3) **Y** se visualiza el botón "Next" a la derecha **Y** la página actual está resaltada visualmente de las demás **Y** si estoy en la página 1, el botón "Previous" está deshabilitado o no clickeable **Y** si estoy en la última página, el botón "Next" está deshabilitado o no clickeable **Y** si estoy en una página intermedia, ambos botones "Previous" y "Next" están habilitados **Y** se muestra solo un subconjunto de **RAA de la asignatura** correspondiente a la página actual en la tabla **Y** cada RAA visible muestra su código (ej: 1.1, 1.2, 2.1), tipo (Conocimiento, Destrezas, Valores) y descripción **Y** cada RAA visible mantiene su checkbox para selección **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible y funcional **Y** puedo identificar claramente en qué página estoy y cuántas páginas hay disponibles para navegar por todos los RAA de la asignatura seleccionada.

---

### **Escenario 2 – Navegar a página específica haciendo clic en número de página**

**Dado que** estoy en el Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** visualizo RAA de la asignatura seleccionada **Y** los controles de paginación están visibles **Y** hay múltiples páginas disponibles (ej: páginas 1, 2, 3),  
**cuando** hago clic en un número de página específico (ej: hago clic en el número "2" o "3"),  
**entonces** la tabla se actualiza automáticamente mostrando los **RAA de la asignatura** correspondientes a la página seleccionada **Y** el número de la página seleccionada se resalta visualmente indicando que es la página actual **Y** el número de la página anterior deja de estar resaltado **Y** la actualización ocurre sin recargar el wizard completo **Y** se mantienen las selecciones previas de RAA (checkboxes marcados en otras páginas persisten) **Y** se mantienen activos los filtros de búsqueda que haya aplicado previamente **Y** el botón "Previous" se habilita si la página seleccionada no es la primera **Y** el botón "Next" se habilita si la página seleccionada no es la última **Y** cada RAA en la nueva página muestra su código (1.1, 2.2, etc.), tipo y descripción completa y checkbox **Y** el botón "Guardar" del wizard mantiene su estado (habilitado si hay RAA seleccionados, deshabilitado si no) **Y** navego eficientemente entre múltiples páginas de RAA de la asignatura en el proceso de vinculación.

---

### **Escenario 3 – Navegar a página siguiente con botón "Next"**

**Dado que** estoy en el Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** estoy visualizando una página que NO es la última (ej: estoy en página 1 o 2) **Y** el botón "Next" está habilitado,  
**cuando** hago clic en el botón "Next",  
**entonces** el sistema avanza automáticamente a la página siguiente (ej: de página 1 a página 2, o de página 2 a página 3) **Y** la tabla se actualiza mostrando los **RAA de la asignatura** de la nueva página **Y** el número de la nueva página actual se resalta visualmente **Y** el botón "Previous" se habilita automáticamente (ya que ya no estoy en la primera página) **Y** si avanzo a la última página, el botón "Next" se deshabilita automáticamente **Y** la actualización ocurre sin recargar el wizard completo **Y** se preservan las selecciones de RAA realizadas en páginas anteriores **Y** se mantienen los filtros de búsqueda aplicados **Y** puedo continuar navegando secuencialmente hacia adelante por todos los RAA de la asignatura **Y** puedo seleccionar RAA adicionales en esta nueva página para el proceso de vinculación con RA de carrera.

---

### **Escenario 4 – Navegar a página anterior con botón "Previous"**

**Dado que** estoy en el Paso 1 del wizard "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** estoy visualizando una página que NO es la primera (ej: estoy en página 2 o 3) **Y** el botón "Previous" está habilitado,  
**cuando** hago clic en el botón "Previous",  
**entonces** el sistema retrocede automáticamente a la página anterior (ej: de página 3 a página 2, o de página 2 a página 1) **Y** la tabla se actualiza mostrando los **RAA de la asignatura** de la página anterior **Y** el número de la nueva página actual se resalta visualmente **Y** el botón "Next" se habilita automáticamente (ya que ya no estoy en la última página) **Y** si retrocedo a la primera página, el botón "Previous" se deshabilita automáticamente **Y** la actualización ocurre sin recargar el wizard completo **Y** se preservan las selecciones de RAA realizadas en otras páginas **Y** puedo ver y modificar las selecciones que hice anteriormente en esta página **Y** se mantienen los filtros de búsqueda aplicados **Y** puedo continuar navegando secuencialmente hacia atrás para revisar RAA de la asignatura en páginas anteriores del proceso de vinculación.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Navegar a página específica haciendo clic en número de página**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero paginar los resultados de aprendizaje de la asignatura para navegar por un gran número de RAAs en el proceso de vinculación". El Escenario 2 valida la funcionalidad principal de navegación: poder saltar directamente a una página específica de RAA.

2. **Crítico para asignaturas con muchos RAA:** Algunas asignaturas pueden tener 15-25+ RAA distribuidos en múltiples páginas. La navegación directa por número es significativamente más eficiente que navegar secuencialmente con Next/Previous cuando el Coordinador busca RAA específicos.

3. **Validación de persistencia de selecciones crítica:** Este escenario valida el aspecto MÁS CRÍTICO de la paginación para el proceso de vinculación:
   - **Persistencia de checkboxes:** Los RAA seleccionados en página 1 NO se pierden al navegar a página 2
   - **Integridad de selección multi-página:** El Coordinador puede seleccionar RAA de múltiples páginas y todos persisten
   - **Estado del botón Guardar:** Refleja correctamente la selección global de todas las páginas
   
   Un fallo aquí significaría pérdida catastrófica de trabajo del Coordinador.

4. **Contexto específico del Coordinador:** A diferencia del Profesor que trabaja con sus propios RAA, el Coordinador:
   - Revisa asignaturas de otros profesores que pueden tener muchos RAA
   - No conoce la estructura interna de cada asignatura
   - Necesita navegar eficientemente por listas desconocidas
   - Puede necesitar seleccionar RAA dispersos en múltiples páginas

5. **Impacto en proceso de vinculación completo:** El Coordinador usa esta funcionalidad para:
   - Revisar TODOS los RAA de una asignatura antes de seleccionar
   - Seleccionar múltiples RAA relevantes para vincular con RA de carrera
   - Comparar RAA entre páginas para decisiones informadas
   - Asegurar que no omite RAA relevantes en páginas no visitadas

6. **Prevención de errores críticos de vinculación:** Si la paginación no funciona correctamente:
   - El Coordinador pierde selecciones al cambiar de página
   - Puede crear vinculaciones incompletas sin darse cuenta
   - La trazabilidad RAA → RA queda incompleta
   - La documentación de acreditación es deficiente
   - Se requiere re-trabajo extenso para corregir

7. **Método de navegación más usado en la práctica:** Cuando hay 3-4 páginas de RAA:
   - Navegación directa (clic en número) es más rápida
   - Permite saltos hacia adelante y atrás fácilmente
   - Facilita revisión no secuencial de RAA
   - Mejora significativamente la experiencia del usuario

8. **Validación de múltiples componentes simultáneamente:** Este escenario prueba:
   - Cambio correcto de contenido de tabla
   - Actualización visual de indicador de página
   - Habilitación/deshabilitación de botones direccionales
   - **Persistencia de estado multi-página (CRÍTICO)**
   - Mantenimiento de filtros
   - Actualización sin recarga del wizard

Los escenarios 1, 3 y 4 son importantes para la visualización inicial y navegación secuencial, pero el Escenario 2 es el que demuestra la funcionalidad de paginación más potente y crítica para el Coordinador. Un fallo en la navegación por número de página o en la persistencia de selecciones comprometería severamente la capacidad del Coordinador de revisar y seleccionar RAA de asignaturas con muchos resultados de aprendizaje.

Por tanto, debe ser validado con máxima prioridad, con especial énfasis en la **persistencia de selecciones de checkboxes a través de múltiples cambios de página**, ya que este es el requisito más crítico para la integridad del proceso de vinculación RAA vs RA.