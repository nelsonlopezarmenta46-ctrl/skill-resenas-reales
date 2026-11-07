# De respuestas de WhatsApp a CSV de Judge.me

Pasos para convertir lo que los clientes contestaron en un archivo que Judge.me acepte. La plantilla está en `plantillas/resenas-reales.csv`.

## Antes de empezar

Reúne por cada cliente: texto de la respuesta, fecha en que la escribió, estrella (la que él puso o, si solo dio texto, pregúntale), permiso para publicar y para usar su nombre, y las fotos si mandó. Si falta el permiso o la estrella, pregunta; no los supongas.

## Columnas de la plantilla

Las columnas de Judge.me van primero. Las tres últimas son de control interno y no se suben:

| Columna | Qué poner |
| :-- | :-- |
| `product_id` | ID numérico del producto de Shopify |
| `product_handle` | Texto final de la URL del producto. Con uno de los dos basta |
| `title` | Opcional. Frase corta de la propia reseña, no un eslogan |
| `body` | El texto del cliente, con ortografía corregida si hace falta |
| `rating` | La estrella que puso el cliente, entero de 1 a 5 |
| `review_date` | Fecha real de la respuesta, `dd/mm/yyyy` |
| `reviewer_name` | Nombre y letra inicial del apellido, como autorizó («Laura M.») |
| `reviewer_email` | Opcional. No se envía nada a ese correo |
| `picture_urls` | URLs públicas de las fotos, separadas por coma, máximo 5 |
| `reply` / `reply_date` | Respuesta pública de la tienda, sobre todo en reseñas de 1 a 3 estrellas |
| `permiso_publicar` | `si` o `no`. Solo se importan las filas con `si` |
| `fuente` | Dónde llegó: `whatsapp`, `correo`, `formulario`, `judge.me-solicitud` |
| `incentivo` | `ninguno` o la descripción (por ejemplo, `descuento 10 %`). Si hay incentivo, añade al final del `body`: «Reseña a cambio de un descuento» |

## Pasos

1. **Copia el texto tal cual** en `body`. No resumas ni «mejores» el estilo.
2. **Corrige solo lo necesario:** tildes, mayúsculas, errores de tecleo. Si el cliente escribió «a mi me funciono bien, no me duele», queda «A mí me funcionó bien, no me duele». No añadas frases, no uses adjetivos que no usó.
3. **Quita datos personales** del texto: teléfono, dirección, número de guía, nombre completo de terceros. Se reemplazan por nada o por «[dato omitido]».
4. **Conserva las quejas.** Una reseña de 2 estrellas con una queja real se publica y se responde.
5. **No toques la estrella.** Si el texto dice «excelente» y puso 3 estrellas, se pregunta al cliente; no se corrige por tu cuenta.
6. **Nombre:** exactamente como el cliente autorizó. Si no autorizó nombre, deja `reviewer_name` vacío (Judge.me muestra «Anonymous») o usa solo la inicial.
7. **Fecha:** la del día en que respondió, no una más antigua. Si no la tienes, deja la celda vacía y Judge.me pone la de hoy.
8. **Fotos:** prepáralas con `fotos-de-clientes.md`, súbelas a una URL pública y pega las URLs.
9. **Filtra:** quédate con las filas con `permiso_publicar = si` y guarda aparte el resto.
10. **Quita las columnas de control** (`permiso_publicar`, `fuente`, `incentivo`) del archivo que subes, o márcalas como «Skipped» en la pantalla de mapeo.
11. **Guarda un respaldo** del CSV completo con las columnas de control junto con las capturas de los permisos. Son la prueba de que cada reseña es real y está autorizada.
12. **Importa** en Judge.me y revisa en la tienda (ver el último paso del flujo en `SKILL.md`).

## Ejemplo corto de proceso con Python

Solo si el usuario tiene Python a mano y el CSV es largo. Genera el archivo para subir sin las columnas de control y deja aparte las filas sin permiso:

```python
import csv

control = {"permiso_publicar", "fuente", "incentivo"}
with open("resenas-reales.csv", newline="", encoding="utf-8") as f:
    filas = list(csv.DictReader(f))

con_permiso = [r for r in filas if r.get("permiso_publicar", "").strip().lower() == "si"]
sin_permiso = [r for r in filas if r not in con_permiso]

columnas = [c for c in filas[0].keys() if c not in control]
with open("para-subir-a-judgeme.csv", "w", newline="", encoding="utf-8") as f:
    w = csv.DictWriter(f, fieldnames=columnas, extrasaction="ignore")
    w.writeheader()
    w.writerows(con_permiso)

print(f"{len(con_permiso)} filas para subir, {len(sin_permiso)} sin permiso (no se suben)")
```

## Revisión antes de importar

- [ ] Todas las filas tienen `body` y `rating` de 1 a 5.
- [ ] Todas tienen `product_id` o `product_handle`.
- [ ] Ninguna fila sin permiso.
- [ ] Las reseñas de 1 a 3 estrellas siguen en el archivo.
- [ ] Ningún texto fue ampliado ni suavizado respecto al original.
- [ ] Las fechas son reales y están en `dd/mm/yyyy`.
- [ ] Ningún teléfono, dirección ni número de guía quedó en el texto.
- [ ] Las URLs de fotos abren la imagen directa en una ventana privada del navegador.
