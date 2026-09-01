
# Region


## Properties

Name | Type
------------ | -------------
`id` | number
`geonameId` | number
`countryCode` | string
`adminCode` | string
`name` | string
`asciiName` | string
`level` | number
`parentGeonameId` | number
`population` | number
`latitude` | number
`longitude` | number
`country` | [CountryRef](CountryRef.md)
`geometry` | [GeoJSONMultiPolygon](GeoJSONMultiPolygon.md)

## Example

```typescript
import type { Region } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "id": 5332921,
  "geonameId": 5332921,
  "countryCode": US,
  "adminCode": CA,
  "name": California,
  "asciiName": California,
  "level": 1,
  "parentGeonameId": null,
  "population": 39538223,
  "latitude": 36.778,
  "longitude": -119.418,
  "country": null,
  "geometry": null,
} satisfies Region

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Region
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


