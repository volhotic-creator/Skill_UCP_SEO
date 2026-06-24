# Mercado Libre — Criterios Generales para Títulos SEO

Fuentes:
- https://vendedores.mercadolibre.com.ar/nota/como-hacer-un-buen-titulo-para-tu-publicacion
- https://developers.mercadolibre.com.ar/es_ar/categorias-y-atributos
- https://global-selling.mercadolibre.com/learning-center/news/how-to-create-a-good-title-for-your-listing

> **Para autopartes**: ver también `/references/autopartes-structures.md` para criterios y estructuras específicas de la categoría, incluido el sistema de Compatibilidades.

---

## Estructura del título

### Formato base

```
[Tipo de producto]  [Marca del producto]  [Posición?]  [Atributos diferenciadores]
```

Las primeras palabras del título tienen mayor peso en el ranking de búsqueda de ML. El tipo de producto (qué es el ítem) debe ir primero.

### Longitud

- No existe un mínimo global definido por ML
- El **máximo varía por categoría** — verificar via API:
  ```
  GET /categories/{category_id}/attributes → max_title_length
  ```
- Categorías de autopartes ML Argentina: **60 caracteres**
- Buena práctica: usar la mayor parte del límite disponible incluyendo los atributos más relevantes

---

## Prohibiciones — clasificadas por consecuencia

### Causan rechazo de la publicación

❌ Texto en mayúsculas — `MEJOR PRODUCTO` → debe ser `Mejor producto`
❌ Símbolos y puntuación decorativa — `★`, `✓`, `>>>`, `---`, `!!!`
❌ Precio en el título — `Camisa azul $5.000`
❌ Condiciones de pago — `12 cuotas sin interés`, `3 MSI`
❌ Condición del producto — `nuevo`, `usado`, `reacondicionado` (va en el campo `condition`)
❌ Información de envío — `envío gratis`, `entrega en 24hs`, `full`
❌ Texto promocional — `Oferta`, `30% OFF`, `Precio especial`, `Liquidación`
❌ Puntuación innecesaria — puntos, comas, guiones usados como decoración

### Pueden derivar en suspensión de cuenta

❌ Comparaciones de marca — `similar a [Marca]`, `tipo [Marca]`, `estilo [Marca]`, `igual a [Marca]`
❌ Marcas de competidores sin ser distribuidor autorizado
❌ Indicadores de falsificación — `réplica`, `copia`, `imitación`, `fake`, `AAA`
❌ Copiar títulos o descripciones de otros vendedores

---

## Algoritmo de búsqueda de ML

### Factores de posicionamiento (mayor a menor impacto)

1. **Reputación del vendedor** — factor #1 general en ML
2. **Calidad del título** — factor #1 dentro del listado
3. **Completitud del listado** — ficha técnica, descripción, imágenes
4. **Conversión** — el algoritmo favorece listados que convierten
5. **Velocidad de ventas** — ítems con más ventas tienen ventaja progresiva
6. **Satisfacción del comprador** — respuesta a consultas, calificaciones

### Cómo el algoritmo procesa el título

- Cada palabra tiene peso de búsqueda; las primeras palabras pesan más
- El sistema matchea la query del comprador contra las palabras del título
- ML procesa más de 4.000 búsquedas por segundo; el 70% de compradores no pasa de la primera página

---

## Reglas sobre variantes y color

### Variantes (colores, tallas, capacidades)

Cuando un producto existe en múltiples variantes (colores, tallas, etc.):
- **No** crear un listado por variante
- Usar el sistema de **variaciones** (`variations`) de ML dentro de un único listado
- **No** incluir la variante en el título si hay múltiples opciones

Incluir el atributo de variante en el título **solo cuando el producto existe en una única opción** (un solo color, una sola talla, etc.).

### Categoría autopartes — variantes de vehículo

En autopartes, la "variante" es el vehículo compatible. Usar el sistema de **Compatibilidades** de ML (no el sistema de variaciones) para asociar múltiples vehículos a un mismo repuesto. Ver `/references/autopartes-structures.md`.

---

## Políticas adicionales

### Edición del título

| Estado del listado | ¿Editable? |
|---|---|
| `sold_quantity = 0` (sin ventas) | ✅ Sí |
| `sold_quantity > 0` (con ventas) | ❌ No |

Validar el título antes del primer push al feed. Una vez publicado con ventas, el título queda bloqueado.

### Idioma

- **Listados nacionales**: idioma local del país (español; portugués para Brasil)
- **Global Selling**: inglés (programa de venta internacional de ML)

### Validaciones técnicas de ML

| Tipo | Descripción | Bloquea publicación |
|------|-------------|:-------------------:|
| `error` | Problema crítico que viola las reglas | ✅ Sí |
| `warning` | Observación o recomendación | ❌ No |

Verificar validaciones via API antes de publicar en producción.

---

## Checklist de validación general ML

```
[ ] ¿El tipo de producto es la primera palabra del título?
[ ] ¿Tiene marca del producto (si aplica)?
[ ] ¿Longitud dentro del límite de la categoría?
[ ] ¿Sin mayúsculas innecesarias?
[ ] ¿Sin símbolos ni puntuación decorativa?
[ ] ¿Sin precio ni condiciones de pago?
[ ] ¿Sin condición del producto (nuevo/usado)?
[ ] ¿Sin texto de envío ni promocional?
[ ] ¿Sin comparaciones de marca?
[ ] ¿Las variantes están manejadas con el sistema correcto (variations / compatibilidades)?
```

---

## Ejemplos generales

```
❌  NUEVA Camisa OFERTA 30% OFF azul M envío gratis calidad premium
    Problemas: mayúsculas, texto promocional, condición, info de envío, sin marca

✅  Lacoste Camisa Polo Algodón Hombre Azul Marino Talla M
    ✓ Tipo + marca + material + género + color + talla

❌  Zapatilla buena para correr
    Problemas: sin marca, sin modelo, sin atributos diferenciadores

✅  Adidas Ultraboost 22 Zapatilla Running Mujer Blanca Talla 38
    ✓ Tipo + marca + modelo + género + color + talla
```
