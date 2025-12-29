# **CRITERIOS DE ACEPTACIÓN - HU: Paginar Asignaturas (PEA)**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imagen 4 del Profesor):**

**C1:** Cantidad total de asignaturas excede el límite por página (requiere paginación)  
**C2:** Usuario está en la primera página  
**C3:** Usuario está en una página intermedia (ni primera ni última)  
**C4:** Usuario está en la última página  
**C5:** Usuario hace clic en botón "Next"  
**C6:** Usuario hace clic en botón "Previous"  
**C7:** Usuario hace clic en número de página específico (ej: 1, 2, 3)

**Nota:** La imagen 4 muestra paginación "Previous, 1, 2, 3, Next" indicando sistema de paginación con navegación por números y botones direccionales.

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar controles de paginación en la parte inferior de la tabla  
**A2:** Mostrar botón "Previous" habilitado  
**A3:** Mostrar botón "Previous" deshabilitado (en página 1)  
**A4:** Mostrar números de página disponibles (1, 2, 3, etc.)  
**A5:** Resaltar visualmente la página actual  
**A6:** Mostrar botón "Next" habilitado  
**A7:** Mostrar botón "Next" deshabilitado (en última página)  
**A8:** Cargar y mostrar asignaturas de la página seleccionada en la tabla  
**A9:** Actualizar tabla sin recargar la página completa  
**A10:** Mantener filtros de búsqueda aplicados al cambiar de página  
**A11:** Mantener estructura completa de UI (búsqueda, filtros, botón Nueva Asignatura)

---

### **Tabla de Decisión Completa (Maximizada)**

Por simplicidad, presento directamente la versión que incluye las combinaciones más relevantes:

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Requiere paginación** | F | V | V | V | V | V | V | V |
| **C2: En primera página** | - | V | F | F | V | V | F | F |
| **C3: En página intermedia** | - | F | V | F | F | F | V | F |
| **C4: En última página** | - | F | F | V | F | F | F | V |
| **C5: Clic en "Next"** | - | F | F | F | V | F | V | F |
| **C6: Clic en "Previous"** | - | F | F | F | F | V | F | V |
| **C7: Clic en número página** | - | F | V | F | F | F | F | F |
| **ACCIONES** |
| A1: Mostrar controles paginación | - | X | X | X | X | X | X | X |
| A3: "Previous" deshabilitado | - | X | - | - | X | - | - | - |
| A2: "Previous" habilitado | - | - | X | X | - | X | X | X |
| A7: "Next" deshabilitado | - | - | - | X | - | - | - | X |
| A6: "Next" habilitado | - | X | X | - | X | X | X | - |
| A4-A5: Mostrar números/destacar actual | - | X | X | X | X | X | X | X |
| A8-A11: Cambiar página y actualizar | - | - | X | - | X | X | X | X |

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** |
|-----------|--------|--------|--------|--------|--------|--------|
| **C1: Requiere paginación** | F | V | V | V | V | V |
| **C2: En primera página** | - | V | - | - | V | - |
| **C4: En última página** | - | - | V | - | - | V |
| **Acción de navegación** | - | Inicial | Inicial | Número | Next | Previous |
| **ACCIONES** |
| A1: Mostrar controles de paginación | - | X | X | X | X | X |
| A2: Botón "Previous" habilitado | - | - | X | X | X | X |
| A3: Botón "Previous" deshabilitado | - | X | - | - | X | - |
| A4: Mostrar números de página (1, 2, 3) | - | X | X | X | X | X |
| A5: Resaltar página actual | - | X | X | X | X | X |
| A6: Botón "Next" habilitado | - | X | X | X | X | - |
| A7: Botón "Next" deshabilitado | - | - | X | - | - | X |
| A8-A11: Cargar página y mantener contexto | - | X | X | X | X | X |

**Justificación de minimización:**

- **R1:** Sin paginación necesaria - fuera del alcance de esta HU (muy pocas asignaturas).
- **R2:** Visualización inicial en página 1 - muestra controles, "Previous" deshabilitado, "Next" habilitado.
- **R3:** Visualización inicial en última página - muestra controles, "Previous" habilitado, "Next" deshabilitado.
- **R4:** Navegación haciendo clic en número específico - carga esa página.
- **R5:** Navegación con botón "Next" - avanza a siguiente página (no disponible en última).
- **R6:** Navegación con botón "Previous" - retrocede a página anterior (no disponible en primera).

**Consolidación:** Las páginas intermedias se manejan con los mismos principios que las páginas 2 y penúltima, por lo que no requieren reglas separadas.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 5 reglas (excluyendo R1 que está fuera de alcance)

**Análisis de consolidación:**
- R2 y R3 representan estados iniciales y pueden describirse en un solo AC sobre "visualización de controles"
- R4, R5, R6 representan diferentes métodos de navegación

**Criterios de Aceptación finales:** **4 AC**

1. **AC1:** Visualizar controles de paginación cuando hay múltiples páginas
2. **AC2:** Navegar a página específica haciendo clic en número
3. **AC3:** Navegar a página siguiente con botón "Next"
4. **AC4:** Navegar a página anterior con botón "Previous"

No se detectaron AC redundantes. Cada uno valida un aspecto distinto de la funcionalidad de paginación.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar controles de paginación con múltiples páginas de asignaturas**

**Dado que** soy un profesor **Y** estoy en la vista "Asignaturas (PEA)" **Y** la cantidad total de asignaturas excede el límite de registros por página,  
**cuando** accedo a la lista de asignaturas,  
**entonces** se muestran los controles de paginación en la parte inferior de la tabla **Y** se visualiza el botón "Previous" a la izquierda **Y** se muestran los números de página disponibles en el centro (ej: 1, 2, 3) **Y** se visualiza el botón "Next" a la derecha **Y** la página actual está resaltada visualmente de las demás **Y** si estoy en la página 1, el botón "Previous" está deshabilitado o no clickeable **Y** si estoy en la última página, el botón "Next" está deshabilitado o no clickeable **Y** si estoy en una página intermedia, ambos botones "Previous" y "Next" están habilitados **Y** se muestra solo un subconjunto de asignaturas correspondiente a la página actual en la tabla **Y** todos los demás elementos de la interfaz (búsqueda, filtros, botón "+ Nueva Asignatura") permanecen visibles y funcionales **Y** puedo identificar claramente en qué página estoy y cuántas páginas hay disponibles para navegar por todos los programas de estudio.

---

### **Escenario 2 – Navegar a página específica haciendo clic en número de página**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** los controles de paginación están visibles **Y** hay múltiples páginas disponibles (ej: páginas 1, 2, 3),  
**cuando** hago clic en un número de página específico (ej: hago clic en el número "2" o "3"),  
**entonces** la tabla se actualiza automáticamente mostrando las asignaturas correspondientes a la página seleccionada **Y** el número de la página seleccionada se resalta visualmente indicando que es la página actual **Y** el número de la página anterior deja de estar resaltado **Y** la actualización ocurre sin recargar la página completa **Y** se mantienen activos los filtros de búsqueda y dropdowns que haya aplicado previamente **Y** el botón "Previous" se habilita si la página seleccionada no es la primera **Y** el botón "Next" se habilita si la página seleccionada no es la última **Y** la tabla muestra las filas de asignaturas con todos sus datos (Código, Nombre, Unidad de Integración, Créditos, Nivel, Acciones) **Y** navego eficientemente entre múltiples páginas de programas de estudio.

---

### **Escenario 3 – Navegar a página siguiente con botón "Next"**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** estoy visualizando una página que NO es la última (ej: estoy en página 1 o 2) **Y** el botón "Next" está habilitado,  
**cuando** hago clic en el botón "Next",  
**entonces** el sistema avanza automáticamente a la página siguiente (ej: de página 1 a página 2, o de página 2 a página 3) **Y** la tabla se actualiza mostrando las asignaturas de la nueva página **Y** el número de la nueva página actual se resalta visualmente **Y** el botón "Previous" se habilita automáticamente (ya que ya no estoy en la primera página) **Y** si avanzo a la última página, el botón "Next" se deshabilita automáticamente **Y** la actualización ocurre sin recargar la página completa **Y** se mantienen los filtros de búsqueda aplicados **Y** puedo continuar navegando secuencialmente hacia adelante por un gran número de programas de estudio.

---

### **Escenario 4 – Navegar a página anterior con botón "Previous"**

**Dado que** estoy en la vista "Asignaturas (PEA)" **Y** estoy visualizando una página que NO es la primera (ej: estoy en página 2 o 3) **Y** el botón "Previous" está habilitado,  
**cuando** hago clic en el botón "Previous",  
**entonces** el sistema retrocede automáticamente a la página anterior (ej: de página 3 a página 2, o de página 2 a página 1) **Y** la tabla se actualiza mostrando las asignaturas de la página anterior **Y** el número de la nueva página actual se resalta visualmente **Y** el botón "Next" se habilita automáticamente (ya que ya no estoy en la última página) **Y** si retrocedo a la primera página, el botón "Previous" se deshabilita automáticamente **Y** la actualización ocurre sin recargar la página completa **Y** se mantienen los filtros de búsqueda aplicados **Y** puedo continuar navegando secuencialmente hacia atrás por un gran número de programas de estudio.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Navegar a página específica haciendo clic en número de página**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumple directamente el objetivo de la Historia de Usuario:** La HU establece "Quiero paginar las asignaturas para navegar por un gran número de programas de estudio". El Escenario 2 valida la funcionalidad principal de navegación: poder saltar directamente a una página específica, que es la forma más eficiente de navegación cuando se conoce aproximadamente dónde está la información buscada.

2. **Método de navegación más versátil:** A diferencia de "Next" y "Previous" que solo permiten avanzar o retroceder secuencialmente de una en una, hacer clic en un número de página permite saltos directos (ej: de página 1 a página 3), lo cual es significativamente más eficiente para navegar en sistemas con muchas páginas.

3. **Happy path principal evidenciado en el prototipo:** La imagen 4 muestra explícitamente los números de página "1, 2, 3" como elementos clickeables, indicando que esta es la forma principal de navegación diseñada. Los números están centralmente ubicados y visualmente destacados entre los botones direccionales.

4. **Mayor impacto en usabilidad:** Si esta funcionalidad falla, los usuarios quedan limitados a navegación secuencial (Next/Previous), lo cual en un sistema con muchas páginas (ej: 10+ páginas de asignaturas) se vuelve extremadamente tedioso e ineficiente. Un profesor con 50+ asignaturas distribuidas en 5 páginas no querría hacer 4 clics en "Next" para llegar a la página 5.

5. **Validación de estado completa:** Este escenario valida múltiples aspectos críticos simultáneamente:
   - Cambio correcto de contenido de tabla
   - Actualización visual del indicador de página actual
   - Habilitación/deshabilitación apropiada de botones direccionales
   - Persistencia de filtros y búsquedas
   - Actualización sin recarga completa de página

6. **Caso de uso más frecuente en producción:** Los profesores típicamente conocen aproximadamente en qué página está una asignatura (ej: "las asignaturas de segundo semestre están en la página 2") y usarán la navegación directa en lugar de avanzar secuencialmente. Este será el método más usado en la práctica diaria.

Los escenarios 1, 3 y 4 son importantes para validar la visualización inicial y navegación secuencial, pero el Escenario 2 es el que demuestra la funcionalidad de paginación más potente y utilizada. Un fallo en la navegación por número de página forzaría a los usuarios a métodos más lentos e ineficientes, comprometiendo significativamente el valor de la funcionalidad. Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación.