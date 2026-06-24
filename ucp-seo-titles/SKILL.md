---
name: ucp-seo-titles
description: |
  Genera, audita y corrige títulos SEO de productos para Mercado Libre y Google (UCP / Merchant Center / AI Mode / Gemini). Activar cuando el equipo necesite generar títulos nuevos, auditar títulos existentes, corregir rechazos del feed, o validar catálogos en lote para cualquiera de estas plataformas. También activar cuando se mencione: "títulos de producto", "Mercado Libre", "Meli", "ML", "feed de Merchant Center", "AI Mode", "Google Shopping", "UCP", "títulos SEO ecommerce", o cuando pidan revisar, mejorar o generar títulos.
---

# Skill: SEO Titles — Mercado Libre & Google UCP

Genera, audita y corrige títulos de productos cumpliendo los criterios específicos de cada plataforma.

**Plataformas soportadas:**
- **Mercado Libre** — Argentina, México, Brasil, Colombia, Chile y otros países de LATAM
- **Google UCP** — Merchant Center, AI Mode (Google Search), Gemini

---

## Plataformas y referencias

| Plataforma | Criterio de referencia |
|------------|----------------------|
| Mercado Libre | `/references/mercadolibre-criteria.md` |
| Google UCP | `/references/ucp-criteria.md` |

---

## Cómo indicar la plataforma

El usuario debe especificar la plataforma objetivo. Si no lo hace, preguntar antes de proceder:

```
¿Para qué plataforma es este título?
  (A) Mercado Libre
  (B) Google UCP / Merchant Center
  (C) Ambas (optimización dual)
```

Si el contexto es claro ("ML", "MercadoLibre", "listado en Meli", "feed de Google", etc.), asumir sin preguntar.

---

## Modos de operación

### MODO GENERAR — Título nuevo

**Paso 1 — Recopilar datos**

Extraer del input o preguntar si falta información crítica:

| Dato | ML | UCP |
|------|----|-----|
| Marca | Obligatorio | Obligatorio |
| Tipo de producto | Obligatorio | Obligatorio |
| Modelo / referencia | Obligatorio si existe | Recomendado |
| Color | Solo si no hay variantes | Siempre incluir |
| Talla / capacidad / peso | Si aplica | Si aplica |
| Género | Si aplica | Si aplica |
| Material | Si aplica | Si aplica |
| Categoría (para ML) | Para verificar límite de chars | — |
| País / idioma objetivo | Para Global Selling | Para target del feed |

**Paso 2 — Construir el título**

Usar la estructura de la sección "Estructuras por categoría" según la plataforma.

**Paso 3 — Validar**

Correr el checklist de la plataforma indicada. Para dual: correr ambos checklists.

**Paso 4 — Presentar resultado**

```
Plataforma:        [ML / UCP / Dual]
Título generado:   [título]
Longitud:          X caracteres  [✅ dentro del límite / ⚠️ revisar]
Score:             X/N criterios cumplidos
Issues:            [ninguno / lista de problemas]
Listo para publicar: Sí / No — [razón si No]
```

---

### MODO AUDITAR — Título existente

**Paso 1** — Recibir el título
**Paso 2** — Correr checklist completo de la plataforma indicada
**Paso 3** — Identificar cada problema con el criterio que viola
**Paso 4** — Proponer versión corregida
**Paso 5** — Explicar cada cambio realizado

```
Original:          [título original]
Plataforma:        [ML / UCP]
Score:             X/N
Problemas encontrados:
  - [descripción del problema] → criterio #N: [nombre]
Título corregido:  [nuevo título]
Longitud:          X caracteres
Cambios aplicados:
  - [cambio 1]
  - [cambio 2]
```

---

### MODO LOTE — Múltiples títulos

Si recibe una lista, tabla o CSV:

1. Procesar cada título en modo AUDITAR
2. Al finalizar, presentar resumen ejecutivo:

```
Resumen del lote — Plataforma: [ML / UCP / Dual]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total procesados:        XX
✅ Aptos sin cambios:    XX  (score perfecto)
⚠️ Con issues menores:   XX  (1–2 problemas)
❌ Requieren corrección:  XX  (3+ problemas)

Issues más frecuentes:
  1. [issue] — XX títulos
  2. [issue] — XX títulos
  3. [issue] — XX títulos
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

3. Ofrecer tabla markdown con todos los títulos originales y corregidos

---

## Checklists de validación

### Checklist Mercado Libre — 10 puntos

Los ítems marcados RECHAZO o SUSPENSIÓN son **bloqueantes**.

```
[1]  ¿Tiene marca identificable?                               CRÍTICO
[2]  ¿Tiene tipo de producto claro?                            CRÍTICO
[3]  ¿Tiene modelo o referencia (si aplica a la categoría)?    IMPORTANTE
[4]  ¿Longitud dentro del límite de la categoría?              CRÍTICO
[5]  ¿Sin mayúsculas innecesarias (ALL CAPS)?                  RECHAZO
[6]  ¿Sin símbolos ni puntuación innecesaria?                  RECHAZO
[7]  ¿Sin precio ni condiciones de pago ("12 cuotas")?         RECHAZO
[8]  ¿Sin info de envío ni texto promocional?                  RECHAZO
[9]  ¿Sin comparaciones de marca
       ("similar a", "tipo", "estilo", "igual a")?             SUSPENSIÓN
[10] ¿Sin indicar condición (nuevo/usado/reacondicionado)?     RECHAZO
```

**Scoring ML:**
- 10/10 → ✅ Apto para publicar
- 8–9/10 → ⚠️ Mejorable, menor visibilidad posible
- <8/10 → ❌ No apto — corregir antes de publicar

---

### Checklist Google UCP — 9 puntos

```
[1]  ¿Tiene marca identificable?                               CRÍTICO
[2]  ¿Tiene tipo de producto claro?                            CRÍTICO
[3]  ¿Tiene atributo diferenciador (color/talla/modelo)?       IMPORTANTE
[4]  ¿Longitud entre 25 y 150 caracteres?                      CRÍTICO
[5]  ¿Sin mayúsculas innecesarias (ALL CAPS)?                  RECHAZO
[6]  ¿Sin símbolos especiales (★ ✓ !!! €€€)?                 RECHAZO
[7]  ¿Sin precio ni información de envío?                      RECHAZO
[8]  ¿Sin texto promocional ("30% OFF", "Oferta limitada")?    RECHAZO
[9]  ¿Un agente IA puede identificar el ítem exacto
       solo con este título, sin ver la imagen?                CRÍTICO
```

**Scoring UCP:**
- 9/9 → ✅ Apto para UCP / AI Mode / Gemini
- 7–8/9 → ⚠️ Mejorable, baja visibilidad posible en Gemini
- <7/9 → ❌ No apto — corregir antes del feed

---

## Estructuras por categoría

### Mercado Libre

| Categoría | Estructura recomendada |
|-----------|----------------------|
| Electrónica / Tecnología | Marca + Modelo + Tipo de producto + Specs clave |
| Smartphones | Marca + Modelo + Almacenamiento + RAM + Color |
| Ropa | Marca + Tipo + Género + Color + Talla/Material |
| Calzado | Marca + Modelo + Tipo + Género + Talla |
| Alimentos | Marca + Nombre + Variante/Sabor + Peso/Cantidad |
| Hogar | Marca + Material + Tipo + Medidas |
| Autopartes | Marca + Tipo + Compatibilidad (marca/modelo auto + año) |
| Genérico | Marca + Modelo + Tipo + Atributos diferenciadores |

> **Regla ML sobre color y variantes**: Si el producto existe en múltiples colores, **no incluir el color en el título** — usar el sistema de variaciones de ML. Incluir color solo cuando el producto es de un único color.

### Google UCP

| Categoría | Estructura recomendada |
|-----------|----------------------|
| Ropa | Marca + Género + Tipo de producto + Color + Talla/Material |
| Electrónica | Marca + Modelo + Tipo de producto + Especificaciones clave |
| Alimentos | Marca + Nombre del producto + Sabor/variante + Peso |
| Hogar | Marca + Material + Tipo de producto + Dimensiones |
| Calzado | Marca + Modelo + Tipo + Género + Color + Talla |
| Genérico | Marca + Tipo de producto + Atributos diferenciadores |

> **Regla UCP sobre atributos**: Incluir siempre el atributo diferenciador porque el agente IA necesita identificar el ítem específico para completar el checkout agéntico sin intervención humana.

---

## Comparativa rápida ML vs Google UCP

| Criterio | Mercado Libre | Google UCP |
|----------|:------------:|:---------:|
| Estructura base | Marca + Modelo + Producto + Specs | Marca + Producto + Atributos |
| Longitud mínima | Sin mínimo global definido | 25 caracteres |
| Longitud máxima | Por categoría (consultar API) | 150 caracteres |
| Longitud óptima | Llegar al límite de la categoría | 70–150 caracteres |
| Color en título | Solo si producto es de un color | Siempre |
| Condición (nuevo/usado) | ❌ Nunca en el título | No aplica |
| Texto promocional | ❌ Prohibido | ❌ Prohibido |
| Info de envío | ❌ Prohibido | ❌ Prohibido |
| MAYÚSCULAS | ❌ Prohibido | ❌ Prohibido |
| Símbolos especiales | ❌ Prohibido | ❌ Prohibido |
| Comparaciones de marca | ❌ Riesgo de suspensión | ❌ Prohibido |
| Idioma | Local / inglés (Global Selling) | Idioma del target del feed |

---

## Notas técnicas

### Mercado Libre

- **Límite de caracteres por categoría**: Verificar via API `GET /categories/{category_id}/attributes` → campo `max_title_length`. Varía por categoría; algunas tienen 60 caracteres, otras más.
- **Edición del título**: El título no puede editarse una vez que el ítem tiene ventas (`sold_quantity > 0`). Antes de la primera venta, sí es editable.
- **Variantes**: Para colores, tallas u otras variantes, usar el sistema de variaciones de ML (`variations`) en lugar de crear listados separados.
- **Global Selling**: En el programa de venta internacional de ML, los títulos deben estar en **inglés**.
- **Validaciones**: ML devuelve dos tipos — `warning` (informativo, no bloquea) y `error` (bloquea publicación). Corregir todos los `error` antes de publicar.
- **Posicionamiento**: La reputación del vendedor es el factor #1 de ranking en ML; dentro del listado, el título es el elemento de mayor impacto.

### Google UCP

- **Campo del feed**: El campo `title` del feed de Merchant Center es la fuente del título UCP. Debe coincidir con el `<title>` o H1 visible de la página de producto.
- **Supplemental feed**: Si se usa `supplemental_feed`, ese título sobreescribe al principal. Validar ambos.
- **Variantes**: Con `item_group_id`, cada variante necesita su propio título con los atributos que la diferencian (color, talla, capacidad, etc.).
- **Idioma**: Los títulos se evalúan por país/idioma del feed. Validar siempre en el idioma correcto del target market.
- **Checkout agéntico**: El título debe ser suficientemente descriptivo para que un agente (Gemini) confirme la compra sin ver la imagen del producto.

---

## Ejemplos de referencia

### Mercado Libre

```
❌  NUEVA Camisa OFERTA 30% OFF azul M envío gratis — calidad premium
    Problemas: mayúsculas, texto promocional, info de envío, condición en título

✅  Lacoste Camisa Polo de Algodón Hombre Azul Marino Talla M
    ✓ Marca + tipo + material + género + color + talla

❌  Zapatilla buena correr
    Problemas: sin marca, sin modelo, sin specs diferenciadores

✅  Adidas Ultraboost 22 Zapatilla Running Mujer Blanca Talla 38
    ✓ Marca + modelo + tipo + género + color + talla

❌  Samsung Galaxy S24 Celular NUEVO 256GB igual al iPhone precio especial
    Problemas: condición en título, comparación de marca, texto promocional

✅  Samsung Galaxy S24 Celular 256GB 8GB RAM Violeta
    ✓ Marca + modelo + tipo + almacenamiento + RAM + color
```

### Google UCP

```
❌  MEJOR Camiseta OFERTA ESPECIAL 30% OFF azul ★★★★★ calidad premium envío gratis
    Problemas: mayúsculas, texto promocional, símbolos, sin marca, sin talla

✅  Nike Dri-FIT Camiseta de running para hombre, color azul marino, talla M
    ✓ Marca + modelo + tipo + género + color + talla — 73 caracteres

❌  Auriculares inalámbricos INCREÍBLES precio especial
    Problemas: mayúsculas, texto promocional, sin marca, sin modelo

✅  Sony WH-1000XM5 Auriculares inalámbricos con cancelación de ruido activa, color negro
    ✓ Marca + modelo + tipo + specs — 86 caracteres — apto UCP / AI Mode
```
