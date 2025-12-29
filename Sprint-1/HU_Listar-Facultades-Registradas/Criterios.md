# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imágenes 5 y 9 del prototipo):**

1. **C1:** Existen facultades registradas en el sistema
2. **C2:** Se ingresa texto en el campo de búsqueda "Buscar por código o nombre..."
3. **C3:** Se aplica filtro en dropdown "Filtrar por Carreras"
4. **C4:** Los filtros/búsqueda aplicados tienen resultados coincidentes
5. **C5:** La cantidad de facultades requiere paginación (más de una página de resultados)

### **Acciones del Sistema (observadas en Imágenes 5 y 9):**

1. **A1:** Mostrar pantalla "Gestión de Facultades" con título visible
2. **A2:** Mostrar tabla con cinco columnas: "Código", "Nombre", "Carreras", "Decano", "Acciones"
3. **A3:** Mostrar todas las facultades registradas en filas de la tabla
4. **A4:** Mostrar código de facultad en la columna "Código" (ej: "FIEE", "FICM", "FAD")
5. **A5:** Mostrar nombre completo de la facultad en la columna "Nombre"
6. **A6:** Mostrar número de carreras asociadas en la columna "Carreras" (valor numérico)
7. **A7:** Mostrar nombre y título del decano en la columna "Decano" (ej: "Dr. Juan Pérez")
8. **A8:** Mostrar dos iconos en la columna "Acciones": icono de lápiz (editar) e icono de papelera (eliminar)
9. **A9:** Mostrar campo de búsqueda con placeholder "Buscar por código o nombre..."
10. **A10:** Mostrar dropdown "Filtrar por Carreras" con flecha desplegable
11. **A11:** Mostrar botón "+ Nueva Facultad" en la esquina superior derecha
12. **A12:** Filtrar tabla según texto de búsqueda ingresado
13. **A13:** Filtrar tabla según criterio del dropdown de carreras
14. **A14:** Mostrar mensaje o tabla vacía cuando no hay resultados
15. **A15:** Mostrar controles de paginación: "< Previous 1 2 3 Next >"
16. **A16:** Actualizar contenido de tabla según página seleccionada
17. **A17:** Mostrar mensaje de notificación de éxito "Completado" con texto "El registro se ha creado exitosamente" (Imagen 9)

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen facultades en el sistema
- **C2:** Se aplican filtros/búsqueda
- **C3:** Hay coincidencias con filtros/búsqueda
- **C4:** Requiere paginación (múltiples páginas)

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Facultades existen | C2: Filtros aplicados | C3: Hay coincidencias | C4: Requiere paginación | Acción |
|-------|----------------------|----------------------|---------------------|------------------------|---------|
| R1 | N | N | N | N | A1, A2, A9, A10, A11, A14: Mostrar interfaz sin datos |
| R2 | N | N | N | S | Imposible (no puede haber paginación sin datos) |
| R3 | N | N | S | N | Imposible (no puede haber coincidencias sin facultades) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A1, A2, A9, A10, A11, A14: Sin resultados |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1-A11: Mostrar todas las facultades sin paginación |
| R10 | S | N | S | S | A1-A11, A15: Mostrar todas las facultades con paginación |
| R11 | S | S | N | N | A1, A2, A9, A10, A11, A14: Sin resultados para filtros |
| R12 | S | S | N | S | Imposible (no puede paginar sin resultados) |
| R13 | S | S | S | N | A1-A13: Mostrar facultades filtradas sin paginación |
| R14 | S | S | S | S | A1-A13, A15, A16: Mostrar facultades filtradas con paginación |

---

## **Tabla de Decisión Minimizada**

| Regla | Facultades existen | Filtros/búsqueda aplicados | Hay coincidencias | Requiere paginación | Acción |
|-------|-------------------|---------------------------|-------------------|---------------------|---------|
| **R1** | N | - | - | - | Mostrar interfaz vacía o mensaje "No hay facultades" |
| **R2** | S | N | - | N | Mostrar lista completa sin paginación |
| **R3** | S | N | - | S | Mostrar lista completa con paginación |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para los criterios" |
| **R5** | S | S | S | N | Mostrar lista filtrada sin paginación |
| **R6** | S | S | S | S | Mostrar lista filtrada con paginación |

**Justificación de la minimización:**
- **R1:** Si no hay facultades, los filtros son irrelevantes (fusiona R1, R5)
- **R2:** Caso básico sin filtros y con pocos resultados que no requieren paginación (R9)
- **R3:** Caso básico sin filtros pero con suficientes resultados para paginar (R10)
- **R4:** Filtros aplicados sin resultados, independiente de paginación (fusiona R11, R12)
- **R5:** Filtros aplicados con resultados que caben en una página (R13)
- **R6:** Filtros aplicados con resultados que requieren múltiples páginas (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de listado y filtrado)
- 3 escenarios adicionales para validar funcionalidades específicas observadas en el prototipo:
  - Búsqueda por código o nombre
  - Filtrado por número de carreras
  - Navegación por paginación

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Visualizar lista completa de facultades registradas**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** existen facultades registradas en la base de datos,  
**cuando** accedo a la sección "Facultades" desde el menú lateral **O** navego directamente a "Gestión de Facultades",  
**entonces** se muestra la pantalla "Gestión de Facultades" con el título visible en la parte superior **Y** se presenta una tabla con cinco columnas: "Código", "Nombre", "Carreras", "Decano", "Acciones" **Y** se muestran todas las facultades registradas en filas de la tabla **Y** cada fila contiene el código de la facultad en la columna "Código" (ej: "FIEE", "FICM", "FAD", "FCyS", "FA", "FCI") **Y** cada fila contiene el nombre completo de la facultad en la columna "Nombre" (ej: "Facultad de Ingeniería Eléctrica y Electrónica", "Facultad de Ingeniería en Ciencias de la Tierra") **Y** cada fila muestra el número de carreras asociadas en la columna "Carreras" como valor numérico (ej: "5", "3", "4", "6", "2", "7") **Y** cada fila muestra el nombre completo del decano con su título en la columna "Decano" (ej: "Dr. Juan Pérez", "Ing. Ana García", "MSc. Carlos Vaca") **Y** cada fila contiene dos iconos en la columna "Acciones": icono de lápiz para editar e icono de papelera para eliminar **Y** se muestra el campo de búsqueda con placeholder "Buscar por código o nombre..." en la parte superior **Y** se muestra el dropdown "Filtrar por Carreras" con flecha desplegable **Y** se muestra el botón "+ Nueva Facultad" en la esquina superior derecha.

---

**Escenario 2 – Visualizar tabla vacía cuando no hay facultades registradas**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** no existen facultades registradas en la base de datos,  
**cuando** accedo a la sección "Gestión de Facultades",  
**entonces** se muestra la pantalla "Gestión de Facultades" con todos los elementos de UI (campo de búsqueda, dropdown de filtro, botón "+ Nueva Facultad") **Y** se presenta la tabla con las cinco columnas: "Código", "Nombre", "Carreras", "Decano", "Acciones" **Y** no se muestran filas de datos en la tabla **Y** se presenta un mensaje indicativo "No hay facultades registradas" o la tabla aparece vacía **Y** los controles de paginación no se muestran.

---

**Escenario 3 – Buscar facultades por código**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen múltiples facultades registradas,  
**cuando** ingreso un código de facultad en el campo de búsqueda "Buscar por código o nombre..." (ej: "FIEE"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestran únicamente las facultades cuyo código coincide con el texto ingresado **Y** se muestra la fila de la facultad "FIEE" con todos sus datos: "Facultad de Ingeniería Eléctrica y Electrónica", número de carreras, decano asignado **Y** se ocultan todas las facultades cuyos códigos no coinciden con el criterio de búsqueda **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** la búsqueda es case-insensitive (no distingue mayúsculas de minúsculas).

---

**Escenario 4 – Buscar facultades por nombre**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades registradas,  
**cuando** ingreso parte del nombre de una facultad en el campo de búsqueda (ej: "Administración"),  
**entonces** la tabla se filtra automáticamente **Y** se muestran únicamente las facultades cuyo nombre contiene el texto ingresado **Y** se muestra la fila de "FAD - Facultad de Administración" con sus datos completos **Y** se ocultan todas las facultades cuyos nombres no coinciden **Y** la búsqueda funciona con coincidencias parciales del nombre.

---

**Escenario 5 – Filtrar facultades por número de carreras**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades con diferentes cantidades de carreras asociadas,  
**cuando** hago clic en el dropdown "Filtrar por Carreras",  
**entonces** se despliega una lista con opciones de filtrado basadas en rangos o números específicos de carreras **Y** puedo seleccionar un criterio de la lista,  
**cuando** selecciono un criterio específico (ej: facultades con más de 5 carreras),  
**entonces** la tabla se actualiza automáticamente sin recargar la página **Y** se muestran únicamente las facultades que cumplen con el criterio seleccionado **Y** se ocultan todas las facultades que no cumplen con el criterio **Y** el dropdown muestra el criterio seleccionado.

---

**Escenario 6 – Mostrar mensaje cuando no hay resultados de búsqueda o filtrado**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades registradas en el sistema,  
**cuando** ingreso un término de búsqueda en el campo "Buscar por código o nombre..." **O** aplico un filtro en "Filtrar por Carreras" **Y** ninguna facultad coincide con los criterios aplicados,  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron resultados" o "Sin resultados para los criterios aplicados" **Y** se mantienen visibles los controles de búsqueda y filtrado con los valores aplicados **Y** puedo modificar o limpiar los filtros para obtener nuevos resultados **Y** los controles de paginación no se muestran.

---

**Escenario 7 – Navegar entre páginas de facultades**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen más facultades de las que se pueden mostrar en una página,  
**cuando** reviso los controles de paginación en la parte inferior,  
**entonces** se muestran los controles "< Previous", números de página (ej: "1 2 3"), y "Next >" **Y** la página actual está resaltada o marcada visualmente **Y** el botón "< Previous" está deshabilitado cuando estoy en la primera página,  
**cuando** hago clic en un número de página específico (ej: "2") **O** hago clic en "Next >",  
**entonces** la tabla se actualiza mostrando las facultades correspondientes a esa página **Y** el número de página seleccionado se resalta **Y** se mantienen aplicados los filtros y búsquedas activos **Y** la transición es fluida sin recargar toda la página.

---

**Escenario 8 – Combinar búsqueda y filtrado simultáneamente**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen múltiples facultades registradas,  
**cuando** ingreso texto en el campo de búsqueda "Buscar por código o nombre..." (ej: "Ingeniería") **Y** selecciono un criterio del dropdown "Filtrar por Carreras" (ej: más de 4 carreras),  
**entonces** la tabla muestra únicamente las facultades que cumplen ambas condiciones simultáneamente **Y** se presentan solo facultades cuyo nombre contiene "Ingeniería" Y tienen más de 4 carreras asociadas **Y** se excluyen todas las facultades que no cumplen ambos criterios **Y** ambos controles (búsqueda y filtro) reflejan los valores aplicados **Y** la tabla se actualiza sin recargar la página.

---

**Escenario 9 – Limpiar búsqueda y filtros para ver lista completa**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** tengo texto ingresado en el campo de búsqueda **Y** tengo un filtro aplicado en el dropdown "Filtrar por Carreras",  
**cuando** borro el texto del campo de búsqueda **Y** cambio el dropdown de vuelta a su opción por defecto (ej: "Filtrar por Carreras" o "Todas"),  
**entonces** la tabla se actualiza mostrando nuevamente todas las facultades registradas sin filtros **Y** se restablece la vista completa con paginación según corresponda **Y** todos los controles vuelven a su estado inicial **Y** la tabla presenta la misma información que al acceder inicialmente a "Gestión de Facultades".

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 1 – Visualizar lista completa de facultades registradas**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que la Autoridad quiere "listar las facultades para gestionar la estructura académica de la EPN". El Escenario 1 valida directamente este objetivo principal al verificar que efectivamente se puede visualizar la lista completa de facultades con toda su información organizacional relevante.

2. **Representa el "happy path" fundamental:** Es el caso de uso más básico y esencial. Sin esta funcionalidad operando correctamente, ninguna de las capacidades avanzadas (búsqueda, filtrado, paginación) tiene sentido o valor para la gestión académica.

3. **Valida la completitud de información estructural crítica:** Verifica que se muestren todos los datos esenciales para la gestión de la estructura académica:
   - **Código:** Identificador único de la facultad
   - **Nombre completo:** Denominación oficial de la unidad académica
   - **Número de carreras:** Indicador de magnitud y complejidad de la facultad
   - **Decano:** Autoridad responsable de la facultad
   - **Acciones disponibles:** Capacidad de editar/eliminar para gestión estructural

4. **Habilita la gestión de la estructura académica:** Solo con una lista completa y precisa de facultades con sus atributos organizacionales, la Autoridad puede:
   - Comprender la estructura completa de la institución
   - Identificar todas las unidades académicas existentes
   - Verificar la asignación de decanos a cada facultad
   - Evaluar la distribución de carreras por facultad
   - Tomar decisiones sobre reorganización académica
   - Gestionar cambios estructurales (crear, editar, eliminar facultades)

5. **Fundamento para todos los demás escenarios:** Los escenarios de búsqueda (3-4), filtrado (5), combinación (8), y paginación (7) son refinamientos o extensiones de esta funcionalidad base. Si el listado básico falla, todas las demás capacidades carecen de fundamento.

6. **Refleja fielmente el prototipo:** El escenario captura con precisión todos los elementos visuales y de datos observados en la Imagen 5, incluyendo la estructura de la tabla, los datos específicos de ejemplo (códigos como "FIEE", "FICM", nombres completos, números de carreras, nombres de decanos con títulos), y todos los controles de la interfaz.

7. **Impacto directo en la gobernanza académica:** La capacidad de listar facultades es crítica para:
   - **Planificación estratégica:** Visualizar la estructura completa para toma de decisiones
   - **Gestión administrativa:** Identificar unidades académicas y sus responsables
   - **Auditoría organizacional:** Verificar integridad de la estructura académica
   - **Asignación de recursos:** Entender la distribución de carreras por facultad
   - **Cumplimiento institucional:** Mantener registro actualizado de la organización de la EPN

8. **Base para gestión jerárquica:** Las facultades son el nivel organizacional superior que contiene las carreras, por lo que su correcta visualización es fundamental para gestionar toda la estructura académica en cascada.

Los demás escenarios son importantes para la eficiencia operativa (búsqueda, filtrado) y usabilidad (paginación), pero el Escenario 1 es el que garantiza que el sistema cumple su propósito esencial declarado en la HU: **permitir a la Autoridad visualizar todas las facultades registradas con su información completa para gestionar efectivamente la estructura académica de la Escuela Politécnica Nacional**.