# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 14 del prototipo):**

1. **C1:** Existen suficientes usuarios registrados que requieren múltiples páginas
2. **C2:** El usuario está en la primera página del listado
3. **C3:** El usuario está en una página intermedia (ni primera ni última)
4. **C4:** El usuario está en la última página del listado
5. **C5:** Hay filtros o búsquedas aplicados que reducen el total de resultados
6. **C6:** El tamaño de página está definido (número de filas por página)

### **Acciones del Sistema (observadas en Imagen 14):**

1. **A1:** Mostrar controles de paginación en la parte inferior de la tabla de usuarios
2. **A2:** Mostrar botón "< Previous" (Anterior)
3. **A3:** Mostrar números de página individuales (ej: "1 2 3")
4. **A4:** Mostrar botón "Next >" (Siguiente)
5. **A5:** Resaltar o marcar visualmente la página actual
6. **A6:** Deshabilitar botón "< Previous" cuando se está en la primera página
7. **A7:** Habilitar botón "< Previous" cuando no se está en la primera página
8. **A8:** Deshabilitar botón "Next >" cuando se está en la última página
9. **A9:** Habilitar botón "Next >" cuando no se está en la última página
10. **A10:** Cargar y mostrar usuarios correspondientes a la página seleccionada
11. **A11:** Actualizar tabla sin recargar la página completa
12. **A12:** Mantener filtros y búsquedas activos al cambiar de página
13. **A13:** Actualizar URL o estado para permitir navegación con botones del navegador
14. **A14:** Ocultar controles de paginación cuando todos los usuarios caben en una página

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 3 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Requiere múltiples páginas
- **C2:** Está en primera página
- **C3:** Está en última página

Total combinaciones teóricas: 2^3 = 8 reglas

| Regla | C1: Múltiples páginas | C2: Primera página | C3: Última página | Acción |
|-------|----------------------|-------------------|------------------|---------|
| R1 | N | N | N | A14: Ocultar controles de paginación |
| R2 | N | N | S | Imposible (no hay páginas múltiples) |
| R3 | N | S | N | Imposible (no hay páginas múltiples) |
| R4 | N | S | S | Imposible (solo hay una página) |
| R5 | S | N | N | A1-A5, A7, A9, A10-A13: Página intermedia |
| R6 | S | N | S | Imposible (no puede ser ni primera ni última a la vez) |
| R7 | S | S | N | A1-A6, A9, A10-A13: Primera página con más páginas |
| R8 | S | S | S | Imposible (solo hay una página entonces) |

---

## **Tabla de Decisión Minimizada**

| Regla | Múltiples páginas | Primera página | Última página | Acción |
|-------|------------------|---------------|---------------|---------|
| **R1** | N | - | - | Ocultar controles de paginación (todos los usuarios en una página) |
| **R2** | S | S | N | Mostrar controles, deshabilitar "Previous", habilitar "Next" |
| **R3** | S | N | S | Mostrar controles, habilitar "Previous", deshabilitar "Next" |
| **R4** | S | N | N | Mostrar controles, habilitar "Previous" y "Next" (página intermedia) |

**Justificación de la minimización:**
- **R1:** Si no requiere múltiples páginas, los controles de paginación no son necesarios (fusiona R1, R4)
- **R2:** En la primera página con más páginas disponibles, "Previous" deshabilitado, "Next" habilitado (R7)
- **R3:** En la última página, "Previous" habilitado, "Next" deshabilitado (combinación lógica)
- **R4:** En página intermedia, ambos botones habilitados (R5)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 9 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios de paginación)
- 5 escenarios adicionales para validar funcionalidades específicas:
  - Clic en número de página específico
  - Navegación con botón "Next"
  - Navegación con botón "Previous"
  - Mantener filtros al cambiar de página
  - Comportamiento responsive de controles

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Visualizar controles de paginación con múltiples páginas de usuarios**

**Dado que** estoy autenticado como Administrador en el sistema **Y** estoy en la pantalla "Gestión de Usuarios" **Y** existen suficientes usuarios registrados que requieren múltiples páginas para mostrarlos todos,  
**cuando** se carga la vista inicial del listado de usuarios,  
**entonces** se muestran controles de paginación en la parte inferior de la tabla **Y** los controles incluyen el botón "< Previous" a la izquierda **Y** se muestran números de página individuales en el centro (ej: "1 2 3") **Y** se incluye el botón "Next >" a la derecha **Y** la página actual (página 1) está resaltada o marcada visualmente de manera diferente a las demás **Y** el botón "< Previous" está deshabilitado o visualmente inactivo porque estoy en la primera página **Y** el botón "Next >" está habilitado para navegación **Y** los números de página son clicables.

---

**Escenario 2 – Ocultar controles cuando todos los usuarios caben en una página**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** el número total de usuarios registrados es igual o menor al tamaño de página definido,  
**cuando** se carga el listado de usuarios,  
**entonces** se muestran todos los usuarios en una sola vista **Y** no se muestran controles de paginación en la parte inferior **Y** no aparecen botones "< Previous" ni "Next >" **Y** no se muestran números de página **Y** la tabla presenta todos los usuarios disponibles sin necesidad de navegación adicional.

---

**Escenario 3 – Navegar a la siguiente página usando botón "Next"**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** estoy visualizando la primera página de usuarios **Y** existen más páginas disponibles **Y** el botón "Next >" está habilitado,  
**cuando** hago clic en el botón "Next >",  
**entonces** la tabla se actualiza mostrando los usuarios de la página 2 **Y** la página actual se marca visualmente como "2" **Y** la tabla se actualiza sin recargar la página completa **Y** el botón "< Previous" se habilita porque ya no estoy en la primera página **Y** el botón "Next >" permanece habilitado si existen más páginas después de la 2 **Y** se mantiene visible la estructura de la tabla con todas sus columnas: "Email", "Nombre", "Rol", "Estado", "Acciones" **Y** la transición es fluida y sin pérdida de contexto.

---

**Escenario 4 – Navegar a la página anterior usando botón "Previous"**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** estoy visualizando la página 2 o superior **Y** el botón "< Previous" está habilitado,  
**cuando** hago clic en el botón "< Previous",  
**entonces** la tabla se actualiza mostrando los usuarios de la página anterior **Y** la página actual se actualiza visualmente (de "2" a "1", o de "3" a "2") **Y** la tabla se actualiza sin recargar la página completa **Y** si navego de vuelta a la página 1, el botón "< Previous" se deshabilita **Y** el botón "Next >" permanece habilitado **Y** se mantienen todos los datos y estructura de la tabla con los usuarios correspondientes.

---

**Escenario 5 – Navegar directamente a una página específica**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** se muestran controles de paginación con múltiples números de página (ej: "1 2 3"),  
**cuando** hago clic en un número de página específico (ej: hago clic en "3"),  
**entonces** la tabla se actualiza mostrando los usuarios correspondientes a la página 3 **Y** el número "3" se resalta o marca visualmente como página actual **Y** el número "1" pierde el resaltado de página actual **Y** la tabla se actualiza sin recargar la página completa **Y** el botón "< Previous" está habilitado porque no estoy en la primera página **Y** el botón "Next >" se habilita o deshabilita según si existen más páginas después de la 3 **Y** la navegación es inmediata al hacer clic.

---

**Escenario 6 – Deshabilitar botón "Next" en la última página**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** estoy navegando por las páginas de usuarios,  
**cuando** llego a la última página disponible (ej: página 3 de 3) mediante navegación o clic directo,  
**entonces** el número de la última página se resalta como página actual **Y** el botón "Next >" se deshabilita o muestra visualmente como inactivo **Y** el botón "< Previous" permanece habilitado porque no estoy en la primera página **Y** no es posible hacer clic en "Next >" para avanzar más **Y** se muestran todos los usuarios restantes de la última página **Y** los controles de paginación permanecen visibles pero con "Next" inactivo.

---

**Escenario 7 – Mantener filtros aplicados al cambiar de página**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** he aplicado filtros (ej: búsqueda por "juan" o filtro de rol "Profesor") **Y** los resultados filtrados requieren múltiples páginas **Y** estoy en la página 1 de los resultados filtrados,  
**cuando** hago clic en "Next >" o en un número de página diferente,  
**entonces** la tabla muestra la siguiente página de resultados filtrados **Y** se mantienen aplicados todos los filtros activos (búsqueda y/o dropdowns de rol y estado) **Y** solo se muestran usuarios que cumplen con los criterios de filtrado **Y** el campo de búsqueda conserva el texto ingresado **Y** los dropdowns de filtro conservan los valores seleccionados **Y** la paginación funciona solo sobre el conjunto de datos filtrados, no sobre todos los usuarios **Y** el número total de páginas se ajusta según los resultados filtrados.

---

**Escenario 8 – Actualizar controles de paginación cuando los filtros reducen resultados**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** tengo múltiples páginas de usuarios sin filtros,  
**cuando** aplico un filtro o búsqueda que reduce significativamente los resultados (ej: búsqueda que devuelve solo 3 usuarios),  
**entonces** los controles de paginación se ocultan automáticamente si todos los resultados caben en una página **Y** regreso automáticamente a la página 1 de los resultados filtrados **Y** si los resultados filtrados aún requieren paginación, se actualiza el número total de páginas mostradas (ej: de "1 2 3" a solo "1 2") **Y** los botones se habilitan/deshabilitan según corresponda a la nueva cantidad de páginas **Y** la actualización es inmediata al aplicar el filtro.

---

**Escenario 9 – Mostrar indicador visual claro de la página actual**

**Dado que** estoy en la pantalla "Gestión de Usuarios" **Y** estoy navegando por diferentes páginas del listado,  
**cuando** me encuentro en cualquier página específica (ej: página 2),  
**entonces** el número de la página actual (2) se distingue visualmente de los demás números de página **Y** la diferenciación puede ser mediante: fondo de color diferente, texto en negrita, subrayado, o cambio de color del texto **Y** solo un número de página está marcado como actual en cualquier momento **Y** al cambiar de página, el indicador visual se mueve inmediatamente al nuevo número de página **Y** es inmediatamente obvio para el administrador en qué página se encuentra sin necesidad de análisis adicional **Y** el indicador visual es consistente con el contenido mostrado en la tabla.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Navegar a la siguiente página usando botón "Next"**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Administrador quiere "navegar por el listado de usuarios en bloques manejables para gestionar grandes volúmenes de usuarios eficientemente". El Escenario 3 valida directamente la navegación secuencial hacia adelante, que es el flujo más natural y frecuente de uso de paginación.

2. **Representa el "happy path" principal de paginación:** Es el comportamiento más común y esperado:
   - Los administradores naturalmente comienzan en la página 1
   - La progresión natural es avanzar hacia adelante para ver más usuarios
   - Es el patrón de navegación más intuitivo y frecuente
   - Refleja el flujo de revisión secuencial de información

3. **Valida la funcionalidad core de gestión de grandes volúmenes:** Sin navegación hacia adelante efectiva:
   - El administrador queda atrapado en la primera página
   - No puede acceder al resto de los usuarios
   - Se pierde completamente el valor de la paginación
   - No se pueden gestionar eficientemente grandes volúmenes de usuarios

4. **Verifica comportamiento dinámico crítico:** El escenario valida múltiples aspectos técnicos esenciales:
   - Actualización de contenido de la tabla sin recarga completa
   - Cambio de estado de botones (habilitar "Previous")
   - Actualización de indicador visual de página actual
   - Carga correcta de datos de la página siguiente
   - Mantenimiento de contexto y estructura de la tabla
   - Preservación de todas las columnas (Email, Nombre, Rol, Estado, Acciones)

5. **Mayor frecuencia de uso que otras navegaciones:** En la práctica de gestión de usuarios:
   - Navegar hacia adelante (Next) es más frecuente que hacia atrás (Previous)
   - Navegar secuencialmente es más común que saltar a páginas específicas
   - Los administradores tienden a revisar usuarios progresivamente

6. **Fundamento para otros escenarios de paginación:**
   - **Escenario 4 (Previous):** Es la operación inversa, pero menos frecuente
   - **Escenario 5 (página específica):** Es un atajo, pero Next es el método base
   - **Escenario 6 (última página):** Es un caso límite del uso repetido de Next
   - Sin Next funcionando, los demás escenarios pierden contexto

7. **Impacto directo en eficiencia de gestión (objetivo de la HU):** La navegación fluida con Next permite:
   - Revisar sistemáticamente todos los usuarios del sistema
   - Gestionar información en bloques manejables (como indica la HU)
   - Mantener contexto mientras se explora el dataset completo de usuarios
   - Evitar sobrecarga cognitiva de ver cientos de usuarios simultáneamente

8. **Validación de experiencia de usuario esperada:** Los administradores esperan que:
   - Next los lleve a la página siguiente inmediatamente
   - El contenido se actualice sin interrupciones
   - El estado de la página se refleje claramente
   - La navegación sea fluida y sin fricciones técnicas

9. **Precedencia operativa en gestión de usuarios:** Los administradores típicamente:
   - Revisan usuarios secuencialmente para auditorías
   - Verifican asignaciones de roles página por página
   - Necesitan avanzar progresivamente para análisis completo de la base de usuarios
   - Raramente saltan aleatoriamente entre páginas sin un patrón

10. **Diferenciación de escenarios complementarios:**
    - **Escenarios 1-2:** Validan presencia/ausencia de controles (setup inicial)
    - **Escenario 3:** Valida la acción principal de navegación hacia adelante
    - **Escenarios 4-6:** Validan direcciones alternativas y casos límite
    - **Escenarios 7-9:** Validan características auxiliares (filtros, indicadores)

Los demás escenarios son importantes para robustez (Previous, página específica, casos límite) y características avanzadas (filtros, indicadores), pero el Escenario 3 es el que garantiza que el sistema cumple su propósito fundamental: **permitir al Administrador navegar eficientemente hacia adelante por bloques manejables de usuarios para gestionar grandes volúmenes de manera efectiva, que es la funcionalidad core y el flujo de uso más frecuente de la paginación para gestión de usuarios a gran escala**.