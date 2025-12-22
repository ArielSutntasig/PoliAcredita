# CRITERIOS DE ACEPTACIÓN - HU: Observar caracteres permitidos en justificaciones en Matrices

---

## **NOTA IMPORTANTE:**
Este análisis se basa en el **límite de 2000 caracteres especificado** para campos de justificación en las matrices (RA-OP, RAA-RA, RA-EUR-ACE). Los criterios están diseñados para ser actualizados fácilmente cuando se defina el límite final en el prototipo.

---

## **1. ANÁLISIS DE TABLA DE DECISIÓN**

### **Paso 1: Identificar Condiciones y Acciones**

#### **Condiciones identificadas basadas en la HU y mejores prácticas de UX:**

**C1: Campo de justificación tiene contenido**
- Estado: Sí / No
- Fuente: Usuario escribe en el campo de texto de justificación al crear/editar una relación
- Estados posibles: Vacío (0 caracteres) o Con contenido (1+ caracteres)

**C2: Cantidad de caracteres dentro del límite permitido**
- Estado: Sí / No
- Rangos:
  - Sí: 0 a 2000 caracteres
  - No: Intento de escribir más de 2000 caracteres
- Fuente: Validación en tiempo real del input del usuario

**C3: Caracteres cerca del límite máximo (zona de advertencia)**
- Estado: Sí / No
- Definición: Últimos 10% del límite (1800-2000 caracteres)
- Propósito: Alertar al usuario que está por alcanzar el límite
- Fuente: Lógica de validación de UI

#### **Acciones del sistema identificadas:**

**A1: Mostrar contador de caracteres**
- Condición: Siempre visible en el campo de justificación
- Formato esperado: "X/2000 caracteres" o "X de 2000 caracteres"
- Ubicación: Debajo o al lado del campo de texto
- Actualización: En tiempo real mientras el usuario escribe

**A2: Actualizar contador en tiempo real**
- Condición: Cada vez que el usuario escribe o borra caracteres
- Comportamiento: Incrementar/decrementar el número actual
- Sin delay: Actualización instantánea

**A3: Mostrar contador en estado normal (sin advertencia)**
- Condición: Caracteres entre 0-1799
- Estilo visual: Color neutral (gris o negro)
- Mensaje: Simple contador numérico

**A4: Mostrar contador en estado de advertencia**
- Condición: Caracteres entre 1800-2000 (últimos 10%)
- Estilo visual: Color de advertencia (amarillo/naranja)
- Propósito: Alertar que está cerca del límite
- Mensaje adicional opcional: "Te acercas al límite de caracteres"

**A5: Prevenir escritura adicional al alcanzar límite**
- Condición: Caracteres = 2000
- Comportamiento: No permitir escribir más caracteres
- Teclas bloqueadas: Caracteres alfanuméricos
- Teclas permitidas: Backspace, Delete, flechas de navegación
- Estilo visual: Contador en rojo

**A6: Permitir pegar texto con truncamiento automático**
- Condición: Usuario pega texto que excedería 2000 caracteres
- Comportamiento: Truncar al límite de 2000 caracteres
- Feedback: Mostrar mensaje informativo sobre truncamiento

**A7: Validar límite al guardar relación**
- Condición: Usuario intenta guardar con justificación válida
- Validación: Verificar que caracteres ≤ 2000
- Si válido: Permitir guardar
- Si inválido: Mostrar mensaje de error (caso edge)

---

### **Paso 2: Tabla de Decisión Completa (Maximizada)**

Con 3 condiciones binarias: 2^3 = **8 reglas**

| Regla | C1: Tiene contenido | C2: Dentro del límite | C3: Cerca del límite | Acción del Sistema |
|-------|---------------------|----------------------|---------------------|-------------------|
| R1    | No                  | Sí                   | No                  | A1 + A2 + A3: Mostrar "0/2000 caracteres" en estado normal |
| R2    | No                  | Sí                   | Sí                  | IMPOSIBLE* - No puede estar vacío y cerca del límite |
| R3    | No                  | No                   | No                  | IMPOSIBLE* - Campo vacío siempre está dentro del límite |
| R4    | No                  | No                   | Sí                  | IMPOSIBLE* - Combinación contradictoria |
| R5    | Sí                  | Sí                   | No                  | A1 + A2 + A3 + A7: Contador normal (1-1799 caracteres) |
| R6    | Sí                  | Sí                   | Sí                  | A1 + A2 + A4 + A7: Contador en advertencia (1800-2000 caracteres) |
| R7    | Sí                  | No                   | No                  | A1 + A2 + A5 + A6: Límite alcanzado, prevenir escritura |
| R8    | Sí                  | No                   | Sí                  | IMPOSIBLE* - No puede estar fuera del límite y en zona de advertencia |

*IMPOSIBLE: Combinaciones lógicamente contradictorias o imposibles por la definición de las condiciones.

---

### **Paso 3: Tabla de Decisión Minimizada**

#### **Lógica de minimización:**

1. **Regla R1:** Campo vacío (0 caracteres). Siempre está dentro del límite y no está cerca del límite. **Se mantiene como M1**.

2. **Reglas R2, R3, R4, R8:** Combinaciones lógicamente imposibles. **Se eliminan**.

3. **Regla R5:** Campo con contenido, dentro del rango normal (1-1799 caracteres). Contador se muestra en estado normal. **Se mantiene como M2**.

4. **Regla R6:** Campo con contenido, en zona de advertencia (1800-2000 caracteres). Contador se muestra con advertencia visual. **Se mantiene como M3**.

5. **Regla R7:** Campo con contenido, límite alcanzado (2000 caracteres). Sistema previene escritura adicional. **Se mantiene como M4**.

#### **Tabla Minimizada:**

| Regla Min | C1: Tiene contenido | C2: Dentro límite | C3: Cerca límite | Rango caracteres | Acción del Sistema |
|-----------|---------------------|------------------|------------------|------------------|-------------------|
| **M1**    | No                  | Sí               | No               | 0                | A1 + A2 + A3: Mostrar "0/2000 caracteres" |
| **M2**    | Sí                  | Sí               | No               | 1-1799           | A1 + A2 + A3 + A7: Contador estado normal |
| **M3**    | Sí                  | Sí               | Sí               | 1800-1999        | A1 + A2 + A4 + A7: Contador en advertencia |
| **M4**    | Sí                  | No               | -                | 2000             | A1 + A2 + A5 + A6 + A7: Límite alcanzado |

**Resultado: 4 reglas minimizadas**

---

### **Paso 4: Número Final de Criterios de Aceptación**

De las 4 reglas minimizadas, procedo a evaluar:

**Criterios derivados directamente de la tabla:**
1. M1 → AC sobre estado inicial con campo vacío
2. M2 → AC sobre contador en rango normal (happy path principal)
3. M3 → AC sobre advertencia al acercarse al límite
4. M4 → AC sobre límite alcanzado y prevención de escritura adicional

**Análisis de criterios adicionales necesarios:**

Del objetivo de la HU ("conocer el máximo de caracteres permitidos para definir justificaciones concretas"):

5. **Visualización consistente en las 3 matrices:** El límite de 2000 caracteres debe aplicarse y mostrarse de forma idéntica en RA-OP, RAA-RA y RA-EUR-ACE.

6. **Comportamiento al pegar texto:** Manejar casos donde el usuario pega texto que excede el límite.

**Criterios a CONSOLIDAR:**

- El comportamiento al pegar (punto 6) se incorporará en M4, ya que es parte del manejo del límite máximo.
- La consistencia entre matrices (punto 5) se validará en cada criterio mencionando las tres matrices.

**TOTAL FINAL: 4 Criterios de Aceptación**
- 4 derivados de la tabla de decisión (M1, M2, M3, M4)
- Comportamiento de pegado integrado en M4
- Consistencia entre matrices validada en cada criterio

**Justificación:**
Todos los criterios son únicos y necesarios para validar el comportamiento completo del contador de caracteres desde el estado inicial hasta el límite máximo, cubriendo todos los rangos y casos de uso.

---

## **2. LISTA DE CRITERIOS DE ACEPTACIÓN (Formato Gherkin)**

---

### **Escenario 1 – Estado inicial del campo de justificación vacío**

**Dado que** soy un profesor en el sistema **Y** estoy creando o editando una relación en cualquiera de las matrices (RA vs OP, RAA vs RA, o RA vs EUR-ACE),
**cuando** visualizo el campo de "Justificación" sin haber escrito ningún contenido,
**entonces** se muestra el contador de caracteres con el texto "0/2000 caracteres" o formato equivalente **Y** el contador se presenta en color neutral (gris o negro) **Y** el campo está vacío y habilitado para escritura **Y** el límite de 2000 caracteres es claramente visible para que yo pueda planificar justificaciones concretas dentro de este límite.

---

### **Escenario 2 – Escribir justificación dentro del rango normal**

**Dado que** estoy en el campo de "Justificación" de cualquiera de las tres matrices **Y** el campo está vacío mostrando "0/2000 caracteres",
**cuando** escribo texto en el campo hasta alcanzar 1500 caracteres (dentro del rango 1-1799),
**entonces** el contador se actualiza en tiempo real mostrando "1500/2000 caracteres" **Y** el contador mantiene el color neutral sin advertencias **Y** puedo continuar escribiendo libremente **Y** cada carácter adicional que escribo incrementa el contador inmediatamente **Y** puedo borrar caracteres y el contador disminuye correspondientemente **Y** el sistema no muestra ninguna restricción o advertencia en este rango **Y** este comportamiento es idéntico en las matrices RA vs OP, RAA vs RA y RA vs EUR-ACE.

---

### **Escenario 3 – Advertencia al acercarse al límite de caracteres**

**Dado que** tengo 1700 caracteres escritos en el campo de "Justificación" de cualquier matriz,
**cuando** escribo caracteres adicionales hasta alcanzar el rango de 1800 a 1999 caracteres (últimos 200 caracteres del límite),
**entonces** el contador se actualiza mostrando el número actual de caracteres (ejemplo: "1850/2000 caracteres") **Y** el color del contador cambia a un color de advertencia (amarillo, naranja o similar) **Y** opcionalmente se muestra un mensaje adicional como "Te acercas al límite de caracteres" o "Quedan X caracteres disponibles" **Y** aún puedo continuar escribiendo hasta alcanzar los 2000 caracteres **Y** la advertencia visual me permite tomar decisiones informadas sobre cómo redactar una justificación concreta dentro del límite **Y** este comportamiento es consistente en las tres matrices del sistema.

---

### **Escenario 4 – Alcanzar el límite máximo y prevenir exceso**

**Dado que** tengo 1995 caracteres escritos en el campo de "Justificación" de cualquier matriz,
**cuando** escribo 5 caracteres adicionales alcanzando exactamente 2000 caracteres,
**entonces** el contador muestra "2000/2000 caracteres" **Y** el color del contador cambia a rojo o color de alerta máxima **Y** el sistema previene que pueda escribir caracteres adicionales mediante teclado **Y** las teclas de caracteres alfanuméricos, espacios y símbolos no insertan más texto **Y** aún puedo usar las teclas Backspace, Delete y flechas de navegación para editar el texto existente **Y** si intento pegar texto que excedería el límite, el sistema trunca automáticamente el texto pegado a 2000 caracteres **Y** se muestra un mensaje informativo indicando "Has alcanzado el límite de 2000 caracteres" o "Texto truncado al límite permitido" (en caso de pegado) **Y** al intentar guardar la relación, la validación confirma que los 2000 caracteres están dentro del límite permitido **Y** este límite de 2000 caracteres y comportamiento es idéntico en las tres matrices (RA vs OP, RAA vs RA, RA vs EUR-ACE) para mantener consistencia en todo el sistema.

---

## **3. ANÁLISIS DE CRITICIDAD**

### **Criterio Más Crítico:**

**Escenario 2 – Escribir justificación dentro del rango normal**

### **Justificación:**

Este criterio es el más crítico porque representa el **caso de uso principal y más frecuente** que valida directamente el objetivo de la HU: "conocer el máximo de caracteres permitidos para definir justificaciones concretas". Las razones específicas son:

1. **Cumplimiento directo del objetivo de la HU:** El profesor necesita "conocer el máximo de caracteres" para poder "definir justificaciones concretas". Este escenario valida que:
   - El límite de 2000 caracteres es claramente visible en todo momento
   - El contador se actualiza en tiempo real, proporcionando feedback constante
   - El profesor puede escribir libremente dentro del límite sin restricciones
   - La información sobre el límite está siempre disponible para planificar el contenido

2. **Caso de uso más frecuente (80-90% de las veces):** En la mayoría de los casos, los profesores escribirán justificaciones que están dentro del rango normal (1-1799 caracteres). Las justificaciones típicas académicas tienen entre 200-1500 caracteres. Este escenario valida que:
   - El comportamiento normal de escritura funciona correctamente
   - El contador es preciso y confiable
   - No hay interferencias o errores durante la escritura normal
   - La experiencia de usuario es fluida y sin interrupciones

3. **Base para todos los demás escenarios:** Este escenario es el "camino feliz" del cual derivan los otros:
   - Escenario 1 (campo vacío) es el punto de partida
   - Escenario 3 (advertencia) es una extensión cuando se acerca al límite
   - Escenario 4 (límite alcanzado) es el caso extremo
   
   Si el Escenario 2 falla, ninguno de los otros tiene sentido porque la funcionalidad básica no funciona.

4. **Validación de actualización en tiempo real:** Este escenario valida que el contador es **dinámico y preciso**:
   - Se actualiza instantáneamente con cada tecla presionada
   - Funciona correctamente al escribir (incremento)
   - Funciona correctamente al borrar (decremento)
   - No hay delays o errores de sincronización
   - El conteo es matemáticamente correcto
   
   Esta precisión es crítica para que el profesor pueda confiar en el contador al redactar.

5. **Fundamento para planificación de contenido:** Para "definir justificaciones concretas", el profesor necesita:
   - Ver cuántos caracteres ha usado en tiempo real
   - Calcular cuántos caracteres le quedan disponibles
   - Decidir si expandir o condensar la justificación
   - Planificar la estructura del texto
   
   Sin un contador preciso en el rango normal, el profesor no puede planificar efectivamente.

6. **Validación de consistencia entre matrices:** Este escenario especifica explícitamente que el comportamiento debe ser "idéntico en las matrices RA vs OP, RAA vs RA y RA vs EUR-ACE". Valida que:
   - El límite de 2000 es consistente en todas las matrices
   - El formato del contador es el mismo
   - El comportamiento de actualización es idéntico
   - No hay discrepancias que confundan al profesor

7. **Punto de fallo de mayor impacto en usabilidad:** Si este escenario falla:
   - El profesor no puede redactar justificaciones con confianza
   - No sabe si está dentro o fuera del límite hasta intentar guardar
   - Puede perder trabajo si escribe más de lo permitido sin saberlo
   - La experiencia de usuario se degrada significativamente
   - El objetivo de "conocer el máximo" no se cumple en tiempo real

8. **Prevención de frustración del usuario:** Los profesores redactan justificaciones académicas complejas que requieren tiempo y reflexión. Si el contador no funciona correctamente:
   - Pueden invertir tiempo en texto que luego debe ser truncado
   - No pueden optimizar el uso del espacio disponible
   - Se frustran al descubrir tarde que excedieron el límite
   - Pierden contexto al tener que editar después

9. **Habilitador de los demás escenarios:** 
   - Sin este escenario funcionando, la advertencia (Escenario 3) no tiene base
   - El límite máximo (Escenario 4) solo se alcanza pasando por este rango
   - El estado inicial (Escenario 1) evoluciona a este escenario
   
   Es el escenario de transición crítico.

10. **Validación de lógica de negocio correcta:** Este escenario confirma que:
    - El límite de 2000 caracteres está correctamente implementado
    - La lógica de conteo incluye todos los caracteres (letras, números, espacios, puntuación)
    - No hay caracteres especiales que se cuenten incorrectamente
    - El sistema maneja correctamente UTF-8 (acentos, ñ, caracteres especiales)

11. **Base para pruebas automatizadas:** Este escenario permite crear tests automatizados que:
    - Escriben N caracteres y verifican que el contador muestra N/2000
    - Borran M caracteres y verifican que el contador disminuye correctamente
    - Validan que el comportamiento es consistente en las 3 matrices
    - Prueban diferentes tipos de caracteres (ASCII, Unicode, emojis)

12. **Feedback en tiempo real crítico para UX:** La actualización instantánea del contador es una expectativa moderna de UX. Los usuarios esperan:
    - Ver cambios inmediatos en contadores
    - No tener que adivinar cuántos caracteres han usado
    - Recibir información continua, no solo al final
    
    Este escenario valida estas expectativas.

**Recomendación de prueba prioritaria:**
- Crear suite automatizada que escriba diferentes cantidades de caracteres (100, 500, 1000, 1500, 1799) y verifique contador
- Validar actualización en tiempo real con assertions de timing (<100ms)
- Probar escritura y borrado alternado para verificar incremento/decremento correcto
- Validar en las 3 matrices (RA-OP, RAA-RA, RA-EUR-ACE) que el contador es idéntico
- Probar con caracteres especiales, acentos, ñ, emojis para confirmar conteo correcto
- Verificar que el contador no se "congela" o tiene delays
- Incluir en regresión crítica para cualquier cambio en campos de texto
- Probar en múltiples navegadores (Chrome, Firefox, Safari, Edge)

**Sin este escenario funcionando, el profesor no puede "conocer el máximo de caracteres permitidos para definir justificaciones concretas"** en tiempo real, lo cual es el core de la HU. Un profesor sin feedback en tiempo real está navegando a ciegas, sin saber si su justificación cabe dentro del límite hasta que intenta guardar, momento en el cual puede ser demasiado tarde. Este escenario transforma un límite técnico en una herramienta útil de planificación de contenido.