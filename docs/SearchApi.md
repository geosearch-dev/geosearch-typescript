# SearchApi

All URIs are relative to *https://geosearch.dev*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**autocomplete**](SearchApi.md#autocomplete) | **GET** /v1/autocomplete | Autocomplete search |
| [**resolveCoordinate**](SearchApi.md#resolvecoordinate) | **GET** /v1/resolve | Resolve coordinates to their containing administrative areas |
| [**reverseGeocode**](SearchApi.md#reversegeocode) | **GET** /v1/reverse | Reverse geocode coordinates |
| [**search**](SearchApi.md#search) | **GET** /v1/search | Cross-type search |



## autocomplete

> AutocompleteListResponse autocomplete(q, lang, limit, fields)

Autocomplete search

Returns autocomplete suggestions matching a query string across cities, regions, and countries. Results are ranked by relevance and population. Minimum 2 characters required. 

### Example

```ts
import {
  Configuration,
  SearchApi,
} from '@geosearch/client';
import type { AutocompleteRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new SearchApi(config);

  const body = {
    // string | Search query (minimum 2 characters)
    q: San Fran,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // number | Maximum results to return (1-25, default 10) (optional)
    limit: 10,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies AutocompleteRequest;

  try {
    const data = await api.autocomplete(body);
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
| **q** | `string` | Search query (minimum 2 characters) | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Maximum results to return (1-25, default 10) | [Optional] [Defaults to `10`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**AutocompleteListResponse**](AutocompleteListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Autocomplete suggestions |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## resolveCoordinate

> HierarchyListResponse resolveCoordinate(lat, lon, lang)

Resolve coordinates to their containing administrative areas

Returns the administrative areas whose BOUNDARY POLYGONS CONTAIN the given coordinate, ordered country first.  ## How this differs from &#x60;/v1/reverse&#x60;  These two endpoints take the same parameters and answer different questions, and the difference is the reason both exist.  &#x60;/v1/reverse&#x60; returns the NEAREST city. It always returns something, and for a point near a border that something is sometimes in the neighbouring country.  &#x60;/v1/resolve&#x60; returns the areas that actually CONTAIN the point. It is never wrong about which country a point is in — and it sometimes returns nothing at all, because no polygon covers the point or because we hold no polygon for that country. Choose this endpoint when correctness at borders matters and choose &#x60;/v1/reverse&#x60; when you always need an answer.  ## &#x60;depth&#x60; RUNS THE OPPOSITE DIRECTION FROM &#x60;/v1/cities/{id}/hierarchy&#x60;  Read this before writing code that consumes both endpoints.  Both return the same node SHAPE — &#x60;geoname_id&#x60;, &#x60;name&#x60;, &#x60;type&#x60;, &#x60;depth&#x60; — so one rendering path can accept either. The &#x60;depth&#x60; SEMANTICS are inverted between them:  - On **this** endpoint &#x60;depth&#x60; is POSITIONAL, counting outward-in from   the largest area: **&#x60;depth: 0&#x60; is the COUNTRY**, &#x60;depth: 1&#x60; is the   region inside it, and so on. - On **&#x60;/v1/cities/{id}/hierarchy&#x60;** &#x60;depth&#x60; counts up from the entity   that was asked about: &#x60;depth: 0&#x60; is the CITY, and the country is at the   highest depth in the list.  So &#x60;data[0]&#x60; is the country here and the city there. Code that sorts or indexes on &#x60;depth&#x60; across both endpoints without accounting for this will silently invert the hierarchy rather than fail.  ## Cost and availability  One quota unit, on every plan including Free. This is a single indexed point-in-polygon probe returning names, not a geometry transfer, so it carries no premium and no tier gate.  &#x60;?fields&#x3D;&#x60; IS NOT SUPPORTED on this endpoint and is ignored if sent. The four node fields are all small, so selection would save nothing. 

### Example

```ts
import {
  Configuration,
  SearchApi,
} from '@geosearch/client';
import type { ResolveCoordinateRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new SearchApi(config);

  const body = {
    // number | Latitude (-90 to 90). Must be a finite number: `NaN` and `Infinity` are rejected with a 400 rather than being passed to the spatial index, which would answer them with an ordinary \"not found\".
    lat: 37.7749,
    // number | Longitude (-180 to 180). Must be a finite number; see `lat`.
    lon: -122.4194,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
  } satisfies ResolveCoordinateRequest;

  try {
    const data = await api.resolveCoordinate(body);
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
| **lat** | `number` | Latitude (-90 to 90). Must be a finite number: &#x60;NaN&#x60; and &#x60;Infinity&#x60; are rejected with a 400 rather than being passed to the spatial index, which would answer them with an ordinary \&quot;not found\&quot;. | [Defaults to `undefined`] |
| **lon** | `number` | Longitude (-180 to 180). Must be a finite number; see &#x60;lat&#x60;. | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |

### Return type

[**HierarchyListResponse**](HierarchyListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The administrative chain covering the coordinate, country first.  A ONE-ELEMENT RESPONSE IS A NORMAL SUCCESS, not a degraded answer: 3.8% of the corpus resolves to a country with no covering region. Do not treat a short chain as an error. |  -  |
| **400** | A missing, unparseable, non-finite or out-of-range &#x60;lat&#x60; or &#x60;lon&#x60;.  NOTE THE STATUS. Parameter failures on THIS endpoint are 400 &#x60;bad_request&#x60;, mirroring &#x60;/v1/reverse&#x60;, whose parameter contract this endpoint deliberately copies so that the generated SDK method reads &#x60;resolve(lat, lon)&#x60; beside &#x60;reverse(lat, lon)&#x60;. That is a different convention from &#x60;?simplify&#x3D;&#x60; on &#x60;/v1/boundaries/{geoname_id}&#x60;, which is a 422 &#x60;validation_error&#x60; with per-field &#x60;error.details&#x60;. The two are separate conventions on purpose, not an inconsistency to be harmonised away — treat them as two shapes when writing a client. |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | No administrative area covers the supplied coordinate.  EXACTLY ONE CODE, AND THE MESSAGE CLAIMS NOTHING ABOUT WHY. Two distinct situations produce this response — the point is in open water, or it is on land we hold no polygon for — and the server genuinely cannot tell them apart. Reporting a confident cause would be wrong a predictable fraction of the time, so it reports neither.  This is not an exotic path and should be handled as a normal outcome: measured over a random 19,558-city sample, 0.70% of cities resolve to no country polygon at all.  An empty 200 was rejected: an empty array cannot be told apart from a successful \&quot;nothing matched\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |
| **503** | The point-in-polygon probe exceeded the statement timeout that bounds it.  This is a 503 and NOT a 500, deliberately: the server is healthy and the request was valid — this one probe against an unusually complex set of candidate polygons simply ran out of its time budget. It is worth retrying.  There is no narrower query to send. This operation takes a single coordinate; there is no &#x60;bbox&#x60;, no &#x60;within&#x60; and no filter set to reduce. Retry, and if the failure persists for a particular coordinate, report it — a coordinate that reliably times out is a data problem on our side, not a malformed request on yours. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## reverseGeocode

> ReverseGeocodeSingleResponse reverseGeocode(lat, lon, fields)

Reverse geocode coordinates

Returns the nearest city for a given latitude/longitude. Uses PostGIS spatial index for fast reverse geocoding. 

### Example

```ts
import {
  Configuration,
  SearchApi,
} from '@geosearch/client';
import type { ReverseGeocodeRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new SearchApi(config);

  const body = {
    // number | Latitude (-90 to 90)
    lat: 37.7749,
    // number | Longitude (-180 to 180)
    lon: -122.4194,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies ReverseGeocodeRequest;

  try {
    const data = await api.reverseGeocode(body);
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
| **lat** | `number` | Latitude (-90 to 90) | [Defaults to `undefined`] |
| **lon** | `number` | Longitude (-180 to 180) | [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**ReverseGeocodeSingleResponse**](ReverseGeocodeSingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Reverse geocoding result |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## search

> SearchListResponse search(q, lang, type, limit, fields)

Cross-type search

Performs a fuzzy text search across countries, regions, and cities using trigram matching. Results are ranked by relevance and population. Uses simple limit pagination (no cursor). 

### Example

```ts
import {
  Configuration,
  SearchApi,
} from '@geosearch/client';
import type { SearchRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new SearchApi(config);

  const body = {
    // string | Search query (minimum 2 characters)
    q: San Fran,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Filter by entity type (comma-separated). Allowed: country, region, city. (optional)
    type: city,
    // number | Maximum results to return (1-100, default 25) (optional)
    limit: 10,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies SearchRequest;

  try {
    const data = await api.search(body);
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
| **q** | `string` | Search query (minimum 2 characters) | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **type** | `string` | Filter by entity type (comma-separated). Allowed: country, region, city. | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Maximum results to return (1-100, default 25) | [Optional] [Defaults to `25`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**SearchListResponse**](SearchListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Search results |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

