
# ErrorResponseError


## Properties

Name | Type
------------ | -------------
`code` | string
`message` | string
`details` | [Array&lt;ErrorResponseErrorDetailsInner&gt;](ErrorResponseErrorDetailsInner.md)
`requestId` | string
`traceId` | string
`quota` | [QuotaDetail](QuotaDetail.md)
`upgrade` | [UpgradeDetail](UpgradeDetail.md)

## Example

```typescript
import type { ErrorResponseError } from '@geoapi/client'

// TODO: Update the object below with actual values
const example = {
  "code": not_found,
  "message": The requested resource was not found,
  "details": null,
  "requestId": req_abc123,
  "traceId": 4bf92f3577b34da6a3ce929d0e0e4736,
  "quota": null,
  "upgrade": null,
} satisfies ErrorResponseError

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ErrorResponseError
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


