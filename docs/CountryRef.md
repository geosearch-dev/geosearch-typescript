
# CountryRef


## Properties

Name | Type
------------ | -------------
`isoCode` | string
`name` | string

## Example

```typescript
import type { CountryRef } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "isoCode": US,
  "name": United States,
} satisfies CountryRef

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as CountryRef
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


