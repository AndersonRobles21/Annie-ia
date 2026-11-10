# ANNIE — Asistente Inteligente de Vestuario

Proyecto independiente con aplicación Flutter para Android y backend FastAPI.
La fundación actual incluye un esqueleto móvil, configuración inicial de la API
y `GET /health`; todavía no integra autenticación, base de datos, Supabase, IA ni
funciones completas del armario.

## Requisitos previos

- Windows, Android SDK y Flutter/Dart configurados.
- Python 3.12 o posterior.
- Entorno virtual existente en `.venv\`.

## Preparar el backend (Windows CMD)

Desde la raíz del repositorio:

```bat
call .venv\Scripts\activate.bat
python -m pip install -r backend\requirements-dev.txt
copy backend\.env.example backend\.env
cd backend
python -m uvicorn app.main:app --reload
```

La API queda disponible en `http://127.0.0.1:8000`; la comprobación es
`http://127.0.0.1:8000/health` y la documentación interactiva está en
`http://127.0.0.1:8000/docs`. El endpoint de salud confirma que la API responde,
no comprueba servicios externos ni una base de datos.

Para ejecutar las pruebas desde la raíz, en otra ventana CMD:

```bat
call .venv\Scripts\activate.bat
python -m pytest
```

## Ejecutar y validar Flutter

Desde la raíz:

```bat
cd mobile
flutter pub get
flutter analyze
flutter test
flutter run
```

Conecta un dispositivo Android o inicia un emulador. La aplicación Flutter de
esta fase es el proyecto inicial generado por Flutter.

## Configuración y seguridad

`backend\.env.example` contiene valores de ejemplo. El archivo local
`backend\.env` se excluye de Git; no agregues credenciales ni claves reales al
repositorio o a la aplicación móvil. `DATABASE_URL` queda vacío hasta que se
implemente la conexión a una base de datos.

## Documentación

- [Arquitectura](docs/ARCHITECTURE.md)
- [Requisitos](docs/REQUIREMENTS.md)
- [Diseño de datos](docs/DATABASE.md)
- [Hoja de ruta](docs/ROADMAP.md)
