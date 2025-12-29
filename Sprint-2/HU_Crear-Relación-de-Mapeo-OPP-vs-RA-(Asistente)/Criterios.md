# **ANÁLISIS COMPLETO - HU: Crear Relación de Mapeo OPP vs RA (Asistente)**

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **PASO 1: LISTA DE CONDICIONES Y ACCIONES**

#### **📋 CONDICIONES IDENTIFICADAS (del análisis visual de imágenes 12-16):**

**C1:** Usuario tiene rol de Coordinador de Carrera (**V** = Sí, **F** = No)

**C2:** OPP seleccionado existe en el sistema (**V** = Sí, **F** = No)

**C3:** RA seleccionado existe en el sistema (**V** = Sí, **F** = No)

**C4:** Campo "Justificación" está completo (**V** = Sí, **F** = No)

**C5:** La relación OPP-RA ya existe en la matriz (**V** = Sí, **F** = No)

---

#### **⚙️ ACCIONES RESULTANTES (observadas en las imágenes del prototipo):**

**A1:** Sistema permite acceso al wizard de creación de relación OPP-RA

**A2:** Sistema muestra mensaje de error "No tiene permisos para realizar esta acción"

**A3:** Sistema permite avanzar al Paso 2 (Seleccionar RA) y muestra la sección "Elementos Seleccionado:" con el OPP

**A4:** Sistema muestra mensaje "Debe seleccionar un Objetivo de Carrera"

**A5:** Sistema permite avanzar al Paso 3 (Justificar) y muestra ambos elementos en "Elementos Seleccionado:"

**A6:** Sistema muestra mensaje "Debe seleccionar un Resultado de Aprendizaje"

**A7:** Sistema guarda la relación, cierra el wizard, muestra notificación "Completado - Se agregó la relación correctamente" y actualiza la matriz con checkmark verde

**A8:** Sistema muestra mensaje "Debe completar el campo de justificación"

**A9:** Sistema muestra mensaje "Esta relación ya existe entre el OPP y el RA seleccionados"

---

#### **📸 COMPONENTES DE UI OBSERVADOS EN LAS IMÁGENES:**

**Imagen 12 - Matriz OPP vs RA:**
- Título: "Matriz: Objetivos de Carrera (OPP) y Resultados de aprendizaje (RA)"
- Subtítulo: "La tabla muestra la relación entre los objetivos de carrera (perfil profesional) y los resultados de aprendizaje (perfil de egreso) de una carrera."
- Botón azul: "+ Nueva Relación" (esquina superior derecha)
- Eje vertical (filas): Objetivos de Carrera con códigos OPP1-OPP7 en celdas azules
- Eje horizontal (columnas): Resultados de Aprendizaje con códigos RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6, RE7
- Checkmarks verdes (✓) en intersecciones donde existe relación
- Íconos de información (ℹ️) en encabezados

**Imagen 13 - Wizard Paso 1:**
- Indicadores de pasos: "1" (activo en círculo azul), "2" (gris), "3" (gris)
- Etiquetas: "Seleccionar Objetivos de carrera (OPP)", "Seleccionar Resultados de Aprendizaje (RA)", "Justificar Relación"
- Líneas conectoras entre pasos
- Campo de búsqueda: "Buscar por código o descripción..."
- Tabla con columnas: "Código" y "Descripción"
- Filas con OPPs: OPP1-OPP5 visibles
- Paginación: "< Previous  1  2  3  Next >"
- Botones: "Cancelar" (rojo) y "Guardar" (azul) en la parte inferior

**Imagen 14 - Wizard Paso 2:**
- Indicadores: "1" (✓ verde), "2" (activo en círculo azul), "3" (gris)
- **Sección destacada: "Elementos Seleccionado:"**
- **Muestra: "Objetivo de Carrera:" seguido del código y descripción completa del OPP seleccionado**
- Dropdown: "Tipo de Aprendizaje" (para filtrar RG/RE)
- Tabla con RAs (códigos RG1, RG2, RG3, RG4, RG5 visibles)
- Mismos botones "Cancelar" y "Guardar"

**Imagen 15 - Wizard Paso 3:**
- Indicadores: "1" (✓), "2" (✓), "3" (activo en círculo azul)
- **Sección "Elementos Seleccionado:" expandida:**
  - **"Objetivo de Carrera:" con texto completo**
  - **"Resultado de aprendizaje de carrera:" con texto completo**
- Título: "Justifique la relación de OP vs RA"
- Subtítulo: "Justificación:"
- Campo de texto grande con placeholder: "Escribe tu justificación detallada aquí para la relación entre el Objetivo de Carrera y el Resultado de Aprendizaje seleccionados."
- Botones "Cancelar" (rojo) y "Guardar" (azul)

**Imagen 16 - Notificación de éxito:**
- Matriz OPP vs RA visible
- Notificación emergente (esquina superior derecha): 
  - Ícono de check verde (✓)
  - Título: "Completado"
  - Mensaje: "Se agregó la relación correctamente"
  - Botón "X" para cerrar
- Nueva celda verde con checkmark visible en la matriz

---

### **PASO 2: TABLA DE DECISIÓN COMPLETA (MAXIMIZADA)**

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

### **PASO 3: TABLA DE DECISIÓN MINIMIZADA**

#### **Análisis de Minimización:**

**Grupo 1 - Sin permisos (C1=F):**
Las reglas R17-R32 (16 reglas) producen la misma acción A2 independientemente de los valores de C2, C3, C4 y C5.
**→ Se fusionan en R_MIN1**

**Grupo 2 - OPP no seleccionado (C1=V, C2=F):**
Las reglas R9-R16 (8 reglas) producen las acciones A1, A4 independientemente de C3, C4 y C5.
**→ Se fusionan en R_MIN2**

**Grupo 3 - RA no seleccionado (C1=V, C2=V, C3=F):**
Las reglas R5-R8 (4 reglas) producen las acciones A1, A3, A6 independientemente de C4 y C5.
**→ Se fusionan en R_MIN3**

**Grupo 4 - Justificación vacía (C1=V, C2=V, C3=V, C4=F):**
Las reglas R3-R4 (2 reglas) producen las acciones A1, A3, A5, A8 independientemente de C5.
**→ Se fusionan en R_MIN4**

**Reglas únicas:**
- **R1** (Happy Path): C1=V, C2=V, C3=V, C4=V, C5=F → Éxito total
- **R2** (Relación duplicada): C1=V, C2=V, C3=V, C4=V, C5=V → Error de duplicación

#### **🎯 TABLA MINIMIZADA FINAL:**

| **Regla** | **C1** | **C2** | **C3** | **C4** | **C5** | **Acciones** | **Descripción** |
|-----------|--------|--------|--------|--------|--------|--------------|-----------------|
| **R_MIN1** | **F** | **-** | **-** | **-** | **-** | **A2** | Usuario sin permisos |
| **R_MIN2** | **V** | **F** | **-** | **-** | **-** | **A1, A4** | OPP no seleccionado |
| **R_MIN3** | **V** | **V** | **F** | **-** | **-** | **A1, A3, A6** | RA no seleccionado |
| **R_MIN4** | **V** | **V** | **V** | **F** | **-** | **A1, A3, A5, A8** | Justificación vacía |
| **R_MIN5** | **V** | **V** | **V** | **V** | **V** | **A1, A3, A5, A9** | Relación duplicada |
| **R_MIN6** ✅ | **V** | **V** | **V** | **V** | **F** | **A1, A3, A5, A7** | **HAPPY PATH** |

**Reducción: De 32 reglas → 6 reglas (81.25% de reducción)**

---

### **PASO 4: NÚMERO TOTAL DE CRITERIOS DE ACEPTACIÓN**

**Número final: 6 Criterios de Aceptación**

#### **Justificación:**

✅ **Se mantienen los 6 AC derivados de la tabla minimizada** porque cada uno valida un escenario único:

1. **R_MIN1**: Validación de seguridad/permisos
2. **R_MIN2**: Validación obligatoria en Paso 1 del wizard
3. **R_MIN3**: Validación obligatoria en Paso 2 del wizard
4. **R_MIN4**: Validación obligatoria en Paso 3 del wizard
5. **R_MIN5**: Validación de regla de negocio (unicidad)
6. **R_MIN6**: Flujo exitoso completo (CRÍTICO)

❌ **No se eliminan criterios** porque:
- Cada criterio valida comportamientos distintos del wizard
- No hay redundancia con otras HUs aunque el patrón sea similar
- Las entidades (OPP, RA) y el propósito (alineación curricular) son específicos de esta HU
- Los datos de entrada son diferentes a otras HUs del sistema

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (FORMATO GHERKIN)**

### **AC1 - Creación exitosa de relación OPP-RA mediante wizard (HAPPY PATH)**

**Dado que** soy un Coordinador de Carrera autenticado en el sistema

**Y** estoy en la pantalla "Matriz: Objetivos de Carrera (OPP) y Resultados de aprendizaje (RA)"

**Cuando** hago clic en el botón "+ Nueva Relación"

**Entonces** se abre el wizard de creación con 3 pasos visibles en la parte superior

**Y** el paso 1 "Seleccionar Objetivos de carrera (OPP)" está activo con círculo azul resaltado

**Y** los pasos 2 "Seleccionar Resultados de Aprendizaje (RA)" y 3 "Justificar Relación" están visibles pero inactivos en color gris

**Y** se muestra una línea conectora entre los 3 pasos

**Y** se presenta una tabla con columnas "Código" y "Descripción"

**Y** se muestra un campo de búsqueda con placeholder "Buscar por código o descripción..."

**Y** se muestran los botones "Cancelar" (color rojo) y "Guardar" (color azul) en la parte inferior.

**Cuando** selecciono un Objetivo de Carrera (ejemplo: OPP3 "Aplicar metodologías ágiles en la gestión de proyectos de software")

**Entonces** el sistema avanza automáticamente al paso 2

**Y** el indicador del paso 1 muestra un checkmark verde (✓)

**Y** el paso 2 "Seleccionar Resultados de Aprendizaje (RA)" está activo con círculo azul

**Y** se muestra la sección "Elementos Seleccionado:" en la parte superior de la pantalla

**Y** debajo aparece "Objetivo de Carrera:" seguido del código y descripción completa del OPP seleccionado

**Y** se presenta un dropdown "Tipo de Aprendizaje" para filtrar entre RG y RE

**Y** se muestra una tabla con los RAs disponibles.

**Cuando** selecciono un Resultado de Aprendizaje (ejemplo: RG3 "Aplicar metodologías ágiles en la gestión de proyectos de software")

**Entonces** el sistema avanza automáticamente al paso 3

**Y** el indicador del paso 2 muestra un checkmark verde (✓)

**Y** el paso 3 "Justificar Relación" está activo con círculo azul

**Y** la sección "Elementos Seleccionado:" se actualiza mostrando ambos elementos:
   - "Objetivo de Carrera:" con su código y descripción
   - "Resultado de aprendizaje de carrera:" con su código y descripción

**Y** se muestra el título "Justifique la relación de OP vs RA"

**Y** se presenta la etiqueta "Justificación:"

**Y** se muestra un campo de texto multilínea con placeholder "Escribe tu justificación detallada aquí para la relación entre el Objetivo de Carrera y el Resultado de Aprendizaje seleccionados."

**Cuando** escribo una justificación válida en el campo de texto (mínimo 10 caracteres)

**Y** hago clic en el botón "Guardar"

**Entonces** el wizard se cierra

**Y** regreso a la vista de la matriz "Objetivos de Carrera (OPP) y Resultados de aprendizaje (RA)"

**Y** se muestra una notificación emergente en la esquina superior derecha con:
   - Ícono de check verde (✓)
   - Título "Completado"
   - Mensaje "Se agregó la relación correctamente"
   - Botón "X" para cerrar la notificación

**Y** en la matriz se visualiza un checkmark verde (✓) en la celda de intersección entre el OPP3 y RG3 seleccionados

**Y** la matriz se actualiza sin necesidad de recargar toda la página.

---

### **AC2 - Intento de acceso sin permisos de Coordinador de Carrera**

**Dado que** estoy autenticado en el sistema

**Y** NO tengo asignado el rol de "Coordinador de Carrera"

**Cuando** intento acceder a la funcionalidad "Editor Mapeos" desde el menú lateral

**O** intento acceder directamente a la URL de la matriz OPP vs RA

**Entonces** el sistema me redirige a la pantalla de inicio o dashboard

**Y** se muestra un mensaje de error "No tiene permisos para realizar esta acción"

**Y** NO puedo visualizar la matriz OPP vs RA

**Y** NO puedo acceder al botón "+ Nueva Relación"

**Y** NO puedo abrir el wizard de creación de relaciones.

---

### **AC3 - Validación de Paso 1: Intento de avanzar sin seleccionar OPP**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** he abierto el wizard haciendo clic en "+ Nueva Relación"

**Y** estoy en el paso 1 "Seleccionar Objetivos de carrera (OPP)"

**Cuando** intento avanzar al paso 2 sin haber seleccionado ningún Objetivo de Carrera

**O** hago clic directamente en el indicador del paso 2

**Entonces** el sistema muestra un mensaje de validación "Debe seleccionar un Objetivo de Carrera"

**Y** permanezco en el paso 1

**Y** el indicador del paso 2 permanece inactivo (color gris)

**Y** NO se permite la navegación al paso 2

**Y** la tabla de OPPs permanece visible para que pueda realizar la selección.

---

### **AC4 - Validación de Paso 2: Intento de avanzar sin seleccionar RA**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** he completado el paso 1 seleccionando un OPP

**Y** estoy en el paso 2 "Seleccionar Resultados de Aprendizaje (RA)"

**Y** la sección "Elementos Seleccionado:" muestra el OPP seleccionado

**Cuando** intento avanzar al paso 3 sin haber seleccionado ningún Resultado de Aprendizaje

**O** hago clic directamente en el indicador del paso 3

**Entonces** el sistema muestra un mensaje de validación "Debe seleccionar un Resultado de Aprendizaje"

**Y** permanezco en el paso 2

**Y** el indicador del paso 3 permanece inactivo (color gris)

**Y** NO se permite la navegación al paso 3

**Y** la tabla de RAs permanece visible para que pueda realizar la selección

**Y** el OPP previamente seleccionado se mantiene visible en "Elementos Seleccionado:".

---

### **AC5 - Validación de Paso 3: Intento de guardar sin completar justificación**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** he completado los pasos 1 y 2 seleccionando un OPP y un RA

**Y** estoy en el paso 3 "Justificar Relación"

**Y** la sección "Elementos Seleccionado:" muestra tanto el OPP como el RA seleccionados

**Cuando** dejo el campo "Justificación:" completamente vacío

**Y** hago clic en el botón "Guardar"

**Entonces** el sistema muestra un mensaje de validación "Debe completar el campo de justificación"

**Y** el botón "Guardar" NO ejecuta la acción de guardado

**Y** permanezco en el paso 3 con el wizard abierto

**Y** el campo "Justificación:" se resalta visualmente (borde rojo o indicador de error)

**Y** NO se cierra el wizard

**Y** NO se crea la relación en la matriz

**Y** ambos elementos seleccionados permanecen visibles para referencia.

---

### **AC6 - Validación de unicidad: Intento de crear relación duplicada**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** ya existe una relación entre OPP3 y RG3 en la matriz (visible con checkmark verde)

**Cuando** abro el wizard haciendo clic en "+ Nueva Relación"

**Y** selecciono el mismo OPP3 en el paso 1

**Y** selecciono el mismo RG3 en el paso 2

**Y** completo el campo de justificación en el paso 3

**Y** hago clic en el botón "Guardar"

**Entonces** el sistema muestra un mensaje de error "Esta relación ya existe entre el OPP y el RA seleccionados"

**Y** NO se crea una segunda relación duplicada en la base de datos

**Y** la matriz NO muestra un segundo checkmark en la misma celda

**Y** el wizard permanece abierto en el paso 3

**Y** puedo hacer clic en "Cancelar" para cerrar el wizard

**O** puedo navegar hacia atrás a los pasos 1 y 2 para modificar mi selección

**Y** los indicadores de pasos completados (✓) se mantienen visibles para permitir navegación hacia atrás.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **🎯 CRITERIO MÁS CRÍTICO:**

**AC1 - Creación exitosa de relación OPP-RA mediante wizard (HAPPY PATH)**

---

### **✅ JUSTIFICACIÓN DE CRITICIDAD:**

1. **Valor central de la Historia de Usuario**: Este AC es el único que valida el **propósito principal completo** expresado en la HU: "establecer nuevas relaciones entre Objetivos de Programa y Resultados de Aprendizaje con una justificación, usando un asistente paso a paso (WIZZARD) Para documentar la alineación curricular de forma guiada y eficiente."

2. **Validación del patrón wizard completo**: Este criterio es el único que prueba los **3 pasos secuenciales del asistente guiado**:
   - Paso 1: Selección de OPP con búsqueda y tabla
   - Paso 2: Selección de RA con filtrado por tipo y contexto persistente
   - Paso 3: Justificación académica con visualización de ambos elementos
   
   Los AC2-AC6 solo validan casos de error, pero no prueban que el flujo completo funcione.

3. **Persistencia de contexto ("Elementos Seleccionado:")**: Este AC valida una característica crítica del diseño del wizard observada en las imágenes 14 y 15: la sección "Elementos Seleccionado:" que permite al usuario siempre ver qué OPP y RA está relacionando. Esta funcionalidad reduce errores y mejora la experiencia del usuario al documentar alineación curricular.

4. **Integración de múltiples componentes**: El AC1 prueba la integración funcional de:
   - Sistema de navegación del wizard (indicadores, estados, transiciones)
   - Tablas de datos (OPPs, RAs)
   - Filtros y búsquedas
   - Formulario de justificación
   - Validación y guardado
   - Actualización asíncrona de la matriz
   - Sistema de notificaciones

5. **Alineación curricular institucional**: Sin este AC funcionando, **no se puede documentar la alineación curricular**, que es el objetivo estratégico de la funcionalidad. La alineación curricular es fundamental para:
   - Diseño coherente del plan de estudios
   - Demostración de que los OPPs del perfil profesional se logran mediante los RAs del perfil de egreso
   - Preparación para procesos de acreditación
   - Revisión y mejora curricular continua

6. **Evidencia visual directa**: Las imágenes 13, 14, 15 y 16 muestran **explícitamente el flujo completo del happy path**, lo que indica que fue el caso de uso principal diseñado por el equipo de producto. Los diseñadores invirtieron esfuerzo en documentar este flujo específico.

7. **Experiencia de usuario diferenciadora**: El uso de un wizard en lugar de un formulario tradicional es una **decisión estratégica de UX** mencionada explícitamente en la HU ("WIZZARD"). Este AC valida que el patrón wizard efectivamente:
   - Reduce complejidad cognitiva (un paso a la vez)
   - Guía al usuario secuencialmente
   - Previene errores mostrando contexto persistente
   - Facilita la tarea de documentar alineación curricular

8. **Complejidad técnica mayor**: Este escenario requiere:
   - Gestión de estado del wizard entre 3 pasos
   - Navegación condicional (solo avanza si hay selección)
   - Actualización de UI reactiva (indicadores, secciones)
   - 3 llamadas al backend (cargar OPPs, cargar RAs, guardar relación)
   - Actualización optimista de la matriz
   - Manejo de transacciones (rollback si falla el guardado)

9. **Impacto en coordinadores de carrera**: Los coordinadores usan esta funcionalidad para una tarea estratégica: **mapear el perfil profesional (OPPs) contra el perfil de egreso (RAs)**. Si el happy path falla, los coordinadores no pueden cumplir con una de sus responsabilidades principales, afectando la calidad del programa académico.

10. **Prerequisito para testing exhaustivo**: Sin validar primero que el flujo happy path funciona correctamente, **no tiene sentido probar los casos de error** (AC2-AC6), ya que no habría una línea base funcional contra la cual comparar el comportamiento de error.

11. **Actualización de matriz sin recarga**: El AC1 valida la funcionalidad crítica observada en la imagen 16: la matriz se actualiza **sin necesidad de recargar la página completa**, mostrando inmediatamente el nuevo checkmark verde. Esto es crucial para la eficiencia del proceso de documentación de múltiples relaciones.

12. **Justificación académica como evidencia auditable**: Este AC valida que el sistema captura la **justificación académica** que explica por qué un OPP específico se relaciona con un RA específico. Esta justificación es evidencia fundamental en procesos de:
   - Revisión curricular interna
   - Auditorías de calidad educativa
   - Procesos de acreditación nacional/internacional
   - Evaluación de coherencia del diseño curricular

---

**CONCLUSIÓN:**

El **AC1 es absolutamente crítico** porque es el único que valida el **valor completo de la Historia de Usuario**: la capacidad de los coordinadores de carrera de documentar la alineación curricular de forma guiada y eficiente mediante un wizard de 3 pasos con contexto persistente. Sin este AC funcionando, el sistema no cumple su propósito fundamental, y los coordinadores no pueden ejecutar una de sus responsabilidades estratégicas más importantes: demostrar la coherencia entre el perfil profesional y el perfil de egreso del programa académico.

---

**FIN DEL ANÁLISIS** ✅