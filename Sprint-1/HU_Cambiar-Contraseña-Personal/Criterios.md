# **1. Análisis de Tabla de Decisión**

## **Lista de Condiciones y Acciones**

### **Condiciones Identificadas (del análisis de HU + Imagen 19 del prototipo):**

1. **C1:** Usuario accede a sección "Cambiar Contraseña" en Mi Perfil
2. **C2:** Usuario hace clic en botón "Actualizar Contraseña"
3. **C3:** Se abre modal/formulario de cambio de contraseña
4. **C4:** Campo "Contraseña Actual" está completo
5. **C5:** Campo "Nueva Contraseña" está completo
6. **C6:** Campo "Confirmar Nueva Contraseña" está completo
7. **C7:** Contraseña actual ingresada es correcta
8. **C8:** Nueva contraseña cumple requisitos de seguridad (longitud, complejidad)
9. **C9:** Nueva contraseña y confirmación coinciden
10. **C10:** Nueva contraseña es diferente a la contraseña actual

### **Acciones del Sistema (observadas en Imagen 19 + inferencias de seguridad):**

1. **A1:** Mostrar sección "Cambiar Contraseña" en Mi Perfil
2. **A2:** Mostrar mensaje motivacional "Mantenga su cuenta segura actualizando su contraseña regularmente"
3. **A3:** Mostrar botón "Actualizar Contraseña" en azul oscuro
4. **A4:** Abrir modal/formulario de cambio de contraseña
5. **A5:** Mostrar campos: "Contraseña Actual", "Nueva Contraseña", "Confirmar Nueva Contraseña"
6. **A6:** Mostrar requisitos de contraseña (longitud mínima, caracteres especiales, etc.)
7. **A7:** Validar contraseña actual contra base de datos
8. **A8:** Validar requisitos de seguridad de nueva contraseña
9. **A9:** Validar coincidencia entre nueva contraseña y confirmación
10. **A10:** Mostrar error "Contraseña actual incorrecta"
11. **A11:** Mostrar error "Las contraseñas no coinciden"
12. **A12:** Mostrar error "La contraseña no cumple los requisitos de seguridad"
13. **A13:** Mostrar error "La nueva contraseña debe ser diferente a la actual"
14. **A14:** Actualizar contraseña en base de datos (hash)
15. **A15:** Cerrar modal/formulario
16. **A16:** Mostrar mensaje de éxito "Contraseña actualizada exitosamente"
17. **A17:** Mantener sesión activa sin requerir nuevo login

---

## **Tabla de Decisión Completa (Maximizada)**

Considerando las 5 condiciones principales más relevantes:

**Condiciones simplificadas:**
- **C1:** Contraseña actual correcta
- **C2:** Nueva contraseña cumple requisitos
- **C3:** Contraseñas coinciden
- **C4:** Nueva contraseña diferente a actual
- **C5:** Se hace clic en "Guardar/Actualizar"

Total combinaciones teóricas: 2^5 = 32 reglas (simplificando a las más relevantes)

| Regla | C1 | C2 | C3 | C4 | C5 | Acción |
|-------|----|----|----|----|----|--------------------|
| R1 | N | - | - | - | S | A10: Error contraseña actual incorrecta |
| R2 | S | N | - | - | S | A12: Error requisitos no cumplidos |
| R3 | S | S | N | - | S | A11: Error contraseñas no coinciden |
| R4 | S | S | S | N | S | A13: Error nueva igual a actual |
| R5 | S | S | S | S | N | Esperar acción usuario |
| R6 | S | S | S | S | S | A14-A17: Actualizar exitosamente |

---

## **Tabla de Decisión Minimizada**

| Regla | Contraseña actual correcta | Nueva cumple requisitos | Contraseñas coinciden | Nueva diferente a actual | Guardar | Acción |
|-------|---------------------------|------------------------|---------------------|------------------------|---------|---------|
| **R1** | N | - | - | - | S | Error "Contraseña actual incorrecta" |
| **R2** | S | N | - | - | S | Error "Requisitos de seguridad no cumplidos" |
| **R3** | S | S | N | - | S | Error "Las contraseñas no coinciden" |
| **R4** | S | S | S | N | S | Error "Nueva contraseña debe ser diferente" |
| **R5** | S | S | S | S | N | Formulario completo, esperando acción |
| **R6** | S | S | S | S | S | Actualizar exitosamente, mostrar éxito |

**Justificación de la minimización:**
- **R1:** Si contraseña actual es incorrecta, las demás validaciones son irrelevantes
- **R2:** Si nueva contraseña no cumple requisitos de seguridad, otras validaciones no importan
- **R3:** Si las contraseñas no coinciden, no se puede proceder
- **R4:** Si la nueva contraseña es igual a la actual, no hay cambio real
- **R5:** Usuario llenó formulario correctamente pero no ha guardado
- **R6:** Happy path: todas las condiciones cumplidas, actualización exitosa

---

## **Número Total de Criterios de Aceptación Requeridos**

**Total: 10 Criterios de Aceptación**

Basado en:
- 6 reglas de la tabla minimizada (escenarios de validación)
- 4 escenarios adicionales para validar aspectos específicos:
  - Acceso a la funcionalidad desde Mi Perfil
  - Visualización de requisitos de contraseña
  - Cancelar cambio de contraseña
  - Seguridad (hash, no mostrar contraseñas en texto plano)

---

# **2. Lista de Criterios de Aceptación (Formato Gherkin)**

**Escenario 1 – Acceder a la funcionalidad de cambio de contraseña desde Mi Perfil**

**Dado que** estoy autenticado como Usuario en el sistema,  
**cuando** accedo a la sección "Mi Perfil",  
**entonces** se muestra la pantalla "Mi Perfil" con tres secciones principales **Y** en el lado derecho se presenta la sección "Cambiar Contraseña" **Y** la sección muestra el título "Cambiar Contraseña" **Y** se presenta un texto motivacional "Mantenga su cuenta segura actualizando su contraseña regularmente" **Y** se muestra un botón "Actualizar Contraseña" con fondo azul oscuro **Y** el botón es clickeable y está claramente visible.

---

**Escenario 2 – Abrir formulario de cambio de contraseña**

**Dado que** estoy en la sección "Mi Perfil" **Y** veo la sección "Cambiar Contraseña",  
**cuando** hago clic en el botón "Actualizar Contraseña",  
**entonces** se abre un modal o formulario con título "Cambiar Contraseña" o "Actualizar Contraseña" **Y** el formulario presenta tres campos de texto tipo password (ocultan caracteres): "Contraseña Actual*", "Nueva Contraseña*", "Confirmar Nueva Contraseña*" **Y** todos los campos están marcados como obligatorios con asterisco (*) **Y** se muestran requisitos de contraseña (ej: "Mínimo 8 caracteres", "Al menos una letra mayúscula", "Al menos un número", "Al menos un carácter especial") **Y** se presentan botones "Cancelar" y "Guardar" o "Actualizar" en la parte inferior del formulario **Y** todos los campos están vacíos y listos para ingreso de datos.

---

**Escenario 3 – Cambiar contraseña exitosamente**

**Dado que** estoy en el formulario de cambio de contraseña **Y** todos los campos están vacíos,  
**cuando** ingreso mi contraseña actual correcta en el campo "Contraseña Actual*" (ej: "MiPass123!") **Y** ingreso una nueva contraseña que cumple todos los requisitos de seguridad en "Nueva Contraseña*" (ej: "NuevaPass456@") **Y** ingreso exactamente la misma contraseña en "Confirmar Nueva Contraseña*" ("NuevaPass456@") **Y** la nueva contraseña es diferente a la contraseña actual **Y** hago clic en el botón "Guardar" o "Actualizar",  
**entonces** el sistema valida la contraseña actual contra la base de datos **Y** verifica que la nueva contraseña cumple los requisitos de seguridad (longitud mínima, mayúsculas, números, caracteres especiales) **Y** verifica que las contraseñas ingresadas coinciden **Y** verifica que la nueva contraseña es diferente a la actual **Y** actualiza la contraseña en la base de datos usando hash seguro **Y** cierra el modal/formulario automáticamente **Y** muestra un mensaje de notificación de éxito con ícono verde "Contraseña actualizada exitosamente" o "Su contraseña ha sido cambiada correctamente" **Y** la notificación aparece en la esquina superior derecha temporalmente **Y** mi sesión permanece activa sin requerir nuevo inicio de sesión **Y** puedo continuar usando el sistema normalmente.

---

**Escenario 4 – Intentar cambiar contraseña con contraseña actual incorrecta**

**Dado que** estoy en el formulario de cambio de contraseña,  
**cuando** ingreso una contraseña incorrecta en el campo "Contraseña Actual*" (ej: "ContraseñaErronea") **Y** ingreso datos válidos en "Nueva Contraseña*" y "Confirmar Nueva Contraseña*" **Y** hago clic en "Guardar" o "Actualizar",  
**entonces** el sistema valida la contraseña actual contra la base de datos **Y** detecta que la contraseña ingresada no coincide con la contraseña almacenada **Y** no se cierra el modal/formulario **Y** no se actualiza la contraseña en la base de datos **Y** se muestra un mensaje de error "Contraseña actual incorrecta" o "La contraseña actual no es válida" **Y** el mensaje se presenta de forma destacada cerca del campo "Contraseña Actual*" (ej: texto rojo, icono de alerta) **Y** el campo "Contraseña Actual*" se resalta visualmente como error **Y** permanezco en el formulario para corregir la contraseña actual **Y** puedo volver a intentar con la contraseña correcta.

---

**Escenario 5 – Intentar cambiar con nueva contraseña que no cumple requisitos de seguridad**

**Dado que** estoy en el formulario de cambio de contraseña,  
**cuando** ingreso mi contraseña actual correcta **Y** ingreso una nueva contraseña que NO cumple los requisitos de seguridad en "Nueva Contraseña*" (ej: "123" - muy corta, sin mayúsculas, sin caracteres especiales) **Y** ingreso la misma contraseña débil en "Confirmar Nueva Contraseña*" **Y** hago clic en "Guardar" o "Actualizar",  
**entonces** el sistema valida la nueva contraseña contra los requisitos de seguridad **Y** detecta que no cumple con los criterios establecidos **Y** no se actualiza la contraseña en la base de datos **Y** se muestra un mensaje de error "La contraseña no cumple los requisitos de seguridad" o "La contraseña debe tener al menos 8 caracteres, una mayúscula, un número y un carácter especial" **Y** el mensaje se presenta cerca del campo "Nueva Contraseña*" resaltado en rojo **Y** opcionalmente se resaltan visualmente los requisitos no cumplidos en la lista de requisitos **Y** permanezco en el formulario para ingresar una contraseña más segura.

---

**Escenario 6 – Intentar cambiar cuando las contraseñas no coinciden**

**Dado que** estoy en el formulario de cambio de contraseña,  
**cuando** ingreso mi contraseña actual correcta **Y** ingreso una nueva contraseña válida en "Nueva Contraseña*" (ej: "NuevaPass456@") **Y** ingreso una contraseña DIFERENTE en "Confirmar Nueva Contraseña*" (ej: "NuevaPass789#") **Y** hago clic en "Guardar" o "Actualizar",  
**entonces** el sistema compara ambos campos **Y** detecta que no coinciden **Y** no se actualiza la contraseña en la base de datos **Y** se muestra un mensaje de error "Las contraseñas no coinciden" o "La confirmación de contraseña no coincide" **Y** el mensaje se presenta cerca del campo "Confirmar Nueva Contraseña*" en texto rojo **Y** ambos campos de nueva contraseña pueden resaltarse visualmente como error **Y** permanezco en el formulario para corregir la confirmación.

---

**Escenario 7 – Intentar cambiar a una contraseña idéntica a la actual**

**Dado que** estoy en el formulario de cambio de contraseña,  
**cuando** ingreso mi contraseña actual correcta en "Contraseña Actual*" (ej: "MiPass123!") **Y** ingreso exactamente la MISMA contraseña en "Nueva Contraseña*" ("MiPass123!") **Y** ingreso la misma en "Confirmar Nueva Contraseña*" ("MiPass123!") **Y** hago clic en "Guardar" o "Actualizar",  
**entonces** el sistema compara la contraseña actual con la nueva **Y** detecta que son idénticas **Y** no se actualiza la contraseña en la base de datos **Y** se muestra un mensaje de error "La nueva contraseña debe ser diferente a la contraseña actual" o "Debe ingresar una contraseña diferente a la actual" **Y** el mensaje se presenta de forma destacada **Y** permanezco en el formulario para ingresar una contraseña realmente nueva.

---

**Escenario 8 – Cancelar cambio de contraseña**

**Dado que** estoy en el formulario de cambio de contraseña **Y** he ingresado información en uno o más campos,  
**cuando** hago clic en el botón "Cancelar",  
**entonces** el modal/formulario se cierra inmediatamente **Y** no se guarda ningún cambio en la base de datos **Y** la contraseña permanece sin modificaciones **Y** regreso a la vista "Mi Perfil" **Y** la sección "Cambiar Contraseña" sigue visible con el botón "Actualizar Contraseña" disponible **Y** no se muestra ningún mensaje de éxito ni error **Y** puedo volver a abrir el formulario si lo deseo.

---

**Escenario 9 – Visualizar requisitos de seguridad de contraseña**

**Dado que** estoy en el formulario de cambio de contraseña,  
**cuando** visualizo el formulario o hago foco en el campo "Nueva Contraseña*",  
**entonces** se muestra una lista clara de requisitos de contraseña (ej: en panel lateral, tooltip, o texto bajo el campo) **Y** los requisitos incluyen información como: "Mínimo 8 caracteres", "Al menos una letra mayúscula (A-Z)", "Al menos una letra minúscula (a-z)", "Al menos un número (0-9)", "Al menos un carácter especial (!@#$%)" **Y** opcionalmente, mientras escribo la nueva contraseña, los requisitos cumplidos se marcan visualmente (ej: con ✓ verde) y los no cumplidos permanecen en estado neutral o con ✗ **Y** esta retroalimentación visual me ayuda a crear una contraseña segura que cumpla todos los requisitos antes de intentar guardar.

---

**Escenario 10 – Validar que las contraseñas se almacenan de forma segura**

**Dado que** he cambiado mi contraseña exitosamente,  
**cuando** el sistema almacena la nueva contraseña en la base de datos,  
**entonces** la contraseña NO se almacena en texto plano **Y** se utiliza un algoritmo de hash seguro (ej: bcrypt, Argon2, PBKDF2) para almacenar la contraseña **Y** se agrega salt único para cada contraseña **Y** el hash resultante es lo que se almacena en la base de datos **Y** la contraseña original nunca es recuperable del hash **Y** al ingresar los campos de contraseña, los caracteres se ocultan mostrando asteriscos (*) o puntos (•) en lugar del texto real **Y** las contraseñas nunca se muestran en logs del sistema **Y** el cambio de contraseña cumple con mejores prácticas de seguridad para proteger las cuentas de usuario.

---

# **3. Análisis de Criticidad**

## **Criterio de Aceptación Más Crítico:**

**Escenario 3 – Cambiar contraseña exitosamente**

### **Justificación:**

Este es el criterio más crítico por las siguientes razones fundamentales:

1. **Valida el propósito central de la HU:** La Historia de Usuario establece que el Usuario quiere "actualizar mi contraseña para mantener mi cuenta segura regularmente". El Escenario 3 valida directamente que el usuario PUEDE efectivamente cambiar su contraseña cuando todo está correcto, cumpliendo el objetivo de seguridad.

2. **Representa el "happy path" completo:** Es el flujo de éxito que valida end-to-end:
   - Acceso al formulario de cambio
   - Ingreso correcto de contraseña actual
   - Validación de requisitos de seguridad
   - Verificación de coincidencia de contraseñas
   - Actualización segura en base de datos (hash)
   - Retroalimentación de éxito al usuario
   - Mantenimiento de sesión activa

3. **Impacto directo en seguridad de la cuenta:** Si este escenario falla:
   - Los usuarios NO pueden actualizar sus contraseñas
   - Las cuentas quedan vulnerables con contraseñas antiguas
   - Se pierde la capacidad de responder a brechas de seguridad
   - El objetivo "mantener cuenta segura regularmente" es imposible

4. **Mayor frecuencia de uso esperado:** En operación normal:
   - Cambiar contraseña exitosamente es el caso de uso principal
   - Los escenarios de error (4-7) son menos frecuentes que el caso exitoso
   - Los usuarios esperan poder cambiar su contraseña cuando lo necesitan

5. **Validación de seguridad crítica:** Verifica aspectos esenciales de seguridad:
   - Autenticación correcta (contraseña actual válida)
   - Aplicación de políticas de contraseñas seguras
   - Almacenamiento seguro mediante hash
   - Prevención de reutilización de contraseña
   - Mantenimiento de sesión (no cierra sesión innecesariamente)

6. **Fundamento para casos de error:** Los escenarios de error (4-7) son variaciones que validan qué pasa cuando algo sale mal, pero el Escenario 3 es el que debe funcionar para que la funcionalidad tenga valor. Sin un cambio exitoso posible, las validaciones de error son irrelevantes.

7. **Impacto en cumplimiento y mejores prácticas:** Muchas políticas de seguridad organizacionales requieren:
   - Cambios periódicos de contraseña
   - Capacidad de los usuarios de autogestionar su seguridad
   - Respuesta rápida ante sospechas de compromiso
   - El Escenario 3 habilita cumplir estos requisitos

8. **Experiencia de usuario crítica:** Un cambio exitoso proporciona:
   - Confirmación clara de que la acción se completó
   - Tranquilidad de que la cuenta está más segura
   - Continuidad sin interrupciones (sesión activa)
   - Confianza en la plataforma

9. **Prevención de bloqueos operativos:** Si los usuarios no pueden cambiar contraseñas:
   - Pueden quedar bloqueados con contraseñas comprometidas
   - No pueden cumplir políticas corporativas de rotación
   - Aumenta la carga en soporte técnico
   - Se reduce la autonomía del usuario

10. **Validación de integración completa:** El escenario verifica:
    - Frontend (formulario, validación cliente)
    - Backend (validación servidor, lógica de negocio)
    - Base de datos (actualización segura, hash)
    - Gestión de sesiones (mantener usuario autenticado)
    - Notificaciones (retroalimentación al usuario)

Los demás escenarios son importantes para robustez (validaciones de error) y usabilidad (cancelar, visualizar requisitos), pero el Escenario 3 es el que garantiza que el sistema cumple su promesa fundamental: **permitir al Usuario actualizar efectivamente su contraseña cuando toda la información es correcta para mantener su cuenta segura regularmente, que es el valor central y el caso de uso principal de esta funcionalidad crítica de seguridad**.