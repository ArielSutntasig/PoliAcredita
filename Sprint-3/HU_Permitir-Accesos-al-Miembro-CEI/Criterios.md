# **CRITERIOS DE ACEPTACIÓN - HU: Permitir Accesos al Miembro CEI**

---

## **1. Análisis de Tabla de Decisión**

### **Lista de Condiciones y Acciones**

#### **CONDICIONES (derivadas de la HU y análisis de imágenes de Login 1-3):**

**NOTA IMPORTANTE:** Las imágenes proporcionadas muestran el flujo de login con la opción "Cómite Evaluación Interna (CEI)" disponible en el dropdown de roles (imagen 2), pero NO incluyen capturas del sistema navegado por un usuario CEI. Por tanto, inferiré los accesos basándome en la estructura de menú observada en los roles Profesor y Coordinador, y en los requisitos explícitos de la HU.

**C1:** Usuario selecciona rol "Cómite Evaluación Interna (CEI)" en el login  
**C2:** Credenciales válidas (correo y contraseña correctos)  
**C3:** Usuario intenta acceder a sección "CARRERA" (OP, RA, Asignaturas)  
**C4:** Usuario intenta acceder a sección "ACREDITACIÓN" (Criterios EUR-ACE)  
**C5:** Usuario intenta acceder a sección "MATRICES" (OP vs RA, CE vs RA, RAA vs RA)

#### **ACCIONES DEL SISTEMA:**

**A1:** Autenticar usuario exitosamente con rol CEI  
**A2:** Redirigir a la interfaz principal del sistema  
**A3:** Mostrar menú lateral con secciones disponibles según permisos CEI  
**A4:** Mostrar indicador de rol "Comité de Evaluación Interna (CEI)" o "Cómite Evaluación Interna (CEI)" en header  
**A5:** Permitir acceso de lectura a sección CARRERA (visualizar OP, RA, Asignaturas)  
**A6:** Permitir acceso de lectura a sección ACREDITACIÓN (visualizar Criterios EUR-ACE)  
**A7:** Permitir acceso de lectura a sección MATRICES (visualizar OP vs RA, CE vs RA, RAA vs RA)  
**A8:** Permitir acceso de lectura a sección REPORTES (visualizar Asignaturas vs CE, OP vs RA vs Asignatura)  
**A9:** Denegar operaciones de creación/edición/eliminación (solo modo lectura para evaluación)

---

### **Tabla de Decisión Completa (Maximizada)**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** | **R6** | **R7** | **R8** | **R9** | **R10** | **R11** | **R12** | **R13** | **R14** | **R15** | **R16** |
|-----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|---------|---------|---------|---------|
| **C1: Rol CEI seleccionado** | F | F | F | F | F | F | F | F | V | V | V | V | V | V | V | V |
| **C2: Credenciales válidas** | F | F | F | F | V | V | V | V | F | F | F | F | V | V | V | V |
| **C3: Acceso a CARRERA** | F | F | V | V | F | F | V | V | F | F | V | V | F | F | V | V |
| **C4: Acceso a ACREDITACIÓN** | F | V | F | V | F | V | F | V | F | V | F | V | F | V | F | V |
| **ACCIONES** |
| A1-A4: Login exitoso y mostrar interfaz | - | - | - | - | - | - | - | - | - | - | - | - | X | X | X | X |
| A5: Permitir acceso a CARRERA | - | - | - | - | - | - | - | - | - | - | - | - | - | - | X | X |
| A6: Permitir acceso a ACREDITACIÓN | - | - | - | - | - | - | - | - | - | - | - | - | - | X | - | X |
| Denegar acceso (login fallido) | X | X | X | X | X | X | X | X | X | X | X | X | - | - | - | - |

**Nota:** Esta tabla se simplificará drásticamente porque las condiciones C3, C4, C5 no son independientes del login exitoso.

---

### **Tabla de Decisión Minimizada**

| **Regla** | **R1** | **R2** | **R3** | **R4** | **R5** |
|-----------|--------|--------|--------|--------|--------|
| **C1: Rol CEI seleccionado** | F | V | V | V | V |
| **C2: Credenciales válidas** | - | F | V | V | V |
| **C3: Acceso a CARRERA solicitado** | - | - | F | V | - |
| **C4: Acceso a ACREDITACIÓN solicitado** | - | - | F | - | V |
| **ACCIONES** |
| A1-A4: Login exitoso con rol CEI | - | - | X | X | X |
| A5: Permitir visualizar información CARRERA | - | - | - | X | - |
| A6: Permitir visualizar información ACREDITACIÓN | - | - | - | - | X |
| A7: Permitir visualizar MATRICES | - | - | X | X | X |
| A8: Permitir visualizar REPORTES | - | - | X | X | X |
| A9: Modo solo lectura (no edición) | - | - | X | X | X |
| Denegar acceso | X | X | - | - | - |

**Justificación de minimización:**

- **R1:** Usuario no selecciona rol CEI o selecciona otro rol - fuera del alcance de esta HU.
- **R2:** Usuario selecciona CEI pero credenciales inválidas - denegar acceso (caso de error de autenticación).
- **R3:** Usuario CEI autenticado - puede acceder al sistema con permisos de lectura en todas las secciones.
- **R4:** Usuario CEI accede específicamente a sección CARRERA - debe poder visualizar OP, RA, Asignaturas.
- **R5:** Usuario CEI accede específicamente a sección ACREDITACIÓN - debe poder visualizar Criterios EUR-ACE.

**Simplificación adicional:** Las matrices y reportes son accesibles por defecto una vez autenticado como CEI según la HU ("visualizar información de carrera, matrices, Acreditación").

---

### **Número Total de Criterios de Aceptación**

**Total de reglas en tabla minimizada significativas:** 4 reglas (excluyendo R1 y R2 que son casos de error/fuera de alcance)

**Análisis de agrupación:** Dado que la HU menciona explícitamente tres áreas de acceso (carrera, matrices, acreditación), estructuraré los AC de la siguiente manera:

**Criterios de Aceptación finales:** **5 AC**

1. **AC1:** Login exitoso con rol CEI
2. **AC2:** Acceso a información de CARRERA (OP, RA, Asignaturas)
3. **AC3:** Acceso a información de ACREDITACIÓN (Criterios EUR-ACE)
4. **AC4:** Acceso a MATRICES (OP vs RA, CE vs RA, RAA vs RA)
5. **AC5:** Acceso a REPORTES (modo lectura para evaluación)

No se detectaron AC redundantes. Cada uno valida un área específica de acceso necesaria para el objetivo "evaluar la acreditación".

---

## **2. Lista de Criterios de Aceptación (Formato Gherkin)**

### **Escenario 1 – Autenticación exitosa con rol CEI**

**Dado que** estoy en la pantalla "Iniciar Sesión" de Poliacredita **Y** tengo credenciales válidas de un miembro del Comité de Evaluación Interna,  
**cuando** ingreso mi correo institucional (ej: "julio.sandobalin@epn.edu.ec") **Y** ingreso mi contraseña **Y** hago clic en el dropdown "Rol" **Y** selecciono la opción "Cómite Evaluación Interna (CEI)" de la lista **Y** hago clic en el botón "Iniciar Sesión",  
**entonces** el sistema autentica mis credenciales exitosamente **Y** se cierra la pantalla de login **Y** se redirige a la interfaz principal del sistema **Y** se muestra el header con el logo POLIACREDITA **Y** se visualiza el indicador de mi rol como "Cómite Evaluación Interna (CEI)" o variante similar en la parte superior **Y** se muestra el menú lateral con las secciones disponibles según mis permisos de evaluador **Y** se visualizan los iconos de configuración y salir en el header **Y** tengo acceso completo al sistema con permisos de lectura para evaluación de acreditación.

---

### **Escenario 2 – Acceder a información de CARRERA para evaluación**

**Dado que** he iniciado sesión exitosamente con el rol "Cómite Evaluación Interna (CEI)" **Y** estoy en la interfaz principal del sistema,  
**cuando** accedo al menú lateral en la sección "CARRERA",  
**entonces** puedo visualizar la opción "Objetivos de carrera (OP)" **Y** puedo hacer clic en "Objetivos de carrera (OP)" para ver los objetivos definidos de la carrera **Y** puedo visualizar la opción "Resultados de aprendizaje (RA)" **Y** puedo hacer clic en "Resultados de aprendizaje (RA)" para revisar los RA de la carrera **Y** puedo visualizar la opción "Asignaturas" **Y** puedo hacer clic en "Asignaturas" para consultar el listado de asignaturas del plan de estudios **Y** obtengo acceso de lectura a toda la información académica de la carrera **Y** puedo navegar libremente por estas secciones para evaluar la estructura curricular **Y** el sistema NO permite operaciones de creación, edición o eliminación desde mi rol **Y** todas las vistas están en modo lectura para evaluación.

---

### **Escenario 3 – Acceder a información de ACREDITACIÓN para evaluación**

**Dado que** he iniciado sesión exitosamente con el rol "Cómite Evaluación Interna (CEI)" **Y** estoy en la interfaz principal del sistema,  
**cuando** accedo al menú lateral en la sección "ACREDITACIÓN",  
**entonces** puedo visualizar la opción "Criterios EUR-ACE (CE)" **Y** puedo hacer clic en "Criterios EUR-ACE (CE)" para acceder a la información de criterios de acreditación **Y** puedo revisar los criterios EUR-ACE definidos para la carrera **Y** puedo consultar cómo se están cumpliendo los estándares de acreditación **Y** obtengo acceso de lectura a toda la información relacionada con criterios de acreditación europea **Y** el sistema NO permite modificar los criterios desde mi rol **Y** la vista está en modo lectura para evaluación y auditoría de cumplimiento.

---

### **Escenario 4 – Acceder a MATRICES para evaluación de trazabilidad**

**Dado que** he iniciado sesión exitosamente con el rol "Cómite Evaluación Interna (CEI)" **Y** estoy en la interfaz principal del sistema,  
**cuando** accedo al menú lateral en la sección "MATRICES",  
**entonces** puedo visualizar la opción "OP vs RA" **Y** puedo hacer clic en "OP vs RA" para ver la matriz de relación entre Objetivos de Programa y Resultados de Aprendizaje **Y** puedo visualizar la opción "CE vs RA" **Y** puedo hacer clic en "CE vs RA" para ver la matriz de relación entre Criterios EUR-ACE y Resultados de Aprendizaje **Y** puedo visualizar la opción "RAA vs RA" **Y** puedo hacer clic en "RAA vs RA" para ver las matrices de relación entre Resultados de Aprendizaje de Asignaturas y Resultados de Aprendizaje de carrera **Y** obtengo acceso de lectura a todas las matrices de trazabilidad académica **Y** puedo analizar visualmente cómo se relacionan los diferentes componentes del plan de estudios **Y** el sistema NO permite crear, editar o eliminar relaciones desde mi rol **Y** todas las matrices están disponibles en modo lectura para evaluación de coherencia curricular y cumplimiento de acreditación.

---

### **Escenario 5 – Acceder a REPORTES para evaluación integral**

**Dado que** he iniciado sesión exitosamente con el rol "Cómite Evaluación Interna (CEI)" **Y** estoy en la interfaz principal del sistema,  
**cuando** accedo al menú lateral en la sección "REPORTES",  
**entonces** puedo visualizar la opción "Asignaturas vs CE" **Y** puedo hacer clic en "Asignaturas vs CE" para ver el reporte de relaciones entre Asignaturas y Criterios EUR-ACE **Y** puedo visualizar la opción "OP vs RA vs Asignatura" **Y** puedo hacer clic en "OP vs RA vs Asignatura" para ver el reporte completo de trazabilidad desde objetivos hasta asignaturas **Y** obtengo acceso de lectura a todos los reportes consolidados del sistema **Y** puedo generar vistas analíticas para evaluar el cumplimiento integral de la acreditación **Y** puedo exportar reportes cuando el sistema lo permita (si existe botón "Exportar") **Y** el sistema NO permite modificar datos desde los reportes **Y** todas las vistas de reportes están en modo lectura para facilitar la evaluación académica y la preparación de informes de acreditación.

---

## **3. Análisis de Criticidad**

### **Criterio Más Crítico:** 

**Escenario 1 – Autenticación exitosa con rol CEI**

### **Justificación:**

Este criterio es el más crítico por las siguientes razones fundamentales:

1. **Prerequisito absoluto para todos los demás escenarios:** Sin autenticación exitosa con el rol CEI, ninguno de los otros criterios de aceptación puede ejecutarse. Es la puerta de entrada obligatoria que habilita todas las funcionalidades de evaluación descritas en la HU.

2. **Validación de control de acceso basado en roles (RBAC):** Este escenario valida que el sistema implementa correctamente la separación de roles. Un error aquí podría significar:
   - Usuarios no autorizados accediendo como CEI
   - Miembros CEI sin poder acceder al sistema
   - Asignación incorrecta de permisos de evaluación
   - Comprometer la seguridad e integridad de la evaluación de acreditación

3. **Cumplimiento del objetivo principal de la HU:** La HU comienza con "Como miembro de la CEI quiero visualizar...". Si el login como CEI no funciona, el valor completo de la historia se pierde, ya que el usuario no puede ejercer su rol de evaluador.

4. **Evidencia directa en el prototipo:** Las imágenes 1-3 del login muestran explícitamente la opción "Cómite Evaluación Interna (CEI)" en el dropdown de roles, confirmando que esta es una funcionalidad diseñada y esperada en el sistema.

5. **Impacto en proceso crítico de negocio:** El Comité de Evaluación Interna es responsable de procesos de acreditación académica, que son críticos para la institución. Un fallo en el acceso podría:
   - Retrasar evaluaciones de acreditación
   - Impedir auditorías internas
   - Bloquear la preparación de informes para agencias acreditadoras (EUR-ACE)
   - Afectar la certificación de calidad de programas académicos

6. **Mayor riesgo de seguridad:** Como rol de evaluación/auditoría, el CEI tiene permisos de lectura amplios sobre información académica sensible. La autenticación correcta es crítica para asegurar que solo personal autorizado del comité pueda acceder a esta información.

Los escenarios 2-5 son importantes para validar los permisos específicos de cada sección, pero todos dependen del éxito del Escenario 1. Sin autenticación exitosa como miembro CEI, el resto de las funcionalidades son inaccesibles. Por tanto, el Escenario 1 debe ser validado con máxima prioridad y rigurosidad en las pruebas de aceptación, incluyendo casos de seguridad como intentos de acceso no autorizado y validación de credenciales.