# **CRITERIOS DE ACEPTACIÓN - HU: Vincular RAA con RA (Coordinador)**

---

## **DIFERENCIA IMPORTANTE DEL ROL**

Esta HU es funcionalmente similar a la analizada en el documento 2, pero con una diferencia crítica:
- **Documento 2:** Rol Profesor (accede desde contexto de SU asignatura)
- **Documento 20:** Rol Coordinador (debe buscar y seleccionar CUALQUIER asignatura primero)

El Coordinador tiene un flujo con pasos adicionales que son prerequisitos.

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y flujo del Coordinador):**

**C0:** Materia seleccionada desde búsqueda (prerequisito del Coordinador)  
**C1:** Al menos un RAA seleccionado en Paso 1  
**C2:** Al menos un RA seleccionado en Paso 2  
**C3:** Nivel de aporte seleccionado en dropdown "Nivel de Aporte" (Paso 3)  
**C4:** Justificación escrita en textarea "Justifique la relación de RAA vs RA:" (Paso 3)

**Nota:** El Coordinador PRIMERO debe buscar y seleccionar una asignatura, LUEGO inicia el wizard de vinculación.

#### **ACCIONES DEL SISTEMA:**

**A0:** Permitir búsqueda y selección de materia  
**A1:** Abrir wizard de vinculación para la materia seleccionada  
**A2:** Mostrar Paso 1 con RAA de la materia seleccionada  
**A3:** Mantener botón "Guardar" deshabilitado (gris) en Paso 1  
**A4:** Habilitar botón "Guardar" (azul) en Paso 1  
**A5:** Avanzar al Paso 2 del wizard  
**A6:** Mostrar RA de la carrera para selección  
**A7:** Habilitar botón "Guardar" (azul) en Paso 2  
**A8:** Avanzar al Paso 3 del wizard  
**A9:** Mostrar elementos seleccionados en sección "Elementos Seleccionado:"  
**A10:** Habilitar botón "Guardar" (azul) final  
**A11:** Crear relación RAA-RA en base de datos  
**A12:** Actualizar matriz visual de la materia seleccionada  
**A13:** Mostrar tooltip "Se agregó la relación correctamente"  
**A14:** Cerrar wizard y volver a matriz de la asignatura

---

### **Tabla de Decisión Completa (Maximizada)**

Por simplicidad, presento versión enfocada en las condiciones clave del wizard (C1-C4), asumiendo C0 ya cumplida:

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|
| **C0: Materia seleccionada** | V | V | V | V | V | V | V | V |
| **C1: RAA seleccionado** | F | F | F | F | V | V | V | V |
| **C2: RA seleccionado** | F | F | V | V | F | F | V | V |
| **C3: Nivel aporte seleccionado** | F | V | F | V | F | V | F | V |
| **C4: Justificación escrita** | F | F | F | F | F | F | F | V |
| **ACCIONES** |
| A2-A3: Paso 1 deshabilitado | X | X | X | X | - | - | - | - |
| A4-A5: Avanzar Paso 2 | - | - | - | - | X | X | X | X |
| A7-A8: Avanzar Paso 3 | - | - | - | - | - | - | X | X |
| A10-A14: Crear vinculación | - | - | - | - | - | - | - | X |

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R0** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** |
|-----------|--------|--------|--------|--------|--------|--------|--------|
| **C0: Materia seleccionada (prerequisito Coordinador)** | F | V | V | V | V | V | V |
| **C1: RAA seleccionado Paso 1** | - | F | V | V | V | V | V |
| **C2: RA seleccionado Paso 2** | - | - | F | V | V | V | V |
| **C3: Nivel aporte seleccionado** | - | - | - | F | V | V | V |
| **C4: Justificación escrita** | - | - | - | - | F | V | V |
| **ACCIONES** |
| A0: Búsqueda y selección materia | X | X | X | X | X | X | X |
| A1-A2: Abrir wizard Paso 1 | - | X | X | X | X | X | X |
| A3: Botón deshabilitado Paso 1 | - | X | - | - | - | - | - |
| A4-A5: Avanzar Paso 2 | - | - | X | X | X | X | X |
| A6: Botón deshabilitado Paso 2 | - | - | X | - | - | - | - |
| A7-A8: Avanzar Paso 3 | - | - | - | X | X | X | X |
| A9: Mostrar elementos seleccionados | - | - | - | X | X | X | X |
| A10: Botón deshabilitado Paso 3 | - | - | - | X | X | - | - |
| A11-A14: Crear vinculación completa | - | - | - | - | - | - | X |

**Justificación de minimización:**

- **R0:** Sin materia seleccionada - Coordinador debe primero buscar y seleccionar asignatura
- **R1-R6:** Similares a flujo del Profesor pero iniciado desde contexto de materia seleccionada por Coordinador

---

### **Número Total de Criterios de Aceptación**

**Total de reglas significativas:** 7 reglas

**Criterios de Aceptación finales:** **7 AC**

1. **AC1:** Buscar y seleccionar materia como prerequisito (específico del Coordinador)
2. **AC2:** Acceder al wizard desde matriz de materia seleccionada
3. **AC3:** Seleccionar RAA y avanzar al Paso 2
4. **AC4:** Seleccionar RA y avanzar al Paso 3
5. **AC5:** Intentar guardar con nivel pero sin justificación
6. **AC6:** Intentar guardar con justificación pero sin nivel
7. **AC7:** Vincular RAA con RA exitosamente (happy path)

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Buscar y seleccionar materia como prerequisito**

**Dado que** soy un coordinador de carrera **Y** estoy en la vista "Matriz: RAA vs RA",  
**cuando** accedo a la sección "Seleccione una materia:" **Y** escribo en el campo de búsqueda (ej: "Ingeniería de") **Y** selecciono una asignatura específica del dropdown de sugerencias (ej: "Ingeniería de Software y Requerimientos"),  
**entonces** el sistema carga la matriz RAA vs RA de la asignatura seleccionada **Y** se muestra la matriz con los RAA de la asignatura y los RA de la carrera **Y** se visualiza el botón "+ Nueva Relación" en la esquina superior derecha **Y** puedo hacer clic en "+ Nueva Relación" para iniciar el proceso de vinculación **Y** he completado el prerequisito específico del Coordinador de seleccionar la asignatura con la que trabajaré.

---

### **Escenario 2 – Acceder al wizard de vinculación desde matriz**

**Dado que** soy un coordinador de carrera **Y** he seleccionado una asignatura específica **Y** estoy visualizando su matriz RAA vs RA,  
**cuando** hago clic en el botón "+ Nueva Relación",  
**entonces** se abre el wizard "Matriz: Resultados de aprendizaje de Asignatura (RAA) y Resultados de aprendizaje (RA)" **Y** se muestra el Paso 1 activo con círculo azul "Seleccionar Resultados de Aprendizaje de Asignatura (RAA)" **Y** se presentan los RAA de la asignatura seleccionada en una tabla **Y** el botón "Guardar" está deshabilitado en gris **Y** puedo comenzar el proceso de vinculación seleccionando RAA de la asignatura que previamente elegí.

---

### **Escenario 3 – Seleccionar RAA y avanzar al Paso 2**

**Dado que** estoy en el Paso 1 del wizard de vinculación **Y** veo los RAA de la asignatura seleccionada,  
**cuando** selecciono al menos un RAA mediante su checkbox,  
**entonces** el botón "Guardar" cambia de gris deshabilitado a azul habilitado **Y** hago clic en "Guardar" para avanzar **Y** el sistema avanza al Paso 2 **Y** el círculo del Paso 2 se activa en azul con texto "Seleccionar Resultados de Aprendizaje (RA)" **Y** se muestra la tabla con TODOS los RA de la carrera **Y** el botón "Guardar" está deshabilitado hasta que seleccione un RA.

---

### **Escenario 4 – Seleccionar RA y avanzar al Paso 3**

**Dado que** estoy en el Paso 2 del wizard **Y** veo los RA de la carrera,  
**cuando** selecciono al menos un RA mediante su checkbox,  
**entonces** el botón "Guardar" cambia a azul habilitado **Y** hago clic en "Guardar" para avanzar **Y** el sistema avanza al Paso 3 **Y** el círculo del Paso 3 se activa en azul con texto "Justificar Relación" **Y** se muestra la sección "Elementos Seleccionado:" con el RAA y el RA elegidos **Y** se visualiza el dropdown "Seleccione el nivel de aporte:" **Y** se muestra el textarea "Justifique la relación de RAA vs RA:" **Y** el botón "Guardar" está deshabilitado hasta completar nivel y justificación.

---

### **Escenario 5 – Intentar guardar con nivel seleccionado pero sin justificación**

**Dado que** estoy en el Paso 3 del wizard **Y** he seleccionado un nivel de aporte (ej: "Alto"),  
**cuando** intento guardar sin escribir justificación en el textarea,  
**entonces** el botón "Guardar" permanece deshabilitado en gris **Y** no puedo completar la vinculación **Y** debo escribir una justificación para continuar.

---

### **Escenario 6 – Intentar guardar con justificación pero sin nivel**

**Dado que** estoy en el Paso 3 del wizard **Y** he escrito una justificación en el textarea,  
**cuando** intento guardar sin seleccionar nivel de aporte en el dropdown,  
**entonces** el botón "Guardar" permanece deshabilitado en gris **Y** no puedo completar la vinculación **Y** debo seleccionar un nivel de aporte para continuar.

---

### **Escenario 7 – Vincular RAA con RA exitosamente como Coordinador**

**Dado que** soy un coordinador de carrera **Y** he seleccionado una asignatura (ej: "Ingeniería de Software y Requerimientos") **Y** estoy en el Paso 3 del wizard **Y** tengo RAA y RA seleccionados **Y** he seleccionado nivel de aporte (ej: "Alto") **Y** he escrito justificación,  
**cuando** hago clic en el botón "Guardar" azul habilitado,  
**entonces** se crea la relación entre el RAA de la asignatura seleccionada y el RA de la carrera **Y** se cierra el wizard automáticamente **Y** vuelvo a la vista de matriz RAA vs RA de la asignatura que seleccioné **Y** la matriz se actualiza con una nueva celda verde con checkmark (✓) en la intersección correspondiente **Y** se muestra tooltip azul con título "Información" **Y** el tooltip muestra "Se agregó la relación correctamente" **Y** puedo visualizar la nueva vinculación en la matriz de la asignatura **Y** he establecido exitosamente cómo la asignatura seleccionada contribuye a las competencias globales de la carrera **Y** puedo continuar vinculando más RAA o seleccionar otra asignatura para analizar.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 7 – Vincular RAA con RA exitosamente como Coordinador**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Cumplimiento del objetivo específico del Coordinador:** La HU establece "Quiero vincular un Resultado de Aprendizaje de Asignatura (RAA) a un Resultado de Aprendizaje (RA) de mi carrera para entender cómo cada asignatura contribuye a las competencias globales". El Escenario 7 es el único que completa este objetivo desde la perspectiva del Coordinador, incluyendo el contexto de trabajar con asignaturas de otros profesores.

2. **Happy path completo del rol supervisor:** A diferencia del Profesor que vincula sus propias asignaturas, el Coordinador ejecuta este proceso como supervisor académico. El Escenario 7 valida el flujo completo específico del Coordinador: buscar asignatura → seleccionar → vincular → analizar contribución → supervisar trazabilidad curricular.

3. **Crítico para supervisión y gestión curricular de la carrera:** El Coordinador usa esta funcionalidad para:
   - **Supervisar vinculaciones:** Verificar que cada asignatura tiene relaciones establecidas
   - **Validar trazabilidad:** Asegurar que hay camino desde asignaturas hasta competencias de egreso
   - **Identificar gaps:** Detectar asignaturas sin vinculaciones o RA sin cobertura
   - **Análisis comparativo:** Evaluar cómo diferentes asignaturas aportan a mismos RA
   - **Preparar acreditación:** Documentar contribución completa del plan de estudios

4. **Impacto en acreditación académica EUR-ACE:** El Coordinador es responsable de demostrar ante agencias acreditadoras que:
   - Existe trazabilidad completa: Asignaturas → RAA → RA → Perfil de Egreso
   - Cada competencia prometida se desarrolla en asignaturas específicas
   - Hay justificación documentada para cada vinculación
   - El diseño curricular es coherente y completo
   
   Un fallo aquí compromete evidencia crítica de acreditación.

5. **Validación del flujo multi-rol del sistema:** Este escenario valida que:
   - El Coordinador puede trabajar con asignaturas de CUALQUIER profesor
   - La búsqueda de materia funciona correctamente como prerequisito
   - Los RAA cargados corresponden a la asignatura seleccionada (no a otra)
   - La vinculación se guarda para la asignatura correcta
   - La matriz actualizada es de la asignatura seleccionada
   
   Errores aquí podrían causar vinculaciones cruzadas entre asignaturas.

6. **Diferenciador clave del rol Coordinador vs Profesor:** Mientras el Profesor vincula para documentar su asignatura, el Coordinador vincula para:
   - Completar vinculaciones faltantes en asignaturas de otros
   - Supervisar calidad de vinculaciones existentes
   - Estandarizar niveles de aporte entre asignaturas
   - Asegurar cobertura completa de todos los RA de la carrera
   - Generar reportes de trazabilidad global

7. **Caso de uso frecuente en gestión académica:** El Coordinador ejecutará este flujo constantemente durante:
   - Auditorías internas de trazabilidad curricular
   - Preparación de auto-estudios para acreditación
   - Revisiones semestrales de coherencia curricular
   - Incorporación de nuevas asignaturas al plan de estudios
   - Actualización de vinculaciones tras cambios en RA de carrera

8. **Validación de persistencia y visualización específica:** Este escenario valida que:
   - La vinculación se guarda con la asignatura CORRECTA (la seleccionada)
   - El Coordinador vuelve a la matriz de ESA asignatura específica
   - Puede continuar trabajando con esa u otra asignatura
   - El sistema mantiene el contexto de cuál asignatura está analizando
   - No hay confusión entre matrices de diferentes asignaturas

Los escenarios 1-6 son importantes para validar prerequisitos, navegación del wizard y validaciones, pero el Escenario 7 es el que demuestra que el sistema permite al Coordinador cumplir su rol estratégico: supervisar, completar y validar que cada asignatura del plan de estudios contribuye documentadamente a las competencias globales de la carrera.

Un fallo en este escenario comprometería la capacidad del Coordinador de ejercer supervisión curricular efectiva, completar documentación de trazabilidad para acreditación, y asegurar coherencia del diseño curricular a nivel de carrera. Por tanto, debe ser validado con máxima prioridad, incluyendo verificación de que la vinculación se guarda para la asignatura correcta y no hay confusión entre asignaturas al trabajar con múltiples programas.