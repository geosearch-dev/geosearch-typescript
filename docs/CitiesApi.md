# CitiesApi

All URIs are relative to *http://localhost*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**cityHierarchy**](CitiesApi.md#cityhierarchy) | **GET** /v1/cities/{id}/hierarchy | Get administrative hierarchy for a city |
| [**getCity**](CitiesApi.md#getcity) | **GET** /v1/cities/{id} | Get city by ID |
| [**listCities**](CitiesApi.md#listcities) | **GET** /v1/cities | List cities |
| [**nearbyCities**](CitiesApi.md#nearbycities) | **GET** /v1/cities/nearby | Find nearby cities |



## cityHierarchy

> HierarchyListResponse cityHierarchy(id, lang)

Get administrative hierarchy for a city

Returns the full administrative hierarchy for a city, ordered from the city itself up through region, country, and continent. 

### Example

```ts
import {
  Configuration,
  CitiesApi,
} from '@geoapi/client';
import type { CityHierarchyRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CitiesApi(config);

  const body = {
    // number | City ID
    id: 5391959,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
  } satisfies CityHierarchyRequest;

  try {
    const data = await api.cityHierarchy(body);
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
| **id** | `number` | City ID | [Defaults to `undefined`] |
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
| **200** | Administrative hierarchy |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getCity

> CitySingleResponse getCity(id, lang, fields)

Get city by ID

Returns a single city by its numeric ID.

### Example

```ts
import {
  Configuration,
  CitiesApi,
} from '@geoapi/client';
import type { GetCityRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CitiesApi(config);

  const body = {
    // number | City ID
    id: 5391959,
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies GetCityRequest;

  try {
    const data = await api.getCity(body);
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
| **id** | `number` | City ID | [Defaults to `undefined`] |
| **lang** | `string` | ISO 639-1 language code for localized names (e.g., de, fr, ja) | [Optional] [Defaults to `undefined`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**CitySingleResponse**](CitySingleResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | City details |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **404** | Resource not found |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## listCities

> CityListResponse listCities(lang, country, admin1, name, populationMin, populationMax, timezone, minElevation, maxElevation, within, bbox, cursor, limit, fields, sort)

List cities

Returns a paginated list of cities with optional filtering by country, admin code, name, population, timezone, and elevation.

### Example

```ts
import {
  Configuration,
  CitiesApi,
} from '@geoapi/client';
import type { ListCitiesRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CitiesApi(config);

  const body = {
    // string | ISO 639-1 language code for localized names (e.g., de, fr, ja) (optional)
    lang: de,
    // string | Filter by ISO alpha-2 country codes (comma-separated) (optional)
    country: US,CA,
    // string | Filter by admin1 code (state/province) (optional)
    admin1: CA,
    // string | Filter by city name (trigram fuzzy search) (optional)
    name: San Fran,
    // number | Minimum population filter (optional)
    populationMin: 1000000,
    // number | Maximum population filter (optional)
    populationMax: 10000000,
    // string | Filter by IANA timezone ID (optional)
    timezone: America/Los_Angeles,
    // number | Minimum elevation in meters (optional)
    minElevation: 500,
    // number | Maximum elevation in meters (optional)
    maxElevation: 3000,
    // number | Return only results whose coordinates fall geometrically inside the boundary of the given area, identified by its GeoNames id. Countries and administrative regions are valid areas; a city id is not.  Accepts exactly one id. A COMMA-SEPARATED LIST IS REJECTED with a 422 naming the limit — a deliberate departure from the comma-separated convention `country` uses, because each value would be a separate polygon intersection. Ask for one area per request.  COST: a request using this parameter consumes 2 quota units instead of 1, on every plan including Free. Combining it with `bbox` still costs 2, not 3 — the highest multiplier applies rather than the sum, and adding a box makes the query cheaper to serve, so it is never penalised.  This asks a GEOMETRIC question and can therefore return a different set of cities than `/v1/regions/{id}/cities`, which asks an administrative one. See that endpoint\'s description for when and why the two disagree.  Two failures are reported with distinct 400 codes so a typo is distinguishable from a coverage gap: `area_not_an_area` means the id does not name a country or region at all, and `area_no_boundary` means it does but no boundary polygon is available for it yet. (optional)
    within: 6252001,
    // string | Return only results inside the bounding box, given as four comma-separated numbers in the order `w,s,e,n` — west longitude, south latitude, east longitude, north latitude.  Longitudes must be within [-180, 180] and latitudes within [-90, 90].  A box where WEST IS GREATER THAN EAST wraps the antimeridian and is fully supported: `bbox=170,-20,-170,-10` is a box around Fiji, evaluated as the union of the two halves it spans. Latitude has no equivalent wrap-around meaning, so `s` greater than `n` is a validation error rather than a wrapped box.  Charged at the standard request cost of 1 unit. Adding it to a `within` query narrows the candidate set before the polygon test and does not raise the charge. (optional)
    bbox: -122.6,37.6,-122.2,37.9,
    // string | Pagination cursor from a previous response (optional)
    cursor: eyJpZCI6MjV9,
    // number | Number of results per page (1-100, default 25) (optional)
    limit: 25,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
    // string | Sort field. Allowed: name, population, elevation, id. (optional)
    sort: -population,
  } satisfies ListCitiesRequest;

  try {
    const data = await api.listCities(body);
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
| **country** | `string` | Filter by ISO alpha-2 country codes (comma-separated) | [Optional] [Defaults to `undefined`] |
| **admin1** | `string` | Filter by admin1 code (state/province) | [Optional] [Defaults to `undefined`] |
| **name** | `string` | Filter by city name (trigram fuzzy search) | [Optional] [Defaults to `undefined`] |
| **populationMin** | `number` | Minimum population filter | [Optional] [Defaults to `undefined`] |
| **populationMax** | `number` | Maximum population filter | [Optional] [Defaults to `undefined`] |
| **timezone** | `string` | Filter by IANA timezone ID | [Optional] [Defaults to `undefined`] |
| **minElevation** | `number` | Minimum elevation in meters | [Optional] [Defaults to `undefined`] |
| **maxElevation** | `number` | Maximum elevation in meters | [Optional] [Defaults to `undefined`] |
| **within** | `number` | Return only results whose coordinates fall geometrically inside the boundary of the given area, identified by its GeoNames id. Countries and administrative regions are valid areas; a city id is not.  Accepts exactly one id. A COMMA-SEPARATED LIST IS REJECTED with a 422 naming the limit — a deliberate departure from the comma-separated convention &#x60;country&#x60; uses, because each value would be a separate polygon intersection. Ask for one area per request.  COST: a request using this parameter consumes 2 quota units instead of 1, on every plan including Free. Combining it with &#x60;bbox&#x60; still costs 2, not 3 — the highest multiplier applies rather than the sum, and adding a box makes the query cheaper to serve, so it is never penalised.  This asks a GEOMETRIC question and can therefore return a different set of cities than &#x60;/v1/regions/{id}/cities&#x60;, which asks an administrative one. See that endpoint\&#39;s description for when and why the two disagree.  Two failures are reported with distinct 400 codes so a typo is distinguishable from a coverage gap: &#x60;area_not_an_area&#x60; means the id does not name a country or region at all, and &#x60;area_no_boundary&#x60; means it does but no boundary polygon is available for it yet. | [Optional] [Defaults to `undefined`] |
| **bbox** | `string` | Return only results inside the bounding box, given as four comma-separated numbers in the order &#x60;w,s,e,n&#x60; — west longitude, south latitude, east longitude, north latitude.  Longitudes must be within [-180, 180] and latitudes within [-90, 90].  A box where WEST IS GREATER THAN EAST wraps the antimeridian and is fully supported: &#x60;bbox&#x3D;170,-20,-170,-10&#x60; is a box around Fiji, evaluated as the union of the two halves it spans. Latitude has no equivalent wrap-around meaning, so &#x60;s&#x60; greater than &#x60;n&#x60; is a validation error rather than a wrapped box.  Charged at the standard request cost of 1 unit. Adding it to a &#x60;within&#x60; query narrows the candidate set before the polygon test and does not raise the charge. | [Optional] [Defaults to `undefined`] |
| **cursor** | `string` | Pagination cursor from a previous response | [Optional] [Defaults to `undefined`] |
| **limit** | `number` | Number of results per page (1-100, default 25) | [Optional] [Defaults to `25`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |
| **sort** | `string` | Sort field. Allowed: name, population, elevation, id. | [Optional] [Defaults to `undefined`] |

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
| **400** | Invalid request. Distinguish the cases by &#x60;error.code&#x60;: &#x60;bad_request&#x60; is a malformed cursor, sort or pagination value; &#x60;area_not_an_area&#x60; means the &#x60;within&#x60; id does not name a country or region; &#x60;area_no_boundary&#x60; means it names a real area for which no boundary polygon is available. The last two are separate codes on purpose — one is a mistake the caller can fix, the other is a limit of our data that they cannot. |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **422** | One or more query parameters were malformed. &#x60;error.details&#x60; names each offending field and what was wrong with it. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |
| **503** | The containment query exceeded the statement timeout that bounds it.  This is a 503 and NOT a 500, deliberately: the server is healthy and the request was valid — this one query against an unusually large or complex boundary simply ran out of its time budget. It is therefore worth retrying, and worth retrying with a narrower query. Adding &#x60;bbox&#x60; or further filters alongside &#x60;within&#x60; reduces the candidate set before the polygon test and is the most effective remedy.  THIS RESPONSE BELONGS TO THE &#x60;within&#x3D;&#x60; ROUTES ONLY. &#x60;GET /v1/resolve&#x60; and &#x60;GET /v1/boundaries/{geoname_id}&#x60; have their own 503 components (&#x60;ResolveQueryTimeout&#x60; and &#x60;BoundaryQueryTimeout&#x60;) because the remedy above is false on both: neither accepts &#x60;bbox&#x60; or &#x60;within&#x60;. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## nearbyCities

> NearbyCityListResponse nearbyCities(lat, lon, radius, limit, fields)

Find nearby cities

Returns cities near a given latitude/longitude within a specified radius. Results are ordered by distance. Uses PostGIS spatial index for fast lookups. 

### Example

```ts
import {
  Configuration,
  CitiesApi,
} from '@geoapi/client';
import type { NearbyCitiesRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new CitiesApi(config);

  const body = {
    // number | Latitude (-90 to 90)
    lat: 37.7749,
    // number | Longitude (-180 to 180)
    lon: -122.4194,
    // number | Search radius in kilometers (default 50, max 200) (optional)
    radius: 50,
    // number | Maximum results to return (1-250, default 10) (optional)
    limit: 10,
    // string | Comma-separated list of fields to include in the response (optional)
    fields: name,population,iso_code,
  } satisfies NearbyCitiesRequest;

  try {
    const data = await api.nearbyCities(body);
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
| **radius** | `number` | Search radius in kilometers (default 50, max 200) | [Optional] [Defaults to `50`] |
| **limit** | `number` | Maximum results to return (1-250, default 10) | [Optional] [Defaults to `10`] |
| **fields** | `string` | Comma-separated list of fields to include in the response | [Optional] [Defaults to `undefined`] |

### Return type

[**NearbyCityListResponse**](NearbyCityListResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Nearby cities with distance |  -  |
| **400** | Invalid request parameters |  -  |
| **401** | Missing or invalid API key. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;authentication_required&#x60; means no key was supplied at all, and &#x60;authentication_failed&#x60; means a key was supplied and is not valid.  The distinction is worth branching on, because the remedies differ: the first is \&quot;sign up and send a key\&quot;, the second is \&quot;the key you sent is wrong, revoked or mistyped\&quot;. |  -  |
| **429** | Rate limit exceeded. Distinguish the two cases by &#x60;error.code&#x60;: &#x60;rate_limit_exceeded&#x60; is the per-second throttle and clears within a second; &#x60;quota_exceeded&#x60; is the monthly allowance and carries an &#x60;error.quota&#x60; object describing the limit, the usage, the period end and where to upgrade. |  * X-RateLimit-Limit - Requests per second allowed <br>  * X-RateLimit-Remaining - Requests remaining in current window <br>  * X-RateLimit-Reset - Unix epoch second at which the limit that tripped resets. An absolute timestamp, not a duration. For &#x60;rate_limit_exceeded&#x60; this is the next per-second window boundary; for &#x60;quota_exceeded&#x60; it is the end of the monthly quota period and may be weeks away. <br>  * Retry-After - Seconds to wait before retrying. Sent on both 429 codes; only its magnitude differs — around a second for the throttle, up to the remainder of the billing period for the quota wall. Floored at 1, so it never instructs a client to retry immediately. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

