
# UpgradeDetail

Structured detail accompanying a `tier_upgrade_required` 403. Present only on that response; absent from every other error body.  ONE FIELD, DELIBERATELY. It says where to go and claims nothing else. It carries no limit, no usage and no reset instant, because none of those describe a plan that simply does not include the feature — there is no quantity to wait for and nothing resets.

## Properties

Name | Type
------------ | -------------
`upgradeUrl` | string

## Example

```typescript
import type { UpgradeDetail } from '@geosearch/client'

// TODO: Update the object below with actual values
const example = {
  "upgradeUrl": https://geosearch.dev/dashboard#billing,
} satisfies UpgradeDetail

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as UpgradeDetail
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


