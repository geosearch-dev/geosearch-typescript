# IPGeolocationApi

All URIs are relative to *https://geosearch.dev*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**lookupIP**](IPGeolocationApi.md#lookupip) | **GET** /v1/ip/{address} | IP geolocation lookup |
| [**lookupMyIP**](IPGeolocationApi.md#lookupmyip) | **GET** /v1/ip/me | Caller\&#39;s IP geolocation |



## lookupIP

> IPSingleResponse lookupIP(address, lang, fields)

IP geolocation lookup

Returns geolocation data for a given IPv4 or IPv6 address.

### Example

```ts
import {
  Configuration,
  IPGeolocationApi,
} from '@geosearch/client';
import type { LookupIPRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new IPGeolocationApi(config);

  const body = {
    // string | IPv4 or IPv6 address
    address: 8.8.8.8,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies LookupIPRequest;

  try {
    const data = await api.lookupIP(body);
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
| **address** | `string` | IPv4 or IPv6 address | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**IPSingleResponse**](IPSingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | IP geolocation result |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **422** | Invalid IP address format |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## lookupMyIP

> IPSingleResponse lookupMyIP(lang, fields)

Caller\&#39;s IP geolocation

Auto-detects the client\&#39;s IP address (from X-Forwarded-For or RemoteAddr) and returns its geolocation data. 

### Example

```ts
import {
  Configuration,
  IPGeolocationApi,
} from '@geosearch/client';
import type { LookupMyIPRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new IPGeolocationApi(config);

  const body = {
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies LookupMyIPRequest;

  try {
    const data = await api.lookupMyIP(body);
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
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**IPSingleResponse**](IPSingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Caller\&#39;s IP geolocation result |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

