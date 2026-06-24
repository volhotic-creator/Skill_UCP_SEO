---
name: ucp-seo-titles
description: |
  Aplica los criterios del Universal Commerce Protocol (UCP) de Google a títulos SEO de productos para Merchant Center, AI Mode y Gemini. Usa este skill siempre que el equipo técnico o de producto necesite: generar títulos de producto optimizados para UCP, auditar títulos existentes contra los criterios de Google, corregir títulos que no cumplen el estándar, o validar feeds de Merchant Center antes de integrar con UCP. Activar también cuando alguien menciona "títulos de producto", "feed de Merchant Center", "AI Mode", "Google Shopping", "UCP criteria", "títulos SEO para ecommerce", o cuando piden revisar/mejorar/generar títulos en lote.
---

# UCP SEO Titles Skill

Genera, audita y corrige títulos de productos siguiendo los criterios del Universal Commerce Protocol (UCP) de Google, necesarios para que los productos sean elegibles en AI Mode (Google Search) y Gemini.

## Cuándo usar este skill

- Generar títulos nuevos para un producto o catálogo
- Auditar títulos existentes e identificar problemas
- Corregir títulos que fallan en el feed de Merchant Center
- Validar en lote antes de un push al feed
- Explicar por qué un título fue rechazado por Google

## Referencia de criterios

Lee `/references/ucp-criteria.md` para los criterios completos. Resumen ejecutivo:

1. **Estructura**: Marca + Tipo de producto + Atributos diferenciadores
2. **Longitud**: 25–150 caracteres (óptimo: 70–150)
3. **Prohibiciones**: mayúsculas innecesarias, símbolos, precios, texto promocional, palabras de relleno
4. **Requisito IA**: un agente debe poder identificar el ítem específico solo con el título
5. **Feed consistency**: el título debe ser consistente con el de la página de producto

## Flujo de trabajo

### Modo GENERAR (título nuevo)

1. Extraer del input: marca, tipo de producto, atributos clave (color, talla, material, modelo, género, etc.)
2. Si falta información crítica, preguntar antes de generar
3. Construir el título siguiendo la estructura por categoría (ver referencias)
4. Validar contra el checklist de 9 puntos
5. Presentar el título + score de confianza UCP + justificación breve

**Salida esperada:**
```
Título generado: [título]
Longitud: X caracteres ✅/⚠️
Score UCP: X/9 criterios
Issues: [lista de problemas si hay]
Listo para feed: Sí / No (con razón)
```

### Modo AUDITAR (título existente)

1. Recibir el título (uno o en lote)
2. Correr el checklist completo de 9 puntos (ver referencias)
3. Identificar cada problema con su criterio violado
4. Proponer versión corregida
5. Explicar qué cambió y por qué

**Salida esperada por título:**
```
Original: [título original]
Score: X/9
Problemas encontrados:
  - [problema] → criterio violado: [nombre criterio]
Título corregido: [nuevo título]
Cambios: [lista de lo que se modificó]
```

### Modo LOTE (múltiples títulos)

Si recibe una lista, tabla o CSV de títulos:
1. Procesar cada uno en modo AUDITAR
2. Generar resumen ejecutivo con métricas:
   - Total procesados
   - Aptos para UCP (score 9/9)
   - Con issues menores (score 7-8/9)
   - Rechazables (score <7/9)
   - Issues más frecuentes en el lote
3. Ofrecer exportar resultados en tabla markdown

## Checklist de validación (9 puntos)

Correr estos checks en orden para cada título:

```
[1] ¿Tiene marca identificable?              → CRÍTICO
[2] ¿Tiene tipo de producto claro?           → CRÍTICO
[3] ¿Tiene atributo diferenciador?           → IMPORTANTE
[4] ¿Longitud 25–150 caracteres?             → CRÍTICO
[5] ¿Sin mayúsculas innecesarias (CAPS)?     → RECHAZO
[6] ¿Sin símbolos especiales (★✓!!!)?       → RECHAZO
[7] ¿Sin precios ni info de envío?           → RECHAZO
[8] ¿Sin texto promocional?                  → RECHAZO
[9] ¿Un agente IA puede identificar el ítem? → CRÍTICO
```

**Scoring:**
- 9/9 → ✅ Apto para UCP
- 7–8/9 → ⚠️ Mejorable, puede tener baja visibilidad
- <7/9 → ❌ No apto, corregir antes del feed

## Estructuras por categoría

| Categoría | Estructura |
|-----------|-----------|
| Ropa | Marca + Género + Tipo + Color + Talla/Material |
| Electrónica | Marca + Modelo + Tipo + Specs clave |
| Alimentos | Marca + Nombre + Variante/Sabor + Peso |
| Hogar | Marca + Material + Tipo + Dimensiones |
| Calzado | Marca + Modelo + Tipo + Género + Color |
| Genérico | Marca + Tipo + Atributos diferenciadores |

## Notas para el equipo técnico

- El campo `title` en el feed de Merchant Center es la fuente del título UCP
- El título del feed debe coincidir con el `<title>` de la página de producto o el H1 visible
- Si el feed usa `supplemental_feed`, el título del supplemental sobreescribe al principal — validar ambos
- Para variantes (item_group_id), cada variante necesita su propio título con los atributos que la diferencian
- Los títulos se evalúan por país/idioma del feed — validar en el idioma correcto del target market

## Ejemplos de referencia rápida

```
❌ MEJOR Camisa OFERTA 30% OFF azul ★★ calidad
✅ Lacoste Camisa polo de algodón para hombre, azul marino, talla L

❌ Zapatilla buena para correr
✅ Adidas Ultraboost 22 Zapatilla de running para mujer, color blanco, talla 38 EU

❌ Auriculares inalámbricos con cancelación de ruido INCREÍBLES precio especial
✅ Sony WH-1000XM5 Auriculares inalámbricos con cancelación de ruido activa, color negro
```
