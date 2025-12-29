# ANÁLISIS Y GENERACIÓN DE CRITERIOS DE ACEPTACIÓN

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

**Condiciones identificadas (de la HU y análisis visual de las imágenes 9 y 10):**

**C1:** Usuario está en la primera página (Sí/No)  
**C2:** Usuario está en la última página (Sí/No)  
**C3:** Existen múltiples páginas de RAs (Sí/No)  
**C4:** Usuario está en tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" (Esta condición no afecta la lógica de paginación, solo el contenido mostrado)

**Acciones del sistema identificadas (observadas en Imágenes 9 y 10):**

**A1:** Deshabilitar botón "< Previous"  
**A2:** Habilitar botón "< Previous"  
**A3:** Deshabilitar botón "Next >"  
**A4:** Habilitar botón "Next >"  
**A5:** Mostrar números de página como enlaces clicables (1, 2, 3)  
**A6:** Resaltar visualmente el número de la página actual  
**A7:** Cargar y mostrar los Resultados de Aprendizaje correspondientes a la página seleccionada  
**A8:** Mantener la estructura de la tabla con columnas "Código" y "Descripción"  
**A9:** Mostrar el campo de búsqueda "Buscar por código o descripción..."  
**A10:** Mostrar el botón "+ Nuevo RA" en la esquina superior derecha  
**A11:** Mostrar solo un indicador de página cuando hay una sola página  
**A12:** Mantener visible los tabs "Resultados Generales (RG)" y "Resultados Específicos (RE)"  
**A13:** Mostrar los códigos de RAs según el tab activo (RG1-RG5 o RE1-RE5)

---

### **Tabla de Decisión Completa (Maximizada)**

| Regla | C1: Primera página | C2: Última página | C3: Múltiples páginas | Acciones |
|-------|-------------------|-------------------|-----------------------|----------|
| R1 | Sí | Sí | No | A1, A3, A11, A7, A8, A9, A10, A12, A13 |
| R2 | Sí | Sí | Sí | *Imposible* |
| R3 | Sí | No | No | *Imposible* |
| R4 | Sí | No | Sí | A1, A4, A5, A6, A7, A8, A9, A10, A12, A13 |
| R5 | No | Sí | No | *Imposible* |
| R6 | No | Sí | Sí | A2, A3, A5, A6, A7, A8, A9, A10, A12, A13 |
| R7 | No | No | No | *Imposible* |
| R8 | No | No | Sí | A2, A4, A5, A6, A7, A8, A9, A10, A12, A13 |

**Análisis de imposibilidades lógicas:**
- R2: No se puede estar en primera y última página simultáneamente si hay múltiples páginas
- R3: No se puede estar solo en primera página sin estar en última si no hay múltiples páginas
- R5: No se puede estar solo en última página sin estar en primera si no hay múltiples páginas
- R7: Debe existir al menos una página con contenido

---

### **Tabla de Decisión Minimizada**

**Lógica de minimización:**
- Se eliminan las reglas imposibles por incompatibilidad lógica de condiciones
- R1 representa el caso de una sola página (única página donde primera = última)
- R4 representa estar en la primera página cuando existen múltiples páginas
- R6 representa estar en la última página cuando existen múltiples páginas
- R8 representa estar en una página intermedia cuando existen múltiples páginas
- La condición C4 (tab activo) no afecta la lógica de paginación, solo determina qué tipo de RAs se muestran (RG o RE)

| Regla | C1: Primera página | C2: Última página | C3: Múltiples páginas | Acciones |
|-------|-------------------|-------------------|-----------------------|----------|
| **R1** | Sí | Sí | No | A1, A3, A11, A7, A8, A9, A10, A12, A13 |
| **R2** | Sí | No | Sí | A1, A4, A5, A6, A7, A8, A9, A10, A12, A13 |
| **R3** | No | Sí | Sí | A2, A3, A5, A6, A7, A8, A9, A10, A12, A13 |
| **R4** | No | No | Sí | A2, A4, A5, A6, A7, A8, A9, A10, A12, A13 |

**Justificación de la minimización:**
Se eliminaron 4 reglas imposibles debido a incompatibilidad lógica de condiciones. Las 4 reglas restantes cubren exhaustivamente todos los estados válidos del sistema de paginación: página única, primera página de múltiples, última página de múltiples, y página intermedia. La paginación funciona de manera idéntica independientemente del tab activo (RG o RE), solo cambia el tipo de contenido mostrado.

---

### **Número Total de Criterios de Aceptación**

**Declaración:** Se requieren **8 Criterios de Aceptación** en total.

**Justificación:** 
- Las 4 reglas de la tabla minimizada generan 4 criterios base de estado (R1→AC1, R2→AC2, R3→AC3, R4→AC4)
- Se agregan 2 criterios adicionales para cubrir las acciones específicas de navegación:
  - Navegación mediante clic en número de página específico (AC5)
  - Navegación mediante botones "Previous" y "Next" (AC6)
- Se agregan 2 criterios adicionales para validar el comportamiento específico de los tabs observados en las imágenes:
  - Cambio entre tabs con paginación independiente (AC7)
  - Validación de que cada tab mantiene su estado de paginación (AC8)

**Criterios eliminados:** Ninguno. Aunque esta HU es similar a las anteriores de paginación (EUR-ACE y OPP), los criterios NO son idénticos debido a que:
1. Los datos de entrada son diferentes (Resultados de Aprendizaje vs Objetivos de Programa vs Criterios EUR-ACE)
2. Existe funcionalidad adicional única: sistema de tabs (RG/RE) que no existe en las otras vistas
3. Los códigos y descripciones mostrados son diferentes (RG1-RG5, RE1-RE5 vs OPP1-OPP5 vs códigos EUR-ACE)

Por lo tanto, todos los criterios deben conservarse ya que validan comportamientos específicos de esta vista.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar listado con una sola página de RAs**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" **Y** el total de Resultados de Aprendizaje del tipo seleccionado cabe en una sola página, **cuando** se carga la vista, **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran todos los RAs disponibles del tipo seleccionado con sus códigos (ej: RG1, RG2, RG3, RG4, RG5 o RE1, RE2, RE3, RE4, RE5) y descripciones completas **Y** el botón "< Previous" está deshabilitado o visualmente inactivo **Y** el botón "Next >" está deshabilitado o visualmente inactivo **Y** se muestra únicamente el número de página "1" sin ser clicable **Y** no se muestran números de páginas adicionales **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo RA" se muestra en la esquina superior derecha **Y** los tabs "Resultados Generales (RG)" y "Resultados Específicos (RE)" permanecen visibles.

### **Escenario 2 – Visualizar primera página cuando existen múltiples páginas de RAs**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" **Y** existen múltiples páginas de Resultados de Aprendizaje del tipo seleccionado, **cuando** cargo la vista por primera vez o navego a la página 1, **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los primeros RAs de la página 1 con sus códigos y descripciones según el tab activo (ej: RG1 "Comprender los principios fundamentales de la ingeniería de software.", RG2, RG3, RG4, RG5 o RE1, RE2, RE3, RE4, RE5) **Y** el botón "< Previous" está deshabilitado o visualmente inactivo **Y** el botón "Next >" está habilitado y es clicable **Y** se muestran los números de página disponibles (1, 2, 3) como enlaces clicables **Y** el número de página "1" aparece resaltado o con estilo diferenciado indicando que es la página actual **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo RA" se muestra en la esquina superior derecha **Y** los tabs "Resultados Generales (RG)" y "Resultados Específicos (RE)" permanecen visibles.

### **Escenario 3 – Visualizar última página cuando existen múltiples páginas de RAs**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" **Y** existen múltiples páginas de Resultados de Aprendizaje del tipo seleccionado, **cuando** navego a la última página disponible (ej: página 3), **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los RAs correspondientes a la última página con sus códigos y descripciones completas según el tab activo **Y** el botón "< Previous" está habilitado y es clicable **Y** el botón "Next >" está deshabilitado o visualmente inactivo **Y** se muestran los números de página disponibles (1, 2, 3) como enlaces clicables **Y** el número de la última página aparece resaltado o con estilo diferenciado indicando que es la página actual **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo RA" se muestra en la esquina superior derecha **Y** los tabs "Resultados Generales (RG)" y "Resultados Específicos (RE)" permanecen visibles.

### **Escenario 4 – Visualizar página intermedia cuando existen múltiples páginas de RAs**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" **Y** existen múltiples páginas de Resultados de Aprendizaje del tipo seleccionado (al menos 3 páginas), **cuando** navego a una página intermedia (ej: página 2), **entonces** se muestra la tabla con las columnas "Código" y "Descripción" **Y** se muestran los RAs correspondientes a la página intermedia seleccionada con sus códigos y descripciones completas según el tab activo **Y** el botón "< Previous" está habilitado y es clicable **Y** el botón "Next >" está habilitado y es clicable **Y** se muestran los números de página disponibles (1, 2, 3) como enlaces clicables **Y** el número de la página actual (2) aparece resaltado o con estilo diferenciado **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible **Y** el botón "+ Nuevo RA" se muestra en la esquina superior derecha **Y** los tabs "Resultados Generales (RG)" y "Resultados Específicos (RE)" permanecen visibles.

### **Escenario 5 – Navegar a página específica mediante número de página**

**Dado que** estoy en cualquier página de la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" **Y** existen múltiples páginas de Resultados de Aprendizaje del tipo seleccionado, **cuando** hago clic en un número de página específico (ej: "2"), **entonces** se actualiza la tabla sin recargar la página completa **Y** se muestran los RAs correspondientes a la página seleccionada con sus códigos y descripciones según el tab activo **Y** el número de página seleccionado (2) aparece resaltado o con estilo diferenciado **Y** el estado de los botones "< Previous" y "Next >" se actualiza según corresponda (habilitados o deshabilitados) **Y** se mantiene la estructura de columnas "Código" y "Descripción" **Y** el campo de búsqueda y el botón "+ Nuevo RA" permanecen visibles **Y** el tab activo se mantiene sin cambios.

### **Escenario 6 – Navegar usando botones Previous y Next**

**Dado que** estoy en una página intermedia de la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" o "Resultados Específicos (RE)" **Y** existen múltiples páginas de Resultados de Aprendizaje del tipo seleccionado, **cuando** hago clic en el botón "Next >", **entonces** se navega a la página siguiente **Y** se muestran los RAs de la nueva página con sus códigos y descripciones según el tab activo **Y** el número de página se incrementa y aparece resaltado **Y** cuando hago clic en el botón "< Previous", **entonces** se navega a la página anterior **Y** se muestran los RAs de esa página con sus códigos y descripciones según el tab activo **Y** el número de página se decrementa y aparece resaltado **Y** la navegación ocurre sin recargar la página completa **Y** se mantiene la estructura visual de la tabla y controles **Y** el tab activo se mantiene sin cambios.

### **Escenario 7 – Cambiar entre tabs con paginación independiente**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" en una página específica (ej: página 2), **cuando** hago clic en el tab "Resultados Específicos (RE)", **entonces** se cambia el contenido de la tabla para mostrar Resultados Específicos (RE) **Y** la paginación se resetea a la página 1 del nuevo tab **Y** se muestran los REs de la primera página con sus códigos (RE1, RE2, RE3, RE4, RE5) y descripciones **Y** los controles de paginación se actualizan según el total de páginas de REs disponibles **Y** el tab "Resultados Específicos (RE)" aparece visualmente activo o resaltado **Y** cuando regreso al tab "Resultados Generales (RG)", **entonces** se muestra nuevamente el contenido de RGs desde la página 1 **Y** se mantiene la estructura de tabla y controles de navegación.

### **Escenario 8 – Mantener estado de paginación al realizar acciones dentro del mismo tab**

**Dado que** estoy en la vista "Gestión de Resultados de Aprendizaje (RA)" **Y** soy un coordinador de carrera en el sistema **Y** estoy en el tab "Resultados Generales (RG)" en la página 2 **Y** realizo una acción que no implica cambio de tab (ej: búsqueda, creación de nuevo RA), **cuando** la acción se completa y regreso a la vista de listado, **entonces** se mantiene el tab activo "Resultados Generales (RG)" **Y** se mantiene la visualización de la página en la que estaba antes de la acción **Y** se mantienen los controles de paginación en el estado correcto según la página actual **Y** se muestra la notificación de "Completado" con el mensaje correspondiente si la acción fue exitosa.

---

## **3. Análisis de Criticidad**

### **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Visualizar primera página cuando existen múltiples páginas de RAs**

### **Justificación de su importancia:**

Este criterio es el **más crítico** por las siguientes razones fundamentales:

1. **Happy Path Principal y Punto de Entrada:** Representa el flujo natural y más frecuente cuando un coordinador de carrera accede a la vista "Gestión de Resultados de Aprendizaje (RA)". Es la primera experiencia del usuario con la funcionalidad de paginación en cualquiera de los tabs y determina si puede comenzar su tarea de revisión sistemática de RAs.

2. **Validación Directa del Valor de la HU:** Demuestra explícitamente el objetivo declarado en la Historia de Usuario: "revisar todos los RAs de forma organizada sin sobrecargar la pantalla". Si este escenario falla, el propósito fundamental de la paginación queda anulado desde el inicio, impidiendo la gestión efectiva de grandes volúmenes de Resultados de Aprendizaje.

3. **Dependencia en Cadena Crítica:** Todos los demás escenarios de navegación (Next, Previous, páginas específicas, última página, cambio de tabs) son inaccesibles o carecen de sentido si este estado inicial no se establece correctamente. Sin una primera página funcional, ninguna navegación posterior es posible.

4. **Elementos UI Completos Visibles en Prototipo:** Es el único escenario que valida simultáneamente todos los elementos esenciales observados en las imágenes 9 y 10: tabla completa con datos reales de RAs (códigos RG1-RG5 o RE1-RE5 con descripciones completas), botón Previous deshabilitado, botón Next habilitado, números de página clicables (1, 2, 3), página actual resaltada, campo de búsqueda, botón "+ Nuevo RA", y sistema de tabs.

5. **Impacto Directo en Responsabilidades Académicas:** Los Resultados de Aprendizaje son elementos centrales del diseño curricular y la evaluación educativa. Una falla en este escenario bloquea completamente la capacidad del coordinador de carrera para:
   - Revisar y validar los RAs del programa académico
   - Verificar la alineación entre RAs generales y específicos
   - Gestionar la trazabilidad curricular hacia Objetivos de Programa y Criterios EUR-ACE
   - Cumplir con procesos de aseguramiento de calidad académica

6. **Riesgo de Negocio y Acreditación:** Los Resultados de Aprendizaje son requisitos obligatorios para procesos de acreditación académica nacional e internacional (como EUR-ACE). Cualquier impedimento para revisarlos y gestionarlos sistemáticamente puede:
   - Afectar la preparación para auditorías de acreditación
   - Comprometer la evidencia de cumplimiento de estándares educativos
   - Impactar negativamente en la calidad y coherencia del programa académico

7. **Contexto Específico del Sistema de Tabs:** Este escenario es crítico porque establece el comportamiento esperado en ambos tabs (RG y RE), que son conceptualmente diferentes pero comparten la misma lógica de paginación. Validar que la primera página funciona correctamente en este contexto sienta las bases para toda la experiencia de navegación dual.