# **PLAN DE PRUEBAS Y CASOS DE PRUEBA PARA HU: VISUALIZAR MATERIA AL CREAR RAA**

**Fecha de ejecución estimada para todos los casos: 28-10-2025**

---

| Fecha Ejecución Estimada | Modo Ejecución | Prioridad Testing | Complejidad | Nombre Testing | Pre-Condiciones | Descripción Caso | Módulo | Rol | Nombre Paso | Descripción Paso | Resultados Esperados | Resultados Obtenido | Restricciones | Tipo de Caso | Tipo de Prueba | Observaciones |
|--------------------------|----------------|-------------------|-------------|----------------|-----------------|------------------|--------|-----|-------------|------------------|----------------------|---------------------|---------------|--------------|----------------|---------------|
| 28-10-2025 | Manual | Alta | Baja | HU: Visualizar materia al crear RAA - Escenario 1 – Visualizar materia en vista de lista de RAA antes de crear | *El usuario debe estar autenticado en el sistema PoliAcredita<br>*El usuario debe tener rol de Profesor<br>*El usuario debe tener la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" seleccionada | Verificar visualización correcta del nombre de la asignatura en la vista de lista de RAA con botón de creación visible | Resultados de Aprendizaje - RAA | Profesor | Paso1 | En el menú de navegación, hacer clic en la pestaña "Resultados de Aprendizaje (RAA)" | *Se navega a la vista de lista de RAA<br>*Se muestra el nombre completo de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" en el encabezado principal de la página<br>*La pestaña "Resultados de Aprendizaje (RAA)" se presenta con fondo azul oscuro indicando que está activa | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar la tabla de RAA existentes | *Se muestra una tabla con los RAA existentes de la asignatura con las columnas: Código, Tipo, Descripción, Acciones<br>*La tabla presenta los datos correctamente estructurados | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Observar el botón de creación de nuevo RAA | *Se presenta el botón "+ Nuevo RAA" en la esquina superior derecha de color azul oscuro<br>*El botón está habilitado y es clickeable<br>*El nombre de la asignatura permanece claramente visible permitiendo confirmar que se está en el contexto correcto antes de crear un nuevo RAA | ESTADO PRUEBA | | | | |
| 28-10-2025 | Manual | Alta | Media | HU: Visualizar materia al crear RAA - Escenario 2 – Visualizar materia al iniciar creación de nuevo RAA | *El usuario debe estar visualizando la lista de RAA de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)"<br>*La pestaña "Resultados de Aprendizaje (RAA)" debe estar activa<br>*El nombre de la asignatura debe ser visible en el encabezado | Verificar persistencia del nombre de la asignatura al abrir formulario de creación de nuevo RAA | Resultados de Aprendizaje - RAA | Profesor | Paso1 | Hacer clic en el botón "+ Nuevo RAA" | *Se abre un formulario o modal para crear un nuevo RAA<br>*El nombre completo de la asignatura "Ingeniería de Software y Requerimientos (ISWD414)" permanece visible en el encabezado durante todo el proceso de creación | ESTADO PRUEBA | | Positivo | Funcional | |
| | | | | | | | | | Paso2 | Observar el formulario de creación de RAA | *El formulario incluye campos para definir el código, tipo y descripción del nuevo RAA<br>*El contexto de la materia está claro en todo momento permitiendo definir correctamente el RAA de esta asignatura específica<br>*No hay ambigüedad sobre para qué materia se está creando el RAA | ESTADO PRUEBA | | | | |
| | | | | | | | | | Paso3 | Verificar claridad del contexto de asociación | *Se puede proceder con confianza sabiendo que el RAA se asociará correctamente a "Ingeniería de Software y Requerimientos (ISWD414)"<br>*El nombre de la asignatura permanece consistentemente visible | ESTADO PRUEBA | | | | |

---

## **RESUMEN DEL PLAN DE PRUEBAS**

**Historia de Usuario**: Visualizar materia al crear RAA

**Total de Casos de Prueba**: 2 casos (1 caso por cada Criterio de Aceptación)

**Distribución por Prioridad**:
- Alta: 2 casos (100%)

**Distribución por Complejidad**:
- Baja: 1 caso (Escenario 1)
- Media: 1 caso (Escenario 2)

**Roles Involucrados**: Profesor

**Módulos a Probar**: 
- Resultados de Aprendizaje - RAA

**Tipo de Pruebas**: Funcional (100%)

**Tipo de Casos**: Positivo (100%)

**Fecha de Ejecución Estimada**: 28-10-2025

---

## **NOTAS IMPORTANTES PARA LA EJECUCIÓN**

1. **Datos de Prueba Requeridos**:
   
   **Asignatura de prueba:**
   - Nombre completo: "Ingeniería de Software y Requerimientos (ISWD414)"
   - Código: ISWD414
   
   **RAA existentes** (según imagen del prototipo):
   - Código: 1.1 (múltiples entradas)
   - Tipo: "De Conocimiento"
   - Descripción: "Conocer los componentes, tecnología, información e impacto social de los sistemas de información"

2. **Consideraciones Especiales**:
   - Esta HU es específica para el **rol Profesor** en el proceso de **creación** de RAA
   - El **nombre de la asignatura** debe estar **siempre visible** en el encabezado
   - El propósito es **evitar confusión** sobre para qué asignatura se está creando el RAA
   - La visibilidad del nombre es crítica en **DOS momentos**:
     1. **Antes** de hacer clic en "+ Nuevo RAA" (vista de lista)
     2. **Durante** el proceso de creación (formulario/modal abierto)
   - La pestaña activa debe tener **fondo azul oscuro** como indicador visual
   - El botón "+ Nuevo RAA" debe estar en la **esquina superior derecha** con **color azul oscuro**

3. **Defectos Potenciales a Detectar**:
   - Nombre de asignatura no visible o incorrecto en encabezado
   - Nombre de asignatura desaparece al abrir formulario de creación
   - Pestaña RAA no muestra fondo azul oscuro (no está activa visualmente)
   - Botón "+ Nuevo RAA" no visible o no clickeable
   - Botón "+ Nuevo RAA" en ubicación incorrecta o color incorrecto
   - Tabla de RAA no muestra las columnas especificadas
   - Formulario de creación no incluye campos requeridos (código, tipo, descripción)
   - Ambigüedad sobre la asignatura al crear RAA
   - Contexto de asignatura se pierde al navegar

4. **Validaciones Críticas por Escenario**:

   **Escenario 1** (Vista de lista antes de crear):
   - ✓ Nombre asignatura: "Ingeniería de Software y Requerimientos (ISWD414)" visible en encabezado
   - ✓ Pestaña "Resultados de Aprendizaje (RAA)" con fondo azul oscuro (activa)
   - ✓ Tabla con columnas: Código, Tipo, Descripción, Acciones
   - ✓ Botón "+ Nuevo RAA" en esquina superior derecha
   - ✓ Botón color azul oscuro
   - ✓ Botón habilitado y clickeable
   - ✓ Nombre asignatura claramente visible
   - ✓ Confirmación del contexto correcto antes de crear
   
   **Escenario 2** (Al iniciar creación):
   - ✓ Al hacer clic: formulario/modal se abre
   - ✓ Nombre asignatura "Ingeniería de Software y Requerimientos (ISWD414)" permanece visible
   - ✓ Visibilidad del nombre durante TODO el proceso
   - ✓ Formulario incluye campo "Código"
   - ✓ Formulario incluye campo "Tipo"
   - ✓ Formulario incluye campo "Descripción"
   - ✓ Contexto de materia claro en todo momento
   - ✓ Sin ambigüedad sobre asignatura asociada
   - ✓ Confianza de asociación correcta

5. **Estructura de la Vista RAA (según prototipo)**:

   **Elementos del Encabezado:**
   - Logo POLIACREDITA (esquina superior izquierda)
   - Indicador de rol: "Profesor" (esquina superior derecha)
   - Nombre de asignatura: "Ingeniería de Software y Requerimientos (ISWD414)" (principal y destacado)
   
   **Pestañas de Navegación:**
   - "Asignatura (PEA)" (inactiva, fondo gris claro)
   - "Resultados de Aprendizaje (RAA)" (ACTIVA, fondo azul oscuro)
   - "Matriz RAA vs RA" (inactiva, fondo gris claro)
   
   **Área de Contenido:**
   - Botón "+ Nuevo RAA" (esquina superior derecha, azul oscuro)
   - Tabla de RAA con 4 columnas
   - Paginación en la parte inferior
   - Botón "Cancelar" (esquina inferior derecha)

6. **Prerequisitos Técnicos**:
   - Sistema PoliAcredita accesible y funcional
   - Usuario con rol Profesor autenticado
   - Asignatura "Ingeniería de Software y Requerimientos (ISWD414)" asignada al profesor
   - Vista de lista de RAA funcional con tabla
   - Formulario/modal de creación de RAA implementado
   - Navegación por pestañas funcional

7. **Propósito de la HU**:
   - **Principal**: Asegurar que el profesor **siempre vea el nombre de la asignatura** al crear un RAA
   - **Contexto**: El profesor puede gestionar múltiples asignaturas y necesita confirmación visual constante
   - **Beneficio**: Evitar errores de asociación al crear RAA en la asignatura incorrecta
   - **Funcionalidad clave**: Persistencia del nombre de asignatura desde la vista de lista hasta el formulario de creación

8. **Comparación con HU Similar**:
   
   | Aspecto | HU: Visualizar materia al relacionar RAA vs RA | HU: Visualizar materia al crear RAA |
   |---------|-----------------------------------------------|-------------------------------------|
   | **Contexto** | Matriz RAA vs RA | Lista de RAA + Formulario de creación |
   | **Acción** | Relacionar RAA con RA | Crear nuevo RAA |
   | **Momento crítico** | Al ver/crear relaciones | Antes y durante creación |
   | **Objetivo** | Confirmar contexto al relacionar | Confirmar contexto al crear |

9. **Flujo Completo del Usuario**:
   ```
   1. Profesor selecciona asignatura "Ingeniería de Software y Requerimientos (ISWD414)"
   2. Hace clic en pestaña "Resultados de Aprendizaje (RAA)"
   3. Ve lista de RAA existentes con nombre de asignatura visible
   4. Hace clic en botón "+ Nuevo RAA"
   5. Se abre formulario de creación
   6. Nombre de asignatura PERMANECE visible
   7. Profesor completa campos con confianza
   8. RAA se crea asociado correctamente a la asignatura
   ```

10. **Orden de Ejecución Recomendado**:
    1. **Escenario 1**: Validar vista de lista con nombre de asignatura visible y botón de creación
    2. **Escenario 2**: Validar apertura de formulario y persistencia del nombre de asignatura

11. **Elementos de UI Críticos**:
    
    **Elementos que DEBEN permanecer visibles:**
    - ✓ Nombre completo de asignatura en encabezado: "Ingeniería de Software y Requerimientos (ISWD414)"
    - ✓ Código de asignatura: (ISWD414)
    
    **Elementos de navegación:**
    - ✓ Pestaña activa con fondo azul oscuro
    - ✓ Botón "+ Nuevo RAA" visible y accesible
    
    **Formulario de creación:**
    - ✓ Campo "Código" del RAA
    - ✓ Campo "Tipo" del RAA (ej: De Conocimiento, De Habilidad, etc.)
    - ✓ Campo "Descripción" del RAA

12. **Criterios de Éxito**:
    - Nombre de asignatura siempre visible en encabezado
    - Nombre permanece visible al abrir formulario de creación
    - Pestaña activa claramente identificada (azul oscuro)
    - Botón de creación visible y funcional
    - Formulario incluye todos los campos necesarios
    - Contexto de asignatura nunca ambiguo
    - Profesor puede crear RAA con confianza de asociación correcta

13. **Dependencias con Otras HUs**:
    - Esta HU puede tener dependencia con:
      - HU de seleccionar asignatura
      - HU de crear RAA (funcionalidad completa)
      - HU de listar RAA existentes
    - Es **prerequisito** para:
      - Crear RAA correctamente asociado
      - Relacionar RAA con RA en matriz

14. **Diferencias vs Otros Roles**:
    - **Profesor**: Crea RAA para SU asignatura asignada
    - **Coordinador/CEI**: No crean RAA, solo visualizan reportes
    - Esta HU es exclusiva del flujo de trabajo del Profesor en gestión de su asignatura

15. **Casos Límite a Considerar** (no cubiertos en esta HU pero relevantes):
    - ¿Qué pasa si el profesor cambia de asignatura mientras el formulario está abierto?
    - ¿El formulario se cierra o se actualiza el contexto?
    - ¿Hay validación para evitar crear RAA con código duplicado?
    - ¿El nombre de asignatura es clickeable para navegar o solo informativo?