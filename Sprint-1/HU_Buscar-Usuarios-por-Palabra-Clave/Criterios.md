# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 14 del prototipo):**

1. **C1:** Existen usuarios registrados en el sistema
2. **C2:** Se ingresa texto en el campo de búsqueda "Buscar usuario..."
3. **C3:** El texto ingresado coincide con algún email de usuario
4. **C4:** El texto ingresado coincide con algún nombre de usuario
5. **C5:** El texto ingresado coincide con algún rol de usuario
6. **C6:** Hay otros filtros activos simultáneamente (dropdowns "Todos los Roles" o "Todos los Estados")

### **Acciones del Sistema (observadas en Imagen 14):**

1. **A1:** Mostrar campo de búsqueda con placeholder "Buscar usuario..."
2. **A2:** Habilitar campo de búsqueda para entrada de texto
3. **A3:** Filtrar tabla automáticamente mientras se escribe (búsqueda en tiempo real)
4. **A4:** Mostrar únicamente usuarios cuyo email coincide con el texto de búsqueda
5. **A5:** Mostrar únicamente usuarios cuyo nombre coincide con el texto de búsqueda
6. **A6:** Mostrar únicamente usuarios cuyo rol coincide con el texto de búsqueda
7. **A7:** Mostrar usuarios que coinciden por email O nombre O rol
8. **A8:** Ocultar usuarios que no coinciden con el criterio de búsqueda
9. **A9:** Mantener visible la estructura completa de la tabla: "Email", "Nombre", "Rol", "Estado", "Acciones"
10. **A10:** Mantener visibles las etiquetas de estado coloreadas (verde "Activo", rojo "Inactivo")
11. **A11:** Realizar búsqueda case-insensitive (no distinguir mayúsculas/minúsculas)
12. **A12:** Mostrar mensaje o tabla vacía cuando no hay coincidencias
13. **A13:** Actualizar controles de paginación según resultados filtrados
14. **A14:** Aplicar búsqueda en combinación con otros filtros activos
15. **A15:** Permitir limpiar búsqueda para restaurar listado completo

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 4 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Existen usuarios en el sistema
- **C2:** Se ingresa texto de búsqueda
- **C3:** Hay coincidencias (email, nombre o rol)
- **C4:** Hay otros filtros activos

Total combinaciones teóricas: 2^4 = 16 reglas

| Regla | C1: Usuarios existen | C2: Texto ingresado | C3: Hay coincidencias | C4: Otros filtros | Acción |
|-------|---------------------|--------------------|--------------------|------------------|---------|
| R1 | N | N | N | N | A1, A2: Mostrar interfaz vacía |
| R2 | N | N | N | S | Imposible (no hay datos base) |
| R3 | N | N | S | N | Imposible (no puede haber coincidencias sin usuarios) |
| R4 | N | N | S | S | Imposible |
| R5 | N | S | N | N | A1, A2, A12: Sin resultados |
| R6 | N | S | N | S | Imposible |
| R7 | N | S | S | N | Imposible |
| R8 | N | S | S | S | Imposible |
| R9 | S | N | - | N | A1, A2, A9: Mostrar todos los usuarios |
| R10 | S | N | - | S | A9, A14: Mostrar según otros filtros |
| R11 | S | S | N | N | A1, A2, A12: Sin resultados para búsqueda |
| R12 | S | S | N | S | A1, A2, A12, A14: Sin resultados combinando filtros |
| R13 | S | S | S | N | A3-A13: Filtrar por palabra clave |
| R14 | S | S | S | S | A3-A14: Filtrar por palabra clave + otros filtros |

---

## **Tabla de Decisión Minimizada**

| Regla | Usuarios existen | Texto ingresado | Hay coincidencias | Otros filtros | Acción |
|-------|-----------------|----------------|-------------------|---------------|---------|
| **R1** | N | - | - | - | Mostrar interfaz pero tabla vacía |
| **R2** | S | N | - | N | Mostrar todos los usuarios sin búsqueda |
| **R3** | S | N | - | S | Mostrar usuarios según otros filtros |
| **R4** | S | S | N | - | Mostrar mensaje "Sin resultados para la búsqueda" |
| **R5** | S | S | S | N | Filtrar por palabra clave solamente |
| **R6** | S | S | S | S | Filtrar por palabra clave Y combinar con otros filtros |

**Justificación de la minimización:**
- **R1:** Si no hay usuarios, la búsqueda no tiene datos (fusiona R1, R5)
- **R2:** Estado inicial sin búsqueda activa, sin otros filtros (R9)
- **R3:** Estado sin búsqueda pero con filtros de rol/estado activos (R10)
- **R4:** Búsqueda sin coincidencias, independiente de otros filtros (fusiona R11, R12)
- **R5:** Caso exitoso básico: búsqueda por palabra clave únicamente (R13)
- **R6:** Caso avanzado: búsqueda combinada con filtros de rol/estado (R14)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de búsqueda)
- 3 escenarios adicionales específicos:
  - Búsqueda en tiempo real (mientras se escribe)
  - Búsqueda por múltiples campos (email, nombre, rol)
  - Limpiar búsqueda para restaurar vista completa

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Buscar usuario por email completo**

**Dado que** estoy autenticado como Autoridad en el sistema **Y** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados con diferentes emails,  
**cuando** ingreso un email completo en el campo de búsqueda "Buscar usuario..." (ej: "juan.perez@epn.edu.ec"),  
**entonces** la tabla se filtra automáticamente mientras escribo **Y** se muestra únicamente el usuario cuyo email coincide con "juan.perez@epn.edu.ec" **Y** se presenta la fila completa con: email en columna Email, nombre completo en columna Nombre, rol(es) en columna Rol, etiqueta de estado coloreada en columna Estado, iconos de acción en columna Acciones **Y** se ocultan todos los demás usuarios cuyos emails no coinciden **Y** el campo de búsqueda mantiene el texto ingresado visible **Y** la búsqueda es case-insensitive (funciona con "JUAN.PEREZ@EPN.EDU.EC", "Juan.Perez@epn.edu.ec").

---

**Escenario 2 – Buscar usuario por email parcial**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen múltiples usuarios,  
**cuando** ingreso parte de un email en el campo de búsqueda (ej: "juan"),  
**entonces** la tabla se filtra automáticamente **Y** se muestran todos los usuarios cuyos emails contienen "juan" **Y** se incluyen usuarios como "juan.perez@epn.edu.ec", "juan.garcia@epn.edu.ec" si existen **Y** se ocultan usuarios cuyo email no contiene "juan" **Y** la búsqueda funciona con coincidencias parciales en cualquier posición del email.

---

**Escenario 3 – Buscar usuario por nombre**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados,  
**cuando** ingreso un nombre o apellido en el campo de búsqueda (ej: "Perez"),  
**entonces** la tabla se filtra automáticamente **Y** se muestran todos los usuarios cuyo nombre completo contiene "Perez" **Y** basado en datos observados, se incluyen usuarios como "Juan Perez" si existe **Y** se ocultan usuarios cuyos nombres no contienen "Perez" **Y** la búsqueda es case-insensitive **Y** funciona con coincidencias parciales del nombre o apellidos.

---

**Escenario 4 – Buscar usuario por rol**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios con diferentes roles asignados,  
**cuando** ingreso un rol en el campo de búsqueda (ej: "Coordinador"),  
**entonces** la tabla se filtra automáticamente **Y** se muestran todos los usuarios que tienen "Coordinador" en su rol **Y** se incluyen usuarios con rol único "Coordinador de Carrera" **Y** se incluyen usuarios con roles múltiples como "Coordinador de Carrera/Profesor" **Y** se ocultan usuarios que no tienen "Coordinador" en ninguno de sus roles **Y** la búsqueda funciona con coincidencias parciales del texto del rol.

---

**Escenario 5 – Mostrar mensaje cuando no hay resultados de búsqueda**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** existen usuarios registrados en el sistema,  
**cuando** ingreso un término de búsqueda en el campo "Buscar usuario..." **Y** ningún usuario tiene un email, nombre o rol que coincida con el término ingresado (ej: "NoExiste123"),  
**entonces** la tabla no muestra ninguna fila de datos **Y** se presenta un mensaje indicativo "No se encontraron resultados" o "Sin coincidencias para la búsqueda" **Y** se mantiene visible la estructura de la tabla con sus columnas **Y** el campo de búsqueda conserva el texto ingresado **Y** puedo modificar o limpiar el texto de búsqueda para obtener nuevos resultados **Y** los controles de paginación no se muestran o están deshabilitados.

---

**Escenario 6 – Combinar búsqueda con filtro de rol**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he seleccionado un rol del dropdown "Todos los Roles" (ej: "Profesor"),  
**cuando** ingreso texto en el campo de búsqueda "Buscar usuario..." (ej: "juan"),  
**entonces** la tabla muestra únicamente los usuarios que tienen rol "Profesor" Y cuyo email o nombre contiene "juan" **Y** se aplican ambos criterios de filtrado simultáneamente **Y** se excluyen usuarios con rol "Profesor" cuyo email/nombre no contiene "juan" **Y** se excluyen usuarios cuyo email/nombre contiene "juan" pero no tienen rol "Profesor" **Y** ambos controles (búsqueda y dropdown) reflejan los valores aplicados **Y** el filtrado es dinámico mientras escribo.

---

**Escenario 7 – Combinar búsqueda con filtro de estado**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he seleccionado un estado del dropdown "Todos los Estados" (ej: "Activo"),  
**cuando** ingreso texto en el campo de búsqueda "Buscar usuario..." (ej: "perez"),  
**entonces** la tabla muestra únicamente los usuarios con estado "Activo" (etiqueta verde) Y cuyo email o nombre contiene "perez" **Y** se aplican ambos criterios simultáneamente **Y** se excluyen usuarios activos cuyo email/nombre no contiene "perez" **Y** se excluyen usuarios cuyo email/nombre contiene "perez" pero tienen estado "Inactivo" **Y** solo se muestran usuarios con etiqueta verde "Activo" que cumplen el criterio de búsqueda.

---

**Escenario 8 – Limpiar búsqueda para restaurar vista completa**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he ingresado texto en el campo de búsqueda "Buscar usuario..." **Y** la tabla muestra usuarios filtrados por ese criterio,  
**cuando** borro completamente el texto del campo de búsqueda,  
**entonces** el campo de búsqueda vuelve a mostrar el placeholder "Buscar usuario..." **Y** el filtro de búsqueda se elimina automáticamente **Y** la tabla se actualiza mostrando todos los usuarios registrados sin filtro de búsqueda **Y** se restablecen las filas originales con todos los usuarios **Y** se mantienen activos otros filtros que estén aplicados (dropdowns de rol o estado) **Y** los controles de paginación se actualizan según el total de usuarios sin filtrar **Y** la restauración ocurre inmediatamente al borrar el último carácter.

---

**Escenario 9 – Búsqueda en tiempo real mientras se escribe**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** el campo de búsqueda está vacío,  
**cuando** comienzo a escribir texto en el campo "Buscar usuario..." carácter por carácter (ej: escribo "j", luego "u", luego "a", luego "n"),  
**entonces** la tabla se actualiza automáticamente con cada carácter ingresado **Y** después de escribir "j" se muestran todos los usuarios con email, nombre o rol que contiene "j" **Y** después de escribir "ju" se filtran mostrando solo usuarios que contienen "ju" **Y** después de escribir "jua" se filtran aún más mostrando solo los que contienen "jua" **Y** después de escribir "juan" se muestran solo los que contienen "juan" **Y** el filtrado es progresivo y en tiempo real sin necesidad de presionar Enter o hacer clic en un botón de búsqueda **Y** la respuesta del sistema es inmediata (sin delay perceptible) **Y** no se recarga la página completa durante el filtrado **Y** se mantiene el foco en el campo de búsqueda durante todo el proceso **Y** la búsqueda ocurre en todos los campos relevantes (email, nombre, rol) simultáneamente.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Buscar usuario por nombre**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que la Autoridad quiere "filtrar usuarios por palabra clave para agilizar la gestión de usuarios". Buscar por nombre es el caso de uso más intuitivo y frecuente de búsqueda por palabra clave en gestión de usuarios.

2. **Representa el caso de uso más natural y frecuente:** Las autoridades administrativas típicamente:
   - Conocen o recuerdan nombres de usuarios (profesores, coordinadores, personal)
   - Raramente memorizan emails completos institucionales
   - Buscan personas por "cómo los conocen" (por nombre)
   - Necesitan encontrar usuarios específicos por apellidos o nombres

3. **Mayor valor práctico para gestión de usuarios:** La búsqueda por nombre es crítica porque:
   - Permite encontrar rápidamente colegas y personal conocido
   - Facilita la gestión cuando solo se conoce el nombre de la persona
   - Es el método más directo para identificar usuarios en contextos administrativos
   - Refleja cómo las personas naturalmente piensan sobre usuarios (por nombre, no por email)

4. **Validación de búsqueda flexible con coincidencias parciales:** Verifica capacidades esenciales:
   - Búsqueda por nombre o apellido indistintamente
   - Coincidencias en cualquier posición del nombre completo
   - No requiere escribir el nombre completo
   - Case-insensitive para facilidad de uso

5. **Impacto directo en agilización de gestión (objetivo de la HU):** La búsqueda por nombre agiliza porque:
   - Es más rápido escribir "Perez" que recordar/escribir un email completo
   - Permite encontrar múltiples usuarios con apellidos comunes
   - No requiere conocimiento de estructura de emails institucionales
   - Es intuitivo para cualquier usuario administrativo

6. **Diferenciación de otros escenarios de búsqueda:**
   - **Escenarios 1-2 (email):** Más específico pero menos intuitivo, requiere recordar emails
   - **Escenario 4 (rol):** Útil pero filtra por categoría, no por persona específica
   - **Escenario 3 (nombre):** Equilibrio perfecto entre especificidad y usabilidad

7. **Mayor probabilidad de uso en operaciones diarias:** Las autoridades frecuentemente necesitan:
   - Buscar a un profesor específico por nombre para gestionar su cuenta
   - Encontrar a un coordinador por apellido para verificar permisos
   - Localizar usuarios por cómo los conocen en la institución
   - Gestionar cuentas de personal identificándolos por nombre

8. **Validación de búsqueda multi-campo inteligente:** Aunque busca por nombre, valida que el sistema:
   - Examina el campo "Nombre" correctamente
   - Maneja nombres compuestos y apellidos
   - Funciona con coincidencias parciales en cualquier parte
   - Mantiene todos los datos del usuario en los resultados

9. **Fundamento para eficiencia administrativa:** Sin búsqueda efectiva por nombre:
   - Las autoridades tendrían que recordar emails exactos
   - Se perdería tiempo navegando por listas completas
   - Se reduciría significativamente la agilidad prometida en la HU
   - La gestión de usuarios sería menos intuitiva

10. **Refleja expectativas de sistemas modernos:** Los usuarios administrativos esperan poder:
    - Buscar personas por nombre como en cualquier directorio
    - Encontrar usuarios escribiendo parte del nombre/apellido
    - Obtener resultados inmediatos y relevantes
    - Este escenario valida estas expectativas estándar

Los demás escenarios son importantes para completitud (búsqueda por email, rol) y características avanzadas (combinación de filtros, tiempo real), pero el Escenario 3 es el que garantiza que el sistema cumple su promesa fundamental: **permitir a la Autoridad buscar usuarios por la forma más natural e intuitiva (nombre) con flexibilidad y rapidez para agilizar efectivamente la gestión de usuarios, que es el caso de uso principal y más frecuente de esta funcionalidad**.