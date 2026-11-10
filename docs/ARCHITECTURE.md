# ANNIE — Arquitectura inicial

## Alcance de la fase 1

Esta fase establece los proyectos Flutter para Android y FastAPI, configuración
por entorno y una comprobación de salud. No incluye autenticación, conexión real
a Supabase, procesamiento de imágenes, IA ni lógica de producto.

## Componentes previstos

- **Aplicación móvil:** Flutter y Dart. Presentación y navegación organizadas por
  funcionalidad conforme crezca el producto.
- **API:** FastAPI y Pydantic, con endpoints delgados y lógica de negocio en
  módulos propios.
- **Persistencia futura:** PostgreSQL administrado por Supabase, con SQLAlchemy
  y migraciones versionadas. La fase 1 define únicamente la base declarativa;
  no abre conexiones.
- **Servicios administrados futuros:** Supabase Auth y Storage.
- **Proveedor de IA futuro:** adaptador del lado del backend; sus credenciales
  nunca se incluirán en la aplicación móvil.

## Estructura inicial

```text
mobile/
  lib/
  test/
  android/
backend/
  app/
    api/routes/
    core/
    db/
  tests/
docs/
```

La aplicación móvil debe usar el backend como frontera para operaciones de
negocio. Se evitarán microservicios y abstracciones innecesarias hasta que el
volumen o la operación justifiquen su introducción.

## Configuración y ejecución

La API obtiene su configuración de variables de entorno y, en desarrollo, del
archivo `backend/.env`, que no debe versionarse. `backend/.env.example` contiene
solo valores de ejemplo no secretos. La URL de PostgreSQL es opcional mientras
no haya conexión real.

`GET /health` confirma que el proceso HTTP responde. No verifica la base de
datos ni servicios externos.

## Rendimiento previsto

El armario se paginará en el backend. La aplicación mostrará miniaturas con carga
progresiva y reservará las imágenes grandes para el detalle. El análisis de IA
será explícito y asíncrono, no se repetirá al abrir el armario.
