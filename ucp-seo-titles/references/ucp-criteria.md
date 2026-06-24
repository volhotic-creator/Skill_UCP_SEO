# Google UCP — Criterios para Títulos SEO de Productos

Fuente: https://developers.google.com/merchant/ucp

---

## ¿Qué es UCP?

El Universal Commerce Protocol (UCP) es el estándar abierto de Google que permite compras directas e instantáneas desde AI Mode en Google Search y Gemini. Para que un producto sea elegible para estas superficies, sus datos de feed (incluyendo el título) deben cumplir criterios específicos.

## Criterios UCP aplicados a títulos SEO

### 1. Claridad para agentes de IA
Los títulos son leídos e interpretados por agentes de IA (Gemini, AI Mode). Deben ser:
- **Unívocos**: sin ambigüedad sobre qué producto es
- **Autoexplicativos**: el agente debe poder confirmar la compra sin ver la imagen
- **Sin jerga de marketing vacía**: "increíble", "revolucionario", "el mejor" → no aportan

### 2. Estructura recomendada por Google Merchant Center (base de UCP)
Formato estándar por categoría:

| Categoría | Estructura ideal |
|-----------|-----------------|
| Ropa | Marca + Género + Tipo de producto + Atributos (color, talla, material) |
| Electrónica | Marca + Modelo + Tipo de producto + Especificaciones clave |
| Alimentos | Marca + Nombre del producto + Sabor/variante + Peso/cantidad |
| Hogar | Marca + Material + Tipo de producto + Tamaño |
| Genérico | Marca + Tipo de producto + Atributos diferenciadores |

### 3. Longitud óptima
- **Mínimo**: 25 caracteres
- **Óptimo**: 70–150 caracteres (para AI Mode y búsqueda tradicional)
- **Máximo técnico**: 150 caracteres (Google trunca después de ahí en muchas superficies)
- Títulos cortos (<25 chars) → rechazo o baja visibilidad en UCP
- Títulos largos (>150 chars) → truncados en cards de Gemini

### 4. Información requerida para checkout agéntico
Para que un agente pueda completar una compra sin intervención humana, el título debe contener suficiente información para identificar el ítem específico:
- **Marca** (obligatorio)
- **Tipo de producto** (obligatorio)
- **Variante diferenciadora** (color, talla, capacidad, sabor — lo que aplique)
- **Modelo o SKU descriptivo** si hay variantes similares

### 5. Prohibiciones explícitas de Google Merchant Center / UCP
❌ Texto en mayúsculas (GRITANDO)
❌ Símbolos y caracteres especiales innecesarios (★, ✓, !!!,  €€€)
❌ Precios en el título ("$19.99 camisa azul")
❌ Información de envío ("Envío gratis - Camiseta azul")
❌ Texto promocional ("Oferta limitada", "30% OFF")
❌ Palabras de relleno sin valor ("producto de calidad", "el mejor del mercado")
❌ Duplicar el tipo de producto redundantemente

### 6. Keywords y search intent para AI Mode
En AI Mode, el usuario hace preguntas conversacionales, no búsquedas de keywords. El título debe funcionar en ambos contextos:
- Búsqueda clásica: "zapatillas running mujer Nike"
- Query conversacional: "quiero zapatillas para correr, soy mujer, me gustan las Nike"

El título ideal contiene los atributos que responden a ambas formas de buscar.

### 7. Compatibilidad con el feed de Merchant Center
El título que se usa en UCP es el mismo `title` del feed de Merchant Center. Debe:
- Ser consistente con el título en la página de producto (no puede diferir radicalmente)
- Usar el idioma del país target del feed
- No contener HTML ni caracteres de escape

### 8. Atributos que potencian la elegibilidad UCP
Aunque van en campos separados del feed, estos atributos complementan el título y aumentan la confianza del agente para completar la compra:
- `brand`
- `color`
- `size`
- `material`
- `item_group_id` (para variantes)
- `gtin` o `mpn`

Si estos atributos NO están en el feed, el título debe compensar incluyendo esa información.

## Checklist de validación rápida

```
[ ] ¿Tiene marca?
[ ] ¿Tiene tipo de producto claro?
[ ] ¿Tiene atributo diferenciador (color/talla/modelo)?
[ ] ¿Longitud entre 25 y 150 caracteres?
[ ] ¿Sin mayúsculas innecesarias?
[ ] ¿Sin símbolos o caracteres especiales?
[ ] ¿Sin precios ni texto promocional?
[ ] ¿Sin palabras de relleno?
[ ] ¿Un agente IA podría confirmar qué ítem es solo con este título?
```

## Ejemplos

### ❌ Título con problemas
`MEJOR Camiseta OFERTA ESPECIAL 30% OFF azul ★★★★★ calidad premium envío gratis`

Problemas: mayúsculas, texto promocional, símbolos, sin marca, sin talla

### ✅ Título optimizado para UCP
`Nike Dri-FIT Camiseta de running para hombre, color azul marino, talla M`

Cumple: marca + tipo + género + color + talla — 73 caracteres — apto para AI Mode
