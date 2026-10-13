# Carrito RC con ESP32-C3

Roadmap de seis semanas para aprender electrónica y programación embebida construyendo un carrito controlado por radio con **ESP-NOW**.

## Meta

Al final de la semana 2: tener un prototipo de banco en el que un ESP32-C3 lea un joystick y mande comandos por ESP-NOW a otro ESP32-C3, que controle motores N20 mediante un driver DRV8251. Los motores se prueban con las ruedas levantadas antes de instalar el carrito.

Al final de la semana 6: tener el carrito integrado, documentado y con el diseño de dos PCB revisado: una para el carro y otra para el control.

## Roadmap

| Semana | Tema | Resultado esperado |
|---|---|---|
| 1 | Fundamentos, componentes y entorno | Diagrama de bloques, componentes identificados, entorno para ESP32-C3 instalado y joystick leído localmente. |
| 2 | ESP-NOW y prototipo mínimo | Joystick → ESP-NOW → ESP32-C3 receptor → DRV8251 → motores N20; prueba segura en banco. |
| 3 | Alimentación y electrónica de potencia | Baterías y reguladores seleccionados con base en voltajes y corrientes medidos; alimentación estable. |
| 4 | Chasis, llantas y control | Montaje mecánico probado; dirección, velocidad, zona muerta y pérdida de señal controladas. |
| 5 | Diseño de las dos PCB | Esquemáticos y diseño de PCB para carro y control, revisados contra el prototipo. |
| 6 | Integración, validación y documentación | Pruebas finales, registro de resultados y preparación de la siguiente revisión de hardware. |

### Semana 1 — Bases y preparación

- Repasar voltaje, corriente, resistencia, polaridad y uso del multímetro.
- Diferenciar señales digitales, ADC (entrada analógica) y PWM (salida para controlar potencia/velocidad).
- Instalar el entorno y las librerías/paquete de placas ESP32; verificar que el modelo exacto de ESP32-C3 compila y carga un ejemplo.
- Leer el joystick B103-348 con el ADC y observar sus rangos y posición central.
- Identificar pines y límites eléctricos del módulo ESP32-C3, del driver DRV8251 y de los motores N20.
- Medir dimensiones y eje de los motores; comparar llantas compatibles con el eje y el chasis.

**Entregable:** diagrama de bloques y tabla inicial de piezas, pines, voltajes y corrientes por confirmar.

### Semana 2 — ESP-NOW y primer movimiento

- Probar comunicación ESP-NOW entre las dos placas ESP32-C3 (control y carro).
- Enviar un paquete de comandos desde el joystick y validar recepción con mensajes de depuración.
- Mapear ejes del joystick a velocidad/dirección; definir zona muerta para evitar movimiento accidental.
- Probar el DRV8251 con un motor N20 y luego con los motores previstos; comprobar sentido y PWM.
- Añadir un timeout: si dejan de llegar paquetes, el receptor debe detener los motores.
- Hacer pruebas con el chasis levantado y una fuente/batería dentro de las especificaciones.

**Entregable:** prototipo de banco joystick → ESP-NOW → motores. No instalarlo en el suelo hasta verificar alimentación, corriente y parada ante pérdida de señal.

### Semana 3 — Baterías, regulador y potencia

- Obtener voltaje nominal/máximo y corriente de arranque o bloqueo de los motores.
- Dimensionar la batería para motores y electrónica, considerando la corriente de bloqueo de ambos motores y el margen térmico del driver.
- Elegir el regulador ajustable por tornillo según entrada, salida, corriente y disipación; ajustar y medir su salida antes de conectar el ESP32-C3.
- Separar las rutas de alimentación de motores y lógica cuando el diseño lo requiera, manteniendo referencia de tierra común según el esquema.
- Añadir interruptor, protección y desacoplo; verificar temperatura y caídas de voltaje.

**Entregable:** esquema de alimentación con componentes seleccionados y mediciones documentadas.

### Semana 4 — Chasis, ruedas y firmware confiable

- Comparar llantas por diámetro, ancho, agarre, montaje y compatibilidad con los ejes N20.
- Montar el sistema de tracción elegido y revisar si será dirección diferencial o dirección mecánica.
- Calibrar joystick, zona muerta, límites de PWM, aceleración y reversa.
- Probar desconexión/reconexión ESP-NOW y arranque seguro; el carro debe quedar detenido si no hay enlace.
- Hacer pruebas de recorrido y registrar autonomía, alcance, temperatura y fallas.

**Entregable:** carrito funcional con comportamiento seguro y una lista priorizada de ajustes.

### Semana 5 — Dos PCB

- Diseñar la PCB del carro: ESP32-C3, DRV8251, conectores de motores, batería/regulador, interruptor y puntos de prueba.
- Diseñar la PCB del control: ESP32-C3, joystick, batería/regulador, interruptor y puntos de prueba.
- Revisar pinout, polaridad, anchos de pista para potencia, separación entre lógica y motores, montaje y conectores.
- Comparar cada esquema contra el cableado que ya funcionó en el prototipo.
- Generar archivos de fabricación y lista de materiales después de revisar los diseños.

**Entregable:** esquemáticos y PCB revisados. La fabricación física puede extenderse más allá de estas seis semanas según el proveedor.

### Semana 6 — Validación y cierre de versión

- Si las PCB ya llegaron, inspeccionarlas sin alimentación y probarlas por etapas; si no, continuar validación con el prototipo y dejar lista la revisión de PCB.
- Verificar regulación, consumo, temperatura, alcance y parada por pérdida de enlace.
- Ejecutar una lista de pruebas repetible para control, motores, batería y autonomía.
- Documentar diagramas, pinout, firmware, materiales, resultados y problemas conocidos.
- Cerrar una lista de mejoras para la siguiente iteración.

**Entregable:** versión de referencia reproducible y backlog para la siguiente etapa.

## Componentes principales por confirmar

- 2 × ESP32-C3 (control y carro; confirmar modelo exacto y antena).
- Motores N20 y llantas compatibles con su eje.
- Driver DRV8251/DRV8251A: confirmar variante, módulo y corriente admisible.
- Joystick B103-348.
- Baterías para control y carro; definir química, voltaje y capacidad.
- Reguladores ajustables por tornillo, elegidos según las cargas reales.
- Chasis, interruptores, conectores, protección y materiales de montaje.

> **Seguridad:** confirmar el modelo exacto de cada módulo y sus límites antes de cablear. No conectar la batería directamente a un pin de alimentación del ESP32-C3 sin verificar el rango permitido. Ajustar y medir el regulador antes de conectar la placa; probar motores con ruedas levantadas y detener la prueba si hay calentamiento excesivo.

## Organización en GitHub

Cada semana debe trabajarse como una tarea independiente. Las seis tareas del roadmap están en Issues; se pueden agregar al Project **Carrito RC** para verlas como tablero.
