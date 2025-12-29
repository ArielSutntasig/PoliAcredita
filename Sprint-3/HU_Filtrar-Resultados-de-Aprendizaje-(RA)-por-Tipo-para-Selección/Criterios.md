# **CRITERIOS DE ACEPTACIÓN - HU: Filtrar Resultados de Aprendizaje (RA) por Tipo para Selección**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis del Paso 2 del wizard):**

**C1:** Usuario está en Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)"  
**C2:** Dropdown "Tipo de Aprendizaje" tiene opción seleccionada  
**C3:** Tipo "Conocimientos" seleccionado  
**C4:** Tipo "Destrezas" seleccionado  
**C5:** Tipo "Valores y actitudes" seleccionado  
**C6:** Existen RA del tipo seleccionado en la carrera

**Nota:** C3, C4, C5 son mutuamente excluyentes (solo una puede ser verdadera a la vez).

#### **ACCIONES DEL SISTEMA:**

**A1:** Mostrar dropdown "Tipo de Aprendizaje" visible y funcional  
**A2:** Mostrar opciones en dropdown: "Conocimientos", "Destrezas", "Valores y actitudes"  
**A3:** Mostrar todos los RA sin filtrar (estado inicial)  
**A4:** Filtrar tabla mostrando solo RA de tipo "Conocimientos"  
**A5:** Filtrar tabla mostrando solo RA de tipo "Destrezas"  
**A6:** Filtrar tabla mostrando solo RA de tipo "Valores y actitudes"  
**A7:** Actualizar tabla automáticamente al seleccionar tipo  
**A8:** Ocultar RA que no corresponden al tipo seleccionado  
**A9:** Mantener checkboxes para selección en RA filtrados  
**A10:** Combinar filtro con búsqueda por código/descripción si está activa  
**A11:** Permitir cambiar de tipo o quitar filtro para ver todos los RA  
**A12:** Mantener estructura de tabla (columnas Código y Descripción)  
**A13:** Actualizar paginación según cantidad de resultados filtrados

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard** | F | F | F | F | V | V | V | V |
| **C2: Dropdown con selección** | F | F | V | V | F | F | V | V |
| **C3: "Conocimientos" seleccionado** | F | V | F | V | F | V | F | V |
| **C4: "Destrezas" seleccionado** | F | F | F | F | F | F | V | V |
| **C6: Existen RA del tipo** | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1-A3: Mostrar sin filtrar | - | - | - | - | X | - | - | - |
| A4-A9: Filtrar por tipo | - | - | - | - | - | - | - | X |

**Análisis:** R1-R4 son inválidas (fuera de contexto). C3, C4, C5 son mutuamente excluyentes.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** |
|-----------|--------|--------|--------|--------|
| **C1: En Paso 2 wizard vinculación** | V | V | V | V |
| **C2: Dropdown "Tipo" con selección** | F | V | V | V |
| **Tipo seleccionado** | - | Conocimientos | Destrezas | Valores/Act. |
| **C6: Existen RA del tipo** | V | V | V | V |
| **ACCIONES** |
| A1-A2: Dropdown visible con opciones | X | X | X | X |
| A3: Mostrar todos los RA (sin filtrar) | X | - | - | - |
| A4: Filtrar por "Conocimientos" | - | X | - | - |
| A5: Filtrar por "Destrezas" | - | - | X | - |
| A6: Filtrar por "Valores y actitudes" | - | - | - | X |
| A7-A9: Actualizar y mantener selección | - | X | X | X |
| A10: Combinar con búsqueda | X | X | X | X |
| A11-A13: Funcionalidad adicional | X | X | X | X |

**Justificación de minimización:**

- **R1:** Estado inicial sin filtro - muestra todos los RA disponibles.
- **R2:** Filtro por "Conocimientos" - muestra solo RA de conocimientos.
- **R3:** Filtro por "Destrezas" - muestra solo RA de destrezas.
- **R4:** Filtro por "Valores y actitudes" - muestra solo RA de este tipo.

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada:** 4 reglas

**Análisis de consolidación:**
- R2, R3, R4 pueden consolidarse parcialmente ya que la lógica de filtrado es idéntica (solo cambia el tipo)
- Sin embargo, mantenerlos separados es valioso para validar cada opción del dropdown

**Criterios de Aceptación finales:** **4 AC**

1. **AC1:** Visualizar dropdown de tipo sin filtro aplicado
2. **AC2:** Filtrar RA por tipo "Conocimientos"
3. **AC3:** Filtrar RA por tipo "Destrezas"
4. **AC4:** Filtrar RA por tipo "Valores y actitudes"

Alternativamente, podría consolidarse en 3 AC (estado inicial + un solo AC para filtrado que cubra los 3 tipos), pero mantendré 4 para mayor claridad en validación.

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Visualizar dropdown de tipo sin filtro aplicado**

**Dado que** soy un coordinador de carrera **Y** estoy en el wizard de vinculación "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** he completado el Paso 1 seleccionando RAA **Y** estoy en el Paso 2 "Seleccionar Resultados de Aprendizaje (RA)",  
**cuando** visualizo el Paso 2 sin haber aplicado ningún filtro de tipo,  
**entonces** se muestra el dropdown "Tipo de Aprendizaje" visible en la parte superior de la tabla **Y** el dropdown está sin selección (mostrando placeholder o valor por defecto) **Y** al hacer clic en el dropdown se despliegan las opciones: "Conocimientos", "Destrezas", "Valores y actitudes" **Y** se presenta la tabla con TODOS los RA de la carrera sin filtrado por tipo **Y** cada RA muestra su código (ej: RG1, RG2, RE1, RE2) y descripción completa **Y** cada RA incluye checkbox para selección **Y** puedo ver la lista completa de RA antes de aplicar filtro **Y** el campo de búsqueda "Buscar por código o descripción..." permanece visible y funcional **Y** puedo comenzar a filtrar por tipo cuando lo necesite para acotar la búsqueda.

---

### **Escenario 2 – Filtrar RA por tipo "Conocimientos"**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la lista completa de RA de la carrera **Y** el dropdown "Tipo de Aprendizaje" está visible,  
**cuando** hago clic en el dropdown "Tipo de Aprendizaje" **Y** selecciono la opción "Conocimientos",  
**entonces** el dropdown se cierra mostrando "Conocimientos" como valor seleccionado **Y** la tabla se actualiza automáticamente mostrando únicamente los RA que pertenecen al tipo "Conocimientos" **Y** se ocultan todos los RA de tipo "Destrezas" y "Valores y actitudes" **Y** cada RA filtrado mantiene su estructura completa con código, descripción y checkbox **Y** puedo seleccionar RA de tipo Conocimientos mediante sus checkboxes **Y** la funcionalidad de búsqueda por código/descripción sigue disponible y se combina con este filtro **Y** puedo cambiar a otro tipo o quitar el filtro haciendo clic nuevamente en el dropdown **Y** la paginación se actualiza según la cantidad de RA de tipo Conocimientos **Y** he acotado exitosamente la búsqueda a RA de conocimientos para el proceso de vinculación.

---

### **Escenario 3 – Filtrar RA por tipo "Destrezas"**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la lista de RA de la carrera (puede estar sin filtrar o con otro filtro aplicado),  
**cuando** hago clic en el dropdown "Tipo de Aprendizaje" **Y** selecciono la opción "Destrezas",  
**entonces** el dropdown se cierra mostrando "Destrezas" como valor seleccionado **Y** la tabla se actualiza automáticamente mostrando únicamente los RA que pertenecen al tipo "Destrezas" **Y** se ocultan todos los RA de tipo "Conocimientos" y "Valores y actitudes" **Y** cada RA filtrado mantiene su estructura completa con código, descripción y checkbox **Y** puedo seleccionar RA de tipo Destrezas mediante sus checkboxes **Y** la funcionalidad de búsqueda por código/descripción sigue disponible y se combina con este filtro **Y** si previamente había otro filtro aplicado, se reemplaza por el nuevo filtro **Y** puedo cambiar a otro tipo o quitar el filtro para ver todos los RA **Y** la paginación se actualiza según la cantidad de RA de tipo Destrezas **Y** he acotado exitosamente la búsqueda a RA de destrezas para el proceso de vinculación.

---

### **Escenario 4 – Filtrar RA por tipo "Valores y actitudes"**

**Dado que** estoy en el Paso 2 del wizard "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la lista de RA de la carrera,  
**cuando** hago clic en el dropdown "Tipo de Aprendizaje" **Y** selecciono la opción "Valores y actitudes",  
**entonces** el dropdown se cierra mostrando "Valores y actitudes" como valor seleccionado **Y** la tabla se actualiza automáticamente mostrando únicamente los RA que pertenecen al tipo "Valores y actitudes" **Y** se ocultan todos los RA de tipo "Conocimientos" y "Destrezas" **Y** cada RA filtrado mantiene su estructura completa con código, descripción y checkbox **Y** puedo seleccionar RA de este tipo mediante sus checkboxes **Y** la funcionalidad de búsqueda por código/descripción sigue disponible y se combina con este filtro **Y** puedo cambiar a otro tipo o quitar el filtro seleccionando otra opción del dropdown **Y** la paginación se actualiza según la cantidad de RA de tipo Valores y actitudes **Y** he acotado exitosamente la búsqueda a RA de valores y actitudes para el proceso de vinculación.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 2 – Filtrar RA por tipo "Conocimientos"**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento directo del objetivo de la Historia de Usuario:** La HU establece "Quiero filtrar los resultados de aprendizaje por tipo para acotar la búsqueda de RAs en el proceso de vinculación". El Escenario 2 es el primero que valida completamente esta funcionalidad de filtrado, y "Conocimientos" es típicamente el tipo más común en carreras académicas.

2. **Happy path de la funcionalidad de filtrado:** Representa el caso de uso principal donde el filtro cumple su propósito: reducir significativamente la lista de RA a un subconjunto manejable basado en el tipo de aprendizaje. Esta es la acción que más valor aporta al coordinador durante la vinculación.

3. **Tipo más frecuente en estructuras curriculares:** En la mayoría de carreras académicas, los RA de tipo "Conocimientos" son los más numerosos (típicamente 40-50% de todos los RA). Por tanto, este filtro será el más usado en la práctica diaria por los coordinadores.

4. **Impacto crítico en eficiencia del proceso de vinculación:** En carreras con 30-50+ RA totales distribuidos en tres tipos:
   - **Con filtro por tipo exitoso:** Reduce lista de 50 RA a ~15-20 RA de un tipo específico, facilitando selección
   - **Sin filtro por tipo:** Debe navegar por lista completa mezclando conocimientos, destrezas y valores, proceso confuso y propenso a errores

5. **Validación de lógica de filtrado fundamental:** Este escenario valida múltiples aspectos críticos:
   - Actualización dinámica de la tabla al seleccionar tipo
   - Ocultación correcta de RA de otros tipos
   - Persistencia de checkboxes y funcionalidad de selección
   - Combinación correcta con búsqueda por código/descripción
   - Actualización de paginación según resultados filtrados

6. **Alineación con taxonomías de aprendizaje académico:** El filtrado por tipo está alineado con marcos educativos como la taxonomía de Bloom y criterios EUR-ACE que categorizan competencias por:
   - **Conocimientos:** Qué debe saber el estudiante
   - **Destrezas:** Qué debe saber hacer el estudiante
   - **Valores y actitudes:** Qué debe valorar y cómo debe comportarse
   
   Esta clasificación es fundamental para acreditación y diseño curricular balanceado.

7. **Crítico para análisis curricular estratégico:** Los coordinadores usan el filtro por tipo para:
   - Verificar balance entre conocimientos, destrezas y valores en vinculaciones
   - Asegurar que asignaturas no solo transmiten conocimientos sino también desarrollan habilidades
   - Identificar gaps en desarrollo de competencias específicas
   - Preparar reportes de acreditación categorizados por tipo de aprendizaje
   - Validar que el perfil de egreso cubre las tres dimensiones del aprendizaje

8. **Caso de uso inicial en flujo de vinculación:** Cuando un coordinador inicia vinculación para una asignatura:
   - Frecuentemente empieza filtrando por tipo para enfocarse (ej: "primero vincularé conocimientos")
   - Trabaja sistemáticamente tipo por tipo para asegurar cobertura completa
   - Usa el filtro como herramienta organizativa para proceso estructurado
   - Reduce carga cognitiva al trabajar con subconjuntos homogéneos de RA

9. **Integración con otras funcionalidades clave:** Este escenario valida que el filtro:
   - Se combina correctamente con búsqueda por código/descripción (filtros acumulativos)
   - No interfiere con selección múltiple mediante checkboxes
   - Mantiene selecciones previas al cambiar de filtro
   - Actualiza correctamente la paginación
   - No bloquea avance al Paso 3 del wizard

Los escenarios 3 y 4 (Destrezas y Valores/actitudes) son igualmente importantes para validar todas las opciones del dropdown, pero el Escenario 2 es el más representativo porque:
- "Conocimientos" es el tipo más común en la práctica
- Valida la lógica completa de filtrado que aplica igual a otros tipos
- Es el primer filtro que típicamente se usa en el flujo

El Escenario 1 (sin filtro) es el estado inicial pero no demuestra el valor de la funcionalidad.

Un fallo en el filtrado por tipo forzaría a los coordinadores a navegar manualmente por listas largas y heterogéneas de RA, mezclando conocimientos con destrezas y valores, incrementando dramáticamente la complejidad cognitiva del proceso de vinculación y aumentando la probabilidad de omitir RA relevantes o vincular incorrectamente.

Por tanto, debe ser validado con máxima prioridad en las pruebas de aceptación, con especial énfasis en la actualización correcta de la tabla, persistencia de selecciones, y combinación con búsqueda por código/descripción.