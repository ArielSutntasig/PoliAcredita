# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 5 del prototipo):**

1. **C1:** Existen facultades registradas en el sistema con carreras asociadas
2. **C2:** El dropdown "Filtrar por Carreras" está en su estado por defecto (sin filtro aplicado)
3. **C3:** Se selecciona un criterio de filtrado del dropdown "Filtrar por Carreras"
4. **C4:** Existen facultades que cumplen con el criterio de filtrado seleccionado
5. **C5:** Hay otros filtros o búsqueda activos simultáneamente (campo de búsqueda)
6. **C6:** La cantidad de resultados filtrados requiere paginación

### **Acciones del Sistema (observadas en Imagen 5):**

1. **A1:** Mostrar dropdown "Filtrar por Carreras" con flecha desplegable habilitado
2. **A2:** Desplegar lista de opciones de filtrado basadas en rangos o cantidad de carreras
3. **A3:** Actualizar el valor del dropdown con el criterio seleccionado
4. **A4:** Filtrar la tabla automáticamente sin recargar la página
5. **A5:** Mostrar únicamente las facultades que cumplen con el criterio de cantidad de carreras
6. **A6:** Ocultar todas las facultades que no cumplen con el criterio
7. **A7:** Mantener visible la estructura completa de la tabla con columnas: "Código", "Nombre", "Carreras", "Decano", "Acciones"
8. **A8:** Ordenar resultados por cantidad de carreras (ascendente o descendente)
9. **A9:** Mantener visibles los valores numéricos en la columna "Carreras"
10. **A10:** Mostrar mensaje o tabla vacía cuando no hay facultades que cumplan el criterio
11. **A11:** Actualizar controles de paginación según cantidad de resultados filtrados
12. **A12:** Aplicar filtro de carreras en combinación con otros filtros activos (búsqueda)

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen facultades con carreras
- **C2:** Se selecciona criterio de filtrado
- **C3:** Hay facultades que cumplen el criterio
- **C4:** Hay otros filtros activos

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Facultades existen | C2: Criterio seleccionado | C3: Hay coincidencias | C4: Otros filtros | Acción |
|-------|----------------------|--------------------------|---------------------|------------------|---------|
| R1 | N | N | N | N | A1: Mostrar dropdown sin datos |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber coincidencias sin facultades) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A10: Mostrar tabla vacía |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A7: Mostrar todas las facultades sin filtro |
| R10 | S | N | - | S | A7, A12: Mostrar facultades según otros filtros |
| R11 | S | S | N | N | A3, A4, A10: Mostrar mensaje "Sin resultados" |
| R12 | S | S | N | S | A3, A4, A10, A12: Sin resultados con múltiples filtros |
| R13 | S | S | S | N | A3, A4, A5, A6, A7, A9, A11: Filtrar y mostrar facultades |
| R14 | S | S | S | S | A3, A4, A5, A6, A7, A9, A11, A12: Filtrar combinando criterios |

---

## **Tabla de Decisión Minimizada**

| Regla | Facultades existen | Criterio seleccionado | Hay coincidencias | Otros filtros | Acción |
|-------|-------------------|----------------------|-------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar dropdown pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todas las facultades sin filtro |
| **R3** | S | N | - | S | Mostrar facultades según otros filtros activos |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para el criterio" |
| **R5** | S | S | S | N | Filtrar por cantidad de carreras solamente |
| **R6** | S | S | S | S | Filtrar por carreras Y combinar con otros filtros |

**Justificación de la minimización:**
- **R1:** Si no hay facultades, el filtro no tiene datos sobre los cuales operar (fusiona R1, R5)
- **R2:** Estado inicial sin filtro de carreras, sin otros filtros (R9)
- **R3:** Estado sin filtro de carreras pero con búsqueda activa (R10)
- **R4:** Filtro aplicado pero sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: filtrar solo por cantidad de carreras (R13)
- **R6:** Caso avanzado: filtrar por carreras en combinación con búsqueda (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de filtrado)
- 3 escenarios adicionales específicos observados en el prototipo:
  - Interacción con el dropdown (desplegar opciones de filtrado)
  - Filtrado por rangos específicos de carreras (ej: 1-3, 4-6, 7+)
  - Cambio dinámico entre diferentes criterios de filtrado

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder y desplegar opciones del filtro de carreras**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** estoy en la pantalla "Gestión de Facultades",  
**cuando** ubico el dropdown "Filtrar por Carreras" en la sección de filtros superior,  
**entonces** se muestra el dropdown con el texto por defecto "Filtrar por Carreras" **Y** el dropdown está habilitado para interacción **Y** se muestra una flecha desplegable indicando que es un menú interactivo,  
**cuando** hago clic en el dropdown "Filtrar por Carreras",  
**entonces** se despliega una lista con opciones de filtrado basadas en cantidad de carreras **Y** las opciones incluyen rangos como: "1-3 carreras", "4-6 carreras", "7 o más carreras" **O** criterios como: "Pocas carreras (1-3)", "Cantidad media (4-6)", "Muchas carreras (7+)" **Y** todas las opciones son claramente legibles **Y** puedo seleccionar cualquier opción de la lista.

---

**Escenario 2 – Filtrar facultades con pocas carreras (1-3)**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades registradas con diferentes cantidades de carreras asociadas **Y** el dropdown "Filtrar por Carreras" está en su estado por defecto,  
**cuando** hago clic en el dropdown "Filtrar por Carreras" **Y** selecciono la opción "1-3 carreras" o "Pocas carreras" de la lista,  
**entonces** el dropdown se actualiza mostrando el criterio seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las facultades que tienen entre 1 y 3 carreras asociadas **Y** basado en los datos observados, se muestran facultades como: "FICM - Facultad de Ingeniería en Ciencias de la Tierra" con 3 carreras, "FA - Facultad de Artes" con 2 carreras **Y** se ocultan todas las facultades con 4 o más carreras **Y** en la columna "Carreras" de las filas mostradas aparecen valores numéricos entre 1 y 3 **Y** se mantienen visibles todas las columnas: "Código", "Nombre", "Carreras", "Decano", "Acciones" **Y** los iconos de editar y eliminar permanecen disponibles **Y** los controles de paginación se actualizan según la cantidad de facultades filtradas.

---

**Escenario 3 – Filtrar facultades con cantidad media de carreras (4-6)**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades con cantidad media de carreras,  
**cuando** selecciono la opción "4-6 carreras" o "Cantidad media" del dropdown "Filtrar por Carreras",  
**entonces** el dropdown se actualiza con el criterio seleccionado **Y** la tabla se actualiza automáticamente **Y** se muestran únicamente las facultades que tienen entre 4 y 6 carreras asociadas **Y** basado en los datos observados, se muestran facultades como: "FIEE - Facultad de Ingeniería Eléctrica y Electrónica" con 5 carreras, "FAD - Facultad de Administración" con 4 carreras, "FCyS - Facultad de Ciencias y Sistemas" con 6 carreras **Y** se ocultan las facultades con 1-3 carreras y las que tienen 7 o más carreras **Y** en la columna "Carreras" aparecen valores numéricos entre 4 y 6 **Y** la respuesta visual es inmediata al cambio de filtro.

---

**Escenario 4 – Filtrar facultades con muchas carreras (7 o más)**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades con 7 o más carreras asociadas,  
**cuando** selecciono la opción "7 o más carreras" o "Muchas carreras" del dropdown "Filtrar por Carreras",  
**entonces** el dropdown se actualiza con el criterio seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las facultades que tienen 7 o más carreras asociadas **Y** basado en los datos observados, se muestra la facultad: "FCI - Facultad de Ciencias Informáticas" con 7 carreras **Y** se ocultan todas las facultades con menos de 7 carreras **Y** en la columna "Carreras" de las filas mostradas aparecen valores numéricos de 7 o superiores **Y** la tabla mantiene su estructura completa.

---

**Escenario 5 – Mostrar mensaje cuando no hay facultades en el rango seleccionado**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades registradas en el sistema,  
**cuando** selecciono un criterio de filtrado del dropdown "Filtrar por Carreras" (ej: "10 o más carreras") **Y** ninguna facultad tiene esa cantidad de carreras asociadas,  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron facultades con el criterio seleccionado" o "Sin resultados para este rango de carreras" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el dropdown "Filtrar por Carreras" conserva el valor seleccionado **Y** los demás controles de filtrado permanecen disponibles para modificar los criterios **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 6 – Combinar filtro de carreras con búsqueda por texto**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** he seleccionado un criterio del dropdown "Filtrar por Carreras" (ej: "4-6 carreras"),  
**cuando** ingreso texto en el campo de búsqueda "Buscar por código o nombre..." (ej: "Ingeniería"),  
**entonces** la tabla muestra únicamente las facultades que tienen entre 4 y 6 carreras asociadas Y cuyo código o nombre contiene "Ingeniería" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** se excluyen las facultades con 4-6 carreras cuyo nombre no contiene "Ingeniería" **Y** se excluyen las facultades cuyo nombre contiene "Ingeniería" pero tienen diferente cantidad de carreras **Y** ambos controles (dropdown y búsqueda) reflejan los valores aplicados **Y** el filtrado es dinámico mientras escribo en el campo de búsqueda.

---

**Escenario 7 – Quitar filtro de carreras para visualizar todas las facultades**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** tengo un criterio específico seleccionado en el dropdown "Filtrar por Carreras" (ej: "1-3 carreras") **Y** la tabla muestra facultades filtradas por ese criterio,  
**cuando** hago clic en el dropdown "Filtrar por Carreras" **Y** selecciono la opción por defecto "Filtrar por Carreras" o "Todas",  
**entonces** el dropdown se actualiza mostrando el texto por defecto "Filtrar por Carreras" **Y** el filtro de cantidad de carreras se elimina **Y** la tabla se actualiza automáticamente mostrando todas las facultades registradas sin filtro de carreras **Y** se restablecen las filas originales con todas las facultades independientemente de su cantidad de carreras **Y** se mantienen activos cualquier otro filtro que esté aplicado (búsqueda) **Y** los controles de paginación se actualizan según el total de facultades sin filtrar.

---

**Escenario 8 – Cambiar dinámicamente entre diferentes rangos de carreras**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** tengo aplicado un filtro de carreras (ej: "1-3 carreras") **Y** la tabla muestra facultades con pocas carreras,  
**cuando** cambio la selección del dropdown "Filtrar por Carreras" a un rango diferente (ej: "7 o más carreras"),  
**entonces** el dropdown se actualiza inmediatamente con "7 o más carreras" **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se ocultan todas las facultades con 1-3 carreras **Y** se muestran únicamente las facultades con 7 o más carreras **Y** la transición entre filtros es fluida e inmediata **Y** no se requiere hacer clic en ningún botón adicional para aplicar el cambio **Y** se mantiene la consistencia visual de la tabla durante el cambio **Y** todos los valores en la columna "Carreras" de las filas mostradas cumplen con el nuevo criterio.

---

**Escenario 9 – Ordenar facultades filtradas por cantidad de carreras**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** he aplicado un filtro de carreras que muestra múltiples facultades (ej: "4-6 carreras"),  
**cuando** la tabla muestra las facultades filtradas,  
**entonces** las facultades se presentan organizadas de manera lógica **Y** opcionalmente se ordenan por cantidad de carreras en orden ascendente (menor a mayor) o descendente (mayor a menor) **Y** puedo visualizar claramente la distribución de facultades según su cantidad de carreras **Y** la columna "Carreras" muestra los valores numéricos que facilitan la comparación **Y** la organización visual ayuda a identificar rápidamente la carga de gestión de cada facultad **Y** puedo hacer clic en el encabezado de la columna "Carreras" para alternar el orden de clasificación si esta funcionalidad está disponible.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Filtrar facultades con cantidad media de carreras (4-6)**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que la Autoridad quiere "filtrar el listado de facultades por carrera para organizar la visualización por la cantidad de carreras que gestionan". El Escenario 3 valida directamente esta capacidad con el rango más representativo y equilibrado del sistema.

2. **Representa el caso de uso más frecuente:** El rango de 4-6 carreras es el más poblado según los datos observados en el prototipo:
   - FIEE: 5 carreras
   - FAD: 4 carreras
   - FCyS: 6 carreras
   - Tres facultades en este rango vs. dos en rango bajo (1-3) y una en rango alto (7+)

3. **Mayor valor para gestión académica:** Las facultades con cantidad media de carreras (4-6) son las que requieren:
   - Atención balanceada en términos de recursos
   - Gestión compleja pero no excesiva
   - Mayor frecuencia de revisión administrativa
   - Equilibrio entre especialización y diversidad académica

4. **Valida el mecanismo completo de filtrado:** Verifica todos los aspectos críticos del filtrado:
   - Interacción correcta con el dropdown
   - Actualización automática de la tabla
   - Visualización de múltiples resultados (no solo uno)
   - Ocultación efectiva de facultades que no cumplen el criterio
   - Preservación de estructura y funcionalidades

5. **Proporciona datos suficientes para validación:** A diferencia de:
   - Rango bajo (1-3): Solo 2 facultades, puede ser caso límite
   - Rango alto (7+): Solo 1 facultad, dificulta validar comportamiento con múltiples resultados
   - Rango medio (4-6): 3 facultades, suficientes para validar listado plural pero manejable

6. **Habilita comparación y análisis efectivo:** Con 3 facultades visibles simultáneamente, la Autoridad puede:
   - Comparar la distribución de carreras dentro del rango
   - Evaluar diferentes decanos gestionando cargas similares
   - Identificar patrones de organización académica
   - Tomar decisiones sobre redistribución de recursos

7. **Fundamento para otros escenarios:** Los escenarios de rangos extremos (2 y 4) son casos límite que validan los bordes del sistema, pero el Escenario 3 valida el comportamiento estándar que se usará más frecuentemente en operaciones normales.

8. **Refleja realidad operativa institucional:** En una institución académica real, la mayoría de facultades tienden a tener una cantidad media de carreras (ni muy pocas ni excesivas), haciendo este el caso de uso más alineado con la realidad operativa de la EPN.

9. **Impacto directo en planificación académica:** La capacidad de filtrar facultades con cantidad media de carreras es crítica para:
   - **Planificación de recursos:** Identificar facultades con carga similar para asignación equitativa
   - **Benchmarking interno:** Comparar facultades con complejidad similar
   - **Gestión de decanos:** Evaluar cargas de trabajo comparables
   - **Reorganización académica:** Identificar oportunidades de consolidación o división

10. **Mayor probabilidad de uso en producción:** Basado en la distribución de datos observada, el filtro de 4-6 carreras será el más utilizado por las autoridades en operaciones diarias, haciendo que cualquier defecto en este escenario tenga mayor impacto en la experiencia del usuario.

Los demás escenarios complementan esta funcionalidad (rangos extremos, combinación de filtros, cambio dinámico), pero el Escenario 3 es el que garantiza que el sistema cumple su propósito esencial con el caso de uso más representativo y frecuente: **permitir a la Autoridad filtrar y visualizar efectivamente las facultades por su cantidad de carreras para organizar y gestionar la estructura académica de manera eficiente, validando el comportamiento con un conjunto significativo de resultados que refleja la realidad operativa de la institución**.