---
name: ml-autopartes-titles
description: |
  Genera, audita y corrige títulos SEO y datos de Compatibilidades para publicaciones de Autopartes / Repuestos para Autos y Camionetas en Mercado Libre Argentina y LATAM. Produce el título optimizado (≤60 chars) más la estructura de Compatibilidades lista para el feed. Activar cuando el equipo necesite generar títulos, auditar publicaciones existentes, corregir rechazos, o procesar catálogos en lote. También activar cuando se mencione: "repuesto", "autoparte", "filtro", "freno", "amortiguador", "faro", "espejo", "correa", "compatibilidad vehículo", o cualquier pieza de auto o camioneta para ML.
---

# Skill: Títulos SEO para Autopartes — Mercado Libre Argentina

Genera títulos optimizados y datos de Compatibilidades para publicaciones del rubro **Repuestos para Autos y Camionetas** en Mercado Libre.

---

## Principio fundamental

> **El título describe el repuesto. El vehículo va en el sistema de Compatibilidades de ML.**

La información del vehículo compatible (marca, modelo, año) se carga via el sistema estructurado de Compatibilidades de ML — no en el título. Este es el estándar oficial de ML para autopartes y genera +61% de conversión en Argentina vs. incluir el vehículo en el título.

| Dato | Dónde va |
|------|----------|
| Tipo de repuesto | Título — primera posición |
| Posición (delantera/trasera) | Título + atributo `POSITION` del ítem |
| Marca del repuesto | Título |
| Spec diferenciadora | Título (si entra en el límite) |
| Marca del vehículo | Sistema de Compatibilidades ML |
| Modelo del vehículo | Sistema de Compatibilidades ML |
| Año(s) del vehículo | Sistema de Compatibilidades ML |
| Motor / versión | Sistema de Compatibilidades ML |
| Número OEM / de parte | Descripción + ficha técnica del ítem |
| Condición (nuevo/usado) | Campo `condition` del ítem ML |

---

## Referencias

- Criterios generales ML: `/references/mercadolibre-criteria.md`
- Estructuras por subcategoría y guía técnica de Compatibilidades: `/references/autopartes-structures.md`

---

## Schema de entrada — Pipeline de datos

El skill acepta este schema como input. Puede llegar en JSON, YAML, tabla o texto libre.

```
REPUESTO
  tipo_repuesto:    [obligatorio]   Pastilla Freno / Filtro Aceite / Amortiguador / etc.
  posicion:         [condicional]   Delantera · Trasera · Izquierda · Derecha
                                    Delantera Izquierda · Delantera Derecha
                                    Trasera Izquierda · Trasera Derecha · N/A
  marca_repuesto:   [si aplica]     Brembo · Gates · Monroe · Bosch · Mahle · etc.
  spec_clave:       [si aplica]     Tamaño · capacidad · tipo de kit · amperaje

COMPATIBILIDADES  (mínimo 1 registro — obligatorio en categorías ML autopartes)
  - marca_vehiculo: [obligatorio]   Ford · Toyota · Volkswagen · Renault · Peugeot · etc.
    modelo:         [obligatorio]   Ranger · Hilux · Amarok · Kangoo · 206 · etc.
    año_desde:      [obligatorio]   ej: 2012
    año_hasta:      [obligatorio]   ej: 2022  (año actual si el modelo sigue vigente)
    motor:          [si aplica]     ej: 2.2 TDi · 2.8 D4D · 1.4 16v
    version:        [si aplica]     ej: XLT · Limited · Trendline
```

---

## Fórmula del título

```
[Tipo de repuesto]  [Marca repuesto?]  [Posición?]  [Spec clave?]
```

**Reglas de construcción:**

1. El tipo de repuesto va **primero** — las primeras palabras tienen mayor peso en el ranking de ML
2. La posición va **después** de la marca del repuesto (o después del tipo si no hay marca)
3. Omitir posición si no aplica al tipo (filtros, correas, juntas de culata)
4. Omitir marca del repuesto si el ítem es genérico o sin marca
5. Límite estricto: **60 caracteres** (límite de categoría en ML Argentina autopartes)
6. Sin vehículo en el título — va en Compatibilidades
7. Sin número OEM — va en ficha técnica

**Tabla de fórmulas por subcategoría:**

| Subcategoría | Fórmula | Ejemplo (con marca) | Ejemplo (sin marca) |
|---|---|---|---|
| Pastillas de freno | Tipo + Marca + Posición | Pastilla Freno Brembo Delantera | Pastilla Freno Delantera |
| Discos de freno | Tipo + Posición + Marca | Disco Freno Delantero Brembo | Disco Freno Delantero |
| Zapatas / tambores | Tipo + Posición + Marca | Zapata Freno Trasera EBC | Zapata Freno Trasera |
| Amortiguadores | Tipo + Posición + Marca | Amortiguador Delantero Monroe | Amortiguador Delantero |
| Resortes | Tipo + Posición + Marca | Resorte Delantero Monroe | Resorte Delantero Suspensión |
| Bujes de suspensión | Tipo + Posición + Marca | Buje Suspensión Delantera Axl | Buje Suspensión Delantera |
| Rótulas | Tipo + Posición + Marca | Rótula Dirección Delantera TRW | Rótula Dirección Delantera |
| Filtro de aceite | Tipo + Marca | Filtro Aceite Mahle | Filtro Aceite |
| Filtro de aire | Tipo + Marca | Filtro Aire Bosch | Filtro Aire |
| Filtro habitáculo | Tipo + Marca | Filtro Habitáculo Cabina Bosch | Filtro Habitáculo Cabina |
| Filtro combustible | Tipo + Variante + Marca | Filtro Combustible Gasoil Mann | Filtro Combustible |
| Correa distribución | Tipo + Marca + Kit? | Correa Distribución Gates | Kit Distribución Gates |
| Cadena distribución | Tipo + Marca | Cadena Distribución Iwis | Kit Cadena Distribución |
| Junta de culata | Tipo + Marca | Junta Culata Corteco | Junta Culata |
| Alternador | Tipo + Marca + Amperaje? | Alternador Bosch 90A | Alternador 90A |
| Arrancador | Tipo + Marca | Arranque Motor Bosch | Arranque Motor |
| Sensor | Tipo específico + Marca | Sensor MAP Bosch | Sensor Posición Cigüeñal |
| Bobina encendido | Tipo + Marca | Bobina Encendido Bosch | Bobina Encendido |
| Radiador de agua | Tipo + Marca | Radiador Agua Valeo | Radiador Agua Motor |
| Bomba de agua | Tipo + Marca | Bomba Agua Hepu | Bomba Agua Motor |
| Termostato | Tipo + Marca | Termostato Motor Wahler | Termostato Motor |
| Faro delantero | Tipo + Posición + Marca | Faro Delantero Izquierdo TYC | Faro Delantero Izquierdo |
| Faro trasero | Tipo + Posición + Marca | Faro Trasero Derecho LAM | Faro Trasero Derecho |
| Espejo retrovisor | Tipo + Posición + Color? | Espejo Retrovisor Izquierdo Negro | Espejo Retrovisor Izquierdo |
| Paragolpe | Tipo + Posición | Paragolpe Delantero | Paragolpe Trasero |
| Guardabarros | Tipo + Posición | Guardabarros Delantero Izquierdo | Guardabarros Trasero Derecho |
| Kit de embrague | Tipo + Marca | Kit Embrague Valeo | Kit Embrague Completo |
| Disco de embrague | Tipo + Marca | Disco Embrague Sachs | Disco Embrague |
| Junta homocinética | Tipo + Posición + Int/Ext | Junta Homocinética Delantera Externa | — |

---

## Modos de operación

### MODO GENERAR — Título nuevo desde datos estructurados

1. Recibir datos según el schema de entrada
2. Identificar subcategoría del repuesto
3. Aplicar fórmula correspondiente de la tabla
4. Validar contra checklist de 13 puntos
5. Presentar output completo

**Output:**
```
Título:              [título generado]
Longitud:            XX/60 caracteres  ✅ / ⚠️ supera límite
Score:               XX/13
Issues:              ninguno  /  [lista de problemas]
Apto para publicar:  Sí  /  No — [razón]

Compatibilidades (para sistema ML):
┌──────────────────┬───────────────┬────────────────┬─────────────┐
│ Marca vehículo   │ Modelo        │ Año            │ Motor       │
├──────────────────┼───────────────┼────────────────┼─────────────┤
│ Ford             │ Ranger        │ 2012–2022      │ 3.2 TDi     │
│ Volkswagen       │ Amarok        │ 2010–2023      │ 2.0 TDi     │
└──────────────────┴───────────────┴────────────────┴─────────────┘
```

---

### MODO AUDITAR — Título existente

1. Recibir título existente (+ datos de compatibilidad si están disponibles)
2. Correr checklist completo de 13 puntos
3. Identificar cada problema con su criterio y severidad
4. Generar título corregido
5. Listar cambios aplicados

**Output:**
```
Original:       [título original]
Score:          XX/13
Problemas:
  - [descripción] → criterio #N  [CRÍTICO / RECHAZO / SUSPENSIÓN]
Corregido:      [nuevo título]
Longitud:       XX/60 caracteres
Cambios:
  - [cambio 1]
  - [cambio 2]
```

---

### MODO LOTE — Múltiples ítems

Si recibe tabla, CSV, JSON array o lista de ítems:

1. Procesar cada ítem en GENERAR o AUDITAR según corresponda
2. Al finalizar, presentar resumen ejecutivo + tabla exportable

**Resumen ejecutivo:**
```
Resumen del lote — ML Autopartes Argentina
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total procesados:          XX
✅ Aptos sin cambios:       XX
⚠️ Con issues menores:      XX  (1–2 problemas, mejorable)
❌ Requieren corrección:     XX  (3+ problemas, no publicar)

Issues más frecuentes:
  1. [issue] — XX ítems
  2. [issue] — XX ítems
  3. [issue] — XX ítems
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Tabla exportable (markdown):**

| # | Título original | Título corregido | Chars | Score | Issues |
|---|----------------|-----------------|-------|-------|--------|
| 1 | ... | ... | 0/60 | 0/13 | ... |

---

## Checklist de validación ML Autopartes — 13 puntos

Correr en orden. Los niveles de severidad son:
- **CRÍTICO** — bloquea la calidad del listado, impacta visibilidad
- **IMPORTANTE** — reduce conversión o posicionamiento
- **RECHAZO** — ML puede rechazar la publicación
- **SUSPENSIÓN** — riesgo de suspensión de cuenta

```
[1]  ¿El tipo de repuesto es la primera palabra(s) del título?        CRÍTICO
[2]  ¿Tiene posición cuando corresponde al tipo de repuesto?          CRÍTICO
[3]  ¿Longitud ≤ 60 caracteres?                                       CRÍTICO
[4]  ¿Las Compatibilidades (vehículo) están definidas?                CRÍTICO
[5]  ¿Sin información de vehículo en el título
       (marca/modelo/año de auto o camioneta)?                        IMPORTANTE
[6]  ¿Tiene marca del repuesto si el ítem tiene marca conocida?       IMPORTANTE
[7]  ¿Sin número OEM ni de parte en el título?                        IMPORTANTE
[8]  ¿Sin mayúsculas innecesarias (ALL CAPS)?                         RECHAZO
[9]  ¿Sin símbolos ni puntuación decorativa (★ · >>> · --- · !!!)?   RECHAZO
[10] ¿Sin precio ni condiciones de pago ("12 cuotas", "$5.000")?      RECHAZO
[11] ¿Sin condición del producto ("nuevo", "usado", "original")?      RECHAZO
[12] ¿Sin texto promocional ni info de envío?                         RECHAZO
[13] ¿Sin comparaciones de marca
       ("similar a", "tipo", "estilo", "igual a" + nombre de marca)? SUSPENSIÓN
```

**Scoring:**
- 13/13 → ✅ Apto para publicar
- 11–12/13 → ⚠️ Mejorable — revisar antes del feed
- ≤10/13 → ❌ No publicar — corregir primero

---

## Notas técnicas — Integración pipeline

- **Compatibilidades obligatorias**: ML pausa automáticamente ítems con tag `incomplete_compatibilities`. Endpoint: `POST /items/{item_id}/compatibilities`. Categorías afectadas: MLA1747, MLM1748, MLB22693, MLU1748, MLC1748, MCO87919.
- **Límite de caracteres**: Verificar por categoría via `GET /categories/{category_id}/attributes` → `max_title_length`. Estándar en autopartes ML Argentina: **60 caracteres**.
- **Número OEM**: Va en descripción y atributos técnicos del ítem. Nunca en el título.
- **Ítems con múltiples posiciones**: No crear listados separados por lado — usar `variations` con posición como atributo de variante cuando el ítem puede ser izquierdo o derecho.
- **Edición post-venta**: El título no se puede editar una vez que `sold_quantity > 0`. Validar títulos antes del primer push al feed.
- **Atributo POSITION del ítem**: Debe coincidir con la posición mencionada en el título. Completarlo siempre que el título incluya posición.

---

## Ejemplos de referencia

```
❌  Pastilla Freno Delantera Ford Ranger 3.2 TDi 2012-2022 Brembo  (64 chars)
    Problemas: vehículo en título [#5 IMPORTANTE], supera 60 chars [#3 CRÍTICO]
    El vehículo debe ir en el sistema de Compatibilidades de ML.

✅  Pastilla Freno Brembo Delantera  (31 chars · 13/13)
    Compatibilidades ML: Ford Ranger 3.2 TDi 2012-2022

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

❌  FILTRO DE ACEITE MAHLE ORIGINAL NUEVO Toyota Hilux 2022  (55 chars)
    Problemas: ALL CAPS [#8 RECHAZO], condición en título [#11 RECHAZO],
               vehículo en título [#5 IMPORTANTE]

✅  Filtro Aceite Mahle  (20 chars · 13/13)
    Compatibilidades ML: Toyota Hilux 2015-2023

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

❌  Amortiguador Monroe Delantero Izquierdo camioneta diesel envio gratis  (70 chars)
    Problemas: supera 60 chars [#3 CRÍTICO], info de envío [#12 RECHAZO],
               descriptor genérico innecesario ("camioneta diesel")

✅  Amortiguador Delantero Izquierdo Monroe  (41 chars · 13/13)
    Compatibilidades ML: [cargadas en sistema ML]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

❌  Kit Embrague completo similar a Valeo calidad premium 3 cuotas sin interes
    Problemas: comparación de marca [#13 SUSPENSIÓN], texto promocional [#12 RECHAZO],
               cuotas en título [#10 RECHAZO]

✅  Kit Embrague Valeo  (20 chars · 13/13)
    Compatibilidades ML: [cargadas en sistema ML]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

❌  04466-0K060 Pastillas Freno Delanteras Toyota Hilux  (51 chars)
    Problemas: OEM en título [#7 IMPORTANTE], vehículo en título [#5 IMPORTANTE]
    El OEM va en ficha técnica. El vehículo va en Compatibilidades.

✅  Pastilla Freno Delantera Toyota  (33 chars · 12/13)
    Nota: si la marca del repuesto no es conocida, esta versión es válida.
    OEM 04466-0K060 → ficha técnica del ítem.
    Compatibilidades ML: Toyota Hilux 2015-2023 / Fortuner 2016-2023
```
