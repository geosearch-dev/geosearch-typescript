
# GeoJSONGeometry

A bare GeoJSON geometry — the `{\"type\": ..., \"coordinates\": ...}` object itself, NOT a GeoJSON `Feature`. There is no `properties` wrapper.

## Properties

Name | Type
------------ | -------------
`type` | string
`coordinates` | Array&lt;any&gt;

## Example

```typescript
import type { GeoJSONGeometry } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "type": MultiPolygon,
  "coordinates": [[[[-124.7, 48.4], [-124.6, 48.4], [-124.6, 48.3], [-124.7, 48.4]]]],
} satisfies GeoJSONGeometry

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as GeoJSONGeometry
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


