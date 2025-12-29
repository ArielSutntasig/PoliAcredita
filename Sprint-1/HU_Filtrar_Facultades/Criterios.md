# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 5 del prototipo):**

1. **C1:** Existen facultades registradas en el sistema
2. **C2:** Se ingresa texto en el campo de búsqueda "Buscar por código o nombre..."
3. **C3:** El texto ingresado coincide con algún código de facultad
4. **C4:** El texto ingresado coincide con algún nombre de facultad (completo o parcial)
5. **C5:** Hay otros filtros activos simultáneamente (dropdown "Filtrar por Carreras")
6. **C6:** La búsqueda distingue entre mayúsculas y minúsculas

### **Acciones del Sistema (observadas en Imagen 5):**

1. **A1:** Mostrar campo de búsqueda con placeholder "Buscar por código o nombre..."
2. **A2:** Habilitar campo de búsqueda para entrada de texto
3. **A3:** Filtrar tabla automáticamente mientras se escribe (búsqueda en tiempo real)
4. **A4:** Mostrar únicamente facultades cuyo código coincide con el texto de búsqueda
5. **A5:** Mostrar únicamente facultades cuyo nombre contiene el texto de búsqueda
6. **A6:** Mostrar facultades que coinciden por código O por nombre
7. **A7:** Ocultar facultades que no coinciden con el criterio de búsqueda
8. **A8:** Mantener visible la estructura completa de la tabla: "Código", "Nombre", "Carreras", "Decano", "Acciones"
9. **A9:** Mantener visibles todos los datos de las facultades coincidentes
10. **A10:** Realizar búsqueda case-insensitive (no distinguir mayúsculas/minúsculas)
11. **A11:** Mostrar mensaje o tabla vacía cuando no hay coincidencias
12. **A12:** Actualizar controles de paginación según resultados filtrados
13. **A13:** Aplicar búsqueda en combinación con otros filtros activos
14. **A14:** Permitir limpiar búsqueda para restaurar listado completo

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen facultades en el sistema
- **C2:** Se ingresa texto de búsqueda
- **C3:** Hay coincidencias (código o nombre)
- **C4:** Hay otros filtros activos

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Facultades existen | C2: Texto ingresado | C3: Hay coincidencias | C4: Otros filtros | Acción |
|-------|----------------------|--------------------|--------------------|------------------|---------|
| R1 | N | N | N | N | A1, A2: Mostrar interfaz vacía |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber coincidencias sin facultades) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A1, A2, A11: Sin resultados |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A2, A8: Mostrar todas las facultades |
| R10 | S | N | - | S | A8, A13: Mostrar según otros filtros |
| R11 | S | S | N | N | A1, A2, A11: Sin resultados para búsqueda |
| R12 | S | S | N | S | A1, A2, A11, A13: Sin resultados combinando filtros |
| R13 | S | S | S | N | A3-A10, A12: Filtrar por palabra clave |
| R14 | S | S | S | S | A3-A10, A12, A13: Filtrar por palabra clave + otros filtros |

---

## **Tabla de Decisión Minimizada**

| Regla | Facultades existen | Texto ingresado | Hay coincidencias | Otros filtros | Acción |
|-------|-------------------|----------------|-------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar interfaz pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todas las facultades sin búsqueda |
| **R3** | S | N | - | S | Mostrar facultades según otros filtros |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para la búsqueda" |
| **R5** | S | S | S | N | Filtrar por palabra clave solamente |
| **R6** | S | S | S | S | Filtrar por palabra clave Y combinar con otros filtros |

**Justificación de la minimización:**
- **R1:** Si no hay facultades, la búsqueda no tiene datos (fusiona R1, R5)
- **R2:** Estado inicial sin búsqueda activa, sin otros filtros (R9)
- **R3:** Estado sin búsqueda pero con filtro de carreras activo (R10)
- **R4:** Búsqueda sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: búsqueda por palabra clave únicamente (R13)
- **R6:** Caso avanzado: búsqueda combinada con filtro de carreras (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de búsqueda)
- 2 escenarios adicionales específicos:
  - Búsqueda en tiempo real (mientras se escribe)
  - Limpiar búsqueda para restaurar vista completa

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Buscar facultad por código exacto**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades registradas con diferentes códigos,  
**cuando** ingreso un código de facultad en el campo de búsqueda "Buscar por código o nombre..." (ej: "FIEE"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestra únicamente la facultad cuyo código coincide exactamente con "FIEE" **Y** se presenta la fila con: "FIEE" en columna Código, "Facultad de Ingeniería Eléctrica y Electrónica" en columna Nombre, el número de carreras asociadas, el nombre del decano, y los iconos de acción **Y** se ocultan todas las demás facultades cuyos códigos no coinciden **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** la búsqueda es case-insensitive (funciona con "fiee", "FIEE", "Fiee").

---

**Escenario 2 – Buscar facultad por código parcial**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen múltiples facultades,  
**cuando** ingreso parte de un código en el campo de búsqueda (ej: "FI"),  
**entonces** la tabla se filtra automáticamente **Y** se muestran todas las facultades cuyos códigos comienzan con "FI" **Y** basado en datos observados, se muestran facultades como: "FIEE - Facultad de Ingeniería Eléctrica y Electrónica", "FICM - Facultad de Ingeniería en Ciencias de la Tierra" **Y** se ocultan facultades como "FAD", "FCyS", "FA" que no contienen "FI" en su código **Y** la búsqueda funciona con coincidencias parciales desde el inicio del código.

---

**Escenario 3 – Buscar facultad por nombre completo**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades registradas,  
**cuando** ingreso el nombre completo de una facultad en el campo de búsqueda (ej: "Facultad de Administración"),  
**entonces** la tabla se filtra automáticamente **Y** se muestra únicamente la facultad cuyo nombre coincide: "FAD - Facultad de Administración" **Y** se presenta con todos sus datos: código "FAD", cantidad de carreras (4), decano ("MSc. Carlos Vaca"), iconos de acción **Y** se ocultan todas las demás facultades **Y** la búsqueda es case-insensitive.

---

**Escenario 4 – Buscar facultad por palabra clave del nombre**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades con nombres que contienen palabras comunes,  
**cuando** ingreso una palabra clave en el campo de búsqueda (ej: "Ingeniería"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestran todas las facultades cuyo nombre contiene la palabra "Ingeniería" **Y** basado en datos observados, se muestran: "FIEE - Facultad de Ingeniería Eléctrica y Electrónica", "FICM - Facultad de Ingeniería en Ciencias de la Tierra" **Y** se ocultan facultades como "FAD - Facultad de Administración", "FA - Facultad de Artes" que no contienen "Ingeniería" **Y** la búsqueda funciona con coincidencias parciales en cualquier posición del nombre **Y** no requiere coincidencia desde el inicio del nombre.

---

**Escenario 5 – Mostrar mensaje cuando no hay resultados de búsqueda**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** existen facultades registradas en el sistema,  
**cuando** ingreso un término de búsqueda en el campo "Buscar por código o nombre..." **Y** ninguna facultad tiene un código o nombre que coincida con el término ingresado (ej: "Arquitectura"),  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron resultados" o "Sin coincidencias para la búsqueda" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el campo de búsqueda conserva el texto ingresado **Y** puedo modificar o limpiar el texto de búsqueda para obtener nuevos resultados **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 6 – Combinar búsqueda con filtro de carreras**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** he seleccionado un criterio del dropdown "Filtrar por Carreras" (ej: "4-6 carreras"),  
**cuando** ingreso texto en el campo de búsqueda "Buscar por código o nombre..." (ej: "Ingeniería"),  
**entonces** la tabla muestra únicamente las facultades que tienen entre 4 y 6 carreras Y cuyo código o nombre contiene "Ingeniería" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** se excluyen las facultades que cumplen solo uno de los dos criterios **Y** basado en datos observados, se muestra "FIEE - Facultad de Ingeniería Eléctrica y Electrónica" con 5 carreras **Y** se ocultan facultades con "Ingeniería" pero con diferente cantidad de carreras **Y** ambos controles (búsqueda y dropdown) reflejan los valores aplicados **Y** el filtrado es dinámico mientras escribo.

---

**Escenario 7 – Limpiar búsqueda para restaurar vista completa**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** he ingresado texto en el campo de búsqueda "Buscar por código o nombre..." **Y** la tabla muestra facultades filtradas por ese criterio,  
**cuando** borro completamente el texto del campo de búsqueda,  
**entonces** el campo de búsqueda vuelve a mostrar el placeholder "Buscar por código o nombre..." **Y** el filtro de búsqueda se elimina automáticamente **Y** la tabla se actualiza mostrando todas las facultades registradas sin filtro de búsqueda **Y** se restablecen las filas originales con todas las facultades **Y** se mantienen activos otros filtros que estén aplicados (dropdown "Filtrar por Carreras") **Y** los controles de paginación se actualizan según el total de facultades sin filtrar **Y** la restauración ocurre inmediatamente al borrar el último carácter.

---

**Escenario 8 – Búsqueda en tiempo real mientras se escribe**

**Dado que** estoy en la pantalla "Gestión de Facultades" **Y** el campo de búsqueda está vacío,  
**cuando** comienzo a escribir texto en el campo "Buscar por código o nombre..." carácter por carácter (ej: escribo "F", luego "I", luego "E"),  
**entonces** la tabla se actualiza automáticamente con cada carácter ingresado **Y** después de escribir "F" se muestran todas las facultades con código o nombre que contiene "F" **Y** después de escribir "FI" se filtran mostrando solo facultades que contienen "FI" **Y** después de escribir "FIE" se filtran aún más mostrando solo las que contienen "FIE" **Y** el filtrado es progresivo y en tiempo real sin necesidad de presionar Enter o hacer clic en un botón de búsqueda **Y** la respuesta del sistema es inmediata (sin delay perceptible) **Y** no se recarga la página completa durante el filtrado **Y** se mantiene el foco en el campo de búsqueda durante todo el proceso.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 4 – Buscar facultad por palabra clave del nombre**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece explícitamente que la Autoridad quiere "filtrar facultades por palabra clave para agilizar la gestión de facultades". El Escenario 4 valida directamente esta funcionalidad de búsqueda por palabra clave, que es el corazón de la historia.

2. **Representa el caso de uso más frecuente en la práctica:** Las autoridades académicas raramente memorizan códigos de facultades (FIEE, FICM, etc.) pero sí conocen conceptos clave de los nombres:
   - Buscar por "Ingeniería" para encontrar todas las facultades de ingeniería
   - Buscar por "Ciencias" para facultades científicas
   - Buscar por palabras descriptivas del área académica

3. **Mayor flexibilidad y valor para el usuario:** A diferencia de:
   - **Escenario 1-2 (código):** Requiere conocimiento exacto del código, menos intuitivo
   - **Escenario 3 (nombre completo):** Requiere escribir el nombre completo, más tedioso
   - **Escenario 4 (palabra clave):** Permite búsqueda rápida y flexible con términos parciales

4. **Valida búsqueda inteligente con coincidencias parciales:** Verifica capacidades críticas:
   - Búsqueda en cualquier posición del nombre (no solo inicio)
   - Múltiples resultados relevantes con una sola palabra clave
   - Filtrado efectivo que reduce significativamente el conjunto de datos
   - Búsqueda case-insensitive para facilidad de uso

5. **Impacto directo en la agilización de gestión (objetivo de la HU):** La búsqueda por palabra clave es lo que realmente agiliza la gestión porque:
   - Reduce tiempo de búsqueda (escribir "Ingeniería" vs. nombre completo)
   - No requiere memorizar códigos específicos
   - Permite exploración conceptual (ver todas las facultades de un área)
   - Facilita identificación rápida de grupos relacionados

6. **Mayor cobertura de casos reales:** Con datos observados en el prototipo:
   - "Ingeniería" encuentra 2 facultades (FIEE, FICM)
   - "Ciencias" podría encontrar FCyS, FCI
   - Demuestra utilidad con resultados múltiples pero manejables

7. **Fundamento para eficiencia operativa:** Las autoridades en operación diaria necesitan:
   - Agrupar facultades conceptualmente
   - Encontrar rápidamente áreas académicas relacionadas
   - Comparar facultades de similar naturaleza
   - Tomar decisiones sobre áreas académicas específicas

8. **Diferenciación de escenarios complementarios:**
   - **Escenarios 1-3:** Validan casos más específicos (código/nombre exacto)
   - **Escenario 5:** Valida caso de error (sin resultados)
   - **Escenarios 6-8:** Validan características adicionales (combinación, limpieza, tiempo real)
   - **Escenario 4:** Valida el caso de uso principal y más potente

9. **Refleja comportamiento esperado de búsqueda moderna:** Los usuarios actuales esperan que las búsquedas funcionen como Google, con:
   - Coincidencias parciales inteligentes
   - Múltiples resultados relevantes
   - No requerir sintaxis exacta
   - Este escenario valida estas expectativas modernas

10. **Impacto en adopción del sistema:** Si la búsqueda por palabra clave no funciona bien:
   - Los usuarios recurrirán a métodos manuales (scrolling)
   - Se perderá el valor de "agilizar la gestión"
   - La funcionalidad no cumplirá su promesa fundamental
   - La satisfacción del usuario será baja

Los demás escenarios son importantes para robustez (búsqueda por código, nombre completo, sin resultados) y usabilidad (tiempo real, limpieza), pero el Escenario 4 es el que garantiza que el sistema cumple su promesa esencial declarada en la HU: **permitir a la Autoridad filtrar facultades por palabra clave de manera flexible e intuitiva para agilizar efectivamente la gestión de facultades, que es precisamente el valor central y el caso de uso más frecuente de esta funcionalidad**.