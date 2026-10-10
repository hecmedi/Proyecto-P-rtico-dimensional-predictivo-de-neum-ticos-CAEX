# Proyecto-Portico-dimensional-predictivo-de-neumaticos-CAEX
 Medir cada CAEX en tránsito con un pórtico instrumentado, mantener la historia dimensional por serial y proyectar las horas de vida útil remanente de cada neumático, para programar el retiro antes de que falle.
# Control de desgaste de neumáticos CAEX

Sistema que mide por imágenes el desgaste de neumáticos de camiones mineros (CAEX), proyecta las horas remanentes y permite agendar la intervención en taller, dejando trazabilidad para la reunión semanal y la negociación con el proveedor.
# Pórtico dimensional predictivo de neumáticos CAEX

Documentación de los avances del proyecto:

- **Avance 1:** propuesta de valor
- **Avance 2:** propuesta de solución, caso de uso principal, maqueta preliminar y roadmap inicial

Ingeniería Digital en Acción: Datos con IA, MVP · Unidad 1 · Equipo 3
Universidad de Santiago de Chile

## Equipo

- Francisco Opazo
- Héctor Medina
- Manuel Ávalos Castillo
- Nicolás Echeverría

## Avance 1: propuesta de valor

### Problemática y beneficiario

**El costo oculto de los neumáticos OTR.** Es el mayor costo variable de una faena a cielo abierto y hoy se gestiona mediante inspecciones por muestreo.


**Quién lo sufre:** las Superintendencias de Servicios Mina y las Gerencias de Mantenimiento de faenas a cielo abierto con flotas de 20 CAEX o más (Cat 793, 797 y 798; Komatsu 930E y 960E). El retiro de cada neumático lo define el planificador de Mantención de Neumáticos, basándose principalmente en inspecciones por muestreo.

**La evidencia**

| Cifra | Significado |
|---|---|
| **US$40M** | En neumáticos por faena tipo: 6 unidades por 120 CAEX por unos US$55.000. En una faena de 20 CAEX son US$6,6M |
| **~30%** | De los neumáticos muere prematuramente, por corte, impacto o desgaste |
| **15 a 30 min** | De inspección manual por CAEX, subjetiva y hecha por muestreo |

**Qué pasa si no se resuelve.** Una falla de neumático en operación puede detener la rampa y generar riesgos para la continuidad operacional. Y sin historia por serial, la faena no tiene data dura para negociar frente al fabricante (Michelin, Bridgestone o BKT).

### Propuesta de valor

**Del muestreo manual a la proyección de vida útil:** medir cada CAEX en tránsito mediante un pórtico instrumentado, mantener el historial dimensional de cada neumático identificado por su número de serie y estimar su vida útil remanente para programar su retiro antes de que falle.

**Por qué es mejor que las alternativas actuales**

| Hoy | Con el pórtico |
|---|---|
| Muestreo humano, 15 a 30 min por CAEX | Una pasada a 2 a 5 km/h, sin detener el camión |
| Inspección por muestreo: cobertura limitada de la flota | Seis neumáticos de cada CAEX, en cada pasada por el pórtico |
| Subjetiva y sujeta a fatiga | Objetiva: escáner 3D, cámaras de daño y termografía |
| Sin historia individual del neumático | Historia dimensional por serial y posición |
| Reactiva: el neumático ya falló | Predictiva: el retiro se programa con anticipación |

**Cobertura de la banda de rodadura.** Al girar la rueda, se observan sucesivamente distintas zonas de la banda de rodadura. La cobertura de todo su ancho y circunferencia es un objetivo para validar mediante la ubicación de sensores y las pruebas de captura en tránsito.

**Qué construiremos en el semestre.** Se desarrollarán el tablero del planificador y el modelo de proyección a partir de datos sensoriales sintéticos. La instalación del pórtico instrumentado, que será la fuente de datos, no forma parte de esta etapa.

## Avance 2: propuesta de solución, caso de uso, maqueta y roadmap

### Propuesta de solución

Proponemos reducir las fallas imprevistas de neumáticos OTR y las detenciones no planificadas mediante un sistema que entregue al planificador de Mantención de Neumáticos una **proyección de vida útil por neumático**, basada en mediciones de un pórtico instrumentado y en el historial asociado a cada número de serie. Evaluaremos su efectividad mediante la reducción de los retiros por fallas imprevistas y el aumento de la vida útil promedio de los neumáticos.

El sistema integra captura automática de datos, gestión del historial y herramientas para programar intervenciones. Su principal aporte es transformar las mediciones en proyecciones de vida útil que apoyen la toma de decisiones y la planificación del mantenimiento.

> **Meta:** identificar condiciones de riesgo con al menos **200 horas de anticipación** al posible punto de falla. Es una hipótesis que deberá validarse con datos operacionales; no constituye una capacidad demostrada del prototipo.

### Caso de uso principal

| | |
|---|---|
| **Actor primario** | Planificador de Mantención de Neumáticos, responsable de programar retiros, rotaciones e intervenciones al inicio de cada turno |
| **Objetivo** | Programar intervenciones preventivas en neumáticos con riesgo de falla, con al menos 200 horas de anticipación respecto del punto probable de falla (sujeto a validación operacional) |
| **Precondición** | El pórtico está instalado en un punto obligatorio de tránsito de la flota (por ejemplo, la salida del taller o la zona de abastecimiento de combustible) y calibrado. Cada neumático tiene su número de serie registrado y al menos dos mediciones dimensionales previas. El planificador dispone del tablero al inicio de cada turno |
| **Postcondición** | Los neumáticos críticos quedan programados para intervención antes de una posible falla en operación. El historial dimensional se actualiza automáticamente. El ERP registra la orden con trazabilidad al pórtico y a la proyección del modelo, como respaldo para la planificación semanal y las gestiones con Michelin, Bridgestone o BKT |

#### Escenario principal de éxito

1. Un CAEX atraviesa el pórtico a una velocidad entre 2 y 5 km/h. Al detectar su paso, los sensores se sincronizan y capturan la condición de los seis neumáticos en una sola pasada.
2. El escáner 3D reconstruye la banda de rodadura y estima la profundidad remanente en cada posición con precisión milimétrica. Las cámaras identifican cortes, rocas incrustadas y desgastes irregulares, y la termografía registra la temperatura superficial de cada flanco.
3. El sistema identifica cada neumático mediante la lectura de su número de serie grabado en el costado o por RFID, cuando esté disponible, y confirma su posición en el camión.
4. El sistema registra profundidad, daños, temperatura y horas de operación en el historial de cada neumático y recalcula su vida útil remanente considerando el desgaste histórico y las condiciones de la ruta del CAEX.
5. El sistema clasifica cada neumático en condición **verde, amarilla o roja** según su riesgo y su proximidad al umbral de retiro seguro, y publica el listado en el tablero de priorización del turno.
6. El planificador revisa el tablero, identifica los neumáticos en rojo o en amarillo cercanos al umbral, y programa su intervención en la próxima ventana disponible del taller.
7. El sistema notifica al taller, genera la orden de trabajo en el ERP y registra el evento con trazabilidad completa, como respaldo para la planificación semanal y la gestión técnica con el proveedor.

#### Extensiones

- **3a. Número de serie no identificable** (suciedad, ángulo desfavorable o desgaste del flanco): se conserva la medición asociada al CAEX y a su posición, la identificación queda pendiente y se programa una nueva lectura. Tras tres pasadas consecutivas sin identificar, se genera una tarea de verificación manual para el operador del punto de control.
- **4a. Medición fuera de tolerancia** (suciedad o interferencias): se descarta, se mantiene la proyección vigente y se solicita una nueva pasada con la superficie limpia. Tras tres mediciones consecutivas fuera de tolerancia del mismo neumático, se emite una alerta para revisar el pórtico.
- **5a. Daño crítico** (corte profundo en el flanco, sobrecalentamiento localizado o signos de delaminación): se alerta de inmediato al despachador y al planificador, antes de la priorización habitual. El CAEX es derivado al taller para su evaluación antes de retomar la operación.

### Maqueta digital preliminar

Cuatro pantallas del flujo principal. Los pasos 1 a 4 del escenario son procesos automáticos. El paso 5 publica el tablero de la pantalla 1; desde el paso 6 interactúa el planificador, que consulta la ficha y agenda la intervención en las pantallas 2 y 3. La pantalla 4 muestra la orden emitida (paso 7). La disposición y los elementos visuales son preliminares.

| 1. Tablero del turno | 2. Ficha del neumático |
|---|---|
| <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/7f489b3a-70dc-472d-83bc-3947c490a0ad" /> | <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/f73b9803-0df4-4eac-b252-233cb2d0b1a2" />
|
| **3. Agendar intervención** | **4. Orden emitida** |
|---|---|
| <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/c8c80b81-3610-4c75-aa9e-156bb6513d68" />| <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/d81bfbe2-738a-4c84-acd9-2833a9994c10" />|

Versión navegable en Figma: [Maqueta de sistema de mantenimiento](https://www.figma.com/make/EDZNEzovnKPwBaUDV0GySq/Maqueta-de-sistema-de-mantenimiento)

#### Herramientas que la maqueta revela

| Característica | Pantalla | Decisión técnica |
|---|---|---|
| Flota ordenada por nivel de riesgo | 1 | Un modelo de proyección y un entorno de ejecución que calculen la vida útil remanente por neumático y por turno |
| Zonas verde, amarilla y roja | 1 | Umbrales de retiro seguro configurables según el tipo de neumático y las condiciones de la faena |
| Curva de desgaste de la ficha | 2 | Una serie temporal por serial que conserve profundidad, temperatura y horas de operación de cada medición |
| Ventana del taller | 3 | Un modelo de capacidad del taller con turnos y cupos disponibles, o una integración con el sistema existente |
| Orden escrita en el ERP | 4 | Una integración con el ERP que defina credenciales, estructura de datos y tratamiento de órdenes rechazadas |
| Trazabilidad de la orden a su medición | 4 | Un registro que vincule cada orden con la medición y la versión del modelo que la originaron |
| Alerta al despachador (extensión 5a) | 1 | Un rol de despachador y un canal de notificación prioritaria para daños que requieren atención inmediata |

### Roadmap inicial

El roadmap reúne ocho resultados esperados distribuidos en **Ahora, Próximo y Después** ([página del proyecto en Notion] (https://app.notion.com/p/Grupo-3-b76498f17d47839d8bf701014eb9d394)

Durante el semestre se desarrollarán el tablero del planificador y el modelo de proyección con **datos sensoriales sintéticos**. La instalación del pórtico corresponde a una etapa posterior.

La meta de anticipación de 200 horas se ubica en *Después*, porque debe contrastarse con la evolución real de los neumáticos y sus fallas registradas. El prototipo permitirá evaluar el funcionamiento del flujo con datos sintéticos, pero no acreditar esa anticipación ni una reducción de fallas en operación.

# Historias de usuario del front end

> Borrador del Equipo 3. Parte de las tres pantallas ya construidas (capturas en [`img/`](img/)) y propone mejoras que integran el **nivel de daño** detectado en las fotos. Cada historia indica si **ya existe** en la interfaz o es una **mejora propuesta**. El recorrido y los criterios deben validarse con un planificador de Mantención de Neumáticos.

## Pantallas actuales

| Pantalla | Captura | Qué hace hoy |
|---|---|---|
| Tablero del turno | ![Tablero](img/ui-tablero.jpg) | Flota ordenada por horas de vida útil remanente, con resumen por zona y filtros |
| Camiones | ![Camiones](img/ui-camiones.jpg) | Seis posiciones por CAEX, cada una abre la ficha del neumático |
| Órdenes de trabajo | ![Órdenes](img/ui-ordenes.jpg) | Órdenes con estado, tipo y trazabilidad a la medición que las originó |

**Zonas de vida útil (según el tablero):** rojo, menos de 200 h, programar el retiro ahora · amarillo, menos de 500 h, entra a la próxima ventana · verde, más de 500 h · sin datos, sin mediciones y por tanto sin proyección.

## Backlog

| Código | Historia | Pantalla | Estado |
|---|---|---|---|
| HU-F01 ★ | Ver la flota ordenada por horas remanentes y zona | Tablero | Existe |
| HU-F02 | Buscar y filtrar el tablero | Tablero | Existe |
| HU-F03 ★ | Ver los camiones con sus seis posiciones | Camiones | Existe |
| HU-F04 ★ | Abrir la ficha y registrar una medición | Ficha | Existe |
| HU-F05 | Ver el daño detectado con la foto marcada y corregirlo | Ficha | Mejora |
| HU-F06 | Ver el nivel de daño y las alertas críticas en tablero y camiones | Tablero, Camiones | Mejora |
| HU-F07 ★ | Consultar y filtrar las órdenes de trabajo | Órdenes | Existe |
| HU-F08 | Ver la trazabilidad de una orden hasta su evidencia | Órdenes | Parcial |
| HU-F09 | Modificar una orden programada | Órdenes | Mejora |
| HU-F10 | Anular una orden con su motivo | Órdenes | Mejora |

★ = flujo principal. Orden según la secuencia real de uso.

---

## HU-F01 ★ Ver la flota ordenada por horas remanentes y zona
**Como** planificador de Mantención de Neumáticos, **quiero** ver al iniciar el turno la flota ordenada por horas de vida útil remanente y agrupada por zona, **para** programar primero los retiros más urgentes sin revisar neumático por neumático.

**Escenario principal**
- **Dado** que existen mediciones de la flota
- **Cuando** abro el tablero del turno
- **Entonces** veo cuatro tarjetas (rojo, amarillo, verde, sin datos) con su cantidad, y una tabla ordenada de menos a más horas remanentes con camión, posición, serial, profundidad, tasa, horas, zona y última medición

**Escenario alternativo**
- **Dado** que un neumático no tiene mediciones
- **Cuando** abro el tablero
- **Entonces** cuenta en «sin datos» y su fila indica que no hay proyección

## HU-F02 Buscar y filtrar el tablero
**Como** planificador, **quiero** buscar por serial, camión o modelo y filtrar por zona y por tipo de tasa, **para** llegar rápido al neumático o grupo que me interesa.

**Escenario principal**
- **Dado** que estoy en el tablero
- **Cuando** elijo la zona «rojo» y la tasa «observada»
- **Entonces** la tabla muestra solo los neumáticos que cumplen ambas condiciones

**Escenario alternativo**
- **Dado** que mi búsqueda no coincide con ningún neumático
- **Cuando** termino de escribir
- **Entonces** veo un mensaje «sin resultados» y la opción de limpiar los filtros

## HU-F03 ★ Ver los camiones con sus seis posiciones
**Como** planificador, **quiero** ver cada CAEX con sus seis posiciones coloreadas por zona, **para** entender el estado de un camión completo de un vistazo.

**Escenario principal**
- **Dado** que estoy en la pantalla Camiones
- **Cuando** se muestra cada camión
- **Entonces** veo su modelo, su horómetro, la cantidad de posiciones en rojo y las posiciones P1 a P6 con sus horas remanentes

**Escenario alternativo**
- **Dado** que una posición no tiene neumático medido
- **Cuando** se dibuja el camión
- **Entonces** la posición aparece como «sin datos» y sigue siendo seleccionable

## HU-F04 ★ Abrir la ficha y registrar una medición
**Como** planificador, **quiero** abrir la ficha de un neumático desde el tablero o desde un camión y registrar una nueva medición, **para** mantener actualizada su proyección.

**Escenario principal**
- **Dado** que selecciono un neumático
- **Cuando** abro su ficha y registro una medición válida
- **Entonces** la ficha, el tablero y el camión muestran la proyección recalculada

**Escenario alternativo**
- **Dado** que la medición tiene un valor imposible (por ejemplo, mayor que la anterior)
- **Cuando** intento guardarla
- **Entonces** el sistema la rechaza con el motivo y conserva la proyección vigente

## HU-F05 Ver el daño detectado con la foto marcada y corregirlo *(mejora)*
**Como** planificador, **quiero** ver en la ficha la foto del neumático con cada daño marcado, su tipo y su nivel, y poder corregirlo, **para** confirmar la gravedad con evidencia y no con una impresión.

**Escenario principal**
- **Dado** que el neumático tiene una foto procesada
- **Cuando** abro su ficha
- **Entonces** veo la foto con cada daño marcado, su tipo, su nivel (0 a 3), su confianza y la fecha de la pasada

**Escenario alternativo**
- **Dado** que el modelo clasificó mal un daño
- **Cuando** lo corrijo e indico el motivo
- **Entonces** la ficha muestra la corrección con mi nombre y la fecha, y la foto queda guardada para reentrenar

## HU-F06 Ver el nivel de daño y las alertas críticas *(mejora)*
**Como** planificador, **quiero** ver el nivel de daño junto a la zona de vida útil en el tablero y en cada posición del camión, y una alerta cuando un neumático esté en nivel 3, **para** no depender solo de las horas cuando hay un daño grave.

**Escenario principal**
- **Dado** que un neumático está en nivel 3
- **Cuando** abro el tablero
- **Entonces** aparece una alerta que lleva a su ficha, y la fila y la posición del camión muestran el nivel además de la zona

**Escenario alternativo**
- **Dado** que un neumático está en zona verde pero con daño nivel 3
- **Cuando** se ordena el tablero
- **Entonces** sube al primer lugar, porque el daño crítico prevalece sobre las horas

## HU-F07 ★ Consultar y filtrar las órdenes de trabajo
**Como** planificador, **quiero** ver las órdenes con su estado, tipo, fecha programada y turno, y filtrarlas, **para** saber qué está pendiente y qué ya se hizo.

**Escenario principal**
- **Dado** que existen órdenes
- **Cuando** abro Órdenes de trabajo
- **Entonces** veo los contadores por estado (programada, ejecutada, anulada) y la tabla con orden, neumático, intervención y nota, fecha programada, horas al emitir, origen y estado

**Escenario alternativo**
- **Dado** que filtro por estado «programada» y tipo «retiro»
- **Cuando** no existe ninguna con ambas condiciones
- **Entonces** veo «sin resultados» y los contadores no cambian

## HU-F08 Ver la trazabilidad de una orden hasta su evidencia *(parcial)*
**Como** planificador, **quiero** que cada orden muestre la medición que la originó y la evidencia asociada, **para** sustentar el retiro frente al taller y reclamar al proveedor.

**Escenario principal**
- **Dado** que abro una orden de retiro
- **Cuando** reviso su origen
- **Entonces** veo la medición (por ejemplo, profundidad y tasa observada), la proyección con que se emitió y, en la mejora, la foto con los daños de ese momento

**Escenario alternativo**
- **Dado** que la orden es anterior al registro de fotos
- **Cuando** la abro
- **Entonces** muestra la medición y avisa que no tiene foto asociada

## HU-F09 Modificar una orden programada *(mejora)*
**Como** planificador, **quiero** cambiar la ventana o la nota de una orden que aún está programada, **para** ajustarla cuando cambian las condiciones sin tener que anularla y emitirla de nuevo.

**Escenario principal**
- **Dado** que una orden está en estado «programada»
- **Cuando** elijo otra ventana con cupos, indico el motivo del cambio y guardo
- **Entonces** la orden muestra la nueva ventana, se libera el cupo anterior y se ocupa el nuevo, el taller es notificado y el historial registra quién, cuándo y por qué

**Escenario alternativo**
- **Dado** que una orden ya está ejecutada o anulada
- **Cuando** intento modificarla
- **Entonces** el sistema no permite el cambio, explica el estado de la orden y muestra su historial

**Reglas:** el motivo es obligatorio; no se puede elegir una ventana sin cupos; la orden conserva su código y su vínculo a la medición de origen.

## HU-F10 Anular una orden con su motivo *(mejora)*
**Como** planificador, **quiero** anular una orden programada indicando el motivo, **para** liberar el cupo del taller sin perder el registro de lo que ocurrió.

**Escenario principal**
- **Dado** que una orden está «programada»
- **Cuando** elijo un motivo, pulso «Anular orden» y confirmo
- **Entonces** la orden pasa a «anulada», se libera su cupo, el contador de anuladas sube en uno y la orden permanece en la lista con su motivo

**Escenario alternativo**
- **Dado** que abrí la confirmación de anulación
- **Cuando** elijo «No»
- **Entonces** la orden queda sin cambios y vuelvo al formulario

**Reglas:** la anulación pide confirmación explícita; la orden nunca se borra, porque es evidencia para la reunión semanal y para el proveedor; una orden anulada no se puede reactivar (se emite una nueva).

---

## Mejoras observadas en las capturas

| Observación | Propuesta | Historia |
|---|---|---|
| Las zonas se basan solo en horas remanentes | Mostrar también el nivel de daño de la foto y priorizar el daño crítico | HU-F06 |
| Las posiciones del camión muestran solo horas | Agregar el nivel de daño y un nivel por camión | HU-F06 |
| La ficha registra mediciones, pero no muestra la imagen | Foto con daños marcados, confianza y corrección | HU-F05 |
| El campo de búsqueda del tablero corta el texto de ayuda | Ensancharlo o acortar el texto | HU-F02 |
| Las notas largas alargan mucho las filas de órdenes | Mostrar un resumen y expandir al hacer clic | HU-F07 |
| La orden guarda la medición, no la evidencia visual | Vincular la foto del momento de la orden | HU-F08 |
| Las capturas no muestran cómo modificar o cancelar una orden | Acciones «Modificar» y «Anular» con motivo e historial | HU-F09, HU-F10 |
| La columna «última medición» muestra «(obs.)» sin explicar | Definir su significado y agregar una leyenda | HU-F01 |

## Revisión INVEST
Las historias de mejora (HU-F05, HU-F06, HU-F08) dependen de que el modelo de visión entregue daños y fotos. Mientras no exista, trabajarlas con fotos y daños de ejemplo, y dividirlas si no caben en un sprint (por ejemplo, separar la alerta crítica de la corrección).




