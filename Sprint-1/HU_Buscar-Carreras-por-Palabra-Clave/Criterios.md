# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 10 del prototipo):**

1. **C1:** Existen carreras registradas en el sistema
2. **C2:** Se ingresa texto en el campo de búsqueda "Buscar carrera..."
3. **C3:** El texto ingresado coincide con algún código de carrera
4. **C4:** El texto ingresado coincide con algún nombre de carrera (completo o parcial)
5. **C5:** El texto ingresado coincide con alguna facultad asociada
6. **C6:** Hay otros filtros activos simultáneamente (dropdowns "Todas las Facultades" o "Todos los Estados")

### **Acciones del Sistema (observadas en Imagen 10):**

1. **A1:** Mostrar campo de búsqueda con placeholder "Buscar carrera..."
2. **A2:** Habilitar campo de búsqueda para entrada de texto
3. **A3:** Filtrar tabla automáticamente mientras se escribe (búsqueda en tiempo real)
4. **A4:** Mostrar únicamente carreras cuyo código coincide con el texto de búsqueda
5. **A5:** Mostrar únicamente carreras cuyo nombre contiene el texto de búsqueda
6. **A6:** Mostrar únicamente carreras cuya facultad contiene el texto de búsqueda
7. **A7:** Mostrar carreras que coinciden por código O nombre O facultad
8. **A8:** Ocultar carreras que no coinciden con el criterio de búsqueda
9. **A9:** Mantener visible la estructura completa de la tabla: "Código", "Nombre", "Facultad", "Coordinador", "Acciones"
10. **A10:** Mantener visibles todos los datos de las carreras coincidentes
11. **A11:** Realizar búsqueda case-insensitive (no distinguir mayúsculas/minúsculas)
12. **A12:** Mostrar mensaje o tabla vacía cuando no hay coincidencias
13. **A13:** Actualizar controles de paginación según resultados filtrados
14. **A14:** Aplicar búsqueda en combinación con otros filtros activos
15. **A15:** Permitir limpiar búsqueda para restaurar listado completo

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen carreras en el sistema
- **C2:** Se ingresa texto de búsqueda
- **C3:** Hay coincidencias (código, nombre o facultad)
- **C4:** Hay otros filtros activos

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Carreras existen | C2: Texto ingresado | C3: Hay coincidencias | C4: Otros filtros | Acción |
|-------|---------------------|--------------------|--------------------|------------------|---------|
| R1 | N | N | N | N | A1, A2: Mostrar interfaz vacía |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber coincidencias sin carreras) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A1, A2, A12: Sin resultados |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A2, A9: Mostrar todas las carreras |
| R10 | S | N | - | S | A9, A14: Mostrar según otros filtros |
| R11 | S | S | N | N | A1, A2, A12: Sin resultados para búsqueda |
| R12 | S | S | N | S | A1, A2, A12, A14: Sin resultados combinando filtros |
| R13 | S | S | S | N | A3-A13: Filtrar por palabra clave |
| R14 | S | S | S | S | A3-A14: Filtrar por palabra clave + otros filtros |

---

## **Tabla de Decisión Minimizada**

| Regla | Carreras existen | Texto ingresado | Hay coincidencias | Otros filtros | Acción |
|-------|-----------------|----------------|-------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar interfaz pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todas las carreras sin búsqueda |
| **R3** | S | N | - | S | Mostrar carreras según otros filtros |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para la búsqueda" |
| **R5** | S | S | S | N | Filtrar por palabra clave solamente |
| **R6** | S | S | S | S | Filtrar por palabra clave Y combinar con otros filtros |

**Justificación de la minimización:**
- **R1:** Si no hay carreras, la búsqueda no tiene datos (fusiona R1, R5)
- **R2:** Estado inicial sin búsqueda activa, sin otros filtros (R9)
- **R3:** Estado sin búsqueda pero con filtros de facultad/estado activos (R10)
- **R4:** Búsqueda sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: búsqueda por palabra clave únicamente (R13)
- **R6:** Caso avanzado: búsqueda combinada con filtros (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de búsqueda)
- 3 escenarios adicionales específicos:
  - Búsqueda en tiempo real (mientras se escribe)
  - Búsqueda por múltiples campos (código, nombre, facultad)
  - Limpiar búsqueda para restaurar vista completa

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Buscar carrera por código completo**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras registradas con diferentes códigos,  
**cuando** ingreso un código completo de carrera en el campo de búsqueda "Buscar carrera..." (ej: "IS-ING"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestra únicamente la carrera cuyo código coincide con "IS-ING" **Y** se presenta la fila completa con: "IS-ING" en columna Código, "Ingeniería de Software" en columna Nombre, "Facultad de Ingeniería de Sistemas" en columna Facultad, nombre del coordinador en columna Coordinador, iconos de acción en columna Acciones **Y** se ocultan todas las demás carreras cuyos códigos no coinciden **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** la búsqueda es case-insensitive (funciona con "is-ing", "IS-ING", "Is-Ing").

---

**Escenario 2 – Buscar carrera por código parcial**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen múltiples carreras,  
**cuando** ingreso parte de un código en el campo de búsqueda (ej: "IS"),  
**entonces** la tabla se filtra automáticamente **Y** se muestran todas las carreras cuyos códigos comienzan con "IS" **Y** basado en datos observados, se muestran carreras como: "IS-ING - Ingeniería de Software" e "IS-RED - Redes y Telecomunicaciones" **Y** se ocultan carreras como "ADM-NEG", "IC-CIV", "GEO-PET" que no contienen "IS" en su código **Y** la búsqueda funciona con coincidencias parciales desde el inicio del código.

---

**Escenario 3 – Buscar carrera por nombre completo**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras registradas,  
**cuando** ingreso el nombre completo de una carrera en el campo de búsqueda (ej: "Ingeniería de Software"),  
**entonces** la tabla se filtra automáticamente **Y** se muestra únicamente la carrera cuyo nombre coincide: "IS-ING - Ingeniería de Software" **Y** se presenta con todos sus datos: código, nombre completo, facultad asociada, coordinador, iconos de acción **Y** se ocultan todas las demás carreras **Y** la búsqueda es case-insensitive.

---

**Escenario 4 – Buscar carrera por palabra clave del nombre**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras con nombres que contienen palabras comunes,  
**cuando** ingreso una palabra clave en el campo de búsqueda (ej: "Ingeniería"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestran todas las carreras cuyo nombre contiene la palabra "Ingeniería" **Y** basado en datos observados, se muestran: "IS-ING - Ingeniería de Software", "IC-CIV - Ingeniería Civil" **Y** se ocultan carreras como "ADM-NEG - Administración de Empresas", "GEO-PET - Geología y Petróleos" que no contienen "Ingeniería" **Y** la búsqueda funciona con coincidencias parciales en cualquier posición del nombre.

---

**Escenario 5 – Buscar carrera por nombre de facultad**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras asociadas a diferentes facultades,  
**cuando** ingreso el nombre de una facultad en el campo de búsqueda (ej: "Sistemas"),  
**entonces** la tabla se filtra automáticamente **Y** se muestran todas las carreras cuya facultad asociada contiene "Sistemas" **Y** basado en datos observados, se muestran carreras como: "IS-ING - Ingeniería de Software" e "IS-RED - Redes y Telecomunicaciones" que pertenecen a "Facultad de Ingeniería de Sistemas" **Y** se ocultan carreras de otras facultades **Y** la búsqueda funciona con coincidencias parciales del nombre de la facultad.

---

**Escenario 6 – Mostrar mensaje cuando no hay resultados de búsqueda**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** existen carreras registradas en el sistema,  
**cuando** ingreso un término de búsqueda en el campo "Buscar carrera..." **Y** ninguna carrera tiene un código, nombre o facultad que coincida con el término ingresado (ej: "Medicina"),  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron resultados" o "Sin coincidencias para la búsqueda" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el campo de búsqueda conserva el texto ingresado **Y** puedo modificar o limpiar el texto de búsqueda para obtener nuevos resultados **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 7 – Combinar búsqueda con filtro de facultad**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** he seleccionado una facultad del dropdown "Todas las Facultades" (ej: "Facultad de Ingeniería de Sistemas"),  
**cuando** ingreso texto en el campo de búsqueda "Buscar carrera..." (ej: "Software"),  
**entonces** la tabla muestra únicamente las carreras que pertenecen a "Facultad de Ingeniería de Sistemas" Y cuyo código o nombre contiene "Software" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** se muestra la carrera "IS-ING - Ingeniería de Software" si cumple ambos criterios **Y** se excluyen carreras de la misma facultad cuyo nombre no contiene "Software" **Y** se excluyen carreras cuyo nombre contiene "Software" pero pertenecen a otras facultades **Y** ambos controles (búsqueda y dropdown) reflejan los valores aplicados **Y** el filtrado es dinámico mientras escribo.

---

**Escenario 8 – Limpiar búsqueda para restaurar vista completa**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** he ingresado texto en el campo de búsqueda "Buscar carrera..." **Y** la tabla muestra carreras filtradas por ese criterio,  
**cuando** borro completamente el texto del campo de búsqueda,  
**entonces** el campo de búsqueda vuelve a mostrar el placeholder "Buscar carrera..." **Y** el filtro de búsqueda se elimina automáticamente **Y** la tabla se actualiza mostrando todas las carreras registradas sin filtro de búsqueda **Y** se restablecen las filas originales con todas las carreras **Y** se mantienen activos otros filtros que estén aplicados (dropdowns de facultad o estado) **Y** los controles de paginación se actualizan según el total de carreras sin filtrar **Y** la restauración ocurre inmediatamente al borrar el último carácter.

---

**Escenario 9 – Búsqueda en tiempo real mientras se escribe**

**Dado que** estoy en la pantalla "Gestión de Carreras" **Y** el campo de búsqueda está vacío,  
**cuando** comienzo a escribir texto en el campo "Buscar carrera..." carácter por carácter (ej: escribo "I", luego "N", luego "G"),  
**entonces** la tabla se actualiza automáticamente con cada carácter ingresado **Y** después de escribir "I" se muestran todas las carreras con código, nombre o facultad que contiene "I" **Y** después de escribir "IN" se filtran mostrando solo carreras que contienen "IN" **Y** después de escribir "ING" se filtran aún más mostrando solo las que contienen "ING" **Y** el filtrado es progresivo y en tiempo real sin necesidad de presionar Enter o hacer clic en un botón de búsqueda **Y** la respuesta del sistema es inmediata (sin delay perceptible) **Y** no se recarga la página completa durante el filtrado **Y** se mantiene el foco en el campo de búsqueda durante todo el proceso **Y** la búsqueda ocurre en todos los campos relevantes (código, nombre, facultad) simultáneamente.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 4 – Buscar carrera por palabra clave del nombre**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece explícitamente que la Autoridad quiere "filtrar las carreras por una palabra clave para agilizar la gestión de carreras". El Escenario 4 valida directamente esta funcionalidad de búsqueda por palabra clave, que es el corazón literal de la historia de usuario.

2. **Representa el caso de uso más frecuente y natural:** Las autoridades académicas típicamente:
   - Buscan carreras por conceptos clave de sus nombres (ej: "Ingeniería", "Administración", "Civil")
   - Raramente memorizan códigos exactos de carreras (IS-ING, ADM-NEG, etc.)
   - Conocen las carreras por sus denominaciones descriptivas
   - Necesitan agrupar carreras conceptualmente por palabras comunes

3. **Mayor valor para agilizar la gestión (objetivo de la HU):** La búsqueda por palabra clave del nombre agiliza porque:
   - Permite encontrar rápidamente grupos de carreras relacionadas escribiendo una sola palabra
   - Es más intuitivo que recordar códigos institucionales
   - Facilita la exploración conceptual del catálogo de carreras
   - Reduce significativamente el tiempo de búsqueda vs. scrolling manual

4. **Validación de búsqueda flexible con coincidencias parciales:** Verifica capacidades esenciales:
   - Búsqueda en cualquier posición del nombre (no solo inicio)
   - Múltiples resultados relevantes con una palabra clave
   - Filtrado efectivo que agrupa carreras por área temática
   - Case-insensitive para facilidad de uso

5. **Impacto directo en gestión de oferta académica:** La búsqueda por palabra clave es crítica para:
   - Identificar rápidamente todas las ingenierías ofertadas
   - Agrupar carreras por áreas disciplinares
   - Revisar carreras relacionadas para planificación curricular
   - Facilitar decisiones sobre nuevas carreras en áreas existentes

6. **Diferenciación de otros escenarios de búsqueda:**
   - **Escenarios 1-2 (código):** Más específico pero menos intuitivo, uso limitado
   - **Escenario 3 (nombre completo):** Requiere más escritura, menos ágil
   - **Escenario 5 (facultad):** Útil pero filtra por organización, no por concepto académico
   - **Escenario 4 (palabra clave nombre):** Equilibrio perfecto entre especificidad, flexibilidad y agilidad

7. **Mayor frecuencia de uso en operaciones académicas:** Las autoridades frecuentemente necesitan:
   - Revisar todas las carreras de ingeniería para evaluaciones curriculares
   - Encontrar carreras técnicas vs. administrativas rápidamente
   - Agrupar carreras por disciplina para asignación de recursos
   - Comparar carreras de áreas similares

8. **Validación de búsqueda inteligente multi-resultado:** Demuestra que el sistema:
   - Examina el campo "Nombre" correctamente
   - Retorna múltiples resultados relevantes simultáneamente
   - Mantiene contexto completo de cada carrera en resultados
   - Facilita comparación visual de carreras relacionadas

9. **Fundamento para eficiencia en gestión académica:** Sin búsqueda efectiva por palabra clave:
   - Las autoridades perderían tiempo navegando listas completas
   - Se dificultaría agrupar carreras conceptualmente
   - Se reduciría la agilidad prometida en la HU
   - La gestión estratégica de oferta académica sería menos eficiente

10. **Refleja expectativas modernas de búsqueda:** Los usuarios administrativos esperan:
    - Buscar conceptos, no códigos técnicos
    - Encontrar grupos de elementos relacionados con palabras clave
    - Resultados inmediatos y relevantes
    - Flexibilidad en cómo expresan sus búsquedas

Los demás escenarios son importantes para completitud (búsqueda por código, facultad) y características técnicas (tiempo real, limpieza), pero el Escenario 4 es el que garantiza que el sistema cumple su promesa fundamental: **permitir a la Autoridad filtrar carreras por palabra clave del nombre de manera flexible, intuitiva y potente para agilizar efectivamente la gestión de carreras, que es el caso de uso principal, más frecuente y de mayor valor de esta funcionalidad de búsqueda**.