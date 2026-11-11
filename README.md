# MedAsist Web

Prototipo web del asistente de estudio de medicina: chat con Gemini, dictado activado por el usuario y lectura en voz alta del navegador.

## Publicación de la interfaz

El flujo de GitHub Actions publica únicamente la carpeta `frontend/`. En el repositorio, abrí **Settings → Pages** y seleccioná **GitHub Actions** como fuente. La página es pública y no ejecuta Python.

## Backend de Gemini

El backend está en `backend/app.py`. Para probarlo localmente, desde la raíz del proyecto:

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r backend/requirements.txt
Copy-Item backend/.env.example .env
```

Guardá `GEMINI_API_KEY` en el archivo local `.env` y ejecutá:

```powershell
uvicorn backend.app:app --reload
```

Abrí <http://127.0.0.1:8000>. **No subas `.env` ni pongas la clave en JavaScript.**

Para conectar GitHub Pages, hay que desplegar este backend en un servicio Python, guardar allí `GEMINI_API_KEY` como secreto y configurar `ALLOWED_ORIGINS` con el origen de Pages. Después se agrega la URL pública del backend en `frontend/config.js`. Antes de abrir el backend al público, configurá autenticación o límites de uso para evitar consumo no autorizado de la API.

## Privacidad y alcance

- El dictado inicia solo al pulsar el micrófono; el navegador puede usar un servicio remoto de reconocimiento.
- Las consultas se envían a Gemini a través del backend. No incluyas datos identificables de pacientes.
- El historial se conserva solo en memoria mientras la pestaña está abierta.
- La aplicación es educativa; no reemplaza la atención profesional.
