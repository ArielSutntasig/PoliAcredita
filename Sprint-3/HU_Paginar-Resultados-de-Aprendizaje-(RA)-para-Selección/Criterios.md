# **CRITERIOS DE ACEPTACIÓN - HU: Paginar Resultados de Aprendizaje (RA) para Selección**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y patrón de paginación del sistema):**

**C1:** Usuario está en Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)"  
**C2:** Cantidad total de RA excede el límite por página (requiere paginación)  
**C3:** Usuario está en la primera página  
**C4:** Usuario está en una página intermedia (ni primera ni última)  
**C5:** Usuario está en la última página  
**C6:** Usuario hace clic en botón "Next"  
**C7:** Usuario hace clic en botón "Previous"  
**C8:** Usuario hace clic en número de página específico (ej: 1, 2, 3)

**Nota:** La paginación sigue el patrón estándar observado en el sistema: "Previous, 1, 2, 3, Next".

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar controles de paginación en la parte inferior de la tabla de RA  
**A2:** Mostrar botón "Previous" habilitado  
**A3:** Mostrar botón "Previous" deshabilitado (en página 1)  
**A4:** Mostrar números de página disponibles (1, 2, 3, etc.)  
**A5:** Resaltar visualmente la página actual  
**A6:** Mostrar botón "Next" habilitado  
**A7:** Mostrar botón "Next" deshabilitado (en última página)  
**A8:** Cargar y mostrar RA de la página seleccionada en la tabla  
**A9:** Actualizar tabla sin recargar el wizard completo  
**A10:** Mantener selecciones previas de RA (checkboxes marcados persisten)  
**A11:** Mantener filtros y búsqueda aplicados al cambiar de página  
**A12:** Mantener estructura del wizard y botón "Guardar"

---

### **Tabla de Decisión Completa (Maximizada)**

Por simplicidad, presento la versión reducida enfocada en las combinaciones relevantes:

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard** | F | V | V | V | V | V | V | V |
| **C2: Requiere paginación** | - | F | V | V | V | V | V | V |
| **C3: En primera página** | - | - | V | F | F | V | F | F |
| **C4: En página intermedia** | - | - | F | V | F | F | V | F |
| **C5: En última página** | - | - | F | F | V | F | F | V |
| **ACCIONES** |
| A1-A5: Mostrar controles | - | - | X | X | X | X | X | X |
| A3: "Previous" deshabilitado | - | - | X | - | - | X | - | - |
| A7: "Next" deshabilitado | - | - | - | - | X | - | - | X |

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** |
|-----------|--------|--------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard vinculación** | V | V | V | V | V | V |
| **C2: Requiere paginación (múltiples páginas)** | F | V | V | V | V | V |
| **C3: En primera página** | - | V | - | - | V | - |
| **C5: En última página** | - | - | V | - | - | V |
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

- **R1:** Sin paginación necesaria - fuera del alcance (pocos RA).
- **R2:** Visualización inicial página 1 - "Previous" deshabilitado, "Next" habilitado.
- **R3:** Visualización última página - "Previous" habilitado, "Next" deshabilitado.
- **R4:** Navegación por número de página - carga página específica.
- **R5:** Navegación con "Next" - avanza a siguiente página.
- **R6:** Navegación con "Previous" - retrocede a página anterior.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 5 reglas (excluyendo R1)

**Criterios de Aceptación finales:** **4 AC**

1. **AC1:** Visualizar controles de paginación con múltiples páginas de RA
2. **AC2:** Navegar a página específica haciendo clic en número
3. **AC3:** Navegar a página siguiente con botón "Next"
4. **AC4:** Navegar a página anterior con botón "Previous"

No se detectaron AC redundantes. Cada uno valida un aspecto crítico de la paginación.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar controles de paginación con múltiples páginas de RA**

**Dado que** soy un coordinador de carrera **Y** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** la cantidad total de RA de la carrera excede el límite de registros por página,  
**cuando** visualizo la lista de RA,  
**entonces** se muestran los controles de paginación en la parte inferior de la tabla **Y** se visualiza el botón "Previous" a la izquierda **Y** se muestran los números de página disponibles en el centro (ej: 1, 2, 3) **Y** se visualiza el botón "Next" a la derecha **Y** la página actual está resaltada visualmente de las demás **Y** si estoy en la página 1, el botón "Previous" está deshabilitado o no clickeable **Y** si estoy en la última página, el botón "Next" está deshabilitado o no clickeable **Y** si estoy en una página intermedia, ambos botones "Previous" y "Next" están habilitados **Y** se muestra solo un subconjunto de RA correspondiente a la página actual en la tabla **Y** cada RA visible mantiene su checkbox para selección **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible y funcional **Y** el dropdown "Tipo de Aprendizaje" permanece disponible **Y** puedo identificar claramente en qué página estoy y cuántas páginas hay disponibles para navegar por todos los RA de la carrera.

---

### **Escenario 2 – Navegar a página específica haciendo clic en número de página**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** los controles de paginación están visibles **Y** hay múltiples páginas disponibles (ej: páginas 1, 2, 3),  
**cuando** hago clic en un número de página específico (ej: hago clic en el número "2" o "3"),  
**entonces** la tabla se actualiza automáticamente mostrando los RA correspondientes a la página seleccionada **Y** el número de la página seleccionada se resalta visualmente indicando que es la página actual **Y** el número de la página anterior deja de estar resaltado **Y** la actualización ocurre sin recargar el wizard completo **Y** se mantienen las selecciones previas de RA (checkboxes marcados en otras páginas persisten) **Y** se mantienen activos los filtros de búsqueda y dropdown "Tipo de Aprendizaje" que haya aplicado previamente **Y** el botón "Previous" se habilita si la página seleccionada no es la primera **Y** el botón "Next" se habilita si la página seleccionada no es la última **Y** cada RA en la nueva página muestra su código, descripción completa y checkbox **Y** el botón "Guardar" del wizard mantiene su estado (habilitado si hay RA seleccionados, deshabilitado si no) **Y** navego eficientemente entre múltiples páginas de RA en el proceso de vinculación.

---

### **Escenario 3 – Navegar a página siguiente con botón "Next"**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** estoy visualizando una página que NO es la última (ej: estoy en página 1 o 2) **Y** el botón "Next" está habilitado,  
**cuando** hago clic en el botón "Next",  
**entonces** el sistema avanza automáticamente a la página siguiente (ej: de página 1 a página 2, o de página 2 a página 3) **Y** la tabla se actualiza mostrando los RA de la nueva página **Y** el número de la nueva página actual se resalta visualmente **Y** el botón "Previous" se habilita automáticamente (ya que ya no estoy en la primera página) **Y** si avanzo a la última página, el botón "Next" se deshabilita automáticamente **Y** la actualización ocurre sin recargar el wizard completo **Y** se preservan las selecciones de RA realizadas en páginas anteriores **Y** se mantienen los filtros de búsqueda y tipo aplicados **Y** puedo continuar navegando secuencialmente hacia adelante por todos los RA de la carrera **Y** puedo seleccionar RA adicionales en esta nueva página para el proceso de vinculación.

---

### **Escenario 4 – Navegar a página anterior con botón "Previous"**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** estoy visualizando una página que NO es la primera (ej: estoy en página 2 o 3) **Y** el botón "Previous" está habilitado,  
**cuando** hago clic en el botón "Previous",  
**entonces** el sistema retrocede automáticamente a la página anterior (ej: de página 3 a página 2, o de página 2 a página 1) **Y** la tabla se actualiza mostrando los RA de la página anterior **Y** el número de la nueva página actual se resalta visualmente **Y** el botón "Next" se habilita automáticamente (ya que ya no estoy en la última página) **Y** si retrocedo a la primera página, el botón "Previous" se deshabilita automáticamente **Y** la actualización ocurre sin recargar el wizard completo **Y** se preservan las selecciones de RA realizadas en otras páginas **Y** puedo ver y modificar las selecciones que hice anteriormente en esta página **Y** se mantienen los filtros de búsqueda y tipo aplicados **Y** puedo continuar navegando secuencialmente hacia atrás para revisar RA en páginas anteriores del proceso de vinculación.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Navegar a página específica haciendo clic en número de página**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero paginar los resultados de aprendizaje para navegar por un gran número de RAs en el proceso de vinculación". El Escenario 2 valida la funcionalidad principal de navegación: poder saltar directamente a una página específica, que es el método más eficiente cuando se conoce aproximadamente dónde está el RA buscado.

2. **Método de navegación más versátil y eficiente:** A diferencia de "Next" y "Previous" que solo permiten avanzar/retroceder secuencialmente de una en una, hacer clic en un número de página permite saltos directos. En carreras con muchos RA distribuidos en 4-5+ páginas, esto es significativamente más eficiente que hacer múltiples clics secuenciales.

3. **Happy path principal del sistema:** El sistema muestra explícitamente números de página clickeables (patrón "1, 2, 3"), indicando que esta es la forma principal de navegación diseñada. Los números están centralmente ubicados y visualmente destacados entre los botones direccionales.

4. **Crítico para el proceso de vinculación en carreras grandes:** En el contexto académico:
   - Carreras pueden tener 30-50+ RA definidos
   - RA suelen estar organizados por tipo o categoría
   - Coordinadores frecuentemente conocen "dónde" están los RA que buscan (ej: "los RA de habilidades están en página 2-3")
   - Navegación directa ahorra tiempo valioso en un proceso que se repite para cada asignatura

5. **Validación de persistencia de estado crítica:** Este escenario valida aspectos cruciales para la integridad del proceso de vinculación:
   - **Persistencia de selecciones:** Los checkboxes marcados en otras páginas NO se pierden al navegar
   - **Persistencia de filtros:** Búsquedas y filtros por tipo se mantienen activos
   - **Estado del botón Guardar:** Refleja correctamente si hay selecciones globales
   
   Un fallo aquí significaría pérdida de trabajo del usuario, resultando en frustración y potencial error en vinculaciones.

6. **Validación de múltiples componentes simultáneamente:** Este escenario prueba la integración correcta de:
   - Cambio de contenido de tabla
   - Actualización visual de indicador de página actual
   - Habilitación/deshabilitación de botones direccionales
   - Preservación de estado de selección multi-página
   - Mantenimiento de filtros activos
   - Actualización sin recarga completa del wizard

7. **Impacto en experiencia de usuario y eficiencia:** Los coordinadores usarán paginación constantemente durante:
   - Revisión de múltiples asignaturas (cada una requiere navegar RA)
   - Búsqueda de RA específicos en páginas conocidas
   - Verificación de selecciones realizadas
   - Corrección de vinculaciones
   
   La navegación directa por número es el método más usado en la práctica.

8. **Prevención de errores críticos de vinculación:** Si la paginación no preserva selecciones correctamente:
   - El coordinador pierde checkboxes marcados al cambiar de página
   - Puede vincular RAA con RA incorrectos sin darse cuenta
   - La matriz RAA vs RA resultante es incorrecta
   - La documentación de acreditación queda comprometida
   - Se requiere re-trabajo extenso para corregir

Los escenarios 1, 3 y 4 son importantes para validar la visualización inicial y navegación secuencial, pero el Escenario 2 es el que demuestra la funcionalidad de paginación más potente y crítica. Un fallo en la navegación por número de página o en la persistencia de selecciones comprometería severamente la usabilidad y confiabilidad del proceso de vinculación, potencialmente causando pérdida de trabajo y errores en la documentación curricular.

Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación, con especial énfasis en la persistencia de selecciones de checkboxes a través de múltiples cambios de página.