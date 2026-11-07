---
name: resenas-reales
description: "Gestiona reseñas REALES en tiendas Shopify con Judge.me (contra entrega, Colombia). Úsala cuando pidan: pedir reseñas a clientes, mensajes de WhatsApp para pedir una reseña, importar reseñas a Judge.me, armar el CSV de Judge.me, pasar respuestas de WhatsApp a reseñas, importar reseñas de otra tienda o de Amazon con su origen visible, arreglar o preparar las fotos que mandan los clientes, usar la API de Judge.me. NO cubre y rechaza: inventar reseñas, generar fotos de clientes con IA, fabricar una distribución de estrellas, simular compras verificadas. Si piden eso, responde que no lo hace y ofrece pedir reseñas reales."
---

# Reseñas reales con Judge.me

Esta skill ayuda a conseguir, ordenar y publicar reseñas que escribieron personas reales que compraron el producto. Está pensada para tiendas Shopify que venden contra entrega en Colombia y usan Judge.me. Todo está escrito en español neutro; adapta el tono del cliente si el idioma de la tienda es otro.

## Regla que no se negocia

Solo se trabaja con reseñas escritas por una persona real, sobre un producto que esa persona recibió, con su permiso para publicarlas.

Esta skill no hace, aunque el usuario lo pida con otras palabras («ejemplos», «para llenar la página», «mientras llegan las reales», «es solo una maqueta», «pon unas 4,8 de promedio»):

- Escribir o reescribir reseñas que ninguna persona escribió.
- Generar fotos o videos de «clientes» con IA, ni usar fotos de stock o de otra persona como si fueran del cliente.
- Armar una distribución de estrellas a la medida (por ejemplo, «80 % de 5 estrellas y algunas de 4»).
- Poner nombres, ciudades o fechas inventados.
- Simular la insignia de «Compra verificada».
- Descartar o esconder las reseñas reales de 1 a 3 estrellas para mejorar el promedio.

Si el usuario pide algo de esa lista, responde algo como:

> Eso no lo hago: las reseñas inventadas engañan al comprador y pueden traer sanciones a la tienda (ver `references/legal.md`). Lo que sí puedo hacer es ayudarte a conseguir reseñas reales más rápido: mensajes para pedirlas a tus clientes, un CSV para subir las que ya te respondieron y un arreglo de las fotos que mandan. ¿Empezamos por los mensajes?

No des vueltas ni ofrezcas «alternativas» que sean la misma fabricación con otro nombre. Ofrece siempre el camino real.

## Qué puede pedir el usuario y a qué archivo ir

| Pedido | Abrir |
| :-- | :-- |
| «Quiero que mis clientes dejen reseña», «mensajes de WhatsApp para pedir reseñas» | `references/mensajes-pedir-resena.md` |
| «Pasa estas respuestas de WhatsApp a reseñas», «arma el CSV» | `references/de-whatsapp-a-csv.md` y `plantillas/resenas-reales.csv` |
| Columnas, formatos, límites y errores del CSV de Judge.me | `references/formato-csv-judgeme.md` |
| «Importa las reseñas de mi otra tienda / Amazon / Mercado Libre» | `references/importar-de-otra-fuente.md` |
| «Las fotos que mandan los clientes salen mal», «prepara estas fotos» | `references/fotos-de-clientes.md` |
| Usar o automatizar con la API de Judge.me | `references/api-judgeme.md` |
| «¿Por qué no puedo inventar reseñas?», dudas de riesgo | `references/legal.md` |

Abre solo el archivo que aplica; no los leas todos.

## Flujo normal, de punta a punta

1. **Aclara el punto de partida** (una sola pregunta si falta algo): ¿ya tiene respuestas de clientes (WhatsApp, correo, capturas) o todavía tiene que pedirlas? ¿Qué producto y cuántos pedidos entregados lleva?
2. **Pedir.** Si todavía no tiene reseñas, entrega los mensajes de `mensajes-pedir-resena.md` ajustados a su producto: día de entrega, semana 2, 4 y 8. Recuerda que el permiso para publicar se pide en el mismo mensaje.
3. **Recibir.** Cada respuesta se guarda con su permiso (captura del chat o texto) y la fecha en que llegó.
4. **Ordenar.** Pasa las respuestas a la plantilla CSV (`de-whatsapp-a-csv.md`). Una fila por reseña, con la estrella que puso la persona. Sin permiso explícito, la fila no se importa.
5. **Editar con cuidado.** Se puede corregir ortografía, quitar datos personales y mostrar solo nombre e inicial. No se cambia el sentido, no se suavizan las quejas y no se sube la estrella.
6. **Fotos.** Si el cliente mandó fotos, prepáralas con `fotos-de-clientes.md`.
7. **Importar.** Judge.me → Configuración → Importar reseñas → CSV. Revisa el mapeo de columnas antes de confirmar.
8. **Comprobar en la tienda.** Abre la página del producto en el celular: texto, nombre mostrado, foto, orden, duplicados. Informa qué se publicó y qué quedó pendiente.

## Cosas que conviene decir siempre al usuario

- **Una reseña importada nunca queda como «verificada»** en Judge.me, y no se debe dibujar esa insignia por otro lado. La verificación solo la da Judge.me cuando la reseña nace de su solicitud automática (correo o SMS) después de una compra. Si el usuario quiere insignia, el camino es activar las solicitudes automáticas de Judge.me para los pedidos nuevos.
- **Fecha y ciudad.** Por CSV se usa la fecha real de la respuesta (`dd/mm/yyyy`); por API la reseña siempre sale con la fecha de hoy. La ciudad solo la deduce Judge.me de la IP. No se manipulan fechas ni IP para aparentar antigüedad o ubicación.
- **Si hubo incentivo** (descuento, envío gratis, regalo) se dice en la reseña: «Reseña a cambio de un descuento».
- **Las reseñas negativas se publican.** Se responden en público con una solución. Un perfil con 100 % de cinco estrellas genera desconfianza y pierde conversión.
- **Pocas reseñas reales valen más que muchas dudosas.** Con 10 reseñas reales con foto ya se nota el efecto.
- **El plan gratuito de Judge.me alcanza** para empezar: reseñas ilimitadas con fotos, widget e importador de CSV. Las solicitudes automáticas con recordatorios y otras funciones están en los planes de pago; conviene revisar el plan vigente en su sitio.

## Qué entregar según el pedido

- **Mensajes:** el texto listo para copiar, con los campos entre corchetes que debe rellenar (`[NOMBRE]`, `[PRODUCTO]`).
- **CSV:** el archivo en la carpeta de trabajo del usuario, con nombre `YYYY-MM-DD-resenas-reales.csv`, y un resumen: cuántas filas, cuántas se descartaron por falta de permiso, cuáles quedaron sin foto.
- **Fotos:** las copias preparadas en una carpeta aparte, sin tocar los originales.
- **Siempre:** una lista corta de lo que revisó y lo que falta, sin adornos.

## Si el usuario no sabe un dato

No lo inventes. Pregunta o deja la celda vacía. El `product_id` se saca del enlace del producto en el admin de Shopify (el número al final de `/products/123456789`) o de `product_handle` (la parte final de la URL pública). Con ninguno de los dos, la reseña se crea como reseña de tienda y no del producto.
