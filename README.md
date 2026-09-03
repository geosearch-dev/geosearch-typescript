# @geosearch/client@1.3.0

A TypeScript SDK client for the geosearch.dev API.

## Usage

First, install the SDK from npm.

```bash
npm install @geosearch/client --save
```

Next, try it out.


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


## Documentation

### API Endpoints

All URIs are relative to *https://geosearch.dev*

| Class | Method | HTTP request | Description
| ----- | ------ | ------------ | -------------
*BatchApi* | [**batchCities**](docs/BatchApi.md#batchcities) | **POST** /v1/batch/cities | Batch lookup cities by IDs
*BatchApi* | [**batchCountries**](docs/BatchApi.md#batchcountries) | **POST** /v1/batch/countries | Batch lookup countries by IDs
*BatchApi* | [**batchRegions**](docs/BatchApi.md#batchregions) | **POST** /v1/batch/regions | Batch lookup regions by IDs
*BoundariesApi* | [**getBoundary**](docs/BoundariesApi.md#getboundary) | **GET** /v1/boundaries/{geoname_id} | Fetch an area\&#39;s boundary polygon as GeoJSON
*CitiesApi* | [**cityHierarchy**](docs/CitiesApi.md#cityhierarchy) | **GET** /v1/cities/{id}/hierarchy | Get administrative hierarchy for a city
*CitiesApi* | [**getCity**](docs/CitiesApi.md#getcity) | **GET** /v1/cities/{id} | Get city by ID
*CitiesApi* | [**listCities**](docs/CitiesApi.md#listcities) | **GET** /v1/cities | List cities
*CitiesApi* | [**nearbyCities**](docs/CitiesApi.md#nearbycities) | **GET** /v1/cities/nearby | Find nearby cities
*CountriesApi* | [**countryNeighbors**](docs/CountriesApi.md#countryneighbors) | **GET** /v1/countries/{code}/neighbors | List neighboring countries
*CountriesApi* | [**getCountry**](docs/CountriesApi.md#getcountry) | **GET** /v1/countries/{code} | Get country by ISO code
*CountriesApi* | [**listCountries**](docs/CountriesApi.md#listcountries) | **GET** /v1/countries | List countries
*CountriesApi* | [**listCountryRegions**](docs/CountriesApi.md#listcountryregions) | **GET** /v1/countries/{code}/regions | List regions in a country
*HealthApi* | [**getStatus**](docs/HealthApi.md#getstatus) | **GET** /v1/status | Health check
*IPGeolocationApi* | [**lookupIP**](docs/IPGeolocationApi.md#lookupip) | **GET** /v1/ip/{address} | IP geolocation lookup
*IPGeolocationApi* | [**lookupMyIP**](docs/IPGeolocationApi.md#lookupmyip) | **GET** /v1/ip/me | Caller\&#39;s IP geolocation
*PostalCodesApi* | [**listPostalCodes**](docs/PostalCodesApi.md#listpostalcodes) | **GET** /v1/postal-codes | List postal codes
*PostalCodesApi* | [**nearestPostalCode**](docs/PostalCodesApi.md#nearestpostalcode) | **GET** /v1/postal-codes/nearest | Find nearest postal codes
*RegionsApi* | [**getRegion**](docs/RegionsApi.md#getregion) | **GET** /v1/regions/{id} | Get region by ID
*RegionsApi* | [**listRegionCities**](docs/RegionsApi.md#listregioncities) | **GET** /v1/regions/{id}/cities | List cities in a region
*RegionsApi* | [**listRegions**](docs/RegionsApi.md#listregions) | **GET** /v1/regions | List regions
*RegionsApi* | [**regionChildren**](docs/RegionsApi.md#regionchildren) | **GET** /v1/regions/{id}/children | List child cities of a region
*SearchApi* | [**autocomplete**](docs/SearchApi.md#autocomplete) | **GET** /v1/autocomplete | Autocomplete search
*SearchApi* | [**resolveCoordinate**](docs/SearchApi.md#resolvecoordinate) | **GET** /v1/resolve | Resolve coordinates to their containing administrative areas
*SearchApi* | [**reverseGeocode**](docs/SearchApi.md#reversegeocode) | **GET** /v1/reverse | Reverse geocode coordinates
*SearchApi* | [**search**](docs/SearchApi.md#search) | **GET** /v1/search | Cross-type search
*TimezonesApi* | [**getTimezone**](docs/TimezonesApi.md#gettimezone) | **GET** /v1/timezones/{tzId} | Get timezone by IANA ID
*TimezonesApi* | [**listTimezones**](docs/TimezonesApi.md#listtimezones) | **GET** /v1/timezones | List timezones


### Models

- [AutocompleteListResponse](docs/AutocompleteListResponse.md)
- [AutocompleteResult](docs/AutocompleteResult.md)
- [BatchRequest](docs/BatchRequest.md)
- [Boundary](docs/Boundary.md)
- [BoundarySingleResponse](docs/BoundarySingleResponse.md)
- [City](docs/City.md)
- [CityListResponse](docs/CityListResponse.md)
- [CitySingleResponse](docs/CitySingleResponse.md)
- [Country](docs/Country.md)
- [CountryListResponse](docs/CountryListResponse.md)
- [CountryRef](docs/CountryRef.md)
- [CountrySingleResponse](docs/CountrySingleResponse.md)
- [ErrorResponse](docs/ErrorResponse.md)
- [ErrorResponseError](docs/ErrorResponseError.md)
- [ErrorResponseErrorDetailsInner](docs/ErrorResponseErrorDetailsInner.md)
- [GeoJSONGeometry](docs/GeoJSONGeometry.md)
- [GeoJSONMultiPolygon](docs/GeoJSONMultiPolygon.md)
- [GetStatus200Response](docs/GetStatus200Response.md)
- [GetStatus200ResponseData](docs/GetStatus200ResponseData.md)
- [HierarchyListResponse](docs/HierarchyListResponse.md)
- [HierarchyNode](docs/HierarchyNode.md)
- [IPResult](docs/IPResult.md)
- [IPResultCity](docs/IPResultCity.md)
- [IPResultContinent](docs/IPResultContinent.md)
- [IPResultCountry](docs/IPResultCountry.md)
- [IPResultLocation](docs/IPResultLocation.md)
- [IPResultPostal](docs/IPResultPostal.md)
- [IPResultRegion](docs/IPResultRegion.md)
- [IPSingleResponse](docs/IPSingleResponse.md)
- [NearbyCity](docs/NearbyCity.md)
- [NearbyCityListResponse](docs/NearbyCityListResponse.md)
- [PaginationMeta](docs/PaginationMeta.md)
- [PostalCode](docs/PostalCode.md)
- [PostalCodeListResponse](docs/PostalCodeListResponse.md)
- [QuotaDetail](docs/QuotaDetail.md)
- [Region](docs/Region.md)
- [RegionListResponse](docs/RegionListResponse.md)
- [RegionRef](docs/RegionRef.md)
- [RegionSingleResponse](docs/RegionSingleResponse.md)
- [ReverseGeocodeResult](docs/ReverseGeocodeResult.md)
- [ReverseGeocodeSingleResponse](docs/ReverseGeocodeSingleResponse.md)
- [SearchListResponse](docs/SearchListResponse.md)
- [SearchResult](docs/SearchResult.md)
- [Timezone](docs/Timezone.md)
- [TimezoneListResponse](docs/TimezoneListResponse.md)
- [TimezoneSingleResponse](docs/TimezoneSingleResponse.md)
- [UpgradeDetail](docs/UpgradeDetail.md)

### Authorization


Authentication schemes defined for the API:
<a id="apiKeyAuth"></a>
#### apiKeyAuth


- **Type**: API key
- **API key parameter name**: `X-API-Key`
- **Location**: HTTP header

## About

This TypeScript SDK client supports the [Fetch API](https://fetch.spec.whatwg.org/)
and is automatically generated by the
[OpenAPI Generator](https://openapi-generator.tech) project:

- API version: `1.3.0`
- Package version: `1.3.0`
- Generator version: `7.21.0`
- Build package: `org.openapitools.codegen.languages.TypeScriptFetchClientCodegen`

The generated npm module supports the following:

- Environments
  * Node.js
  * Webpack
  * Browserify
- Language levels
  * ES5 - you must have a Promises/A+ library installed
  * ES6
- Module systems
  * CommonJS
  * ES6 module system


## Development

### Building

To build the TypeScript source code, you need to have Node.js and npm installed.
After cloning the repository, navigate to the project directory and run:

```bash
npm install
npm run build
```

### Publishing

Once you've built the package, you can publish it to npm:

```bash
npm publish
```

## License

[MIT]()
