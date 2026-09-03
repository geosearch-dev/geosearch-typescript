
# QuotaDetail

Structured detail accompanying a `quota_exceeded` 429. Present only on that response; absent from every other error body. It answers, in machine-readable form, what the limit is, how much was used, when it resets, and where to raise it — the same four facts `error.message` repeats in prose for the benefit of log lines and stack traces.

## Properties

Name | Type
------------ | -------------
`limit` | number
`used` | number
`resetsAt` | Date
`upgradeUrl` | string

## Example

```typescript
import type { QuotaDetail } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "limit": 2000000,
  "used": 2000000,
  "resetsAt": 2026-03-01T00:00:00Z,
  "upgradeUrl": https://geosearch.dev/dashboard/billing,
} satisfies QuotaDetail

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as QuotaDetail
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


