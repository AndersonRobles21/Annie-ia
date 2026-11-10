# ANNIE — Diseño inicial de datos

La base propuesta es PostgreSQL. Supabase administrará el servicio; SQLAlchemy
representará los modelos y las migraciones versionarán los cambios de esquema.
En la fase 1 no se configura ni se abre una conexión. `backend/.env.example`
deja `DATABASE_URL` vacío.

## Entidades previstas

| Entidad | Campos principales | Relaciones |
|---|---|---|
| `profiles` | `user_id`, nombre visible, preferencias, fechas | Una por usuario de Auth |
| `garments` | `id`, `user_id`, categoría, subcategoría, colores, estado, fechas | Pertenece a un perfil |
| `garment_images` | `id`, `garment_id`, claves de original y miniaturas, dimensiones | Una prenda puede tener varias imágenes |
| `image_analysis_jobs` | `id`, `user_id`, `garment_id`, estado, intentos, fechas | Trabajo asíncrono de análisis |
| `outfits` | `id`, `user_id`, nombre, contexto, origen, fecha | Pertenece a un perfil |
| `outfit_items` | `outfit_id`, `garment_id` | Relaciona prendas con atuendos |
| `outfit_feedback` | `id`, `user_id`, `outfit_id`, valoración, fecha | Valoración del usuario |
| `user_preferences` | `user_id`, preferencia, valor controlado | Preferencias declaradas o aprendidas |

## Reglas de diseño

- Identificadores UUID; relaciones explícitas y restricciones de integridad.
- Incluir `user_id` en entidades del usuario para autorización y consultas
  eficientes.
- Índices en propietario, estado y columnas de ordenamiento que respalden
  consultas reales.
- Listar prendas con orden estable y paginación por cursor.
- Guardar imágenes en Storage privado, no como blobs de PostgreSQL. La base
  contiene sus claves y metadatos.
- Usar campos relacionales para los atributos consultables; reservar JSONB para
  metadatos variables puntuales.
- Definir migraciones y política coordinada de borrado de metadatos y archivos
  antes de habilitar persistencia en producción.
- Aplicar políticas de Row Level Security cuando las tablas estén expuestas a
  clientes de Supabase; el backend también verificará propiedad.

## Configuración futura

`DATABASE_URL` será opcional en esta fase y solo se configurará al implementar
persistencia. La URL real debe mantenerse fuera de Git y de la aplicación
móvil. No hay migraciones ni tablas creadas todavía.
