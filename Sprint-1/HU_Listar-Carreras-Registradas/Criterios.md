# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 10 del prototipo):**

1. **C1:** Existen carreras registradas en el sistema
2. **C2:** Se ingresa texto en el campo de búsqueda "Buscar carrera..."
3. **C3:** Se aplica filtro en dropdown "Todas las Facultades"
4. **C4:** Se aplica filtro en dropdown "Todos los Estados"
5. **C5:** Los filtros/búsqueda aplicados tienen resultados coincidentes
6. **C6:** La cantidad de carreras requiere paginación (más de una página)

### **Acciones del Sistema (observadas en Imagen 10):**

1. **A1:** Mostrar pantalla "Gestión de Carreras" con título visible
2. **A2:** Mostrar tabla con cinco columnas: "Código", "Nombre", "Facultad", "Coordinador", "Acciones"
3. **A3:** Mostrar todas las carreras registradas en filas de la tabla
4. **A4:** Mostrar código de carrera en columna "Código" (ej: "IS-ING", "ADM-NEG", "IC-CIV")
5. **A5:** Mostrar nombre completo de la carrera en columna "Nombre"
6. **A6:** Mostrar facultad asociada en columna "Facultad"
7. **A7:** Mostrar nombre del coordinador en columna "Coordinador"
8. **A8:** Mostrar dos iconos en columna "Acciones": icono de lápiz (editar) e icono de papelera (eliminar)
9. **A9:** Mostrar campo de búsqueda con placeholder "Buscar carrera..."
10. **A10:** Mostrar dropdown "Todas las Facultades" con flecha desplegable
11. **A11:** Mostrar dropdown "Todos los Estados" con flecha desplegable
12. **A12:** Mostrar botón "+ Nueva Carrera" en esquina superior derecha
13. **A13:** Filtrar tabla según texto de búsqueda ingresado
14. **A14:** Filtrar tabla según facultad seleccionada
15. **A15:** Filtrar tabla según estado seleccionado
16. **A16:** Mostrar mensaje o tabla vacía cuando no hay resultados
17. **A17:** Mostrar controles de paginación: "< Previous 1 2 3 Next >"
18. **A18:** Actualizar contenido de tabla según página seleccionada

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen carreras en el sistema
- **C2:** Se aplican filtros/búsqueda
- **C3:** Hay coincidencias con filtros/búsqueda
- **C4:** Requiere paginación (múltiples páginas)

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Carreras existen | C2: Filtros aplicados | C3: Hay coincidencias | C4: Requiere paginación | Acción |
|-------|---------------------|----------------------|---------------------|------------------------|---------|
| R1 | N | N | N | N | A1, A2, A9-A12, A16: Mostrar interfaz sin datos |
| R2 | N | N | N | S | Imposible (no puede paginar sin datos) |
| R3 | N | N | S | N | Imposible (no puede haber coincidencias sin carreras) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A1, A2, A9-A12, A16: Sin resultados |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1-A12: Mostrar todas las carreras sin paginación |
| R10 | S | N | S | S | A1-A12, A17: Mostrar todas con paginación |
| R11 | S | S | N | N | A1, A2, A9-A12, A16: Sin resultados para filtros |
| R12 | S | S | N | S | Imposible |
| R13 | S | S | S | N | A1-A15: Mostrar carreras filtradas sin paginación |
| R14 | S | S | S | S | A1-A15, A17, A18: Mostrar filtradas con paginación |

---

## **Tabla de Decisión Minimizada**

| Regla | Carreras existen | Filtros/búsqueda aplicados | Hay coincidencias | Requiere paginación | Acción |
|-------|-----------------|---------------------------|-------------------|---------------------|---------|
| **R1** | N | - | - | - | Mostrar interfaz vacía o mensaje "No hay carreras" |
| **R2** | S | N | - | N | Mostrar lista completa sin paginación |
| **R3** | S | N | - | S | Mostrar lista completa con paginación |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para los criterios" |
| **R5** | S | S | S | N | Mostrar lista filtrada sin paginación |
| **R6** | S | S | S | S | Mostrar lista filtrada con paginación |

**Justificación de la minimización:**
- **R1:** Si no hay carreras, los filtros son irrelevantes (fusiona R1, R5)
- **R2:** Caso básico sin filtros y pocos resultados (R9)
- **R3:** Caso básico sin filtros con múltiples páginas (R10)
- **R4:** Filtros aplicados sin resultados (fusiona R11, R12)
- **R5:** Filtros aplicados con resultados en una página (R13)
- **R6:** Filtros aplicados con resultados en múltiples páginas (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de listado y filtrado)
- 3 escenarios adicionales para validar funcionalidades específicas:
  - Búsqueda por texto
  - Filtrado por facultad
  - Navegación por paginación

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Visualizar lista completa de carreras registradas**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** existen carreras registradas en la base de datos,  
**cuando** accedo a la sección "Carreras" desde el menú lateral **O** navego directamente a "Gestión de Carreras",  
**entonces** se muestra la pantalla "Gestión de Carreras" con el título visible en la parte superior **Y** se presenta una tabla con cinco columnas: "Código", "Nombre", "Facultad", "Coordinador", "Acciones" **Y** se muestran todas las carreras registradas en filas de la tabla **Y** cada fila contiene el código de la carrera en la columna "Código" (ej: "IS-ING", "ADM-NEG", "IC-CIV", "GEO-PET", "IS-RED") **Y** cada fila contiene el nombre completo de la carrera en la columna "Nombre" (ej: "Ingeniería de Software", "Administración de Empresas", "Ingeniería Civil", "Geología y Petróleos", "Redes y Telecomunicaciones") **Y** cada fila muestra el nombre de la facultad asociada en la columna "Facultad" (ej: "Facultad de Ingeniería de Sistemas", "Facultad de Ciencias Administrativas", "Facultad de Ingeniería Civil", "Facultad de Geología y Petróleos", "Facultad de Ingeniería de Sistemas") **Y** cada fila muestra el nombre del coordinador en la columna "Coordinador" (ej: "Dr. Juan Pérez", "Dra. Ana García", "Ing. Luis Martínez", "MSc. Sofía Rodríguez", "Dr. Juan Pérez", "Dr. Carlitos") **Y** cada fila contiene dos iconos en la columna "Acciones": icono de lápiz para editar e icono de papelera para eliminar **Y** se muestra el campo de búsqueda con placeholder "Buscar carrera..." en la parte superior **Y** se muestran dos dropdowns: "Todas las Facultades" y "Todos los Estados" **Y** se muestra el botón "+ Nueva Carrera" en la esquina superior derecha.

---

**Escenario 2 – Visualizar tabla vacía cuando no hay carreras registradas**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** no existen carreras registradas en la base de datos,  
**cuando** accedo a la sección "Gestión de Carreras",  
**entonces** se muestra la pantalla "Gestión de Carreras" con todos los elementos de UI (campo de búsqueda, dropdowns de filtro, botón "+ Nueva Carrera") **Y** se presenta la tabla con las cinco columnas: "Código", "Nombre", "Facultad", "Coordinador", "Acciones" **Y** no se muestran filas de datos en la tabla **Y** se presenta un mensaje indicativo "No hay carreras registradas" o la tabla aparece vacía **Y** los controles de paginación no se muestran.

---

**Escenario 3 – Buscar carreras por código o nombre**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen múltiples carreras registradas,  
**cuando** ingreso texto en el campo de búsqueda "Buscar carrera..." (ej: "Software" o "IS-ING"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestran únicamente las carreras cuyo código o nombre contiene el texto ingresado **Y** si busco "Software", se muestra la carrera "IS-ING - Ingeniería de Software" **Y** si busco "IS", se muestran carreras como "IS-ING" e "IS-RED" que comienzan con ese código **Y** se ocultan todas las carreras que no coinciden con el criterio de búsqueda **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** la búsqueda es case-insensitive (no distingue mayúsculas de minúsculas).

---

**Escenario 4 – Filtrar carreras por facultad**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras asociadas a diferentes facultades,  
**cuando** hago clic en el dropdown "Todas las Facultades",  
**entonces** se despliega una lista con las facultades disponibles en el sistema **Y** puedo seleccionar una facultad específica de la lista (ej: "Facultad de Ingeniería de Sistemas"),  
**cuando** selecciono una facultad específica,  
**entonces** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las carreras que pertenecen a la facultad seleccionada **Y** basado en datos observados, al seleccionar "Facultad de Ingeniería de Sistemas" se mostrarían carreras como "IS-ING - Ingeniería de Software" e "IS-RED - Redes y Telecomunicaciones" **Y** se ocultan todas las carreras de otras facultades **Y** el dropdown muestra la facultad seleccionada.

---

**Escenario 5 – Filtrar carreras por estado**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras con diferentes estados,  
**cuando** hago clic en el dropdown "Todos los Estados",  
**entonces** se despliega una lista con las opciones de estado disponibles (probablemente "Activo" e "Inactivo") **Y** puedo seleccionar un estado específico de la lista,  
**cuando** selecciono un estado (ej: "Activo"),  
**entonces** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las carreras que tienen el estado seleccionado **Y** se ocultan todas las carreras con estado diferente **Y** el dropdown muestra el estado seleccionado **Y** la respuesta visual es inmediata al cambio de filtro.

---

**Escenario 6 – Mostrar mensaje cuando no hay resultados de búsqueda o filtrado**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras registradas en el sistema,  
**cuando** ingreso un término de búsqueda **O** aplico filtros de facultad/estado **Y** ninguna carrera coincide con los criterios aplicados,  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron resultados" o "Sin resultados para los criterios aplicados" **Y** se mantienen visibles los controles de búsqueda y filtrado con los valores aplicados **Y** puedo modificar o limpiar los filtros para obtener nuevos resultados **Y** los controles de paginación no se muestran.

---

**Escenario 7 – Navegar entre páginas de carreras**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen más carreras de las que se pueden mostrar en una página,  
**cuando** reviso los controles de paginación en la parte inferior,  
**entonces** se muestran los controles "< Previous", números de página (ej: "1 2 3"), y "Next >" **Y** la página actual está resaltada o marcada visualmente **Y** el botón "< Previous" está deshabilitado cuando estoy en la primera página,  
**cuando** hago clic en un número de página específico (ej: "2") **O** hago clic en "Next >",  
**entonces** la tabla se actualiza mostrando las carreras correspondientes a esa página **Y** el número de página seleccionado se resalta **Y** se mantienen aplicados los filtros y búsquedas activos **Y** la transición es fluida sin recargar toda la página.

---

**Escenario 8 – Combinar múltiples filtros simultáneamente**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen múltiples carreras registradas,  
**cuando** ingreso texto en el campo de búsqueda "Buscar carrera..." (ej: "Ingeniería") **Y** selecciono una facultad del dropdown "Todas las Facultades" (ej: "Facultad de Ingeniería de Sistemas") **Y** selecciono un estado del dropdown "Todos los Estados" (ej: "Activo"),  
**entonces** la tabla muestra únicamente las carreras que cumplen las tres condiciones simultáneamente **Y** se presentan solo carreras cuyo nombre contiene "Ingeniería" Y pertenecen a "Facultad de Ingeniería de Sistemas" Y tienen estado "Activo" **Y** se excluyen todas las carreras que no cumplen los tres criterios **Y** todos los controles (búsqueda y dropdowns) reflejan los valores aplicados **Y** la tabla se actualiza sin recargar la página.

---

**Escenario 9 – Limpiar búsqueda y filtros para ver lista completa**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** tengo texto ingresado en el campo de búsqueda **Y** tengo filtros aplicados en los dropdowns de facultad y/o estado,  
**cuando** borro el texto del campo de búsqueda **Y** cambio los dropdowns de vuelta a sus opciones por defecto ("Todas las Facultades" y "Todos los Estados"),  
**entonces** la tabla se actualiza mostrando nuevamente todas las carreras registradas sin filtros **Y** se restablece la vista completa con paginación según corresponda **Y** todos los controles vuelven a su estado inicial **Y** la tabla presenta la misma información que al acceder inicialmente a "Gestión de Carreras".

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 1 – Visualizar lista completa de carreras registradas**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que la Autoridad quiere "listar las carreras para gestionar la oferta académica de la EPN". El Escenario 1 valida directamente este objetivo principal al verificar que efectivamente se puede visualizar la lista completa de carreras con toda su información relevante para la gestión académica.

2. **Representa el "happy path" fundamental:** Es el caso de uso más básico y esencial. Sin esta funcionalidad operando correctamente, ninguna de las capacidades avanzadas (búsqueda, filtrado, paginación) tiene sentido o valor para la gestión de la oferta académica.

3. **Valida la completitud de información académica crítica:** Verifica que se muestren todos los datos esenciales para gestionar la oferta académica:
   - **Código:** Identificador único de la carrera
   - **Nombre completo:** Denominación oficial de la carrera
   - **Facultad:** Unidad académica organizacional a la que pertenece
   - **Coordinador:** Responsable académico de la carrera
   - **Acciones disponibles:** Capacidad de editar/eliminar para gestión dinámica

4. **Habilita la gestión de la oferta académica:** Solo con una lista completa y precisa de carreras con sus atributos, la Autoridad puede:
   - Comprender la oferta académica completa de la EPN
   - Identificar todas las carreras activas en la institución
   - Verificar la distribución de carreras por facultades
   - Confirmar asignación de coordinadores responsables
   - Tomar decisiones sobre ampliación o ajuste de oferta académica
   - Gestionar cambios en la estructura de carreras

5. **Fundamento para todos los demás escenarios:** Los escenarios de búsqueda (3), filtrado (4-5), combinación (8), y paginación (7) son refinamientos de esta funcionalidad base. Si el listado básico falla, todas las demás capacidades carecen de fundamento.

6. **Refleja fielmente el prototipo:** El escenario captura con precisión todos los elementos visuales y de datos observados en la Imagen 10, incluyendo la estructura de la tabla, los datos específicos de ejemplo (códigos como "IS-ING", "ADM-NEG", nombres completos de carreras, facultades asociadas, coordinadores asignados), y todos los controles de la interfaz.

7. **Impacto directo en la gestión de oferta académica:** La capacidad de listar carreras es crítica para:
   - **Planificación académica:** Visualizar el portafolio completo de carreras
   - **Gestión curricular:** Identificar carreras para actualizaciones de planes de estudio
   - **Asignación de recursos:** Entender distribución de carreras para recursos docentes
   - **Publicación institucional:** Mantener actualizada la oferta visible para estudiantes
   - **Cumplimiento regulatorio:** Demostrar registro actualizado de carreras acreditadas

8. **Mayor frecuencia de uso:** En operaciones diarias, las autoridades necesitan ver el panorama completo de carreras con mayor frecuencia que realizar búsquedas o filtrados específicos.

9. **Base para decisiones estratégicas:** Las autoridades académicas necesitan:
   - Revisar sistemáticamente todas las carreras ofertadas
   - Comparar carreras entre facultades
   - Evaluar cobertura de áreas académicas
   - Identificar oportunidades de nuevas carreras
   - Todo esto requiere primero poder listar completamente las carreras existentes

10. **Validación de integridad de datos:** El escenario verifica que toda la información relacional está correctamente conectada:
    - Carreras vinculadas a facultades
    - Coordinadores asignados a carreras
    - Códigos únicos identificables
    - Estructura organizacional coherente

Los demás escenarios son importantes para usabilidad (búsqueda, filtrado) y eficiencia operativa (paginación), pero el Escenario 1 es el que garantiza que el sistema cumple su propósito esencial declarado en la HU: **permitir a la Autoridad visualizar todas las carreras registradas con su información completa para gestionar efectivamente la oferta académica de la Escuela Politécnica Nacional**.