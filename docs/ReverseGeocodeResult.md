
# ReverseGeocodeResult


## Properties

Name | Type
------------ | -------------
`city` | [NearbyCity](NearbyCity.md)
`distanceKm` | number

## Example

```typescript
import type { ReverseGeocodeResult } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "city": null,
  "distanceKm": 0.3,
} satisfies ReverseGeocodeResult

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ReverseGeocodeResult
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


