
# Weather Observation (Schema)

`ogc.deepdive1.weatherObservation` *v0.1*

A simple weather station observation of air temperature, with semantic uplift to SOSA.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Weather Observation

A minimal **weather station observation**: a single air temperature reading, taken at a
station at a given time.

This block is used to illustrate the main parts of an OGC Building Block:

* **Metadata** (`bblock.json`)
* **Description** (this text, in Markdown)
* **JSON Schema** (`schema.yaml`)
* **Semantic uplift** (`context.jsonld`), mapping the JSON properties to [SOSA](https://www.w3.org/TR/vocab-ssn/)
* **Examples** (`examples.yaml`)
* **Transforms** (`transforms.yaml`)

## Examples

### Temperature reading at Madrid - Retiro
A single air temperature observation, shown both as JSON and as the Turtle
produced by the semantic uplift.
#### json
```json
{
  "id": "https://example.org/observations/1",
  "type": "Observation",
  "stationName": "Madrid - Retiro",
  "observedAt": "2026-10-01T09:00:00Z",
  "temperature": 17.4
}

```

#### jsonld
```jsonld
{
  "@context": "https://avillar.github.io/bblocks-deep-dive-01/build/annotated/deepdive1/weatherObservation/context.jsonld",
  "id": "https://example.org/observations/1",
  "type": "Observation",
  "stationName": "Madrid - Retiro",
  "observedAt": "2026-10-01T09:00:00Z",
  "temperature": 17.4
}
```

#### ttl
```ttl
@prefix ex: <https://example.org/deepdive1/> .
@prefix schema: <https://schema.org/> .
@prefix sosa: <http://www.w3.org/ns/sosa/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/observations/1> a sosa:Observation ;
    sosa:resultTime "2026-10-01T09:00:00+00:00"^^xsd:dateTime ;
    ex:airTemperatureCelsius 1.74e+01 ;
    schema:name "Madrid - Retiro" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: Weather Observation
description: A weather station observation of air temperature
type: object
properties:
  id:
    type: string
    format: uri
    description: Identifier (URI) of the observation
    x-jsonld-id: '@id'
  type:
    const: Observation
    x-jsonld-id: '@type'
  stationName:
    type: string
    description: Name of the weather station
    x-jsonld-id: https://schema.org/name
  observedAt:
    type: string
    format: date-time
    description: Time at which the observation was made
    x-jsonld-id: http://www.w3.org/ns/sosa/resultTime
    x-jsonld-type: http://www.w3.org/2001/XMLSchema#dateTime
  temperature:
    type: number
    description: Air temperature, in degrees Celsius
    minimum: -90
    maximum: 60
    x-jsonld-id: https://example.org/deepdive1/airTemperatureCelsius
    x-jsonld-type: http://www.w3.org/2001/XMLSchema#double
required:
- id
- type
- observedAt
- temperature
x-jsonld-extra-terms:
  Observation: http://www.w3.org/ns/sosa/Observation
x-jsonld-prefixes:
  sosa: http://www.w3.org/ns/sosa/
  schema: https://schema.org/
  xsd: http://www.w3.org/2001/XMLSchema#
  ex: https://example.org/deepdive1/

```

Links to the schema:

* YAML version: [schema.yaml](https://avillar.github.io/bblocks-deep-dive-01/build/annotated/deepdive1/weatherObservation/schema.json)
* JSON version: [schema.json](https://avillar.github.io/bblocks-deep-dive-01/build/annotated/deepdive1/weatherObservation/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "Observation": "sosa:Observation",
    "id": "@id",
    "type": "@type",
    "stationName": "schema:name",
    "observedAt": {
      "@id": "sosa:resultTime",
      "@type": "xsd:dateTime"
    },
    "temperature": {
      "@id": "ex:airTemperatureCelsius",
      "@type": "xsd:double"
    },
    "sosa": "http://www.w3.org/ns/sosa/",
    "schema": "https://schema.org/",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "ex": "https://example.org/deepdive1/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://avillar.github.io/bblocks-deep-dive-01/build/annotated/deepdive1/weatherObservation/context.jsonld)

## Sources

* [SOSA/SSN Ontology](https://www.w3.org/TR/vocab-ssn/)
* [OGC SensorThings API Part 1: Sensing](https://www.ogc.org/standards/sensorthings/)
* [WMO Guide to Instruments and Methods of Observation (WMO-No. 8)](https://community.wmo.int/en/activity-areas/imop/wmo-no_8)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/avillar/bblocks-deep-dive-01](https://github.com/avillar/bblocks-deep-dive-01)
* Path: `_sources/weatherObservation`

