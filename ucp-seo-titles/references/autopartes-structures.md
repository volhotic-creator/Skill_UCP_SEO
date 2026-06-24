# ML Autopartes — Estructuras por Subcategoría y Sistema de Compatibilidades

Fuentes:
- https://developers.mercadolibre.com.ar/es_ar/referencias-de-dominios-productos-y-atributos-para-autopartes
- https://developers.mercadolibre.com.mx/es_ar/compatibilidades-entre-items-y-productos
- https://anymarket.global/blog/argentina/vender-autopartes-en-mercado-libre/

---

## Mapa de atributos: qué va en el título vs. en el sistema

| Atributo | Título | Sistema ML | Campo |
|----------|:------:|:----------:|-------|
| Tipo de repuesto | ✅ (1ra posición) | — | — |
| Posición (delantero/trasero) | ✅ | ✅ | `POSITION` |
| Marca del repuesto | ✅ | — | `BRAND` del ítem |
| Spec diferenciadora | ✅ (si cabe) | — | Ficha técnica |
| Marca del vehículo | ❌ | ✅ | `BRAND` compatibilidad |
| Modelo del vehículo | ❌ | ✅ | `CAR_AND_VAN_MODEL` |
| Año del vehículo | ❌ | ✅ | `VEHICLE_YEAR` |
| Motor / versión | ❌ | ✅ | `CAR_AND_VAN_ENGINE` |
| Número OEM / parte | ❌ | ❌ | Descripción + ficha técnica |
| Condición (nuevo/usado) | ❌ | — | `condition` del ítem |

---

## Estructuras por subcategoría

### Frenos

#### Pastillas de freno

Fórmula: `Pastilla Freno [Marca] [Posición]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Con marca, Delantera | Pastilla Freno Brembo Delantera | 31 |
| Con marca, Trasera | Pastilla Freno Frasle Trasera | 29 |
| Sin marca, Delantera | Pastilla Freno Delantera | 24 |
| Kit eje completo (delantera+trasera) | Pastilla Freno Cobreq Kit Completo | 34 |

> **Posición obligatoria** para pastillas. Siempre especificar Delantera o Trasera.

#### Discos de freno

Fórmula: `Disco Freno [Posición] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Delantero, Brembo | Disco Freno Delantero Brembo | 28 |
| Trasero, Frasle | Disco Freno Trasero Frasle | 26 |
| Ventilado, Delantero | Disco Freno Delantero Ventilado | 31 |
| Par de discos, Delantero | Par Discos Freno Delantero Brembo | 33 |

#### Tambores y zapatas

Fórmula: `[Tambor / Zapata] Freno [Posición] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Zapata trasera, EBC | Zapata Freno Trasera EBC | 24 |
| Tambor trasero | Tambor Freno Trasero | 20 |

---

### Suspensión

#### Amortiguadores

Fórmula: `Amortiguador [Posición] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Delantero, Monroe | Amortiguador Delantero Monroe | 29 |
| Trasero, KYB | Amortiguador Trasero KYB | 24 |
| Delantero Izquierdo (ítem de un lado) | Amortiguador Delantero Izquierdo Monroe | 39 |
| Par delanteros | Par Amortiguadores Delantero Monroe | 35 |

> Si el ítem incluye ambos lados, usar "Par" y omitir Izquierdo/Derecho.
> Si es para un solo lado, especificar Izquierdo o Derecho.

#### Resortes / Espirales

Fórmula: `Resorte [Posición] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Delantero, Monroe | Resorte Delantero Monroe | 24 |
| Trasero, sin marca | Resorte Trasero Suspensión | 26 |
| Par delanteros | Par Resortes Delantero | 22 |

#### Bujes de suspensión

Fórmula: `Buje Suspensión [Posición] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Delantera, Axl | Buje Suspensión Delantera Axl | 29 |
| Trasera, sin marca | Buje Suspensión Trasera | 23 |
| Kit completo eje | Kit Buje Suspensión Delantera | 29 |

#### Rótulas

Fórmula: `Rótula [Dirección/Suspensión] [Posición] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Dirección, Delantera Derecha, TRW | Rótula Dirección Delantera Derecha TRW | 38 |
| Suspensión, Inferior | Rótula Suspensión Inferior | 26 |
| Dirección, sin posición específica | Rótula Dirección Delantera | 26 |

---

### Filtros

> Para filtros, **la posición no aplica**. No incluir Delantera/Trasera.

#### Filtro de aceite

Fórmula: `Filtro Aceite [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Mahle | Filtro Aceite Mahle | 19 |
| Mann | Filtro Aceite Mann | 18 |
| Sin marca | Filtro Aceite | 13 |

#### Filtro de aire

Fórmula: `Filtro Aire [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Bosch | Filtro Aire Bosch | 17 |
| Sin marca | Filtro Aire | 11 |

#### Filtro de habitáculo / cabina / polen

Fórmula: `Filtro Habitáculo Cabina [Marca]`

Notas: Usar "Habitáculo Cabina" para maximizar keywords de búsqueda (los compradores buscan ambos términos).

| Escenario | Título | Chars |
|-----------|--------|-------|
| Bosch | Filtro Habitáculo Cabina Bosch | 30 |
| Sin marca | Filtro Habitáculo Cabina | 24 |

#### Filtro de combustible

Fórmula: `Filtro Combustible [Variante?] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Gasoil, Mann | Filtro Combustible Gasoil Mann | 30 |
| Nafta, sin marca | Filtro Combustible | 18 |

#### Filtro de caja automática

Fórmula: `Filtro Caja Automática [Marca]`

---

### Motor

#### Correa de distribución

Fórmula:
- Solo correa: `Correa Distribución [Marca]`
- Kit completo: `Kit Distribución [Marca] [Componentes?]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Solo correa, Gates | Correa Distribución Gates | 25 |
| Kit con tensor, Gates | Kit Distribución Gates Correa Tensor | 36 |
| Kit con bomba, Dayco | Kit Distribución Dayco Correa Bomba | 35 |

#### Cadena de distribución

Fórmula: `[Kit] Cadena Distribución [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Solo cadena, Iwis | Cadena Distribución Iwis | 24 |
| Kit completo | Kit Cadena Distribución Iwis | 28 |

#### Junta de culata

Fórmula: `Junta Culata [Marca]`
Kit: `Kit Juntas Motor [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Junta, Corteco | Junta Culata Corteco | 20 |
| Kit completo juntas | Kit Juntas Motor Corteco | 24 |

#### Bomba de aceite

Fórmula: `Bomba Aceite Motor [Marca]`

#### Tapa de válvulas / Junta tapa

Fórmula: `[Tapa / Junta] Válvulas [Marca]`

---

### Eléctrico

#### Alternador

Fórmula: `Alternador [Marca] [Amperaje?]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Bosch, 90A | Alternador Bosch 90A | 20 |
| Sin marca, 120A | Alternador 120A | 15 |

> El amperaje es un diferenciador útil cuando hay múltiples versiones.

#### Motor de arranque / Arrancador

Fórmula: `Arranque Motor [Marca]` o `Arrancador [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Bosch | Arranque Motor Bosch | 20 |
| Sin marca | Arranque Motor | 14 |

#### Sensores

Fórmula: `Sensor [Tipo específico] [Posición?] [Marca]`

> El tipo específico del sensor va antes que la marca — es el primer criterio de búsqueda.

| Tipo | Título | Chars |
|------|--------|-------|
| MAP | Sensor MAP Bosch | 16 |
| Posición cigüeñal | Sensor Posición Cigüeñal Bosch | 30 |
| Temperatura refrigerante | Sensor Temperatura Refrigerante | 31 |
| Oxígeno / Lambda | Sensor Oxígeno Lambda Bosch | 27 |
| ABS rueda delantera | Sensor ABS Rueda Delantera | 26 |
| Presión aceite | Sensor Presión Aceite | 21 |
| TPS (posición mariposa) | Sensor Posición Mariposa TPS | 28 |

#### Bobinas de encendido

Fórmula: `Bobina Encendido [Marca]`

---

### Refrigeración

#### Radiador de agua

Fórmula: `Radiador Agua [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Valeo | Radiador Agua Valeo | 19 |
| Sin marca | Radiador Agua Motor | 19 |

#### Bomba de agua

Fórmula: `Bomba Agua [Marca]`
Kit con correa: `Kit Bomba Agua Correa Distribución [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Hepu | Bomba Agua Hepu | 15 |
| Kit con correa, Gates | Kit Bomba Agua Correa Distribución Gates | 40 |

#### Termostato

Fórmula: `Termostato Motor [Marca] [Temperatura?]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Wahler, 87°C | Termostato Motor Wahler 87 | 26 |
| Sin marca | Termostato Motor | 16 |

---

### Iluminación / Ópticas

> Para ópticas y faros, **la posición (izquierdo/derecho) es obligatoria** salvo que el ítem sea el par completo.

#### Faros delanteros

Fórmula: `Faro Delantero [Izquierdo/Derecho] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Izquierdo, TYC | Faro Delantero Izquierdo TYC | 28 |
| Derecho, sin marca | Faro Delantero Derecho | 22 |
| Par completo | Par Faros Delantero TYC | 23 |

#### Faros traseros / ópticas

Fórmula: `Faro Trasero [Izquierdo/Derecho] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Izquierdo, LAM | Faro Trasero Izquierdo LAM | 26 |
| Derecho, sin marca | Faro Trasero Derecho | 20 |

#### Faros auxiliares y neblineros

Fórmula: `[Faro / Luz] Auxiliar [Posición] [Tipo]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Neblinero delantero | Neblinero Delantero | 19 |
| Faro auxiliar giro | Faro Auxiliar Giro Izquierdo | 28 |

---

### Carrocería

#### Espejos retrovisores

Fórmula: `Espejo Retrovisor [Izquierdo/Derecho] [Color?] [Eléctrico?]`

> El color va en el título cuando es una característica que el comprador necesita elegir antes de comprar (espejos, molduras visibles).

| Escenario | Título | Chars |
|-----------|--------|-------|
| Izquierdo, Negro | Espejo Retrovisor Izquierdo Negro | 32 |
| Derecho, Plata | Espejo Retrovisor Derecho Plata | 31 |
| Eléctrico, Izquierdo | Espejo Retrovisor Eléctrico Izquierdo | 37 |

#### Paragolpes

Fórmula: `Paragolpe [Delantero/Trasero]`

> No incluir color — los paragolpes generalmente se pintan al color del vehículo.

| Escenario | Título | Chars |
|-----------|--------|-------|
| Delantero | Paragolpe Delantero | 19 |
| Trasero | Paragolpe Trasero | 17 |

#### Guardabarros / Aleta

Fórmula: `Guardabarros [Posición completa]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Delantero Izquierdo | Guardabarros Delantero Izquierdo | 32 |
| Trasero Derecho | Guardabarros Trasero Derecho | 28 |

#### Capot / Cofre

Fórmula: `Capot` (no lleva posición — es único por vehículo)

---

### Transmisión

#### Kit de embrague

Fórmula: `[Kit Embrague / Disco / Plato] [Marca]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Kit completo, Valeo | Kit Embrague Valeo | 18 |
| Solo disco, Sachs | Disco Embrague Sachs | 20 |
| Solo plato, LUK | Plato Embrague LUK | 18 |

#### Juntas homocinéticas / CVJ

Fórmula: `Junta Homocinética [Posición] [Interior/Exterior]`

| Escenario | Título | Chars |
|-----------|--------|-------|
| Delantera Derecha Externa | Junta Homocinética Delantera Derecha | 36 |
| Árbol de levas, con posición | Árbol Transmisión Delantero Derecho | 35 |

---

## Nomenclatura de posición — Valores oficiales ML

Usar estos términos exactos en el título y en el atributo `POSITION` del ítem.

| Valor API | Usar en título (masculino) | Usar en título (femenino) |
|-----------|---------------------------|--------------------------|
| `FRONT` | Delantero | Delantera |
| `REAR` | Trasero | Trasera |
| `LEFT` | Izquierdo | Izquierda |
| `RIGHT` | Derecho | Derecha |
| `FRONT_LEFT` | Delantero Izquierdo | Delantera Izquierda |
| `FRONT_RIGHT` | Delantero Derecho | Delantera Derecha |
| `REAR_LEFT` | Trasero Izquierdo | Trasera Izquierda |
| `REAR_RIGHT` | Trasero Derecho | Trasera Derecha |
| `UPPER` | Superior | Superior |
| `LOWER` | Inferior | Inferior |
| `CENTER` | Central | Central |
| `FRONT_LEFT_LOWER` | Delantera Izquierda Inferior | Delantera Izquierda Inferior |

**Concordancia de género en el título:**

El género de la posición debe concordar con el sustantivo del repuesto:
- "Pastilla Freno **Delantera**" — pastilla (femenino)
- "Amortiguador **Delantero**" — amortiguador (masculino)
- "Disco Freno **Delantero**" — disco (masculino)
- "Rótula Dirección **Delantera**" — rótula (femenino)
- "Espejo Retrovisor **Izquierdo**" — espejo (masculino)
- "Junta Homocinética **Delantera**" — junta (femenino)

---

## Sistema de Compatibilidades ML — Guía técnica

### Por qué es obligatorio para autopartes

En las categorías de autopartes de ML, la compatibilidad con vehículos es **obligatoria**. Ítems sin compatibilidad reciben el tag `incomplete_compatibilities` y pueden ser pausados automáticamente.

**Categorías afectadas:**

| Código | País |
|--------|------|
| MLA1747 | Argentina |
| MLM1748 | México |
| MLB22693 | Brasil |
| MLU1748 | Uruguay |
| MLC1748 | Chile |
| MCO87919 | Colombia |

### Endpoint

```
POST /items/{item_id}/compatibilities
```

### Atributos disponibles para la restricción de compatibilidad

| Attribute ID | Descripción | Requerido |
|---|---|---|
| `BRAND` | Marca del vehículo (Ford, Toyota, VW, etc.) | Sí |
| `CAR_AND_VAN_MODEL` | Modelo del vehículo (Ranger, Hilux, Amarok) | Sí |
| `VEHICLE_YEAR` | Año del vehículo | Sí |
| `CAR_AND_VAN_SUBMODEL` | Versión / Trim (XLT, SR, Highline) | Opcional |
| `CAR_AND_VAN_ENGINE` | Motor (2.2 TDi, 2.8 D4D, 1.6 NA) | Opcional |
| `POSITION` | Posición en el vehículo | Cuando aplica |

### Estructura del request

```json
{
  "domain_id": "MLA-AUTOPARTS",
  "products_group": [
    {
      "creation_source": "DEFAULT",
      "restrictions": [
        {
          "attribute_id": "BRAND",
          "attribute_values": ["Ford"]
        },
        {
          "attribute_id": "CAR_AND_VAN_MODEL",
          "attribute_values": ["Ranger"]
        },
        {
          "attribute_id": "VEHICLE_YEAR",
          "attribute_values": [
            "2012","2013","2014","2015","2016",
            "2017","2018","2019","2020","2021","2022"
          ]
        },
        {
          "attribute_id": "CAR_AND_VAN_ENGINE",
          "attribute_values": ["3.2 TDi"]
        }
      ]
    }
  ]
}
```

### Schema de compatibilidades en el pipeline

El skill usa este formato simplificado como entrada para generar el JSON de ML:

```yaml
compatibilidades:
  - marca_vehiculo: Ford
    modelo:         Ranger
    año_desde:      2012
    año_hasta:      2022
    motor:          3.2 TDi       # opcional
    version:        XLT           # opcional

  - marca_vehiculo: Volkswagen
    modelo:         Amarok
    año_desde:      2010
    año_hasta:      2023
    motor:          2.0 TDi

  - marca_vehiculo: Toyota
    modelo:         Hilux
    año_desde:      2016
    año_hasta:      2023
    motor:          2.8 D4D
```

### Tag `incomplete_position_compatibilities`

Cuando el ítem aplica a una posición específica (delantera/trasera, izquierdo/derecho), ML también verifica que la posición esté declarada. El tag `incomplete_position_compatibilities` indica que falta este dato.

**Checklist de campo POSITION por tipo de repuesto:**

| Tipo de repuesto | ¿POSITION requerido? |
|---|---|
| Pastillas de freno | Sí — Delantera o Trasera |
| Discos de freno | Sí — Delantero o Trasero |
| Amortiguadores | Sí — Delantero/Trasero + Izquierdo/Derecho si es de un lado |
| Rótulas y bujes | Sí — según ubicación |
| Sensores ABS | Sí — por rueda |
| Faros y ópticas | Sí — Delantero/Trasero + Izquierdo/Derecho |
| Espejos retrovisores | Sí — Izquierdo o Derecho |
| Paragolpes y guardabarros | Sí — Delantero o Trasero |
| Filtros (aceite/aire/habitáculo) | No aplica |
| Correas y cadenas de distribución | No aplica |
| Juntas de culata y motor | No aplica |
| Sensores MAP / temperatura / lambda | No aplica |
| Radiadores y bombas de agua | No aplica |
| Alternadores y arrancadores | No aplica |
| Kits de embrague | No aplica |

### Beneficios medidos en Argentina

- **+61% de conversión** vs. incluir el vehículo en el título
- Reducción de retornos por incompatibilidad
- Un solo listado cubre múltiples vehículos sin duplicar publicaciones
- El algoritmo ML asocia automáticamente búsquedas con vehículo ("pastilla freno Ford Ranger 2018") a listados con esas compatibilidades cargadas
