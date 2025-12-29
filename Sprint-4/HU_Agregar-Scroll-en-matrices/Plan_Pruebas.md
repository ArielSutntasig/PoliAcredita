# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: AGREGAR SCROLL EN MATRICES**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Media | HU: Agregar Scroll en matrices - Escenario 1 – Scroll vertical en matriz con muchas filas | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Profesor o Coordinador<br>*El usuario debe estar visualizando una matriz (RA vs OP, RAA vs RA, o RA vs EUR-ACE)<br>*La matriz debe tener más filas de las que caben en la pantalla visible (por ejemplo, 20+ asignaturas o 15+ RAA) | Verificar funcionamiento correcto del scroll vertical con encabezados de columnas fijos | Matrices - RA vs OP / RAA vs RA / RA vs EUR-ACE | Profesor / Coordinador | Paso1 | Cargar inicialmente la matriz con muchas filas (20+ elementos) | *Se muestra una barra de scroll vertical en el lado derecho de la matriz<br>*Los encabezados de las columnas (códigos de RA, criterios EUR-ACE, o nombres de OP) permanecen fijos en la parte superior de la matriz | ESTADO PRUEBA | La matriz debe tener suficientes filas para requerir scroll | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Arrastrar la barra de scroll vertical hacia abajo con el mouse | *La matriz se desplaza verticalmente mostrando las filas que estaban fuera de vista<br>*Los encabezados de columnas permanecen visibles y fijos durante todo el desplazamiento vertical<br>*Se pueden ver filas que inicialmente estaban ocultas en la parte inferior de la matriz<br>*El desplazamiento es suave y fluido sin saltos ni lag | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Usar la rueda del mouse para desplazarse verticalmente | *La matriz se desplaza verticalmente de manera suave<br>*Los encabezados permanecen fijos<br>*Se puede volver al inicio arrastrando el scroll hacia arriba | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Repetir la prueba en las otras dos matrices | *Este comportamiento es idéntico en las tres matrices del sistema (RA vs OP, RAA vs RA, RA vs EUR-ACE) | ESTADO PRUEBA | Validar en las 3 matrices | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Agregar Scroll en matrices - Escenario 2 – Scroll horizontal en matriz con muchas columnas | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Profesor o Coordinador<br>*El usuario debe estar visualizando una matriz (RA vs OP, RAA vs RA, o RA vs EUR-ACE)<br>*La matriz debe tener más columnas de las que caben en el ancho visible de la pantalla (por ejemplo, 9+ códigos de RA o 12+ criterios EUR-ACE) | Verificar funcionamiento correcto del scroll horizontal con primera columna fija | Matrices - RA vs OP / RAA vs RA / RA vs EUR-ACE | Profesor / Coordinador | Paso1 | Cargar inicialmente la matriz con muchas columnas (9+ elementos) | *Se muestra una barra de scroll horizontal en la parte inferior de la matriz<br>*La primera columna con los códigos o nombres (RAA, nombres de asignaturas, o códigos de RA) permanece fija en el lado izquierdo | ESTADO PRUEBA | La matriz debe tener suficientes columnas para requerir scroll | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Arrastrar la barra de scroll horizontal hacia la derecha con el mouse | *La matriz se desplaza horizontalmente mostrando las columnas que estaban fuera de vista<br>*La primera columna identificadora permanece visible y fija durante todo el desplazamiento horizontal<br>*Se pueden ver columnas adicionales de RA o criterios EUR-ACE que inicialmente estaban ocultas en el lado derecho<br>*El desplazamiento es suave y responsive sin saltos | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar retorno al inicio y comportamiento en gestos horizontales | *Se puede volver al inicio arrastrando el scroll hacia la izquierda<br>*Los gestos horizontales funcionan correctamente para desplazamiento | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Repetir la prueba en las otras dos matrices | *Este comportamiento es consistente en las tres matrices del sistema | ESTADO PRUEBA | Validar en las 3 matrices | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Agregar Scroll en matrices - Escenario 3 – Scroll bidireccional en matriz grande con muchas filas y columnas | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Profesor o Coordinador<br>*El usuario debe estar visualizando una matriz (RA vs OP, RAA vs RA, o RA vs EUR-ACE)<br>*La matriz debe tener tanto muchas filas como muchas columnas que exceden el espacio visible (por ejemplo, 20+ filas y 9+ columnas) | Verificar funcionamiento correcto del scroll bidireccional con elementos fijos en ambos ejes | Matrices - RA vs OP / RAA vs RA / RA vs EUR-ACE | Profesor / Coordinador | Paso1 | Cargar inicialmente la matriz grande con muchas filas y columnas | *Se muestran simultáneamente la barra de scroll vertical en el lado derecho y la barra de scroll horizontal en la parte inferior | ESTADO PRUEBA | La matriz debe requerir scroll en ambas direcciones | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Desplazarse verticalmente y verificar fijación de encabezados | *Se puede desplazar verticalmente para ver más filas manteniendo los encabezados de columnas fijos en la parte superior<br>*Los encabezados superiores permanecen visibles independientemente del scroll vertical | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Desplazarse horizontalmente y verificar fijación de primera columna | *Se puede desplazar horizontalmente para ver más columnas manteniendo la primera columna identificadora fija en el lado izquierdo<br>*La primera columna permanece visible independientemente del scroll horizontal | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso4 | Combinar desplazamientos verticales y horizontales simultáneamente | *Se pueden combinar ambos desplazamientos moviéndose en diagonal para navegar a cualquier celda de la matriz<br>*Los elementos fijos (encabezados superiores y primera columna) permanecen visibles independientemente de la dirección del scroll | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso5 | Usar rueda del mouse para scroll vertical y Shift+rueda para scroll horizontal | *La rueda del mouse desplaza verticalmente<br>*Shift+rueda desplaza horizontalmente<br>*El desplazamiento es fluido y responsive sin lag, manteniendo al menos 60 fps | ESTADO PRUEBA | | | No Funcional (Performance) | |
| | | | | | | | | | Paso6 | En dispositivos táctiles, usar gestos de dos dedos para desplazamiento | *Los gestos de dos dedos permiten desplazarse en ambas direcciones<br>*El desplazamiento táctil es suave y responsive | ESTADO PRUEBA | Solo aplica en dispositivos táctiles | | | |
| | | | | | | | | | Paso7 | Verificar indicadores visuales de contenido adicional | *Hay indicadores visuales (sombras o gradientes) que muestran cuando hay más contenido fuera de vista en cualquier dirección | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso8 | Navegar a diferentes posiciones de la matriz | *Se puede navegar a cualquier celda de la matriz sin importar su posición (esquina superior izquierda, centro, esquina inferior derecha)<br>*Se pueden analizar relaciones en cualquier parte de la matriz desplazándose libremente | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso9 | Repetir la prueba en las otras dos matrices | *Este comportamiento de scroll bidireccional funciona idénticamente en las tres matrices (RA vs OP, RAA vs RA, RA vs EUR-ACE) | ESTADO PRUEBA | Validar en las 3 matrices | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Agregar Scroll en matrices (RA-OP, RAA-RA, RA-EUR-ACE)

**Total de Casos de Prueba**: 3 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 3 casos (100%)

**Distribución por Complejidad**:
- Media: 2 casos (Escenarios 1, 2)
- Alta: 1 caso (Escenario 3)

**Roles Involucrados**: Profesor / Coordinador

**Módulos a Probar**: 
- Matrices - RA vs OP
- Matrices - RAA vs RA
- Matrices - RA vs EUR-ACE

**Tipo de Pruebas**: 
- Funcional (100%)
- No Funcional - Performance (Escenario 3, Paso 5)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Requisitos de Datos de Prueba**:
   
   **Para Scroll Vertical (Escenario 1):**
   - Matriz RA vs OP: 20+ Objetivos de Programa
   - Matriz RAA vs RA: 15+ Resultados de Aprendizaje de Asignatura
   - Matriz RA vs EUR-ACE: 20+ Resultados de Aprendizaje
   
   **Para Scroll Horizontal (Escenario 2):**
   - Matriz RA vs OP: 9+ códigos de RA en columnas
   - Matriz RAA vs RA: 9+ códigos de RA en columnas
   - Matriz RA vs EUR-ACE: 12+ criterios EUR-ACE en columnas
   
   **Para Scroll Bidireccional (Escenario 3):**
   - Combinación de ambos: 20+ filas Y 9+ columnas simultáneamente

2. **Consideraciones Especiales**:
   - Esta HU es **transversal** a tres matrices diferentes
   - Aplica a **DOS roles**: Profesor y Coordinador
   - Incluye validaciones de **performance** (60 fps mínimo)
   - Requiere pruebas en **dispositivos táctiles** además de desktop
   - Los **elementos fijos** son críticos:
     - **Encabezados de columnas** deben permanecer fijos en scroll vertical
     - **Primera columna** debe permanecer fija en scroll horizontal
   - El comportamiento debe ser **idéntico** en las 3 matrices
   - Requiere pruebas de **usabilidad** (suavidad, fluidez)

3. **Defectos Potenciales a Detectar**:
   - Barras de scroll no aparecen cuando deberían
   - Encabezados de columnas no permanecen fijos al hacer scroll vertical
   - Primera columna no permanece fija al hacer scroll horizontal
   - Scroll con saltos o lag (no fluido)
   - Performance inferior a 60 fps
   - Rueda del mouse no funciona para scroll
   - Shift+rueda no funciona para scroll horizontal
   - Gestos táctiles no funcionan
   - Indicadores visuales de contenido adicional ausentes
   - No se puede alcanzar ciertas celdas de la matriz
   - Comportamiento inconsistente entre las 3 matrices
   - Elementos fijos desaparecen o se desplazan incorrectamente
   - Scroll diagonal no funciona correctamente

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Scroll vertical):
   - ✓ Barra de scroll vertical visible
   - ✓ Encabezados de columnas fijos en la parte superior
   - ✓ Desplazamiento vertical suave con mouse drag
   - ✓ Rueda del mouse funciona para scroll vertical
   - ✓ Filas ocultas se hacen visibles al desplazarse
   - ✓ Encabezados permanecen visibles durante todo el scroll
   - ✓ Sin saltos ni lag
   - ✓ Puede volver al inicio
   - ✓ Comportamiento idéntico en 3 matrices
   
   **Escenario 2** (Scroll horizontal):
   - ✓ Barra de scroll horizontal visible
   - ✓ Primera columna fija en el lado izquierdo
   - ✓ Desplazamiento horizontal suave con mouse drag
   - ✓ Gestos horizontales funcionan
   - ✓ Columnas ocultas se hacen visibles al desplazarse
   - ✓ Primera columna permanece visible durante todo el scroll
   - ✓ Sin saltos, responsive
   - ✓ Puede volver al inicio
   - ✓ Comportamiento consistente en 3 matrices
   
   **Escenario 3** (Scroll bidireccional):
   - ✓ Ambas barras de scroll visibles simultáneamente
   - ✓ Scroll vertical con encabezados fijos
   - ✓ Scroll horizontal con primera columna fija
   - ✓ Scroll diagonal funciona (combinado)
   - ✓ Elementos fijos permanecen en ambas direcciones
   - ✓ Rueda del mouse para vertical
   - ✓ Shift+rueda para horizontal
   - ✓ Gestos de dos dedos en táctil
   - ✓ Performance ≥ 60 fps
   - ✓ Indicadores visuales de más contenido
   - ✓ Navegación a cualquier celda posible
   - ✓ Comportamiento idéntico en 3 matrices

5. **Elementos Fijos (Freeze Columns/Rows)**:

   | Dirección de Scroll | Elemento Fijo | Posición | Debe Permanecer Visible |
   |---------------------|---------------|----------|------------------------|
   | **Vertical** ↕ | Encabezados de columnas | Parte superior | SÍ, siempre |
   | **Horizontal** ↔ | Primera columna identificadora | Lado izquierdo | SÍ, siempre |
   | **Diagonal** ↗↘ | Ambos | Superior e izquierda | SÍ, ambos simultáneamente |

6. **Métodos de Interacción a Validar**:

   **Desktop:**
   - ✓ Arrastrar barra de scroll vertical
   - ✓ Arrastrar barra de scroll horizontal
   - ✓ Rueda del mouse (scroll vertical)
   - ✓ Shift + rueda del mouse (scroll horizontal)
   - ✓ Flechas del teclado (opcional)
   - ✓ Page Up/Page Down (opcional)
   
   **Dispositivos Táctiles:**
   - ✓ Gestos verticales (deslizar arriba/abajo)
   - ✓ Gestos horizontales (deslizar izquierda/derecha)
   - ✓ Gestos de dos dedos en cualquier dirección
   - ✓ Gesto diagonal

7. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Usuarios con roles Profesor y Coordinador autenticados
   - Matrices con datos suficientes:
     - **RA vs OP** con 20+ filas y 9+ columnas
     - **RAA vs RA** con 15+ filas y 9+ columnas
     - **RA vs EUR-ACE** con 20+ filas y 12+ columnas
   - Implementación de scroll con elementos fijos (sticky headers/columns)
   - Optimización para performance (≥60 fps)
   - Soporte para dispositivos táctiles

8. **Indicadores Visuales de Más Contenido**:
   
   Deben estar presentes cuando hay contenido oculto:
   - **Sombra superior**: Si hay contenido arriba (después de scroll hacia abajo)
   - **Sombra inferior**: Si hay contenido abajo
   - **Sombra izquierda**: Si hay contenido a la izquierda (después de scroll a derecha)
   - **Sombra derecha**: Si hay contenido a la derecha
   - **Gradientes**: Alternativamente, usar gradientes en lugar de sombras

9. **Métricas de Performance**:
   
   | Métrica | Requisito | Método de Medición |
   |---------|-----------|-------------------|
   | **Frame Rate** | ≥ 60 fps | Usar herramientas de desarrollo del navegador |
   | **Latencia de scroll** | < 16ms por frame | Verificar suavidad visual |
   | **Tiempo de respuesta** | Inmediato | No debe haber delay perceptible |
   | **Fluidez** | Sin saltos | Observación visual durante scroll |

10. **Matrices a Probar (Validar en TODAS)**:

    | Matriz | Descripción | Filas Típicas | Columnas Típicas |
    |--------|-------------|---------------|------------------|
    | **RA vs OP** | Resultados de Aprendizaje vs Objetivos de Programa | RAs de carrera | OPPs |
    | **RAA vs RA** | Resultados de Aprendizaje de Asignatura vs Resultados de Aprendizaje | RAAs (1.1, 1.2, etc.) | RAs (RG1, RE1, etc.) |
    | **RA vs EUR-ACE** | Resultados de Aprendizaje vs Criterios EUR-ACE | RAs de carrera | Criterios EUR-ACE (5.2.1, 5.3.1, etc.) |

11. **Orden de Ejecución Recomendado**:
    1. **Escenario 1**: Validar scroll vertical en cada una de las 3 matrices
    2. **Escenario 2**: Validar scroll horizontal en cada una de las 3 matrices
    3. **Escenario 3**: Validar scroll bidireccional en cada una de las 3 matrices

12. **Criterios de Éxito**:
    - Barras de scroll aparecen cuando son necesarias
    - Elementos fijos permanecen visibles durante todo el scroll
    - Desplazamiento suave y fluido (≥60 fps)
    - Todos los métodos de interacción funcionan correctamente
    - Indicadores visuales de contenido adicional presentes
    - Navegación a cualquier celda de la matriz posible
    - Comportamiento 100% consistente en las 3 matrices
    - Sin lag, saltos o errores visuales
    - Funciona en desktop y dispositivos táctiles

13. **Dependencias con Otras HUs**:
    - Esta HU es una **mejora de usabilidad** para todas las HUs de matrices
    - Depende de que las matrices estén implementadas:
      - HU de matriz RA vs OP
      - HU de matriz RAA vs RA
      - HU de matriz RA vs EUR-ACE
    - Es **transversal** y afecta la experiencia de usuario en todas las matrices

14. **Casos Límite a Considerar**:
    - ¿Qué pasa con matrices muy pequeñas que no requieren scroll?
    - ¿Las barras de scroll desaparecen apropiadamente?
    - ¿Qué pasa si cambia el tamaño de la ventana del navegador?
    - ¿El scroll se adapta dinámicamente?
    - ¿Funciona en navegadores móviles?
    - ¿Qué pasa con zoom del navegador (Ctrl +/-)?
    - ¿El scroll sigue funcionando correctamente?

15. **Diferencias entre Roles** (No aplica en esta HU):
    - Profesor y Coordinador tienen el **mismo comportamiento** de scroll
    - No hay restricciones diferentes por rol
    - Ambos roles deben tener la misma experiencia de usuario