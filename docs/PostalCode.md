
# PostalCode


## Properties

Name | Type
------------ | -------------
`id` | number
`countryCode` | string
`postalCode` | string
`placeName` | string
`adminName1` | string
`adminCode1` | string
`adminName2` | string
`adminCode2` | string
`adminName3` | string
`adminCode3` | string
`latitude` | number
`longitude` | number
`accuracy` | number
`country` | [CountryRef](CountryRef.md)

## Example

```typescript
import type { PostalCode } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "id": 1140425,
  "countryCode": US,
  "postalCode": 94105,
  "placeName": San Francisco,
  "adminName1": California,
  "adminCode1": CA,
  "adminName2": San Francisco,
  "adminCode2": 075,
  "adminName3": ,
  "adminCode3": ,
  "latitude": 37.7864,
  "longitude": -122.3892,
  "accuracy": 4,
  "country": null,
} satisfies PostalCode

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as PostalCode
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


