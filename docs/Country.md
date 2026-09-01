
# Country


## Properties

Name | Type
------------ | -------------
`id` | number
`geonameId` | number
`isoCode` | string
`iso3Code` | string
`isoNumeric` | number
`fipsCode` | string
`name` | string
`capital` | string
`areaSqKm` | number
`population` | number
`continentCode` | string
`tld` | string
`currencyCode` | string
`currencyName` | string
`phone` | string
`postalCodeFormat` | string
`postalCodeRegex` | string
`languages` | Array&lt;string&gt;
`neighbours` | Array&lt;string&gt;
`latitude` | number
`longitude` | number
`flagEmoji` | string
`geometry` | [GeoJSONMultiPolygon](GeoJSONMultiPolygon.md)

## Example

```typescript
import type { Country } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "id": 1,
  "geonameId": 6252001,
  "isoCode": US,
  "iso3Code": USA,
  "isoNumeric": 840,
  "fipsCode": US,
  "name": United States,
  "capital": Washington,
  "areaSqKm": 9833520.0,
  "population": 331002651,
  "continentCode": NA,
  "tld": .us,
  "currencyCode": USD,
  "currencyName": Dollar,
  "phone": 1,
  "postalCodeFormat": #####-####,
  "postalCodeRegex": ^\d{5}(-\d{4})?$,
  "languages": [en-US, es-US],
  "neighbours": [CA, MX],
  "latitude": 39.76,
  "longitude": -98.5,
  "flagEmoji": null,
  "geometry": null,
} satisfies Country

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Country
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


