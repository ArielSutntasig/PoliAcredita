# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 19 del prototipo):**

1. **C1:** Usuario está autenticado en el sistema
2. **C2:** Usuario accede a la opción "Mi Perfil" desde el menú lateral
3. **C3:** Usuario tiene información personal registrada (nombre, email, facultad, teléfono, fecha)
4. **C4:** Usuario tiene roles asignados
5. **C5:** Usuario tiene un solo rol asignado
6. **C6:** Usuario tiene múltiples roles asignados
7. **C7:** Usuario tiene permisos asociados a sus roles
8. **C8:** Sección "Ver Permisos Detallados" está expandida
9. **C9:** Sección "Ver Permisos Detallados" está colapsada

### **Acciones del Sistema (observadas en Imagen 19):**

1. **A1:** Mostrar pantalla "Mi Perfil" con título principal
2. **A2:** Mostrar sección "Información Personal" con todos los campos poblados
3. **A3:** Mostrar "Nombre Completo: Juan Pérez García"
4. **A4:** Mostrar "Correo Institucional: juan.perez@epn.edu.ec"
5. **A5:** Mostrar "Facultad: Ingeniería de Sistemas"
6. **A6:** Mostrar "Teléfono: +593 987 654 321"
7. **A7:** Mostrar "Fecha de Registro: 2023-01-15"
8. **A8:** Mostrar sección "Rol y Permisos" en el centro
9. **A9:** Mostrar etiqueta "Rol Asignado:"
10. **A10:** Mostrar badge(s) de rol(es) con colores distintivos
11. **A11:** Mostrar sección expandible "Ver Permisos Detallados"
12. **A12:** Mostrar lista de permisos con iconos de candado cuando está expandida
13. **A13:** Ocultar lista de permisos cuando está colapsada
14. **A14:** Mostrar sección "Cambiar Contraseña" en el lado derecho
15. **A15:** Permitir interacción con botón "Actualizar Contraseña"
16. **A16:** Mostrar mensaje si algún campo de información está vacío

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 3 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Usuario autenticado
- **C2:** Tiene información personal completa
- **C3:** Tiene roles asignados

Total combinaciones teóricas: 2^3 = 8 reglas

| Regla | C1: Autenticado | C2: Info personal | C3: Roles asignados | Acción |
|-------|----------------|------------------|-------------------|---------|
| R1 | N | - | - | Redirigir a login (no aplicable) |
| R2 | S | N | N | A1-A2, A16: Perfil con campos vacíos |
| R3 | S | N | S | A1-A2, A8-A11, A16: Perfil parcial con roles |
| R4 | S | S | N | A1-A7, A14-A15: Perfil sin roles |
| R5 | S | S | S | A1-A15: Perfil completo (happy path) |

---

## **Tabla de Decisión Minimizada**

| Regla | Autenticado | Info personal completa | Roles asignados | Acción |
|-------|------------|----------------------|----------------|---------|
| **R1** | N | - | - | Redirigir a login (prerrequisito) |
| **R2** | S | N | - | Mostrar perfil con campos vacíos o incompletos |
| **R3** | S | S | N | Mostrar perfil completo sin roles asignados |
| **R4** | S | S | S | Mostrar perfil completo con roles y permisos |

**Justificación de la minimización:**
- **R1:** Usuario no autenticado no puede acceder (prerrequisito de seguridad)
- **R2:** Perfil con información incompleta, independiente de roles
- **R3:** Perfil completo pero sin roles (posible para usuarios nuevos)
- **R4:** Happy path: perfil completo con información y roles (como muestra la Imagen 19)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 8 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios principales)
- 4 escenarios adicionales para validar aspectos específicos:
  - Visualización de un solo rol vs múltiples roles
  - Expandir/colapsar permisos detallados
  - Navegación desde menú lateral
  - Formato y presentación visual de datos

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder a Mi Perfil desde el menú lateral**

**Dado que** estoy autenticado como Usuario en el sistema,  
**cuando** hago clic en la opción "Mi Perfil" ubicada en el menú lateral izquierdo,  
**entonces** se carga y muestra la pantalla "Mi Perfil" **Y** el título "Mi Perfil" aparece en la parte superior de la pantalla **Y** se presentan tres secciones principales organizadas horizontalmente: "Información Personal" (izquierda), "Rol y Permisos" (centro), y "Cambiar Contraseña" (derecha) **Y** todas las secciones son visibles simultáneamente sin necesidad de scroll horizontal **Y** la opción "Mi Perfil" en el menú lateral se resalta indicando que es la sección activa.

---

**Escenario 2 – Visualizar información personal completa en el perfil**

**Dado que** estoy autenticado como Usuario en el sistema **Y** tengo información personal completa registrada,  
**cuando** accedo a la pantalla "Mi Perfil",  
**entonces** se muestra la sección "Información Personal" en el lado izquierdo **Y** se presenta el campo "Nombre Completo:" seguido del valor registrado (ej: "Juan Pérez García") **Y** se presenta el campo "Correo Institucional:" seguido del email institucional (ej: "juan.perez@epn.edu.ec") **Y** se presenta el campo "Facultad:" seguida del nombre de la facultad asociada (ej: "Ingeniería de Sistemas") **Y** se presenta el campo "Teléfono:" seguido del número de contacto (ej: "+593 987 654 321") **Y** se presenta el campo "Fecha de Registro:" seguida de la fecha de creación de la cuenta (ej: "2023-01-15") **Y** todos los datos se muestran en formato de solo lectura (no editables directamente desde esta vista) **Y** toda la información es claramente legible con etiquetas y valores bien diferenciados.

---

**Escenario 3 – Visualizar roles asignados con múltiples roles**

**Dado que** estoy autenticado como Usuario en el sistema **Y** tengo múltiples roles asignados (ej: "Profesor" y "Decano"),  
**cuando** accedo a la pantalla "Mi Perfil",  
**entonces** se muestra la sección "Rol y Permisos" en el centro de la pantalla **Y** se presenta la etiqueta "Rol Asignado:" en la parte superior de esta sección **Y** se muestran badges/etiquetas de roles con colores distintivos **Y** específicamente se muestra badge "Profesor" con fondo azul oscuro y texto blanco **Y** se muestra badge "Decano" con fondo verde y texto blanco **Y** ambos badges están alineados horizontalmente uno al lado del otro **Y** cada badge tiene esquinas redondeadas **Y** puedo confirmar visualmente que tengo ambos roles asignados **Y** la información me permite verificar mis roles actuales en el sistema.

---

**Escenario 4 – Visualizar rol único asignado**

**Dado que** estoy autenticado como Usuario en el sistema **Y** tengo exactamente un rol asignado (ej: "Profesor"),  
**cuando** accedo a la pantalla "Mi Perfil",  
**entonces** se muestra la sección "Rol y Permisos" **Y** bajo la etiqueta "Rol Asignado:" se muestra un único badge con el rol "Profesor" (fondo azul oscuro, texto blanco) **Y** solo se presenta ese badge sin badges adicionales **Y** puedo confirmar claramente que tengo un solo rol activo **Y** la presentación visual es limpia y no sugiere roles múltiples.

---

**Escenario 5 – Visualizar permisos detallados en estado colapsado (inicial)**

**Dado que** estoy autenticado como Usuario en el sistema **Y** tengo roles con permisos asignados,  
**cuando** accedo por primera vez a la pantalla "Mi Perfil",  
**entonces** en la sección "Rol y Permisos" se muestra la opción "Ver Permisos Detallados" **Y** la sección está en estado colapsado (no expandida) por defecto **Y** se muestra una flecha apuntando hacia abajo (▼) indicando que se puede expandir **Y** no se muestran los permisos individuales detallados **Y** solo son visibles los badges de roles **Y** la interfaz es compacta y no muestra información excesiva inicialmente.

---

**Escenario 6 – Expandir y visualizar lista completa de permisos detallados**

**Dado que** estoy en la pantalla "Mi Perfil" **Y** la sección "Ver Permisos Detallados" está colapsada,  
**cuando** hago clic en la sección "Ver Permisos Detallados" o en la flecha desplegable,  
**entonces** la sección se expande mostrando la lista completa de permisos **Y** la flecha cambia de dirección apuntando hacia arriba (▲) **Y** se muestra una lista vertical de permisos específicos **Y** cada permiso se presenta con un icono de candado (🔒) a la izquierda del texto **Y** los permisos incluyen elementos como: "Visualizar Dashboard", "Gestionar Cursos", "Registrar Calificaciones", "Acceso a Mi Perfil", "Participar en proyectos de acreditación" **Y** cada permiso está en una línea separada para fácil lectura **Y** puedo confirmar visualmente todos los permisos que tengo asociados a mis roles **Y** puedo colapsar nuevamente la sección haciendo clic nuevamente.

---

**Escenario 7 – Visualizar perfil sin roles asignados**

**Dado que** estoy autenticado como Usuario en el sistema **Y** no tengo ningún rol asignado actualmente,  
**cuando** accedo a la pantalla "Mi Perfil",  
**entonces** se muestra toda la información personal correctamente en la sección "Información Personal" **Y** en la sección "Rol y Permisos" se muestra la etiqueta "Rol Asignado:" **Y** no se muestran badges de roles debajo de esta etiqueta **Y** se presenta un mensaje indicativo como "Sin roles asignados" o "No tienes roles actualmente" **Y** la sección "Ver Permisos Detallados" no se muestra o está deshabilitada **Y** opcionalmente se muestra orientación como "Contacta al Administrador para asignación de roles" **Y** puedo confirmar que mi información personal está registrada pero no tengo roles activos.

---

**Escenario 8 – Confirmar que la información es de solo lectura para visualización**

**Dado que** estoy en la pantalla "Mi Perfil" **Y** puedo ver toda mi información personal, roles y permisos,  
**cuando** intento interactuar con los campos de información personal (Nombre, Email, Facultad, Teléfono, Fecha),  
**entonces** los campos se presentan en formato de solo lectura (no son editables directamente) **Y** no aparecen campos de texto editables ni botones "Guardar" en la sección "Información Personal" **Y** puedo OBSERVAR y CONFIRMAR la información registrada como indica la historia de usuario **Y** para modificar esta información, necesitaría acceder a una funcionalidad de edición separada (no disponible en esta vista de visualización) **Y** los badges de roles son solo informativos y no editables desde esta pantalla **Y** la funcionalidad cumple su propósito de permitirme confirmar la información sin riesgo de modificaciones accidentales.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Visualizar información personal completa en el perfil**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Usuario quiere "observar mi perfil para confirmar la información registrada". El Escenario 2 valida directamente la capacidad de VER y CONFIRMAR la información personal completa, que es el objetivo principal.

2. **Representa el "happy path" del caso de uso principal:** Es el escenario que los usuarios ejecutarán con mayor frecuencia:
   - Acceder a su perfil para verificar datos de contacto
   - Confirmar que su información institucional es correcta
   - Validar datos antes de realizar trámites académicos
   - Verificar información para actualización o corrección

3. **Valida todos los campos críticos observados en el prototipo:** El Escenario 2 verifica la visualización de los 5 campos de información personal mostrados en la Imagen 19:
   - Nombre Completo (identificación del usuario)
   - Correo Institucional (contacto oficial)
   - Facultad (vinculación organizacional)
   - Teléfono (contacto alternativo)
   - Fecha de Registro (antigüedad en el sistema)

4. **Impacto en confianza del usuario:** Si la información personal no se muestra correctamente:
   - El usuario pierde confianza en la exactitud del sistema
   - No puede confirmar que sus datos están correctos
   - Puede proceder con información incorrecta en trámites
   - Se genera incertidumbre sobre la integridad de sus datos

5. **Fundamento para otros escenarios:** Los escenarios de roles (3-4) y permisos (5-6) son importantes, pero complementarios. Sin la capacidad de ver la información personal básica, la funcionalidad de perfil pierde su valor fundamental. Un usuario puede vivir sin ver permisos expandidos, pero DEBE poder ver su información personal.

6. **Mayor frecuencia de necesidad:** En operación:
   - Verificar información personal es más frecuente que revisar permisos
   - Los datos de contacto cambian y requieren confirmación
   - Los trámites académicos requieren validación de información personal
   - La información personal es relevante para todos los usuarios, independiente de roles

7. **Crítico para casos de uso reales:** Los usuarios acceden a Mi Perfil principalmente para:
   - Verificar email institucional antes de enviar comunicaciones
   - Confirmar teléfono de contacto actualizado
   - Validar facultad correcta antes de inscripciones
   - Revisar nombre completo registrado oficialmente
   - Estos son casos de uso cotidianos y prácticos

8. **Validación de integridad de datos:** Verifica que:
   - La información del usuario se recupera correctamente de la base de datos
   - Los datos se presentan en formato legible y estructurado
   - Todos los campos obligatorios tienen valores
   - La información coincide con lo registrado en el sistema

9. **Precedencia sobre funcionalidades avanzadas:** Antes de explorar roles y permisos complejos, el usuario necesita lo básico:
   - "¿Quién soy yo en el sistema?" (Nombre)
   - "¿Cómo me contactan?" (Email, Teléfono)
   - "¿A dónde pertenezco?" (Facultad)
   - Estas son preguntas fundamentales que el Escenario 2 responde

10. **Impacto en procesos institucionales:** La información personal es crítica para:
    - Comunicaciones oficiales (email institucional)
    - Contacto de emergencia (teléfono)
    - Reportes por facultad (vinculación organizacional)
    - Verificación de identidad (nombre completo)
    - Auditorías de antigüedad (fecha de registro)

Los demás escenarios son importantes para funcionalidad completa (roles múltiples, permisos detallados, casos sin roles), pero el Escenario 2 es el que garantiza que el sistema cumple su promesa fundamental: **permitir al Usuario observar su información personal completa para confirmar que los datos registrados en el sistema son correctos y están actualizados, que es el valor central y el caso de uso más frecuente de la visualización de perfil personal**.