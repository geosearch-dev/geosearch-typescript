# CountriesApi

All URIs are relative to *https://geosearch.dev*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**countryNeighbors**](CountriesApi.md#countryneighbors) | **GET** /v1/countries/{code}/neighbors | List neighboring countries |
| [**getCountry**](CountriesApi.md#getcountry) | **GET** /v1/countries/{code} | Get country by ISO code |
| [**listCountries**](CountriesApi.md#listcountries) | **GET** /v1/countries | List countries |
| [**listCountryRegions**](CountriesApi.md#listcountryregions) | **GET** /v1/countries/{code}/regions | List regions in a country |



## countryNeighbors

> CountryListResponse countryNeighbors(code, lang, fields)

List neighboring countries

Returns countries that share a border with the specified country.

### Example

```ts
import {
  Configuration,
  CountriesApi,
} from '@geosearch/client';
import type { CountryNeighborsRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CountriesApi(config);

  const body = {
    // string | ISO alpha-2 country code
    code: DE,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies CountryNeighborsRequest;

  try {
    const data = await api.countryNeighbors(body);
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
| **code** | `string` | ISO alpha-2 country code | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**CountryListResponse**](CountryListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of neighboring countries |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getCountry

> CountrySingleResponse getCountry(code, lang, fields)

Get country by ISO code

Returns a single country by its ISO alpha-2 code.

### Example

```ts
import {
  Configuration,
  CountriesApi,
} from '@geosearch/client';
import type { GetCountryRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CountriesApi(config);

  const body = {
    // string | ISO alpha-2 country code
    code: US,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies GetCountryRequest;

  try {
    const data = await api.getCountry(body);
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
| **code** | `string` | ISO alpha-2 country code | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**CountrySingleResponse**](CountrySingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Country details |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listCountries

> CountryListResponse listCountries(lang, continent, isoCode, populationMin, populationMax, cursor, limit, fields, sort)

List countries

Returns a paginated list of countries with optional filtering and sorting.

### Example

```ts
import {
  Configuration,
  CountriesApi,
} from '@geosearch/client';
import type { ListCountriesRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CountriesApi(config);

  const body = {
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // 'AF' | 'AN' | 'AS' | 'EU' | 'NA' | 'OC' | 'SA' | Filter by continent code (AF, AN, AS, EU, NA, OC, SA) (optional)
    continent: EU,
    // string | Filter by ISO alpha-2 codes (comma-separated) (optional)
    isoCode: US,CA,GB,
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
    // string | Sort field and direction. Allowed: name, population, area_sq_km. Prefix with - for descending. (optional)
    sort: -population,
  } satisfies ListCountriesRequest;

  try {
    const data = await api.listCountries(body);
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
| **continent** | `AF`, `AN`, `AS`, `EU`, `NA`, `OC`, `SA` | Filter by continent code (AF, AN, AS, EU, NA, OC, SA) | [Optional] [Defaults to `undefined`] [Enum: AF, AN, AS, EU, NA, OC, SA] |
| **isoCode** | `string` | Filter by ISO alpha-2 codes (comma-separated) | [Optional] [Defaults to `undefined`] |
| **populationMin** | `number` | Minimum population filter | [Optional] [Defaults to `undefined`] |
| **populationMax** | `number` | Maximum population filter | [Optional] [Defaults to `undefined`] |
| **cursor** | `string` | Pagination cursor from a previous response | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Number of results per page (1-100, default 25) | [Optional] [Defaults to `25`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |
| **sort** | `string` | Sort field and direction. Allowed: name, population, area_sq_km. Prefix with - for descending. | [Optional] [Defaults to `undefined`] |

### Return type

[**CountryListResponse**](CountryListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of countries |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listCountryRegions

> RegionListResponse listCountryRegions(code, lang, cursor, limit, fields, sort)

List regions in a country

Returns a paginated list of regions (administrative divisions) within a country.

### Example

```ts
import {
  Configuration,
  CountriesApi,
} from '@geosearch/client';
import type { ListCountryRegionsRequest } from '@geosearch/client';

async function example() {
  console.log("🚀 Testing @geosearch/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CountriesApi(config);

  const body = {
    // string | ISO alpha-2 country code
    code: US,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Pagination cursor from a previous response (optional)
    cursor: eyJpZCI6MjV9,
    // number | Number of results per page (1-100, default 25) (optional)
    limit: 25,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
    // string | Sort field. Allowed: name, population. (optional)
    sort: name,
  } satisfies ListCountryRegionsRequest;

  try {
    const data = await api.listCountryRegions(body);
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
| **code** | `string` | ISO alpha-2 country code | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
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
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

