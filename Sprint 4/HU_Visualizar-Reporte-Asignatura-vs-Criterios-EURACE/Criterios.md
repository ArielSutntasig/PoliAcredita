# CRITERIOS DE ACEPTACIÓN - HU: Visualizar Reporte Asignatura vs Criterios EURACE

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas del análisis visual:**

**C1: Facultad seleccionada**
- Estado: Sí / No
- Fuente: Campo de búsqueda "Facultad:" con autocompletado
- Valores observados: "Sistemas", estado vacío "Buscar una facultad"

**C2: Carrera seleccionada**
- Estado: Sí / No
- Fuente: Dropdown "Carrera:" dependiente de Facultad
- Valores observados: "Software", "Ingeniería de Software", estado inicial "Seleccionar una carrera"

**C3: Al menos un nivel de aporte marcado**
- Estado: Sí / No
- Fuente: Checkboxes "Alto", "Medio", "Bajo"
- Observado: Ninguno marcado, solo Alto, todos marcados

**C4: Click en cruce de matriz**
- Estado: Sí / No
- Fuente: Mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:"
- Acción: Click en celda con checkmark verde

#### **Acciones del sistema identificadas:**

**A1: Habilitar dropdown "Carrera:"**
- Condición: Cuando Facultad está seleccionada
- Observado: Dropdown cambia de estado deshabilitado a activo

**A2: Mostrar mensaje instructivo y estructura de tabla**
- Condición: Cuando Facultad y Carrera están seleccionadas
- Texto observado: "Haga clic en un cruce para ver el detalle de la relación:"

**A3: Generar y mostrar matriz completa con datos**
- Condición: Cuando Facultad, Carrera y al menos un nivel de aporte están seleccionados
- Elementos: Encabezados EUR-ACE (5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7), filas de asignaturas, checkmarks verdes

**A4: Filtrar contenido de matriz según niveles marcados**
- Condición: Checkboxes afectan qué relaciones se muestran
- Observado: Solo Alto vs. Todos los niveles muestra diferente cantidad de información

**A5: Mostrar vista de trazabilidad detallada**
- Condición: Click en cruce de matriz
- Elementos: Título "Trazabilidad de [Nombre Asignatura]", botón "Regresar", secciones por nivel (Alto/Verde, Medio/Amarillo, Bajo/Rosa), flujo de 4 columnas (RAA → RA → Justificación → Criterio EUR-ACE)

**A6: No mostrar contenido de matriz**
- Condición: Cuando no se cumplen todos los filtros requeridos
- Observado: Área de contenido vacía con solo filtros visibles

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 4 condiciones binarias: 2^4 = **16 reglas**

| Regla | C1: Facultad | C2: Carrera | C3: Nivel aporte | C4: Click cruce | Acción del Sistema |
|-------|--------------|-------------|------------------|-----------------|-------------------|
| R1    | No           | No          | No               | No              | A6: No mostrar contenido |
| R2    | No           | No          | No               | Sí              | A6: No mostrar contenido (click inválido) |
| R3    | No           | No          | Sí               | No              | A6: No mostrar contenido |
| R4    | No           | No          | Sí               | Sí              | A6: No mostrar contenido (click inválido) |
| R5    | No           | Sí          | No               | No              | A6: No mostrar contenido (estado imposible*) |
| R6    | No           | Sí          | No               | Sí              | A6: No mostrar contenido (estado imposible*) |
| R7    | No           | Sí          | Sí               | No              | A6: No mostrar contenido (estado imposible*) |
| R8    | No           | Sí          | Sí               | Sí              | A6: No mostrar contenido (estado imposible*) |
| R9    | Sí           | No          | No               | No              | A1: Habilitar Carrera + A6: No mostrar contenido |
| R10   | Sí           | No          | No               | Sí              | A1: Habilitar Carrera + A6: No mostrar contenido (click inválido) |
| R11   | Sí           | No          | Sí               | No              | A1: Habilitar Carrera + A6: No mostrar contenido |
| R12   | Sí           | No          | Sí               | Sí              | A1: Habilitar Carrera + A6: No mostrar contenido (click inválido) |
| R13   | Sí           | Sí          | No               | No              | A1 + A2: Mostrar estructura sin datos |
| R14   | Sí           | Sí          | No               | Sí              | A1 + A2: Mostrar estructura sin datos (click inválido) |
| R15   | Sí           | Sí          | Sí               | No              | A1 + A2 + A3 + A4: Mostrar matriz completa |
| R16   | Sí           | Sí          | Sí               | Sí              | A1 + A2 + A3 + A4 + A5: Mostrar trazabilidad |

*Nota: Estado imposible porque Carrera solo se puede seleccionar si Facultad está seleccionada (dependencia de cascada).

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Reglas R1-R8:** Todas resultan en "No mostrar contenido" cuando Facultad=No, independientemente de otros valores. Carrera=Sí sin Facultad=Sí es imposible (dependencia). **Se fusionan en Regla Minimizada M1**.

2. **Reglas R9-R12:** Cuando Facultad=Sí pero Carrera=No, el sistema habilita Carrera pero no muestra contenido. Nivel de aporte y Click son irrelevantes. **Se fusionan en Regla Minimizada M2**.

3. **Reglas R13-R14:** Cuando Facultad=Sí y Carrera=Sí pero Nivel=No, muestra estructura sin datos. Click es irrelevante (no hay datos clicables). **Se fusionan en Regla Minimizada M3**.

4. **Regla R15:** Cuando Facultad=Sí, Carrera=Sí, Nivel=Sí pero Click=No, muestra matriz completa con datos. **Regla Minimizada M4**.

5. **Regla R16:** Cuando Facultad=Sí, Carrera=Sí, Nivel=Sí y Click=Sí, muestra vista de trazabilidad. **Regla Minimizada M5**.

#### **Tabla Minimizada:**

| Regla Min | C1: Facultad | C2: Carrera | C3: Nivel aporte | C4: Click cruce | Acción del Sistema |
|-----------|--------------|-------------|------------------|-----------------|-------------------|
| **M1**    | No           | -           | -                | -               | A6: No mostrar contenido de matriz |
| **M2**    | Sí           | No          | -                | -               | A1: Habilitar dropdown "Carrera:" + A6: No mostrar contenido |
| **M3**    | Sí           | Sí          | No               | -               | A1 + A2: Habilitar Carrera + Mostrar mensaje instructivo sin datos |
| **M4**    | Sí           | Sí          | Sí               | No              | A1 + A2 + A3 + A4: Mostrar matriz completa con checkmarks verdes |
| **M5**    | Sí           | Sí          | Sí               | Sí              | A1 + A2 + A3 + A4 + A5: Mostrar vista de trazabilidad detallada |

**Resultado: 5 reglas minimizadas = 5 Criterios de Aceptación base**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 5 reglas minimizadas, procedo a evaluar si hay redundancias o si se requieren criterios adicionales basados en el análisis visual:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre estado sin facultad seleccionada
2. M2 → AC sobre habilitación de carrera cuando facultad está seleccionada
3. M3 → AC sobre estado con facultad y carrera pero sin niveles marcados
4. M4 → AC sobre visualización de matriz completa (HAPPY PATH)
5. M5 → AC sobre navegación a vista de trazabilidad

**Análisis de criterios adicionales necesarios:**

Del análisis visual, identifico comportamientos críticos NO cubiertos por la tabla base:

6. **Filtrado dinámico por niveles:** Las imágenes muestran que marcar/desmarcar checkboxes actualiza la matriz sin recargar. Esto es un comportamiento interactivo importante.

7. **Búsqueda en matriz:** Las imágenes muestran campo de búsqueda "Buscar por código o nombre de asignatura" con funcionalidad de filtrado en tiempo real.

8. **Botón "Regresar":** La vista de trazabilidad incluye navegación de regreso a matriz.

**Criterios eliminados por redundancia:**
- ~~Cambio entre carreras de la misma facultad~~: Redundante con M2 y M4, es simplemente una repetición de la selección.
- ~~Reset de filtros~~: No se observa en las imágenes, no añadir funcionalidad no solicitada.

**TOTAL FINAL: 8 Criterios de Aceptación**
- 5 de la tabla de decisión base
- 3 adicionales por funcionalidades críticas observadas en el prototipo

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

Aplicando la guía de estilo internalizada previamente:

---

### **Escenario 1 – Estado inicial sin filtros aplicados**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" **Y** soy un Coordinador de Carrera o CEI en el sistema,
**cuando** accedo al reporte sin haber seleccionado filtros,
**entonces** se muestra el título "Reporte: Asignatura vs Criterios EURACE" **Y** se presenta la descripción "Visualización detallada de la contribución de asignaturas a los criterios EUR-ACE." **Y** se muestra el campo de búsqueda "Facultad:" con placeholder "Buscar una facultad" **Y** se muestra el dropdown "Carrera:" con texto "Seleccionar una carrera" en estado deshabilitado **Y** se muestran los checkboxes "Alto", "Medio", "Bajo" desmarcados en la sección "Nivel de aporte" **Y** no se muestra contenido de matriz ni mensaje instructivo **Y** el área de contenido principal permanece vacía.

---

### **Escenario 2 – Seleccionar facultad y habilitar carrera**

**Dado que** estoy en el reporte "Reporte: Asignatura vs Criterios EURACE" **Y** el dropdown "Carrera:" está deshabilitado,
**cuando** escribo "Sis" en el campo "Facultad:" **Y** selecciono "Sistemas" de las opciones desplegadas,
**entonces** el campo "Facultad:" se actualiza con el valor "Sistemas" **Y** el dropdown "Carrera:" se habilita **Y** el dropdown "Carrera:" muestra el texto "Seleccionar una carrera" disponible para interacción **Y** no se muestra contenido de matriz **Y** el área de contenido principal permanece vacía hasta completar los filtros.

---

### **Escenario 3 – Seleccionar carrera sin marcar niveles de aporte**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** el dropdown "Carrera:" está habilitado,
**cuando** hago clic en el dropdown "Carrera:" **Y** selecciono "Ingeniería de Software" de las opciones disponibles (Ingeniería de Software, Ingeniería Ciencias de la Computación, Ingeniería en Inteligencia Artificial),
**entonces** el dropdown "Carrera:" se actualiza con el valor "Ingeniería de Software" **Y** se muestra el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:" **Y** no se muestra la matriz con datos **Y** los checkboxes "Alto", "Medio", "Bajo" permanecen visibles y desmarcados **Y** es evidente que se requiere marcar al menos un nivel de aporte para visualizar datos.

---

### **Escenario 4 – Generar matriz completa con todos los filtros aplicados**

**Dado que** tengo la facultad "Sistemas" seleccionada **Y** tengo la carrera "Ingeniería de Software" seleccionada,
**cuando** marco el checkbox "Alto" en "Nivel de aporte:",
**entonces** se mantiene el mensaje instructivo "Haga clic en un cruce para ver el detalle de la relación:" **Y** se genera la matriz completa con encabezados de columnas EUR-ACE (5.2.1, 5.2.2, 5.2.3, 5.2.4, 5.2.5, 5.3.1, 5.3.2, 5.3.3, 5.3.4, 5.3.5, 5.3.6, 5.3.7) en fondo azul oscuro **Y** se muestra la columna "Asignatura" como primera columna fija **Y** se presentan las filas de asignaturas (Álgebra Lineal, Cálculo en una Variable, Mecánica Newtoniana, Programación I, Comunicación Oral y Escrita, Ecuaciones Diferenciales, Matemática Computacional, Fundamentos de Electrónica) **Y** se muestran checkmarks verdes (✓) en las intersecciones donde existe relación entre asignatura y criterio EUR-ACE **Y** las celdas vacías indican ausencia de relación **Y** el campo de búsqueda "Buscar por código o nombre de asignatura" se muestra disponible sobre la matriz.

---

### **Escenario 5 – Visualizar matriz con múltiples niveles de aporte**

**Dado que** tengo la facultad "Sistemas" y carrera "Ingeniería de Software" seleccionadas **Y** tengo al menos un nivel de aporte marcado,
**cuando** marco los checkboxes "Alto", "Medio" y "Bajo" simultáneamente,
**entonces** se actualiza la matriz automáticamente sin recargar la página **Y** se muestran todas las relaciones de los tres niveles de aporte en la matriz **Y** se presentan checkmarks verdes (✓) en todas las intersecciones que corresponden a cualquiera de los niveles seleccionados **Y** se mantiene la estructura de encabezados y columnas **Y** se incrementa la cantidad de checkmarks verdes visibles respecto a tener un solo nivel marcado **Y** la respuesta visual es inmediata al cambio de filtros.

---

### **Escenario 6 – Filtrar asignaturas mediante búsqueda**

**Dado que** tengo la matriz completa visible con asignaturas y relaciones **Y** hay múltiples asignaturas en la tabla,
**cuando** escribo "MATD113 Álgebra Lineal" en el campo de búsqueda "Buscar por código o nombre de asignatura",
**entonces** la tabla se filtra automáticamente mostrando únicamente la fila correspondiente a "Álgebra Lineal" **Y** se muestran solo los checkmarks verdes (✓) en las columnas 5.3.4 y 5.3.5 para esta asignatura **Y** se mantienen visibles todos los encabezados de columnas EUR-ACE **Y** las demás filas de asignaturas desaparecen de la vista **Y** el filtrado ocurre en tiempo real sin necesidad de presionar botón de búsqueda.

---

### **Escenario 7 – Navegar a vista de trazabilidad detallada**

**Dado que** tengo la matriz completa visible con checkmarks verdes **Y** veo la asignatura "Cálculo en una Variable" con checkmark en la intersección con criterio "5.2.2",
**cuando** hago clic en la celda con checkmark verde de la intersección entre "Cálculo en una Variable" y criterio "5.2.2",
**entonces** se navega a una nueva vista con título "Trazabilidad de Cálculo en una Variable" **Y** se muestra el botón "Regresar" en la esquina superior derecha **Y** se presenta la sección "Nivel de aporte: Alto" con fondo verde/turquesa claro **Y** se muestra el flujo horizontal de 4 columnas: "R. de Aprendizaje Asignatura", "R. de Aprendizaje", "Justificación RA-EURACE", "Criterio EUR-ACE" **Y** se presentan flechas direccionales (→) entre las columnas **Y** se visualizan cards con bordes redondeados conteniendo RAA, RA, justificación y criterio EUR-ACE **Y** se muestra la sección "Nivel de aporte: Medio" con fondo amarillo claro **Y** se muestra la sección "Nivel de aporte: Bajo" con fondo rosa claro **Y** cada sección mantiene la misma estructura de 4 columnas con flujo completo.

---

### **Escenario 8 – Regresar de trazabilidad a matriz**

**Dado que** estoy en la vista de trazabilidad detallada "Trazabilidad de Cálculo en una Variable" **Y** veo el botón "Regresar" en la esquina superior derecha,
**cuando** hago clic en el botón "Regresar",
**entonces** se navega de regreso a la vista del reporte "Reporte: Asignatura vs Criterios EURACE" **Y** se mantiene la matriz completa visible con los mismos filtros aplicados (Facultad: Sistemas, Carrera: Ingeniería de Software, Niveles de aporte previamente marcados) **Y** se preserva el estado de los checkboxes de nivel de aporte **Y** se mantiene visible la búsqueda y todos los checkmarks verdes de la matriz **Y** no se reinician los filtros aplicados.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 4 – Generar matriz completa con todos los filtros aplicados**

### **Justificación:**

Este criterio representa el **happy path principal** y el núcleo de valor de la Historia de Usuario. Es el más crítico por las siguientes razones:

1. **Valor de negocio directo:** Cumple directamente con el objetivo de la HU "visualizar el reporte de contribución de asignaturas a los criterios EURACE para analizar la alineación de los programas de estudio con los estándares de acreditación".

2. **Dependencia de funcionalidades posteriores:** Los escenarios 6, 7 y 8 (búsqueda, navegación a detalle, regreso) solo tienen sentido si la matriz se genera correctamente. Sin este escenario funcionando, el resto del flujo carece de utilidad.

3. **Complejidad técnica crítica:** Integra múltiples componentes del sistema:
   - Filtrado en cascada (Facultad → Carrera)
   - Procesamiento de niveles de aporte
   - Generación dinámica de matriz multidimensional
   - Renderizado de relaciones (checkmarks verdes)
   - Visualización de códigos EUR-ACE específicos

4. **Punto de fallo más riesgoso:** Si la matriz no se genera o muestra datos incorrectos, la funcionalidad completa falla. Los usuarios (Coordinadores de Carrera y CEI) no podrán realizar su análisis de acreditación, lo cual es el propósito fundamental del sistema.

5. **Validación de reglas de negocio:** Este escenario valida que:
   - Solo se muestran asignaturas de la carrera seleccionada
   - Solo se muestran relaciones que corresponden a los niveles de aporte marcados
   - Los criterios EUR-ACE se presentan en el orden y formato correcto
   - Los checkmarks verdes aparecen exclusivamente donde existe una relación documentada

6. **Evidencia visual completa en prototipo:** Es el escenario más documentado en las imágenes (imágenes 5-7 para ambos roles), lo que indica su importancia desde la fase de diseño.

**Recomendación de prueba prioritaria:** Este escenario debe ser el primero en automatizarse y el que reciba mayor cobertura de pruebas, incluyendo pruebas de regresión exhaustivas en cada iteración del desarrollo.