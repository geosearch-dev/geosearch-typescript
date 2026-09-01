
# TimezoneListResponse


## Properties

Name | Type
------------ | -------------
`data` | [Array&lt;Timezone&gt;](Timezone.md)
`meta` | [PaginationMeta](PaginationMeta.md)

## Example

```typescript
import type { TimezoneListResponse } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "data": null,
  "meta": null,
} satisfies TimezoneListResponse

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as TimezoneListResponse
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


