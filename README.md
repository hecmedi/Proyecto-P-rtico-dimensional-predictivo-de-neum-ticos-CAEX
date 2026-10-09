# Proyecto-Portico-dimensional-predictivo-de-neumaticos-CAEX
 Medir cada CAEX en tránsito con un pórtico instrumentado, mantener la historia dimensional por serial y proyectar las horas de vida útil remanente de cada neumático, para programar el retiro antes de que falle.
# Control de desgaste de neumáticos CAEX

Sistema que mide por imágenes el desgaste de neumáticos de camiones mineros (CAEX), proyecta las horas remanentes y permite agendar la intervención en taller, dejando trazabilidad para la reunión semanal y la negociación con el proveedor.

## Flujo (4 pantallas)
1. **Tablero del turno**: neumáticos ordenados por horas restantes, con semáforo.
2. **Ficha del neumático**: profundidad por pasada, umbral de retiro y proyección.
3. **Agendar intervención**: ventanas del taller y verificación de margen.
4. **Orden emitida**: OT, ventana elegida y trazabilidad (pasada, versión del modelo).

## Estructura
```
frontend/   Prototipo navegable (HTML + JS, datos de ejemplo)
backend/    API FastAPI: proyección, semáforo, ventanas, órdenes
docs/       Arquitectura y hoja de ruta
```

## Cómo ejecutar
Frontend: abrir `frontend/index.html` en el navegador.

Backend:
```bash
cd backend
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload      # http://localhost:8000/docs
pytest
```

## Estado
Ver [CHANGELOG.md](CHANGELOG.md) y [docs/ARQUITECTURA.md](docs/ARQUITECTURA.md).

# Avances

## v0.1 (actual)
- [x] Wireframe de 4 pantallas definido
- [x] Prototipo frontend navegable con datos de ejemplo (`frontend/index.html`)
- [x] Backend base con datos de ejemplo: proyección lineal, semáforo, ventanas, creación de órdenes
- [x] Pruebas unitarias de proyección y semáforo

## Pendiente
- [ ] Conectar el frontend a la API (reemplazar los datos de ejemplo)
- [ ] Base de datos real (PostgreSQL) y migraciones
- [ ] Captura de imágenes y modelo de visión (detección, OCR del serial, profundidad, daños)
- [ ] Validación de las mediciones contra medición manual en terreno
- [ ] Integración con el ERP y notificación al taller
- [ ] Autenticación y roles (planificador, taller)
- [ ] Despliegue con Docker Compose

# Arquitectura

**Frontend** (React/Vite a futuro; hoy HTML + JS) → **API FastAPI** → **PostgreSQL**
La **visión por computador** corre como proceso aparte y escribe mediciones en la base.

## Rutas del frontend
`/` tablero · `/neumatico/:serial` ficha · `/agendar/:serial` agenda · `/orden/:id` orden

## Modelo de datos
- `neumatico`: serial, marca, caex, posicion, umbral_retiro_mm
- `medicion`: neumatico_id, fecha_pasada, horas_operacion, profundidad_mm, imagen_url, modelo_version
- `dano`: neumatico_id, tipo, fecha
- `ventana_taller`: fecha, turno, cupos_totales, cupos_ocupados
- `orden_trabajo`: codigo, neumatico_id, ventana_id, medicion_id, estado, creada_en

## API
| Método | Ruta | Descripción |
|---|---|---|
| GET | `/turnos/{fecha}/neumaticos` | Lista con horas restantes y semáforo |
| GET | `/neumaticos/{serial}` | Ficha, historial y proyección |
| GET | `/neumaticos/{serial}/ventanas` | Ventanas con indicador de margen |
| POST | `/ordenes` | Crea la orden de trabajo |

## Proyección
Regresión lineal de profundidad contra horas de operación. Horas remanentes = (horas al cruzar el umbral) - (horas actuales). Semáforo: rojo < 300 h, amarillo < 600 h, verde el resto (valores a validar con mantenimiento).

## Visión por computador (hoja de ruta)
1. Captura fija en el punto de pasada. 2. Detección de neumático y lectura del serial (detector + OCR). 3. Profundidad: sensor láser o perfil 3D (preferible) o modelo solo con imágenes. 4. Detección de daños. 5. Registro con `modelo_version` para trazabilidad.
Validar siempre contra medición manual: polvo, barro y luz afectan la precisión.

file:///C:/Users/hecto/AppData/Local/Temp/6eae35f5-04d6-4399-8deb-9c4b7cb5be9a_neumaticos-caex-repo.zip.e9a/neumaticos-caex/frontend/index.html
