
# IPResult


## Properties

Name | Type
------------ | -------------
`ip` | string
`network` | string
`continent` | [IPResultContinent](IPResultContinent.md)
`country` | [IPResultCountry](IPResultCountry.md)
`region` | [IPResultRegion](IPResultRegion.md)
`city` | [IPResultCity](IPResultCity.md)
`postal` | [IPResultPostal](IPResultPostal.md)
`location` | [IPResultLocation](IPResultLocation.md)
`isAnonymousProxy` | boolean
`isSatelliteProvider` | boolean

## Example

```typescript
import type { IPResult } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "ip": 8.8.8.8,
  "network": 8.8.8.0/24,
  "continent": null,
  "country": null,
  "region": null,
  "city": null,
  "postal": null,
  "location": null,
  "isAnonymousProxy": false,
  "isSatelliteProvider": false,
} satisfies IPResult

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as IPResult
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


