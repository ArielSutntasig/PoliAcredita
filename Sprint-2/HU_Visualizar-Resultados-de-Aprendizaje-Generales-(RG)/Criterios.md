# **ANÁLISIS COMPLETO - HU: Visualizar Resultados de Aprendizaje Generales (RG)**

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **PASO 1: LISTA DE CONDICIONES Y ACCIONES**

#### **📋 CONDICIONES IDENTIFICADAS:**

**C1:** Usuario tiene rol de "Coordinador de Carrera" (**V** = Sí, **F** = No)

**C2:** Existen Resultados de Aprendizaje Generales (RG) registrados en la carrera (**V** = Sí, **F** = No)

**C3:** Término de búsqueda ingresado coincide con algún RG (**V** = Sí, **F** = No)

---

#### **⚙️ ACCIONES RESULTANTES:**

**A1:** Sistema muestra la pantalla "Gestión de Resultados de Aprendizaje (RA)" con la tab "Resultados Generales (RG)" activa

**A2:** Sistema muestra mensaje de error "No tiene permisos para acceder a esta funcionalidad"

**A3:** Sistema muestra mensaje "No hay Resultados de Aprendizaje Generales registrados para esta carrera"

**A4:** Sistema filtra y muestra únicamente los RG que coinciden con el término de búsqueda

**A5:** Sistema muestra mensaje "No se encontraron resultados para '[término buscado]'"

---

#### **📸 ANÁLISIS VISUAL DETALLADO DE LA IMAGEN 9:**

**Estructura de la pantalla "Gestión de Resultados de Aprendizaje (RA)":**

1. **Header/Navegación Superior:**
   - Logo "POLIACREDITA" (esquina superior izquierda)
   - Identificación de rol: "Coordinador de Carrera" (esquina superior derecha)
   - Íconos de configuración, notificaciones y perfil de usuario

2. **Menú Lateral (Sidebar):**
   - Ícono de inicio: "Inicio"
   - Ícono de capas: "Objetivos de Carrera"
   - Ícono de libro: **"R. de Aprendizaje"** (activo/seleccionado)
   - Ícono de documento: "Criterios EUR-ACE"
   - Ícono de configuración: "Editor Mapeos" (con dropdown)
     - "RA vs OPP"
     - "RA vs EUR-ACE"
   - Sección "Configuración" expandida con:
     - "Usuarios"
     - "Roles"
   - Ícono de usuario: "Mi Perfil"

3. **Título Principal:**
   - Texto: "Gestión de Resultados de Aprendizaje (RA)"
   - Tipografía: Grande, negrita, color negro

4. **Sistema de Tabs (Pestañas):**
   - **Tab 1:** "Resultados Generales (RG)" (ACTIVA, subrayada en azul)
   - **Tab 2:** "Resultados Específicos (RE)" (inactiva, color gris)
   - Indicador visual: Línea azul gruesa debajo de la tab activa

5. **Barra de Búsqueda:**
   - Ícono de lupa (🔍) a la izquierda
   - Placeholder: "Buscar por código o descripción..."
   - Ancho: Aproximadamente 50% del ancho de la pantalla
   - Posición: Debajo de las tabs, lado izquierdo

6. **Botón de Acción Principal:**
   - Texto: "+ Nuevo RA"
   - Color: Azul oscuro (fondo), texto blanco
   - Posición: Esquina superior derecha, alineado con la barra de búsqueda
   - Tamaño: Botón mediano rectangular con esquinas redondeadas

7. **Notificación de Éxito (Toast/Alert):**
   - Posición: Esquina superior derecha
   - Ícono: Check verde (✓) dentro de un círculo
   - Título: "Completado" (negrita)
   - Mensaje: "Se agregó exitosamente el Resultado de Aprendizaje (RG1)"
   - Botón cerrar: "X" en la esquina superior derecha de la notificación

8. **Tabla de Resultados de Aprendizaje Generales:**
   
   - **Columna 1 - "Código":**
     - Códigos mostrados: RG1, RG2, RG3, RG4, RG5
     - Formato: Prefijo "RG" + número secuencial
     - Estilo: Texto negro, tamaño medio
     - Ancho: Aproximadamente 15% del ancho de la tabla
   
   - **Columna 2 - "Descripción":**
     - Descripciones completas de cada RG (competencias genéricas)
     - Ejemplos de texto observados:
       - RG1: "Comprender los principios fundamentales de la ingeniería de software."
       - RG2: "Diseñar y desarrollar sistemas de software escalables y seguros."
       - RG3: "Aplicar metodologías ágiles en la gestión de proyectos de software."
       - RG4: "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo"
       - RG5: "Comprender los principios fundamentales de la ingeniería de software."
     - Texto con wrap automático para descripciones largas
     - Ancho: Aproximadamente 70% del ancho de la tabla
   
   - **Columna 3 - "Acciones":**
     - Dos íconos de acción por cada fila:
       - Ícono de lápiz/editar (✏️) - color azul
       - Ícono de papelera/eliminar (🗑️) - color rojo
     - Alineación: Centrada en la columna
     - Ancho: Aproximadamente 15% del ancho de la tabla

9. **Paginación:**
   - Posición: Centro inferior de la pantalla, debajo de la tabla
   - Controles: "< Previous  1  2  3  Next >"
   - Página actual: "1" (resaltada visualmente)
   - Páginas totales disponibles: 3 páginas
   - Flechas de navegación: "< Previous" y "Next >" activas
   - Estilo: Números clicables, página actual con fondo destacado

10. **Footer:**
    - Enlaces: "Navegación  Recursos  Legal"
    - Íconos de redes sociales: LinkedIn (ℹ️), Twitter (🐦)
    - Posición: Parte inferior fija de la pantalla
    - Color de fondo: Gris claro

11. **Características Específicas Observadas:**
    - La tab "Resultados Generales (RG)" está **claramente activa** (subrayada en azul)
    - Los códigos comienzan con **"RG"** (diferenciándose de "RE" para específicos)
    - Los RGs representan **competencias genéricas/transversales** aplicables a cualquier programa
    - Notificación visible indica que se acaba de agregar RG1 exitosamente
    - Hay opciones completas de edición y eliminación (a diferencia de EUR-ACE)
    - El botón "+ Nuevo RA" permite agregar nuevos resultados de aprendizaje generales
    - La tabla muestra que RG1 y RG5 tienen la misma descripción (posible duplicado o reutilización)

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

**Grupo 2 - Sin RGs registrados (C1=V, C2=F):**
Las reglas R3-R4 (2 reglas) producen la acción A3 independientemente de C3.
Nota: Si no hay RGs, C3 es irrelevante (no hay nada que buscar).
**→ Se fusionan en R_MIN2**

**Reglas únicas - Considerando el caso sin búsqueda:**
Al igual que en la HU anterior, debo considerar el caso de visualización sin búsqueda activa como el happy path principal.

#### **🎯 TABLA MINIMIZADA FINAL:**

| **Regla** | **C1** | **C2** | **C3** | **Acciones** | **Descripción** |
|-----------|--------|--------|--------|--------------|-----------------|
| **R_MIN1** | **F** | **-** | **-** | **A2** | Usuario sin permisos Coordinador |
| **R_MIN2** | **V** | **F** | **-** | **A3** | No hay RGs registrados |
| **R_MIN3** ✅ | **V** | **V** | **No búsqueda** | **A1** | **Listado completo RGs (Happy Path)** |
| **R_MIN4** | **V** | **V** | **Búsqueda sin resultados** | **A1, A5** | Búsqueda sin coincidencias |
| **R_MIN5** | **V** | **V** | **Búsqueda con resultados** | **A1, A4** | Búsqueda exitosa |

**Reducción: De 8 reglas originales → 5 reglas (37.5% de reducción)**

---

### **PASO 4: NÚMERO TOTAL DE CRITERIOS DE ACEPTACIÓN**

**Número final: 5 Criterios de Aceptación**

#### **Justificación:**

✅ **Se mantienen los 5 AC derivados de la tabla minimizada** porque cada uno valida un escenario único:

1. **R_MIN1**: Validación de seguridad/permisos (específico para rol Coordinador de Carrera)
2. **R_MIN2**: Validación de estado del sistema (sin RGs en la carrera)
3. **R_MIN3**: Visualización completa del listado de RGs con tab "Resultados Generales (RG)" activa (CRÍTICO)
4. **R_MIN4**: Funcionalidad de búsqueda sin resultados
5. **R_MIN5**: Funcionalidad de búsqueda con resultados

❌ **No se eliminan criterios** porque:
- Esta HU es específica para **Resultados de Aprendizaje Generales (RG)**, que son cualitativamente diferentes de:
  - **RE (Resultados Específicos)**: Competencias técnicas específicas de la carrera
  - **OPP (Objetivos de Programa)**: Objetivos del perfil profesional
  - **Criterios EUR-ACE**: Estándares externos de acreditación
- Los **RGs representan competencias genéricas/transversales** aplicables a múltiples carreras
- Los **RGs son editables** por el Coordinador de Carrera
- La **tab "Resultados Generales (RG)" es distintiva** y diferencia esta vista de la de REs
- El **propósito educativo es diferente**: los RGs cubren competencias como comunicación, trabajo en equipo, pensamiento crítico, mientras los REs cubren competencias técnicas específicas

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (FORMATO GHERKIN)**

### **AC1 - Visualización completa del listado de Resultados de Aprendizaje Generales (HAPPY PATH)**

**Dado que** soy un Coordinador de Carrera autenticado en el sistema

**Y** existen Resultados de Aprendizaje Generales (RG) registrados para mi carrera

**Cuando** accedo a la funcionalidad "R. de Aprendizaje" desde el menú lateral

**Entonces** se muestra la pantalla con el título "Gestión de Resultados de Aprendizaje (RA)"

**Y** se muestran dos tabs (pestañas) en la parte superior:
   - "Resultados Generales (RG)" (ACTIVA, subrayada con línea azul)
   - "Resultados Específicos (RE)" (inactiva, color gris)

**Y** la tab "Resultados Generales (RG)" está seleccionada por defecto al entrar

**Y** se muestra un campo de búsqueda con ícono de lupa (🔍) y placeholder "Buscar por código o descripción..."

**Y** se muestra el botón "+ Nuevo RA" en color azul en la esquina superior derecha

**Y** se muestra una tabla con tres columnas: "Código", "Descripción" y "Acciones"

**Y** la columna "Código" muestra códigos con formato "RG" seguido de números (RG1, RG2, RG3, RG4, RG5)

**Y** la columna "Descripción" muestra las descripciones completas de cada Resultado de Aprendizaje General, como:
   - "Comprender los principios fundamentales de la ingeniería de software."
   - "Diseñar y desarrollar sistemas de software escalables y seguros."
   - "Aplicar metodologías ágiles en la gestión de proyectos de software."
   - "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo"

**Y** la columna "Acciones" muestra dos íconos para cada fila:
   - Ícono de lápiz (editar) en color azul
   - Ícono de papelera (eliminar) en color rojo

**Y** se muestra la paginación en la parte inferior con formato "< Previous  1  2  3  Next >"

**Y** la página actual (página 1) está resaltada visualmente

**Y** el menú lateral muestra "R. de Aprendizaje" como opción activa/seleccionada

**Y** si se acaba de agregar un RG, puede mostrarse una notificación de éxito en la esquina superior derecha con:
   - Ícono de check verde (✓)
   - Título "Completado"
   - Mensaje "Se agregó exitosamente el Resultado de Aprendizaje (RG[número])"
   - Botón "X" para cerrar la notificación.

---

### **AC2 - Intento de acceso sin permisos de Coordinador de Carrera**

**Dado que** estoy autenticado en el sistema

**Y** NO tengo asignado el rol de "Coordinador de Carrera"

**Y** tengo un rol diferente como "Profesor", "Administrador", "Miembro CEI" u otro

**Cuando** intento acceder a la funcionalidad "R. de Aprendizaje" desde el menú lateral

**O** intento acceder directamente a la URL de Resultados de Aprendizaje Generales

**Entonces** el sistema me redirige a la pantalla de inicio o dashboard

**Y** se muestra un mensaje de error "No tiene permisos para acceder a esta funcionalidad"

**Y** NO puedo visualizar la tab "Resultados Generales (RG)"

**Y** NO puedo visualizar el listado de RGs de ninguna carrera

**Y** la opción "R. de Aprendizaje" en el menú lateral puede estar oculta o deshabilitada según mi rol.

---

### **AC3 - Visualización cuando no existen RGs registrados en la carrera**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** NO existen Resultados de Aprendizaje Generales (RG) registrados para mi carrera

**Y** puede que la carrera esté en proceso de configuración inicial o los RGs fueron eliminados

**Cuando** accedo a la funcionalidad "R. de Aprendizaje"

**Y** la tab "Resultados Generales (RG)" se muestra activa por defecto

**Entonces** se muestra la pantalla con el título "Gestión de Resultados de Aprendizaje (RA)"

**Y** la tab "Resultados Generales (RG)" está activa y subrayada en azul

**Y** se muestra el campo de búsqueda vacío

**Y** se muestra el botón "+ Nuevo RA" disponible para agregar nuevos RGs

**Y** se muestra un mensaje informativo "No hay Resultados de Aprendizaje Generales registrados para esta carrera"

**Y** la tabla de RGs está vacía sin registros

**Y** NO se muestra la paginación

**Y** puedo hacer clic en "+ Nuevo RA" para comenzar a agregar RGs a mi carrera.

---

### **AC4 - Búsqueda de RGs sin resultados**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** estoy visualizando el listado de Resultados de Aprendizaje Generales (RG)

**Y** la tab "Resultados Generales (RG)" está activa

**Y** existen RGs registrados para mi carrera

**Cuando** ingreso un término de búsqueda en el campo "Buscar por código o descripción..."

**Y** el término no coincide con ningún código o descripción de los RGs

**Ejemplo:** ingreso "blockchain" pero ningún RG contiene ese texto

**Entonces** la tabla se actualiza dinámicamente

**Y** NO se muestran registros en la tabla

**Y** se muestra un mensaje "No se encontraron resultados para 'blockchain'"

**Y** el botón "+ Nuevo RA" permanece visible y activo

**Y** puedo borrar el término de búsqueda para volver a visualizar el listado completo

**Y** la paginación desaparece si no hay resultados

**Y** permanezco en la tab "Resultados Generales (RG)".

---

### **AC5 - Búsqueda exitosa de RGs**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** estoy visualizando el listado de Resultados de Aprendizaje Generales (RG)

**Y** la tab "Resultados Generales (RG)" está activa

**Y** existen múltiples RGs registrados para mi carrera

**Cuando** ingreso un término de búsqueda en el campo "Buscar por código o descripción..."

**Y** el término coincide con uno o más códigos o descripciones de RGs

**Ejemplo 1:** ingreso "RG3" y coincide con el código exacto

**Ejemplo 2:** ingreso "principios fundamentales" y coincide con múltiples descripciones

**Entonces** la tabla se actualiza dinámicamente mostrando únicamente los RGs que coinciden

**Y** cada resultado mostrado incluye:
   - Código completo del RG
   - Descripción completa del RG
   - Íconos de acciones (editar y eliminar)

**Y** se mantiene visible el botón "+ Nuevo RA"

**Y** si los resultados requieren paginación, se actualiza para reflejar solo las páginas de resultados filtrados

**Y** puedo interactuar con los íconos de editar o eliminar en los resultados filtrados

**Y** puedo borrar el término de búsqueda para volver al listado completo sin filtros

**Y** permanezco en la tab "Resultados Generales (RG)" durante toda la búsqueda.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **🎯 CRITERIO MÁS CRÍTICO:**

**AC1 - Visualización completa del listado de Resultados de Aprendizaje Generales (HAPPY PATH)**

---

### **✅ JUSTIFICACIÓN DE CRITICIDAD:**

1. **Propósito central de la HU**: Este AC valida directamente el objetivo expresado en la Historia de Usuario: "**listar los Resultados de Aprendizaje Generales Para revisar los resultados de aprendizaje esperados de mi carrera**". Sin este AC funcionando, la HU no cumple su propósito fundamental.

2. **Diferenciación crítica: RGs como competencias genéricas**: Este AC valida la funcionalidad específica de visualizar **Resultados de Aprendizaje Generales (RG)**, que representan **competencias genéricas/transversales** fundamentales para cualquier profesional:
   - Comunicación efectiva oral y escrita
   - Trabajo en equipo y liderazgo
   - Pensamiento crítico y resolución de problemas
   - Compromiso ético y responsabilidad profesional
   - Aprendizaje autónomo y continuo
   
   Estas competencias son **obligatorias en modelos educativos modernos** y requeridas por organismos de acreditación.

3. **Cumplimiento de modelos educativos basados en competencias**: Los sistemas educativos actuales (especialmente en ingeniería) requieren **separación explícita** entre:
   - **Competencias genéricas (RG)**: Aplicables a cualquier profesional, independientemente de su especialidad
   - **Competencias específicas (RE)**: Técnicas y especializadas de cada carrera
   
   Este AC valida que el sistema implementa correctamente esta separación mediante tabs diferenciadas.

4. **Prerequisito para alineación curricular completa**: Los Coordinadores necesitan visualizar los RGs para:
   - Mapear RGs contra Objetivos de Carrera (OPP)
   - Mapear RGs contra Criterios EUR-ACE (varios criterios EUR-ACE exigen competencias genéricas)
   - Diseñar asignaturas que desarrollen competencias transversales
   - Identificar brechas en competencias genéricas del currículo
   - Garantizar desarrollo integral de estudiantes (no solo técnico)

5. **Base para acreditación nacional e internacional**: Los organismos de acreditación (EUR-ACE, ABET, CEAACES, etc.) **exigen explícitamente** demostrar que el programa desarrolla competencias genéricas. Sin visualización de RGs:
   - No se puede mapear contra criterios de acreditación que requieren competencias genéricas
   - No se puede demostrar cobertura de competencias transversales
   - No se puede evidenciar formación integral del estudiante
   - Se compromete la acreditación del programa

6. **Evidencia visual directa del diseño**: La imagen 9 muestra explícitamente:
   - La tab "Resultados Generales (RG)" ACTIVA (subrayada en azul)
   - Códigos con formato "RG" (RG1, RG2, RG3, RG4, RG5)
   - Notificación de éxito reciente: "Se agregó exitosamente el Resultado de Aprendizaje (RG1)"
   
   Esto indica que la visualización de RGs es una funcionalidad principal y recientemente utilizada.

7. **Gestión de competencias reutilizables**: Los RGs típicamente son **compartibles o reutilizables** entre carreras similares (ej: todas las ingenierías comparten competencias genéricas básicas). Este AC valida que los coordinadores pueden:
   - Revisar los RGs definidos para su carrera
   - Identificar RGs comunes con otras carreras
   - Mantener consistencia institucional en competencias genéricas
   - Actualizar RGs cuando evolucionan estándares educativos

8. **Acciones de edición críticas**: El AC valida que los RGs son **editables y eliminables**, lo cual es fundamental porque:
   - Las competencias genéricas evolucionan con cambios en el mercado laboral
   - Nuevas competencias emergen (ej: competencias digitales, sostenibilidad)
   - Los coordinadores deben poder adaptar RGs a contextos locales
   - Se requiere actualización periódica según feedback de empleadores/egresados

9. **Contexto de "mi carrera" con alcance institucional**: Aunque el coordinador ve RGs de "su carrera", muchos RGs pueden ser **definidos institucionalmente** y aplicarse a múltiples carreras. Este AC valida:
   - El filtrado correcto por carrera (cada coordinador ve sus RGs)
   - La posibilidad de reutilizar RGs comunes
   - La autonomía de cada carrera en definir sus competencias genéricas específicas

10. **Diferencia con REs validada por tabs**: El sistema de tabs (RG vs RE) que este AC valida es **crítico para usabilidad** porque:
    - Evita confusión entre competencias genéricas y específicas
    - Facilita navegación organizada
    - Permite gestión independiente de ambos tipos
    - Cumple con modelos educativos que separan ambas categorías

11. **Impacto en diseño de planes de estudio**: Los RGs son base para:
    - Diseñar asignaturas de formación general (ej: comunicación, ética, emprendimiento)
    - Incluir actividades transversales en asignaturas técnicas
    - Definir estrategias pedagógicas para competencias blandas
    - Establecer criterios de evaluación de competencias genéricas
    - Garantizar coherencia horizontal y vertical del currículo

12. **Notificación de éxito como feedback crítico**: La imagen 9 muestra una notificación de éxito "Se agregó exitosamente el Resultado de Aprendizaje (RG1)", lo cual indica:
    - Flujo reciente de creación de RG
    - Importancia del feedback visual inmediato
    - Integración entre funcionalidades de creación y visualización
    - Confirmación de que los RGs se están gestionando activamente

13. **Códigos RG distintivos para trazabilidad**: El AC valida que los códigos comienzan con "RG" (no "RE", "OPP" o "5.x.x"), lo cual es **fundamental para**:
    - Referencia cruzada en matrices de alineación
    - Documentos de acreditación
    - Syllabus de asignaturas
    - Reportes de evaluación de aprendizajes
    - Comunicación clara con stakeholders

14. **Paginación para múltiples RGs**: Aunque típicamente hay menos RGs que REs (10-15 RGs vs 20-40 REs), el AC valida el manejo correcto de paginación para carreras con múltiples competencias genéricas definidas.

15. **Búsqueda como herramienta de consulta rápida**: Los AC4 y AC5 validan la búsqueda, pero el **AC1 es más crítico** porque:
    - Los coordinadores necesitan primero una visión completa de todas las competencias genéricas
    - La búsqueda es útil para localizar RGs específicos en conjuntos grandes
    - El listado completo es prerequisito para validar completitud del perfil

---

**CONCLUSIÓN:**

El **AC1 es absolutamente crítico** porque valida la funcionalidad central que permite al Coordinador de Carrera visualizar y revisar los **Resultados de Aprendizaje Generales (RG)** de su carrera, que representan las **competencias genéricas/transversales obligatorias** en modelos educativos modernos. Esta visualización es **prerequisito fundamental** para la alineación curricular completa (genérica + específica), el cumplimiento de requisitos de acreditación nacional e internacional, y el diseño de un programa académico que garantice formación integral de profesionales con competencias técnicas Y transversales. Sin este AC funcionando, los coordinadores no pueden gestionar el componente de competencias genéricas del perfil de egreso, lo cual compromete la calidad integral del programa y su capacidad de formar profesionales completos que respondan a las demandas del siglo XXI.

---

**FIN DEL ANÁLISIS** ✅