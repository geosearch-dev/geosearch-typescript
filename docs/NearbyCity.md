
# NearbyCity


## Properties

Name | Type
------------ | -------------
`id` | number
`name` | string
`countryCode` | string
`population` | number
`timezone` | string
`latitude` | number
`longitude` | number
`distanceKm` | number
`country` | [CountryRef](CountryRef.md)
`region` | [RegionRef](RegionRef.md)

## Example

```typescript
import type { NearbyCity } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "id": 5391959,
  "name": San Francisco,
  "countryCode": US,
  "population": 873965,
  "timezone": America/Los_Angeles,
  "latitude": 37.77493,
  "longitude": -122.41942,
  "distanceKm": 12.5,
  "country": null,
  "region": null,
} satisfies NearbyCity

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as NearbyCity
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


