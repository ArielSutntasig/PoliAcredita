# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 19 del prototipo):**

1. **C1:** El usuario está autenticado en el sistema
2. **C2:** El usuario accede a la sección "Mi Perfil"
3. **C3:** El usuario tiene roles asignados
4. **C4:** El usuario tiene un solo rol asignado
5. **C5:** El usuario tiene múltiples roles asignados (ej: "Profesor" y "Decano")
6. **C6:** La sección "Ver Permisos Detallados" está expandida
7. **C7:** La sección "Ver Permisos Detallados" está colapsada

### **Acciones del Sistema (observadas en Imagen 19):**

1. **A1:** Mostrar pantalla "Mi Perfil" con tres secciones principales
2. **A2:** Mostrar sección "Información Personal" con datos del usuario
3. **A3:** Mostrar sección "Rol y Permisos" en el centro
4. **A4:** Mostrar etiqueta "Rol Asignado:" 
5. **A5:** Mostrar roles en formato de badges/etiquetas de colores (azul oscuro para "Profesor", verde para "Decano")
6. **A6:** Mostrar sección expandible/colapsable "Ver Permisos Detallados" con flecha desplegable
7. **A7:** Mostrar lista de permisos con iconos de candado cuando está expandida
8. **A8:** Mostrar permisos específicos: "Visualizar Dashboard", "Gestionar Cursos", "Registrar Calificaciones", "Acceso a Mi Perfil", "Participar en proyectos de acreditación"
9. **A9:** Permitir expandir/colapsar la sección de permisos detallados
10. **A10:** Mantener visible la información de roles independiente del estado de expansión de permisos

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 3 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Usuario autenticado
- **C2:** Tiene roles asignados
- **C3:** Sección permisos expandida

Total combinaciones teóricas: 2^3 = 8 reglas

| Regla | C1: Autenticado | C2: Tiene roles | C3: Permisos expandidos | Acción |
|-------|----------------|----------------|------------------------|---------|
| R1 | N | N | N | No aplicable (debe estar autenticado) |
| R2 | N | N | S | Imposible |
| R3 | N | S | N | Imposible |
| R4 | N | S | S | Imposible |
| R5 | S | N | N | A1-A3: Mostrar perfil sin roles |
| R6 | S | N | S | Imposible (no puede expandir sin roles) |
| R7 | S | S | N | A1-A6: Mostrar roles, permisos colapsados |
| R8 | S | S | S | A1-A8: Mostrar roles y permisos expandidos |

---

## **Tabla de Decisión Minimizada**

| Regla | Autenticado | Tiene roles | Permisos expandidos | Acción |
|-------|------------|------------|-------------------|---------|
| **R1** | N | - | - | Redirigir a login (prerrequisito) |
| **R2** | S | N | - | Mostrar perfil sin roles asignados |
| **R3** | S | S | N | Mostrar roles como badges, permisos colapsados |
| **R4** | S | S | S | Mostrar roles como badges y lista detallada de permisos |

**Justificación de la minimización:**
- **R1:** Usuario no autenticado no puede acceder (prerrequisito de seguridad)
- **R2:** Usuario sin roles ve perfil completo pero sin badges de roles ni permisos
- **R3:** Usuario con roles ve badges de roles y puede expandir permisos (estado inicial colapsado)
- **R4:** Usuario con roles expande la sección y ve lista completa de permisos con iconos

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios principales)
- 4 escenarios adicionales para validar aspectos específicos:
  - Visualización de un solo rol
  - Visualización de múltiples roles con diferentes colores
  - Interacción expandir/colapsar permisos
  - Formato de presentación de permisos con iconos

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder a la pantalla Mi Perfil**

**Dado que** estoy autenticado como Usuario en el sistema,  
**cuando** accedo a la opción "Mi Perfil" desde el menú lateral,  
**entonces** se muestra la pantalla con el título "Mi Perfil" **Y** se presentan tres secciones principales: "Información Personal" (izquierda), "Rol y Permisos" (centro), y "Cambiar Contraseña" (derecha) **Y** en la sección "Información Personal" se muestra: Nombre Completo, Correo Institucional, Facultad, Teléfono, y Fecha de Registro **Y** en la sección "Rol y Permisos" se muestra la etiqueta "Rol Asignado:" **Y** se presenta una subsección expandible "Ver Permisos Detallados" con flecha desplegable **Y** todas las secciones están visibles en la misma vista sin necesidad de scroll horizontal.

---

**Escenario 2 – Visualizar un solo rol asignado**

**Dado que** estoy autenticado como Usuario en el sistema **Y** tengo exactamente un rol asignado (ej: "Profesor"),  
**cuando** accedo a la sección "Mi Perfil",  
**entonces** en la sección "Rol y Permisos" bajo la etiqueta "Rol Asignado:" se muestra un badge/etiqueta con el texto "Profesor" **Y** el badge tiene fondo de color azul oscuro con texto blanco **Y** el badge tiene esquinas redondeadas **Y** el rol se presenta de forma clara y destacada **Y** solo se muestra un badge correspondiente al único rol asignado.

---

**Escenario 3 – Visualizar múltiples roles asignados con diferentes colores**

**Dado que** estoy autenticado como Usuario en el sistema **Y** tengo múltiples roles asignados (ej: "Profesor" y "Decano"),  
**cuando** accedo a la sección "Mi Perfil",  
**entonces** en la sección "Rol y Permisos" bajo la etiqueta "Rol Asignado:" se muestran dos badges/etiquetas **Y** el primer badge muestra "Profesor" con fondo azul oscuro y texto blanco **Y** el segundo badge muestra "Decano" con fondo verde y texto blanco **Y** ambos badges están alineados horizontalmente uno al lado del otro **Y** cada badge tiene esquinas redondeadas **Y** los diferentes colores ayudan a distinguir visualmente cada rol **Y** puedo identificar claramente que tengo dos roles activos simultáneamente.

---

**Escenario 4 – Visualizar permisos detallados en estado colapsado (inicial)**

**Dado que** estoy autenticado como Usuario en el sistema **Y** tengo roles asignados con permisos,  
**cuando** accedo por primera vez a la sección "Mi Perfil",  
**entonces** en la sección "Rol y Permisos" se muestra la opción "Ver Permisos Detallados" **Y** la sección está en estado colapsado (no expandida) **Y** se muestra una flecha apuntando hacia abajo (▼) indicando que se puede expandir **Y** no se muestran los permisos detallados hasta que el usuario expanda la sección **Y** los badges de roles permanecen visibles independientemente del estado de expansión.

---

**Escenario 5 – Expandir y visualizar lista detallada de permisos**

**Dado que** estoy en la pantalla "Mi Perfil" **Y** tengo roles con permisos asignados **Y** la sección "Ver Permisos Detallados" está colapsada,  
**cuando** hago clic en la sección "Ver Permisos Detallados" o en la flecha desplegable,  
**entonces** la sección se expande mostrando una lista de permisos detallados **Y** la flecha cambia de dirección apuntando hacia arriba (▲) indicando que se puede colapsar **Y** se muestra una lista vertical de permisos, cada uno con un icono de candado (🔒) a la izquierda **Y** los permisos mostrados incluyen: "Visualizar Dashboard", "Gestionar Cursos", "Registrar Calificaciones", "Acceso a Mi Perfil", "Participar en proyectos de acreditación" **Y** cada permiso se presenta en una línea separada **Y** el texto de cada permiso es claro y descriptivo de la acción permitida **Y** puedo comprender mis capacidades específicas dentro del sistema.

---

**Escenario 6 – Colapsar lista de permisos detallados**

**Dado que** estoy en la pantalla "Mi Perfil" **Y** la sección "Ver Permisos Detallados" está expandida mostrando la lista de permisos,  
**cuando** hago clic nuevamente en la sección "Ver Permisos Detallados" o en la flecha hacia arriba,  
**entonces** la sección se colapsa ocultando la lista de permisos detallados **Y** la flecha cambia de dirección apuntando hacia abajo (▼) **Y** solo permanece visible el texto "Ver Permisos Detallados" **Y** los badges de roles permanecen visibles **Y** la transición de expandir/colapsar es fluida **Y** puedo alternar entre estados expandido y colapsado según necesite revisar los permisos.

---

**Escenario 7 – Comprender capacidades mediante permisos descriptivos**

**Dado que** estoy en la pantalla "Mi Perfil" **Y** he expandido la sección "Ver Permisos Detallados",  
**cuando** reviso la lista de permisos mostrados,  
**entonces** cada permiso tiene un nombre descriptivo que indica claramente la acción que puedo realizar **Y** por ejemplo, "Visualizar Dashboard" me indica que puedo ver el tablero principal **Y** "Gestionar Cursos" me indica que puedo administrar cursos académicos **Y** "Registrar Calificaciones" me indica que puedo ingresar notas de estudiantes **Y** "Acceso a Mi Perfil" me indica que puedo ver y gestionar mi información personal **Y** "Participar en proyectos de acreditación" me indica que puedo colaborar en procesos de acreditación **Y** el icono de candado (🔒) en cada permiso refuerza visualmente que son accesos autorizados **Y** puedo comprender mis capacidades y accesos dentro del sistema sin ambigüedad.

---

**Escenario 8 – Visualizar perfil sin roles asignados**

**Dado que** estoy autenticado como Usuario en el sistema **Y** no tengo ningún rol asignado actualmente,  
**cuando** accedo a la sección "Mi Perfil",  
**entonces** se muestra la pantalla completa con las tres secciones principales **Y** la sección "Información Personal" muestra todos mis datos correctamente **Y** en la sección "Rol y Permisos" se muestra la etiqueta "Rol Asignado:" **Y** no se muestran badges de roles debajo de esta etiqueta **Y** se presenta un mensaje indicativo como "Sin roles asignados" o "No tienes roles actualmente" **Y** la sección "Ver Permisos Detallados" no se muestra o está deshabilitada **Y** se proporciona orientación como "Contacta al Administrador para asignación de roles" **Y** el mensaje es claro y no genera confusión sobre mi estado en el sistema.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Visualizar múltiples roles asignados con diferentes colores**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Usuario quiere "observar mis roles y permisos para comprender mis capacidades y accesos dentro del sistema". El Escenario 3 valida directamente el caso mostrado en el prototipo: un usuario con múltiples roles ("Profesor" y "Decano"), que es el ejemplo real presentado en la Imagen 19.

2. **Representa el caso de uso real del prototipo:** El prototipo muestra específicamente:
   - Usuario: Juan Pérez García
   - Dos roles: "Profesor" (badge azul oscuro) y "Decano" (badge verde)
   - Este es el ejemplo diseñado como flujo principal del sistema

3. **Valida diferenciación visual crítica:** El uso de diferentes colores (azul para "Profesor", verde para "Decano") es una decisión de diseño intencional que:
   - Ayuda a distinguir visualmente cada rol
   - Mejora la escaneabilidad de la información
   - Facilita la identificación rápida de roles múltiples
   - Previene confusión cuando hay varios roles

4. **Mayor complejidad funcional y de negocio:** Valida aspectos críticos:
   - Correcta asignación de múltiples roles simultáneos
   - Presentación visual distintiva de cada rol
   - Diseño que previene confusión entre roles
   - Sistema que soporta roles no mutuamente excluyentes

5. **Refleja realidad operativa en contextos académicos:** Es común que:
   - Un profesor también sea decano de facultad
   - Una autoridad tenga roles académicos y administrativos
   - El personal senior acumule múltiples responsabilidades
   - La comprensión de roles múltiples sea esencial para operación efectiva

6. **Impacto directo en comprensión de capacidades ampliadas:** Con múltiples roles claramente diferenciados:
   - El usuario comprende que tiene capacidades extendidas
   - Puede identificar que actúa en múltiples contextos
   - Entiende que sus permisos son agregados de ambos roles
   - La claridad visual facilita auto-comprensión de su alcance

7. **Fundamento para permisos agregados:** Los permisos mostrados en "Ver Permisos Detallados" son la suma de capacidades de ambos roles:
   - "Visualizar Dashboard" - común a ambos roles
   - "Gestionar Cursos" - típico de Profesor
   - "Registrar Calificaciones" - típico de Profesor
   - "Participar en proyectos de acreditación" - típico de Decano
   - La visualización de roles múltiples explica por qué tiene permisos diversos

8. **Prevención de confusión crítica:** Si este escenario falla:
   - Los usuarios no comprenderán que tienen múltiples roles
   - Podrían pensar que solo tienen un rol y capacidades limitadas
   - La falta de diferenciación visual causaría confusión
   - No entenderían el origen de sus permisos ampliados

9. **Validación de diseño de UI específico del prototipo:** Verifica elementos exactos observados:
   - Badges con esquinas redondeadas
   - Badge azul oscuro para "Profesor"
   - Badge verde para "Decano"
   - Alineación horizontal de múltiples badges
   - Tipografía y espaciado específicos

10. **Impacto en gobernanza y transparencia:** Un sistema que muestra claramente múltiples roles con diferenciación visual:
    - Fomenta transparencia en asignación de responsabilidades
    - Permite al usuario auto-auditar sus roles
    - Facilita comprensión de por qué tiene ciertos accesos
    - Mejora la rendición de cuentas institucional

Los demás escenarios son importantes para completitud (sin roles, expandir/colapsar permisos) y funcionalidad (un solo rol, permisos descriptivos), pero el Escenario 3 es el que garantiza que el sistema cumple su promesa fundamental tal como está diseñado en el prototipo: **permitir al Usuario visualizar claramente múltiples roles con diferenciación visual mediante badges de colores para comprender efectivamente que tiene capacidades y accesos ampliados dentro del sistema, que es el caso de uso principal mostrado explícitamente en el diseño del prototipo (Juan Pérez García como Profesor y Decano)**.