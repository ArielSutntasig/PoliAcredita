# **ANÁLISIS COMPLETO - HU: Visualizar Criterios EUR-ACE**

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **PASO 1: LISTA DE CONDICIONES Y ACCIONES**

#### **📋 CONDICIONES IDENTIFICADAS:**

**C1:** Usuario tiene rol de "miembro de la CEI" (Comité de Evaluación Interna) (**V** = Sí, **F** = No)

**C2:** Existen criterios EUR-ACE registrados en el sistema (**V** = Sí, **F** = No)

**C3:** Término de búsqueda ingresado coincide con algún criterio (**V** = Sí, **F** = No)

---

#### **⚙️ ACCIONES RESULTANTES:**

**A1:** Sistema muestra la pantalla "Criterios EUR-ACE" con el listado completo

**A2:** Sistema muestra mensaje de error "No tiene permisos para acceder a esta funcionalidad"

**A3:** Sistema muestra mensaje "No hay criterios EUR-ACE registrados en el sistema"

**A4:** Sistema filtra y muestra únicamente los criterios que coinciden con el término de búsqueda

**A5:** Sistema muestra mensaje "No se encontraron resultados para '[término buscado]'"

---

#### **📸 ANÁLISIS VISUAL DETALLADO DE LA IMAGEN 11:**

**Estructura de la pantalla "Criterios EUR-ACE":**

1. **Header/Navegación Superior:**
   - Logo "POLIACREDITA" (esquina superior izquierda)
   - Identificación de rol: "Coordinador de Carrera" (esquina superior derecha)
   - Íconos de configuración y perfil

2. **Menú Lateral (Sidebar):**
   - Ícono de inicio: "Inicio"
   - Ícono de capas: "Objetivos de Carrera"
   - Ícono de libro: "R. de Aprendizaje"
   - Ícono de documento: **"Criterios EUR-ACE"** (activo/seleccionado)
   - Ícono de configuración: "Editor Mapeos" (con dropdown expandible)
     - "RA vs OPP"
     - "RA vs EUR-ACE"
   - Ícono de usuario: "Mi Perfil"

3. **Título Principal:**
   - Texto: "Criterios EUR-ACE"
   - Tipografía: Grande, negrita

4. **Barra de Búsqueda:**
   - Ícono de lupa (🔍)
   - Placeholder: "Buscar por código o descripción..."
   - Ancho: Aproximadamente 50% del ancho de la pantalla
   - Posición: Debajo del título principal

5. **Tabla de Criterios:**
   - **Columna 1 - "Código":**
     - Códigos mostrados: 5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5
     - Formato: Numeración jerárquica (5.x.x)
     - Alineación: Izquierda
     - Ancho: Aproximadamente 15% del ancho de la tabla
   
   - **Columna 2 - "Descripción":**
     - Descripciones extensas de cada criterio (párrafos completos)
     - Ejemplos de texto:
       - 5.4.1: "La investigación en la solución de problemas complejos de ingeniería en el campo de estudio pertinente, incluyendo la formulación experimental, análisis e interpretación de datos utilizando conocimientos básicos y avanzados."
       - 5.4.2: "Creación, selección y aplicación de los recursos y métodos necesarios, incluyendo la predicción y la modelación, técnicas modernas y herramientas de TI para resolver problemas complejos de ingeniería en el campo de estudio pertinente, teniendo en cuenta las posibles restricciones"
     - Alineación: Izquierda
     - Ancho: Aproximadamente 85% del ancho de la tabla
     - Texto multilínea con wrap automático

6. **Paginación:**
   - Posición: Centro inferior de la pantalla
   - Controles: "< Previous  1  2  3  Next >"
   - Página actual: "1" (resaltada)
   - Páginas disponibles: 3 páginas totales
   - Flechas de navegación: "< Previous" y "Next >"

7. **Footer:**
   - Enlaces: "Navegación  Recursos  Legal"
   - Posición: Parte inferior de la pantalla

8. **Características Observadas:**
   - **NO hay botón de "Agregar" o "Nuevo Criterio"** (los criterios EUR-ACE son estándares fijos, no editables por la institución)
   - **NO hay columna de acciones** (editar/eliminar) - solo visualización
   - Los criterios son de **solo lectura**
   - Diseño limpio enfocado en consulta y referencia
   - Formato de tabla simple sin interacciones complejas

---

### **PASO 2: TABLA DE DECISIÓN COMPLETA (MAXIMIZADA)**

Con 3 condiciones, tenemos **2^3 = 8 reglas teóricas posibles**.

| **Regla** | **C1** | **C2** | **C3** | **Acciones** |
|-----------|--------|--------|--------|--------------|
| R1 | V | V | V | A1, A4 ✅ **BÚSQUEDA EXITOSA** |
| R2 | V | V | F | A1, A5 |
| R3 | V | F | V | A3 |
| R4 | V | F | F | A3 |
| R5 | F | V | V | A2 |
| R6 | F | V | F | A2 |
| R7 | F | F | V | A2 |
| R8 | F | F | F | A2 |

---

### **PASO 3: TABLA DE DECISIÓN MINIMIZADA**

#### **Análisis de Minimización:**

**Grupo 1 - Sin permisos (C1=F):**
Las reglas R5-R8 (4 reglas) producen la acción A2 independientemente de C2 y C3.
**→ Se fusionan en R_MIN1**

**Grupo 2 - Sin criterios EUR-ACE en el sistema (C1=V, C2=F):**
Las reglas R3-R4 (2 reglas) producen la acción A3 independientemente de C3.
Nota: Si no hay criterios, C3 es irrelevante (no hay nada que buscar).
**→ Se fusionan en R_MIN2**

**Reglas únicas:**
- **R1** (Búsqueda exitosa): C1=V, C2=V, C3=V → Búsqueda con resultados
- **R2** (Búsqueda sin resultados): C1=V, C2=V, C3=F → Búsqueda sin coincidencias

Sin embargo, necesito considerar el **caso de listado sin búsqueda** (usuario solo visualiza todos los criterios sin filtrar). Este es el happy path principal.

**Refinamiento:** La condición C3 solo aplica cuando el usuario **activamente realiza una búsqueda**. Necesito reformular:

**Condiciones reformuladas:**
- **C1:** Usuario tiene rol de miembro CEI (V/F)
- **C2:** Existen criterios EUR-ACE en el sistema (V/F)
- **C3:** Usuario ha ingresado un término de búsqueda (V/F)
- **C4:** Si C3=V, el término coincide con algún criterio (V/F)

Esto da 2^4 = 16 reglas, pero puedo optimizar directamente en la tabla minimizada:

#### **🎯 TABLA MINIMIZADA FINAL:**

| **Regla** | **C1** | **C2** | **C3** | **Acciones** | **Descripción** |
|-----------|--------|--------|--------|--------------|-----------------|
| **R_MIN1** | **F** | **-** | **-** | **A2** | Usuario sin permisos CEI |
| **R_MIN2** | **V** | **F** | **-** | **A3** | No hay criterios EUR-ACE |
| **R_MIN3** ✅ | **V** | **V** | **No búsqueda** | **A1** | **Listado completo (Happy Path)** |
| **R_MIN4** | **V** | **V** | **Búsqueda sin resultados** | **A1, A5** | Búsqueda sin coincidencias |
| **R_MIN5** | **V** | **V** | **Búsqueda con resultados** | **A1, A4** | Búsqueda exitosa |

**Reducción: De 8 reglas originales → 5 reglas (37.5% de reducción)**

---

### **PASO 4: NÚMERO TOTAL DE CRITERIOS DE ACEPTACIÓN**

**Número final: 5 Criterios de Aceptación**

#### **Justificación:**

✅ **Se mantienen los 5 AC derivados de la tabla minimizada** porque cada uno valida un escenario único:

1. **R_MIN1**: Validación de seguridad/permisos (específico para rol CEI)
2. **R_MIN2**: Validación de estado del sistema (sin datos)
3. **R_MIN3**: Visualización completa del listado de criterios EUR-ACE (CRÍTICO - Happy Path principal)
4. **R_MIN4**: Funcionalidad de búsqueda sin resultados
5. **R_MIN5**: Funcionalidad de búsqueda con resultados

❌ **No se eliminan criterios** porque:
- Esta HU es específica para **criterios EUR-ACE** (datos diferentes a OPP o RA)
- El **rol autorizado es diferente**: "miembro de la CEI" (no Coordinador de Carrera)
- Los **criterios EUR-ACE son estándares fijos** de acreditación europea (no editables)
- El **propósito es diferente**: consulta de estándares de acreditación para evaluación
- Aunque el patrón de visualización es similar a otras HUs de listado, los **datos y contexto son únicos**

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (FORMATO GHERKIN)**

### **AC1 - Visualización completa del listado de Criterios EUR-ACE (HAPPY PATH)**

**Dado que** soy un miembro autenticado del Comité de Evaluación Interna (CEI)

**Y** existen criterios EUR-ACE registrados en el sistema

**Cuando** accedo a la funcionalidad "Criterios EUR-ACE" desde el menú lateral

**Entonces** se muestra la pantalla con el título "Criterios EUR-ACE"

**Y** se muestra un campo de búsqueda con el placeholder "Buscar por código o descripción..."

**Y** se muestra una tabla con dos columnas: "Código" y "Descripción"

**Y** la columna "Código" muestra los códigos de los criterios EUR-ACE en formato jerárquico (ejemplo: 5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5)

**Y** la columna "Descripción" muestra el texto completo de cada criterio EUR-ACE con wrap automático para descripciones extensas

**Y** se muestran ejemplos de criterios como:
   - "5.4.1: La investigación en la solución de problemas complejos de ingeniería en el campo de estudio pertinente, incluyendo la formulación experimental, análisis e interpretación de datos utilizando conocimientos básicos y avanzados."
   - "5.4.2: Creación, selección y aplicación de los recursos y métodos necesarios, incluyendo la predicción y la modelación, técnicas modernas y herramientas de TI para resolver problemas complejos de ingeniería en el campo de estudio pertinente, teniendo en cuenta las posibles restricciones"

**Y** se muestra la paginación en la parte inferior con formato "< Previous  1  2  3  Next >"

**Y** la página actual (página 1) está resaltada visualmente

**Y** se muestran múltiples páginas indicando que hay más criterios disponibles

**Y** **NO se muestra ningún botón de "Agregar", "Editar" o "Eliminar"** porque los criterios EUR-ACE son estándares fijos de acreditación

**Y** el listado se presenta en formato de solo lectura para consulta.

---

### **AC2 - Intento de acceso sin permisos de miembro CEI**

**Dado que** estoy autenticado en el sistema

**Y** NO tengo asignado el rol de "miembro de la CEI" (Comité de Evaluación Interna)

**Y** tengo un rol diferente como "Coordinador de Carrera", "Profesor" u otro

**Cuando** intento acceder a la opción "Criterios EUR-ACE" del menú lateral

**O** intento acceder directamente a la URL de la funcionalidad de criterios EUR-ACE

**Entonces** el sistema me redirige a la pantalla de inicio o dashboard

**Y** se muestra un mensaje de error "No tiene permisos para acceder a esta funcionalidad"

**Y** NO puedo visualizar el listado de criterios EUR-ACE

**Y** la opción "Criterios EUR-ACE" en el menú lateral puede estar oculta o deshabilitada visualmente.

---

### **AC3 - Visualización cuando no existen criterios EUR-ACE registrados**

**Dado que** soy un miembro autenticado del Comité de Evaluación Interna (CEI)

**Y** NO existen criterios EUR-ACE registrados en el sistema (base de datos vacía o en proceso de configuración inicial)

**Cuando** accedo a la funcionalidad "Criterios EUR-ACE"

**Entonces** se muestra la pantalla con el título "Criterios EUR-ACE"

**Y** se muestra el campo de búsqueda vacío

**Y** se muestra un mensaje informativo "No hay criterios EUR-ACE registrados en el sistema"

**Y** la tabla de criterios está vacía sin registros

**Y** NO se muestra la paginación

**Y** se sugiere contactar al administrador del sistema para cargar los estándares EUR-ACE.

---

### **AC4 - Búsqueda de criterios EUR-ACE sin resultados**

**Dado que** soy un miembro autenticado del Comité de Evaluación Interna (CEI)

**Y** estoy visualizando el listado de criterios EUR-ACE

**Y** existen criterios registrados en el sistema

**Cuando** ingreso un término de búsqueda en el campo "Buscar por código o descripción..."

**Y** el término no coincide con ningún código o texto de descripción de los criterios EUR-ACE

**Ejemplo:** ingreso "metodología ágil" pero ningún criterio EUR-ACE contiene ese texto

**Entonces** la tabla se actualiza dinámicamente

**Y** NO se muestran registros en la tabla

**Y** se muestra un mensaje "No se encontraron resultados para 'metodología ágil'"

**Y** puedo borrar el término de búsqueda para volver a visualizar el listado completo

**Y** la paginación desaparece si no hay resultados.

---

### **AC5 - Búsqueda exitosa de criterios EUR-ACE**

**Dado que** soy un miembro autenticado del Comité de Evaluación Interna (CEI)

**Y** estoy visualizando el listado de criterios EUR-ACE

**Y** existen criterios registrados en el sistema

**Cuando** ingreso un término de búsqueda en el campo "Buscar por código o descripción..."

**Y** el término coincide con uno o más códigos o descripciones de criterios EUR-ACE

**Ejemplo 1:** ingreso "5.4.1" y coincide con el código exacto

**Ejemplo 2:** ingreso "investigación" y coincide con múltiples descripciones que contienen esa palabra

**Entonces** la tabla se actualiza dinámicamente mostrando únicamente los criterios que coinciden con el término

**Y** se resalta visualmente el término buscado en los resultados (opcional)

**Y** se muestra el número de resultados encontrados

**Y** si los resultados requieren paginación, se actualiza la paginación para reflejar solo las páginas de resultados filtrados

**Y** cada resultado muestra el código completo y la descripción completa del criterio

**Y** puedo borrar el término de búsqueda para volver a visualizar el listado completo sin filtros.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **🎯 CRITERIO MÁS CRÍTICO:**

**AC1 - Visualización completa del listado de Criterios EUR-ACE (HAPPY PATH)**

---

### **✅ JUSTIFICACIÓN DE CRITICIDAD:**

1. **Propósito central de la HU**: Este AC valida directamente el objetivo principal expresado en la Historia de Usuario: "**listar los Criterios EUR-ACE Para consultar y gestionar los estándares de acreditación**". Sin este AC funcionando, la HU no cumple su razón de existir.

2. **Funcionalidad base para acreditación internacional**: Los criterios EUR-ACE son **estándares obligatorios** para acreditación de programas de ingeniería en Europa y a nivel internacional. Los miembros del CEI necesitan consultar estos criterios constantemente para:
   - Evaluar si el programa cumple con los estándares EUR-ACE
   - Preparar documentación de autoevaluación
   - Identificar brechas de cumplimiento
   - Planificar mejoras curriculares para alineación con estándares
   - Preparar evidencias para auditorías externas

3. **Rol crítico del CEI**: El Comité de Evaluación Interna (CEI) es el responsable institucional de:
   - Liderar procesos de autoevaluación para acreditación
   - Verificar cumplimiento de estándares de calidad
   - Coordinar preparación de informes de acreditación
   - Identificar oportunidades de mejora continua
   
   Sin acceso visual a los criterios EUR-ACE, el CEI no puede ejecutar ninguna de estas responsabilidades.

4. **Prerequisito para otras funcionalidades**: Este AC es prerequisito para:
   - La funcionalidad de mapeo RA vs EUR-ACE (no puedes mapear si no puedes ver los criterios)
   - Generación de reportes de cumplimiento EUR-ACE
   - Análisis de cobertura de criterios EUR-ACE en el programa
   - Identificación de criterios sin mapear

5. **Criterios EUR-ACE como referencia constante**: A diferencia de OPPs o RAs (que son específicos de cada institución), los **criterios EUR-ACE son estándares externos fijos** que el CEI debe consultar repetidamente durante todo el ciclo de acreditación. Este AC valida el acceso a esta referencia crítica.

6. **Complejidad de los criterios EUR-ACE**: Los criterios son textos extensos y técnicos (como se observa en la imagen 11) que requieren una presentación clara:
   - Códigos jerárquicos (5.4.1, 5.4.2, etc.)
   - Descripciones de varios párrafos
   - Agrupación por categorías (5.4.x, 5.5.x, etc.)
   
   Este AC valida que toda esta información compleja se presenta de forma legible y consultable.

7. **Evidencia visual directa**: La imagen 11 muestra explícitamente el listado de criterios EUR-ACE, lo que indica que fue el caso de uso principal diseñado por el equipo de producto. El diseño enfocado en visualización (sin botones de edición) refuerza que la consulta es la funcionalidad core.

8. **Impacto en proceso de acreditación**: Sin este AC funcionando:
   - El CEI no puede consultar los estándares que debe evaluar
   - No se puede realizar autoevaluación contra EUR-ACE
   - No se puede preparar documentación de acreditación
   - Se pone en riesgo todo el proceso de acreditación internacional

9. **Formato de solo lectura crítico**: Este AC valida que los criterios EUR-ACE se presentan en **formato de solo lectura**, lo cual es correcto porque son estándares externos que la institución NO debe modificar. Cualquier error aquí (permitir edición accidental) comprometería la integridad de los estándares.

10. **Base para trazabilidad de cumplimiento**: El listado de criterios EUR-ACE es el punto de partida para crear la **matriz de trazabilidad** que demuestra cómo el programa de ingeniería cumple cada criterio. Sin visualización clara de los criterios, no se puede construir esta matriz fundamental para acreditación.

11. **Paginación para múltiples criterios**: El AC valida que el sistema maneja correctamente la paginación de los 50+ criterios EUR-ACE existentes, presentándolos de forma organizada y navegable (páginas 1, 2, 3 como se ve en la imagen 11).

12. **Búsqueda como funcionalidad secundaria**: Aunque los AC4 y AC5 validan la búsqueda, el **AC1 es más crítico** porque la búsqueda solo es útil si primero funciona el listado base. La mayoría de usuarios del CEI primero navegarán el listado completo para familiarizarse con todos los criterios antes de usar búsqueda específica.

---

**CONCLUSIÓN:**

El **AC1 es absolutamente crítico** porque valida la funcionalidad central que permite al Comité de Evaluación Interna consultar los estándares EUR-ACE, lo cual es **prerequisito fundamental** para todo el proceso de acreditación internacional del programa de ingeniería. Sin este AC funcionando, el CEI no puede cumplir su responsabilidad de evaluar y demostrar cumplimiento de estándares de calidad europeos, poniendo en riesgo la acreditación internacional del programa.

---

**FIN DEL ANÁLISIS** ✅