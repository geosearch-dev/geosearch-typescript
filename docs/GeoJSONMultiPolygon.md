
# GeoJSONMultiPolygon

GeoJSON MultiPolygon geometry.  WHEN IT IS RETURNED DEPENDS ON THE ENDPOINT AND ON THE PLAN, and there is no single rule. The previous wording here — \"only returned when explicitly requested via `?fields=geometry`\" — was false in both directions and is corrected below.  `GET /v1/countries/{code}` and `GET /v1/regions/{id}`: returned by default. These are detail endpoints and they have always served geometry without `?fields=geometry` being present.  `GET /v1/countries`, `GET /v1/regions` and `GET /v1/countries/{code}/regions`: returned only when `?fields=geometry` is requested. Omitting it from a list response is a payload decision — a 100-row page of region polygons is several megabytes.  REGION GEOMETRY ADDITIONALLY REQUIRES A PAID PLAN. On `GET /v1/regions/{id}`, `GET /v1/regions?fields=geometry` and `GET /v1/countries/{code}/regions?fields=geometry`, the `geometry` key is OMITTED ENTIRELY for Free-tier keys — absent, not null. Country geometry is not gated: `GET /v1/countries/{code}` and `GET /v1/countries?fields=geometry` serve it on every plan, including Free.  The omission is silent by design: it is not an error, and these endpoints still return 200. A client that reads `data.geometry.type` without checking for the key will fail on a null dereference rather than receive a typed zero. To fetch a boundary polygon explicitly — and to receive a 403 with an upgrade link rather than a silent omission when the plan does not include it — use `GET /v1/boundaries/{geoname_id}`.

## Properties

Name | Type
------------ | -------------
`type` | string
`coordinates` | Array&lt;Array&lt;Array&lt;Array&lt;number&gt;&gt;&gt;&gt;

## Example

```typescript
import type { GeoJSONMultiPolygon } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "type": null,
  "coordinates": null,
} satisfies GeoJSONMultiPolygon

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as GeoJSONMultiPolygon
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


