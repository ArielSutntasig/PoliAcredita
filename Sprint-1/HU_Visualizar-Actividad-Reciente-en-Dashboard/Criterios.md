# **NOTA IMPORTANTE**

Revisando las imágenes analizadas previamente en nuestra conversación (Gestión de Facultades, Gestión de Carreras, Gestión de Usuarios, Gestión de Roles, y Mi Perfil), **no he identificado una imagen específica que muestre un Dashboard con sección de "Actividad Reciente" o registro de acciones del sistema**.

Procederé con el análisis basándome en:
1. La Historia de Usuario proporcionada
2. Mejores prácticas para dashboards administrativos con logs de actividad
3. El patrón de diseño y navegación observado en las pantallas previas del sistema
4. Elementos estándar en registros de actividad (audit logs)

Si existe una imagen específica de Dashboard que no he visto, por favor compártela para un análisis más preciso.

---

# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + inferencias de patrón de UI):**

1. **C1:** Administrador está autenticado en el sistema
2. **C2:** Administrador accede a la opción "Dashboard" desde el menú lateral
3. **C3:** Existen acciones registradas en el sistema (log de actividad)
4. **C4:** Hay actividad reciente (últimas 24 horas, 7 días, etc.)
5. **C5:** El registro de actividad contiene múltiples tipos de acciones (crear, editar, eliminar)
6. **C6:** Hay actividad de múltiples usuarios
7. **C7:** Se aplica filtro por tipo de acción
8. **C8:** Se aplica filtro por módulo (Facultades, Carreras, Usuarios, Roles)
9. **C9:** Se aplica filtro por rango de fechas

### **Acciones del Sistema (inferidas según mejores prácticas):**

1. **A1:** Mostrar pantalla "Dashboard" con título principal
2. **A2:** Mostrar sección "Actividad Reciente" o "Últimas Acciones"
3. **A3:** Presentar lista/tabla cronológica de acciones (más reciente primero)
4. **A4:** Mostrar para cada acción: timestamp, usuario, tipo de acción, módulo/entidad afectada
5. **A5:** Usar iconos distintivos por tipo de acción (crear, editar, eliminar, ver)
6. **A6:** Mostrar información contextual (ej: "Juan Pérez creó la carrera 'Ingeniería de Software'")
7. **A7:** Ordenar actividad por fecha/hora (descendente por defecto)
8. **A8:** Mostrar número limitado de entradas (ej: últimas 10, 20, 50)
9. **A9:** Proporcionar controles de filtrado (por usuario, tipo de acción, módulo, fecha)
10. **A10:** Mostrar indicador visual de tiempo transcurrido (ej: "Hace 5 minutos", "Hace 2 horas")
11. **A11:** Actualizar actividad automáticamente o con botón de refrescar
12. **A12:** Mostrar mensaje "No hay actividad reciente" cuando no hay datos
13. **A13:** Permitir paginación si hay muchas entradas
14. **A14:** Diferenciar visualmente tipos de acciones (códigos de color, iconos)

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 3 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Administrador autenticado
- **C2:** Hay actividad registrada en el sistema
- **C3:** Hay actividad reciente (periodo definido)

Total combinaciones teóricas: 2^3 = 8 reglas

| Regla | C1: Autenticado | C2: Actividad registrada | C3: Actividad reciente | Acción |
|-------|----------------|------------------------|---------------------|---------|
| R1 | N | - | - | Redirigir a login |
| R2 | S | N | N | A1-A2, A12: Dashboard sin actividad |
| R3 | S | N | S | Imposible (no puede tener reciente sin registro) |
| R4 | S | S | N | A1-A4, A7: Mostrar actividad antigua |
| R5 | S | S | S | A1-A11, A13-A14: Mostrar actividad reciente |

---

## **Tabla de Decisión Minimizada**

| Regla | Autenticado | Actividad registrada | Actividad reciente | Acción |
|-------|------------|---------------------|-------------------|---------|
| **R1** | N | - | - | Redirigir a login (prerrequisito) |
| **R2** | S | N | - | Mostrar Dashboard con mensaje "No hay actividad reciente" |
| **R3** | S | S | N | Mostrar Dashboard con actividad pero fuera del periodo reciente |
| **R4** | S | S | S | Mostrar Dashboard con actividad reciente completa (happy path) |

**Justificación de la minimización:**
- **R1:** Usuario no autenticado no puede acceder (seguridad)
- **R2:** Dashboard sin datos cuando no hay actividad registrada
- **R3:** Actividad existe pero no en el periodo "reciente" definido
- **R4:** Happy path: Dashboard con actividad reciente para monitoreo

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios principales)
- 5 escenarios adicionales para validar aspectos específicos:
  - Acceso desde menú lateral
  - Formato y estructura de entradas de actividad
  - Filtrado por tipo de acción o módulo
  - Actualización de actividad
  - Paginación o límite de entradas

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder al Dashboard desde el menú lateral**

**Dado que** estoy autenticado como Administrador en el sistema,  
**cuando** hago clic en la opción "Dashboard" ubicada en el menú lateral izquierdo,  
**entonces** se carga y muestra la pantalla "Dashboard" **Y** el título "Dashboard" aparece en la parte superior de la pantalla **Y** se presenta una sección claramente identificada como "Actividad Reciente" o "Últimas Acciones del Sistema" **Y** la opción "Dashboard" en el menú lateral se resalta indicando que es la sección activa **Y** puedo visualizar el registro de acciones realizadas en la plataforma.

---

**Escenario 2 – Visualizar registro de actividad reciente con múltiples acciones**

**Dado que** estoy autenticado como Administrador **Y** existen acciones recientes registradas en el sistema,  
**cuando** accedo a la pantalla "Dashboard",  
**entonces** se muestra la sección "Actividad Reciente" **Y** se presenta una lista o tabla cronológica de las últimas acciones realizadas **Y** las acciones se ordenan de más reciente a más antigua (orden descendente por timestamp) **Y** cada entrada de actividad muestra: fecha y hora de la acción, nombre del usuario que la realizó, tipo de acción (Crear, Editar, Eliminar, Ver), módulo o entidad afectada, descripción contextual de la acción **Y** por ejemplo, se muestran entradas como: "Juan Pérez creó la carrera 'Ingeniería de Software' - Hace 5 minutos", "María García editó la facultad 'Ingeniería Civil' - Hace 1 hora", "Admin eliminó el usuario 'test@epn.edu.ec' - Hace 2 horas" **Y** se muestran las últimas 10-20 acciones por defecto **Y** puedo monitorear efectivamente la actividad de la plataforma.

---

**Escenario 3 – Diferenciar visualmente tipos de acciones**

**Dado que** estoy visualizando el registro de "Actividad Reciente" en el Dashboard,  
**cuando** reviso las diferentes entradas de actividad,  
**entonces** cada tipo de acción tiene un indicador visual distintivo **Y** las acciones de tipo "Crear" se identifican con icono de "+" o color verde **Y** las acciones de tipo "Editar" se identifican con icono de lápiz o color azul **Y** las acciones de tipo "Eliminar" se identifican con icono de papelera o color rojo **Y** las acciones de tipo "Ver" o "Acceso" se identifican con icono de ojo o color gris **Y** la diferenciación visual me permite identificar rápidamente el tipo de acción sin leer el texto completo **Y** puedo escanear visualmente la actividad para detectar patrones o acciones específicas.

---

**Escenario 4 – Visualizar información contextual completa de cada acción**

**Dado que** estoy revisando el registro de actividad en el Dashboard,  
**cuando** observo cualquier entrada de actividad,  
**entonces** cada entrada proporciona contexto completo de la acción **Y** se muestra el nombre completo del usuario que realizó la acción (ej: "Juan Pérez García") **Y** se indica el módulo del sistema afectado (ej: "Gestión de Carreras", "Gestión de Usuarios") **Y** se especifica la entidad específica afectada (ej: nombre de la carrera creada, nombre del usuario editado) **Y** se presenta timestamp con formato legible y relativo (ej: "Hace 5 minutos", "Hace 2 horas", "Hace 1 día", "2025-01-15 14:30") **Y** opcionalmente se muestra información adicional como cambios específicos realizados **Y** la información es suficiente para entender qué ocurrió, quién lo hizo, cuándo y dónde sin necesidad de abrir detalles adicionales.

---

**Escenario 5 – Visualizar Dashboard sin actividad reciente**

**Dado que** estoy autenticado como Administrador **Y** no existen acciones recientes registradas en el sistema (plataforma nueva o sin actividad en periodo definido),  
**cuando** accedo a la pantalla "Dashboard",  
**entonces** se muestra la sección "Actividad Reciente" **Y** se presenta un mensaje informativo "No hay actividad reciente registrada" o "Aún no se han realizado acciones en el sistema" **Y** el mensaje se muestra de forma clara y centrada en el área de actividad **Y** opcionalmente se muestra un ícono o ilustración indicando ausencia de datos **Y** no se muestra una lista vacía sin contexto **Y** el mensaje me confirma que el sistema está funcionando pero simplemente no hay actividad que mostrar.

---

**Escenario 6 – Filtrar actividad por tipo de acción**

**Dado que** estoy en el Dashboard visualizando "Actividad Reciente" **Y** hay múltiples tipos de acciones registradas,  
**cuando** aplico un filtro seleccionando un tipo de acción específico (ej: selecciono filtro "Crear" o "Eliminar"),  
**entonces** la lista de actividad se actualiza mostrando solo las acciones del tipo seleccionado **Y** por ejemplo, si filtro por "Crear" solo se muestran acciones de creación de entidades **Y** se mantiene el orden cronológico descendente **Y** se muestra indicador visual del filtro activo (ej: "Mostrando solo: Crear") **Y** puedo quitar el filtro para volver a ver todas las acciones **Y** el filtrado me permite enfocarme en tipos específicos de actividad para monitoreo especializado.

---

**Escenario 7 – Filtrar actividad por módulo del sistema**

**Dado que** estoy en el Dashboard visualizando "Actividad Reciente" **Y** hay acciones de múltiples módulos (Facultades, Carreras, Usuarios, Roles),  
**cuando** aplico un filtro seleccionando un módulo específico (ej: selecciono "Gestión de Usuarios"),  
**entonces** la lista de actividad se actualiza mostrando solo las acciones realizadas en el módulo "Gestión de Usuarios" **Y** se excluyen acciones de otros módulos (Facultades, Carreras, Roles) **Y** se mantiene el orden cronológico **Y** se muestra indicador del filtro activo (ej: "Módulo: Gestión de Usuarios") **Y** puedo cambiar a otro módulo o quitar el filtro **Y** el filtrado por módulo me permite monitorear actividad específica de áreas del sistema.

---

**Escenario 8 – Actualizar registro de actividad para ver acciones nuevas**

**Dado que** estoy visualizando "Actividad Reciente" en el Dashboard **Y** han transcurrido varios minutos desde que cargué la pantalla,  
**cuando** hago clic en un botón "Actualizar" o "Refrescar" (ícono de círculo con flechas) **O** el sistema actualiza automáticamente después de un intervalo de tiempo,  
**entonces** el registro de actividad se actualiza con las acciones más recientes **Y** las nuevas acciones aparecen en la parte superior de la lista **Y** las acciones anteriores se desplazan hacia abajo **Y** opcionalmente se resaltan brevemente las nuevas entradas (ej: fondo amarillo temporal) para indicar que son nuevas **Y** los timestamps se actualizan (ej: "Hace 5 minutos" cambia a "Hace 15 minutos") **Y** puedo monitorear la actividad en tiempo casi real sin recargar la página completa.

---

**Escenario 9 – Limitar y paginar el registro de actividad**

**Dado que** estoy visualizando "Actividad Reciente" en el Dashboard **Y** existen cientos o miles de acciones registradas en el sistema,  
**cuando** se carga la pantalla Dashboard por primera vez,  
**entonces** se muestran solo las últimas 10, 20 o 50 acciones más recientes (número definido por diseño) **Y** se proporciona un mecanismo de paginación (botones "Ver más", "Cargar más acciones", o controles de paginación) **Y** si hago clic en "Ver más" o "Siguiente página", se cargan las siguientes acciones cronológicamente **Y** opcionalmente se muestra indicador de cuántas acciones se están mostrando (ej: "Mostrando 20 de 500 acciones") **Y** la limitación evita sobrecarga de datos y mejora el rendimiento **Y** puedo acceder a actividad más antigua si es necesario mediante paginación o link a vista completa de logs.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 2 – Visualizar registro de actividad reciente con múltiples acciones**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Administrador quiere "ver un registro de las últimas acciones realizadas en el sistema para monitorear la actividad de la plataforma". El Escenario 2 valida directamente la capacidad de VER y MONITOREAR el registro de acciones, que es el objetivo principal.

2. **Representa el "happy path" del caso de uso principal:** Es el escenario que los administradores ejecutarán constantemente:
   - Revisar qué acciones se han realizado recientemente
   - Monitorear actividad de usuarios en tiempo real
   - Detectar patrones de uso de la plataforma
   - Identificar acciones sospechosas o erróneas
   - Auditar operaciones del sistema

3. **Valida todos los elementos informativos críticos:** El Escenario 2 verifica que cada entrada de actividad incluya:
   - **Timestamp** (fecha y hora) - cuándo ocurrió
   - **Usuario** - quién lo hizo
   - **Tipo de acción** - qué tipo de operación (crear, editar, eliminar)
   - **Módulo/Entidad** - dónde y sobre qué
   - **Descripción contextual** - información completa de la acción
   - **Orden cronológico** - más reciente primero para monitoreo efectivo

4. **Impacto directo en monitoreo de plataforma:** Sin este escenario funcionando:
   - El administrador no puede supervisar actividad del sistema
   - No puede detectar acciones no autorizadas o erróneas
   - No puede auditar operaciones realizadas
   - No puede identificar patrones de uso o problemas
   - Se pierde visibilidad sobre qué está ocurriendo en la plataforma

5. **Crítico para seguridad y auditoría:** El registro de actividad es fundamental para:
   - **Seguridad:** Detectar accesos no autorizados o actividad sospechosa
   - **Auditoría:** Cumplir requisitos de trazabilidad y rendición de cuentas
   - **Troubleshooting:** Identificar qué cambios causaron problemas
   - **Cumplimiento:** Demostrar controles y registros ante auditorías externas
   - **Gobernanza:** Validar que las políticas se están siguiendo

6. **Fundamento para otros escenarios:** Los escenarios de filtrado (6-7), actualización (8), y paginación (9) son mejoras sobre el escenario base. Sin la capacidad de ver el registro básico de actividad, las capacidades avanzadas de filtrado carecen de valor.

7. **Mayor frecuencia de uso:** En operación diaria:
   - Los administradores revisan actividad reciente múltiples veces al día
   - Es una de las primeras cosas que se verifica al entrar al sistema
   - Es el punto de partida para investigaciones de incidentes
   - Es la herramienta principal de supervisión continua

8. **Validación de integridad del sistema de logging:** Verifica que:
   - Las acciones se están registrando correctamente en el sistema
   - Los datos se recuperan adecuadamente de la base de datos
   - La información se presenta de forma legible y útil
   - El orden cronológico se mantiene correctamente

9. **Impacto en respuesta a incidentes:** Cuando ocurre un problema:
   - El administrador accede inmediatamente al Dashboard
   - Revisa la actividad reciente para identificar qué cambió
   - Busca acciones específicas que puedan haber causado el problema
   - Identifica al usuario responsable para comunicación
   - Sin esta funcionalidad, la resolución de problemas es ciega

10. **Crítico para casos de uso reales en instituciones académicas:** En la EPN:
    - Detectar si alguien eliminó una carrera o facultad por error
    - Monitorear quién está editando información crítica
    - Verificar que los coordinadores están actualizando información
    - Auditar cambios en permisos de roles
    - Identificar acciones masivas o sospechosas
    - Cumplir requisitos de acreditación sobre trazabilidad

Los demás escenarios son importantes para funcionalidad completa (filtros avanzados, actualización automática, diferenciación visual), pero el Escenario 2 es el que garantiza que el sistema cumple su promesa fundamental: **permitir al Administrador ver un registro completo y ordenado cronológicamente de las últimas acciones realizadas en el sistema para monitorear efectivamente la actividad de la plataforma, que es el valor central y el caso de uso más crítico para supervisión, seguridad, auditoría y gobernanza institucional**.