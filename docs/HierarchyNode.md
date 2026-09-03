
# HierarchyNode


## Properties

Name | Type
------------ | -------------
`geonameId` | number
`name` | string
`type` | string
`depth` | number

## Example

```typescript
import type { HierarchyNode } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "geonameId": 5391959,
  "name": San Francisco,
  "type": city,
  "depth": 0,
} satisfies HierarchyNode

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as HierarchyNode
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


