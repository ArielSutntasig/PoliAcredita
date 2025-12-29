# **NOTA IMPORTANTE**

Revisando las imágenes analizadas en nuestra conversación (Gestión de Facultades, Gestión de Carreras, Gestión de Usuarios, Gestión de Roles, y Mi Perfil), **no he identificado una imagen específica que muestre un Dashboard con "Estadísticas Generales" o indicadores numéricos sobre el estado de la EPN**.

Procederé con el análisis basándome en:
1. La Historia de Usuario proporcionada
2. Mejores prácticas para dashboards administrativos con métricas institucionales
3. El patrón de diseño y navegación observado en las pantallas previas
4. Datos típicos relevantes para una institución académica (total de facultades, carreras, usuarios, estudiantes, etc.)

Si existe una imagen específica de Dashboard con Estadísticas Generales, por favor compártela para un análisis más preciso.

---

# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + inferencias de patrón de UI):**

1. **C1:** Administrador está autenticado en el sistema
2. **C2:** Administrador accede a la pantalla "Dashboard"
3. **C3:** Existen datos registrados en el sistema (facultades, carreras, usuarios)
4. **C4:** Existe sección "Estadísticas Generales" o "Resumen General" visible
5. **C5:** Hay métricas numéricas actualizadas disponibles
6. **C6:** Las estadísticas cubren múltiples áreas (académica, administrativa, usuarios)
7. **C7:** Los datos se actualizan en tiempo real o periódicamente
8. **C8:** Hay visualizaciones gráficas (gráficos, tarjetas, indicadores)

### **Acciones del Sistema (inferidas según mejores prácticas):**

1. **A1:** Mostrar pantalla "Dashboard" con título principal
2. **A2:** Presentar sección "Estadísticas Generales" o "Resumen de la EPN" prominentemente
3. **A3:** Mostrar tarjetas de métricas clave con iconos distintivos
4. **A4:** Presentar métricas numéricas: Total de Facultades, Total de Carreras, Total de Usuarios/Profesores, Total de Estudiantes
5. **A5:** Usar formato de tarjetas con número grande + etiqueta descriptiva
6. **A6:** Incluir iconos representativos (edificio para facultades, diploma para carreras, persona para usuarios)
7. **A7:** Organizar métricas en cuadrícula (ej: 2x2 o 4 columnas)
8. **A8:** Mostrar indicadores de tendencia (flechas arriba/abajo, porcentajes de cambio)
9. **A9:** Incluir visualizaciones gráficas (gráficos de barras, líneas, tortas) para distribuciones
10. **A10:** Actualizar datos al cargar la pantalla
11. **A11:** Mostrar timestamp de última actualización
12. **A12:** Proporcionar opción de refrescar datos manualmente
13. **A13:** Mostrar mensaje "Sin datos disponibles" si no hay información
14. **A14:** Permitir hacer clic en métricas para ir a detalles (ej: clic en "Facultades" → Gestión de Facultades)

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 3 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Administrador autenticado
- **C2:** Hay datos registrados en sistema
- **C3:** Datos están actualizados

Total combinaciones teóricas: 2^3 = 8 reglas

| Regla | C1: Autenticado | C2: Datos existen | C3: Datos actualizados | Acción |
|-------|----------------|------------------|----------------------|---------|
| R1 | N | - | - | Redirigir a login |
| R2 | S | N | N | A1-A2, A13: Dashboard sin datos |
| R3 | S | N | S | Imposible (no puede actualizar sin datos) |
| R4 | S | S | N | A1-A7: Datos desactualizados |
| R5 | S | S | S | A1-A12, A14: Dashboard completo (happy path) |

---

## **Tabla de Decisión Minimizada**

| Regla | Autenticado | Datos existen | Datos actualizados | Acción |
|-------|------------|--------------|-------------------|---------|
| **R1** | N | - | - | Redirigir a login (prerrequisito) |
| **R2** | S | N | - | Mostrar Dashboard con "Sin datos disponibles" |
| **R3** | S | S | N | Mostrar estadísticas con advertencia de datos desactualizados |
| **R4** | S | S | S | Mostrar estadísticas generales completas y actualizadas |

**Justificación de la minimización:**
- **R1:** Usuario no autenticado no puede acceder (seguridad)
- **R2:** Dashboard sin métricas cuando no hay datos en el sistema
- **R3:** Datos existen pero pueden estar desactualizados (caso de actualización periódica)
- **R4:** Happy path: Dashboard con todas las estadísticas actualizadas

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 10 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios principales)
- 6 escenarios adicionales para validar aspectos específicos:
  - Visualización de métricas específicas (Facultades, Carreras, Usuarios)
  - Formato visual de tarjetas de estadísticas
  - Interactividad (clic para detalles)
  - Actualización de datos
  - Visualizaciones gráficas complementarias

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder al Dashboard con estadísticas generales**

**Dado que** estoy autenticado como Administrador en el sistema,  
**cuando** accedo a la opción "Dashboard" desde el menú lateral,  
**entonces** se carga y muestra la pantalla "Dashboard" con título principal **Y** se presenta una sección claramente identificada como "Estadísticas Generales", "Resumen de la EPN", o "Indicadores Institucionales" **Y** la sección contiene datos generales sobre el estado actual de la EPN **Y** puedo observar métricas numéricas clave de forma inmediata **Y** la información está organizada de manera visual y escaneable **Y** la opción "Dashboard" en el menú lateral se resalta indicando que es la sección activa.

---

**Escenario 2 – Visualizar estadísticas de total de facultades**

**Dado que** estoy en la pantalla "Dashboard" **Y** existen facultades registradas en el sistema,  
**cuando** visualizo la sección de "Estadísticas Generales",  
**entonces** se muestra una tarjeta o indicador de métrica para "Total de Facultades" o "Facultades" **Y** la tarjeta presenta el número total de facultades registradas en formato grande y destacado (ej: número de 2-3 dígitos en tamaño 32-48px) **Y** la etiqueta descriptiva "Facultades" o "Total de Facultades" está debajo o al lado del número **Y** se incluye un icono representativo de facultades (ej: edificio, universidad, columnas griegas) **Y** el diseño de la tarjeta es consistente con el sistema (fondo blanco, bordes, sombra sutil) **Y** puedo conocer inmediatamente cuántas facultades tiene la EPN actualmente.

---

**Escenario 3 – Visualizar estadísticas de total de carreras**

**Dado que** estoy en la pantalla "Dashboard" **Y** existen carreras registradas en el sistema,  
**cuando** visualizo la sección de "Estadísticas Generales",  
**entonces** se muestra una tarjeta o indicador de métrica para "Total de Carreras" o "Carreras" **Y** la tarjeta presenta el número total de carreras registradas en formato grande (ej: 25, 42, 67) **Y** la etiqueta "Carreras" o "Programas Académicos" identifica claramente la métrica **Y** se incluye un icono representativo (ej: diploma, birrete de graduación, certificado) **Y** puedo conocer el alcance de la oferta académica de la EPN **Y** el diseño visual es consistente con otras tarjetas de métricas.

---

**Escenario 4 – Visualizar estadísticas de total de usuarios o profesores**

**Dado que** estoy en la pantalla "Dashboard" **Y** existen usuarios registrados en el sistema,  
**cuando** visualizo la sección de "Estadísticas Generales",  
**entonces** se muestra una tarjeta para "Total de Usuarios", "Profesores", o "Personal" **Y** la tarjeta presenta el número total de usuarios/profesores registrados (ej: 150, 320, 500) **Y** la etiqueta identifica claramente si son usuarios totales, solo profesores, o personal académico **Y** se incluye icono de persona o grupo de personas **Y** puedo conocer el tamaño del cuerpo docente o usuarios activos de la EPN **Y** la tarjeta sigue el mismo patrón visual de las demás.

---

**Escenario 5 – Visualizar múltiples métricas organizadas en cuadrícula**

**Dado que** estoy en la pantalla "Dashboard" **Y** hay datos de múltiples categorías,  
**cuando** visualizo las "Estadísticas Generales",  
**entonces** las tarjetas de métricas están organizadas en una cuadrícula limpia (ej: 2 filas × 2 columnas, o 1 fila × 4 columnas) **Y** todas las tarjetas tienen el mismo tamaño y diseño para consistencia visual **Y** hay espaciado adecuado entre tarjetas (ej: 16-24px) **Y** las métricas están ordenadas lógicamente (ej: Facultades → Carreras → Profesores → Estudiantes) **Y** el diseño es responsive y se adapta a diferentes tamaños de pantalla **Y** puedo escanear todas las métricas rápidamente con una vista general **Y** obtengo una visión panorámica del estado actual de la EPN.

---

**Escenario 6 – Navegar a detalles haciendo clic en una métrica**

**Dado que** estoy visualizando las "Estadísticas Generales" en el Dashboard **Y** veo la tarjeta "Total de Carreras" con el número actual,  
**cuando** hago clic en la tarjeta "Total de Carreras" o en el número/ícono,  
**entonces** soy redirigido directamente a la pantalla "Gestión de Carreras" (observada en imagen 10) **Y** puedo ver el listado completo de todas las carreras registradas **Y** la navegación me permite profundizar desde el resumen a los detalles **Y** puedo regresar al Dashboard usando el menú lateral o botón "atrás" del navegador **Y** la interactividad de las métricas facilita la navegación contextual desde estadísticas a gestión detallada.

---

**Escenario 7 – Visualizar Dashboard sin datos registrados en el sistema**

**Dado que** estoy autenticado como Administrador **Y** el sistema es nuevo y NO tiene facultades, carreras ni usuarios registrados,  
**cuando** accedo a la pantalla "Dashboard",  
**entonces** se muestra la sección "Estadísticas Generales" **Y** las tarjetas de métricas muestran valores en cero: "0 Facultades", "0 Carreras", "0 Usuarios" **Y** opcionalmente se muestra un mensaje informativo como "No hay datos registrados aún. Comience agregando facultades y carreras." **Y** se pueden mostrar enlaces de acción rápida para "Crear Primera Facultad" o "Configurar Sistema" **Y** el mensaje es claro y orientador sin ser alarmante **Y** puedo conocer que el sistema está funcionando pero vacío.

---

**Escenario 8 – Actualizar estadísticas manualmente**

**Dado que** estoy visualizando las "Estadísticas Generales" en el Dashboard **Y** han transcurrido varios minutos o he realizado cambios en otros módulos,  
**cuando** hago clic en un botón "Actualizar" o "Refrescar" (ícono de círculo con flechas) asociado a las estadísticas,  
**entonces** el sistema recalcula las métricas consultando la base de datos **Y** los números en las tarjetas se actualizan con los valores más recientes **Y** se muestra brevemente un indicador de carga (spinner) durante la actualización **Y** se actualiza el timestamp de "Última actualización" (ej: "Actualizado: 2025-10-02 15:30") **Y** las estadísticas reflejan el estado actual real de la EPN después de cualquier cambio reciente **Y** puedo asegurarme de que estoy viendo información actualizada.

---

**Escenario 9 – Visualizar indicadores de tendencia o cambios**

**Dado que** estoy visualizando las "Estadísticas Generales" **Y** el sistema tiene datos históricos de periodos anteriores,  
**cuando** observo las tarjetas de métricas,  
**entonces** opcionalmente se muestran indicadores de tendencia junto a cada número **Y** por ejemplo: "42 Carreras ↑ +3 (7%)" indica que aumentaron 3 carreras respecto al periodo anterior **Y** o "15 Facultades → (0%)" indica que no hubo cambios **Y** flechas verdes hacia arriba indican crecimiento, flechas rojas hacia abajo indican disminución **Y** los porcentajes de cambio proporcionan contexto sobre la evolución **Y** puedo conocer no solo el estado actual sino también la dirección del cambio **Y** los indicadores me ayudan a monitorear crecimiento o contracción institucional.

---

**Escenario 10 – Visualizar gráficos complementarios de distribución**

**Dado que** estoy en el Dashboard visualizando "Estadísticas Generales" **Y** hay suficientes datos para análisis,  
**cuando** scroll hacia abajo o reviso la sección completa de estadísticas,  
**entonces** opcionalmente se presentan visualizaciones gráficas complementarias **Y** por ejemplo: gráfico de barras mostrando "Carreras por Facultad" con número de carreras de cada facultad **Y** o gráfico de torta mostrando "Distribución de Usuarios por Rol" (% Profesores, % Coordinadores, % Administradores) **Y** o gráfico de líneas mostrando "Evolución de Estudiantes" en los últimos 6-12 meses **Y** cada gráfico tiene título descriptivo, leyenda clara, y etiquetas en ejes **Y** los colores son consistentes con el esquema del sistema **Y** las visualizaciones complementan las métricas numéricas proporcionando contexto adicional **Y** puedo obtener insights más profundos sobre el estado y distribución de datos de la EPN.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 5 – Visualizar múltiples métricas organizadas en cuadrícula**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Administrador quiere "observar datos generales de la EPN para conocer el estado actual de la EPN". El Escenario 5 valida que MÚLTIPLES datos generales se presentan SIMULTÁNEAMENTE de forma organizada, permitiendo conocer el estado actual completo de un vistazo.

2. **Representa el "happy path" completo de la visualización:** Es el escenario que demuestra el valor real del Dashboard:
   - Administrador accede al Dashboard
   - Ve TODAS las métricas clave simultáneamente (Facultades, Carreras, Usuarios, etc.)
   - Las métricas están organizadas visualmente para fácil escaneo
   - Obtiene visión panorámica del estado institucional en segundos
   - No necesita navegar a múltiples pantallas para obtener el resumen

3. **Valida la experiencia de usuario completa:** El escenario verifica aspectos críticos de usabilidad:
   - **Organización visual:** Cuadrícula limpia y ordenada
   - **Consistencia:** Todas las tarjetas con mismo diseño
   - **Espaciado:** Separación adecuada entre elementos
   - **Orden lógico:** Métricas organizadas coherentemente
   - **Responsive:** Adaptación a diferentes pantallas
   - **Escaneabilidad:** Información accesible de un vistazo

4. **Mayor valor informativo agregado:** Una sola métrica (Escenarios 2-4) proporciona información limitada:
   - "42 Carreras" → información parcial
   - Pero "15 Facultades + 42 Carreras + 320 Profesores + 2,500 Estudiantes" → **visión completa**
   - El conjunto de métricas proporciona contexto y relaciones entre datos
   - Puedo entender proporciones (ej: 42 carreras / 15 facultades = ~3 carreras por facultad)

5. **Impacto directo en toma de decisiones institucionales:** Con múltiples métricas visibles:
   - Los administradores pueden identificar desbalances (ej: pocas carreras en una facultad grande)
   - Pueden detectar necesidades de recursos (ej: muchos estudiantes, pocos profesores)
   - Pueden monitorear crecimiento equilibrado
   - Pueden tomar decisiones informadas sobre expansión o ajustes

6. **Fundamento para otros escenarios:** Los escenarios individuales (2-4) son componentes del escenario completo. Si las múltiples métricas NO se organizan bien en cuadrícula:
   - Las métricas individuales pierden valor en conjunto
   - La información se vuelve confusa o difícil de comparar
   - Se pierde la visión panorámica que es el objetivo

7. **Mayor frecuencia de uso y valor percibido:** En operación diaria:
   - Los administradores NO acceden al Dashboard para ver una sola métrica
   - Acceden para obtener una visión general completa del estado institucional
   - El valor está en ver TODO el panorama simultáneamente
   - Es el caso de uso principal y más frecuente

8. **Crítico para contexto institucional:** En la EPN como institución académica:
   - El "estado actual" no es un número aislado, es el conjunto
   - Los datos se relacionan entre sí (facultades contienen carreras, carreras tienen profesores)
   - La organización visual refleja la estructura institucional
   - El Dashboard debe proporcionar inteligencia situacional completa

9. **Validación de arquitectura de información:** El escenario verifica que:
   - El sistema puede consultar y presentar múltiples métricas simultáneamente
   - El rendimiento es adecuado al cargar varios datos
   - La interfaz maneja múltiples tarjetas sin sobrecarga visual
   - La información se prioriza y organiza correctamente

10. **Impacto en satisfacción del usuario:** Si las métricas NO están bien organizadas:
    - El Dashboard se ve desordenado y poco profesional
    - Los usuarios tienen dificultad para encontrar información
    - Se reduce la confianza en el sistema
    - Se pierde el beneficio de tener un resumen ejecutivo
    - Pero con buena organización: valor percibido alto, satisfacción, eficiencia

Los demás escenarios son importantes para completitud (métricas individuales, interactividad, actualización, gráficos), pero el Escenario 5 es el que garantiza que el sistema cumple su promesa fundamental: **permitir al Administrador observar simultáneamente múltiples datos generales de la EPN organizados visualmente en una cuadrícula coherente para conocer el estado actual completo de la institución de un vistazo, que es el valor central y el caso de uso principal de las estadísticas generales en un Dashboard administrativo**.