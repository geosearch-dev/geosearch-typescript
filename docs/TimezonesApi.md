# TimezonesApi

All URIs are relative to *https://geosearch.dev*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getTimezone**](TimezonesApi.md#gettimezone) | **GET** /v1/timezones/{tzId} | Get timezone by IANA ID |
| [**listTimezones**](TimezonesApi.md#listtimezones) | **GET** /v1/timezones | List timezones |



## getTimezone

> TimezoneSingleResponse getTimezone(tzId, lang, fields)

Get timezone by IANA ID

Returns a single timezone by its IANA identifier. Note: IANA timezone IDs contain slashes (e.g., America/New_York), so the path uses a wildcard match. 

### Example

```ts
import {
  Configuration,
  TimezonesApi,
} from '@geoapi/client';
import type { GetTimezoneRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new TimezonesApi(config);

  const body = {
    // string | IANA timezone ID (e.g., America/New_York)
    tzId: America/New_York,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies GetTimezoneRequest;

  try {
    const data = await api.getTimezone(body);
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
| **tzId** | `string` | IANA timezone ID (e.g., America/New_York) | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**TimezoneSingleResponse**](TimezoneSingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Timezone details |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listTimezones

> TimezoneListResponse listTimezones(lang, country, cursor, limit, fields, sort)

List timezones

Returns a paginated list of timezones with optional filtering by country.

### Example

```ts
import {
  Configuration,
  TimezonesApi,
} from '@geoapi/client';
import type { ListTimezonesRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new TimezonesApi(config);

  const body = {
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Filter by ISO alpha-2 country code (optional)
    country: US,
    // string | Pagination cursor from a previous response (optional)
    cursor: eyJpZCI6MjV9,
    // number | Number of results per page (1-100, default 25) (optional)
    limit: 25,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
    // string | Sort field. Allowed: timezone_id, gmt_offset, country_code. (optional)
    sort: gmt_offset,
  } satisfies ListTimezonesRequest;

  try {
    const data = await api.listTimezones(body);
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
| **cursor** | `string` | Pagination cursor from a previous response | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Number of results per page (1-100, default 25) | [Optional] [Defaults to `25`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |
| **sort** | `string` | Sort field. Allowed: timezone_id, gmt_offset, country_code. | [Optional] [Defaults to `undefined`] |

### Return type

[**TimezoneListResponse**](TimezoneListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of timezones |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

