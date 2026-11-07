# Importar reseñas de otra tienda, Amazon, Mercado Libre u otra fuente

Importar reseñas que ya existen en otro lugar es legítimo solo si se cumplen las tres condiciones siguientes. Si falla alguna, no se importa.

1. **Son reseñas reales** de personas reales sobre ese mismo producto o uno idéntico.
2. **El origen queda visible** para quien lee la reseña. No se presentan como compras de tu tienda.
3. **La plataforma de origen lo permite** y no estás copiando contenido que no puedes usar.

## Casos

### A. Reseñas de otra tienda tuya (mismo producto)

Es el caso más limpio. Ejemplos: cambiaste de dominio, tienes otra tienda con el mismo producto, vienes de otra app de reseñas.

- Exporta las reseñas desde la app de origen (casi todas tienen exportación a CSV). Si la app de origen es Loox, Stamped, Yotpo, Okendo o similar, revisa también el asistente de migración de Judge.me.
- Arma el CSV con el formato de `formato-csv-judgeme.md`. Conserva texto, estrella, nombre mostrado y fecha original.
- Deja claro el origen. Opciones: en `title` o al final de `body` añade «Reseña de nuestra tienda anterior», o agrega una nota cerca del widget («Incluye reseñas de [otra tienda], mismo producto»).
- No mezcles reseñas de productos distintos. Si la otra tienda vendía otra marca o presentación, no cuentan.

### B. Reseñas de una plataforma de terceros (Amazon, Mercado Libre, AliExpress, Google)

Esas reseñas pertenecen a los autores y a la plataforma. Antes de copiar nada:

- Lee los términos de uso de la plataforma. Muchas prohíben extraer o reutilizar sus reseñas fuera de ellas (scraping, copia masiva).
- Revisa si el producto es el tuyo: reseñas de un producto de otro vendedor, aunque se parezca, no son tuyas.
- Usa solo lo que la plataforma entrega por una vía oficial (exportación propia del vendedor, API autorizada) o lo que el autor te permite usar por escrito.

Si es viable, la presentación correcta es citar, no suplantar:

- Texto fiel a la reseña original, con su estrella.
- Origen escrito en la reseña: «Reseña publicada originalmente en Mercado Libre» (con la fecha original si la tienes).
- Sin mostrarla como cliente de tu tienda, sin insignia de compra verificada.
- Nombre como aparece públicamente en el origen o iniciales; nada de nombres cambiados.

Si no puedes cumplir lo anterior, la salida es pedirles la reseña a tus propios clientes (`mensajes-pedir-resena.md`) o, si compraron en esa plataforma, invitar al comprador a repetirla en tu tienda.

### C. Reseñas de redes sociales y comentarios de anuncios

Los comentarios públicos de un anuncio o una publicación se pueden mostrar como captura (con el permiso de la persona y cuidando los datos personales), no como reseñas importadas a Judge.me. Un comentario en Facebook o Instagram no es una reseña de compra.

## Lo que no se hace

- Importar reseñas de un producto que no es el tuyo «porque viene del mismo proveedor» sin que sea verificable que es el mismo artículo y sin decir el origen.
- Cambiar el nombre, la fecha o la estrella de una reseña ajena.
- Traducir de forma que se agregue lo que el autor no dijo. Una traducción fiel está bien y se marca como traducida.
- Reutilizar fotos de clientes de otra tienda sin permiso del autor o sin que la plataforma las ofrezca para reutilizar.
- Repetir la misma reseña en varios productos.

## Revisión antes de importar

- [ ] Está documentado de dónde viene cada lote (tienda, plataforma, fecha de exportación).
- [ ] El origen se ve en cada reseña o junto al widget.
- [ ] Ninguna reseña aparece como compra verificada de tu tienda.
- [ ] Texto y estrellas están igual que en el origen.
- [ ] El producto de origen y el tuyo son el mismo artículo.
- [ ] Los términos de la plataforma de origen permiten el uso.
- [ ] Se puede explicar a un cliente o a una autoridad de dónde salió cada reseña.
