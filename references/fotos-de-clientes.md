# Fotos que mandan los clientes

Las fotos reales de clientes son lo que más pesa en una reseña. Casi siempre llegan por WhatsApp: oscuras, torcidas, comprimidas o con datos que no deben publicarse. Aquí se explica cómo dejarlas listas sin cambiar lo que muestran.

## Regla

Se mejora la foto, no su contenido. Se puede recortar, enderezar, aclarar un poco y tapar datos personales. No se generan fotos, no se cambia el producto o el resultado que se ve, no se retoca la piel ni el cuerpo y no se usan fotos de otra persona. Si el cliente no mandó foto, la reseña sale sin foto.

## Antes de publicar

- Confirma que el cliente dio permiso para publicar la foto (el permiso del texto no siempre incluye la imagen). Si no se lo preguntaste, pregúntaselo.
- Si aparece su cara o una parte del cuerpo reconocible, pide permiso expreso o recorta para que no se vea.
- Menores de edad: no se publican sin autorización del adulto responsable.

## Pasos

1. **Copia el original** a una carpeta `originales/`. No se edita ese archivo.
2. **Corrige la orientación** (las fotos de celular suelen salir giradas).
3. **Recorta** a lo importante: el producto, la zona o el resultado. Un recorte cuadrado o 4:5 se ve mejor en el widget.
4. **Aclara de forma sutil.** Si está oscura, sube un poco la exposición y el contraste. No uses filtros fuertes ni cambies el color del producto: el cliente que compre tiene que ver algo parecido a lo que recibirá.
5. **Quita los datos personales:**
   - Nombre y dirección en etiquetas de envío o guías.
   - Número de teléfono, número de guía, código de barras.
   - Caras de terceros, pantallas con chats, matrículas.
   - Se tapan con un recorte o con un bloque liso, no con un difuminado leve que se pueda revertir.
6. **Borra los metadatos** (ubicación GPS, modelo del teléfono, fecha).
7. **Convierte a `.jpg` o `.png`**. Las fotos de iPhone vienen en HEIC y Judge.me no las acepta.
8. **Reduce el tamaño:** lado mayor de 1600 px y calidad cerca de 85 es suficiente.
9. **Sube a una URL pública** y verifica que abre la imagen directa en una ventana privada. Shopify (Contenido → Archivos) sirve.
10. **Pega la URL** en `picture_urls` (máximo 5 por reseña, separadas por coma).

## Comandos útiles

Mac o Linux con ImageMagick (`magick`) y ExifTool:

```bash
# Orientar, reducir y pasar a JPG
magick original.heic -auto-orient -resize "1600x1600>" -quality 85 foto.jpg

# Un poco de luz y contraste (valores suaves)
magick foto.jpg -brightness-contrast 8x6 foto-aclarada.jpg

# Recortar un cuadrado desde la esquina (ancho x alto + x + y)
magick foto.jpg -crop 1200x1200+200+300 +repage foto-recorte.jpg

# Tapar una zona con un bloque liso (por ejemplo, una etiqueta de envío)
magick foto.jpg -fill black -draw "rectangle 100,800 700,950" foto-tapada.jpg

# Quitar metadatos
exiftool -all= -overwrite_original foto-tapada.jpg
```

En Mac, sin instalar nada, `sips` pasa HEIC a JPG y reduce:

```bash
sips -s format jpeg -Z 1600 original.heic --out foto.jpg
```

Si el usuario prefiere hacerlo a mano, la app Fotos del Mac o del celular recorta y aclara, y el editor de Google Fotos tapa zonas.

## Qué decirle al usuario cuando hay problemas

- **Foto muy oscura o borrosa que no mejora:** mejor pedir otra al cliente: «¿Me puedes mandar otra con más luz?». No se «reconstruye» con IA.
- **Muestra la caja o la guía con datos:** se tapan los datos o se recorta.
- **Foto que parece de internet:** no la publiques como del cliente. Haz una búsqueda inversa de imagen si hay duda razonable.
- **Foto de varios productos o antes y después:** se publica tal cual la mandó, sin añadir flechas ni textos que prometan resultados.

## Lo que no se hace

- Generar «clientes» o fotos de resultados con IA, ni usar caras de stock.
- Combinar fotos de dos personas para armar un antes y después.
- Retocar el resultado (piel, cabello, peso, color).
- Poner marcas de agua de otra tienda o de otra persona.
- Publicar la foto de alguien que no la autorizó.
