# ANÁLISIS COMPLETO - HU: Visualizar Matriz de Mapeo OPP vs RA

---

## 📋 **PASO 1: ANÁLISIS VISUAL EXHAUSTIVO DE IMÁGENES DEL PROTOTIPO**

### **🔍 ELEMENTOS DE UI IDENTIFICADOS EN LAS IMÁGENES:**

#### **Imagen 12 - Matriz: Objetivos de Carrera (OPP) y Resultados de Aprendizaje (RA):**

**Componentes de UI principales:**

1. **Header de página:**
   - Título principal: "Matriz: Objetivos de Carrera (OPP) y Resultados de aprendizaje (RA)" (tipografía grande, negrita)
   - Subtítulo descriptivo: "La tabla muestra la relación entre los objetivos de carrera (perfil profesional) y los resultados de aprendizaje (perfil de egreso) de una carrera."
   - Botón "+ Nueva Relación" (color azul oscuro, esquina superior derecha)

2. **Sistema de pestañas:**
   - **Pestaña 1**: "Objetivos de Carrera" (activa, con fondo azul sólido y checkbox marcado)
   - **Pestaña 2**: "Resultados de Aprendizaje Carrera"
   - Indicador visual de pestaña activa muy claro

3. **Tooltip/Descripción contextual:**
   - Cuadro de texto flotante en la parte superior derecha
   - Contiene descripción detallada de un objetivo
   - Texto visible: "Ser capaz de identificar las necesidades de los sectores estratégicos públicos o privados del país, que requieren una solución a través de productos de software eficientes y costo-efectivos."
   - Diseño: Fondo blanco, texto negro, posicionado sobre la matriz

4. **Matriz bidimensional (estructura de tabla):**
   
   **Eje Vertical (Filas) - Objetivos de Programa (OPP):**
   - Código: **OP1** con ícono de información (ⓘ)
   - Código: **OP2** con ícono de información (ⓘ)
   - Código: **OP3** con ícono de información (ⓘ)
   - Código: **OP4** con ícono de información (ⓘ)
   - Código: **OP5** con ícono de información (ⓘ)
   - Código: **OP6** con ícono de información (ⓘ)
   - Código: **OP7** con ícono de información (ⓘ)
   - **Color de fondo**: Azul oscuro (#2c5282 aprox.)
   - **Posición**: Columna fija izquierda

   **Eje Horizontal (Columnas) - Resultados de Aprendizaje:**
   - **RG1** con ícono (ⓘ) - Resultado General 1
   - **RG2** con ícono (ⓘ) - Resultado General 2
   - **RG3** con ícono (ⓘ) - Resultado General 3
   - **RE1** con ícono (ⓘ) - Resultado Específico 1
   - **RE2** con ícono (ⓘ) - Resultado Específico 2
   - **RE3** con ícono (ⓘ) - Resultado Específico 3
   - **RE4** con ícono (ⓘ) - Resultado Específico 4
   - **RE5** con ícono (ⓘ) - Resultado Específico 5
   - **RE6** con ícono (ⓘ) - Resultado Específico 6
   - **RE7** con ícono (ⓘ) - Resultado Específico 7 (parcialmente visible, extremo derecho)
   - **Color de fondo**: Gris (#718096 aprox.)
   - **Posición**: Fila de encabezado superior

5. **Celdas de intersección (relaciones):**
   
   **Celdas CON relación (relación existente):**
   - Color de fondo: **Verde turquesa/menta** (#81C995 o #4FD1C5 aprox.)
   - Ícono: **Checkmark blanco (✓)** centrado
   - Estado visual: Celda completa rellena de color
   
   **Celdas SIN relación:**
   - Color de fondo: **Blanco** o gris muy claro
   - Sin ícono
   - Estado: Vacía/sin contenido

6. **Relaciones específicas observadas en el prototipo:**
   - **OP1 ↔ RE1**: Relación existente (✓ verde)
   - **OP2 ↔ RE2**: Relación existente (✓ verde)
   - **OP3 ↔ RG2**: Relación existente (✓ verde)
   - **OP4 ↔ RG3**: Relación existente (✓ verde)
   - **OP5 ↔ RE3**: Relación existente (✓ verde)
   - **OP6 ↔ RG1**: Relación existente (✓ verde)
   - **OP6 ↔ RE4**: Relación existente (✓ verde)
   - **OP7 ↔ RE7**: Relación existente (✓ verde) - extremo derecho

7. **Íconos de información (ⓘ):**
   - Clickeables junto a cada código
   - Al hacer hover o clic, muestran tooltip con descripción completa
   - Presentes en TODOS los códigos de OPP y RA

---

#### **Imagen 16 - Matriz después de crear relación (con notificación):**

**Elementos adicionales identificados:**

1. **Notificación de éxito:**
   - Ubicación: Esquina superior derecha
   - Ícono: Checkmark verde (✓) en círculo
   - Texto: "**Completado**"
   - Subtexto: "Se agregó la relación correctamente"
   - Color de fondo: Blanco con borde verde
   - Botón cerrar (X) en la esquina de la notificación

2. **Nueva celda verde visible:**
   - Indica que se acaba de crear una nueva relación
   - Se integra visualmente con las relaciones existentes

---

### **🎯 COMPORTAMIENTOS OBSERVADOS:**

1. **Visualización matricial bidimensional completa**: Muestra todas las relaciones entre OPP y RA simultáneamente
2. **Diferenciación visual inmediata**: Celdas verdes con ✓ indican relaciones, celdas blancas indican ausencia
3. **Tooltip contextual dinámico**: Al interactuar con íconos (ⓘ), se muestra descripción completa
4. **Sistema de pestañas bidireccional**: Permite alternar entre vista OPP→RA y RA→OPP
5. **Feedback visual de acciones**: Notificación de éxito confirma creación de relaciones
6. **Inclusión de ambos tipos de RA**: Muestra RG (Generales) y RE (Específicos) en la misma matriz
7. **Scroll horizontal disponible**: Matriz se extiende más allá del viewport (RE7 visible en extremo)
8. **Acceso a creación de relaciones**: Botón "+ Nueva Relación" siempre visible

---

### **📊 CONDICIONES IDENTIFICADAS:**

Basándome en el análisis visual de las imágenes y la HU:

**C1: Existencia de relaciones OPP-RA en el sistema**
- **Valor TRUE**: Existen una o más relaciones establecidas entre OPP y RA
- **Valor FALSE**: No existen relaciones establecidas (matriz vacía)

**C2: Usuario autenticado como Coordinador de Carrera**
- **Valor TRUE**: Usuario tiene rol de Coordinador y sesión activa
- **Valor FALSE**: Usuario no autenticado o rol diferente

**C3: Tipo de vista de la matriz**
- **Valor TRUE**: Vista desde pestaña "Objetivos de Carrera" (OPP en filas, RA en columnas)
- **Valor FALSE**: Vista desde pestaña "Resultados de Aprendizaje Carrera" (RA en filas, OPP en columnas)

---

## 📊 **PASO 2: CREAR TABLA DE DECISIÓN COMPLETA (MAXIMIZADA)**

### **Condiciones identificadas:**
- **C1**: Existen relaciones OPP-RA (TRUE/FALSE)
- **C2**: Usuario autenticado como Coordinador (TRUE/FALSE)
- **C3**: Vista desde pestaña OPP activa (TRUE/FALSE)

### **Cálculo de combinaciones:**
**2^3 = 8 reglas teóricas**

### **TABLA DE DECISIÓN COMPLETA:**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Existen relaciones OPP-RA** | T | T | T | T | F | F | F | F |
| **C2: Usuario es Coordinador** | T | T | F | F | T | T | F | F |
| **C3: Vista OPP activa** | T | F | T | F | T | F | T | F |
| **ACCIÓN RESULTANTE** | **A1** | **A2** | **A3** | **A3** | **A4** | **A5** | **A3** | **A3** |

### **ACCIONES:**

- **A1**: Mostrar matriz OPP vs RA con relaciones visualizadas (celdas verdes con ✓)
- **A2**: Mostrar matriz RA vs OPP con relaciones visualizadas (matriz transpuesta)
- **A3**: Redirigir a login (acceso denegado)
- **A4**: Mostrar matriz OPP vs RA vacía (sin relaciones)
- **A5**: Mostrar matriz RA vs OPP vacía (sin relaciones, vista transpuesta)

---

## 🔄 **PASO 3: CREAR TABLA DE DECISIÓN MINIMIZADA**

### **Análisis de Minimización:**

**Observaciones:**

1. **R3, R4, R7, R8**: Todas las reglas donde C2=FALSE (usuario no es coordinador) producen la misma acción **A3** (redirigir a login), independientemente de C1 y C3

2. **R1**: Usuario coordinador, existen relaciones, vista OPP activa → **A1** (matriz con datos desde perspectiva OPP)

3. **R2**: Usuario coordinador, existen relaciones, vista RA activa → **A2** (matriz con datos desde perspectiva RA - transpuesta)

4. **R5**: Usuario coordinador, no existen relaciones, vista OPP activa → **A4** (matriz vacía OPP)

5. **R6**: Usuario coordinador, no existen relaciones, vista RA activa → **A5** (matriz vacía RA)

**Minimización:**

- **R3, R4, R7, R8** → **RM1**: `- FALSE -` → A3 (redirigir a login)
- **R1** → **RM2**: `TRUE TRUE TRUE` → A1 (matriz OPP con datos)
- **R2** → **RM3**: `TRUE TRUE FALSE` → A2 (matriz RA con datos - transpuesta)
- **R5** → **RM4**: `FALSE TRUE TRUE` → A4 (matriz OPP vacía)
- **R6** → **RM5**: `FALSE TRUE FALSE` → A5 (matriz RA vacía)

### **TABLA DE DECISIÓN MINIMIZADA:**

| **Regla Minimizada** | **RM1** | **RM2** | **RM3** | **RM4** | **RM5** |
|----------------------|---------|---------|---------|---------|---------|
| **C1: Existen relaciones OPP-RA** | - | TRUE | TRUE | FALSE | FALSE |
| **C2: Usuario es Coordinador** | FALSE | TRUE | TRUE | TRUE | TRUE |
| **C3: Vista OPP activa** | - | TRUE | FALSE | TRUE | FALSE |
| **ACCIÓN RESULTANTE** | **A3** | **A1** | **A2** | **A4** | **A5** |

**Reglas minimizadas: 5**
**Criterios de Aceptación necesarios: 5**

---

## ✅ **PASO 4: DECLARAR NÚMERO FINAL DE CRITERIOS DE ACEPTACIÓN**

**Número total de Criterios de Aceptación:** **5 (cinco)**

Basándome en la tabla de decisión minimizada, se requieren exactamente **5 Criterios de Aceptación** que corresponden a las 5 reglas minimizadas:

1. **AC1 (RM2)**: Visualizar matriz OPP vs RA con relaciones existentes (Vista OPP) - **Happy Path**
2. **AC2 (RM3)**: Visualizar matriz RA vs OPP con relaciones existentes (Vista RA transpuesta)
3. **AC3 (RM4)**: Visualizar matriz OPP vacía cuando no hay relaciones
4. **AC4 (RM5)**: Visualizar matriz RA vacía cuando no hay relaciones
5. **AC5 (RM1)**: Redirigir a login cuando no está autenticado como Coordinador

**Nota sobre criterios eliminados:** 

Al revisar otras HUs similares del sistema:
- **HU "Visualizar Mapeo RA vs EUR-ACE"** (Imagen 17): Aunque tiene estructura matricial similar, NO se eliminan criterios porque los datos son completamente diferentes (EUR-ACE vs OPP, códigos 5.X.X vs OPP#)
- **HU "Visualizar OPP"** (Imagen 2): Es una lista simple, no una matriz, por lo que no hay solapamiento
- **HU "Visualizar RA"** (Imágenes 9-10): También es lista con pestañas, no matriz bidimensional

**NO SE ELIMINAN CRITERIOS** porque esta HU es única en su funcionalidad: es la única matriz que relaciona **Objetivos de Programa (perfil profesional)** con **Resultados de Aprendizaje (perfil de egreso)**, que es la alineación curricular fundamental del programa académico.

Por lo tanto, los 5 criterios son únicos y necesarios para esta HU específica.

---

## 📝 **PASO 5: GENERAR CRITERIOS DE ACEPTACIÓN EN FORMATO GHERKIN**

### **Criterio de Aceptación 1 (AC1 - RM2): Visualizar matriz OPP vs RA con relaciones (Vista OPP)**

```gherkin
Escenario 1: Visualizar matriz de mapeo OPP-RA desde pestaña Objetivos de Carrera
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y existen relaciones establecidas entre Objetivos de Programa y Resultados de Aprendizaje para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs OPP"
Cuando accedo a la matriz desde la pestaña "Objetivos de Carrera"
Entonces el sistema muestra el título "Matriz: Objetivos de Carrera (OPP) y Resultados de aprendizaje (RA)"
Y se presenta el subtítulo "La tabla muestra la relación entre los objetivos de carrera (perfil profesional) y los resultados de aprendizaje (perfil de egreso) de una carrera."
Y la pestaña "Objetivos de Carrera" aparece activa con fondo azul sólido y checkbox marcado
Y el botón "+ Nueva Relación" se visualiza en color azul oscuro en la esquina superior derecha
Y la matriz muestra en el eje vertical (filas) los Objetivos de Programa con formato "OP#" en recuadros azules oscuros
Y cada código OPP incluye un ícono de información (ⓘ) clickeable
Y la matriz muestra en el eje horizontal (columnas) los Resultados de Aprendizaje (RG y RE) en recuadros grises
Y cada código de RA incluye un ícono de información (ⓘ) clickeable
Y las celdas donde existe una relación establecida se muestran en color verde turquesa/menta con un checkmark blanco (✓) centrado
Y las celdas sin relación aparecen vacías de color blanco
Y se incluyen tanto Resultados Generales (RG1, RG2, RG3) como Resultados Específicos (RE1, RE2, RE3, etc.) en la misma matriz
Y la matriz permite scroll horizontal para visualizar todos los RAs disponibles
Y al hacer clic en un ícono (ⓘ), se muestra un tooltip flotante con la descripción completa del objetivo o resultado
Y el tooltip aparece con fondo blanco, texto negro, posicionado sobre la matriz
Y la visualización se actualiza sin recargar la página completa
```

---

### **Criterio de Aceptación 2 (AC2 - RM3): Visualizar matriz desde pestaña Resultados de Aprendizaje (transpuesta)**

```gherkin
Escenario 2: Visualizar matriz de mapeo OPP-RA desde pestaña Resultados de Aprendizaje Carrera
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y existen relaciones establecidas entre Objetivos de Programa y Resultados de Aprendizaje para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs OPP"
Cuando hago clic en la pestaña "Resultados de Aprendizaje Carrera"
Entonces el sistema muestra la matriz con la vista transpuesta
Y la pestaña "Resultados de Aprendizaje Carrera" aparece activa con indicador visual
Y la pestaña "Objetivos de Carrera" aparece inactiva sin fondo azul sólido
Y la matriz muestra en el eje vertical (filas) los Resultados de Aprendizaje (RG y RE)
Y la matriz muestra en el eje horizontal (columnas) los Objetivos de Programa con formato "OP#"
Y las mismas relaciones establecidas se visualizan con celdas verdes turquesa/menta y checkmark blanco (✓)
Y los íconos de información (ⓘ) permanecen disponibles en todos los códigos
Y los tooltips funcionan correctamente mostrando descripciones completas
Y el botón "+ Nueva Relación" permanece visible y habilitado
Y el título y subtítulo de la matriz se mantienen sin cambios
Y la transición entre pestañas ocurre de forma fluida sin recarga completa de página
Y todas las funcionalidades de información y navegación permanecen activas
```

---

### **Criterio de Aceptación 3 (AC3 - RM4): Visualizar matriz OPP vacía cuando no hay relaciones**

```gherkin
Escenario 3: Mostrar matriz vacía cuando no existen relaciones establecidas (Vista OPP)
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y NO existen relaciones establecidas entre Objetivos de Programa y Resultados de Aprendizaje para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs OPP"
Cuando accedo a la matriz desde la pestaña "Objetivos de Carrera"
Entonces el sistema muestra la estructura completa de la matriz
Y el título "Matriz: Objetivos de Carrera (OPP) y Resultados de aprendizaje (RA)" se visualiza correctamente
Y se presenta el subtítulo descriptivo sobre perfil profesional y perfil de egreso
Y la matriz muestra todos los Objetivos de Programa disponibles en el eje vertical (OP1, OP2, OP3, etc.)
Y la matriz muestra todos los Resultados de Aprendizaje disponibles en el eje horizontal (RG1, RG2, RG3, RE1, RE2, etc.)
Y TODAS las celdas de intersección aparecen vacías de color blanco sin checkmarks
Y NO hay ninguna celda con color verde turquesa/menta
Y los íconos de información (ⓘ) permanecen disponibles y funcionales
Y los tooltips con descripciones funcionan correctamente
Y el botón "+ Nueva Relación" está visible y habilitado para crear la primera relación
Y se muestra un mensaje informativo "No hay relaciones establecidas. Haga clic en + Nueva Relación para crear una."
Y la interfaz permite scroll para visualizar toda la estructura de la matriz
```

---

### **Criterio de Aceptación 4 (AC4 - RM5): Visualizar matriz RA vacía cuando no hay relaciones**

```gherkin
Escenario 4: Mostrar matriz vacía cuando no existen relaciones (Vista RA transpuesta)
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y NO existen relaciones establecidas entre Objetivos de Programa y Resultados de Aprendizaje para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs OPP"
Cuando accedo a la matriz desde la pestaña "Resultados de Aprendizaje Carrera"
Entonces el sistema muestra la matriz con vista transpuesta
Y la pestaña "Resultados de Aprendizaje Carrera" aparece activa
Y la matriz muestra todos los Resultados de Aprendizaje en el eje vertical (filas)
Y la matriz muestra todos los Objetivos de Programa en el eje horizontal (columnas)
Y TODAS las celdas de intersección aparecen vacías sin checkmarks verdes
Y NO hay ninguna celda con color verde turquesa/menta
Y los íconos de información (ⓘ) permanecen disponibles en ambos ejes
Y los tooltips funcionan correctamente para todos los elementos
Y el botón "+ Nueva Relación" está visible y habilitado
Y se mantiene el mensaje informativo sobre la ausencia de relaciones
Y la funcionalidad de cambio entre pestañas permanece activa
Y el usuario puede crear la primera relación haciendo clic en "+ Nueva Relación"
```

---

### **Criterio de Aceptación 5 (AC5 - RM1): Redirigir a login cuando no está autenticado**

```gherkin
Escenario 5: Denegar acceso y redirigir a login cuando el usuario no está autenticado como Coordinador
Dado que NO tengo una sesión activa en el sistema como Coordinador de Carrera
O tengo una sesión activa pero con un rol diferente (Profesor, Autoridad Académica, CEI, Administrador)
Cuando intento acceder directamente a la URL "Editor Mapeos" → "RA vs OPP"
Entonces el sistema me redirige automáticamente a la página de inicio de sesión
Y se muestra la pantalla "Iniciar Sesión" con el logo POLIACREDITA
Y aparece el mensaje "Introduce tus credenciales para acceder a Poliacredita"
Y se presentan los campos "Correo Institucional" y "Contraseña"
Y se muestra el dropdown "Rol" con las opciones disponibles
Y aparece el botón "Iniciar Sesión" de color azul
Y se visualiza el enlace "¿Olvidaste tu contraseña?"
Y NO se permite el acceso a la matriz de mapeo sin autenticación válida como Coordinador
Y se preserva la URL solicitada para redirigir después del login exitoso
Y se mantiene la seguridad del sistema bloqueando accesos no autorizados
```

---

## 🎯 **PASO 6: IDENTIFICAR EL CRITERIO DE ACEPTACIÓN MÁS CRÍTICO**

### **Criterio de Aceptación Más Crítico:**

**AC1 (Escenario 1): Visualizar matriz de mapeo OPP-RA desde pestaña Objetivos de Carrera**

---

### **🔥 JUSTIFICACIÓN DETALLADA DE CRITICIDAD:**

El **Criterio de Aceptación 1** es el más crítico de esta Historia de Usuario por las siguientes **20 razones fundamentales**:

1. **Cumple el objetivo central de la HU**: La HU establece textualmente "Quiero **visualizar las relaciones** de los Objetivos de Programa con Resultados de Aprendizaje", y este AC es el único que valida directamente la capacidad de visualizar todas las relaciones en formato matricial, que es exactamente el valor que el usuario necesita.

2. **Happy Path principal según prototipo**: La Imagen 12 muestra explícitamente este escenario como el flujo de éxito esperado: matriz completa con múltiples relaciones establecidas (al menos 8 visibles), vista desde la pestaña "Objetivos de Carrera" activa con checkbox marcado y fondo azul.

3. **Comprensión visual de alineación curricular completa**: La HU indica "Para comprender visualmente la alineación curricular de mi carrera". Este AC valida que el coordinador pueda ver la alineación completa entre:
   - **OPP (Perfil Profesional)**: Lo que la carrera promete formar
   - **RA (Perfil de Egreso)**: Cómo se evidencia esa formación
   
   Esta es la alineación curricular más fundamental en el diseño de programas académicos.

4. **Relación crítica entre dos perfiles estratégicos**: El subtítulo del prototipo define explícitamente:
   - **Objetivos de Carrera** = "perfil profesional"
   - **Resultados de Aprendizaje** = "perfil de egreso"
   
   Esta relación es el núcleo de la coherencia curricular y diferencia claramente entre:
   - Lo que el programa **pretende lograr** (OPP)
   - Lo que los estudiantes **efectivamente demuestran** (RA)

5. **Requisito obligatorio para acreditación institucional**: Los organismos acreditadores (CACES en Ecuador, CNA en Colombia, CONEAU en Argentina) exigen demostrar trazabilidad entre:
   - Objetivos del programa → Resultados de aprendizaje → Asignaturas → Evaluaciones
   
   Sin esta matriz funcionando, no hay forma de evidenciar esta trazabilidad obligatoria.

6. **Validación de coherencia horizontal del currículo**: Este AC permite al coordinador verificar que:
   - Cada OPP tiene al menos un RA que lo evidencia
   - No hay OPPs "huérfanos" sin resultados medibles
   - Los RAs cubren todos los OPPs declarados
   - La distribución de relaciones es equilibrada

7. **Diferenciación crítica entre RG y RE en contexto OPP**: El AC valida que la matriz muestra AMBOS tipos de resultados:
   - **RG (Resultados Generales)**: Competencias transversales que también deben alinearse con objetivos profesionales
   - **RE (Resultados Específicos)**: Competencias técnicas específicas de la carrera
   
   Esto permite entender cómo tanto competencias genéricas como específicas contribuyen al perfil profesional.

8. **Tooltips como elemento educativo crítico**: El AC valida los tooltips flotantes (visible en Imagen 12) que muestran descripciones completas. Ejemplo observado:
   - Texto: "Ser capaz de identificar las necesidades de los sectores estratégicos públicos o privados del país, que requieren una solución a través de productos de software eficientes y costo-efectivos."
   
   Estos tooltips son esenciales porque los códigos OPP# y RG#/RE# por sí solos no son autoexplicativos.

9. **Visualización matricial única y superior**: A diferencia de listas o reportes, la matriz bidimensional permite:
   - Ver TODAS las relaciones simultáneamente en una sola pantalla
   - Identificar patrones de cobertura visualmente
   - Detectar concentraciones o vacíos en la alineación
   - Comparar qué RAs contribuyen a cada OPP
   - Analizar distribución de competencias en el perfil

10. **Codificación de colores para comprensión inmediata**: El AC valida el sistema de colores:
    - **Verde turquesa + ✓ blanco**: Relación establecida y documentada
    - **Blanco vacío**: No hay relación (posible gap curricular)
    
    Esta codificación permite identificar instantáneamente fortalezas y debilidades del diseño curricular.

11. **Volumen de datos representativo real**: El prototipo muestra 7 OPPs (OP1-OP7) relacionados con 10 RAs (RG1-RG3, RE1-RE7), con al menos 8 relaciones establecidas. Esto representa un programa académico real de tamaño medio, no un caso de prueba trivial.

12. **Inclusión explícita de ambos tipos de RA**: El hecho de que la matriz incluya tanto RG como RE en las mismas columnas es significativo porque:
    - Refleja la realidad del modelo educativo basado en competencias
    - Permite ver cómo objetivos profesionales requieren tanto competencias genéricas como específicas
    - Facilita análisis de balance entre formación técnica y transversal

13. **Sistema de pestañas para perspectivas duales**: Aunque este AC se enfoca en vista OPP, valida la existencia del sistema de pestañas que permite dos análisis complementarios:
    - Vista OPP (filas): "¿Qué RAs evidencian cada objetivo profesional?"
    - Vista RA (columnas): "¿A qué objetivos profesionales contribuye cada resultado?"
    
    Ambas perspectivas son necesarias para análisis curricular completo.

14. **Scroll horizontal para escalabilidad**: El AC valida que la matriz soporta scroll, lo cual indica que:
    - El sistema puede manejar programas con muchos RAs (visible hasta RE7 y probablemente más)
    - La interfaz es escalable a diferentes tamaños de carreras
    - No hay limitaciones artificiales en el número de relaciones visualizables

15. **Botón "+ Nueva Relación" accesible siempre**: El AC valida que después de visualizar relaciones existentes, el coordinador tiene acceso inmediato a crear nuevas si identifica gaps. Este flujo (visualizar → analizar → corregir) es el proceso natural de mejora curricular.

16. **Notificación de feedback inmediato**: La Imagen 16 muestra notificación "Completado - Se agregó la relación correctamente" con checkmark verde, confirmando que las acciones del usuario se reflejan inmediatamente en la matriz, cerrando el ciclo de feedback.

17. **Nomenclatura institucional específica**: El AC valida códigos específicos:
    - **OP# (no OPP#)**: Objetivos de Programa
    - **RG#**: Resultados Generales
    - **RE#**: Resultados Específicos
    
    Esta nomenclatura diferencia claramente los elementos y facilita la comunicación institucional.

18. **Base para generación de reportes de trazabilidad**: Esta matriz es típicamente el punto de partida para:
    - Reportes de cobertura curricular
    - Matrices de trazabilidad completas (OPP→RA→Asignaturas→Evaluaciones)
    - Documentos de autoevaluación para acreditación
    - Análisis de brechas en el diseño curricular

19. **Integración con workflow completo de justificación**: Las Imágenes 13-15 muestran que cada relación requiere un wizard de 3 pasos con justificación detallada. Este AC valida que todas esas relaciones documentadas se visualizan correctamente en la matriz final.

20. **Diferenciación respecto a matriz EUR-ACE**: Aunque existe otra matriz (RA vs EUR-ACE de la Imagen 17), esta matriz OPP vs RA es ÚNICA porque:
    - Mapea elementos internos de la institución (no externos como EUR-ACE)
    - Es la primera capa de trazabilidad (la más cercana al diseño curricular)
    - Requiere mayor revisión y ajuste durante el ciclo de vida del programa
    - Es prerequisito para matrices de niveles superiores

---

### **📊 IMPACTO DE FALLO DEL AC1:**

Si este Criterio de Aceptación falla:

**Impacto en el Usuario:**
- El Coordinador no puede visualizar las relaciones OPP-RA existentes
- No puede evaluar la alineación entre perfil profesional y perfil de egreso
- Pierde visibilidad sobre qué RAs evidencian cada objetivo profesional
- No puede identificar gaps en la cobertura de objetivos del programa

**Impacto en el Sistema:**
- La funcionalidad principal de la HU queda completamente inutilizable
- Se pierde la trazabilidad fundamental entre OPP y RA
- Se bloquea la capacidad de análisis de coherencia curricular
- Se impide la visualización completa de la alineación del programa

**Impacto en el Negocio:**
- **Riesgo crítico de pérdida de acreditación institucional**
- Imposibilidad de demostrar coherencia entre perfil profesional y perfil de egreso
- Incapacidad de evidenciar trazabilidad curricular obligatoria
- Bloqueo de preparación de documentos de autoevaluación
- Compromiso de la calidad del diseño curricular
- Pérdida de capacidad de detectar y corregir gaps curriculares
- Imposibilidad de justificar decisiones de diseño curricular ante auditores
- Riesgo de inconsistencias entre lo prometido (OPP) y lo logrado (RA)

---

**CONCLUSIÓN:**

El **AC1 es absolutamente crítico** porque valida la funcionalidad central que permite al Coordinador de Carrera **visualizar todas las relaciones establecidas entre Objetivos de Programa (perfil profesional) y Resultados de Aprendizaje (perfil de egreso)** en formato de matriz bidimensional interactiva con tooltips contextuales y codificación visual por colores. Esta visualización es **prerequisito fundamental e indispensable** para comprender y validar la alineación curricular del programa académico, que es la relación más importante en el diseño de cualquier carrera universitaria. Sin este AC funcionando, el coordinador pierde completamente la capacidad de evidenciar la coherencia entre lo que el programa promete formar profesionalmente (OPP) y cómo se mide efectivamente ese logro (RA), compromete el cumplimiento de requisitos obligatorios de acreditación que exigen demostrar esta trazabilidad, y pone en riesgo la calidad integral del diseño curricular al imposibilitar la detección y corrección de gaps en la cobertura de objetivos del programa. Esta matriz es el eslabón fundamental de la cadena de trazabilidad curricular completa y su fallo compromete todo el sistema de aseguramiento de calidad académica de la institución.

---

**FIN DEL ANÁLISIS COMPLETO** ✅