# **ANÁLISIS COMPLETO - HU: Visualizar Resultados de Aprendizaje Específicos (RE)**

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **PASO 1: LISTA DE CONDICIONES Y ACCIONES**

#### **📋 CONDICIONES IDENTIFICADAS:**

**C1:** Usuario tiene rol de "Coordinador de Carrera" (**V** = Sí, **F** = No)

**C2:** Existen Resultados de Aprendizaje Específicos (RE) registrados en la carrera (**V** = Sí, **F** = No)

**C3:** Término de búsqueda ingresado coincide con algún RE (**V** = Sí, **F** = No)

---

#### **⚙️ ACCIONES RESULTANTES:**

**A1:** Sistema muestra la pantalla "Gestión de Resultados de Aprendizaje (RA)" con la tab "Resultados Específicos (RE)" activa

**A2:** Sistema muestra mensaje de error "No tiene permisos para acceder a esta funcionalidad"

**A3:** Sistema muestra mensaje "No hay Resultados de Aprendizaje Específicos registrados para esta carrera"

**A4:** Sistema filtra y muestra únicamente los RE que coinciden con el término de búsqueda

**A5:** Sistema muestra mensaje "No se encontraron resultados para '[término buscado]'"

---

#### **📸 ANÁLISIS VISUAL DETALLADO DE LA IMAGEN 10:**

**Estructura de la pantalla "Gestión de Resultados de Aprendizaje (RA)":**

1. **Header/Navegación Superior:**
   - Logo "POLIACREDITA" (esquina superior izquierda)
   - Identificación de rol: "Coordinador de Carrera" (esquina superior derecha)
   - Íconos de configuración, notificaciones y perfil

2. **Menú Lateral (Sidebar):**
   - Ícono de inicio: "Inicio"
   - Ícono de capas: "Objetivos de Carrera" (anteriormente llamado "Objetivos de Programa")
   - Ícono de libro: **"R. de Aprendizaje"** (activo/seleccionado)
   - Ícono de documento: "Criterios EUR-ACE"
   - Ícono de configuración: "Editor Mapeos" (con dropdown)
   - Sección "Configuración" con:
     - "Usuarios"
     - "Roles"
   - Ícono de usuario: "Mi Perfil"

3. **Título Principal:**
   - Texto: "Gestión de Resultados de Aprendizaje (RA)"
   - Tipografía: Grande, negrita

4. **Sistema de Tabs (Pestañas):**
   - **Tab 1:** "Resultados Generales (RG)" (inactiva, color gris)
   - **Tab 2:** "Resultados Específicos (RE)" (activa, subrayada en azul)
   - Indicador visual: Línea azul debajo de la tab activa

5. **Barra de Búsqueda:**
   - Ícono de lupa (🔍)
   - Placeholder: "Buscar por código o descripción..."
   - Ancho: Aproximadamente 50% del ancho de la pantalla
   - Posición: Debajo de las tabs

6. **Botón de Acción Principal:**
   - Texto: "+ Nuevo RA"
   - Color: Azul oscuro
   - Posición: Esquina superior derecha, alineado con la barra de búsqueda

7. **Tabla de Resultados de Aprendizaje Específicos:**
   
   - **Columna 1 - "Código":**
     - Códigos mostrados: RE1, RE2, RE3, RE4, RE5
     - Formato: Prefijo "RE" + número
     - Ancho: Aproximadamente 15% del ancho de la tabla
   
   - **Columna 2 - "Descripción":**
     - Descripciones completas de cada RE
     - Ejemplos de texto observados:
       - RE1: "Comprender los principios fundamentales de la ingeniería de software."
       - RE2: "Diseñar y desarrollar sistemas de software escalables y seguros."
       - RE3: "Aplicar metodologías ágiles en la gestión de proyectos de software."
       - RE4: "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo"
       - RE5: "Comprender los principios fundamentales de la ingeniería de software."
     - Ancho: Aproximadamente 70% del ancho de la tabla
   
   - **Columna 3 - "Acciones":**
     - Íconos de acción por cada fila:
       - Ícono de lápiz (editar) - color azul
       - Ícono de papelera (eliminar) - color rojo
     - Ancho: Aproximadamente 15% del ancho de la tabla

8. **Paginación:**
   - Posición: Centro inferior de la pantalla
   - Controles: "< Previous  1  2  3  Next >"
   - Página actual: "1" (resaltada)
   - Páginas disponibles: 3 páginas totales
   - Flechas de navegación activas

9. **Footer:**
   - Enlaces: "Navegación  Recursos  Legal"
   - Íconos de redes sociales: LinkedIn, Twitter
   - Posición: Parte inferior de la pantalla

10. **Características Específicas Observadas:**
    - La tab "Resultados Específicos (RE)" está claramente diferenciada de "Resultados Generales (RG)"
    - Los códigos comienzan con "RE" (no "RG")
    - Los REs son específicos de la carrera/programa
    - Hay opciones de edición y eliminación (a diferencia de los criterios EUR-ACE que son solo lectura)
    - El botón "+ Nuevo RA" permite agregar nuevos resultados de aprendizaje

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

**Grupo 2 - Sin REs registrados (C1=V, C2=F):**
Las reglas R3-R4 (2 reglas) producen la acción A3 independientemente de C3.
Nota: Si no hay REs, C3 es irrelevante (no hay nada que buscar).
**→ Se fusionan en R_MIN2**

**Reglas únicas - Considerando el caso sin búsqueda:**
Similar al análisis anterior, necesito considerar el caso de visualización sin búsqueda activa como el happy path principal.

#### **🎯 TABLA MINIMIZADA FINAL:**

| **Regla** | **C1** | **C2** | **C3** | **Acciones** | **Descripción** |
|-----------|--------|--------|--------|--------------|-----------------|
| **R_MIN1** | **F** | **-** | **-** | **A2** | Usuario sin permisos Coordinador |
| **R_MIN2** | **V** | **F** | **-** | **A3** | No hay REs registrados |
| **R_MIN3** ✅ | **V** | **V** | **No búsqueda** | **A1** | **Listado completo REs (Happy Path)** |
| **R_MIN4** | **V** | **V** | **Búsqueda sin resultados** | **A1, A5** | Búsqueda sin coincidencias |
| **R_MIN5** | **V** | **V** | **Búsqueda con resultados** | **A1, A4** | Búsqueda exitosa |

**Reducción: De 8 reglas originales → 5 reglas (37.5% de reducción)**

---

### **PASO 4: NÚMERO TOTAL DE CRITERIOS DE ACEPTACIÓN**

**Número final: 5 Criterios de Aceptación**

#### **Justificación:**

✅ **Se mantienen los 5 AC derivados de la tabla minimizada** porque cada uno valida un escenario único:

1. **R_MIN1**: Validación de seguridad/permisos (específico para rol Coordinador de Carrera)
2. **R_MIN2**: Validación de estado del sistema (sin REs en la carrera)
3. **R_MIN3**: Visualización completa del listado de REs con tab activa (CRÍTICO - Happy Path)
4. **R_MIN4**: Funcionalidad de búsqueda sin resultados
5. **R_MIN5**: Funcionalidad de búsqueda con resultados

❌ **No se eliminan criterios** porque:
- Esta HU es específica para **Resultados de Aprendizaje Específicos (RE)**, que son diferentes de:
  - **RG (Resultados Generales)**: Competencias genéricas aplicables a cualquier carrera
  - **OPP (Objetivos de Programa)**: Objetivos del perfil profesional
  - **Criterios EUR-ACE**: Estándares externos de acreditación
- Los **REs son editables** por el Coordinador de Carrera (a diferencia de EUR-ACE)
- Los **REs son específicos de cada carrera** y reflejan el perfil de egreso detallado
- El **contexto de uso es único**: revisar resultados de aprendizaje detallados de "mi carrera"
- La **tab "Resultados Específicos (RE)" es distintiva** y diferencia esta vista de la de RGs

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (FORMATO GHERKIN)**

### **AC1 - Visualización completa del listado de Resultados de Aprendizaje Específicos (HAPPY PATH)**

**Dado que** soy un Coordinador de Carrera autenticado en el sistema

**Y** existen Resultados de Aprendizaje Específicos (RE) registrados para mi carrera

**Cuando** accedo a la funcionalidad "R. de Aprendizaje" desde el menú lateral

**Entonces** se muestra la pantalla con el título "Gestión de Resultados de Aprendizaje (RA)"

**Y** se muestran dos tabs (pestañas) en la parte superior:
   - "Resultados Generales (RG)" (inactiva, color gris)
   - "Resultados Específicos (RE)" (activa, subrayada con línea azul)

**Y** la tab "Resultados Específicos (RE)" está seleccionada por defecto

**Y** se muestra un campo de búsqueda con ícono de lupa y placeholder "Buscar por código o descripción..."

**Y** se muestra el botón "+ Nuevo RA" en color azul en la esquina superior derecha

**Y** se muestra una tabla con tres columnas: "Código", "Descripción" y "Acciones"

**Y** la columna "Código" muestra códigos con formato "RE" seguido de números (RE1, RE2, RE3, RE4, RE5)

**Y** la columna "Descripción" muestra las descripciones completas de cada Resultado de Aprendizaje Específico, como:
   - "Comprender los principios fundamentales de la ingeniería de software."
   - "Diseñar y desarrollar sistemas de software escalables y seguros."
   - "Aplicar metodologías ágiles en la gestión de proyectos de software."
   - "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo"

**Y** la columna "Acciones" muestra dos íconos para cada fila:
   - Ícono de lápiz (editar) en color azul
   - Ícono de papelera (eliminar) en color rojo

**Y** se muestra la paginación en la parte inferior con formato "< Previous  1  2  3  Next >"

**Y** la página actual (página 1) está resaltada visualmente

**Y** el menú lateral muestra "R. de Aprendizaje" como opción activa/seleccionada.

---

### **AC2 - Intento de acceso sin permisos de Coordinador de Carrera**

**Dado que** estoy autenticado en el sistema

**Y** NO tengo asignado el rol de "Coordinador de Carrera"

**Y** tengo un rol diferente como "Profesor", "Administrador" u otro

**Cuando** intento acceder a la funcionalidad "R. de Aprendizaje" desde el menú lateral

**O** intento acceder directamente a la URL de Resultados de Aprendizaje Específicos

**Entonces** el sistema me redirige a la pantalla de inicio o dashboard

**Y** se muestra un mensaje de error "No tiene permisos para acceder a esta funcionalidad"

**Y** NO puedo visualizar la tab "Resultados Específicos (RE)"

**Y** NO puedo visualizar el listado de REs de ninguna carrera

**Y** la opción "R. de Aprendizaje" en el menú lateral puede estar oculta o deshabilitada según mi rol.

---

### **AC3 - Visualización cuando no existen REs registrados en la carrera**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** NO existen Resultados de Aprendizaje Específicos (RE) registrados para mi carrera

**Y** puede que la carrera esté en proceso de configuración inicial o los REs fueron eliminados

**Cuando** accedo a la funcionalidad "R. de Aprendizaje"

**Y** selecciono la tab "Resultados Específicos (RE)"

**Entonces** se muestra la pantalla con el título "Gestión de Resultados de Aprendizaje (RA)"

**Y** la tab "Resultados Específicos (RE)" está activa y subrayada

**Y** se muestra el campo de búsqueda vacío

**Y** se muestra el botón "+ Nuevo RA" disponible para agregar nuevos REs

**Y** se muestra un mensaje informativo "No hay Resultados de Aprendizaje Específicos registrados para esta carrera"

**Y** la tabla de REs está vacía sin registros

**Y** NO se muestra la paginación

**Y** puedo hacer clic en "+ Nuevo RA" para comenzar a agregar REs a mi carrera.

---

### **AC4 - Búsqueda de REs sin resultados**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** estoy visualizando el listado de Resultados de Aprendizaje Específicos (RE)

**Y** la tab "Resultados Específicos (RE)" está activa

**Y** existen REs registrados para mi carrera

**Cuando** ingreso un término de búsqueda en el campo "Buscar por código o descripción..."

**Y** el término no coincide con ningún código o descripción de los REs

**Ejemplo:** ingreso "machine learning avanzado" pero ningún RE contiene ese texto

**Entonces** la tabla se actualiza dinámicamente

**Y** NO se muestran registros en la tabla

**Y** se muestra un mensaje "No se encontraron resultados para 'machine learning avanzado'"

**Y** el botón "+ Nuevo RA" permanece visible y activo

**Y** puedo borrar el término de búsqueda para volver a visualizar el listado completo

**Y** la paginación desaparece si no hay resultados

**Y** permanezco en la tab "Resultados Específicos (RE)".

---

### **AC5 - Búsqueda exitosa de REs**

**Dado que** soy un Coordinador de Carrera autenticado

**Y** estoy visualizando el listado de Resultados de Aprendizaje Específicos (RE)

**Y** la tab "Resultados Específicos (RE)" está activa

**Y** existen múltiples REs registrados para mi carrera

**Cuando** ingreso un término de búsqueda en el campo "Buscar por código o descripción..."

**Y** el término coincide con uno o más códigos o descripciones de REs

**Ejemplo 1:** ingreso "RE2" y coincide con el código exacto

**Ejemplo 2:** ingreso "software" y coincide con múltiples descripciones que contienen esa palabra

**Entonces** la tabla se actualiza dinámicamente mostrando únicamente los REs que coinciden

**Y** cada resultado mostrado incluye:
   - Código completo del RE
   - Descripción completa del RE
   - Íconos de acciones (editar y eliminar)

**Y** se mantiene visible el botón "+ Nuevo RA"

**Y** si los resultados requieren paginación, se actualiza para reflejar solo las páginas de resultados filtrados

**Y** puedo interactuar con los íconos de editar o eliminar en los resultados filtrados

**Y** puedo borrar el término de búsqueda para volver al listado completo sin filtros

**Y** permanezco en la tab "Resultados Específicos (RE)" durante toda la búsqueda.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **🎯 CRITERIO MÁS CRÍTICO:**

**AC1 - Visualización completa del listado de Resultados de Aprendizaje Específicos (HAPPY PATH)**

---

### **✅ JUSTIFICACIÓN DE CRITICIDAD:**

1. **Propósito central de la HU**: Este AC valida directamente el objetivo expresado en la Historia de Usuario: "**listar los Resultados de Aprendizaje Específicos Para revisar los resultados de aprendizaje detallados de mi carrera**". Sin este AC funcionando, la HU no cumple su razón de existir.

2. **Diferenciación crítica: REs vs RGs**: Este AC valida la funcionalidad específica de visualizar **Resultados de Aprendizaje Específicos (RE)**, que son cualitativamente diferentes de los Resultados Generales (RG):
   - **REs**: Competencias específicas del perfil de egreso de la carrera de ingeniería de software
   - **RGs**: Competencias genéricas transversales aplicables a cualquier carrera
   
   La tab activa "Resultados Específicos (RE)" es el elemento diferenciador que este AC debe validar.

3. **Prerequisito para gestión del perfil de egreso**: Los Coordinadores de Carrera necesitan visualizar los REs constantemente para:
   - Diseñar y revisar el perfil de egreso detallado de la carrera
   - Mapear REs contra Objetivos de Carrera (OPP)
   - Mapear REs contra Criterios EUR-ACE para acreditación
   - Identificar brechas en competencias específicas
   - Planificar actualizaciones curriculares basadas en tendencias tecnológicas
   - Responder a requerimientos del mercado laboral

4. **Base para alineación curricular específica**: Este AC es prerequisito para:
   - Creación de relaciones OPP-RE (matriz de alineación curricular interna)
   - Creación de relaciones RE-EURACE (matriz de cumplimiento de estándares)
   - Análisis de cobertura de competencias específicas en el plan de estudios
   - Identificación de REs sin asignaturas asociadas
   - Generación de reportes de trazabilidad curricular

5. **Evidencia visual directa del diseño**: La imagen 10 muestra explícitamente la tab "Resultados Específicos (RE)" activa, lo que indica que esta es una funcionalidad diferenciada y principal en el diseño del sistema.

6. **Acciones de edición disponibles**: A diferencia de los criterios EUR-ACE (solo lectura), los REs son **editables y eliminables** por el Coordinador de Carrera. Este AC valida que estas acciones están disponibles en la interfaz, lo cual es crítico para que los coordinadores puedan:
   - Actualizar descripciones de REs cuando evolucionan las competencias requeridas
   - Eliminar REs obsoletos cuando cambia el perfil de egreso
   - Mantener alineados los REs con las necesidades del sector profesional

7. **Contexto de "mi carrera"**: Este AC valida el filtrado implícito por carrera. El Coordinador solo ve los REs de **su carrera específica**, no de todas las carreras de la institución. Esto es crítico para:
   - Evitar confusión entre REs de diferentes programas
   - Mantener autonomía de cada carrera en su diseño curricular
   - Facilitar la gestión independiente del perfil de egreso

8. **Complejidad de navegación por tabs**: Este AC valida la funcionalidad del sistema de tabs (RG vs RE), lo cual es un elemento de navegación crítico que permite a los coordinadores:
   - Distinguir claramente entre competencias genéricas y específicas
   - Gestionar ambos tipos de resultados de aprendizaje de forma organizada
   - Cumplir con modelos educativos que separan competencias genéricas de específicas

9. **Impacto en procesos de acreditación**: Sin visualización de REs, los coordinadores no pueden:
   - Demostrar cobertura de competencias específicas requeridas por EUR-ACE
   - Preparar evidencia de que el perfil de egreso está alineado con estándares
   - Responder a observaciones de auditores sobre competencias técnicas específicas
   - Justificar decisiones de diseño curricular en informes de autoevaluación

10. **Base para diseño de asignaturas**: Los REs son la base para:
    - Definir los resultados de aprendizaje de cada asignatura
    - Diseñar contenidos y actividades de aprendizaje
    - Establecer criterios de evaluación
    - Garantizar coherencia vertical y horizontal del currículo

11. **Códigos RE distintivos**: El AC valida que los códigos comienzan con "RE" (no "RG", "OPP" o "5.x.x"), lo cual es fundamental para la trazabilidad y referencia cruzada en matrices y documentos de acreditación.

12. **Paginación para múltiples REs**: Las carreras de ingeniería típicamente tienen 20-40 REs específicos. El AC valida que el sistema maneja correctamente la paginación de estos múltiples resultados, presentándolos de forma organizada (páginas 1, 2, 3 como se ve en la imagen).

13. **Búsqueda como funcionalidad complementaria**: Los AC4 y AC5 validan la búsqueda, pero el **AC1 es más crítico** porque:
    - La mayoría de coordinadores primero revisarán el listado completo
    - La búsqueda solo es útil si el listado base funciona
    - Los coordinadores necesitan ver todos los REs para validar completitud del perfil

14. **Gestión continua del perfil de egreso**: A diferencia de visualizaciones puntuales, este listado es consultado **frecuentemente** durante:
    - Reuniones de comité curricular
    - Procesos de autoevaluación
    - Revisiones periódicas del plan de estudios
    - Preparación de informes institucionales
    - Respuesta a empleadores sobre competencias de egresados

---

**CONCLUSIÓN:**

El **AC1 es absolutamente crítico** porque valida la funcionalidad central que permite al Coordinador de Carrera visualizar y revisar los **Resultados de Aprendizaje Específicos (RE)** de su carrera, diferenciándolos de los Resultados Generales (RG). Esta visualización es **prerequisito fundamental** para la gestión del perfil de egreso, la alineación curricular interna y externa, y los procesos de acreditación. Sin este AC funcionando, los coordinadores no pueden ejecutar su responsabilidad principal de diseñar, revisar y mantener actualizado el perfil de egreso específico de la carrera, lo cual compromete la calidad y pertinencia del programa académico.

---

**FIN DEL ANÁLISIS** ✅