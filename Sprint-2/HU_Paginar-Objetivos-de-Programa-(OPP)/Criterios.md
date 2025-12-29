# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de las imágenes 2 y 5):**

**C1:** Usuario está en la primera página (Sí/No)  
**C2:** Usuario está en la última página (Sí/No)  
**C3:** Existen múltiples páginas de OPPs (Sí/No)

**Acciones del sistema identificadas (observadas en Imágenes 2 y 5):**

**A1:** Deshabilitar botón "< Previous"  
**A2:** Habilitar botón "< Previous"  
**A3:** Deshabilitar botón "Next >"  
**A4:** Habilitar botón "Next >"  
**A5:** Mostrar números de página como enlaces clicables (1, 2, 3)  
**A6:** Resaltar visualmente el número de la página actual  
**A7:** Cargar y mostrar los Objetivos de Programa (OPP) correspondientes a la página seleccionada  
**A8:** Mantener la estructura de la tabla con columnas "Código" y "Descripción"  
**A9:** Mostrar el campo de búsqueda "Buscar por código o descripción..."  
**A10:** Mostrar el botón "+ Nuevo OPP" en la esquina superior derecha  
**A11:** Mostrar solo un indicador de página cuando hay una sola página  

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Primera página | C2: Última página | C3: Múltiples páginas | Acciones |
|-------|-------------------|-------------------|-----------------------|----------|
| R1 | Sí | Sí | No | A1, A3, A11, A7, A8, A9, A10 |
| R2 | Sí | Sí | Sí | *Imposible* |
| R3 | Sí | No | No | *Imposible* |
| R4 | Sí | No | Sí | A1, A4, A5, A6, A7, A8, A9, A10 |
| R5 | No | Sí | No | *Imposible* |
| R6 | No | Sí | Sí | A2, A3, A5, A6, A7, A8, A9, A10 |
| R7 | No | No | No | *Imposible* |
| R8 | No | No | Sí | A2, A4, A5, A6, A7, A8, A9, A10 |

**Análisis de imposibilidades lógicas:**
- R2: No se puede estar en primera y última página simultáneamente si hay múltiples páginas
- R3: No se puede estar solo en primera página sin estar en última si no hay múltiples páginas
- R5: No se puede estar solo en última página sin estar en primera si no hay múltiples páginas
- R7: Debe existir al menos una página con contenido

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Se eliminan las reglas imposibles por incompatibilidad lógica
- R1 representa el caso de una sola página (única página donde primera = última)
- R4 representa estar en la primera página cuando existen múltiples páginas
- R6 representa estar en la última página cuando existen múltiples páginas
- R8 representa estar en una página intermedia cuando existen múltiples páginas

| Regla | C1: Primera página | C2: Última página | C3: Múltiples páginas | Acciones |
|-------|-------------------|-------------------|-----------------------|----------|
| **R1** | Sí | Sí | No | A1, A3, A11, A7, A8, A9, A10 |
| **R2** | Sí | No | Sí | A1, A4, A5, A6, A7, A8, A9, A10 |
| **R3** | No | Sí | Sí | A2, A3, A5, A6, A7, A8, A9, A10 |
| **R4** | No | No | Sí | A2, A4, A5, A6, A7, A8, A9, A10 |

**Justificación de la minimización:**
Se eliminaron 4 reglas imposibles debido a incompatibilidad lógica de condiciones. Las 4 reglas restantes cubren exhaustivamente todos los estados válidos del sistema de paginación: página única, primera página de múltiples, última página de múltiples, y página intermedia de múltiples.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **6 Criterios de Aceptación** en total.

**Justificación:** 
- Las 4 reglas de la tabla minimizada generan 4 criterios base de estado (R1→AC1, R2→AC2, R3→AC3, R4→AC4)
- Se agregan 2 criterios adicionales para cubrir las acciones específicas de navegación observadas en el prototipo:
  - Navegación mediante clic en número de página específico (AC5)
  - Navegación mediante botones "Previous" y "Next" (AC6)

**Criterios eliminados:** Ninguno. No se identificaron criterios redundantes, idénticos o repetidos. Cada criterio valida un estado o interacción única del sistema de paginación de OPPs que se observa en el prototipo.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar listado con una sola página de OPPs**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** el total de Objetivos de Programa existentes cabe en una sola página, **cuando** se carga la vista, **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran todos los OPPs disponibles con sus códigos (ej: OPP1, OPP2, OPP3, OPP4, OPP5) y descripciones completas **Y** el botón "< Previous" está deshabilitado o visualmente inactivo **Y** el botón "Next >" está deshabilitado o visualmente inactivo **Y** se muestra únicamente el número de página "1" sin ser clicable **Y** no se muestran números de páginas adicionales **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo OPP" se muestra en la esquina superior derecha.

### **Escenario 2 – Visualizar primera página cuando existen múltiples páginas de OPPs**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** existen múltiples páginas de Objetivos de Programa, **cuando** cargo la vista por primera vez o navego a la página 1, **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los primeros OPPs de la página 1 con sus códigos y descripciones (ej: OPP1 "Comprender los principios fundamentales de la ingeniería de software.", OPP2, OPP3, OPP4, OPP5) **Y** el botón "< Previous" está deshabilitado o visualmente inactivo **Y** el botón "Next >" está habilitado y es clicable **Y** se muestran los números de página disponibles (1, 2, 3) como enlaces clicables **Y** el número de página "1" aparece resaltado o con estilo diferenciado indicando que es la página actual **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo OPP" se muestra en la esquina superior derecha.

### **Escenario 3 – Visualizar última página cuando existen múltiples páginas de OPPs**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** existen múltiples páginas de Objetivos de Programa, **cuando** navego a la última página disponible (ej: página 3), **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los OPPs correspondientes a la última página con sus códigos y descripciones completas **Y** el botón "< Previous" está habilitado y es clicable **Y** el botón "Next >" está deshabilitado o visualmente inactivo **Y** se muestran los números de página disponibles (1, 2, 3) como enlaces clicables **Y** el número de la última página aparece resaltado o con estilo diferenciado indicando que es la página actual **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo OPP" se muestra en la esquina superior derecha.

### **Escenario 4 – Visualizar página intermedia cuando existen múltiples páginas de OPPs**

**Dado que** estoy en la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** existen múltiples páginas de Objetivos de Programa (al menos 3 páginas), **cuando** navego a una página intermedia (ej: página 2), **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los OPPs correspondientes a la página intermedia seleccionada con sus códigos y descripciones completas **Y** el botón "< Previous" está habilitado y es clicable **Y** el botón "Next >" está habilitado y es clicable **Y** se muestran los números de página disponibles (1, 2, 3) como enlaces clicables **Y** el número de la página actual (2) aparece resaltado o con estilo diferenciado **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo OPP" se muestra en la esquina superior derecha.

### **Escenario 5 – Navegar a página específica mediante número de página**

**Dado que** estoy en cualquier página de la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** existen múltiples páginas de Objetivos de Programa, **cuando** hago clic en un número de página específico (ej: "2"), **entonces** se actualiza la tabla sin recargar la página completa **Y** se muestran los OPPs correspondientes a la página seleccionada con sus códigos y descripciones **Y** el número de página seleccionado (2) aparece resaltado o con estilo diferenciado **Y** el estado de los botones "< Previous" y "Next >" se actualiza según corresponda (habilitados o deshabilitados) **Y** se mantiene la estructura de columnas "Código" y "Descripción" **Y** el campo de búsqueda y el botón "+ Nuevo OPP" permanecen visibles.

### **Escenario 6 – Navegar usando botones Previous y Next**

**Dado que** estoy en una página intermedia de la vista "Gestión de Objetivos de Carrera (OPP)" **Y** soy un coordinador de carrera en el sistema **Y** existen múltiples páginas de Objetivos de Programa, **cuando** hago clic en el botón "Next >", **entonces** se navega a la página siguiente **Y** se muestran los OPPs de la nueva página con sus códigos y descripciones **Y** el número de página se incrementa y aparece resaltado **Y** cuando hago clic en el botón "< Previous", **entonces** se navega a la página anterior **Y** se muestran los OPPs de esa página con sus códigos y descripciones **Y** el número de página se decrementa y aparece resaltado **Y** la navegación ocurre sin recargar la página completa **Y** se mantiene la estructura visual de la tabla y controles.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Visualizar primera página cuando existen múltiples páginas de OPPs**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Happy Path Principal y Punto de Entrada:** Representa el flujo natural y más frecuente cuando un coordinador de carrera accede a la vista "Gestión de Objetivos de Carrera (OPP)". Es la primera experiencia del usuario con la funcionalidad de paginación y determina si puede comenzar su tarea de revisión.

2. **Validación Directa del Valor de la HU:** Demuestra explícitamente el objetivo declarado en la Historia de Usuario: "revisar todos los OPPs de forma organizada sin sobrecargar la pantalla". Si este escenario falla, el propósito fundamental de la paginación queda anulado desde el inicio.

3. **Dependencia en Cadena:** Todos los demás escenarios de navegación (Next, Previous, páginas específicas, última página) son inaccesibles si este estado inicial no se establece correctamente. Sin una primera página funcional, ninguna navegación posterior es posible.

4. **Elementos UI Completos Visibles:** Es el único escenario que valida simultáneamente todos los elementos esenciales observados en el prototipo (Imagen 2): tabla completa con datos reales de OPPs, botón Previous deshabilitado, botón Next habilitado, números de página clicables (1, 2, 3), página actual resaltada, campo de búsqueda, y botón "+ Nuevo OPP".

5. **Impacto en Experiencia del Usuario y Adopción:** Una falla en este escenario bloquea completamente la capacidad del coordinador de carrera para revisar los Objetivos de Programa, impidiendo el cumplimiento de sus responsabilidades académicas de supervisión y planificación curricular.

6. **Riesgo de Negocio:** Los Objetivos de Programa son elementos críticos para la acreditación académica y la planificación curricular. Cualquier impedimento para revisarlos sistemáticamente puede afectar procesos de aseguramiento de calidad educativa y cumplimiento normativo.