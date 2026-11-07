# Formato del CSV de Judge.me

Referencia para armar el archivo que se sube en Judge.me. Los nombres de columna conviene dejarlos tal cual: así el mapeo se resuelve solo. Si Judge.me cambia algo, manda su plantilla oficial («Importing reviews using Judge.me template» en su centro de ayuda).

## Encabezado recomendado

```
product_id,product_handle,title,body,rating,review_date,reviewer_name,reviewer_email,picture_urls,reply,reply_date
```

Con una de las columnas de producto basta. Columnas avanzadas opcionales: `ip_address`, `CF_<pregunta>` (formularios personalizados, solo en planes de pago).

| Dato | Columna | Notas |
| :-- | :-- | :-- |
| Producto | `product_id` (recomendado), `product_handle` o `product_url` | Con las tres vacías se crea una reseña de tienda, no de producto. Es el error más común |
| Título | `title` | Opcional |
| Texto | `body` | **Obligatorio**, máximo 5.000 caracteres. Una reseña solo con estrellas se rechaza |
| Puntuación | `rating` | **Obligatorio**, entero de 1 a 5. Nada de 4,5 |
| Fecha | `review_date` | Formato `dd/mm/yyyy`. Usa la fecha real en que el cliente respondió. Vacía = fecha de hoy |
| Nombre | `reviewer_name` | Opcional, máximo 100 caracteres. Vacío = «Anonymous». Se recomienda nombre y letra inicial del apellido |
| Correo | `reviewer_email` | Opcional. No se envía ningún correo al importar |
| Fotos | `picture_urls` | URLs públicas separadas por coma, hasta 5 por reseña |
| Respuesta de la tienda | `reply`, `reply_date` | Respuesta pública. Úsala sobre todo en las reseñas negativas |

## Reglas de las fotos

- Solo `.jpg`, `.jpeg` y `.png`. Los videos no se importan: Judge.me los ignora sin avisar.
- La URL tiene que ser pública y abrir la imagen directa. Los enlaces de «vista» de Google Drive o Dropbox suelen fallar. Una opción gratuita es subir las fotos a Shopify (Contenido → Archivos) y copiar la URL de `cdn.shopify.com`.
- Las fotos se descargan después de importar; pueden tardar de minutos a horas. Si la URL no era pública, la reseña queda sin foto y no hay aviso de error.
- Preparación de las imágenes: `fotos-de-clientes.md`.

## Lo que el CSV no puede hacer

- **No existe columna de «verificado».** Todo lo importado queda sin la insignia de compra verificada, por CSV y por API. Es una limitación de Judge.me y no se contorna.
- **No hay columna de ciudad.** Judge.me solo la deduce de `ip_address`. No pongas IP que no sean las del cliente: sería fabricar un dato.
- **No hay columna de estado** (aprobada, pendiente). Las reseñas importadas se publican de inmediato.

## Dónde se sube

Shopify Admin → Apps → Judge.me → Configuración → Importar reseñas → «Import from a spreadsheet». Acepta CSV, XLS y XLSX; recomiendan CSV en UTF-8, hasta 100 MB. Después sale una pantalla de mapeo de columnas: las que no uses (por ejemplo `permiso_publicar` o `fuente` de la plantilla de este repo) se marcan como «Skipped».

Para que las reseñas se vean, el widget de Judge.me tiene que estar instalado en el tema (bloque en la página de producto). Importar no instala el widget.

## Errores frecuentes

- **Fila rechazada:** `body` vacío o `rating` fuera de 1 a 5.
- **Reseñas que aparecen como de tienda:** las columnas de producto estaban vacías o mal escritas.
- **`product_url` falla** con enlaces del admin, tildes, `%` o símbolos como ™. Usa `product_id`.
- **«Review already exists»** al reimportar un archivo exportado de Judge.me: borra la columna `metaobject_handle`.
- **Caracteres raros (ñ, tildes):** abre el CSV en Google Sheets y descárgalo de nuevo como CSV, o guarda en UTF-8.
- **La primera fila no puede estar vacía.**
- **Volumen alto:** existe un tope diario de reseñas por tienda. Si vas a subir cientos de una vez, escribe a soporte de Judge.me antes.
- **Duplicados:** si importas dos veces el mismo archivo, se duplican. Antes de subir, revisa en Judge.me qué ya existe.
