
# City


## Properties

Name | Type
------------ | -------------
`id` | number
`geonameId` | number
`name` | string
`asciiName` | string
`countryCode` | string
`admin1Code` | string
`admin2Code` | string
`population` | number
`elevation` | number
`timezone` | string
`latitude` | number
`longitude` | number
`country` | [CountryRef](CountryRef.md)
`region` | [RegionRef](RegionRef.md)

## Example

```typescript
import type { City } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "id": 5391959,
  "geonameId": 5391959,
  "name": San Francisco,
  "asciiName": San Francisco,
  "countryCode": US,
  "admin1Code": CA,
  "admin2Code": 075,
  "population": 873965,
  "elevation": 16,
  "timezone": America/Los_Angeles,
  "latitude": 37.77493,
  "longitude": -122.41942,
  "country": null,
  "region": null,
} satisfies City

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as City
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


