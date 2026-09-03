# BoundariesApi

All URIs are relative to *https://geosearch.dev*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getBoundary**](BoundariesApi.md#getboundary) | **GET** /v1/boundaries/{geoname_id} | Fetch an area\&#39;s boundary polygon as GeoJSON |



## getBoundary

> BoundarySingleResponse getBoundary(geonameId, simplify, lang)

Fetch an area\&#39;s boundary polygon as GeoJSON

Returns the boundary polygon for one country or region as a bare GeoJSON geometry.  ## COSTS 5 QUOTA UNITS  This endpoint charges five units against the monthly quota, not one. The premium is priced on PAYLOAD rather than on query time: country GeoJSON averages 62.6 KB and reaches 1.9 MB, and region GeoJSON reaches 2.8 MB — two to three orders of magnitude above an ordinary list response.  &#x60;?simplify&#x3D;&#x60; does NOT reduce the cost. It trades server CPU for client bytes (simplification measures 209–248 ms against 10.3 ms for the plain fetch), so the route is expensive to serve either way.  REJECTIONS COST ONE UNIT, NOT FIVE. A 400, a 422, either 404 and the 403 below all charge the standard single unit, so probing which ids are fetchable — and bouncing off the paywall — is not billed at the premium rate. Only a request that actually reaches the polygon fetch is charged five, including one that reaches it and then times out.  ## Plan requirements  REGION boundaries require a paid plan. COUNTRY boundaries are available on every plan, including Free. A Free key requesting a region boundary receives a 403 &#x60;tier_upgrade_required&#x60; carrying an upgrade link — a visible refusal, not a silent omission.  This is the same split the &#x60;geometry&#x60; field follows on the country and region endpoints, with one deliberate difference: there the field is simply absent from a 200, while here the refusal is explicit and tells you what to do about it.  ## Response shape  &#x60;data.geometry&#x60; is a BARE GeoJSON geometry — the &#x60;{\&quot;type\&quot;: ..., \&quot;coordinates\&quot;: ...}&#x60; object — and NOT a GeoJSON &#x60;Feature&#x60;. There is no &#x60;properties&#x60; wrapper; the three sibling fields carry that information. This matches the geometry &#x60;/v1/countries/{code}&#x60; and &#x60;/v1/regions/{id}&#x60; already return.  &#x60;type&#x60; is &#x60;Polygon&#x60; OR &#x60;MultiPolygon&#x60;. Do not pin it: applying &#x60;?simplify&#x3D;&#x60; can collapse a MultiPolygon into a Polygon for areas whose smaller parts disappear at the requested tolerance.  &#x60;?fields&#x3D;&#x60; IS NOT SUPPORTED on this endpoint and is ignored if sent. Field selection here works by serialising the whole object and then dropping keys, so &#x60;?fields&#x3D;name&#x60; on a 1.9 MB polygon would build the polygon in full and discard it — strictly more expensive than not sending the parameter. Callers who want only the name should use &#x60;/v1/countries/{code}&#x60; or &#x60;/v1/regions/{id}&#x60;. 

### Example

```ts
import {
  Configuration,
  BoundariesApi,
} from '@geosearch/client';
import type { GetBoundaryRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new BoundariesApi(config);

  const body = {
    // number | GeoNames id of a country or a region. A city id — or any id that does not name an area — is a 404 `area_not_an_area`, not a 400.
    geonameId: 6252001,
    // number | Douglas-Peucker tolerance in EPSG:4326 DEGREES, applied before the polygon is serialised. Omit it for full precision.  DEGREES, NOT METRES. The upper bound of 10 is roughly 1,100 km, chosen to make the unit obviously wrong to anyone who typed a value in metres. Simplification stops changing the shape above about 1 degree, so values beyond that buy nothing.  `0` is accepted and is a no-op: the response reports `simplify: null`, because no tolerance was actually applied.  A negative, non-finite or out-of-range value is a 422, never a 500.  SUPPLY IT AT MOST ONCE. `?simplify=0.01&simplify=0.5` is a 422 rather than a request served with one of the two values silently dropped: two tolerances are two conflicting instructions, and the server does not guess which was meant. (optional)
    simplify: 0.01,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
  } satisfies GetBoundaryRequest;

  try {
    const data = await api.getBoundary(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **geonameId** | `number` | GeoNames id of a country or a region. A city id — or any id that does not name an area — is a 404 &#x60;area_not_an_area&#x60;, not a 400. | [Defaults to `undefined`] |
| **simplify** | `number` | Douglas-Peucker tolerance in EPSG:4326 DEGREES, applied before the polygon is serialised. Omit it for full precision.  DEGREES, NOT METRES. The upper bound of 10 is roughly 1,100 km, chosen to make the unit obviously wrong to anyone who typed a value in metres. Simplification stops changing the shape above about 1 degree, so values beyond that buy nothing.  &#x60;0&#x60; is accepted and is a no-op: the response reports &#x60;simplify: null&#x60;, because no tolerance was actually applied.  A negative, non-finite or out-of-range value is a 422, never a 500.  SUPPLY IT AT MOST ONCE. &#x60;?simplify&#x3D;0.01&amp;simplify&#x3D;0.5&#x60; is a 422 rather than a request served with one of the two values silently dropped: two tolerances are two conflicting instructions, and the server does not guess which was meant. | [Optional] [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |

### Return type

[**BoundarySingleResponse**](BoundarySingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The area\&#39;s boundary polygon. |  -  |
| **400** | The path segment is not an integer. A malformed id is a 400 rather than a 404, so a typo is distinguishable from a coverage gap. |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **403** | The authenticated key\&#39;s plan does not include the requested feature.  NOT RETRYABLE, AND THIS MATTERS FOR CLIENT CODE. Generated SDKs and hand-written clients commonly retry 429 with backoff. This is a 403 and must not be routed into that path: no amount of waiting changes the answer, because nothing is exhausted and no window resets. The only resolution is to raise the plan at &#x60;error.upgrade.upgrade_url&#x60;.  It carries no &#x60;Retry-After&#x60; and no &#x60;X-RateLimit-*&#x60; semantics of its own, which is the machine-readable form of the same statement. |  -  |
| **404** | No boundary can be returned for that id. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;area_not_an_area&#x60; means the id does not name a country or a region at all, and &#x60;area_no_boundary&#x60; means it names a real area for which no boundary polygon is held. One is a mistake the caller can fix; the other is a limit of our data that they cannot.  &#x60;area_no_boundary&#x60; is returned REGARDLESS OF PLAN, and is checked before the plan is. A Free key asking about a region we hold no polygon for is told we do not have it, not that an upgrade would produce it — an upgrade would not. |  -  |
| **422** | &#x60;simplify&#x60; was malformed. &#x60;error.details&#x60; names the field and what was wrong with it.  A 422 HERE, WHERE &#x60;/v1/resolve&#x60; USES 400 FOR ITS COORDINATES. That is deliberate: this is a shape failure decidable from the request text alone and it has a field name to report, which is this API\&#39;s 422 convention. The two endpoints follow two conventions; see the 400 on &#x60;/v1/resolve&#x60;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |
| **503** | Building the boundary polygon exceeded the statement timeout that bounds it.  This is a 503 and NOT a 500, deliberately: the server is healthy and the request was valid — this one polygon is large enough that assembling and serialising it ran out of its time budget. It is worth retrying.  THE EFFECTIVE REMEDY ON THIS ROUTE IS &#x60;simplify&#x60;, not &#x60;bbox&#x60; — this operation has no &#x60;bbox&#x60; and no &#x60;within&#x60;. A larger tolerance means fewer vertices to generalise, serialise and transmit, so a request that times out at the full resolution frequently succeeds at &#x60;?simplify&#x3D;0.01&#x60;. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

