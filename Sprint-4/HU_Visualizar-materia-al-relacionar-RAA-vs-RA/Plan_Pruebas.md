# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: VISUALIZAR MATERIA AL RELACIONAR RAA VS RA**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar materia al relacionar RAA vs RA - Escenario 1 – Visualizar materia con matriz RAA vs RA activa | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Profesor<br>*El usuario debe tener la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" seleccionada | Verificar visualización correcta de la matriz RAA vs RA con el nombre de la asignatura visible | Matrices - RAA vs RA | Profesor | Paso1 | En el menú lateral izquierdo, sección "MATRICES", hacer clic en la pestaña "Matriz RAA vs RA" | *Se navega a la matriz RAA vs RA<br>*Se muestra el nombre completo de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" en el encabezado principal de la página<br>*Se presenta el título "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el toggle de vista y el dropdown de filtro | *Se muestra el toggle con las opciones "Resultados de Aprendizaje de Asignatura" y "Resultados de Aprendizaje Carrera"<br>*El toggle está posicionado en "Resultados de Aprendizaje de Asignatura" (opción izquierda en azul)<br>*Se muestra el dropdown "Filtrar por Nivel de Aporte"<br>*Se presenta el botón "+ Nueva Relación" en la esquina superior derecha | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar la estructura de la matriz | *Se presenta la matriz con los RAA de la asignatura en las filas del eje Y: 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1 con fondo azul<br>*Se muestran los RA de carrera en las columnas del eje X: RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6<br>*Cada código de RAA y RA incluye un icono de información (i)<br>*La materia es claramente visible permitiendo identificar el contexto de las relaciones RAA-RA que se están observando | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar materia al relacionar RAA vs RA - Escenario 2 – Visualizar relaciones existentes entre RAA y RA de la materia | *El usuario debe estar visualizando la matriz RAA vs RA de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)"<br>*El toggle debe estar en "Resultados de Aprendizaje de Asignatura" | Verificar visualización correcta de las relaciones existentes entre RAA y RA de la asignatura específica | Matrices - RAA vs RA | Profesor | Paso1 | Observar el contenido de la matriz y las intersecciones con checkmarks | *Se muestran checkmarks (✓) con fondo verde/turquesa en las intersecciones donde existe una relación entre un RAA y un RA<br>*Las celdas sin relación permanecen vacías sin checkmark | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Verificar las relaciones específicas mostradas en la matriz | *Se visualizan las relaciones: RAA 1.1 con RE1, RAA 1.2 con RE2, RAA 1.3 con RG2, RAA 1.4 con RG3, RAA 2.1 con RE3, RAA 2.2 con RG1, RAA 2.2 con RE4, RAA 3.1 con RE6<br>*Se puede identificar visualmente y de forma rápida qué resultados de aprendizaje de esta asignatura específica contribuyen a qué resultados de aprendizaje de la carrera | ESTADO PRUEBA | Validar cada relación específica | | | |
| | | | | | | | | | Paso3 | Verificar visibilidad del contexto de la asignatura | *El nombre de la asignatura permanece visible en el encabezado confirmando el contexto de las relaciones que se están analizando | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Alta | HU: Visualizar materia al relacionar RAA vs RA - Escenario 3 – Cambiar vista a Resultados de Aprendizaje de Carrera | *El usuario debe estar visualizando la matriz RAA vs RA de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)"<br>*El toggle debe estar en "Resultados de Aprendizaje de Asignatura" | Verificar reorganización correcta de la matriz al cambiar toggle manteniendo visible el nombre de la asignatura | Matrices - RAA vs RA | Profesor | Paso1 | Hacer clic en la opción "Resultados de Aprendizaje Carrera" del toggle | *El toggle cambia de posición mostrando "Resultados de Aprendizaje Carrera" en azul (derecha) y "Resultados de Aprendizaje de Asignatura" en gris (izquierda) | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar la reorganización de la matriz | *La matriz se reorganiza mostrando los RA de carrera (RG1, RG2, RG3, RE1, RE2, RE3, etc.) en las filas del eje Y<br>*Los RAA de la asignatura (1.1, 1.2, 1.3, etc.) se muestran en las columnas del eje X<br>*Las relaciones existentes se mantienen visibles con checkmarks verdes en las intersecciones correspondientes pero en la nueva orientación | ESTADO PRUEBA | Validar que los ejes se invierten correctamente | | | |
| | | | | | | | | | Paso3 | Verificar persistencia del contexto y funcionalidad de alternancia | *El nombre de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" permanece visible en el encabezado<br>*Se puede alternar entre ambas vistas para analizar las relaciones desde diferentes perspectivas mientras siempre se observa la materia que se está analizando | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Visualizar materia al relacionar RAA vs RA

**Total de Casos de Prueba**: 3 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 3 casos (100%)

**Distribución por Complejidad**:
- Media: 2 casos (Escenarios 1, 2)
- Alta: 1 caso (Escenario 3)

**Roles Involucrados**: Profesor

**Módulos a Probar**: 
- Matrices - RAA vs RA

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   
   **Asignatura de prueba:**
   - Nombre completo: "Ingeniería de Software y Requerimientos (ISWD414)"
   - Código: ISWD414
   
   **RAA (Resultados de Aprendizaje de Asignatura):**
   - 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1
   
   **RA (Resultados de Aprendizaje de Carrera):**
   - RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6
   
   **Relaciones existentes RAA-RA:**
   - RAA 1.1 ↔ RE1
   - RAA 1.2 ↔ RE2
   - RAA 1.3 ↔ RG2
   - RAA 1.4 ↔ RG3
   - RAA 2.1 ↔ RE3
   - RAA 2.2 ↔ RG1
   - RAA 2.2 ↔ RE4
   - RAA 3.1 ↔ RE6

2. **Consideraciones Especiales**:
   - Esta HU es específica para el **rol Profesor**
   - El **contexto de la asignatura** (nombre completo) debe estar **siempre visible** en el encabezado
   - La funcionalidad principal es **visualizar** (no crear/editar) relaciones existentes
   - El toggle permite **dos orientaciones** de la misma matriz (RAA en Y vs RAA en X)
   - Cada código de RAA y RA debe tener un **ícono de información (i)** para tooltips/detalles
   - El botón "+ Nueva Relación" sugiere funcionalidad de creación (fuera del alcance de esta HU)
   - El dropdown "Filtrar por Nivel de Aporte" sugiere funcionalidad de filtrado (fuera del alcance de esta HU)

3. **Defectos Potenciales a Detectar**:
   - Nombre de asignatura no visible o incorrecto en encabezado
   - Toggle no funciona o no cambia de estado visual
   - Matriz no se reorganiza al cambiar toggle
   - Checkmarks no visibles o en posiciones incorrectas
   - Íconos de información (i) faltantes en RAA o RA
   - Relaciones incorrectas entre RAA y RA
   - Ejes X/Y no se invierten correctamente al cambiar toggle
   - Pérdida de relaciones al cambiar vista
   - Botón "+ Nueva Relación" no visible
   - Dropdown "Filtrar por Nivel de Aporte" no visible
   - Celdas vacías muestran checkmarks incorrectamente

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Visualizar matriz activa):
   - ✓ Nombre asignatura: "Ingeniería de Software y Requerimientos (ISWD414)" visible en encabezado
   - ✓ Título de matriz completo y correcto
   - ✓ Toggle visible con ambas opciones
   - ✓ Toggle en posición "Resultados de Aprendizaje de Asignatura" (izquierda, azul)
   - ✓ RAA en eje Y (filas): 1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1 con fondo azul
   - ✓ RA en eje X (columnas): RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6
   - ✓ Cada código tiene ícono (i)
   - ✓ Dropdown "Filtrar por Nivel de Aporte" visible
   - ✓ Botón "+ Nueva Relación" visible
   
   **Escenario 2** (Visualizar relaciones):
   - ✓ Checkmarks verdes/turquesa en intersecciones correctas
   - ✓ 8 relaciones específicas visibles:
     - 1.1-RE1 ✓
     - 1.2-RE2 ✓
     - 1.3-RG2 ✓
     - 1.4-RG3 ✓
     - 2.1-RE3 ✓
     - 2.2-RG1 ✓
     - 2.2-RE4 ✓
     - 3.1-RE6 ✓
   - ✓ Celdas sin relación vacías (sin checkmarks)
   - ✓ Nombre asignatura permanece visible
   - ✓ Identificación visual rápida de contribuciones
   
   **Escenario 3** (Cambiar vista toggle):
   - ✓ Al hacer clic: toggle cambia posición
   - ✓ "Resultados de Aprendizaje Carrera" en azul (derecha)
   - ✓ "Resultados de Aprendizaje de Asignatura" en gris (izquierda)
   - ✓ Matriz reorganizada: RA en eje Y (filas), RAA en eje X (columnas)
   - ✓ Relaciones mantienen checkmarks verdes en nueva orientación
   - ✓ Nombre asignatura permanece visible
   - ✓ Alternancia fluida entre vistas

5. **Estructura de la Matriz - Orientaciones**:

   **Vista 1: "Resultados de Aprendizaje de Asignatura" (Estado inicial)**
   ```
   EJE Y (Filas) = RAA (1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1) - Fondo azul
   EJE X (Columnas) = RA (RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6) - Fondo gris
   ```
   
   **Vista 2: "Resultados de Aprendizaje Carrera" (Después de toggle)**
   ```
   EJE Y (Filas) = RA (RG1, RG2, RG3, RE1, RE2, RE3, RE4, RE5, RE6)
   EJE X (Columnas) = RAA (1.1, 1.2, 1.3, 1.4, 2.1, 2.2, 3.1)
   ```
   
   **CRÍTICO**: Las relaciones se mantienen, solo cambia la orientación de la matriz.

6. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Usuario con rol Profesor autenticado
   - Asignatura "Ingeniería de Software y Requerimientos (ISWD414)" asignada al profesor
   - Base de datos con:
     - RAA de la asignatura (7 resultados)
     - RA de la carrera (9 resultados)
     - Relaciones RAA-RA predefinidas (8 relaciones)
   - Componente de matriz con toggle funcional
   - Lógica de reorganización de ejes al cambiar toggle

7. **Propósito de la HU**:
   - **Principal**: Permitir al profesor **visualizar el nombre de la asignatura** junto con las relaciones RAA-RA
   - **Contexto**: El profesor necesita tener claro **qué asignatura** está analizando mientras observa las relaciones
   - **Beneficio**: Evitar confusión al trabajar con múltiples asignaturas
   - **Funcionalidad clave**: El nombre de la asignatura debe permanecer **siempre visible** independientemente de la vista del toggle

8. **Elementos Visuales Críticos**:
   - **Encabezado principal**: "Ingeniería de Software y Requerimientos (ISWD414)" - Debe estar siempre visible
   - **Códigos de color**:
     - Azul oscuro: RAA (filas en vista 1) o toggle activo
     - Gris claro: RA (columnas en vista 1) o toggle inactivo
     - Verde/turquesa: Checkmarks de relaciones existentes
   - **Íconos (i)**: Deben aparecer en TODOS los códigos de RAA y RA
   - **Toggle**: Cambio visual claro entre estado activo (azul) e inactivo (gris)

9. **Orden de Ejecución Recomendado**:
   1. **Escenario 1**: Validar visualización inicial con nombre de asignatura visible
   2. **Escenario 2**: Validar relaciones existentes en vista por defecto
   3. **Escenario 3**: Validar reorganización de matriz y persistencia de nombre de asignatura

10. **Criterios de Éxito**:
    - Nombre de asignatura siempre visible en encabezado
    - Toggle funcional con cambio visual claro
    - Matriz se reorganiza correctamente al cambiar toggle
    - Relaciones (checkmarks) se mantienen visibles en ambas orientaciones
    - Todos los íconos (i) presentes
    - Identificación visual rápida de relaciones RAA-RA
    - Contexto de asignatura nunca se pierde

11. **Dependencias con Otras HUs**:
    - Esta HU es **específica del módulo de Matrices** para el rol Profesor
    - Puede tener dependencia con HUs de:
      - Seleccionar asignatura
      - Crear/editar relaciones RAA-RA (botón "+ Nueva Relación")
      - Filtrar por nivel de aporte (dropdown)
    - Es **independiente** de las HUs de reportes de Coordinador/CEI

12. **Diferencias vs Otros Roles**:
    - **Profesor**: Ve matriz RAA vs RA de SU asignatura asignada
    - **Coordinador/CEI**: Ven reportes globales con múltiples asignaturas
    - Esta HU es exclusiva del flujo de trabajo del Profesor en su asignatura