# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 10 del prototipo):**

1. **C1:** Existen carreras registradas en el sistema
2. **C2:** Las carreras están asociadas a diferentes facultades
3. **C3:** El dropdown "Todas las Facultades" está en su estado por defecto (sin filtro)
4. **C4:** Se selecciona una facultad específica del dropdown
5. **C5:** Existen carreras asociadas a la facultad seleccionada
6. **C6:** Hay otros filtros activos simultáneamente (búsqueda o dropdown "Todos los Estados")

### **Acciones del Sistema (observadas en Imagen 10):**

1. **A1:** Mostrar dropdown "Todas las Facultades" con flecha desplegable
2. **A2:** Desplegar lista de facultades disponibles al hacer clic
3. **A3:** Mostrar nombres de facultades en la lista (ej: "Facultad de Ingeniería de Sistemas", "Facultad de Ingeniería Civil", etc.)
4. **A4:** Actualizar el valor del dropdown con la facultad seleccionada
5. **A5:** Filtrar la tabla automáticamente sin recargar la página
6. **A6:** Mostrar únicamente las carreras que pertenecen a la facultad seleccionada
7. **A7:** Ocultar todas las carreras de otras facultades
8. **A8:** Mantener visible la estructura completa de la tabla: "Código", "Nombre", "Facultad", "Coordinador", "Acciones"
9. **A9:** Mantener visibles todos los datos de las carreras coincidentes
10. **A10:** Mostrar mensaje o tabla vacía cuando no hay carreras de la facultad seleccionada
11. **A11:** Actualizar controles de paginación según cantidad de resultados filtrados
12. **A12:** Aplicar filtro de facultad en combinación con otros filtros activos (búsqueda, estado)
13. **A13:** Permitir cambiar a otra facultad o volver a "Todas las Facultades"

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen carreras en el sistema
- **C2:** Se selecciona una facultad específica
- **C3:** Hay carreras de la facultad seleccionada
- **C4:** Hay otros filtros activos

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Carreras existen | C2: Facultad seleccionada | C3: Carreras de esa facultad | C4: Otros filtros | Acción |
|-------|---------------------|--------------------------|----------------------------|------------------|---------|
| R1 | N | N | N | N | A1: Mostrar dropdown sin datos |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber carreras sin carreras) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A10: Mostrar tabla vacía |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A8: Mostrar todas las carreras sin filtro |
| R10 | S | N | - | S | A8, A12: Mostrar carreras según otros filtros |
| R11 | S | S | N | N | A4, A5, A10: Mostrar mensaje "Sin carreras" |
| R12 | S | S | N | S | A4, A5, A10, A12: Sin resultados con múltiples filtros |
| R13 | S | S | S | N | A4-A9, A11: Filtrar y mostrar carreras |
| R14 | S | S | S | S | A4-A9, A11, A12: Filtrar combinando criterios |

---

## **Tabla de Decisión Minimizada**

| Regla | Carreras existen | Facultad seleccionada | Carreras de esa facultad | Otros filtros | Acción |
|-------|-----------------|----------------------|-------------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar dropdown pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todas las carreras sin filtro de facultad |
| **R3** | S | N | - | S | Mostrar carreras según otros filtros, sin filtro de facultad |
| **R4** | S | S | N | - | Mostrar mensaje "Sin carreras para la facultad" |
| **R5** | S | S | S | N | Filtrar por facultad solamente |
| **R6** | S | S | S | S | Filtrar por facultad Y combinar con otros filtros |

**Justificación de la minimización:**
- **R1:** Si no hay carreras, el filtro no tiene datos sobre los cuales operar (fusiona R1, R5)
- **R2:** Estado inicial sin filtro de facultad, sin otros filtros (R9)
- **R3:** Estado sin filtro de facultad pero con búsqueda/estado activos (R10)
- **R4:** Filtro aplicado pero sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: filtrar solo por facultad (R13)
- **R6:** Caso avanzado: filtrar por facultad en combinación con otros filtros (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de filtrado)
- 2 escenarios adicionales específicos:
  - Interacción con el dropdown (desplegar opciones)
  - Cambio dinámico entre diferentes facultades

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder y desplegar opciones del filtro de facultades**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** estoy en la pantalla "Gestión de Carreras",  
**cuando** ubico el dropdown "Todas las Facultades" en la sección de filtros superior,  
**entonces** se muestra el dropdown con el texto por defecto "Todas las Facultades" **Y** el dropdown está habilitado para interacción **Y** se muestra una flecha desplegable indicando que es un menú interactivo,  
**cuando** hago clic en el dropdown "Todas las Facultades",  
**entonces** se despliega una lista con las facultades disponibles en el sistema **Y** la lista incluye nombres completos de facultades registradas (ej: "Facultad de Ingeniería de Sistemas", "Facultad de Ingeniería Civil", "Facultad de Ciencias Administrativas", "Facultad de Geología y Petróleos") **Y** todas las opciones son claramente legibles **Y** puedo seleccionar cualquier facultad de la lista.

---

**Escenario 2 – Filtrar carreras por una facultad específica**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras asociadas a diferentes facultades **Y** el dropdown "Todas las Facultades" está en su estado por defecto,  
**cuando** hago clic en el dropdown "Todas las Facultades" **Y** selecciono una facultad específica de la lista (ej: "Facultad de Ingeniería de Sistemas"),  
**entonces** el dropdown se actualiza mostrando "Facultad de Ingeniería de Sistemas" como valor seleccionado **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las carreras que pertenecen a "Facultad de Ingeniería de Sistemas" **Y** basado en datos observados, se muestran carreras como "IS-ING - Ingeniería de Software" e "IS-RED - Redes y Telecomunicaciones" **Y** se ocultan todas las carreras de otras facultades como "ADM-NEG - Administración de Empresas", "IC-CIV - Ingeniería Civil", "GEO-PET - Geología y Petróleos" **Y** se mantienen visibles todas las columnas: "Código", "Nombre", "Facultad", "Coordinador", "Acciones" **Y** todos los datos de las carreras filtradas se conservan completos **Y** los iconos de editar (lápiz) y eliminar (papelera) permanecen disponibles **Y** los controles de paginación se actualizan según la cantidad de carreras de la facultad seleccionada.

---

**Escenario 3 – Mostrar mensaje cuando no hay carreras de la facultad seleccionada**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras registradas en el sistema,  
**cuando** selecciono una facultad específica del dropdown "Todas las Facultades" **Y** no existen carreras asociadas a esa facultad en la base de datos,  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No hay carreras registradas para esta facultad" o "Sin carreras para la facultad seleccionada" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el dropdown "Todas las Facultades" conserva el valor seleccionado **Y** los demás controles de filtrado permanecen disponibles para modificar los criterios **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 4 – Combinar filtro de facultad con búsqueda por palabra clave**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras de diversas facultades,  
**cuando** selecciono una facultad del dropdown "Todas las Facultades" (ej: "Facultad de Ingeniería de Sistemas") **Y** ingreso texto en el campo de búsqueda "Buscar carrera..." (ej: "Software"),  
**entonces** la tabla muestra únicamente las carreras que pertenecen a "Facultad de Ingeniería de Sistemas" Y cuyo código o nombre contiene "Software" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** basado en datos observados, se muestra "IS-ING - Ingeniería de Software" si cumple ambos criterios **Y** se excluyen carreras de la misma facultad que no contienen "Software" (como "IS-RED - Redes y Telecomunicaciones") **Y** se excluyen carreras que contienen "Software" pero pertenecen a otras facultades **Y** ambos controles (dropdown y búsqueda) reflejan los valores aplicados **Y** el filtrado es dinámico.

---

**Escenario 5 – Combinar filtro de facultad con filtro de estado**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras con diversos estados y facultades,  
**cuando** selecciono una facultad del dropdown "Todas las Facultades" (ej: "Facultad de Ingeniería Civil") **Y** selecciono un estado del dropdown "Todos los Estados" (ej: "Activo"),  
**entonces** la tabla muestra únicamente las carreras que pertenecen a "Facultad de Ingeniería Civil" Y tienen estado "Activo" **Y** se aplican ambos criterios simultáneamente **Y** se excluyen carreras activas de otras facultades **Y** se excluyen carreras de la facultad seleccionada con estado diferente (ej: "Inactivo") **Y** ambos dropdowns reflejan los valores seleccionados **Y** la tabla se actualiza sin recargar la página.

---

**Escenario 6 – Quitar filtro de facultad para visualizar todas las carreras**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** tengo una facultad específica seleccionada en el dropdown "Todas las Facultades" (ej: "Facultad de Ingeniería de Sistemas") **Y** la tabla muestra carreras filtradas por esa facultad,  
**cuando** hago clic en el dropdown "Todas las Facultades" **Y** selecciono nuevamente la opción "Todas las Facultades",  
**entonces** el dropdown se actualiza mostrando "Todas las Facultades" **Y** el filtro de facultad se elimina **Y** la tabla se actualiza automáticamente mostrando todas las carreras registradas sin filtro de facultad **Y** se muestran carreras de todas las facultades simultáneamente (ej: "IS-ING", "ADM-NEG", "IC-CIV", "GEO-PET", "IS-RED") **Y** se restablecen las filas originales **Y** se mantienen activos cualquier otro filtro que esté aplicado (búsqueda, estado) **Y** los controles de paginación se actualizan según el total de carreras sin filtrar por facultad.

---

**Escenario 7 – Cambiar dinámicamente entre diferentes facultades**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** tengo aplicado un filtro de facultad (ej: "Facultad de Ingeniería de Sistemas") **Y** la tabla muestra carreras de esa facultad,  
**cuando** cambio la selección del dropdown "Todas las Facultades" a otra facultad diferente (ej: "Facultad de Ciencias Administrativas"),  
**entonces** el dropdown se actualiza inmediatamente con "Facultad de Ciencias Administrativas" **Y** la tabla se actualiza automáticamente sin recargar la página **Y** se ocultan todas las carreras de "Facultad de Ingeniería de Sistemas" **Y** se muestran únicamente las carreras de "Facultad de Ciencias Administrativas" **Y** basado en datos observados, se muestra "ADM-NEG - Administración de Empresas" **Y** la transición entre filtros es fluida e inmediata **Y** no se requiere hacer clic en ningún botón adicional para aplicar el cambio **Y** se mantiene la consistencia visual de la tabla durante el cambio **Y** todas las carreras mostradas pertenecen a la nueva facultad seleccionada.

---

**Escenario 8 – Validar organización de visualización por facultad**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen múltiples carreras distribuidas en diferentes facultades,  
**cuando** aplico el filtro de facultad seleccionando una facultad específica,  
**entonces** la visualización se organiza mostrando exclusivamente carreras de la facultad seleccionada **Y** la oferta académica se presenta de manera organizada por unidad académica **Y** puedo visualizar claramente cuántas carreras ofrece cada facultad al filtrar **Y** la agrupación lógica por facultad facilita la revisión de la oferta académica institucional **Y** puedo alternar entre facultades para comparar la oferta de cada unidad **Y** la organización mejora la eficiencia en la revisión de carreras por áreas organizacionales **Y** la interfaz proporciona una vista clara y enfocada de la oferta académica según la facultad de interés.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Filtrar carreras por una facultad específica**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que la Autoridad quiere "filtrar carreras por facultad para organizar la visualización de la oferta académica". El Escenario 2 valida directamente esta funcionalidad core, demostrando que el sistema puede filtrar efectivamente carreras por facultad específica.

2. **Representa el "happy path" principal:** Es el caso de uso más frecuente y esencial:
   - Las autoridades necesitan ver carreras organizadas por facultad regularmente
   - Es el flujo natural de navegación por la estructura organizacional
   - Refleja cómo está estructurada académicamente la EPN (por facultades)
   - Es el método primario de organización de la oferta académica

3. **Mayor valor para organización de la visualización (objetivo de la HU):** Filtrar por facultad organiza porque:
   - Agrupa carreras por unidad académica organizacional
   - Permite enfoque en áreas específicas de la institución
   - Facilita la revisión estructurada de la oferta por dependencias
   - Reduce complejidad visual mostrando solo carreras relevantes de una facultad

4. **Valida comportamiento completo del filtro:** Verifica todos los aspectos críticos:
   - Interacción correcta con el dropdown "Todas las Facultades"
   - Actualización automática sin recarga de página
   - Visualización exclusiva de carreras de la facultad seleccionada
   - Ocultación de carreras de otras facultades
   - Preservación de estructura y funcionalidades de la tabla
   - Actualización de controles de paginación según resultados

5. **Impacto directo en gestión académica:** Filtrar por facultad permite:
   - Revisar oferta académica por unidad organizacional
   - Evaluar distribución de carreras por facultad
   - Identificar facultades con mayor/menor oferta
   - Planificar crecimiento académico por áreas
   - Gestionar coordinadores y recursos por facultad

6. **Fundamento para otros escenarios:** Los escenarios de combinación (4-5), eliminación (6), y cambio dinámico (7) son extensiones de esta funcionalidad base. Sin el filtrado por facultad funcionando, las demás capacidades carecen de fundamento.

7. **Refleja estructura organizacional real:** En la EPN:
   - Las facultades son la unidad organizacional fundamental
   - Las carreras están estructuradas bajo facultades
   - La toma de decisiones se da por facultades
   - Los recursos se asignan por facultades

8. **Mayor frecuencia de uso:** Las autoridades típicamente:
   - Revisan carreras facultad por facultad
   - Comparan oferta entre facultades
   - Gestionan por unidades académicas (facultades)
   - Necesitan vistas organizadas por dependencia

9. **Validación de datos relacionales críticos:** El escenario verifica:
   - Correcta asociación entre carreras y facultades en base de datos
   - Integridad referencial de las relaciones
   - Coherencia de la estructura organizacional
   - Datos consistentes entre tabla y filtros

10. **Precedencia institucional:** En gestión universitaria:
    - La estructura por facultades es estándar
    - La oferta académica se presenta por facultades
    - Los reportes institucionales se organizan por facultades
    - La acreditación se gestiona por facultades

Los demás escenarios son importantes para completitud (casos sin resultados, cambio dinámico) y características avanzadas (combinación de filtros), pero el Escenario 2 es el que garantiza que el sistema cumple su promesa fundamental: **permitir a la Autoridad filtrar carreras por facultad específica para organizar efectivamente la visualización de la oferta académica según la estructura organizacional de la EPN, que es el caso de uso principal y de mayor valor para la gestión académica institucional**.