# Mercado Libre — Criterios para Títulos SEO de Productos

Fuentes: https://global-selling.mercadolibre.com · https://developers.mercadolibre.com

---

## ¿Por qué importa el título en Mercado Libre?

El título es el elemento de mayor impacto en el posicionamiento de un listado dentro de la búsqueda de ML. MercadoLibre procesa más de 4.000 búsquedas por segundo y el 70% de los compradores nunca pasa de la primera página de resultados. Un título mal construido reduce la visibilidad del listado incluso si los demás atributos son correctos.

---

## Criterios de construcción del título

### 1. Estructura recomendada

Formato base por categoría:

| Categoría | Estructura ideal |
|-----------|-----------------|
| Electrónica / Tecnología | Marca + Modelo + Tipo de producto + Specs clave |
| Smartphones | Marca + Modelo + Almacenamiento + RAM + Color |
| Ropa | Marca + Tipo + Género + Color + Talla/Material |
| Calzado | Marca + Modelo + Tipo + Género + Talla |
| Alimentos | Marca + Nombre + Variante/Sabor + Peso/Cantidad |
| Hogar | Marca + Material + Tipo + Dimensiones |
| Autopartes | Marca + Tipo + Compatibilidad (marca vehículo + modelo + año) |
| Genérico | Marca + Modelo + Tipo + Atributos diferenciadores |

### 2. Longitud del título

- **No existe un mínimo global** establecido por ML
- El **máximo varía por categoría** y se define en el atributo `max_title_length`
- Cómo verificar el límite de una categoría específica:
  ```
  GET /categories/{category_id}/attributes
  → buscar el campo max_title_length
  ```
- **Buena práctica**: usar la mayor parte del límite disponible para incluir todos los atributos relevantes
- Títulos demasiado cortos tienen menor visibilidad en los resultados de búsqueda

### 3. Atributos requeridos vs. opcionales

**Obligatorios en la mayoría de las categorías:**
- `brand` — Marca del producto
- `model` — Modelo (cuando el campo está marcado como `catalog_required` para esa categoría)

**Recomendados para aumentar visibilidad:**
- Color (solo si el producto no tiene variantes de color)
- Talla / capacidad / peso
- Material
- Especificaciones técnicas relevantes (RAM, almacenamiento, resolución, etc.)
- Género (ropa, calzado)

**Verificar obligatoriedad por categoría:**
```
GET /categories/{category_id}/attributes
→ atributos con "catalog_required": true son obligatorios
```

### 4. Regla especial — Variantes y color

Cuando un producto existe en **múltiples colores**, ML utiliza el sistema de variaciones (`variations`):
- **No incluir el color en el título** del listado principal
- Registrar cada variante de color dentro del mismo listado usando el campo `variations`
- Incluir el color en el título **solo cuando el producto existe en un único color**

Esto aplica también a otras variantes (tallas, capacidades, modelos) cuando se agrupan en un mismo listado.

---

## Prohibiciones explícitas

### Rechazadas por ML (bloquean la publicación)

❌ **Texto en mayúsculas** — `MEJOR CAMISA AZUL` → debe ser `Mejor camisa azul`
❌ **Símbolos y puntuación innecesaria** — `★`, `✓`, `!!!`, `>>>`, `---`
❌ **Precio en el título** — `Camisa azul $5.000`
❌ **Condiciones de pago** — `12 cuotas sin interés`, `3 MSI`
❌ **Información de condición del producto** — `nuevo`, `usado`, `reacondicionado` (va en el campo `condition`)
❌ **Información de envío** — `envío gratis`, `entrega en 24hs`, `full`
❌ **Texto promocional** — `Oferta`, `30% OFF`, `Precio especial`, `Liquidación`

### Que pueden derivar en suspensión de cuenta

❌ **Comparaciones de marca** — `similar a`, `tipo`, `estilo`, `igual a`, `clase de` + nombre de marca
❌ **Marcas no autorizadas** — usar marcas de competidores sin ser distribuidor autorizado
❌ **Indicadores de falsificación** — `réplica`, `copia`, `imitación`, `fake`, `AAA`
❌ **Copiar títulos o descripciones de otros vendedores** — violación de propiedad intelectual

---

## Algoritmo de búsqueda de Mercado Libre

### Factores de posicionamiento (por impacto)

1. **Reputación del vendedor** — factor #1 general en ML
2. **Calidad del título** — factor #1 dentro del listado
3. **Completitud del listado** — fichas técnicas, descripción, imágenes
4. **Rendimiento de conversión** — el algoritmo favorece listados que convierten
5. **Velocidad de ventas** — ítems con más ventas tienen ventaja progresiva
6. **Satisfacción del comprador** — respuesta a consultas, calificaciones, reclamos

### Cómo el título afecta el ranking

- Las palabras del título son el principal signal de relevancia para la búsqueda
- Los compradores buscan con términos naturales: "auriculares inalámbricos sony" o "zapatillas running mujer adidas"
- El título debe contener exactamente esas palabras en el orden más natural posible
- No hay campo de "backend keywords" visible, pero la completitud de la ficha técnica complementa el título para búsquedas de cola larga

---

## Diferencias por país y programa

### Países donde opera ML

Argentina, Bolivia, Brasil, Chile, Colombia, Costa Rica, Ecuador, El Salvador, Guatemala, Honduras, México, Nicaragua, Panamá, Paraguay, Perú, Uruguay, Venezuela.

### Idioma del título

- **Listados nacionales**: usar el idioma local del país objetivo (español o portugués para Brasil)
- **Global Selling** (programa de venta internacional): título en **inglés**

### Global Selling

El programa Global Selling permite listar en México, Brasil, Chile, Colombia y Argentina desde una sola cuenta. Para estos listados:
- El título debe estar en inglés
- Los comportamientos de compra varían por país (México y Brasil difieren significativamente en estacionalidad y preferencias)

---

## Edición del título

| Estado del listado | ¿Se puede editar el título? |
|-------------------|-----------------------------|
| Sin ventas (`sold_quantity = 0`) | ✅ Sí |
| Con al menos una venta | ❌ No |

Planificar y validar el título **antes de la primera venta**. Una vez que el ítem registra ventas, el título queda bloqueado.

---

## Validaciones técnicas de ML

Antes de publicar, ML corre validaciones automáticas. Pueden devolver:

| Tipo | Descripción | ¿Bloquea publicación? |
|------|-------------|----------------------|
| `error` | Problema crítico que viola las reglas | ✅ Sí |
| `warning` | Observación o recomendación | ❌ No |

Verificar validaciones via API antes de publicar en producción.

---

## Calidad del listado (Listing Quality Score)

ML asigna un **puntaje de calidad** a cada listado. Un puntaje más alto se correlaciona directamente con más visitas y ventas. Los factores que afectan el score:

1. Completitud del título (atributos incluidos)
2. Ficha técnica completa (todos los atributos de la categoría)
3. Imágenes de calidad (fondo blanco, múltiples ángulos)
4. Descripción detallada
5. Preguntas respondidas

El título tiene el **mayor peso individual** dentro del score de calidad del listado.

---

## Checklist de validación rápida

```
[ ] ¿Tiene marca?
[ ] ¿Tiene tipo de producto claro?
[ ] ¿Tiene modelo o referencia (si aplica)?
[ ] ¿Longitud dentro del límite de la categoría?
[ ] ¿Sin mayúsculas innecesarias?
[ ] ¿Sin símbolos o puntuación decorativa?
[ ] ¿Sin precio, condiciones de pago o info de envío?
[ ] ¿Sin texto promocional?
[ ] ¿Sin comparaciones de marca ("similar a", "tipo", "estilo")?
[ ] ¿Sin indicar condición del producto (nuevo/usado)?
```

---

## Ejemplos

### ❌ Títulos con problemas

```
NUEVA Camisa OFERTA 30% OFF azul M envío gratis — calidad premium
→ Mayúsculas, texto promocional, condición, info de envío, sin marca

Zapatilla buena para correr
→ Sin marca, sin modelo, sin atributos diferenciadores

Samsung Galaxy S24 NUEVO igual al iPhone mejor precio especial
→ Condición en título, comparación de marca, texto promocional
```

### ✅ Títulos optimizados para ML

```
Lacoste Camisa Polo de Algodón Hombre Azul Marino Talla M
→ Marca + tipo + material + género + color + talla

Adidas Ultraboost 22 Zapatilla Running Mujer Blanca Talla 38
→ Marca + modelo + tipo + género + color + talla

Samsung Galaxy S24 Celular 256GB 8GB RAM Violeta
→ Marca + modelo + tipo + almacenamiento + RAM + color

Sony WH-1000XM5 Auriculares Inalámbricos Cancelación de Ruido Negro
→ Marca + modelo + tipo + specs + color
```
