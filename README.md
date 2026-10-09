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
