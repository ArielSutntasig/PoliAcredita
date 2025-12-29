# HU: Permitir Accesos al Miembro CEI

## Plan de Pruebas

| Campo | Detalle |
|-------|---------|
| **Fecha Ejecución** | 23-10-2025 |
| **Modo Ejecución** | Manual |
| **Prioridad Testing** | Alta |
| **Módulo** | Gestión de Usuarios y Permisos |
| **Rol** | Administrador / Miembro CEI |

---

## Escenario 1: Acceso exitoso como Miembro CEI

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Baja |
| **Nombre Testing** | CP_Acceso_Exitoso_Miembro_CEI |
| **Pre-Condiciones** | El usuario tiene cuenta activa con rol de Miembro CEI |
| **Descripción Caso** | Verificar que un usuario con rol Miembro CEI puede acceder correctamente al sistema |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | El usuario debe estar registrado con el rol correspondiente |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Acceder a la página de inicio de sesión |
| 2 | Ingresar credenciales válidas de Miembro CEI |
| 3 | Hacer clic en "Iniciar Sesión" |
| 4 | Esperar la carga del dashboard |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema permite el acceso y muestra el dashboard correspondiente al rol Miembro CEI. Se muestran únicamente las opciones de menú permitidas para este rol |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 2: Verificar menú disponible para Miembro CEI

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Verificar_Menú_Miembro_CEI |
| **Pre-Condiciones** | El usuario Miembro CEI ha iniciado sesión exitosamente |
| **Descripción Caso** | Verificar que el menú muestra solo las opciones permitidas para el rol Miembro CEI |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Los permisos deben estar correctamente configurados |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Iniciar sesión como Miembro CEI |
| 2 | Observar las opciones del menú lateral |
| 3 | Verificar cada opción disponible |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El menú muestra únicamente las opciones correspondientes al rol Miembro CEI. Las opciones restringidas no están visibles. Las opciones disponibles son funcionales |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 3: Intentar acceder a módulos restringidos

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Acceso_Módulos_Restringidos_CEI |
| **Pre-Condiciones** | El usuario Miembro CEI ha iniciado sesión |
| **Descripción Caso** | Verificar que el sistema impide el acceso a módulos no permitidos para Miembro CEI |
| **Tipo de Caso** | Negativo |
| **Tipo de Prueba** | Funcional / Seguridad |
| **Restricciones** | Ninguna |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Iniciar sesión como Miembro CEI |
| 2 | Intentar acceder vía URL directa a un módulo restringido |
| 3 | Observar la respuesta del sistema |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema deniega el acceso y muestra un mensaje de error o redirige a una página permitida. No se expone información de módulos restringidos |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |

---

## Escenario 4: Visualizar reportes permitidos para Miembro CEI

| Campo | Detalle |
|-------|---------|
| **Complejidad** | Media |
| **Nombre Testing** | CP_Visualizar_Reportes_Miembro_CEI |
| **Pre-Condiciones** | El usuario Miembro CEI ha iniciado sesión. Existen reportes disponibles |
| **Descripción Caso** | Verificar que el Miembro CEI puede visualizar los reportes permitidos para su rol |
| **Tipo de Caso** | Positivo |
| **Tipo de Prueba** | Funcional |
| **Restricciones** | Deben existir reportes generados |

### Pasos

| Paso | Acción |
|------|--------|
| 1 | Iniciar sesión como Miembro CEI |
| 2 | Acceder a la sección de reportes |
| 3 | Seleccionar un reporte disponible |
| 4 | Visualizar el contenido del reporte |

### Resultados

| Tipo | Descripción |
|------|-------------|
| **Esperado** | El sistema muestra los reportes permitidos para el rol. El contenido del reporte es correcto y completo. Se pueden exportar o imprimir si la funcionalidad está disponible |
| **Obtenido** | ESTADO PRUEBA |
| **Observaciones** | - |
