
# Boundary

One area\'s boundary polygon, as returned by `GET /v1/boundaries/{geoname_id}`.

## Properties

Name | Type
------------ | -------------
`geonameId` | number
`name` | string
`type` | string
`geometry` | [GeoJSONGeometry](GeoJSONGeometry.md)
`simplify` | number

## Example

```typescript
import type { Boundary } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "geonameId": 6252001,
  "name": United States,
  "type": country,
  "geometry": null,
  "simplify": null,
} satisfies Boundary

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Boundary
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


