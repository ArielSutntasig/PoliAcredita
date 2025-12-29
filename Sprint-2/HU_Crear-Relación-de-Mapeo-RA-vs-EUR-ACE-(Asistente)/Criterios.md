# **ANÁLISIS COMPLETO - HU: Crear Relación de Mapeo RA vs EUR-ACE (Asistente)**

---

## **PASO 1: IDENTIFICAR CONDICIONES Y ACCIONES**

### **📋 CONDICIONES IDENTIFICADAS:**

**C1:** Usuario tiene rol de Coordinador de Carrera (**V** = Sí, **F** = No)

**C2:** Criterio EUR-ACE seleccionado existe en el sistema (**V** = Sí, **F** = No)

**C3:** RA seleccionado existe en el sistema (**V** = Sí, **F** = No)

**C4:** Campo "Justificación" está completo (**V** = Sí, **F** = No)

**C5:** La relación RA-EURACE ya existe en la matriz (**V** = Sí, **F** = No)

---

### **⚙️ ACCIONES RESULTANTES:**

**A1:** Sistema permite acceso al wizard de creación de relación RA-EURACE

**A2:** Sistema muestra mensaje de error "No tiene permisos para realizar esta acción"

**A3:** Sistema permite avanzar al Paso 2 (Seleccionar RA)

**A4:** Sistema muestra mensaje "Debe seleccionar un Criterio EUR-ACE"

**A5:** Sistema permite avanzar al Paso 3 (Justificar)

**A6:** Sistema muestra mensaje "Debe seleccionar un Resultado de Aprendizaje"

**A7:** Sistema guarda la relación RA-EURACE con su justificación y muestra mensaje "Se agregó la relación correctamente"

**A8:** Sistema muestra mensaje "Debe completar el campo de justificación"

**A9:** Sistema muestra mensaje "Esta relación ya existe entre el RA y el Criterio EUR-ACE seleccionados"

---

### **📸 ANÁLISIS VISUAL DE IMÁGENES DEL PROTOTIPO:**

**Imagen 11 - Listado de Criterios EUR-ACE:**
- Tabla con códigos EUR-ACE: 5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5
- Descripciones detalladas de cada criterio
- Campo de búsqueda "Buscar por código o descripción..."
- Paginación en la parte inferior

**Imagen 17 - Matriz RA vs EUR-ACE (Vista Final):**
- Título: "Matriz: Resultados de Aprendizaje (RA) y Criterios EUR-ACE"
- Eje horizontal: Códigos RA (RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6, RE7...)
- Eje vertical: Códigos Criterios EUR-ACE (5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5, 5.4.6, 5.5.1)
- Checkmarks verdes (✓) en las intersecciones donde existe relación
- Botón "+ Nueva Relación" en esquina superior derecha
- Íconos de información (ℹ️) en encabezados de filas y columnas

**Imagen 19 y 20 - Wizard Paso 3 "Justificar Relación":**
- Indicadores de pasos: 1 (✓), 2 (✓), 3 (activo)
- Título del paso 3: "Justificar Relación"
- **Sección "Elementos Seleccionado:"**
  - **"Criterio EUR-ACE:"** con descripción completa
  - **"Resultado de aprendizaje de carrera:"** con descripción completa
- **Título del formulario:** "Justifique la relación de RA vs EUR-ACE"
- **Campo de texto:** Área multilínea con placeholder "Escribe tu justificación detallada aquí para la relación entre el Objetivo de Carrera y el Resultado de Aprendizaje seleccionados."
- **Botones:**
  - "Cancelar" (rojo, izquierda)
  - "Guardar" (azul, derecha)

---

## **PASO 2: TABLA DE DECISIÓN COMPLETA (MAXIMIZADA)**

Con 5 condiciones, tenemos **2^5 = 32 reglas teóricas posibles**.

| **Regla** | **C1** | **C2** | **C3** | **C4** | **C5** | **Acciones** |
|-----------|--------|--------|--------|--------|--------|--------------|
| R1 | V | V | V | V | F | A1, A3, A5, A7 ✅ **HAPPY PATH** |
| R2 | V | V | V | V | V | A1, A3, A5, A9 |
| R3 | V | V | V | F | F | A1, A3, A5, A8 |
| R4 | V | V | V | F | V | A1, A3, A5, A8 |
| R5 | V | V | F | V | F | A1, A3, A6 |
| R6 | V | V | F | V | V | A1, A3, A6 |
| R7 | V | V | F | F | F | A1, A3, A6 |
| R8 | V | V | F | F | V | A1, A3, A6 |
| R9 | V | F | V | V | F | A1, A4 |
| R10 | V | F | V | V | V | A1, A4 |
| R11 | V | F | V | F | F | A1, A4 |
| R12 | V | F | V | F | V | A1, A4 |
| R13 | V | F | F | V | F | A1, A4 |
| R14 | V | F | F | V | V | A1, A4 |
| R15 | V | F | F | F | F | A1, A4 |
| R16 | V | F | F | F | V | A1, A4 |
| R17 | F | V | V | V | F | A2 |
| R18 | F | V | V | V | V | A2 |
| R19 | F | V | V | F | F | A2 |
| R20 | F | V | V | F | V | A2 |
| R21 | F | V | F | V | F | A2 |
| R22 | F | V | F | V | V | A2 |
| R23 | F | V | F | F | F | A2 |
| R24 | F | V | F | F | V | A2 |
| R25 | F | F | V | V | F | A2 |
| R26 | F | F | V | V | V | A2 |
| R27 | F | F | V | F | F | A2 |
| R28 | F | F | V | F | V | A2 |
| R29 | F | F | F | V | F | A2 |
| R30 | F | F | F | V | V | A2 |
| R31 | F | F | F | F | F | A2 |
| R32 | F | F | F | F | V | A2 |

---

## **PASO 3: TABLA DE DECISIÓN MINIMIZADA**

### **Análisis de Minimización:**

**Grupo 1 - Sin permisos (C1=F):**
Todas las reglas R17-R32 resultan en A2, independientemente de C2, C3, C4, C5.
**→ Se fusionan en R_MIN1**

**Grupo 2 - Criterio EUR-ACE no seleccionado (C1=V, C2=F):**
Reglas R9-R16 resultan en A1, A4, independientemente de C3, C4, C5.
**→ Se fusionan en R_MIN2**

**Grupo 3 - RA no seleccionado (C1=V, C2=V, C3=F):**
Reglas R5-R8 resultan en A1, A3, A6, independientemente de C4, C5.
**→ Se fusionan en R_MIN3**

**Grupo 4 - Justificación vacía (C1=V, C2=V, C3=V, C4=F):**
Reglas R3-R4 resultan en A1, A3, A5, A8, independientemente de C5.
**→ Se fusionan en R_MIN4**

**Reglas individuales:**
- **R1** (Happy path): C1=V, C2=V, C3=V, C4=V, C5=F → Único camino exitoso
- **R2** (Relación duplicada): C1=V, C2=V, C3=V, C4=V, C5=V → Error específico

---

### **🎯 TABLA MINIMIZADA FINAL:**

| **Regla** | **C1** | **C2** | **C3** | **C4** | **C5** | **Acciones** | **Descripción** |
|-----------|--------|--------|--------|--------|--------|--------------|-----------------|
| **R_MIN1** | **F** | **-** | **-** | **-** | **-** | **A2** | Sin permisos |
| **R_MIN2** | **V** | **F** | **-** | **-** | **-** | **A1, A4** | EUR-ACE no seleccionado |
| **R_MIN3** | **V** | **V** | **F** | **-** | **-** | **A1, A3, A6** | RA no seleccionado |
| **R_MIN4** | **V** | **V** | **V** | **F** | **-** | **A1, A3, A5, A8** | Justificación vacía |
| **R_MIN5** | **V** | **V** | **V** | **V** | **V** | **A1, A3, A5, A9** | Relación duplicada |
| **R_MIN6** ✅ | **V** | **V** | **V** | **V** | **F** | **A1, A3, A5, A7** | **HAPPY PATH** |

**Reducción: De 32 reglas → 6 reglas (81.25% de reducción)**

---

## **PASO 4: NÚMERO FINAL DE CRITERIOS DE ACEPTACIÓN**

Con base en la tabla minimizada, se requieren **6 Criterios de Aceptación**.

### **Justificación de eliminaciones:**

✅ **Se mantienen los 6 AC** derivados directamente de la tabla minimizada.

❌ **No se eliminan criterios** porque cada uno valida un escenario único y no redundante:
- R_MIN1: Validación de permisos (específica para esta matriz RA-EURACE)
- R_MIN2: Validación de selección obligatoria de Criterio EUR-ACE en Paso 1
- R_MIN3: Validación de selección obligatoria de RA en Paso 2
- R_MIN4: Validación de campo obligatorio "Justificación" en Paso 3
- R_MIN5: Validación de regla de negocio (unicidad de relaciones RA-EURACE)
- R_MIN6: Flujo completo exitoso para alineación con estándares EUR-ACE (CRÍTICO)

**Nota sobre similitud con HU anterior (OPP vs RA):**
Aunque esta HU sigue el mismo **patrón de wizard** que la HU "Crear Relación OPP vs RA", los criterios NO son redundantes porque:
- Las **entidades relacionadas son diferentes**: RA-EURACE vs OPP-RA
- El **propósito de negocio es diferente**: Alineación con estándares de acreditación EUR-ACE vs alineación curricular interna
- Los **datos manejados son distintos**: Códigos EUR-ACE (5.4.1, 5.4.2...) vs códigos OPP (OPP1, OPP2...)
- La **matriz resultante es diferente**: Una matriz mapea competencias internas, la otra mapea cumplimiento de estándares externos
- El **momento en el proceso de acreditación es diferente**: Esta HU es crítica para evidenciar cumplimiento de EUR-ACE ante auditores externos

---

## **PASO 5: CRITERIOS DE ACEPTACIÓN EN FORMATO GHERKIN**

### **AC1 - Creación exitosa de relación RA-EURACE (HAPPY PATH)**

**Dado que** soy un Coordinador de Carrera autenticado en el sistema

**Y** estoy en la pantalla "Matriz: Resultados de Aprendizaje (RA) y Criterios EUR-ACE"

**Cuando** hago clic en el botón "+ Nueva Relación"

**Entonces** se abre el wizard de creación con 3 pasos visibles en la parte superior

**Y** el paso 1 "Seleccionar Criterio EUR-ACE" está activo y resaltado

**Y** se muestra una tabla con columnas "Código" y "Descripción" de los Criterios EUR-ACE disponibles

**Y** se muestra un campo de búsqueda "Buscar por código o descripción..."

**Y** los pasos 2 y 3 están visibles pero inactivos.

**Cuando** selecciono un Criterio EUR-ACE de la tabla (ejemplo: 5.4.3)

**Entonces** el sistema avanza automáticamente al paso 2 "Seleccionar Resultados de Aprendizaje (RA)"

**Y** el paso 1 muestra un ícono de completado (✓)

**Y** el paso 2 está activo y resaltado

**Y** se muestra la sección "Elementos Seleccionado:" en la parte superior

**Y** se muestra el "Criterio EUR-ACE:" con el código y descripción del criterio seleccionado

**Y** se muestra un dropdown "Tipo de Aprendizaje" con opciones para filtrar RG/RE

**Y** se muestra una tabla con los RAs disponibles según el tipo seleccionado.

**Cuando** selecciono un RA de la tabla (ejemplo: RE1)

**Entonces** el sistema avanza automáticamente al paso 3 "Justificar Relación"

**Y** el paso 2 muestra un ícono de completado (✓)

**Y** el paso 3 está activo y resaltado

**Y** la sección "Elementos Seleccionado:" muestra tanto el Criterio EUR-ACE como el RA seleccionados

**Y** se muestra el título "Justifique la relación de RA vs EUR-ACE"

**Y** se muestra un campo de texto multilínea con placeholder "Escribe tu justificación detallada aquí para la relación entre el Objetivo de Carrera y el Resultado de Aprendizaje seleccionados."

**Y** se muestran los botones "Cancelar" (rojo) y "Guardar" (azul).

**Cuando** escribo una justificación válida en el campo de texto

**Y** hago clic en el botón "Guardar"

**Entonces** se cierra el wizard

**Y** regreso a la vista de la matriz RA vs Criterios EUR-ACE

**Y** se muestra un mensaje de éxito "Completado - Se agregó la relación correctamente"

**Y** en la matriz se muestra un checkmark verde (✓) en la intersección del RA y Criterio EUR-ACE seleccionados

**Y** la matriz se actualiza sin necesidad de recargar la página completa.

---

### **AC2 - Intento de crear relación sin permisos**

**Dado que** estoy autenticado en el sistema

**Y** NO tengo el rol de "Coordinador de Carrera"

**Cuando** intento acceder a la pantalla "Matriz: Resultados de Aprendizaje (RA) y Criterios EUR-ACE"

**Entonces** el sistema me redirige a la pantalla de inicio

**Y** se muestra un mensaje de error "No tiene permisos para realizar esta acción"

**Y** NO puedo acceder al botón "+ Nueva Relación"

**Y** NO puedo abrir el wizard de creación de relaciones RA-EURACE.

---

### **AC3 - Intento de avanzar sin seleccionar Criterio EUR-ACE (Paso 1 incompleto)**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** he abierto el wizard de creación de relación RA-EURACE

**Y** estoy en el paso 1 "Seleccionar Criterio EUR-ACE"

**Cuando** intento avanzar al paso 2 sin seleccionar ningún Criterio EUR-ACE

**Entonces** el sistema muestra un mensaje de validación "Debe seleccionar un Criterio EUR-ACE"

**Y** permanezco en el paso 1

**Y** el paso 2 permanece inactivo

**Y** NO se permite avanzar hasta que seleccione un Criterio EUR-ACE válido.

---

### **AC4 - Intento de avanzar sin seleccionar RA (Paso 2 incompleto)**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** he completado el paso 1 seleccionando un Criterio EUR-ACE

**Y** estoy en el paso 2 "Seleccionar Resultados de Aprendizaje (RA)"

**Cuando** intento avanzar al paso 3 sin seleccionar ningún RA

**Entonces** el sistema muestra un mensaje de validación "Debe seleccionar un Resultado de Aprendizaje"

**Y** permanezco en el paso 2

**Y** el paso 3 permanece inactivo

**Y** NO se permite avanzar hasta que seleccione un RA válido.

---

### **AC5 - Intento de guardar sin completar justificación (Paso 3 incompleto)**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** he completado los pasos 1 y 2 seleccionando un Criterio EUR-ACE y un RA

**Y** estoy en el paso 3 "Justificar Relación"

**Cuando** dejo el campo de "Justificación" vacío

**Y** hago clic en el botón "Guardar"

**Entonces** el sistema muestra un mensaje de validación "Debe completar el campo de justificación"

**Y** el botón "Guardar" NO ejecuta la acción de guardado

**Y** permanezco en el paso 3 con el wizard abierto

**Y** el campo "Justificación" se resalta visualmente indicando que es obligatorio.

---

### **AC6 - Intento de crear relación duplicada**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** ya existe una relación entre un Criterio EUR-ACE específico (ejemplo: 5.4.3) y un RA específico (ejemplo: RE1) en la matriz

**Cuando** abro el wizard de creación de relación

**Y** selecciono el mismo Criterio EUR-ACE (5.4.3) en el paso 1

**Y** selecciono el mismo RA (RE1) en el paso 2

**Y** completo la justificación en el paso 3

**Y** hago clic en el botón "Guardar"

**Entonces** el sistema muestra un mensaje de error "Esta relación ya existe entre el RA y el Criterio EUR-ACE seleccionados"

**Y** NO se crea una relación duplicada en la matriz

**Y** el wizard permanece abierto en el paso 3

**Y** puedo modificar mi selección o cancelar la operación.

---

## **PASO 6: IDENTIFICAR EL CRITERIO MÁS CRÍTICO**

### **🎯 CRITERIO MÁS CRÍTICO:**

**AC1 - Creación exitosa de relación RA-EURACE (HAPPY PATH)**

---

### **✅ JUSTIFICACIÓN DE CRITICIDAD:**

1. **Propósito central de acreditación EUR-ACE**: Este criterio valida la **capacidad del sistema de documentar el cumplimiento de estándares de acreditación europeos** (EUR-ACE). Sin esta funcionalidad, el programa académico no puede demostrar alineación con estándares internacionales de calidad en ingeniería, lo cual es **requisito obligatorio** para acreditación internacional.

2. **Evidencia auditable para acreditadores externos**: La creación de relaciones RA-EURACE con justificación genera la **documentación formal** que los auditores EUR-ACE requieren para verificar que el programa cumple con criterios específicos (ej: 5.4.1 "investigación en solución de problemas"). Sin este AC funcionando, no hay evidencia auditable.

3. **Diferenciador vs alineación interna**: A diferencia de la HU anterior (OPP-RA que es alineación curricular interna), esta HU mapea contra **estándares externos obligatorios**. El impacto del fallo es mayor: no solo afecta la gestión interna, sino que compromete la **acreditación internacional del programa**.

4. **Flujo completo del wizard para EUR-ACE**: Este AC valida los **3 pasos especializados** del asistente guiado para documentación de estándares:
   - Paso 1: Selección de Criterio EUR-ACE específico (códigos 5.x.x)
   - Paso 2: Selección de RA que cumple ese criterio
   - Paso 3: Justificación que explica cómo el RA satisface el criterio EUR-ACE

5. **Trazabilidad bidireccional para auditorías**: Permite a los auditores verificar:
   - **Dirección RA→EURACE**: "¿Este resultado de aprendizaje cumple qué criterios EUR-ACE?"
   - **Dirección EURACE→RA**: "¿Este criterio EUR-ACE está cubierto por qué resultados de aprendizaje?"

6. **Valor diferenciador del wizard guiado**: La HU especifica usar un **asistente paso a paso (WIZARD)** para "documentar la alineación con los estándares de acreditación **de forma guiada y eficiente**". Este AC valida que el patrón wizard efectivamente reduce la complejidad de mapear contra 50+ criterios EUR-ACE.

7. **Impacto institucional crítico**: El fallo de este AC tiene consecuencias institucionales severas:
   - **No acreditación internacional** del programa de ingeniería
   - **Pérdida de prestigio** y competitividad internacional
   - **Impedimento para convenios** de doble titulación con universidades europeas
   - **Restricción de movilidad estudiantil** internacional
   - **Pérdida de reconocimiento profesional** de egresados en el extranjero

8. **Complejidad técnica especializada**: Este AC requiere validar:
   - Manejo de códigos EUR-ACE jerárquicos (5.4.1, 5.4.2...)
   - Integración con descripciones extensas de criterios (párrafos completos)
   - Filtrado por tipo de RA (RG vs RE) relevante para cada criterio
   - Justificaciones académicas que serán revisadas por evaluadores externos
   - Actualización de matriz bidimensional compleja (7+ RAs × 10+ Criterios EUR-ACE)

9. **Prerequisito para reportes de acreditación**: Los reportes que se entregarán a EUR-ACE se generan a partir de las relaciones creadas mediante este wizard. Sin este AC funcionando correctamente, los reportes de acreditación estarán incompletos o incorrectos.

10. **Evidencia visual directa del caso de uso principal**: Las imágenes 17, 19 y 20 muestran explícitamente:
    - La matriz RA-EURACE poblada con checkmarks (imagen 17)
    - El paso 3 del wizard con ambos elementos seleccionados (imagen 19-20)
    - El formulario de justificación específico para "RA vs EUR-ACE"
    - Esto indica que es el **flujo principal** diseñado para cumplir con requisitos de acreditación

11. **Diferencia crítica en los datos**: A diferencia de OPP-RA, los criterios EUR-ACE son:
    - **Estándares externos fijos** (no editables por la institución)
    - **Jerárquicos y categorizados** (5.1.x, 5.2.x, 5.3.x...)
    - **Con descripciones extensas** que los coordinadores deben comprender
    - **Requeridos para cumplimiento regulatorio** (no opcionales)

12. **Base para demostración de calidad educativa**: Las relaciones RA-EURACE son la **evidencia objetiva** que demuestra que el programa de ingeniería cumple con estándares de calidad reconocidos internacionalmente. Son la prueba tangible de que los egresados desarrollan competencias al nivel requerido por EUR-ACE.

---

**CONCLUSIÓN:**

El AC1 es el más crítico porque sin él, **el sistema no puede cumplir su propósito fundamental de documentar la alineación con estándares EUR-ACE**, lo cual compromete directamente la **acreditación internacional del programa de ingeniería**. Es el único AC que valida el flujo completo de creación de evidencia auditable para evaluadores externos, y su fallo tiene consecuencias institucionales severas que van más allá de la gestión curricular interna, afectando el reconocimiento, prestigio y competitividad internacional del programa académico.

---

**FIN DEL ANÁLISIS** ✅