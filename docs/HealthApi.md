# HealthApi

All URIs are relative to *https://geosearch.dev*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getStatus**](HealthApi.md#getstatus) | **GET** /v1/status | Health check |



## getStatus

> GetStatus200Response getStatus()

Health check

Returns the API health status and database connectivity. No authentication required.

### Example

```ts
import {
  Configuration,
  HealthApi,
} from '@geoapi/client';
import type { GetStatusRequest } from '@geoapi/client';

async function example() {
  console.log("🚀 Testing @geoapi/client SDK...");
  const api = new HealthApi();

  try {
    const data = await api.getStatus();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**GetStatus200Response**](GetStatus200Response.md)

### Authorization

No authorization required

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | API status |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

