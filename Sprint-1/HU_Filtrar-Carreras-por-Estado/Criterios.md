# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 10 del prototipo):**

1. **C1:** Existen carreras registradas en el sistema con estados asignados
2. **C2:** El dropdown "Todos los Estados" está en su estado por defecto (sin filtro aplicado)
3. **C3:** Se selecciona un estado específico del dropdown "Todos los Estados"
4. **C4:** Existen carreras con el estado seleccionado en la base de datos
5. **C5:** Hay otros filtros activos simultáneamente (búsqueda o dropdown "Todas las Facultades")

### **Acciones del Sistema (observadas en Imagen 10):**

1. **A1:** Mostrar dropdown "Todos los Estados" con flecha desplegable
2. **A2:** Desplegar lista de opciones de estado al hacer clic (probablemente "Activo", "Inactivo")
3. **A3:** Actualizar el valor del dropdown con el estado seleccionado
4. **A4:** Filtrar la tabla automáticamente sin recargar la página
5. **A5:** Mostrar únicamente las carreras que tienen el estado seleccionado
6. **A6:** Ocultar todas las carreras con estado diferente al seleccionado
7. **A7:** Mantener visible la estructura completa de la tabla: "Código", "Nombre", "Facultad", "Coordinador", "Acciones"
8. **A8:** Mantener visibles todos los datos de las carreras coincidentes
9. **A9:** Mostrar mensaje o tabla vacía cuando no hay carreras con el estado seleccionado
10. **A10:** Actualizar controles de paginación según cantidad de resultados filtrados
11. **A11:** Aplicar filtro de estado en combinación con otros filtros activos (búsqueda, facultad)

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen carreras con estados asignados
- **C2:** Se selecciona un estado específico
- **C3:** Hay carreras con el estado seleccionado
- **C4:** Hay otros filtros activos

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Carreras existen | C2: Estado seleccionado | C3: Carreras con ese estado | C4: Otros filtros | Acción |
|-------|---------------------|------------------------|----------------------------|------------------|---------|
| R1 | N | N | N | N | A1: Mostrar dropdown sin datos |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber carreras con estado sin carreras) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A9: Mostrar tabla vacía |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A7: Mostrar todas las carreras sin filtro |
| R10 | S | N | - | S | A7, A11: Mostrar carreras según otros filtros |
| R11 | S | S | N | N | A3, A4, A9: Mostrar mensaje "Sin resultados" |
| R12 | S | S | N | S | A3, A4, A9, A11: Sin resultados con múltiples filtros |
| R13 | S | S | S | N | A3, A4, A5, A6, A7, A8, A10: Filtrar y mostrar carreras |
| R14 | S | S | S | S | A3, A4, A5, A6, A7, A8, A10, A11: Filtrar combinando criterios |

---

## **Tabla de Decisión Minimizada**

| Regla | Carreras existen | Estado seleccionado | Carreras con ese estado | Otros filtros | Acción |
|-------|-----------------|---------------------|------------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar dropdown pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todas las carreras sin filtro de estado |
| **R3** | S | N | - | S | Mostrar carreras según otros filtros, sin filtro de estado |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para el estado" |
| **R5** | S | S | S | N | Filtrar por estado solamente |
| **R6** | S | S | S | S | Filtrar por estado Y combinar con otros filtros |

**Justificación de la minimización:**
- **R1:** Si no hay carreras, el filtro no tiene datos sobre los cuales operar (fusiona R1, R5)
- **R2:** Estado inicial sin filtro de estado aplicado, sin otros filtros (R9)
- **R3:** Estado sin filtro de estado pero con búsqueda/facultad activos (R10)
- **R4:** Filtro aplicado pero sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: filtrar solo por estado (R13)
- **R6:** Caso avanzado: filtrar por estado en combinación con otros filtros (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de filtrado)
- 2 escenarios adicionales específicos:
  - Interacción con el dropdown (desplegar opciones)
  - Cambio dinámico entre diferentes estados

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder y desplegar opciones del filtro de estados**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** estoy en la pantalla "Gestión de Carreras",  
**cuando** ubico el dropdown "Todos los Estados" en la sección de filtros superior,  
**entonces** se muestra el dropdown con el texto por defecto "Todos los Estados" **Y** el dropdown está habilitado para interacción **Y** se muestra una flecha desplegable indicando que es un menú interactivo,  
**cuando** hago clic en el dropdown "Todos los Estados",  
**entonces** se despliega una lista con las opciones de estado disponibles en el sistema **Y** la lista incluye las opciones: "Activo" e "Inactivo" (o estados definidos en el sistema) **Y** todas las opciones son claramente legibles **Y** puedo seleccionar cualquier opción de la lista.

---

**Escenario 2 – Filtrar carreras por estado "Activo"**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras registradas con diferentes estados (Activo e Inactivo) **Y** el dropdown "Todos los Estados" está en su estado por defecto,  
**cuando** hago clic en el dropdown "Todos los Estados" **Y** selecciono la opción "Activo" de la lista,  
**entonces** el dropdown se actualiza mostrando "Activo" como valor seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las carreras que tienen estado "Activo" **Y** se ocultan todas las carreras con estado "Inactivo" **Y** se mantienen visibles todas las columnas: "Código", "Nombre", "Facultad", "Coordinador", "Acciones" **Y** se conservan todos los datos completos de las carreras activas **Y** los iconos de editar (lápiz) y eliminar (papelera) permanecen disponibles **Y** los controles de paginación se actualizan según la cantidad de carreras activas.

---

**Escenario 3 – Filtrar carreras por estado "Inactivo"**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras con estado "Inactivo" en el sistema,  
**cuando** hago clic en el dropdown "Todos los Estados" **Y** selecciono la opción "Inactivo" de la lista,  
**entonces** el dropdown se actualiza mostrando "Inactivo" como valor seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las carreras que tienen estado "Inactivo" **Y** se ocultan todas las carreras con estado "Activo" **Y** se mantiene la estructura completa de la tabla **Y** la respuesta visual es inmediata al cambio de filtro.

---

**Escenario 4 – Mostrar mensaje cuando no hay carreras con el estado seleccionado**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras registradas en el sistema,  
**cuando** selecciono un estado específico del dropdown "Todos los Estados" (ej: "Inactivo") **Y** todas las carreras en la base de datos tienen el estado opuesto (ej: todas son "Activo"),  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron carreras con el estado seleccionado" o "Sin resultados" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el dropdown "Todos los Estados" conserva el valor seleccionado ("Inactivo") **Y** los demás controles de filtrado permanecen disponibles para modificar los criterios **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 5 – Combinar filtro de estado con búsqueda**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras con diversos estados,  
**cuando** selecciono un estado específico del dropdown "Todos los Estados" (ej: "Activo") **Y** ingreso texto en el campo de búsqueda "Buscar carrera..." (ej: "Ingeniería"),  
**entonces** la tabla muestra únicamente las carreras que tienen estado "Activo" Y cuyo código o nombre contiene "Ingeniería" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** se excluyen las carreras activas que no contienen "Ingeniería" **Y** se excluyen las carreras que contienen "Ingeniería" pero tienen estado "Inactivo" **Y** ambos controles (dropdown y búsqueda) reflejan los valores aplicados **Y** el filtrado es dinámico mientras escribo.

---

**Escenario 6 – Combinar filtro de estado con filtro de facultad**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras con diversos estados y facultades,  
**cuando** selecciono un estado del dropdown "Todos los Estados" (ej: "Activo") **Y** selecciono una facultad del dropdown "Todas las Facultades" (ej: "Facultad de Ingeniería de Sistemas"),  
**entonces** la tabla muestra únicamente las carreras que tienen estado "Activo" Y pertenecen a "Facultad de Ingeniería de Sistemas" **Y** se aplican ambos criterios simultáneamente **Y** se excluyen carreras activas de otras facultades **Y** se excluyen carreras de la facultad seleccionada con estado diferente **Y** ambos dropdowns reflejan los valores seleccionados **Y** la tabla se actualiza sin recargar la página.

---

**Escenario 7 – Quitar filtro de estado para visualizar todas las carreras**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** tengo un estado específico seleccionado en el dropdown "Todos los Estados" (ej: "Activo") **Y** la tabla muestra carreras filtradas por ese estado,  
**cuando** hago clic en el dropdown "Todos los Estados" **Y** selecciono nuevamente la opción "Todos los Estados",  
**entonces** el dropdown se actualiza mostrando "Todos los Estados" **Y** el filtro de estado se elimina **Y** la tabla se actualiza automáticamente mostrando todas las carreras registradas sin filtro de estado **Y** se muestran carreras con estado "Activo" e "Inactivo" simultáneamente **Y** se restablecen las filas originales con todas las carreras **Y** se mantienen activos cualquier otro filtro que esté aplicado (búsqueda, facultad) **Y** los controles de paginación se actualizan según el total de carreras sin filtrar.

---

**Escenario 8 – Cambiar dinámicamente entre diferentes estados**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** tengo aplicado un filtro de estado (ej: "Activo") **Y** la tabla muestra carreras con estado activo,  
**cuando** cambio la selección del dropdown "Todos los Estados" al estado opuesto (ej: "Inactivo"),  
**entonces** el dropdown se actualiza inmediatamente con "Inactivo" **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se ocultan todas las carreras con estado "Activo" **Y** se muestran únicamente las carreras con estado "Inactivo" **Y** la transición entre filtros es fluida e inmediata **Y** no se requiere hacer clic en ningún botón adicional para aplicar el cambio **Y** se mantiene la consistencia visual de la tabla durante el cambio **Y** todas las carreras mostradas cumplen con el nuevo criterio de estado seleccionado.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Filtrar carreras por estado "Activo"**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que la Autoridad quiere "filtrar carreras por estado para organizar la visualización". El Escenario 2 valida directamente la capacidad de filtrar por el estado más relevante operativamente: "Activo", que representa las carreras vigentes y en oferta.

2. **Representa el caso de uso más frecuente:** Filtrar por estado "Activo" es el escenario más común porque:
   - Las autoridades necesitan visualizar regularmente las carreras en oferta actual
   - Es el estado operativo principal para gestión académica
   - Permite organizar la vista enfocándose en lo que está activo/vigente
   - Es más frecuente que filtrar por "Inactivo" (carreras suspendidas o descontinuadas)

3. **Mayor valor para organización de la visualización (objetivo de la HU):** Filtrar por "Activo" organiza porque:
   - Reduce el ruido visual eliminando carreras no vigentes
   - Permite concentrarse en la oferta académica actual
   - Facilita la gestión diaria al mostrar solo lo relevante
   - Simplifica la toma de decisiones sobre carreras operativas

4. **Valida comportamiento completo del filtro:** Verifica todos los aspectos críticos del filtrado:
   - Interacción correcta con el dropdown
   - Actualización automática sin recarga
   - Visualización exclusiva de carreras filtradas
   - Ocultación de carreras no coincidentes
   - Preservación de estructura y funcionalidades
   - Actualización de controles de paginación

5. **Impacto directo en gestión operativa:** Filtrar por "Activo" permite:
   - Gestionar eficientemente la oferta académica vigente
   - Planificar recursos para carreras operativas
   - Revisar coordinadores de carreras activas
   - Tomar decisiones sobre carreras en funcionamiento

6. **Fundamento para otros escenarios:** Los escenarios de filtrado por "Inactivo" (3), combinación (5-6), y cambio dinámico (8) son extensiones de esta funcionalidad base. Si el filtrado por "Activo" falla, las demás capacidades carecen de fundamento.

7. **Mayor relevancia para organización académica:** Las carreras activas son las que:
   - Requieren gestión constante
   - Tienen estudiantes matriculados
   - Necesitan supervisión de coordinadores
   - Demandan actualización curricular

8. **Precedencia operativa:** En la práctica académica:
   - Se revisa el estado activo con mayor frecuencia
   - Las decisiones estratégicas se toman sobre carreras activas
   - Los reportes y análisis se enfocan en lo vigente
   - La oferta pública se basa en carreras activas

9. **Validación de organización efectiva:** Solo con filtrado efectivo por "Activo", la Autoridad puede:
   - Organizar la vista para enfoque operativo
   - Reducir complejidad visual
   - Priorizar información relevante
   - Facilitar navegación en la interfaz

10. **Refleja el flujo operativo principal:** El prototipo (Imagen 10) muestra una interfaz diseñada para gestión activa, donde filtrar por estado "Activo" es el caso de uso que más valor aporta a la organización de la visualización.

Los demás escenarios son importantes para completitud (filtrar inactivos, casos sin resultados) y características avanzadas (combinación de filtros, cambio dinámico), pero el Escenario 2 es el que garantiza que el sistema cumple su promesa fundamental: **permitir a la Autoridad filtrar carreras por estado "Activo" para organizar efectivamente la visualización enfocándose en la oferta académica vigente y operativa, que es el caso de uso principal y de mayor valor para la gestión académica diaria**.