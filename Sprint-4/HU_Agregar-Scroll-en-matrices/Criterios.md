# CRITERIOS DE ACEPTACIÓN - HU: Agregar Scroll en matrices

---

## **NOTA IMPORTANTE:**
Este análisis se basa en las imágenes de matrices analizadas en Historias de Usuario anteriores (específicamente la matriz RAA vs RA visible en la HU "Visualizar materia al relacionar RAA vs RA" y las matrices de reportes). Si existen imágenes específicas adicionales para esta HU, los criterios pueden ajustarse según esos detalles visuales.

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas basadas en la HU y mejores prácticas de UI:**

**C1: Contenido de la matriz excede el ancho del viewport (scroll horizontal necesario)**
- Estado: Sí / No
- Fuente: Cantidad de columnas en la matriz supera el espacio visible
- Contexto de matrices observadas:
  - **RAA vs RA:** Columnas RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6 (9+ columnas)
  - **RA vs OP:** Múltiples objetivos de programa
  - **Asignatura vs EUR-ACE:** Criterios 5.2.1 hasta 5.3.7 (12+ columnas)
- Resultado: Cuando hay muchas columnas, se necesita scroll horizontal

**C2: Contenido de la matriz excede el alto del viewport (scroll vertical necesario)**
- Estado: Sí / No
- Fuente: Cantidad de filas en la matriz supera el espacio visible
- Contexto de matrices observadas:
  - **RAA vs RA:** RAA con códigos 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1 (7+ filas visibles)
  - **Asignatura vs EUR-ACE:** Múltiples asignaturas (Álgebra, Cálculo, Mecánica, Programación, etc.)
  - Puede haber 20-50+ filas según el tamaño de la carrera/asignatura
- Resultado: Cuando hay muchas filas, se necesita scroll vertical

**C3: Usuario intenta desplazarse en la matriz**
- Estado: Sí / No
- Acciones posibles:
  - Usar scroll de mouse/trackpad
  - Arrastrar barra de desplazamiento
  - Usar teclas de flecha
  - Gestos táctiles (en dispositivos móviles)

#### **Acciones del sistema identificadas:**

**A1: Mostrar matriz completa sin scroll**
- Condición: Contenido cabe completamente en viewport
- Resultado: Toda la matriz visible sin necesidad de desplazamiento
- Caso: Matriz pequeña con pocas filas y columnas

**A2: Mostrar barra de scroll horizontal**
- Condición: Ancho de matriz > ancho de viewport
- Ubicación: Parte inferior de la matriz
- Estilo: Barra de desplazamiento estándar del navegador o personalizada
- Comportamiento: Permite desplazamiento izquierda-derecha

**A3: Mostrar barra de scroll vertical**
- Condición: Alto de matriz > alto de viewport
- Ubicación: Lado derecho de la matriz
- Estilo: Barra de desplazamiento estándar o personalizada
- Comportamiento: Permite desplazamiento arriba-abajo

**A4: Habilitar desplazamiento horizontal**
- Condición: Usuario arrastra/mueve scroll horizontal o usa gestos horizontales
- Resultado: La matriz se desplaza mostrando columnas que estaban fuera de vista
- Columnas fijas: Primera columna (RAA/Asignaturas) puede mantenerse fija (sticky)

**A5: Habilitar desplazamiento vertical**
- Condición: Usuario arrastra/mueve scroll vertical o usa gestos verticales
- Resultado: La matriz se desplaza mostrando filas que estaban fuera de vista
- Fila fija: Encabezados de columna (RA/Criterios) se mantienen fijos (sticky)

**A6: Mantener encabezados visibles durante scroll**
- Condición: Usuario hace scroll vertical
- Comportamiento: Encabezados de columnas permanecen fijos en la parte superior
- Técnica: Position sticky o fixed en CSS
- Propósito: Usuario siempre sabe qué representa cada columna

**A7: Mantener primera columna visible durante scroll horizontal**
- Condición: Usuario hace scroll horizontal
- Comportamiento: Primera columna (códigos RAA/nombres asignaturas) permanece fija
- Técnica: Position sticky en primera columna
- Propósito: Usuario siempre sabe qué fila está viendo

**A8: Scroll suave y responsive**
- Condición: Usuario usa cualquier método de scroll
- Comportamiento: Desplazamiento fluido sin saltos
- Performance: Sin lag ni stuttering
- Feedback visual: Indicadores de posición actualizados

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Excede ancho | C2: Excede alto | C3: Intenta scroll | Acción del Sistema |
|-------|------------------|----------------|-------------------|-------------------|
| R1    | No               | No             | No                | A1: Mostrar matriz completa sin scroll |
| R2    | No               | No             | Sí                | A1: Matriz completa, no hay scroll disponible |
| R3    | No               | Sí             | No                | A3: Mostrar solo scroll vertical visible |
| R4    | No               | Sí             | Sí                | A3 + A5 + A6: Permitir scroll vertical con headers fijos |
| R5    | Sí               | No             | No                | A2: Mostrar solo scroll horizontal visible |
| R6    | Sí               | No             | Sí                | A2 + A4 + A7: Permitir scroll horizontal con columna fija |
| R7    | Sí               | Sí             | No                | A2 + A3: Mostrar ambos scrolls visibles (ESTADO MÁS COMÚN) |
| R8    | Sí               | Sí             | Sí                | A2 + A3 + A4 + A5 + A6 + A7 + A8: Scroll completo bidireccional (HAPPY PATH) |

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Reglas R1-R2:** Matriz pequeña que cabe completamente en viewport. No hay scroll necesario ni disponible. El intento de scroll es irrelevante. **Se fusionan en M1**.

2. **Reglas R3-R4:** Solo se necesita scroll vertical (ancho cabe, alto excede). Cuando el usuario intenta scroll vertical, se ejecuta. **Se fusionan en M2**, diferenciando entre estado estático (no intenta) y estado activo (intenta scroll).

3. **Reglas R5-R6:** Solo se necesita scroll horizontal (alto cabe, ancho excede). Cuando el usuario intenta scroll horizontal, se ejecuta. **Se fusionan en M3**, diferenciando entre estado estático y activo.

4. **Reglas R7-R8:** Matriz grande que requiere ambos scrolls (bidireccional). Este es el caso más común en matrices académicas con muchas filas y columnas. **Se mantienen como M4 (estado estático) y M5 (happy path activo)**.

#### **Tabla Minimizada:**

| Regla Min | C1: Excede ancho | C2: Excede alto | C3: Intenta scroll | Acción del Sistema |
|-----------|------------------|----------------|-------------------|-------------------|
| **M1**    | No               | No             | -                 | A1: Matriz completa visible sin scroll |
| **M2**    | No               | Sí             | Sí                | A3 + A5 + A6: Scroll vertical con headers fijos |
| **M3**    | Sí               | No             | Sí                | A2 + A4 + A7: Scroll horizontal con columna fija |
| **M4**    | Sí               | Sí             | No                | A2 + A3: Mostrar ambos scrolls disponibles |
| **M5**    | Sí               | Sí             | Sí                | A2 + A3 + A4 + A5 + A6 + A7 + A8: Scroll bidireccional completo |

**Resultado: 5 reglas minimizadas**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 5 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre matriz que no requiere scroll (caso edge)
2. M2 → AC sobre scroll vertical únicamente
3. M3 → AC sobre scroll horizontal únicamente
4. M4 → AC sobre ambos scrolls visibles pero sin uso activo
5. M5 → AC sobre scroll bidireccional activo (HAPPY PATH)

**Análisis de criterios adicionales necesarios:**

Del objetivo de la HU ("desplazarme a través de la matriz") y mejores prácticas de UX:

6. **Consistencia entre las 3 matrices:** El comportamiento de scroll debe ser idéntico en RA-OP, RAA-RA y RA-EUR-ACE.

7. **Performance del scroll:** El scroll debe ser fluido sin lag (60fps).

8. **Indicadores visuales de scroll:** Usuario debe poder ver que hay más contenido fuera de vista.

**Criterios a ELIMINAR por redundancia:**

- **M1 (Matriz completa sin scroll):** Este es un caso edge que no valida la funcionalidad principal de la HU ("agregar scroll"). La HU asume que las matrices necesitan scroll. **ELIMINADO por no validar la funcionalidad core de la HU**.

- **M4 (Scrolls visibles pero sin uso):** Este es solo un estado intermedio entre mostrar los scrolls y usarlos. El valor real está en M5 (usar los scrolls). **ELIMINADO por ser estado intermedio sin acción del usuario**.

- **Criterios adicionales de performance e indicadores:** Se consolidarán en M5 como parte del comportamiento esperado del happy path.

**TOTAL FINAL: 3 Criterios de Aceptación**
- 1 de M2 (scroll vertical únicamente)
- 1 de M3 (scroll horizontal únicamente)
- 1 de M5 (scroll bidireccional - HAPPY PATH)

**Justificación de eliminaciones:**
- **M1:** Caso edge que no valida agregar scroll, la HU asume que se necesita scroll
- **M4:** Estado intermedio sin interacción, el valor está en usar los scrolls (M5)
- **Performance e indicadores:** Consolidados en M5 como parte del comportamiento esperado

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

---

### **Escenario 1 – Scroll vertical en matriz con muchas filas**

**Dado que** soy un profesor o coordinador visualizando una matriz (RA vs OP, RAA vs RA, o RA vs EUR-ACE) **Y** la matriz tiene más filas de las que caben en la pantalla visible (por ejemplo, 20+ asignaturas o 15+ RAA),
**cuando** la matriz se carga inicialmente,
**entonces** se muestra una barra de scroll vertical en el lado derecho de la matriz **Y** los encabezados de las columnas (códigos de RA, criterios EUR-ACE, o nombres de OP) permanecen fijos en la parte superior de la matriz **Y** cuando arrastro la barra de scroll vertical hacia abajo o uso la rueda del mouse, la matriz se desplaza verticalmente mostrando las filas que estaban fuera de vista **Y** los encabezados de columnas permanecen visibles y fijos durante todo el desplazamiento vertical **Y** puedo ver filas que inicialmente estaban ocultas en la parte inferior de la matriz **Y** el desplazamiento es suave y fluido sin saltos ni lag **Y** puedo volver al inicio arrastrando el scroll hacia arriba **Y** este comportamiento es idéntico en las tres matrices del sistema (RA vs OP, RAA vs RA, RA vs EUR-ACE).

---

### **Escenario 2 – Scroll horizontal en matriz con muchas columnas**

**Dado que** soy un profesor o coordinador visualizando una matriz (RA vs OP, RAA vs RA, o RA vs EUR-ACE) **Y** la matriz tiene más columnas de las que caben en el ancho visible de la pantalla (por ejemplo, 9+ códigos de RA o 12+ criterios EUR-ACE),
**cuando** la matriz se carga inicialmente,
**entonces** se muestra una barra de scroll horizontal en la parte inferior de la matriz **Y** la primera columna con los códigos o nombres (RAA, nombres de asignaturas, o códigos de RA) permanece fija en el lado izquierdo **Y** cuando arrastro la barra de scroll horizontal hacia la derecha o uso gestos horizontales, la matriz se desplaza horizontalmente mostrando las columnas que estaban fuera de vista **Y** la primera columna identificadora permanece visible y fija durante todo el desplazamiento horizontal **Y** puedo ver columnas adicionales de RA o criterios EUR-ACE que inicialmente estaban ocultas en el lado derecho **Y** el desplazamiento es suave y responsive sin saltos **Y** puedo volver al inicio arrastrando el scroll hacia la izquierda **Y** este comportamiento es consistente en las tres matrices del sistema.

---

### **Escenario 3 – Scroll bidireccional en matriz grande con muchas filas y columnas**

**Dado que** soy un profesor o coordinador visualizando una matriz (RA vs OP, RAA vs RA, o RA vs EUR-ACE) **Y** la matriz tiene tanto muchas filas como muchas columnas que exceden el espacio visible de la pantalla (por ejemplo, 20+ filas y 9+ columnas),
**cuando** interactúo con la matriz para desplazarme,
**entonces** se muestran simultáneamente la barra de scroll vertical en el lado derecho y la barra de scroll horizontal en la parte inferior **Y** puedo desplazarme verticalmente para ver más filas manteniendo los encabezados de columnas fijos en la parte superior **Y** puedo desplazarme horizontalmente para ver más columnas manteniendo la primera columna identificadora fija en el lado izquierdo **Y** puedo combinar ambos desplazamientos moviéndome en diagonal para navegar a cualquier celda de la matriz (por ejemplo, desplazarme hacia abajo y hacia la derecha simultáneamente) **Y** los elementos fijos (encabezados superiores y primera columna) permanecen visibles independientemente de la dirección del scroll **Y** puedo usar la rueda del mouse para scroll vertical y Shift+rueda para scroll horizontal **Y** en dispositivos táctiles, puedo usar gestos de dos dedos para desplazarme en ambas direcciones **Y** el desplazamiento es fluido y responsive sin lag, manteniendo al menos 60 fps **Y** hay indicadores visuales (sombras o gradientes) que muestran cuando hay más contenido fuera de vista en cualquier dirección **Y** puedo navegar a cualquier celda de la matriz sin importar su posición (esquina superior izquierda, centro, esquina inferior derecha) **Y** este comportamiento de scroll bidireccional funciona idénticamente en las tres matrices (RA vs OP, RAA vs RA, RA vs EUR-ACE) **Y** puedo analizar relaciones en cualquier parte de la matriz desplazándome libremente.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 3 – Scroll bidireccional en matriz grande con muchas filas y columnas**

### **Justificación:**

Este criterio es el más crítico porque representa el **caso de uso real más común** en matrices académicas y valida directamente el objetivo completo de la HU: "observar un scroll vertical y horizontal para desplazarme a través de la matriz". Las razones específicas son:

1. **Cumplimiento completo del objetivo de la HU:** El profesor/coordinador necesita "observar un scroll vertical Y horizontal" (no uno u otro). Este escenario valida que:
   - Ambos scrolls están disponibles simultáneamente
   - Funcionan de manera independiente y combinada
   - Permiten navegación completa por toda la matriz
   - El usuario puede desplazarse libremente en cualquier dirección

2. **Caso más común en matrices académicas reales:** En el contexto de acreditación y gestión curricular, las matrices típicamente son grandes:
   - **RAA vs RA:** 15-30 RAA × 10-20 RA = 150-600 celdas
   - **Asignatura vs EUR-ACE:** 30-50 asignaturas × 12 criterios = 360-600 celdas
   - **RA vs OP:** 20-40 RA × 5-10 OP = 100-400 celdas
   
   Es raro que una matriz académica real sea lo suficientemente pequeña para caber sin scroll bidireccional.

3. **Validación de funcionalidad compleja e integrada:** Este escenario valida la interacción más compleja:
   - Scroll vertical funciona mientras horizontal está presente
   - Scroll horizontal funciona mientras vertical está presente
   - Ambos scrolls no interfieren entre sí
   - Los elementos sticky (encabezados y primera columna) se mantienen correctamente con ambos scrolls activos
   - La performance se mantiene con contenido bidimensional grande

4. **Punto de fallo de mayor complejidad técnica:** Implementar scroll bidireccional con elementos sticky es técnicamente desafiante:
   - CSS: Requiere position:sticky en dos ejes simultáneamente
   - JavaScript: Puede requerir scroll listeners en ambas direcciones
   - Performance: Debe renderizar eficientemente contenido grande en 2D
   - Cross-browser: Debe funcionar en Chrome, Firefox, Safari, Edge
   - Responsive: Debe adaptarse a diferentes tamaños de pantalla
   
   Si este escenario complejo funciona, los casos más simples (M2, M3) funcionarán por transitividad.

5. **Habilitador crítico para análisis académico:** Los profesores y coordinadores necesitan scroll bidireccional para:
   - Analizar relaciones en toda la matriz, no solo en la porción visible inicial
   - Identificar patrones en asignaturas/RAA que están en la parte inferior
   - Revisar criterios/RA que están en columnas de la derecha
   - Hacer análisis comparativos entre elementos distantes en la matriz
   - Verificar completitud de la trazabilidad curricular
   
   Sin scroll bidireccional completo, el análisis se limita a una "ventana" pequeña de la matriz.

6. **Prevención de frustración del usuario:** Si el scroll bidireccional no funciona correctamente:
   - Usuario no puede ver relaciones importantes que están "escondidas"
   - Se siente limitado y frustrado al no poder navegar libremente
   - Puede concluir incorrectamente que faltan datos (cuando solo están fuera de vista)
   - La herramienta pierde utilidad práctica para matrices grandes

7. **Validación de elementos sticky críticos:** Este escenario valida que:
   - **Encabezados superiores permanecen fijos** durante scroll vertical (usuario siempre sabe qué RA/criterio está viendo)
   - **Primera columna permanece fija** durante scroll horizontal (usuario siempre sabe qué RAA/asignatura está viendo)
   - **Ambos permanecen fijos simultáneamente** durante scroll diagonal
   - Sin estos elementos fijos, el usuario se pierde en una matriz grande

8. **Experiencia de usuario moderna esperada:** Los usuarios modernos esperan:
   - Scroll fluido sin lag (60fps)
   - Elementos sticky que mantienen contexto
   - Capacidad de usar rueda del mouse, trackpad, touch
   - Indicadores visuales de contenido adicional
   - Navegación libre sin restricciones artificiales
   
   Este escenario valida todas estas expectativas de UX.

9. **Caso que abarca los demás escenarios:** 
   - Si funciona el scroll bidireccional (M5), entonces funcionan scroll vertical (M2) y horizontal (M3) individualmente
   - Los casos más simples son subconjuntos de este caso complejo
   - Validar M5 implica validar implícitamente M2 y M3

10. **Validación de performance crítica:** Con contenido bidimensional grande:
    - Renderizar 500+ celdas simultáneamente
    - Actualizar posición de scroll en dos ejes
    - Mantener elementos sticky sin flicker
    - Responder a input del usuario sin delay
    
    Este escenario estresa-prueba la implementación más que los casos simples.

11. **Consistencia entre 3 matrices:** El escenario especifica que debe funcionar idénticamente en las tres matrices:
    - RA vs OP
    - RAA vs RA
    - RA vs EUR-ACE
    
    Valida que la implementación es reutilizable y consistente, no específica de una matriz.

12. **Habilitador de todas las demás funcionalidades de matriz:** Otras funcionalidades de matriz dependen de scroll bidireccional:
    - Click en celdas para ver detalle (debe poder llegar a cualquier celda)
    - Filtrado por nivel de aporte (debe ver resultados filtrados en toda la matriz)
    - Búsqueda de asignaturas (debe poder desplazarse a resultados en cualquier posición)
    - Creación de relaciones (debe poder navegar a la celda objetivo)
    
    Sin scroll bidireccional funcional, estas funcionalidades se limitan a la porción visible.

13. **Validación de accesibilidad:** Este escenario incluye múltiples métodos de navegación:
    - Mouse + rueda (usuarios desktop)
    - Trackpad con gestos (usuarios laptop)
    - Touch con dos dedos (usuarios tablet/móvil)
    - Teclado con Shift+flechas (accesibilidad)
    
    Valida que la matriz es accesible para diferentes tipos de usuarios.

**Recomendación de prueba prioritaria:**
- Crear matrices de prueba grandes (30 filas × 15 columnas) y verificar scroll suave en ambas direcciones
- Validar que encabezados permanecen sticky durante scroll vertical
- Validar que primera columna permanece sticky durante scroll horizontal
- Probar scroll diagonal (vertical + horizontal simultáneo) para verificar que no interfieren
- Medir FPS durante scroll para confirmar que mantiene 60fps sin drops
- Probar en Chrome, Firefox, Safari y Edge para confirmar compatibilidad cross-browser
- Validar en diferentes tamaños de pantalla (desktop, tablet, móvil)
- Probar con rueda del mouse, trackpad, touch y teclado
- Verificar que funciona idénticamente en las 3 matrices del sistema
- Incluir en regresión crítica para cambios en componentes de matriz
- Probar casos edge: matriz muy larga (100 filas), matriz muy ancha (30 columnas)

**Sin este escenario funcionando, el profesor/coordinador no puede "desplazarse a través de la matriz"** de manera efectiva para ver todas las relaciones y realizar análisis completo. Las matrices académicas reales son grandes y complejas, y requieren navegación bidireccional fluida. Este escenario valida que la implementación no es solo técnicamente correcta, sino prácticamente útil para el trabajo académico real de gestión curricular y acreditación.