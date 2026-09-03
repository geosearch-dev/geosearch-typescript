
# AutocompleteResult


## Properties

Name | Type
------------ | -------------
`id` | number
`name` | string
`type` | string
`countryCode` | string
`population` | number

## Example

```typescript
import type { AutocompleteResult } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "id": 5391959,
  "name": San Francisco,
  "type": city,
  "countryCode": US,
  "population": 873965,
} satisfies AutocompleteResult

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as AutocompleteResult
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


