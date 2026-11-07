# skill-resenas-reales

Skill de Claude Code para pedir, ordenar e importar **reseñas reales** en tiendas Shopify con Judge.me, pensada para venta contra entrega en Colombia.

Qué hace:

- Redacta los mensajes de WhatsApp para pedir una reseña (día de entrega, semana 2, 4 y 8), con el permiso para publicar incluido.
- Convierte las respuestas de los clientes en un CSV listo para Judge.me, con columna de permiso y de fuente.
- Prepara las fotos que mandan los clientes (recorte, luz, datos personales fuera).
- Importa reseñas de otra tienda o de otra plataforma solo con su origen visible.
- Explica las limitaciones de Judge.me (verificación, fechas, API).

Qué no hace: inventar reseñas, generar fotos de clientes con IA ni fabricar una distribución de estrellas. Si se le pide, responde que no y ofrece el camino real.

## Instalación

Mac o Linux:

```bash
git clone https://github.com/nelsonlopezarmenta46-ctrl/skill-resenas-reales ~/.claude/skills/resenas-reales
```

Windows (PowerShell):

```powershell
git clone https://github.com/nelsonlopezarmenta46-ctrl/skill-resenas-reales $HOME\.claude\skills\resenas-reales
```

O dile a Claude Code: «Instala esta skill: https://github.com/nelsonlopezarmenta46-ctrl/skill-resenas-reales»

Reinicia Claude Code (o abre una sesión nueva). Para actualizarla más adelante: `git -C ~/.claude/skills/resenas-reales pull`.

## Cómo se usa

Escríbele a Claude con frases como:

- «Arma los mensajes de WhatsApp para pedirles reseña a mis clientes de [producto]».
- «Pasa estas respuestas de WhatsApp a un CSV para importar en Judge.me» (pega las respuestas o indica la carpeta con las capturas).
- «Tengo unas fotos que me mandaron los clientes, prepáralas para subirlas a las reseñas».

También se activa con «importar reseñas de mi otra tienda» o «cómo uso la API de Judge.me».

## Contenido

```
SKILL.md                         reglas y flujo
references/
  formato-csv-judgeme.md         columnas, formatos y errores del CSV
  mensajes-pedir-resena.md       mensajes de WhatsApp
  de-whatsapp-a-csv.md           pasos y revisión previa
  importar-de-otra-fuente.md     otra tienda, Amazon, Mercado Libre
  fotos-de-clientes.md           preparar fotos de clientes
  api-judgeme.md                 trampas de la API
  legal.md                       por qué no se inventan reseñas
plantillas/resenas-reales.csv    plantilla con filas de ejemplo
```

Esta skill no tiene relación oficial con Judge.me ni con Shopify. Judge.me puede cambiar su importador o sus planes: confirma los detalles en su centro de ayuda.
