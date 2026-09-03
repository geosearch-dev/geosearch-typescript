
# IPResultLocation


## Properties

Name | Type
------------ | -------------
`latitude` | number
`longitude` | number
`accuracyRadius` | number
`timezone` | string

## Example

```typescript
import type { IPResultLocation } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "latitude": 37.386,
  "longitude": -122.0838,
  "accuracyRadius": 1000,
  "timezone": America/Los_Angeles,
} satisfies IPResultLocation

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as IPResultLocation
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


