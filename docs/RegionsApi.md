# RegionsApi

All URIs are relative to *http://localhost*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getRegion**](RegionsApi.md#getregion) | **GET** /v1/regions/{id} | Get region by ID |
| [**listRegionCities**](RegionsApi.md#listregioncities) | **GET** /v1/regions/{id}/cities | List cities in a region |
| [**listRegions**](RegionsApi.md#listregions) | **GET** /v1/regions | List regions |
| [**regionChildren**](RegionsApi.md#regionchildren) | **GET** /v1/regions/{id}/children | List child cities of a region |



## getRegion

> RegionSingleResponse getRegion(id, lang, fields)

Get region by ID

Returns a single region by its numeric ID.

### Example

```ts
import {
  Configuration,
  RegionsApi,
} from '@geoapi/client';
import type { GetRegionRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new RegionsApi(config);

  const body = {
    // number | Region ID
    id: 5332921,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies GetRegionRequest;

  try {
    const data = await api.getRegion(body);
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
| **id** | `number` | Region ID | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**RegionSingleResponse**](RegionSingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Region details |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listRegionCities

> CityListResponse listRegionCities(id, lang, cursor, limit, fields, sort)

List cities in a region

Returns a paginated list of cities within a specific region.  THIS ENDPOINT AND &#x60;/v1/cities?within&#x3D;&#x60; ANSWER DIFFERENT QUESTIONS AND WILL SOMETIMES RETURN DIFFERENT CITIES FOR THE SAME REGION. That is intended, not a bug. This endpoint answers the ADMINISTRATIVE question — which cities are assigned to this region by GeoNames\&#39; own admin codes — while &#x60;?within&#x3D;&#x60; answers the GEOMETRIC one, which cities fall inside the region\&#39;s polygon. The two disagree wherever an enclave, an exclave or a blank admin code puts a city\&#39;s assignment at odds with its location.  Use this endpoint when you want the official assignment; use &#x60;/v1/cities?within&#x3D;&#x60; when you want what is physically inside the boundary. This one is charged at the standard 1 unit; &#x60;?within&#x3D;&#x60; costs 2.

### Example

```ts
import {
  Configuration,
  RegionsApi,
} from '@geoapi/client';
import type { ListRegionCitiesRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new RegionsApi(config);

  const body = {
    // number | Region ID
    id: 5332921,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Pagination cursor from a previous response (optional)
    cursor: eyJpZCI6MjV9,
    // number | Number of results per page (1-100, default 25) (optional)
    limit: 25,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
    // string | Sort field. Allowed: name, population. (optional)
    sort: -population,
  } satisfies ListRegionCitiesRequest;

  try {
    const data = await api.listRegionCities(body);
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
| **id** | `number` | Region ID | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **cursor** | `string` | Pagination cursor from a previous response | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Number of results per page (1-100, default 25) | [Optional] [Defaults to `25`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |
| **sort** | `string` | Sort field. Allowed: name, population. | [Optional] [Defaults to `undefined`] |

### Return type

[**CityListResponse**](CityListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of cities |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listRegions

> RegionListResponse listRegions(lang, country, level, populationMin, populationMax, cursor, limit, fields, sort)

List regions

Returns a paginated list of regions with optional filtering by country, level, and population.

### Example

```ts
import {
  Configuration,
  RegionsApi,
} from '@geoapi/client';
import type { ListRegionsRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new RegionsApi(config);

  const body = {
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Filter by ISO alpha-2 country code (optional)
    country: US,
    // number | Filter by administrative level (optional)
    level: 1,
    // number | Minimum population filter (optional)
    populationMin: 1000000,
    // number | Maximum population filter (optional)
    populationMax: 10000000,
    // string | Pagination cursor from a previous response (optional)
    cursor: eyJpZCI6MjV9,
    // number | Number of results per page (1-100, default 25) (optional)
    limit: 25,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
    // string | Sort field. Allowed: name, population. (optional)
    sort: -population,
  } satisfies ListRegionsRequest;

  try {
    const data = await api.listRegions(body);
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
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **country** | `string` | Filter by ISO alpha-2 country code | [Optional] [Defaults to `undefined`] |
| **level** | `number` | Filter by administrative level | [Optional] [Defaults to `undefined`] |
| **populationMin** | `number` | Minimum population filter | [Optional] [Defaults to `undefined`] |
| **populationMax** | `number` | Maximum population filter | [Optional] [Defaults to `undefined`] |
| **cursor** | `string` | Pagination cursor from a previous response | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Number of results per page (1-100, default 25) | [Optional] [Defaults to `25`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |
| **sort** | `string` | Sort field. Allowed: name, population. | [Optional] [Defaults to `undefined`] |

### Return type

[**RegionListResponse**](RegionListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of regions |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## regionChildren

> CityListResponse regionChildren(id, lang, fields)

List child cities of a region

Returns all cities that are direct children of the specified region in the administrative hierarchy.

### Example

```ts
import {
  Configuration,
  RegionsApi,
} from '@geoapi/client';
import type { RegionChildrenRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new RegionsApi(config);

  const body = {
    // number | Region ID
    id: 5332921,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies RegionChildrenRequest;

  try {
    const data = await api.regionChildren(body);
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
| **id** | `number` | Region ID | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**CityListResponse**](CityListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of child cities |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

