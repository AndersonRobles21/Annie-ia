# ANNIE — Requisitos iniciales

## Plataforma y tecnologías

- Aplicación Flutter/Dart para Android.
- API Python/FastAPI con esquemas Pydantic.
- SQLAlchemy como base de acceso relacional, inicialmente sin conexión.
- PostgreSQL mediante Supabase en una fase posterior.
- Supabase Auth y Supabase Storage previstos; todavía no integrados.
- Pruebas móviles con Flutter Test y backend con Pytest.

## Requisitos transversales

- Configuración por entorno; ningún secreto ni clave privada en el cliente móvil
  ni en el repositorio.
- Mantener aislados los datos y archivos de cada usuario cuando se incorporen
  autenticación y almacenamiento.
- Paginar listados y cargar imágenes de manera progresiva para armarios de
  cientos de prendas.
- No llamar a un proveedor de IA cada vez que se abra el armario.
- Mostrar errores recuperables y estados de carga en las operaciones de red.

## Alcance entregado en fase 1

- Esqueleto Flutter preparado para Android.
- Aplicación FastAPI con `GET /health`.
- Configuración inicial de Pydantic Settings y clase base de SQLAlchemy.
- Plantilla `.env.example`, dependencias del backend y pruebas de salud.
- Sin autenticación, base de datos real, integración Supabase, IA ni funciones
  completas del armario.

## Requisitos por confirmar antes de una beta

- Flujo de registro y recuperación de cuenta.
- Consentimiento, retención y eliminación de fotografías.
- Límites de archivos y formatos de imagen admitidos.
- Categorías de prendas, filtros y paginación del armario.
- Calidad y explicación esperadas de las recomendaciones.
- Alcance visual y opciones del avatar.
- Proveedor de análisis de imágenes, capacidades, costos y condiciones de datos.
