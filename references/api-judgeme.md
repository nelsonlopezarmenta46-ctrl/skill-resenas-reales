# API de Judge.me: lo que conviene saber

Para leer o crear reseñas reales por script (por ejemplo, subir las respuestas ya autorizadas sin pasar por el CSV). Confirma siempre los campos en la documentación vigente: https://judge.me/api/docs

## Acceso

- Base: `https://judge.me/api/v1`
- Autenticación por parámetros: `api_token=<token privado>` y `shop_domain=<tu-tienda>.myshopify.com`.
- El token se saca en Judge.me → Configuración → Integraciones → «Ver token de API». Hay un token público y uno privado; para escribir se usa el privado.
- **El token es una contraseña.** No lo pegues en el chat, no lo guardes en un repositorio, no lo dejes en un archivo compartido. Guárdalo en una variable de entorno (`JUDGEME_API_TOKEN`) y léelo desde ahí.
- `shop_domain` es el dominio interno `.myshopify.com`, no el dominio público. La URL del admin de Shopify puede llevar un identificador distinto del dominio interno (por ejemplo, un sufijo numérico); si da 404, revisa el dominio exacto en Shopify → Configuración → Dominios.

## Qué se puede hacer

- Leer: `GET /reviews?per_page=100&page=N` (paginado). Útil para exportar, auditar duplicados o ver qué ya se publicó.
- Crear: `POST /reviews`. Campos habituales: `shop_domain`, `platform` (`shopify`), `name`, `email`, `rating`, `title`, `body`, `id` (ID del producto en Shopify), `url` (URL del producto) y `picture_urls`. Revisa en la documentación cuáles aplican a tu caso.

## Trampas que ya hicieron perder tiempo

1. **No hay DELETE.** `DELETE /api/v1/reviews/:id` devuelve 404. Borrar una reseña solo se puede desde el admin de Judge.me: busca una frase literal del texto, menú «...» → «Eliminar reseña» y confirma en el modal. El botón de confirmación del modal tiene el mismo nombre que la opción del menú; apunta al último. Consecuencia práctica: prueba con una sola reseña real antes de lanzar un lote.
2. **Ignora `created_at`.** Toda reseña creada por API se fecha el día de hoy. Si necesitas conservar la fecha real de una respuesta, usa el CSV (`review_date`). No ocultes las fechas de las reseñas para aparentar que son más antiguas o más recientes; si las ocultas, que sea una decisión de diseño para todas.
3. **Un campo desconocido rompe el trabajo en silencio.** La API puede responder `201 Created` y la reseña nunca aparecer. Envía solo campos documentados y verifica después cuántas reseñas aparecen en el admin contra cuántas enviaste.
4. **Límite de velocidad:** unos 12 segundos entre `POST` para no recibir 429. En un lote, espera entre peticiones y reintenta con pausa creciente.
5. **El iframe del admin se cae** si entras directo a `/apps/judgeme/reviews`. Entra por `/apps/judgeme/home` y navega desde la barra lateral de la app.
6. **Verificación:** las reseñas creadas por API o CSV no reciben la insignia de «Verified». Solo la tienen las que nacen de una solicitud de Judge.me a un comprador. No hay parámetro para forzarla.
7. **Fotos:** `picture_urls` tiene que ser público. Si la URL no se puede descargar, la reseña entra sin foto y sin aviso.
8. **Mismas reglas de contenido que el CSV:** permiso del cliente, texto fiel, estrella que puso la persona.

## Patrón seguro para un lote

1. Prepara el CSV con la plantilla y revisa filas y permisos (`de-whatsapp-a-csv.md`).
2. Crea una sola reseña por API como prueba. Ábrela en el admin y en la página del producto.
3. Si salió bien, envía el resto con pausa de 12 segundos o más entre peticiones.
4. Al terminar, cuenta en el admin y compara con el número de filas enviadas.
5. Guarda la lista de reseñas enviadas (ID de fila, fecha, respuesta de la API) por si hay que borrar algo a mano.

Para menos de 50 reseñas, el CSV desde el admin suele ser más simple y más seguro que la API.
