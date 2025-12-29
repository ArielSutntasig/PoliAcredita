# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de las imágenes):**

**C1:** Usuario está en la primera página (Sí/No)  
**C2:** Usuario está en la última página (Sí/No)  
**C3:** Existen múltiples páginas de criterios (Sí/No)

**Acciones del sistema identificadas (observadas en Imagen 11):**

**A1:** Deshabilitar botón "< Previous"  
**A2:** Habilitar botón "< Previous"  
**A3:** Deshabilitar botón "Next >"  
**A4:** Habilitar botón "Next >"  
**A5:** Mostrar números de página como enlaces clicables (1, 2, 3)  
**A6:** Resaltar visualmente el número de la página actual  
**A7:** Cargar y mostrar los criterios EUR-ACE correspondientes a la página seleccionada  
**A8:** Mantener la estructura de la tabla (columnas "Código" y "Descripción")  
**A9:** Mostrar solo un indicador de página cuando hay una sola página  

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Primera página | C2: Última página | C3: Múltiples páginas | Acciones |
|-------|-------------------|-------------------|-----------------------|----------|
| R1 | Sí | Sí | No | A1, A3, A9, A7, A8 |
| R2 | Sí | Sí | Sí | *Imposible* |
| R3 | Sí | No | No | *Imposible* |
| R4 | Sí | No | Sí | A1, A4, A5, A6, A7, A8 |
| R5 | No | Sí | No | *Imposible* |
| R6 | No | Sí | Sí | A2, A3, A5, A6, A7, A8 |
| R7 | No | No | No | *Imposible* |
| R8 | No | No | Sí | A2, A4, A5, A6, A7, A8 |

**Análisis de imposibilidades lógicas:**
- R2: No puedes estar en primera y última página si hay múltiples páginas
- R3: No puedes estar solo en primera página sin estar en última si no hay múltiples páginas
- R5: No puedes estar solo en última página sin estar en primera si no hay múltiples páginas
- R7: Debe existir al menos una página

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Las reglas imposibles se eliminan
- R1 representa el caso de una sola página (primera = última = única página)
- R4 representa la navegación en la primera página cuando hay múltiples páginas
- R6 representa la navegación en la última página cuando hay múltiples páginas
- R8 representa la navegación en páginas intermedias

| Regla | C1: Primera página | C2: Última página | C3: Múltiples páginas | Acciones |
|-------|-------------------|-------------------|-----------------------|----------|
| **R1** | Sí | Sí | No | A1, A3, A9, A7, A8 |
| **R2** | Sí | No | Sí | A1, A4, A5, A6, A7, A8 |
| **R3** | No | Sí | Sí | A2, A3, A5, A6, A7, A8 |
| **R4** | No | No | Sí | A2, A4, A5, A6, A7, A8 |

**Justificación de la minimización:**
Se eliminaron 4 reglas imposibles por incompatibilidad lógica de condiciones. Las 4 reglas restantes cubren todos los estados válidos del sistema de paginación: una sola página, primera página de múltiples, última página de múltiples, y página intermedia.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **6 Criterios de Aceptación** en total.

**Justificación:** 
- Las 4 reglas de la tabla minimizada generan 4 criterios base (R1→AC1, R2→AC2, R3→AC3, R4→AC4)
- Se agregan 2 criterios adicionales para cubrir las acciones de navegación específicas: hacer clic en un número de página específico (AC5) y hacer clic en "Next"/"Previous" para navegación real (AC6)
- No se generan criterios redundantes o superfluos

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar listado con una sola página de criterios**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema **Y** el total de criterios EUR-ACE existentes cabe en una sola página, **cuando** se carga la vista, **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran todos los criterios EUR-ACE disponibles (ej: 5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5) **Y** el botón "< Previous" está deshabilitado **Y** el botón "Next >" está deshabilitado **Y** se muestra únicamente el número de página "1" sin ser clicable **Y** no se muestran números de páginas adicionales.

### **Escenario 2 – Visualizar primera página cuando existen múltiples páginas**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema **Y** existen múltiples páginas de criterios EUR-ACE, **cuando** cargo la vista por primera vez o navego a la página 1, **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los primeros criterios EUR-ACE de la página 1 **Y** el botón "< Previous" está deshabilitado o visualmente inactivo **Y** el botón "Next >" está habilitado y es clicable **Y** se muestran los números de página disponibles (1, 2, 3...) como enlaces clicables **Y** el número de página "1" aparece resaltado o con estilo diferenciado indicando que es la página actual **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible.

### **Escenario 3 – Visualizar última página cuando existen múltiples páginas**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema **Y** existen múltiples páginas de criterios EUR-ACE, **cuando** navego a la última página disponible (ej: página 3), **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los criterios EUR-ACE correspondientes a la última página **Y** el botón "< Previous" está habilitado y es clicable **Y** el botón "Next >" está deshabilitado o visualmente inactivo **Y** se muestran los números de página disponibles (1, 2, 3...) como enlaces clicables **Y** el número de la última página aparece resaltado o con estilo diferenciado indicando que es la página actual.

### **Escenario 4 – Visualizar página intermedia cuando existen múltiples páginas**

**Dado que** estoy en la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema **Y** existen múltiples páginas de criterios EUR-ACE (al menos 3 páginas), **cuando** navego a una página intermedia (ej: página 2), **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los criterios EUR-ACE correspondientes a la página intermedia seleccionada **Y** el botón "< Previous" está habilitado y es clicable **Y** el botón "Next >" está habilitado y es clicable **Y** se muestran los números de página disponibles (1, 2, 3...) como enlaces clicables **Y** el número de la página actual (2) aparece resaltado o con estilo diferenciado.

### **Escenario 5 – Navegar a página específica mediante número de página**

**Dado que** estoy en cualquier página de la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema **Y** existen múltiples páginas de criterios EUR-ACE, **cuando** hago clic en un número de página específico (ej: "2"), **entonces** se actualiza la tabla sin recargar la página completa **Y** se muestran los criterios EUR-ACE correspondientes a la página seleccionada **Y** el número de página seleccionado (2) aparece resaltado **Y** el estado de los botones "< Previous" y "Next >" se actualiza según corresponda (habilitados o deshabilitados) **Y** se mantiene la estructura de columnas "Código" y "Descripción".

### **Escenario 6 – Navegar usando botones Previous y Next**

**Dado que** estoy en una página intermedia de la vista "Criterios EUR-ACE" **Y** soy un administrador en el sistema **Y** existen múltiples páginas de criterios EUR-ACE, **cuando** hago clic en el botón "Next >", **entonces** se navega a la página siguiente **Y** se muestran los criterios EUR-ACE de la nueva página **Y** el número de página se incrementa y aparece resaltado **Y** cuando hago clic en el botón "< Previous", **entonces** se navega a la página anterior **Y** se muestran los criterios EUR-ACE de esa página **Y** el número de página se decrementa y aparece resaltado **Y** la navegación ocurre sin recargar la página completa.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Visualizar primera página cuando existen múltiples páginas**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones:

1. **Happy Path Principal:** Representa el flujo de entrada natural del usuario administrador al acceder a la funcionalidad por primera vez, que es el caso de uso más común y frecuente.

2. **Validación del Valor de la HU:** Demuestra directamente el objetivo declarado en la Historia de Usuario: "revisar todos los criterios de forma organizada sin sobrecargar la pantalla". Si la primera página no se visualiza correctamente con los controles de paginación, el valor completo de la funcionalidad queda comprometido.

3. **Base para Navegación Posterior:** Todos los demás escenarios de navegación (siguiente, anterior, páginas específicas) dependen de que este estado inicial funcione correctamente. Si falla, ninguna otra interacción de paginación será posible.

4. **Elementos UI Críticos Visibles:** Es el único escenario donde se validan simultáneamente todos los elementos esenciales que se observan en el prototipo (Imagen 11): tabla completa, botón Previous deshabilitado, botón Next habilitado, números de página clicables, y página actual resaltada.

5. **Impacto en Experiencia del Usuario:** Una falla en este escenario impediría al administrador comenzar su tarea de revisión de criterios EUR-ACE, bloqueando completamente la funcionalidad desde el punto de entrada.