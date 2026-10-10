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
| <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/7f489b3a-70dc-472d-83bc-3947c490a0ad" />
 | <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/f73b9803-0df4-4eac-b252-233cb2d0b1a2" />
|
| **3. Agendar intervención** | **4. Orden emitida** |
| <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/c8c80b81-3610-4c75-aa9e-156bb6513d68" />
| <img width="442" height="547" alt="image" src="https://github.com/user-attachments/assets/d81bfbe2-738a-4c84-acd9-2833a9994c10" />
|

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
# CAEX Monitor — prototipo interactivo

## Abrir en Visual Studio Code
1. Descomprime el ZIP.
2. Abre la carpeta `caex_tire_monitor` en Visual Studio Code.
3. Abre `index.html` en el navegador o usa la extensión Live Server.

## Pestañas conectadas
- **Tablero del turno:** indicadores, colores rojo/amarillo/verde/sin datos, búsqueda y filtros. Al pulsar una fila se abre la ficha del neumático.
- **Camiones:** seis posiciones por CAEX. Al pulsar una posición ocupada se abre la misma ficha; una posición vacía permite registrar un neumático.
- **Órdenes de trabajo:** crea órdenes asociadas a neumáticos existentes; desde una orden puedes abrir la ficha relacionada. Las órdenes pueden pasar a ejecutadas o anuladas.
- **Mediciones:** al guardar una nueva medición se actualizan la proyección, el color de estado, los contadores del tablero y la vista del camión.
- **Persistencia:** los cambios se guardan en localStorage del navegador.

## Fórmula de demostración
Horas remanentes = ((profundidad actual - umbral de retiro) / tasa de desgaste) × 100.

La tasa se expresa en mm por cada 100 horas. Validar el umbral y el método de proyección con el área técnica antes de usar datos operacionales.

## Límites
Es un prototipo local con datos de ejemplo. No procesa automáticamente fotografías, no tiene usuarios/permisos y no sincroniza datos entre equipos. Para producción se recomienda API/backend, base de datos centralizada, auditoría, autenticación, respaldos y validación del método de medición.

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CAEX | Control de neumáticos</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <aside class="sidebar">
    <div class="brand"><div class="brand-mark">C</div><div><strong>CAEX Monitor</strong><small>Gestión de neumáticos</small></div></div>
    <div class="nav-label">OPERACIONES</div>
    <button class="nav-link active" data-tab="dashboard">▦ <span>Tablero del turno</span></button>
    <button class="nav-link" data-tab="trucks">▤ <span>Camiones</span></button>
    <button class="nav-link" data-tab="orders">☷ <span>Órdenes de trabajo</span></button>
    <div class="sidebar-bottom"><span class="status-dot"></span> Prototipo local <small>v1.0</small></div>
  </aside>
  <main class="main">
    <header class="topbar">
      <div><span class="eyebrow">GESTIÓN DE FLOTA / NEUMÁTICOS</span><h1 id="page-title">Tablero del turno</h1></div>
      <div class="top-actions"><span class="date-label" id="today"></span><button class="btn primary" id="new-order">＋ Nueva orden</button></div>
    </header>

    <section class="tab-page active" id="dashboard">
      <p class="intro">Flota ordenada por horas de vida útil remanente. Selecciona un neumático para consultar su ficha y registrar una medición.</p>
      <div class="stats-grid">
        <article class="stat-card"><div class="stat-heading"><span class="dot red"></span> ROJO</div><strong id="red-count">0</strong><p>Menos de 200 horas: priorizar retiro</p></article>
        <article class="stat-card"><div class="stat-heading"><span class="dot yellow"></span> AMARILLO</div><strong id="yellow-count">0</strong><p>Menos de 500 horas: planificar intervención</p></article>
        <article class="stat-card"><div class="stat-heading"><span class="dot green"></span> VERDE</div><strong id="green-count">0</strong><p>Más de 500 horas remanentes</p></article>
        <article class="stat-card"><div class="stat-heading"><span class="dot gray"></span> SIN DATOS</div><strong id="nodata-count">0</strong><p>Sin mediciones para proyectar</p></article>
      </div>
      <div class="toolbar">
        <input id="tire-search" placeholder="Buscar por serial, camión o modelo…">
        <select id="zone-filter"><option value="all">Todas las zonas</option><option value="red">Rojo</option><option value="yellow">Amarillo</option><option value="green">Verde</option><option value="nodata">Sin datos</option></select>
        <select id="rate-filter"><option value="all">Cualquier tasa</option><option value="observed">Tasa observada</option><option value="nominal">Tasa nominal</option></select>
      </div>
      <div class="table-wrap"><table><thead><tr><th>CAMIÓN</th><th>POS.</th><th>SERIAL</th><th>PROFUNDIDAD</th><th>TASA RECIENTE</th><th>TASA SEGÚN</th><th>HORAS REMANENTES</th><th>ZONA</th><th>ÚLTIMA MEDICIÓN</th></tr></thead><tbody id="tire-table"></tbody></table></div>
      <p class="footnote">La proyección es una estimación basada en la profundidad, el umbral de retiro y la tasa de desgaste seleccionada. Validar siempre según los criterios técnicos y de seguridad de la operación.</p>
    </section>

    <section class="tab-page" id="trucks">
      <p class="intro">Seis posiciones por camión. Selecciona una posición para abrir la ficha del neumático y registrar una nueva medición.</p>
      <div class="toolbar"><input id="truck-search" placeholder="Buscar por camión, modelo, serial o zona…"></div>
      <div id="truck-list" class="truck-list"></div>
    </section>

    <section class="tab-page" id="orders">
      <p class="intro">Cada orden conserva la medición y la proyección que la originaron, dejando trazabilidad para el taller, la reunión semanal y el proveedor.</p>
      <div class="stats-grid order-stats">
        <article class="stat-card"><div class="stat-heading">PROGRAMADA</div><strong id="scheduled-count">0</strong></article>
        <article class="stat-card"><div class="stat-heading">EJECUTADA</div><strong id="done-count">0</strong></article>
        <article class="stat-card"><div class="stat-heading">ANULADA</div><strong id="cancelled-count">0</strong></article>
      </div>
      <div class="toolbar"><input id="order-search" placeholder="Buscar por orden, serial, camión o nota…"><select id="order-status"><option value="all">Todos los estados</option><option>Programada</option><option>Ejecutada</option><option>Anulada</option></select><select id="order-type"><option value="all">Todos los tipos</option><option>Retiro</option><option>Rotación</option><option>Inspección</option></select></div>
      <div class="table-wrap"><table><thead><tr><th>ORDEN</th><th>NEUMÁTICO</th><th>INTERVENCIÓN Y NOTA</th><th>PROGRAMADA</th><th>HORAS AL EMITIR</th><th>ORIGEN</th><th>ESTADO</th><th>ACCIONES</th></tr></thead><tbody id="order-table"></tbody></table></div>
    </section>
  </main>

  <dialog id="tire-dialog">
    <form method="dialog" class="dialog-close"><button class="close-btn" aria-label="Cerrar">×</button></form>
    <div id="tire-detail"></div>
  </dialog>

  <dialog id="order-dialog">
    <form id="order-form" class="modal-form">
      <div class="modal-heading"><div><span class="eyebrow">GESTIÓN DE MANTENIMIENTO</span><h2>Nueva orden de trabajo</h2></div><button type="button" class="close-btn" id="close-order">×</button></div>
      <label>Neumático<select id="order-tire" required></select></label>
      <div class="form-grid"><label>Tipo de intervención<select id="order-kind"><option>Retiro</option><option>Rotación</option><option>Inspección</option></select></label><label>Fecha programada<input id="order-date" type="date" required></label></div>
      <label>Responsable / turno<input id="order-shift" placeholder="Ej. Turno A, 08:00–12:00"></label>
      <label>Nota y coordinación<textarea id="order-note" rows="3" placeholder="Motivo, coordinación con taller, proveedor, despacho…"></textarea></label>
      <div class="form-actions"><button type="button" class="btn secondary" id="cancel-order">Cancelar</button><button class="btn primary" type="submit">Guardar orden</button></div>
    </form>
  </dialog>

  <dialog id="add-tire-dialog">
    <form id="add-tire-form" class="modal-form">
      <div class="modal-heading"><div><span class="eyebrow">FLOTA / POSICIÓN VACÍA</span><h2>Registrar neumático</h2></div><button type="button" class="close-btn" id="close-add-tire">×</button></div>
      <div class="form-grid">
        <label>Camión<select id="add-truck" required></select></label>
        <label>Posición<select id="add-pos" required><option value="1">P1</option><option value="2">P2</option><option value="3">P3</option><option value="4">P4</option><option value="5">P5</option><option value="6">P6</option></select></label>
      </div>
      <label>Serial del neumático<input id="add-serial" required placeholder="Ej. 5980R63-0000-0000"></label>
      <label>Modelo<input id="add-model" required value="Cat 793F"></label>
      <div class="form-grid">
        <label>Profundidad (mm)<input id="add-depth" type="number" min="0" max="100" step=".1" placeholder="Ej. 32.5"></label>
        <label>Tasa observada (mm/100 h)<input id="add-rate" type="number" min=".01" max="20" step=".01" placeholder="Ej. 1.3"></label>
      </div>
      <label>Umbral de retiro (mm)<input id="add-threshold" type="number" min="0" max="100" step=".1" value="10" required></label>
      <div class="form-actions"><button type="button" class="btn secondary" id="cancel-add-tire">Cancelar</button><button class="btn primary" type="submit">Guardar neumático</button></div>
    </form>
  </dialog>

  <div id="toast" role="status"></div>
  <script src="app.js"></script>
</body>
</html>



