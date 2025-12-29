# ANÁLISIS COMPLETO - HU: Visualizar Objetivos de Programa (OPP)

---

## 📋 **PASO 1: ANÁLISIS VISUAL EXHAUSTIVO DE IMÁGENES DEL PROTOTIPO**

### **🔍 ELEMENTOS DE UI IDENTIFICADOS EN LAS IMÁGENES:**

#### **Imagen 2 - Pantalla Principal "Gestión de Objetivos de Carrera (OPP)":**

**Componentes de UI:**
1. **Header de página:**
   - Título: "Gestión de Objetivos de Carrera (OPP)" (tipografía grande, negrita)
   - Botón "+ Nuevo OPP" (azul oscuro, esquina superior derecha)

2. **Barra de búsqueda:**
   - Campo de texto con ícono de lupa (🔍)
   - Placeholder: "Buscar por código o descripción..."
   - Posición: Debajo del título

3. **Tabla de datos:**
   - **Columna 1 - Código:** Ancho fijo, alineación izquierda
   - **Columna 2 - Descripción:** Ancho expandido, texto largo
   - **Columna 3 - Acciones:** Ancho fijo, dos íconos:
     - Ícono de lápiz (editar) en azul
     - Ícono de papelera (eliminar) en rojo

4. **Datos visibles en la tabla:**
   - **OPP1**: "Comprender los principios fundamentales de la ingeniería de software."
   - **OPP2**: "Diseñar y desarrollar sistemas de software escalables y seguros."
   - **OPP3**: "Aplicar metodologías ágiles en la gestión de proyectos de software."
   - **OPP4**: "Integrar herramientas y tecnologías modernas en el ciclo de vida de desarrollo"
   - **OPP5**: "Comprender los principios fundamentales de la ingeniería de software."

5. **Paginación:**
   - Botones: "< Previous", "1", "2", "3", "Next >"
   - Posición: Centrado en la parte inferior
   - Página actual: "1" (resaltada)

6. **Menú lateral izquierdo (navegación):**
   - Inicio
   - **Objetivos de Carrera** (resaltado/activo)
   - R. de Aprendizaje
   - Criterios EUR-ACE
   - Editor Mapeos (expandible)
     - RA vs OPP
     - RA vs EUR-ACE
   - Mi Perfil

---

### **🎯 COMPORTAMIENTOS OBSERVADOS:**

1. **Búsqueda dinámica:** Campo de búsqueda permite filtrar por código o descripción
2. **Paginación funcional:** Navegación entre múltiples páginas de OPPs
3. **Listado completo:** Muestra todos los OPPs de la carrera del coordinador autenticado
4. **Acciones por registro:** Cada OPP tiene opciones de editar y eliminar
5. **Navegación consistente:** Menú lateral permite moverse entre secciones

---

### **📊 CONDICIONES IDENTIFICADAS:**

Basándome en el análisis visual de las imágenes y la HU:

**C1: Existencia de OPPs en el sistema**
- **Valor TRUE**: Existen uno o más OPPs registrados para la carrera
- **Valor FALSE**: No existen OPPs registrados para la carrera

**C2: Usuario autenticado como Coordinador de Carrera**
- **Valor TRUE**: Usuario tiene rol de Coordinador y sesión activa
- **Valor FALSE**: Usuario no autenticado o rol diferente

**C3: Uso de búsqueda**
- **Valor TRUE**: Usuario ingresa texto en el campo de búsqueda
- **Valor FALSE**: Campo de búsqueda vacío (vista completa)

---

## 📊 **PASO 2: CREAR TABLA DE DECISIÓN COMPLETA (MAXIMIZADA)**

### **Condiciones identificadas:**
- **C1**: Existen OPPs en el sistema (TRUE/FALSE)
- **C2**: Usuario autenticado como Coordinador (TRUE/FALSE)
- **C3**: Usuario aplica búsqueda (TRUE/FALSE)

### **Cálculo de combinaciones:**
**2^3 = 8 reglas teóricas**

### **TABLA DE DECISIÓN COMPLETA:**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Existen OPPs** | T | T | T | T | F | F | F | F |
| **C2: Usuario es Coordinador** | T | T | F | F | T | T | F | F |
| **C3: Usuario aplica búsqueda** | T | F | T | F | T | F | T | F |
| **ACCIÓN RESULTANTE** | **A1** | **A2** | **A3** | **A3** | **A4** | **A4** | **A3** | **A3** |

### **ACCIONES:**

- **A1**: Mostrar listado de OPPs filtrado según búsqueda con paginación
- **A2**: Mostrar listado completo de OPPs con paginación
- **A3**: Redirigir a login (acceso denegado)
- **A4**: Mostrar mensaje "No hay OPPs registrados para esta carrera"

---

## 🔄 **PASO 3: CREAR TABLA DE DECISIÓN MINIMIZADA**

### **Análisis de Minimización:**

**Observaciones:**
1. **R3, R4, R7, R8**: Todas las reglas donde C2=FALSE (usuario no es coordinador) producen la misma acción **A3** (redirigir a login), independientemente de C1 y C3
2. **R5, R6**: Cuando usuario es coordinador (C2=TRUE) pero no hay OPPs (C1=FALSE), siempre se muestra **A4** (mensaje de lista vacía), independientemente de C3
3. **R1**: Usuario coordinador, existen OPPs, y aplica búsqueda → **A1** (filtrado)
4. **R2**: Usuario coordinador, existen OPPs, sin búsqueda → **A2** (listado completo)

**Minimización:**
- **R3, R4, R7, R8** → **RM1**: `- - FALSE` → A3
- **R5, R6** → **RM2**: `FALSE TRUE -` → A4
- **R1** → **RM3**: `TRUE TRUE TRUE` → A1
- **R2** → **RM4**: `TRUE TRUE FALSE` → A2

### **TABLA DE DECISIÓN MINIMIZADA:**

| **Regla Minimizada** | **RM1** | **RM2** | **RM3** | **RM4** |
|----------------------|---------|---------|---------|---------|
| **C1: Existen OPPs** | - | FALSE | TRUE | TRUE |
| **C2: Usuario es Coordinador** | FALSE | TRUE | TRUE | TRUE |
| **C3: Usuario aplica búsqueda** | - | - | TRUE | FALSE |
| **ACCIÓN RESULTANTE** | **A3** | **A4** | **A1** | **A2** |

**Reglas minimizadas: 4**
**Criterios de Aceptación necesarios: 4**

---

## ✅ **PASO 4: DECLARAR NÚMERO FINAL DE CRITERIOS DE ACEPTACIÓN**

**Número total de Criterios de Aceptación:** **4 (cuatro)**

Basándome en la tabla de decisión minimizada, se requieren exactamente **4 Criterios de Aceptación** que corresponden a las 4 reglas minimizadas:

1. **AC1 (RM4)**: Listar OPPs completos (Happy Path - sin búsqueda)
2. **AC2 (RM3)**: Buscar y filtrar OPPs por código o descripción
3. **AC3 (RM2)**: Visualizar mensaje cuando no hay OPPs
4. **AC4 (RM1)**: Redirigir a login cuando no está autenticado como Coordinador

**Nota sobre criterios eliminados:** 
Al analizar otras HUs similares en el sistema, se identificó que ya existe la HU "Listar Objetivos de Programa (OPP)" previamente documentada. Sin embargo, tras revisar su alcance, se confirmó que ambas HUs son **equivalentes y duplicadas**. Dado que la presente HU ("Visualizar Objetivos de Programa (OPP)") ya está en desarrollo activo y cuenta con prototipos visuales completos, **se recomienda consolidar ambas HUs en una sola** para evitar redundancia en el backlog. Los 4 criterios aquí definidos cubren completamente la funcionalidad de listado y búsqueda de OPPs.

---

## 📝 **PASO 5: GENERAR CRITERIOS DE ACEPTACIÓN EN FORMATO GHERKIN**

### **Criterio de Aceptación 1 (AC1 - RM4): Listar todos los OPPs de la carrera**

```gherkin
Escenario 1: Visualizar listado completo de Objetivos de Programa sin aplicar búsqueda
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y existen Objetivos de Programa registrados para mi carrera
Y estoy en la pantalla "Gestión de Objetivos de Carrera (OPP)"
Cuando accedo al listado sin ingresar texto en el campo de búsqueda
Entonces el sistema muestra la tabla completa con columnas "Código", "Descripción" y "Acciones"
Y se visualizan todos los OPPs de mi carrera en la tabla
Y cada fila de la tabla muestra el código del OPP (ej: "OPP1", "OPP2", etc.)
Y cada fila muestra la descripción completa del OPP
Y cada fila incluye dos íconos de acción: lápiz azul (editar) y papelera roja (eliminar)
Y se presenta el sistema de paginación en la parte inferior ("Previous", números de página, "Next")
Y la página actual está resaltada en la paginación
Y el botón "+ Nuevo OPP" aparece en la esquina superior derecha de color azul oscuro
Y el campo de búsqueda muestra el placeholder "Buscar por código o descripción..."
Y la información se actualiza automáticamente sin recargar la página completa
```

---

### **Criterio de Aceptación 2 (AC2 - RM3): Buscar OPPs por código o descripción**

```gherkin
Escenario 2: Filtrar Objetivos de Programa mediante búsqueda por código o descripción
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y existen Objetivos de Programa registrados para mi carrera
Y estoy en la pantalla "Gestión de Objetivos de Carrera (OPP)"
Cuando ingreso texto en el campo de búsqueda (por ejemplo: "escalables" o "OPP2")
Entonces el sistema filtra automáticamente la tabla de OPPs
Y se muestran únicamente los OPPs cuyo código o descripción contienen el texto ingresado
Y el filtrado ocurre de forma dinámica sin necesidad de presionar un botón de búsqueda
Y se mantiene visible el texto de búsqueda ingresado en el campo
Y la paginación se actualiza según los resultados filtrados
Y si no hay coincidencias, se muestra la tabla vacía con mensaje "No se encontraron resultados"
Y al limpiar el campo de búsqueda, se restaura el listado completo de OPPs
Y el filtrado funciona sin recargar la página completa
```

---

### **Criterio de Aceptación 3 (AC3 - RM2): Visualizar mensaje cuando no hay OPPs registrados**

```gherkin
Escenario 3: Mostrar mensaje informativo cuando la carrera no tiene OPPs registrados
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y mi carrera NO tiene Objetivos de Programa registrados en el sistema
Cuando accedo a la pantalla "Gestión de Objetivos de Carrera (OPP)"
Entonces el sistema muestra la estructura de la tabla con columnas "Código", "Descripción" y "Acciones"
Y la tabla aparece vacía sin filas de datos
Y se presenta un mensaje informativo "No hay OPPs registrados para esta carrera"
Y el botón "+ Nuevo OPP" permanece visible y habilitado en la esquina superior derecha
Y el campo de búsqueda está presente pero inactivo
Y NO se muestra el sistema de paginación
Y se ofrece la opción de crear el primer OPP mediante el botón "+ Nuevo OPP"
Y la interfaz mantiene la consistencia visual con otras pantallas del sistema
```

---

### **Criterio de Aceptación 4 (AC4 - RM1): Redirigir a login cuando no está autenticado**

```gherkin
Escenario 4: Denegar acceso y redirigir a login cuando el usuario no está autenticado como Coordinador
Dado que NO tengo una sesión activa en el sistema como Coordinador de Carrera
O tengo una sesión activa pero con un rol diferente (Profesor, Autoridad Académica, CEI, Administrador)
Cuando intento acceder directamente a la URL "Gestión de Objetivos de Carrera (OPP)"
Entonces el sistema me redirige automáticamente a la página de inicio de sesión
Y se muestra la pantalla "Iniciar Sesión" con el logo POLIACREDITA
Y aparece el mensaje "Introduce tus credenciales para acceder a Poliacredita"
Y se presentan los campos "Correo Institucional" y "Contraseña"
Y se muestra el dropdown "Rol" con las opciones disponibles
Y aparece el botón "Iniciar Sesión" de color azul
Y se visualiza el enlace "¿Olvidaste tu contraseña?"
Y NO se permite el acceso a la funcionalidad sin autenticación válida como Coordinador
Y se preserva la URL solicitada para redirigir después del login exitoso
```

---

## 🎯 **PASO 6: IDENTIFICAR EL CRITERIO DE ACEPTACIÓN MÁS CRÍTICO**

### **Criterio de Aceptación Más Crítico:**

**AC1 (Escenario 1): Listar todos los OPPs de la carrera**

---

### **🔥 JUSTIFICACIÓN DETALLADA DE CRITICIDAD:**

El **Criterio de Aceptación 1** es el más crítico de esta Historia de Usuario por las siguientes **15 razones fundamentales**:

1. **Cumple el objetivo central de la HU**: La HU establece textualmente "Quiero **listar** los Objetivos de Programa", y este AC es el único que valida directamente la capacidad de visualizar el listado completo de OPPs, que es exactamente el valor que el usuario (Coordinador) necesita.

2. **Happy Path principal**: Según las imágenes del prototipo (especialmente Imagen 2), este es el flujo de éxito esperado y el escenario más común de uso. Los coordinadores necesitan primero ver **todos** sus OPPs para poder gestionarlos.

3. **Prerequisito para gestión efectiva**: La HU indica "Para gestionar los objetivos de mi carrera". Sin poder visualizar el listado completo, el coordinador no puede:
   - Revisar los OPPs existentes
   - Identificar OPPs que necesitan edición
   - Planificar la creación de nuevos OPPs
   - Validar la cobertura curricular
   - Detectar OPPs duplicados o inconsistentes

4. **Fundamento del perfil profesional**: Los OPPs representan el **perfil profesional de la carrera** (perfil de egreso desde la perspectiva de las competencias profesionales). Este AC valida que el coordinador pueda acceder a la visión completa del perfil profesional que define su programa académico.

5. **Base para acreditación nacional e internacional**: Los OPPs son requisito obligatorio en procesos de acreditación como CACES (Ecuador) y EUR-ACE (Europa). Sin la visualización completa, el coordinador no puede:
   - Preparar evidencias para auditorías
   - Verificar cobertura de competencias profesionales
   - Documentar el perfil de egreso institucional
   - Demostrar alineación con estándares internacionales

6. **Trazabilidad curricular completa**: La Imagen 12 muestra la matriz OPP vs RA, demostrando que los OPPs son el punto inicial de la cadena de trazabilidad:
   - **OPP** → RA → Asignaturas → Actividades → Instrumentos de evaluación
   
   Sin visualizar los OPPs correctamente, toda la estructura de trazabilidad se vuelve inaccesible.

7. **Validación de elementos de UI críticos**: Este AC es el único que valida **todos los elementos visuales principales** mostrados en el prototipo:
   - Estructura de tabla con 3 columnas
   - Códigos de OPP (OPP1, OPP2, etc.)
   - Descripciones completas
   - Íconos de acción (editar/eliminar)
   - Sistema de paginación
   - Botón "+ Nuevo OPP"
   - Campo de búsqueda

8. **Volumen de datos esperado**: A diferencia de AC3 (lista vacía), este AC valida el comportamiento con datos reales. Los programas académicos típicamente tienen entre 5-15 OPPs, por lo que este es el escenario de producción real.

9. **Punto de entrada para funcionalidades posteriores**: Las imágenes muestran que desde esta vista el coordinador puede:
   - Crear nuevos OPPs (botón "+ Nuevo OPP" - Imágenes 3-5)
   - Editar OPPs existentes (ícono de lápiz)
   - Eliminar OPPs obsoletos (ícono de papelera)
   - Buscar OPPs específicos (AC2)
   - Navegar a matrices de relación (Imagen 12)

10. **Diferenciación institucional crítica**: La Imagen 12 muestra que el sistema diferencia entre:
    - **OPP (Objetivos de Programa)**: Perfil profesional
    - **RA (Resultados de Aprendizaje)**: Perfil de egreso
    
    Este AC valida que los OPPs se muestren correctamente con su nomenclatura específica (OPP1, OPP2, etc.), no confundiéndolos con RA o EUR-ACE.

11. **Contexto de usuario específico**: La Imagen 1 muestra que el sistema tiene múltiples roles (Administrador, Coordinador, CEI, Autoridad, Profesor). Este AC valida que **solo el Coordinador de Carrera** tiene acceso a gestionar los OPPs de **su** carrera específica.

12. **Navegación funcional del sistema**: El menú lateral de la Imagen 2 muestra que "Objetivos de Carrera" es una sección principal del sistema. Si este AC falla, toda la sección principal se vuelve inaccesible.

13. **Paginación como requisito funcional**: El prototipo muestra explícitamente paginación (Previous, 1, 2, 3, Next). Esto indica que:
    - Algunas carreras tendrán más de 5-10 OPPs
    - El sistema debe manejar múltiples páginas de datos
    - La performance debe ser óptima incluso con muchos OPPs

14. **Integración con otros módulos**: Las Imágenes 6-11 muestran que los OPPs se relacionan con:
    - Resultados de Aprendizaje (RG y RE)
    - Criterios EUR-ACE
    - Matrices de mapeo
    
    Sin poder visualizar OPPs, estas integraciones no funcionan.

15. **Consistencia de datos mostrados**: Este AC valida que:
    - Cada OPP muestra exactamente la información correcta
    - Los códigos son únicos y secuenciales
    - Las descripciones son las almacenadas en la base de datos
    - Las acciones están correctamente asociadas a cada OPP
    - No hay datos corruptos o duplicados en la vista

---

### **📊 IMPACTO DE FALLO DEL AC1:**

Si este Criterio de Aceptación falla:

**Impacto en el Usuario:**
- El Coordinador no puede revisar los OPPs de su carrera
- No puede identificar qué OPPs existen para editarlos o eliminarlos
- Pierde visibilidad completa del perfil profesional del programa

**Impacto en el Sistema:**
- La funcionalidad principal de la HU queda inutilizable
- Se bloquea el acceso a matrices de relación (OPP vs RA)
- Se impide la trazabilidad curricular completa
- Se compromete la preparación de documentación de acreditación

**Impacto en el Negocio:**
- Riesgo de incumplimiento de requisitos de acreditación
- Imposibilidad de gestionar el perfil profesional de la carrera
- Bloqueo de la planificación curricular basada en OPPs
- Pérdida de capacidad de evidenciar competencias profesionales

---

**CONCLUSIÓN:**

El **AC1 es absolutamente crítico** porque valida la funcionalidad central que permite al Coordinador de Carrera **listar y visualizar los Objetivos de Programa (OPPs)** de su carrera, que representan el **perfil profesional completo del programa académico**. Esta visualización es **prerequisito fundamental** para la gestión curricular, la preparación de evidencias de acreditación, la trazabilidad de competencias profesionales, y el cumplimiento de requisitos institucionales y de organismos acreditadores. Sin este AC funcionando, el coordinador pierde acceso a la información más importante para gestionar el diseño y la evaluación del perfil de egreso de su programa, comprometiendo la calidad académica y la capacidad de demostrar conformidad con estándares nacionales e internacionales.

---

**FIN DEL ANÁLISIS COMPLETO** ✅