# ANÁLISIS COMPLETO - HU: Visualizar Mapeo RA vs EUR-ACE

---

## 📋 **PASO 1: ANÁLISIS VISUAL EXHAUSTIVO DE IMÁGENES DEL PROTOTIPO**

### **🔍 ELEMENTOS DE UI IDENTIFICADOS EN LAS IMÁGENES:**

#### **Imagen 17 - Matriz: Resultados de Aprendizaje (RA) y Criterios EUR-ACE:**

**Componentes de UI principales:**

1. **Header de página:**
   - Título principal: "Matriz: Resultados de Aprendizaje (RA) y Criterios EUR-ACE" (tipografía grande, negrita)
   - Subtítulo descriptivo: "La tabla muestra la relación entre los Resultados de Aprendizaje (RA) y los Criterios EUR-ACE."
   - Botón "+ Nueva Relación" (color azul oscuro, esquina superior derecha)

2. **Sistema de pestañas:**
   - **Pestaña 1**: "Criterio EUR-ACE" (activa, con subrayado azul)
   - **Pestaña 2**: "Resultados de Aprendizaje Carrera"
   - Indicador visual de pestaña activa

3. **Matriz bidimensional (estructura de tabla):**
   
   **Eje Vertical (Filas) - Criterios EUR-ACE:**
   - Código: **5.4.1** con ícono de información (ⓘ)
   - Código: **5.4.2** con ícono de información (ⓘ)
   - Código: **5.4.3** con ícono de información (ⓘ)
   - Código: **5.4.4** con ícono de información (ⓘ)
   - Código: **5.4.5** con ícono de información (ⓘ)
   - Código: **5.4.6** con ícono de información (ⓘ)
   - Código: **5.5.1** con ícono de información (ⓘ)
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
   - **RE7** con ícono (ⓘ) - Resultado Específico 7
   - **Color de fondo**: Gris (#718096 aprox.)
   - **Posición**: Fila de encabezado superior

4. **Celdas de intersección (relaciones):**
   
   **Celdas CON relación (relación existente):**
   - Color de fondo: **Verde turquesa** (#81C995 o #4FD1C5 aprox.)
   - Ícono: **Checkmark blanco (✓)** centrado
   - Estado visual: Celda completa rellena de color
   
   **Celdas SIN relación:**
   - Color de fondo: **Blanco** o gris muy claro
   - Sin ícono
   - Estado: Vacía/sin contenido

5. **Relaciones específicas observadas en el prototipo:**
   - **5.4.1 ↔ RE1**: Relación existente (✓ verde)
   - **5.4.2 ↔ RE2**: Relación existente (✓ verde)
   - **5.4.3 ↔ RG2**: Relación existente (✓ verde)
   - **5.4.4 ↔ RG3**: Relación existente (✓ verde)
   - **5.4.5 ↔ RE3**: Relación existente (✓ verde)
   - **5.4.6 ↔ RG1**: Relación existente (✓ verde)
   - **5.4.6 ↔ RE4**: Relación existente (✓ verde)
   - **5.5.1 ↔ RE7**: Relación existente (✓ verde) - extremo derecho

6. **Íconos de información (ⓘ):**
   - Clickeables junto a cada código
   - Permiten ver información detallada (tooltip o modal)
   - Presentes en TODOS los códigos de RA y EUR-ACE

---

#### **Imagen 11 - Criterios EUR-ACE (Referencia para descripciones):**

**Lista completa de Criterios EUR-ACE con descripciones:**

1. **5.4.1**: "La investigación en la solución de problemas complejos de ingeniería en el campo de estudio pertinente, incluyendo la formulación experimental, análisis e interpretación de datos utilizando conocimientos básicos y avanzados."

2. **5.4.2**: "Creación, selección y aplicación de los recursos y métodos necesarios, incluyendo la predicción y la modelación, técnicas modernas y herramientas de TI para resolver problemas complejos de ingeniería en el campo de estudio pertinente, teniendo en cuenta las posibles restricciones"

3. **5.4.3**: "La especialización y enfoque en el mercado de trabajo. Demostración de competencias relacionadas con los problemas, objetivos y tipos de actividades complejas de ingeniería específicos, correspondientes a la formación y el perfil de la dirección en las empresas y organizaciones -. Potenciales empleadores."

4. **5.4.4**: "Ingeniería práctica. Creación, selección y aplicación de los recursos y métodos necesarios, incluyendo la predicción y la modelación, técnicas modernas y herramientas de TI para resolver problemas complejos de ingeniería en el campo de estudio pertinente, teniendo en cuenta las posibles restricciones"

5. **5.4.5**: "La investigación en la solución de problemas complejos de ingeniería en el campo de estudio pertinente, incluyendo la formulación experimental, análisis e interpretación de datos utilizando conocimientos básicos y avanzados."

---

### **🎯 COMPORTAMIENTOS OBSERVADOS:**

1. **Visualización matricial bidimensional**: Permite ver todas las relaciones entre RA y EUR-ACE en una sola vista
2. **Diferenciación visual clara**: Celdas con relación (verde + ✓) vs sin relación (blanco)
3. **Navegación por pestañas**: Sistema permite alternar entre vistas de EUR-ACE y RA
4. **Información contextual accesible**: Íconos (ⓘ) permiten obtener detalles de cada elemento
5. **Acción de creación disponible**: Botón "+ Nueva Relación" permite agregar nuevas relaciones
6. **Scroll horizontal**: La matriz se extiende más allá del viewport (visible RE7 en extremo derecho)
7. **Inclusión de ambos tipos de RA**: La matriz incluye tanto RG (Resultados Generales) como RE (Resultados Específicos)

---

### **📊 CONDICIONES IDENTIFICADAS:**

Basándome en el análisis visual de las imágenes y la HU:

**C1: Existencia de relaciones RA-EUR-ACE en el sistema**
- **Valor TRUE**: Existen una o más relaciones establecidas entre RA y Criterios EUR-ACE
- **Valor FALSE**: No existen relaciones establecidas (matriz vacía)

**C2: Usuario autenticado como Coordinador de Carrera**
- **Valor TRUE**: Usuario tiene rol de Coordinador y sesión activa
- **Valor FALSE**: Usuario no autenticado o rol diferente

**C3: Tipo de vista de la matriz**
- **Valor TRUE**: Vista desde pestaña "Criterio EUR-ACE" (EUR-ACE en filas, RA en columnas)
- **Valor FALSE**: Vista desde pestaña "Resultados de Aprendizaje Carrera" (RA en filas, EUR-ACE en columnas)

---

## 📊 **PASO 2: CREAR TABLA DE DECISIÓN COMPLETA (MAXIMIZADA)**

### **Condiciones identificadas:**
- **C1**: Existen relaciones RA-EUR-ACE (TRUE/FALSE)
- **C2**: Usuario autenticado como Coordinador (TRUE/FALSE)
- **C3**: Vista desde pestaña EUR-ACE activa (TRUE/FALSE)

### **Cálculo de combinaciones:**
**2^3 = 8 reglas teóricas**

### **TABLA DE DECISIÓN COMPLETA:**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: Existen relaciones RA-EUR-ACE** | T | T | T | T | F | F | F | F |
| **C2: Usuario es Coordinador** | T | T | F | F | T | T | F | F |
| **C3: Vista EUR-ACE activa** | T | F | T | F | T | F | T | F |
| **ACCIÓN RESULTANTE** | **A1** | **A2** | **A3** | **A3** | **A4** | **A5** | **A3** | **A3** |

### **ACCIONES:**

- **A1**: Mostrar matriz EUR-ACE vs RA con relaciones visualizadas (celdas verdes con ✓)
- **A2**: Mostrar matriz RA vs EUR-ACE con relaciones visualizadas (matriz transpuesta)
- **A3**: Redirigir a login (acceso denegado)
- **A4**: Mostrar matriz EUR-ACE vs RA vacía (sin relaciones)
- **A5**: Mostrar matriz RA vs EUR-ACE vacía (sin relaciones, vista transpuesta)

---

## 🔄 **PASO 3: CREAR TABLA DE DECISIÓN MINIMIZADA**

### **Análisis de Minimización:**

**Observaciones:**

1. **R3, R4, R7, R8**: Todas las reglas donde C2=FALSE (usuario no es coordinador) producen la misma acción **A3** (redirigir a login), independientemente de C1 y C3

2. **R1**: Usuario coordinador, existen relaciones, vista EUR-ACE activa → **A1** (matriz con datos desde perspectiva EUR-ACE)

3. **R2**: Usuario coordinador, existen relaciones, vista RA activa → **A2** (matriz con datos desde perspectiva RA - transpuesta)

4. **R5**: Usuario coordinador, no existen relaciones, vista EUR-ACE activa → **A4** (matriz vacía EUR-ACE)

5. **R6**: Usuario coordinador, no existen relaciones, vista RA activa → **A5** (matriz vacía RA)

**Minimización:**

- **R3, R4, R7, R8** → **RM1**: `- FALSE -` → A3 (redirigir a login)
- **R1** → **RM2**: `TRUE TRUE TRUE` → A1 (matriz EUR-ACE con datos)
- **R2** → **RM3**: `TRUE TRUE FALSE` → A2 (matriz RA con datos - transpuesta)
- **R5** → **RM4**: `FALSE TRUE TRUE` → A4 (matriz EUR-ACE vacía)
- **R6** → **RM5**: `FALSE TRUE FALSE` → A5 (matriz RA vacía)

### **TABLA DE DECISIÓN MINIMIZADA:**

| **Regla Minimizada** | **RM1** | **RM2** | **RM3** | **RM4** | **RM5** |
|----------------------|---------|---------|---------|---------|---------|
| **C1: Existen relaciones RA-EUR-ACE** | - | TRUE | TRUE | FALSE | FALSE |
| **C2: Usuario es Coordinador** | FALSE | TRUE | TRUE | TRUE | TRUE |
| **C3: Vista EUR-ACE activa** | - | TRUE | FALSE | TRUE | FALSE |
| **ACCIÓN RESULTANTE** | **A3** | **A1** | **A2** | **A4** | **A5** |

**Reglas minimizadas: 5**
**Criterios de Aceptación necesarios: 5**

---

## ✅ **PASO 4: DECLARAR NÚMERO FINAL DE CRITERIOS DE ACEPTACIÓN**

**Número total de Criterios de Aceptación:** **5 (cinco)**

Basándome en la tabla de decisión minimizada, se requieren exactamente **5 Criterios de Aceptación** que corresponden a las 5 reglas minimizadas:

1. **AC1 (RM2)**: Visualizar matriz RA vs EUR-ACE con relaciones existentes (Vista EUR-ACE) - **Happy Path**
2. **AC2 (RM3)**: Visualizar matriz RA vs EUR-ACE con relaciones existentes (Vista RA transpuesta)
3. **AC3 (RM4)**: Visualizar matriz EUR-ACE vacía cuando no hay relaciones
4. **AC4 (RM5)**: Visualizar matriz RA vacía cuando no hay relaciones
5. **AC5 (RM1)**: Redirigir a login cuando no está autenticado como Coordinador

**Nota sobre criterios eliminados:** 

Al revisar otras HUs similares del sistema (como "Visualizar Matriz OPP vs RA" de la Imagen 12), se observa que existe un patrón visual similar de matriz bidimensional. Sin embargo, **NO se eliminan criterios** porque:

1. **Los datos son diferentes**: Esta matriz mapea RA ↔ EUR-ACE, mientras que la otra mapea OPP ↔ RA
2. **Los códigos son distintos**: EUR-ACE usa formato "5.4.X", mientras que OPP usa "OPP1, OPP2..."
3. **El propósito es diferente**: Esta HU evalúa alineación con estándares internacionales, la otra evalúa perfil profesional vs perfil de egreso
4. **Las justificaciones son únicas**: Cada relación requiere justificación específica según el contexto

Por lo tanto, los 5 criterios son únicos y necesarios para esta HU específica.

---

## 📝 **PASO 5: GENERAR CRITERIOS DE ACEPTACIÓN EN FORMATO GHERKIN**

### **Criterio de Aceptación 1 (AC1 - RM2): Visualizar matriz RA vs EUR-ACE con relaciones (Vista EUR-ACE)**

```gherkin
Escenario 1: Visualizar matriz de relaciones RA-EUR-ACE desde pestaña Criterio EUR-ACE
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y existen relaciones establecidas entre Resultados de Aprendizaje y Criterios EUR-ACE para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs EUR-ACE"
Cuando accedo a la matriz desde la pestaña "Criterio EUR-ACE"
Entonces el sistema muestra el título "Matriz: Resultados de Aprendizaje (RA) y Criterios EUR-ACE"
Y se presenta el subtítulo "La tabla muestra la relación entre los Resultados de Aprendizaje (RA) y los Criterios EUR-ACE."
Y la pestaña "Criterio EUR-ACE" aparece activa con subrayado azul
Y el botón "+ Nueva Relación" se visualiza en color azul oscuro en la esquina superior derecha
Y la matriz muestra en el eje vertical (filas) los Criterios EUR-ACE con formato "5.X.X" en recuadros azules oscuros
Y cada código EUR-ACE incluye un ícono de información (ⓘ) clickeable
Y la matriz muestra en el eje horizontal (columnas) los Resultados de Aprendizaje (RG y RE) en recuadros grises
Y cada código de RA incluye un ícono de información (ⓘ) clickeable
Y las celdas donde existe una relación establecida se muestran en color verde turquesa con un checkmark blanco (✓) centrado
Y las celdas sin relación aparecen vacías de color blanco o gris muy claro
Y se incluyen tanto Resultados Generales (RG1, RG2, RG3) como Resultados Específicos (RE1, RE2, RE3, etc.)
Y la matriz permite scroll horizontal para visualizar todos los RAs disponibles
Y al hacer clic en un ícono (ⓘ), se muestra información detallada del criterio o resultado correspondiente
Y la visualización se actualiza sin recargar la página completa
```

---

### **Criterio de Aceptación 2 (AC2 - RM3): Visualizar matriz desde pestaña Resultados de Aprendizaje (transpuesta)**

```gherkin
Escenario 2: Visualizar matriz de relaciones RA-EUR-ACE desde pestaña Resultados de Aprendizaje Carrera
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y existen relaciones establecidas entre Resultados de Aprendizaje y Criterios EUR-ACE para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs EUR-ACE"
Cuando hago clic en la pestaña "Resultados de Aprendizaje Carrera"
Entonces el sistema muestra la matriz con la vista transpuesta
Y la pestaña "Resultados de Aprendizaje Carrera" aparece activa con subrayado azul
Y la pestaña "Criterio EUR-ACE" aparece inactiva sin subrayado
Y la matriz muestra en el eje vertical (filas) los Resultados de Aprendizaje (RG y RE)
Y la matriz muestra en el eje horizontal (columnas) los Criterios EUR-ACE con formato "5.X.X"
Y las mismas relaciones establecidas se visualizan con celdas verdes turquesa y checkmark blanco (✓)
Y los íconos de información (ⓘ) permanecen disponibles en todos los códigos
Y el botón "+ Nueva Relación" permanece visible y habilitado
Y el título y subtítulo de la matriz se mantienen sin cambios
Y la transición entre pestañas ocurre de forma fluida sin recarga completa de página
Y todas las funcionalidades de información y navegación permanecen activas
```

---

### **Criterio de Aceptación 3 (AC3 - RM4): Visualizar matriz EUR-ACE vacía cuando no hay relaciones**

```gherkin
Escenario 3: Mostrar matriz vacía cuando no existen relaciones establecidas (Vista EUR-ACE)
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y NO existen relaciones establecidas entre Resultados de Aprendizaje y Criterios EUR-ACE para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs EUR-ACE"
Cuando accedo a la matriz desde la pestaña "Criterio EUR-ACE"
Entonces el sistema muestra la estructura completa de la matriz
Y el título "Matriz: Resultados de Aprendizaje (RA) y Criterios EUR-ACE" se visualiza correctamente
Y se presenta el subtítulo descriptivo
Y la matriz muestra todos los Criterios EUR-ACE disponibles en el eje vertical (5.4.1, 5.4.2, 5.4.3, etc.)
Y la matriz muestra todos los Resultados de Aprendizaje disponibles en el eje horizontal (RG1, RG2, RG3, RE1, RE2, etc.)
Y TODAS las celdas de intersección aparecen vacías de color blanco sin checkmarks
Y NO hay ninguna celda con color verde turquesa
Y los íconos de información (ⓘ) permanecen disponibles y funcionales
Y el botón "+ Nueva Relación" está visible y habilitado para crear la primera relación
Y se muestra un mensaje informativo "No hay relaciones establecidas. Haga clic en + Nueva Relación para crear una."
Y la interfaz permite scroll para visualizar toda la estructura de la matriz
```

---

### **Criterio de Aceptación 4 (AC4 - RM5): Visualizar matriz RA vacía cuando no hay relaciones**

```gherkin
Escenario 4: Mostrar matriz vacía cuando no existen relaciones (Vista RA transpuesta)
Dado que soy un Coordinador de Carrera autenticado en el sistema
Y NO existen relaciones establecidas entre Resultados de Aprendizaje y Criterios EUR-ACE para mi carrera
Y estoy en la sección "Editor Mapeos" → "RA vs EUR-ACE"
Cuando accedo a la matriz desde la pestaña "Resultados de Aprendizaje Carrera"
Entonces el sistema muestra la matriz con vista transpuesta
Y la pestaña "Resultados de Aprendizaje Carrera" aparece activa
Y la matriz muestra todos los Resultados de Aprendizaje en el eje vertical (filas)
Y la matriz muestra todos los Criterios EUR-ACE en el eje horizontal (columnas)
Y TODAS las celdas de intersección aparecen vacías sin checkmarks verdes
Y NO hay ninguna celda con color verde turquesa
Y los íconos de información (ⓘ) permanecen disponibles en ambos ejes
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
Cuando intento acceder directamente a la URL "Editor Mapeos" → "RA vs EUR-ACE"
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

**AC1 (Escenario 1): Visualizar matriz de relaciones RA-EUR-ACE desde pestaña Criterio EUR-ACE**

---

### **🔥 JUSTIFICACIÓN DETALLADA DE CRITICIDAD:**

El **Criterio de Aceptación 1** es el más crítico de esta Historia de Usuario por las siguientes **15 razones fundamentales**:

1. **Cumple el objetivo central de la HU**: La HU establece textualmente "Quiero **visualizar las relaciones** de los Resultados de Aprendizaje con Criterios EUR-ACE", y este AC es el único que valida directamente la capacidad de visualizar todas las relaciones establecidas en formato matricial, que es exactamente el valor que el usuario necesita.

2. **Happy Path principal según prototipo**: La Imagen 17 muestra explícitamente este escenario como el flujo de éxito esperado: matriz con múltiples relaciones ya establecidas, vista desde la pestaña "Criterio EUR-ACE", con celdas verdes y checkmarks visibles.

3. **Evaluación de alineación con estándares internacionales**: La HU indica "Para evaluar la alineación de mi carrera con los estándares internacionales." Sin poder visualizar las relaciones existentes, el coordinador no puede:
   - Verificar qué criterios EUR-ACE están cubiertos
   - Identificar gaps en la cobertura de estándares
   - Validar que todos los RAs contribuyen a criterios EUR-ACE
   - Demostrar conformidad con requisitos de acreditación EUR-ACE
   - Preparar evidencias para auditorías internacionales

4. **Acreditación internacional EUR-ACE obligatoria**: EUR-ACE (European Accredited Engineer) es un sistema de acreditación de programas de ingeniería reconocido internacionalmente. Este AC valida que el coordinador pueda visualizar cómo su programa cumple con estos estándares, lo cual es **requisito obligatorio** para:
   - Acreditación internacional de programas de ingeniería
   - Reconocimiento de títulos en el Espacio Europeo de Educación Superior
   - Movilidad internacional de graduados
   - Cumplimiento de directivas europeas de profesiones reguladas

5. **Trazabilidad curricular completa hacia estándares internacionales**: La imagen 17 muestra que los criterios EUR-ACE (formato 5.4.X y 5.5.X) representan el nivel más alto de la jerarquía de trazabilidad:
   - **OPP** → RA → **EUR-ACE** (nivel internacional)
   
   Este AC valida el eslabón final que conecta el currículo institucional con estándares reconocidos globalmente.

6. **Visualización matricial bidimensional única**: A diferencia de listas simples, esta matriz permite:
   - Ver TODAS las relaciones simultáneamente
   - Identificar patrones de cobertura
   - Detectar concentraciones o vacíos en la alineación
   - Comparar visualmente qué RAs aportan a cada criterio EUR-ACE
   - Analizar distribución de competencias técnicas vs transversales

7. **Diferenciación entre RG y RE en contexto EUR-ACE**: El AC valida que la matriz muestra AMBOS tipos de resultados de aprendizaje:
   - **RG (Resultados Generales)**: Competencias transversales que también deben alinearse con EUR-ACE
   - **RE (Resultados Específicos)**: Competencias técnicas específicas de la carrera
   
   Esta diferenciación es crítica porque EUR-ACE requiere tanto competencias técnicas como transversales.

8. **Códigos EUR-ACE específicos y normalizados**: El AC valida que los códigos mostrados (5.4.1, 5.4.2, 5.4.3, 5.4.4, 5.4.5, 5.4.6, 5.5.1) corresponden EXACTAMENTE a la estructura del marco EUR-ACE:
   - **5.4**: Resultados de aprendizaje específicos de ingeniería
   - **5.5**: Competencias transversales de ingeniería
   
   Estos códigos no son arbitrarios sino que siguen la nomenclatura oficial de EUR-ACE Framework Standards.

9. **Íconos de información contextuales críticos**: El AC valida que cada código EUR-ACE y RA tiene un ícono (ⓘ) clickeable. Esto es fundamental porque:
   - Los criterios EUR-ACE son complejos y técnicos
   - Los coordinadores necesitan acceso rápido a las descripciones completas
   - Facilita la comprensión del significado de cada criterio (ej: 5.4.3 = "especialización y enfoque en mercado de trabajo")
   - Permite tomar decisiones informadas sobre nuevas relaciones

10. **Representación visual clara de estado de relaciones**: El AC valida la diferenciación visual mediante:
    - **Celdas verdes turquesa + ✓**: Relación establecida y documentada
    - **Celdas blancas vacías**: No hay relación (gap potencial)
    
    Esta codificación de colores permite identificar instantáneamente el estado de alineación del programa.

11. **Scroll horizontal para completitud de datos**: El AC valida que la matriz soporta scroll horizontal, lo cual indica que:
    - Puede haber numerosos RAs (observamos hasta RE7 y probablemente más)
    - Todos los RAs deben poder visualizarse sin pérdida de información
    - La interfaz se adapta a diferentes tamaños de programas académicos

12. **Sistema de pestañas para múltiples perspectivas**: Aunque este AC se enfoca en la vista EUR-ACE, valida la existencia del sistema de pestañas que permite alternar entre:
    - Vista EUR-ACE (filas) vs RA (columnas) - Pregunta: "¿Qué RAs cubren cada criterio?"
    - Vista RA (filas) vs EUR-ACE (columnas) - Pregunta: "¿A qué criterios contribuye cada RA?"
    
    Ambas perspectivas son necesarias para análisis curricular completo.

13. **Botón "+ Nueva Relación" como punto de acción**: El AC valida que después de visualizar las relaciones existentes, el coordinador tiene acceso inmediato a crear nuevas relaciones si identifica gaps. Este flujo de trabajo (visualizar → identificar gaps → crear relaciones) es el proceso natural de gestión curricular.

14. **Volumen de datos representativo**: El prototipo muestra múltiples relaciones establecidas (al menos 8 relaciones visibles: 5.4.1↔RE1, 5.4.2↔RE2, 5.4.3↔RG2, 5.4.4↔RG3, 5.4.5↔RE3, 5.4.6↔RG1, 5.4.6↔RE4, 5.5.1↔RE7), lo cual representa un caso de uso real con datos significativos, no una matriz vacía o de prueba.

15. **Integración con workflow de justificación**: Las Imágenes 18-20 muestran que cada relación RA-EUR-ACE requiere un wizard de 3 pasos con justificación obligatoria. Este AC valida que todas esas relaciones creadas previamente se visualizan correctamente en la matriz final, completando el ciclo de gestión de alineación curricular.

---

### **📊 IMPACTO DE FALLO DEL AC1:**

Si este Criterio de Aceptación falla:

**Impacto en el Usuario:**
- El Coordinador no puede visualizar las relaciones RA-EUR-ACE existentes
- No puede evaluar el grado de alineación con estándares internacionales
- Pierde visibilidad sobre qué criterios EUR-ACE están cubiertos
- No puede identificar gaps en la cobertura de requisitos EUR-ACE

**Impacto en el Sistema:**
- La funcionalidad principal de la HU queda completamente inutilizable
- Se pierde la trazabilidad entre currículo local y estándares internacionales
- Se bloquea la capacidad de análisis de cobertura de competencias
- Se impide la preparación de evidencias para acreditación EUR-ACE

**Impacto en el Negocio:**
- **Riesgo de pérdida de acreditación internacional EUR-ACE**
- Imposibilidad de demostrar conformidad con estándares europeos
- Compromiso de la reputación internacional del programa
- Limitación de oportunidades de movilidad para estudiantes y graduados
- Pérdida de reconocimiento de títulos en el Espacio Europeo de Educación Superior
- Incapacidad de participar en programas de intercambio internacional
- Desventaja competitiva frente a programas acreditados internacionalmente

---

**CONCLUSIÓN:**

El **AC1 es absolutamente crítico** porque valida la funcionalidad central que permite al Coordinador de Carrera **visualizar todas las relaciones establecidas entre Resultados de Aprendizaje y Criterios EUR-ACE** en formato de matriz bidimensional interactiva, con representación visual clara del estado de alineación mediante códigos de colores. Esta visualización es **prerequisito fundamental e indispensable** para evaluar la conformidad del programa académico con los estándares internacionales de acreditación EUR-ACE, identificar gaps en la cobertura de competencias, demostrar trazabilidad curricular hacia estándares globalmente reconocidos, y preparar evidencias documentales para auditorías de acreditación internacional. Sin este AC funcionando, el coordinador pierde completamente la capacidad de gestionar la alineación de su programa con requisitos que son **obligatorios para acreditación internacional**, compromete el reconocimiento global de los títulos otorgados, y pone en riesgo la reputación académica y competitividad internacional de la institución.

---

**FIN DEL ANÁLISIS COMPLETO** ✅