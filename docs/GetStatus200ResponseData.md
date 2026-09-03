
# GetStatus200ResponseData


## Properties

Name | Type
------------ | -------------
`status` | string
`database` | string

## Example

```typescript
import type { GetStatus200ResponseData } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "status": healthy,
  "database": connected,
} satisfies GetStatus200ResponseData

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as GetStatus200ResponseData
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


