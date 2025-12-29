# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas:**
1. **C1:** Campo "Correo Institucional" está completo
2. **C2:** Campo "Contraseña" está completo  
3. **C3:** Dropdown "Rol" tiene una opción seleccionada
4. **C4:** Las credenciales (correo + contraseña) son válidas en el sistema
5. **C5:** El rol seleccionado está asignado al usuario autenticado

### **Acciones del Sistema:**
1. **A1:** Validar campos obligatorios y mostrar indicadores de error
2. **A2:** Habilitar/Deshabilitar botón "Iniciar Sesión"
3. **A3:** Validar credenciales contra base de datos
4. **A4:** Mostrar mensaje de error "Credenciales inválidas"
5. **A5:** Validar que el rol seleccionado pertenezca al usuario
6. **A6:** Mostrar mensaje de error "Rol no asignado"
7. **A7:** Redirigir al dashboard correspondiente al rol
8. **A8:** Mostrar mensaje de bienvenida personalizado ("Bienvenido, [Nombre]")
9. **A9:** Cargar menú y funcionalidades específicas del rol seleccionado

---

## **Tabla de Decisión Completa (Maximizada)**

Para el análisis, simplificaré a 3 condiciones principales que generan los escenarios más relevantes:

| Regla | C1: Campos completos | C2: Credenciales válidas | C3: Rol asignado | Acción |
|-------|---------------------|-------------------------|------------------|---------|
| R1 | N | - | - | A1: Mostrar error de validación |
| R2 | S | N | - | A4: Mostrar error "Credenciales inválidas" |
| R3 | S | S | N | A6: Mostrar error "Rol no asignado" |
| R4 | S | S | S | A7, A8, A9: Login exitoso + Redirección |

**Total de combinaciones teóricas:** 2^3 = 8 reglas  
**Reglas después de eliminar las lógicamente imposibles:** 4 reglas

---

## **Tabla de Decisión Minimizada**

| Regla | Campos completos | Credenciales válidas | Rol asignado | Acción |
|-------|-----------------|---------------------|--------------|---------|
| **R1** | N | - | - | Mostrar error de campos requeridos |
| **R2** | S | N | - | Mostrar error "Credenciales inválidas" |
| **R3** | S | S | N | Mostrar error "Rol no asignado al usuario" |
| **R4** | S | S | S | Autenticar y redirigir al dashboard del rol |

**Justificación de la minimización:**
- Las reglas donde los campos están incompletos hacen irrelevante la validez de credenciales o rol (se fusionan en R1)
- Si las credenciales son inválidas, no se puede validar el rol (R2)
- Solo si ambas validaciones previas son exitosas, se puede proceder al login (R4)

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 7 Criterios de Aceptación**

Basado en:
- 4 reglas de la tabla minimizada (escenarios principales)
- 3 escenarios adicionales para casos de uso específicos observados en el prototipo (validaciones individuales de campos, interacción con dropdown, funcionalidad "¿Olvidaste tu contraseña?")

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Validar campos obligatorios vacíos**

**Dado que** estoy en la pantalla "Iniciar Sesión" de Poliacredita **Y** todos los campos están vacíos,  
**cuando** intento hacer clic en el botón "Iniciar Sesión",  
**entonces** el botón permanece deshabilitado o inactivo **Y** no se ejecuta ninguna acción de autenticación **Y** se mantiene visible el formulario de inicio de sesión.

---

**Escenario 2 – Intentar login con credenciales inválidas**

**Dado que** estoy en la pantalla "Iniciar Sesión" **Y** he completado el campo "Correo Institucional" con un correo válido **Y** he completado el campo "Contraseña" **Y** he seleccionado una opción del dropdown "Rol",  
**cuando** hago clic en el botón "Iniciar Sesión" **Y** las credenciales (correo y/o contraseña) no son válidas en el sistema,  
**entonces** se muestra un mensaje de error indicando "Credenciales inválidas" o "Usuario o contraseña incorrectos" **Y** permanezco en la pantalla de inicio de sesión **Y** los campos mantienen los valores ingresados **Y** no se redirige a ningún dashboard.

---

**Escenario 3 – Intentar login con rol no asignado al usuario**

**Dado que** estoy en la pantalla "Iniciar Sesión" **Y** he ingresado credenciales válidas (ej: "julio.sandobalin@epn.edu.ec") **Y** he seleccionado un rol del dropdown "Rol" que no está asignado a mi usuario,  
**cuando** hago clic en el botón "Iniciar Sesión",  
**entonces** se muestra un mensaje de error indicando "El rol seleccionado no está asignado a este usuario" o "No tienes permisos para este rol" **Y** permanezco en la pantalla de inicio de sesión **Y** no se ejecuta la redirección al dashboard.

---

**Escenario 4 – Login exitoso con rol Administrador**

**Dado que** estoy en la pantalla "Iniciar Sesión" de Poliacredita **Y** ingreso credenciales válidas en el campo "Correo Institucional" (ej: "julio.sandobalin@epn.edu.ec") **Y** ingreso la contraseña correcta en el campo "Contraseña" **Y** selecciono "Administrador" del dropdown "Rol",  
**cuando** hago clic en el botón "Iniciar Sesión",  
**entonces** se autentica mi sesión exitosamente **Y** se redirige al dashboard del Administrador **Y** se muestra el mensaje de bienvenida "Bienvenido, Julio" en la parte superior **Y** se presenta la barra lateral izquierda con las opciones: "Dashboard", "Facultades", "Carreras", "Usuarios", "Roles", "Mi Perfil" **Y** se muestran tres tarjetas con métricas: "TOTAL FACULTADES" con valor numérico, "TOTAL CARRERAS" con valor numérico, "USUARIOS ACTIVOS" con valor numérico **Y** se presenta la sección "Acceso Rápido" con tres tarjetas: "Gestionar Carreras", "Gestionar Usuarios", "Ver Mi Perfil" **Y** se muestra la sección "Actividad Reciente" con una tabla de acciones del sistema **Y** en la esquina superior derecha aparece "Administrador" junto con iconos de configuración y logout.

---

**Escenario 5 – Desplegar y seleccionar rol del dropdown**

**Dado que** estoy en la pantalla "Iniciar Sesión" **Y** he completado los campos "Correo Institucional" y "Contraseña",  
**cuando** hago clic en el dropdown "Rol" con texto "Seleccionar un rol",  
**entonces** se despliega una lista con las opciones disponibles: "Administrador", "Coordinador de Carrera", "Cómite Evaluación Interna (CEI)", "Autoridad Académica", "Profesor" **Y** puedo seleccionar una opción de la lista **Y** el dropdown se actualiza mostrando la opción seleccionada **Y** se habilita el botón "Iniciar Sesión" si todos los campos están completos.

---

**Escenario 6 – Acceder a funcionalidad "¿Olvidaste tu contraseña?"**

**Dado que** estoy en la pantalla "Iniciar Sesión",  
**cuando** hago clic en el link "¿Olvidaste tu contraseña?" ubicado debajo del botón "Iniciar Sesión",  
**entonces** se redirige a una pantalla o modal de recuperación de contraseña **Y** se mantiene visible el contexto del sistema Poliacredita **Y** se proporciona un mecanismo para restablecer la contraseña institucional.

---

**Escenario 7 – Validar formato de correo institucional**

**Dado que** estoy en la pantalla "Iniciar Sesión" **Y** comienzo a ingresar datos en el campo "Correo Institucional",  
**cuando** ingreso un correo que no tiene el formato "@epn.edu.ec" (ej: "usuario@gmail.com"),  
**entonces** se muestra un mensaje de validación indicando "Debe ingresar un correo institucional válido" o "Formato de correo incorrecto" **Y** el botón "Iniciar Sesión" permanece deshabilitado hasta corregir el formato **Y** se señala visualmente el campo con error.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 4 – Login exitoso con rol Administrador**

### **Justificación:**

Este es el criterio más crítico porque representa el **"happy path"** principal de la Historia de Usuario y valida la funcionalidad completa del inicio de sesión exitoso. Específicamente:

1. **Valida el flujo completo end-to-end:** Desde la entrada de credenciales hasta la carga exitosa del dashboard con todas sus funcionalidades.

2. **Confirma la integración correcta:** Verifica que el sistema autentica, valida roles, y carga correctamente los módulos correspondientes al rol seleccionado.

3. **Representa el valor de negocio principal:** El propósito fundamental de la HU es permitir que usuarios accedan a sus funcionalidades según su rol. Este escenario valida ese valor directamente.

4. **Incluye verificaciones visuales concretas:** Basado en el análisis del prototipo (Imagen 4), valida elementos específicos como el mensaje de bienvenida personalizado, las métricas del dashboard, las opciones del menú lateral, y la sección de acceso rápido.

5. **Fundamento para otros escenarios:** Si este escenario falla, los demás escenarios de error pierden relevancia, ya que el flujo principal no funciona.

Los otros escenarios (validaciones de error) son importantes para la robustez del sistema, pero el Escenario 4 es el que garantiza que el sistema cumple su propósito fundamental: **permitir el acceso seguro y contextualizado de usuarios según sus roles institucionales**.