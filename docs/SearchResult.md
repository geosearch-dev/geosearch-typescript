
# SearchResult


## Properties

Name | Type
------------ | -------------
`type` | string
`id` | number
`name` | string
`rank` | number
`country` | string
`population` | number
`latitude` | number
`longitude` | number

## Example

```typescript
import type { SearchResult } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "type": city,
  "id": 5391959,
  "name": San Francisco,
  "rank": 0.95,
  "country": US,
  "population": 873965,
  "latitude": 37.77493,
  "longitude": -122.41942,
} satisfies SearchResult

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SearchResult
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


