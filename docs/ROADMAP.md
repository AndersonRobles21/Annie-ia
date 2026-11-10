# ANNIE — Hoja de ruta

## Fase 1 — Fundación

**Alcance:** estructura Flutter Android y FastAPI, configuración por entorno,
base declarativa SQLAlchemy sin conexión y endpoint de salud.

**Aceptación:** `flutter analyze` y `flutter test` pasan; FastAPI inicia;
`GET /health` responde `200` con `{"status":"ok"}`; Pytest pasa; no se
versionan entornos virtuales ni secretos.

## Fase 2 — Persistencia y cuentas

**Alcance:** validar el flujo de Auth de Supabase, modelos, migraciones y
autorización por usuario antes de habilitar CRUD del armario.

**Aceptación:** migraciones reproducibles; peticiones sin identidad válida se
rechazan; un usuario no puede leer ni modificar los datos de otro; secretos solo
en configuración del servidor.

## Fase 3 — Armario e imágenes

**Alcance:** alta, listado paginado y detalle de prendas; carga privada de
fotografías y generación de miniaturas.

**Aceptación:** la lista no descarga originales en bloque; errores de carga son
recuperables; las imágenes privadas no pueden leerse sin autorización.

## Fase 4 — Análisis asistido

**Alcance:** análisis de imágenes asíncrono, validación de resultados y edición
de atributos sugeridos.

**Aceptación:** abrir el armario no dispara análisis; fallos no pierden la
prenda; resultados se validan y pueden corregirse manualmente.

## Fase 5 — Recomendaciones

**Alcance:** candidatos de atuendos con reglas y ranking inicial, valoración y
ajuste gradual por preferencias.

**Aceptación:** combinaciones respetan reglas configuradas; feedback se guarda y
afecta al orden de manera verificable.

## Fase 6 — Avatar y beta

**Alcance:** visualización inicial 2D y endurecimiento de seguridad,
observabilidad y rendimiento.

**Aceptación:** prendas sin representación gráfica tienen una alternativa
clara; pruebas Android y aislamiento de usuarios pasan; el armario se mantiene
utilizable con cientos de elementos y carga progresiva.

Las fechas, límites de carga, objetivos de latencia, política de imágenes y
alcance final del avatar se acordarán antes de las fases correspondientes.
