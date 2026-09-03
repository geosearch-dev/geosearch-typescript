# BatchApi

All URIs are relative to *https://geosearch.dev*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**batchCities**](BatchApi.md#batchcities) | **POST** /v1/batch/cities | Batch lookup cities by IDs |
| [**batchCountries**](BatchApi.md#batchcountries) | **POST** /v1/batch/countries | Batch lookup countries by IDs |
| [**batchRegions**](BatchApi.md#batchregions) | **POST** /v1/batch/regions | Batch lookup regions by IDs |



## batchCities

> CityListResponse batchCities(batchRequest, lang, fields)

Batch lookup cities by IDs

Returns multiple cities in a single request. Maximum 50 IDs per request.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@geosearch/client';
import type { BatchCitiesRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new BatchApi(config);

  const body = {
    // BatchRequest
    batchRequest: {"ids":[5391959,5128581,4887398]},
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies BatchCitiesRequest;

  try {
    const data = await api.batchCities(body);
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
| **batchRequest** | [BatchRequest](BatchRequest.md) |  | |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**CityListResponse**](CityListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Batch city results |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## batchCountries

> CountryListResponse batchCountries(batchRequest, lang, fields)

Batch lookup countries by IDs

Returns multiple countries in a single request. Maximum 50 IDs per request.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@geosearch/client';
import type { BatchCountriesRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new BatchApi(config);

  const body = {
    // BatchRequest
    batchRequest: {"ids":[6252001,2635167,2921044]},
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies BatchCountriesRequest;

  try {
    const data = await api.batchCountries(body);
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
| **batchRequest** | [BatchRequest](BatchRequest.md) |  | |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**CountryListResponse**](CountryListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Batch country results |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## batchRegions

> RegionListResponse batchRegions(batchRequest, lang, fields)

Batch lookup regions by IDs

Returns multiple regions in a single request. Maximum 50 IDs per request.

### Example

```ts
import {
  Configuration,
  BatchApi,
} from '@geosearch/client';
import type { BatchRegionsRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new BatchApi(config);

  const body = {
    // BatchRequest
    batchRequest: {"ids":[5332921,5128638,4862182]},
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies BatchRegionsRequest;

  try {
    const data = await api.batchRegions(body);
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
| **batchRequest** | [BatchRequest](BatchRequest.md) |  | |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**RegionListResponse**](RegionListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Batch region results |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

