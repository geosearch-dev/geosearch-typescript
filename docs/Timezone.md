
# Timezone


## Properties

Name | Type
------------ | -------------
`id` | number
`countryCode` | string
`timezoneId` | string
`gmtOffset` | number
`dstOffset` | number
`rawOffset` | number

## Example

```typescript
import type { Timezone } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "id": null,
  "countryCode": US,
  "timezoneId": America/New_York,
  "gmtOffset": -5.0,
  "dstOffset": -4.0,
  "rawOffset": -5.0,
} satisfies Timezone

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as Timezone
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


