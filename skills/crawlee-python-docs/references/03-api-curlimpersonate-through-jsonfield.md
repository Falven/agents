# CurlImpersonateHttpClient<!-- -->

HTTP client based on the `curl-cffi` library.

This client uses the `curl-cffi` library to perform HTTP requests in crawlers (`BasicCrawler` subclasses) and to manage sessions, proxies, and error handling.

See the `HttpClient` class for more common information about HTTP clients.

### Usage

```
from crawlee.crawlers import HttpCrawler  # or any other HTTP client-based crawler
from crawlee.http_clients import CurlImpersonateHttpClient

http_client = CurlImpersonateHttpClient()
crawler = HttpCrawler(http_client=http_client)
```

### Hierarchy

* [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)
  * *CurlImpersonateHttpClient*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#__init__)
* [**cleanup](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#cleanup)
* [**crawl](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#crawl)
* [**send\_request](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#send_request)
* [**stream](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#stream)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md#active)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L201)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

- Inherited from [HttpClient.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aenter__)

  Initialize the client when entering the context manager.

  ***

  #### Returns [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L213)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, traceback): None

- Inherited from [HttpClient.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aexit__)

  Deinitialize the client and clean up resources when exiting the context manager.

  ***

  #### Parameters

  * ##### exc\_type: BaseException | None
  * ##### exc\_value: BaseException | None
  * ##### traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L128)\_\_init\_\_

* ****\_\_init\_\_**(\*, persist\_cookies\_per\_session, async\_session\_kwargs): None

- Overrides [HttpClient.\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypersist\_cookies\_per\_session: bool = <!-- -->True

    Whether to persist cookies per HTTP session.

  * ##### async\_session\_kwargs: Any

    Additional keyword arguments for `curl_cffi.requests.AsyncSession`.

  #### Returns None

### [**](#cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L360)cleanup

* **async **cleanup**(): None

- Overrides [HttpClient.cleanup](https://crawlee.dev/python/python/api/class/HttpClient.md#cleanup)

  Clean up resources used by the client.

  This method is called when the client is no longer needed and should be overridden in subclasses to perform any necessary cleanup such as closing connections, releasing file handles, or other resource deallocation.

  ***

  #### Returns None

### [**](#crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L148)crawl

* **async **crawl**(request, \*, session, proxy\_info, statistics, timeout): [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

- Overrides [HttpClient.crawl](https://crawlee.dev/python/python/api/class/HttpClient.md#crawl)

  Perform the crawling for a given request.

  This method is called from `crawler.run()`.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to be crawled.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlystatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md) | None = <!-- -->None

    The statistics object to register status codes.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

  The result of the crawling.

### [**](#send_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L189)send\_request

* **async **send\_request**(url, \*, method, headers, payload, session, proxy\_info, timeout): [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

- Overrides [HttpClient.send\_request](https://crawlee.dev/python/python/api/class/HttpClient.md#send_request)

  Send an HTTP request via the client.

  This method is called from `context.send_request()` helper.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  The HTTP response received from the server.

### [**](#stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L230)stream

* ****stream**(url, \*, method, headers, payload, session, proxy\_info, timeout): AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

- Overrides [HttpClient.stream](https://crawlee.dev/python/python/api/class/HttpClient.md#stream)

  Stream an HTTP request via the client.

  This method should be used for downloading potentially large data where you need to process the response body in chunks rather than loading it entirely into memory.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    The maximum time to wait for establishing the connection.

  #### Returns AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

  An async context manager yielding the HTTP response with streaming capabilities.

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L95)active

**active: bool

Inherited from [HttpClient.active](https://crawlee.dev/python/python/api/class/HttpClient.md#active)

Indicate whether the context is active.


---

# Dataset<!-- -->

Dataset is a storage for managing structured tabular data.

The dataset class provides a high-level interface for storing and retrieving structured data with consistent schema, similar to database tables or spreadsheets. It abstracts the underlying storage implementation details, offering a consistent API regardless of where the data is physically stored.

Dataset operates in an append-only mode, allowing new records to be added but not modified or deleted after creation. This makes it particularly suitable for storing crawling results and other data that should be immutable once collected.

The class provides methods for adding data, retrieving data with various filtering options, and exporting data to different formats. You can create a dataset using the `open` class method, specifying either a name or ID. The underlying storage implementation is determined by the configured storage client.

### Usage

```
from crawlee.storages import Dataset

# Open a dataset
dataset = await Dataset.open(name='my-dataset')

# Add data
await dataset.push_data({'title': 'Example Product', 'price': 99.99})

# Retrieve filtered data
results = await dataset.get_data(limit=10, desc=True)

# Export data
await dataset.export_to('results.json', content_type='json')
```

### Hierarchy

* [Storage](https://crawlee.dev/python/python/api/class/Storage.md)
  * *Dataset*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/Dataset.md#__init__)
* [**drop](https://crawlee.dev/python/python/api/class/Dataset.md#drop)
* [**export\_to](https://crawlee.dev/python/python/api/class/Dataset.md#export_to)
* [**get\_data](https://crawlee.dev/python/python/api/class/Dataset.md#get_data)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/Dataset.md#get_metadata)
* [**iterate\_items](https://crawlee.dev/python/python/api/class/Dataset.md#iterate_items)
* [**list\_items](https://crawlee.dev/python/python/api/class/Dataset.md#list_items)
* [**open](https://crawlee.dev/python/python/api/class/Dataset.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/Dataset.md#purge)
* [**push\_data](https://crawlee.dev/python/python/api/class/Dataset.md#push_data)

### Properties

* [**id](https://crawlee.dev/python/python/api/class/Dataset.md#id)
* [**name](https://crawlee.dev/python/python/api/class/Dataset.md#name)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L69)\_\_init\_\_

* ****\_\_init\_\_**(client, id, name): None

- Initialize a new instance.

  Preferably use the `Dataset.open` constructor to create a new instance.

  ***

  #### Parameters

  * ##### client: [DatasetClient](https://crawlee.dev/python/python/api/class/DatasetClient.md)

    An instance of a storage client.

  * ##### id: str

    The unique identifier of the storage.

  * ##### name: str | None

    The name of the storage, if available.

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L128)drop

* **async **drop**(): None

- Overrides [Storage.drop](https://crawlee.dev/python/python/api/class/Storage.md#drop)

  Drop the storage, removing it from the underlying storage client and clearing the cache.

  ***

  #### Returns None

### [**](#export_to)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L323)export\_to

* **async **export\_to**(key: str, content\_type?
  <!-- -->
  : Literal\[json, csv], to\_kvs\_id?
  <!-- -->
  : str | None, to\_kvs\_name?
  <!-- -->
  : str | None, to\_kvs\_storage\_client?
  <!-- -->
  : [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None, to\_kvs\_configuration?
  <!-- -->
  : [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None, kwargs: Any): None
* **async **export\_to**(key: str, content\_type: Literal\[json], to\_kvs\_id?
  <!-- -->
  : str | None, to\_kvs\_name?
  <!-- -->
  : str | None, to\_kvs\_storage\_client?
  <!-- -->
  : [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None, to\_kvs\_configuration?
  <!-- -->
  : [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None, \*: , skipkeys: NotRequired\[bool], ensure\_ascii: NotRequired\[bool], check\_circular: NotRequired\[bool], allow\_nan: NotRequired\[bool], cls: NotRequired\[[type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[json.JSONEncoder]], indent: NotRequired\[int], separators: NotRequired\[tuple\[str, str]], default: NotRequired\[Callable], sort\_keys: NotRequired\[bool]): None
* **async **export\_to**(key: str, content\_type: Literal\[csv], to\_kvs\_id?
  <!-- -->
  : str | None, to\_kvs\_name?
  <!-- -->
  : str | None, to\_kvs\_storage\_client?
  <!-- -->
  : [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None, to\_kvs\_configuration?
  <!-- -->
  : [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None, \*: , dialect: NotRequired\[str], delimiter: NotRequired\[str], doublequote: NotRequired\[bool], escapechar: NotRequired\[str], lineterminator: NotRequired\[str], quotechar: NotRequired\[str], quoting: NotRequired\[int], skipinitialspace: NotRequired\[bool], strict: NotRequired\[bool]): None

- Export the entire dataset into a specified file stored under a key in a key-value store.

  This method consolidates all entries from a specified dataset into one file, which is then saved under a given key in a key-value store. The format of the exported file is determined by the `content_type` parameter. Either the dataset's ID or name should be specified, and similarly, either the target key-value store's ID or name should be used.

  ***

  #### Parameters

  * ##### key: str

    The key under which to save the data in the key-value store.

  * ##### optionalcontent\_type: Literal\[json, csv] = <!-- -->'json'

    The format in which to export the data.

  * ##### optionalto\_kvs\_id: str | None = <!-- -->None

    ID of the key-value store to save the exported file. Specify only one of ID or name.

  * ##### optionalto\_kvs\_name: str | None = <!-- -->None

    Name of the key-value store to save the exported file. Specify only one of ID or name.

  * ##### optionalto\_kvs\_storage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None = <!-- -->None

    Storage client to use for the key-value store.

  * ##### optionalto\_kvs\_configuration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

    Configuration for the key-value store.

  * ##### kwargs: Any

    Additional parameters for the export operation, specific to the chosen content type.

  #### Returns None

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L150)get\_data

* **async **get\_data**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden, flatten, view): [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

- Retrieve a paginated list of items from a dataset based on various filtering parameters.

  This method provides the flexibility to filter, sort, and modify the appearance of dataset items when listed. Each parameter modifies the result set according to its purpose. The method also supports pagination through 'offset' and 'limit' parameters.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyoffset: int = <!-- -->0

    Skips the specified number of items at the start.

  * ##### optionalkeyword-onlylimit: int | None = <!-- -->999\_999\_999\_999

    The maximum number of items to retrieve. Unlimited if None.

  * ##### optionalkeyword-onlyclean: bool = <!-- -->False

    Return only non-empty items and excludes hidden fields. Shortcut for skip\_hidden and skip\_empty.

  * ##### optionalkeyword-onlydesc: bool = <!-- -->False

    Set to True to sort results in descending order.

  * ##### optionalkeyword-onlyfields: list\[str] | None = <!-- -->None

    Fields to include in each item. Sorts fields as specified if provided.

  * ##### optionalkeyword-onlyomit: list\[str] | None = <!-- -->None

    Fields to exclude from each item.

  * ##### optionalkeyword-onlyunwind: list\[str] | None = <!-- -->None

    Unwinds items by a specified array field, turning each element into a separate item.

  * ##### optionalkeyword-onlyskip\_empty: bool = <!-- -->False

    Excludes empty items from the results if True.

  * ##### optionalkeyword-onlyskip\_hidden: bool = <!-- -->False

    Excludes fields starting with '#' if True.

  * ##### optionalkeyword-onlyflatten: list\[str] | None = <!-- -->None

    Fields to be flattened in returned items.

  * ##### optionalkeyword-onlyview: str | None = <!-- -->None

    Specifies the dataset view to be used.

  #### Returns [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

  An object with filtered, sorted, and paginated dataset items plus pagination details.

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L96)get\_metadata

* **async **get\_metadata**(): ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [Storage.get\_metadata](https://crawlee.dev/python/python/api/class/Storage.md#get_metadata)

  Get the storage metadata.

  ***

  #### Returns ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#iterate_items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L201)iterate\_items

* **async **iterate\_items**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden): AsyncIterator\[dict\[str, Any]]

- Iterate over items in the dataset according to specified filters and sorting.

  This method allows for asynchronously iterating through dataset items while applying various filters such as skipping empty items, hiding specific fields, and sorting. It supports pagination via `offset` and `limit` parameters, and can modify the appearance of dataset items using `fields`, `omit`, `unwind`, `skip_empty`, and `skip_hidden` parameters.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyoffset: int = <!-- -->0

    Skips the specified number of items at the start.

  * ##### optionalkeyword-onlylimit: int | None = <!-- -->999\_999\_999\_999

    The maximum number of items to retrieve. Unlimited if None.

  * ##### optionalkeyword-onlyclean: bool = <!-- -->False

    Return only non-empty items and excludes hidden fields. Shortcut for skip\_hidden and skip\_empty.

  * ##### optionalkeyword-onlydesc: bool = <!-- -->False

    Set to True to sort results in descending order.

  * ##### optionalkeyword-onlyfields: list\[str] | None = <!-- -->None

    Fields to include in each item. Sorts fields as specified if provided.

  * ##### optionalkeyword-onlyomit: list\[str] | None = <!-- -->None

    Fields to exclude from each item.

  * ##### optionalkeyword-onlyunwind: list\[str] | None = <!-- -->None

    Unwinds items by a specified array field, turning each element into a separate item.

  * ##### optionalkeyword-onlyskip\_empty: bool = <!-- -->False

    Excludes empty items from the results if True.

  * ##### optionalkeyword-onlyskip\_hidden: bool = <!-- -->False

    Excludes fields starting with '#' if True.

  #### Returns AsyncIterator\[dict\[str, Any]]

### [**](#list_items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L249)list\_items

* **async **list\_items**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden): list\[dict\[str, Any]]

- Retrieve a list of all items from the dataset according to specified filters and sorting.

  This method collects all dataset items into a list while applying various filters such as skipping empty items, hiding specific fields, and sorting. It supports pagination via `offset` and `limit` parameters, and can modify the appearance of dataset items using `fields`, `omit`, `unwind`, `skip_empty`, and `skip_hidden` parameters.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyoffset: int = <!-- -->0

    Skips the specified number of items at the start.

  * ##### optionalkeyword-onlylimit: int | None = <!-- -->999\_999\_999\_999

    The maximum number of items to retrieve. Unlimited if None.

  * ##### optionalkeyword-onlyclean: bool = <!-- -->False

    Return only non-empty items and excludes hidden fields. Shortcut for skip\_hidden and skip\_empty.

  * ##### optionalkeyword-onlydesc: bool = <!-- -->False

    Set to True to sort results in descending order.

  * ##### optionalkeyword-onlyfields: list\[str] | None = <!-- -->None

    Fields to include in each item. Sorts fields as specified if provided.

  * ##### optionalkeyword-onlyomit: list\[str] | None = <!-- -->None

    Fields to exclude from each item.

  * ##### optionalkeyword-onlyunwind: list\[str] | None = <!-- -->None

    Unwinds items by a specified array field, turning each element into a separate item.

  * ##### optionalkeyword-onlyskip\_empty: bool = <!-- -->False

    Excludes empty items from the results if True.

  * ##### optionalkeyword-onlyskip\_hidden: bool = <!-- -->False

    Excludes fields starting with '#' if True.

  #### Returns list\[dict\[str, Any]]

  A list of dictionary objects, each representing a dataset item after applying the specified filters and transformations.

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L101)open

* **async **open**(\*, id, name, alias, configuration, storage\_client): [Storage](https://crawlee.dev/python/python/api/class/Storage.md)

- Overrides [Storage.open](https://crawlee.dev/python/python/api/class/Storage.md#open)

  Open a storage, either restore existing or create a new one.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None

    The storage ID.

  * ##### optionalkeyword-onlyname: str | None = <!-- -->None

    The storage name (global scope, persists across runs). Name can only contain letters "a" through "z", the digits "0" through "9", and the hyphen ("-") but only in the middle of the string (e.g. "my-value-1").

  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

    The storage alias (run scope, creates unnamed storage).

  * ##### optionalkeyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

    Configuration object used during the storage creation or restoration process.

  * ##### optionalkeyword-onlystorage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None = <!-- -->None

    Underlying storage client to use. If not provided, the default global storage client from the service locator will be used.

  #### Returns [Storage](https://crawlee.dev/python/python/api/class/Storage.md)

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L134)purge

* **async **purge**(): None

- Overrides [Storage.purge](https://crawlee.dev/python/python/api/class/Storage.md#purge)

  Purge the storage, removing all items from the underlying storage client.

  This method does not remove the storage itself, e.g. don't remove the metadata, but clears all items within it.

  ***

  #### Returns None

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L137)push\_data

* **async **push\_data**(data): None

- Store an object or an array of objects to the dataset.

  The size of the data is limited by the receiving API and therefore `push_data()` will only allow objects whose JSON representation is smaller than 9MB. When an array is passed, none of the included objects may be larger than 9MB, but the array itself may be of any size.

  ***

  #### Parameters

  * ##### data: list\[dict\[str, Any]] | dict\[str, Any]

    A JSON serializable data structure to be stored in the dataset. The JSON representation of each item must be smaller than 9MB.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L87)id

**id: str

Overrides [Storage.id](https://crawlee.dev/python/python/api/class/Storage.md#id)

Get the storage ID.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_dataset.py#L92)name

**name: str | None

Overrides [Storage.name](https://crawlee.dev/python/python/api/class/Storage.md#name)

Get the storage name.


---

# DatasetClient<!-- -->

An abstract class for dataset storage clients.

Dataset clients provide an interface for accessing and manipulating dataset storage. They handle operations like adding and getting dataset items across different storage backends.

Storage clients are specific to the type of storage they manage (`Dataset`, `KeyValueStore`, `RequestQueue`), and can operate with various storage systems including memory, file system, databases, and cloud storage solutions.

This abstract class defines the interface that all specific dataset clients must implement.

### Hierarchy

* *DatasetClient*

  * [MemoryDatasetClient](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md)
  * [FileSystemDatasetClient](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md)
  * [SqlDatasetClient](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md)
  * [RedisDatasetClient](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md)

## Index[**](#Index)

### Methods

* [**drop](https://crawlee.dev/python/python/api/class/DatasetClient.md#drop)
* [**get\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_data)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_metadata)
* [**iterate\_items](https://crawlee.dev/python/python/api/class/DatasetClient.md#iterate_items)
* [**purge](https://crawlee.dev/python/python/api/class/DatasetClient.md#purge)
* [**push\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#push_data)

## Methods<!-- -->[**](#Methods)

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_dataset_client.py#L31)drop

* **async **drop**(): None

- Overrides [DatasetClient.drop](https://crawlee.dev/python/python/api/class/DatasetClient.md#drop)

  Drop the whole dataset and remove all its items.

  The backend method for the `Dataset.drop` call.

  ***

  #### Returns None

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_dataset_client.py#L52)get\_data

* **async **get\_data**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden, flatten, view): [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

- Overrides [DatasetClient.get\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_data)

  Get data from the dataset with various filtering options.

  The backend method for the `Dataset.get_data` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyoffset: int = <!-- -->0
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->999\_999\_999\_999
  * ##### optionalkeyword-onlyclean: bool = <!-- -->False
  * ##### optionalkeyword-onlydesc: bool = <!-- -->False
  * ##### optionalkeyword-onlyfields: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyomit: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyunwind: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyskip\_empty: bool = <!-- -->False
  * ##### optionalkeyword-onlyskip\_hidden: bool = <!-- -->False
  * ##### optionalkeyword-onlyflatten: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyview: str | None = <!-- -->None

  #### Returns [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_dataset_client.py#L27)get\_metadata

* **async **get\_metadata**(): [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

- Overrides [DatasetClient.get\_metadata](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_metadata)

  Get the metadata of the dataset.

  ***

  #### Returns [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

### [**](#iterate_items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_dataset_client.py#L73)iterate\_items

* **async **iterate\_items**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden): AsyncIterator\[dict\[str, Any]]

- Overrides [DatasetClient.iterate\_items](https://crawlee.dev/python/python/api/class/DatasetClient.md#iterate_items)

  Iterate over the dataset items with filtering options.

  The backend method for the `Dataset.iterate_items` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyoffset: int = <!-- -->0
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->None
  * ##### optionalkeyword-onlyclean: bool = <!-- -->False
  * ##### optionalkeyword-onlydesc: bool = <!-- -->False
  * ##### optionalkeyword-onlyfields: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyomit: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyunwind: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyskip\_empty: bool = <!-- -->False
  * ##### optionalkeyword-onlyskip\_hidden: bool = <!-- -->False

  #### Returns AsyncIterator\[dict\[str, Any]]

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_dataset_client.py#L38)purge

* **async **purge**(): None

- Overrides [DatasetClient.purge](https://crawlee.dev/python/python/api/class/DatasetClient.md#purge)

  Purge all items from the dataset.

  The backend method for the `Dataset.purge` call.

  ***

  #### Returns None

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_dataset_client.py#L45)push\_data

* **async **push\_data**(data): None

- Overrides [DatasetClient.push\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#push_data)

  Push data to the dataset.

  The backend method for the `Dataset.push_data` call.

  ***

  #### Parameters

  * ##### data: list\[Any] | dict\[str, Any]

  #### Returns None


---

# DatasetItemDb<!-- -->

Items table for datasets.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *DatasetItemDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/DatasetItemDb.md#__tablename__)
* [**data](https://crawlee.dev/python/python/api/class/DatasetItemDb.md#data)
* [**dataset](https://crawlee.dev/python/python/api/class/DatasetItemDb.md#dataset)
* [**dataset\_id](https://crawlee.dev/python/python/api/class/DatasetItemDb.md#dataset_id)
* [**item\_id](https://crawlee.dev/python/python/api/class/DatasetItemDb.md#item_id)
* [**storage\_id](https://crawlee.dev/python/python/api/class/DatasetItemDb.md#storage_id)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L180)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L192)data

**data: Mapped\[list\[dict\[str, Any]] | dict\[str, Any]]

JSON serializable item data.

### [**](#dataset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L196)dataset

**dataset: Mapped\[[DatasetMetadataDb](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md)]

### [**](#dataset_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L185)dataset\_id

**dataset\_id: Mapped\[str]

Foreign key to metadata dataset record.

### [**](#item_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L182)item\_id

**item\_id: Mapped\[int]

Auto-increment primary key preserving insertion order.

### [**](#storage_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L198)storage\_id

**storage\_id: Undefined

Alias for dataset\_id to match SqlClientMixin expectations.


---

# DatasetItemsListPage<!-- -->

Model for a single page of dataset items returned from a collection list method.

## Index[**](#Index)

### Properties

* [**count](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md#count)
* [**desc](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md#desc)
* [**limit](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md#limit)
* [**model\_config](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md#model_config)
* [**offset](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md#offset)
* [**total](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md#total)

## Properties<!-- -->[**](#Properties)

### [**](#count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L115)count

**count: int

The number of objects returned on this page.

### [**](#desc)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L127)desc

**desc: bool

Indicates if the returned list is in descending order.

### [**](#limit)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L121)limit

**limit: int

The maximum number of objects to return, as specified in the API call.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L113)model\_config

**model\_config: Undefined

### [**](#offset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L118)offset

**offset: int

The starting position of the first object returned, as specified in the API call.

### [**](#total)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L124)total

**total: int

The total number of objects that match the criteria of the API call.


---

# DatasetMetadata<!-- -->

Model for a dataset metadata.

### Hierarchy

* [StorageMetadata](https://crawlee.dev/python/python/api/class/StorageMetadata.md)
  * *DatasetMetadata*

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/DatasetMetadata.md#accessed_at)
* [**created\_at](https://crawlee.dev/python/python/api/class/DatasetMetadata.md#created_at)
* [**id](https://crawlee.dev/python/python/api/class/DatasetMetadata.md#id)
* [**item\_count](https://crawlee.dev/python/python/api/class/DatasetMetadata.md#item_count)
* [**model\_config](https://crawlee.dev/python/python/api/class/DatasetMetadata.md#model_config)
* [**modified\_at](https://crawlee.dev/python/python/api/class/DatasetMetadata.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/DatasetMetadata.md#name)

## Properties<!-- -->[**](#Properties)

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L31)accessed\_at

**accessed\_at: Annotated\[datetime, Field(alias='accessedAt')]

Inherited from [StorageMetadata.accessed\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#accessed_at)

The timestamp when the storage was last accessed.

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L34)created\_at

**created\_at: Annotated\[datetime, Field(alias='createdAt')]

Inherited from [StorageMetadata.created\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#created_at)

The timestamp when the storage was created.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L25)id

**id: Annotated\[str, Field(alias='id')]

Inherited from [StorageMetadata.id](https://crawlee.dev/python/python/api/class/StorageMetadata.md#id)

The unique identifier of the storage.

### [**](#item_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L47)item\_count

**item\_count: int

The number of items in the dataset.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L45)model\_config

**model\_config: Undefined

Overrides [StorageMetadata.model\_config](https://crawlee.dev/python/python/api/class/StorageMetadata.md#model_config)

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L37)modified\_at

**modified\_at: Annotated\[datetime, Field(alias='modifiedAt')]

Inherited from [StorageMetadata.modified\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#modified_at)

The timestamp when the storage was last modified.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L28)name

**name: Annotated\[str | None, Field(alias='name', default=None)]

Inherited from [StorageMetadata.name](https://crawlee.dev/python/python/api/class/StorageMetadata.md#name)

The name of the storage.


---

# DatasetMetadataBufferDb<!-- -->

Buffer table for deferred dataset metadata updates to reduce concurrent access issues.

### Hierarchy

* [MetadataBufferDb](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md)
* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *DatasetMetadataBufferDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md#__tablename__)
* [**accessed\_at](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md#accessed_at)
* [**dataset\_id](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md#dataset_id)
* [**delta\_item\_count](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md#delta_item_count)
* [**id](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md#id)
* [**modified\_at](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md#modified_at)
* [**storage\_id](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md#storage_id)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L309)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L286)accessed\_at

**accessed\_at: Mapped\[datetime]

Inherited from [MetadataBufferDb.accessed\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#accessed_at)

New accessed\_at timestamp, if being updated.

### [**](#dataset_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L312)dataset\_id

**dataset\_id: Mapped\[str]

ID of the dataset being updated.

### [**](#delta_item_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L316)delta\_item\_count

**delta\_item\_count: Mapped\[int | None]

Delta for dataset item\_count.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L282)id

**id: Mapped\[int]

Inherited from [MetadataBufferDb.id](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#id)

Auto-increment primary key for ordering.

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L289)modified\_at

**modified\_at: Mapped\[datetime | None]

Inherited from [MetadataBufferDb.modified\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#modified_at)

New modified\_at timestamp, if being updated.

### [**](#storage_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L319)storage\_id

**storage\_id: Undefined

Alias for dataset\_id to match SqlClientMixin expectations.


---

# DatasetMetadataDb<!-- -->

Metadata table for datasets.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
* [StorageMetadataDb](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md)
  * *DatasetMetadataDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#__tablename__)
* [**accessed\_at](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#accessed_at)
* [**buffer\_locked\_until](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#buffer_locked_until)
* [**created\_at](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#created_at)
* [**dataset\_id](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#dataset_id)
* [**id](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#id)
* [**internal\_name](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#internal_name)
* [**item\_count](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#item_count)
* [**items](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#items)
* [**modified\_at](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md#name)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L77)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L61)accessed\_at

**accessed\_at: Mapped\[datetime]

Inherited from [StorageMetadataDb.accessed\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#accessed_at)

Last access datetime for usage tracking.

### [**](#buffer_locked_until)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L70)buffer\_locked\_until

**buffer\_locked\_until: Mapped\[datetime | None]

Inherited from [StorageMetadataDb.buffer\_locked\_until](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#buffer_locked_until)

Timestamp until which buffer processing is locked for this storage. NULL = unlocked.

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L64)created\_at

**created\_at: Mapped\[datetime]

Inherited from [StorageMetadataDb.created\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#created_at)

Creation datetime.

### [**](#dataset_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L79)dataset\_id

**dataset\_id: Mapped\[str]

Unique identifier for the dataset.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L90)id

**id: Undefined

Alias for dataset\_id to match Pydantic expectations.

### [**](#internal_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L55)internal\_name

**internal\_name: Mapped\[str]

Inherited from [StorageMetadataDb.internal\_name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#internal_name)

Internal unique name for a storage instance based on a name or alias.

### [**](#item_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L82)item\_count

**item\_count: Mapped\[int]

Number of items in the dataset.

### [**](#items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L86)items

**items: Mapped\[list\[[DatasetItemDb](https://crawlee.dev/python/python/api/class/DatasetItemDb.md)]]

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L67)modified\_at

**modified\_at: Mapped\[datetime]

Inherited from [StorageMetadataDb.modified\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#modified_at)

Last modification datetime.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L58)name

**name: Mapped\[str | None]

Inherited from [StorageMetadataDb.name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#name)

Human-readable name. None becomes 'default' in database to enforce uniqueness.


---

# DefaultRenderingTypePredictor<!-- -->

Stores rendering type for previously crawled URLs and predicts the rendering type for unvisited urls.

`RenderingTypePredictor` implementation based on logistic regression: <https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html>

### Hierarchy

* [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md)
  * *DefaultRenderingTypePredictor*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md#__init__)
* [**clear](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md#clear)
* [**initialize](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md#initialize)
* [**predict](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md#predict)
* [**store\_result](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md#store_result)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L99)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md)

- Inherited from [RenderingTypePredictor.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#__aenter__)

  Initialize the predictor upon entering the context manager.

  ***

  #### Returns [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L104)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Inherited from [RenderingTypePredictor.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#__aexit__)

  Clear the predictor upon exiting the context manager.

  ***

  #### Parameters

  * ##### exc\_type: type\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L122)\_\_init\_\_

* ****\_\_init\_\_**(detection\_ratio, \*, persistence\_enabled, persist\_state\_key): None

- Overrides [RenderingTypePredictor.\_\_init\_\_](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionaldetection\_ratio: float = <!-- -->0.1

    A number between 0 and 1 that determines the desired ratio of rendering type detections.

  * ##### optionalkeyword-onlypersistence\_enabled: bool = <!-- -->False

    Whether to enable persistence of the trained model parameters for reuse.

  * ##### optionalkeyword-onlypersist\_state\_key: str = <!-- -->'rendering-type-predictor-state'

    Key in the key-value storage where the trained model parameters will be saved. If None, defaults to 'rendering-type-predictor-state'.

  #### Returns None

### [**](#clear)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L169)clear

* **async **clear**(): None

- Overrides [RenderingTypePredictor.clear](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#clear)

  Clear the predictor state.

  ***

  #### Returns None

### [**](#initialize)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L161)initialize

* **async **initialize**(): None

- Overrides [RenderingTypePredictor.initialize](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#initialize)

  Get current state of the predictor.

  ***

  #### Returns None

### [**](#predict)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L177)predict

* ****predict**(request): [RenderingTypePrediction](https://crawlee.dev/python/python/api/class/RenderingTypePrediction.md)

- Overrides [RenderingTypePredictor.predict](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#predict)

  Get `RenderingTypePrediction` based on the input request.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    `Request` instance for which the prediction is made.

  #### Returns [RenderingTypePrediction](https://crawlee.dev/python/python/api/class/RenderingTypePrediction.md)

### [**](#store_result)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L209)store\_result

* ****store\_result**(request, rendering\_type): None

- Overrides [RenderingTypePredictor.store\_result](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#store_result)

  Store prediction results and retrain the model.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    Used `Request` instance.

  * ##### rendering\_type: [RenderingType](https://crawlee.dev/python/python/api.md#RenderingType)

    Known suitable `RenderingType` for the used `Request` instance.

  #### Returns None


---

# EnqueueLinksFunction<!-- -->

A function for enqueueing new URLs to crawl based on elements selected by a given selector or explicit requests.

It adds explicitly passed `requests` to the `RequestManager` or it extracts URLs from the current page and enqueues them for further crawling. It allows filtering through selectors and other options. You can also specify labels and user data to be associated with the newly created `Request` objects.

It should not be called with `selector`, `label`, `user_data` or `transform_request_function` arguments together with `requests` argument.

For even more control over the enqueued links you can use combination of `ExtractLinksFunction` and `AddRequestsFunction`.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L414)\_\_call\_\_

* ****\_\_call\_\_**(\*: , selector?
  <!-- -->
  : str | None, attribute?
  <!-- -->
  : str | None, label?
  <!-- -->
  : str | None, user\_data?
  <!-- -->
  : dict\[str, Any] | None, transform\_request\_function?
  <!-- -->
  : Callable\[\[RequestOptions], [RequestOptions](https://crawlee.dev/python/python/api/class/RequestOptions.md) | [RequestTransformAction](https://crawlee.dev/python/python/api.md#RequestTransformAction)] | None, requests?
  <!-- -->
  : Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)] | None, rq\_id?
  <!-- -->
  : str | None, rq\_name?
  <!-- -->
  : str | None, rq\_alias?
  <!-- -->
  : str | None, limit: NotRequired\[int], base\_url: NotRequired\[str], strategy: NotRequired\[[EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)], include: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]], exclude: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]]): Coroutine\[None, None, None]
* ****\_\_call\_\_**(\*: , selector?
  <!-- -->
  : str | None, attribute?
  <!-- -->
  : str | None, label?
  <!-- -->
  : str | None, user\_data?
  <!-- -->
  : dict\[str, Any] | None, transform\_request\_function?
  <!-- -->
  : Callable\[\[RequestOptions], [RequestOptions](https://crawlee.dev/python/python/api/class/RequestOptions.md) | [RequestTransformAction](https://crawlee.dev/python/python/api.md#RequestTransformAction)] | None, rq\_id?
  <!-- -->
  : str | None, rq\_name?
  <!-- -->
  : str | None, rq\_alias?
  <!-- -->
  : str | None, limit: NotRequired\[int], base\_url: NotRequired\[str], strategy: NotRequired\[[EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)], include: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]], exclude: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]]): Coroutine\[None, None, None]
* ****\_\_call\_\_**(\*: , requests?
  <!-- -->
  : Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)] | None, rq\_id?
  <!-- -->
  : str | None, rq\_name?
  <!-- -->
  : str | None, rq\_alias?
  <!-- -->
  : str | None, limit: NotRequired\[int], base\_url: NotRequired\[str], strategy: NotRequired\[[EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)], include: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]], exclude: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]]): Coroutine\[None, None, None]

- Call enqueue links function.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyselector: str | None = <!-- -->None

    A selector used to find the elements containing the links. The behaviour differs based on the crawler used:

    * `PlaywrightCrawler` supports CSS and XPath selectors.
    * `ParselCrawler` supports CSS selectors.
    * `BeautifulSoupCrawler` supports CSS selectors.

  * ##### optionalkeyword-onlyattribute: str | None = <!-- -->None

    Which node attribute to extract the links from.

  * ##### optionalkeyword-onlylabel: str | None = <!-- -->None

    Label for the newly created `Request` objects, used for request routing.

  * ##### optionalkeyword-onlyuser\_data: dict\[str, Any] | None = <!-- -->None

    User data to be provided to the newly created `Request` objects.

  * ##### optionalkeyword-onlytransform\_request\_function: Callable\[\[RequestOptions], [RequestOptions](https://crawlee.dev/python/python/api/class/RequestOptions.md) | [RequestTransformAction](https://crawlee.dev/python/python/api.md#RequestTransformAction)] | None = <!-- -->None

    A function that takes `RequestOptions` and returns either:

    * Modified `RequestOptions` to update the request configuration,
    * `'skip'` to exclude the request from being enqueued,
    * `'unchanged'` to use the original request options without modification.

  * ##### optionalkeyword-onlyrequests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)] | None = <!-- -->None

    Requests to be added to the `RequestManager`.

  * ##### optionalkeyword-onlyrq\_id: str | None = <!-- -->None

    ID of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

  * ##### optionalkeyword-onlyrq\_name: str | None = <!-- -->None

    Name of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

  * ##### optionalkeyword-onlyrq\_alias: str | None = <!-- -->None

    Alias of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

  * ##### keyword-onlyoptionallimit: int

    Maximum number of requests to be enqueued.

  * ##### keyword-onlyoptionalbase\_url: str

    Base URL to be used for relative URLs.

  * ##### keyword-onlyoptionalstrategy: [EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)

    Enqueue strategy to be used for determining which links to extract and enqueue.

    Options: all: Enqueue every link encountered, regardless of the target domain. Use this option to ensure that all links, including those leading to external websites, are followed. same-domain: Enqueue links that share the same domain name as the current page, including any subdomains. This strategy is ideal for crawling within the same top-level domain while still allowing for subdomain exploration. same-hostname: Enqueue links only if they match the exact hostname of the current page. This is the default behavior and restricts the crawl to the current hostname, excluding subdomains. same-origin: Enqueue links that share the same origin as the current page. The origin is defined by the combination of protocol, domain, and port, ensuring a strict scope for the crawl.

  * ##### keyword-onlyoptionalinclude: Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]

    List of regular expressions or globs that URLs must match to be enqueued.

  * ##### keyword-onlyoptionalexclude: Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]

    List of regular expressions or globs that URLs must not match to be enqueued.

  #### Returns Coroutine\[None, None, None]


---

# EnqueueLinksKwargs<!-- -->

Keyword arguments for the `enqueue_links` methods.

### Hierarchy

* *EnqueueLinksKwargs*
  * [AddRequestsKwargs](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md)

## Index[**](#Index)

### Properties

* [**base\_url](#base_url)
* [**exclude](#exclude)
* [**include](#include)
* [**limit](#limit)
* [**strategy](#strategy)

## Properties<!-- -->[**](#Properties)

### [**](#base_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L153)keyword-onlyoptionalbase\_url

**base\_url: NotRequired\[str]

Base URL to be used for relative URLs.

### [**](#exclude)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L174)keyword-onlyoptionalexclude

**exclude: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]]

List of regular expressions or globs that URLs must not match to be enqueued.

### [**](#include)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L171)keyword-onlyoptionalinclude

**include: NotRequired\[Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]]

List of regular expressions or globs that URLs must match to be enqueued.

### [**](#limit)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L150)keyword-onlyoptionallimit

**limit: NotRequired\[int]

Maximum number of requests to be enqueued.

### [**](#strategy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L156)keyword-onlyoptionalstrategy

**strategy: NotRequired\[[EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)]

Enqueue strategy to be used for determining which links to extract and enqueue.

Options: all: Enqueue every link encountered, regardless of the target domain. Use this option to ensure that all links, including those leading to external websites, are followed. same-domain: Enqueue links that share the same domain name as the current page, including any subdomains. This strategy is ideal for crawling within the same top-level domain while still allowing for subdomain exploration. same-hostname: Enqueue links only if they match the exact hostname of the current page. This is the default behavior and restricts the crawl to the current hostname, excluding subdomains. same-origin: Enqueue links that share the same origin as the current page. The origin is defined by the combination of protocol, domain, and port, ensuring a strict scope for the crawl.


---

# ErrorSnapshotter<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#__init__)
* [**capture\_snapshot](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#capture_snapshot)

### Properties

* [**ALLOWED\_CHARACTERS](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#ALLOWED_CHARACTERS)
* [**BASE\_MESSAGE](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#BASE_MESSAGE)
* [**MAX\_ERROR\_CHARACTERS](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#MAX_ERROR_CHARACTERS)
* [**MAX\_FILENAME\_LENGTH](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#MAX_FILENAME_LENGTH)
* [**MAX\_HASH\_LENGTH](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#MAX_HASH_LENGTH)
* [**SNAPSHOT\_PREFIX](https://crawlee.dev/python/python/api/class/ErrorSnapshotter.md#SNAPSHOT_PREFIX)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L23)\_\_init\_\_

* ****\_\_init\_\_**(\*, snapshot\_kvs\_name): None

- #### Parameters

  * ##### optionalkeyword-onlysnapshot\_kvs\_name: str | None = <!-- -->None

  #### Returns None

### [**](#capture_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L26)capture\_snapshot

* **async **capture\_snapshot**(error\_message, file\_and\_line, context): None

- Capture error snapshot and save it to key value store.

  It saves the error snapshot directly to a key value store. It can't use `context.get_key_value_store` because it returns `KeyValueStoreChangeRecords` which is committed to the key value store only if the `RequestHandler` returned without an exception. ErrorSnapshotter is on the contrary active only when `RequestHandler` fails with an exception.

  ***

  #### Parameters

  * ##### error\_message: str

    Used in filename of the snapshot.

  * ##### file\_and\_line: str

    Used in filename of the snapshot.

  * ##### context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)

    Context that is used to get the snapshot.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#ALLOWED_CHARACTERS)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L21)ALLOWED\_CHARACTERS

**ALLOWED\_CHARACTERS: Undefined

### [**](#BASE_MESSAGE)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L19)BASE\_MESSAGE

**BASE\_MESSAGE: Undefined

### [**](#MAX_ERROR_CHARACTERS)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L16)MAX\_ERROR\_CHARACTERS

**MAX\_ERROR\_CHARACTERS: Undefined

### [**](#MAX_FILENAME_LENGTH)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L18)MAX\_FILENAME\_LENGTH

**MAX\_FILENAME\_LENGTH: Undefined

### [**](#MAX_HASH_LENGTH)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L17)MAX\_HASH\_LENGTH

**MAX\_HASH\_LENGTH: Undefined

### [**](#SNAPSHOT_PREFIX)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_snapshotter.py#L20)SNAPSHOT\_PREFIX

**SNAPSHOT\_PREFIX: Undefined


---

# ErrorTracker<!-- -->

Track errors and aggregates their counts by similarity.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ErrorTracker.md#__init__)
* [**add](https://crawlee.dev/python/python/api/class/ErrorTracker.md#add)
* [**get\_most\_common\_errors](https://crawlee.dev/python/python/api/class/ErrorTracker.md#get_most_common_errors)

### Properties

* [**total](https://crawlee.dev/python/python/api/class/ErrorTracker.md#total)
* [**unique\_error\_count](https://crawlee.dev/python/python/api/class/ErrorTracker.md#unique_error_count)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_tracker.py#L26)\_\_init\_\_

* ****\_\_init\_\_**(\*, snapshot\_kvs\_name, show\_error\_name, show\_file\_and\_line\_number, show\_error\_message, show\_full\_message, save\_error\_snapshots): None

- #### Parameters

  * ##### optionalkeyword-onlysnapshot\_kvs\_name: str | None = <!-- -->None
  * ##### optionalkeyword-onlyshow\_error\_name: bool = <!-- -->True
  * ##### optionalkeyword-onlyshow\_file\_and\_line\_number: bool = <!-- -->True
  * ##### optionalkeyword-onlyshow\_error\_message: bool = <!-- -->True
  * ##### optionalkeyword-onlyshow\_full\_message: bool = <!-- -->False
  * ##### optionalkeyword-onlysave\_error\_snapshots: bool = <!-- -->False

  #### Returns None

### [**](#add)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_tracker.py#L45)add

* **async **add**(error, \*, context): None

- Add an error in the statistics.

  ***

  #### Parameters

  * ##### error: Exception

    Error to be added to statistics.

  * ##### optionalkeyword-onlycontext: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md) | None = <!-- -->None

    Context used to collect error snapshot.

  #### Returns None

### [**](#get_most_common_errors)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_tracker.py#L141)get\_most\_common\_errors

* ****get\_most\_common\_errors**(n): list\[tuple\[str | None, int]]

- Return n most common errors.

  ***

  #### Parameters

  * ##### optionaln: int = <!-- -->3

  #### Returns list\[tuple\[str | None, int]]

## Properties<!-- -->[**](#Properties)

### [**](#total)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_tracker.py#L133)total

**total: int

Total number of errors.

### [**](#unique_error_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_error_tracker.py#L124)unique\_error\_count

**unique\_error\_count: int

Number of distinct kinds of errors.


---

# EventAbortingData<!-- -->

Data for the aborting event.

## Index[**](#Index)

### Properties

* [**model\_config](https://crawlee.dev/python/python/api/class/EventAbortingData.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L76)model\_config

**model\_config: Undefined


---

# EventCrawlerStatusData<!-- -->

Data for the crawler status event.

## Index[**](#Index)

### Properties

* [**crawler\_id](https://crawlee.dev/python/python/api/class/EventCrawlerStatusData.md#crawler_id)
* [**message](https://crawlee.dev/python/python/api/class/EventCrawlerStatusData.md#message)
* [**model\_config](https://crawlee.dev/python/python/api/class/EventCrawlerStatusData.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#crawler_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L95)crawler\_id

**crawler\_id: int

The ID of the crawler that emitted the event.

### [**](#message)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L92)message

**message: str

A message describing the current status of the crawler.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L90)model\_config

**model\_config: Undefined


---

# EventExitData<!-- -->

Data for the exit event.

## Index[**](#Index)

### Properties

* [**model\_config](https://crawlee.dev/python/python/api/class/EventExitData.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L83)model\_config

**model\_config: Undefined


---

# EventLoopSnapshot<!-- -->

Snapshot of the state of the event loop.

## Index[**](#Index)

### Properties

* [**created\_at](https://crawlee.dev/python/python/api/class/EventLoopSnapshot.md#created_at)
* [**delay](https://crawlee.dev/python/python/api/class/EventLoopSnapshot.md#delay)
* [**is\_overloaded](https://crawlee.dev/python/python/api/class/EventLoopSnapshot.md#is_overloaded)
* [**max\_delay](https://crawlee.dev/python/python/api/class/EventLoopSnapshot.md#max_delay)
* [**max\_delay\_exceeded](https://crawlee.dev/python/python/api/class/EventLoopSnapshot.md#max_delay_exceeded)

## Properties<!-- -->[**](#Properties)

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L135)created\_at

**created\_at: datetime

The time at which the system load information was measured.

### [**](#delay)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L129)delay

**delay: timedelta

The current delay of the event loop.

### [**](#is_overloaded)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L144)is\_overloaded

**is\_overloaded: bool

Indicate whether the event loop is considered as overloaded.

### [**](#max_delay)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L132)max\_delay

**max\_delay: timedelta

The maximum delay that is considered acceptable.

### [**](#max_delay_exceeded)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L139)max\_delay\_exceeded

**max\_delay\_exceeded: timedelta

The amount of time by which the delay exceeds the maximum delay.


---

# EventManager<!-- -->

Manage events and their listeners, enabling registration, emission, and execution control.

It allows for registering event listeners, emitting events, and ensuring all listeners complete their execution. Built on top of `pyee.asyncio.AsyncIOEventEmitter`. It implements additional features such as waiting for all listeners to complete and emitting `PersistState` events at regular intervals.

### Hierarchy

* *EventManager*
  * [LocalEventManager](https://crawlee.dev/python/python/api/class/LocalEventManager.md)

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/EventManager.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/EventManager.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/EventManager.md#__init__)
* [**emit](https://crawlee.dev/python/python/api/class/EventManager.md#emit)
* [**off](https://crawlee.dev/python/python/api/class/EventManager.md#off)
* [**on](https://crawlee.dev/python/python/api/class/EventManager.md#on)
* [**wait\_for\_all\_listeners\_to\_complete](https://crawlee.dev/python/python/api/class/EventManager.md#wait_for_all_listeners_to_complete)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/EventManager.md#active)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L104)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

- Initialize the event manager upon entering the async context.

  ***

  #### Returns [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L113)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Close the local event manager upon exiting the async context.

  This will stop listening for the events, and it will wait for all the event listeners to finish.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L63)\_\_init\_\_

* ****\_\_init\_\_**(\*, persist\_state\_interval, close\_timeout): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypersist\_state\_interval: timedelta = <!-- -->timedelta(minutes=1)

    Interval between emitted `PersistState` events to maintain state persistence.

  * ##### optionalkeyword-onlyclose\_timeout: timedelta | None = <!-- -->None

    Optional timeout for canceling pending event listeners if they exceed this duration.

  #### Returns None

### [**](#emit)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L242)emit

* ****emit**(\*: , event: [Event](https://crawlee.dev/python/python/api/enum/Event.md), event\_data: [EventData](https://crawlee.dev/python/python/api.md#EventData)): None
* ****emit**(\*: , event: Literal\[Event.PERSIST\_STATE], event\_data: [EventPersistStateData](https://crawlee.dev/python/python/api/class/EventPersistStateData.md)): None
* ****emit**(\*: , event: Literal\[Event.SYSTEM\_INFO], event\_data: [EventSystemInfoData](https://crawlee.dev/python/python/api/class/EventSystemInfoData.md)): None
* ****emit**(\*: , event: Literal\[Event.MIGRATING], event\_data: [EventMigratingData](https://crawlee.dev/python/python/api/class/EventMigratingData.md)): None
* ****emit**(\*: , event: Literal\[Event.ABORTING], event\_data: [EventAbortingData](https://crawlee.dev/python/python/api/class/EventAbortingData.md)): None
* ****emit**(\*: , event: Literal\[Event.EXIT], event\_data: [EventExitData](https://crawlee.dev/python/python/api/class/EventExitData.md)): None
* ****emit**(\*: , event: Literal\[Event.CRAWLER\_STATUS], event\_data: [EventCrawlerStatusData](https://crawlee.dev/python/python/api/class/EventCrawlerStatusData.md)): None
* ****emit**(\*: , event: [Event](https://crawlee.dev/python/python/api/enum/Event.md), event\_data: Any): None

- Emit an event with the associated data to all registered listeners.

  ***

  #### Parameters

  * ##### keyword-onlyevent: [Event](https://crawlee.dev/python/python/api/enum/Event.md)

    The event which will be emitted.

  * ##### keyword-onlyevent\_data: [EventData](https://crawlee.dev/python/python/api.md#EventData)

    The data which will be passed to the event listeners.

  #### Returns None

### [**](#off)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L210)off

* ****off**(\*, event, listener): None

- Remove a specific listener or all listeners for an event.

  ***

  #### Parameters

  * ##### keyword-onlyevent: [Event](https://crawlee.dev/python/python/api/enum/Event.md)

    The Actor event for which to remove listeners.

  * ##### optionalkeyword-onlylistener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[Any] | None = <!-- -->None

    The listener which is supposed to be removed. If not passed, all listeners of this event are removed.

  #### Returns None

### [**](#on)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L160)on

* ****on**(\*: , event: [Event](https://crawlee.dev/python/python/api/enum/Event.md), listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[Any]): None
* ****on**(\*: , event: Literal\[Event.PERSIST\_STATE], listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[[EventPersistStateData](https://crawlee.dev/python/python/api/class/EventPersistStateData.md)]): None
* ****on**(\*: , event: Literal\[Event.SYSTEM\_INFO], listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[[EventSystemInfoData](https://crawlee.dev/python/python/api/class/EventSystemInfoData.md)]): None
* ****on**(\*: , event: Literal\[Event.MIGRATING], listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[[EventMigratingData](https://crawlee.dev/python/python/api/class/EventMigratingData.md)]): None
* ****on**(\*: , event: Literal\[Event.ABORTING], listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[[EventAbortingData](https://crawlee.dev/python/python/api/class/EventAbortingData.md)]): None
* ****on**(\*: , event: Literal\[Event.EXIT], listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[[EventExitData](https://crawlee.dev/python/python/api/class/EventExitData.md)]): None
* ****on**(\*: , event: Literal\[Event.CRAWLER\_STATUS], listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[[EventCrawlerStatusData](https://crawlee.dev/python/python/api/class/EventCrawlerStatusData.md)]): None
* ****on**(\*: , event: [Event](https://crawlee.dev/python/python/api/enum/Event.md), listener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[None]): None

- Register an event listener for a specific event.

  ***

  #### Parameters

  * ##### keyword-onlyevent: [Event](https://crawlee.dev/python/python/api/enum/Event.md)

    The event for which to listen to.

  * ##### keyword-onlylistener: [EventListener](https://crawlee.dev/python/python/api.md#EventListener)\[Any]

    The function (sync or async) which is to be called when the event is emitted.

  #### Returns None

### [**](#wait_for_all_listeners_to_complete)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L252)wait\_for\_all\_listeners\_to\_complete

* **async **wait\_for\_all\_listeners\_to\_complete**(\*, timeout): None

- Wait for all currently executing event listeners to complete.

  ***

  #### Parameters

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    The maximum time to wait for the event listeners to finish. If they do not complete within the specified timeout, they will be canceled.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L100)active

**active: bool

Indicate whether the context is active.


---

# EventManagerOptions<!-- -->

Arguments for the `EventManager` constructor.

It is intended for typing forwarded `__init__` arguments in the subclasses.

## Index[**](#Index)

### Properties

* [**close\_timeout](#close_timeout)
* [**persist\_state\_interval](#persist_state_interval)

## Properties<!-- -->[**](#Properties)

### [**](#close_timeout)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L50)keyword-onlyoptionalclose\_timeout

**close\_timeout: NotRequired\[timedelta | None]

Optional timeout for canceling pending event listeners if they exceed this duration.

### [**](#persist_state_interval)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L47)keyword-onlyoptionalpersist\_state\_interval

**persist\_state\_interval: NotRequired\[timedelta]

Interval between emitted `PersistState` events to maintain state persistence.


---

# EventMigratingData<!-- -->

Data for the migrating event.

## Index[**](#Index)

### Properties

* [**model\_config](https://crawlee.dev/python/python/api/class/EventMigratingData.md#model_config)
* [**time\_remaining](https://crawlee.dev/python/python/api/class/EventMigratingData.md#time_remaining)

## Properties<!-- -->[**](#Properties)

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L65)model\_config

**model\_config: Undefined

### [**](#time_remaining)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L69)time\_remaining

**time\_remaining: [timedelta\_secs](https://crawlee.dev/python/python/api.md#timedelta_secs) | None


---

# EventPersistStateData<!-- -->

Data for the persist state event.

## Index[**](#Index)

### Properties

* [**is\_migrating](https://crawlee.dev/python/python/api/class/EventPersistStateData.md#is_migrating)
* [**model\_config](https://crawlee.dev/python/python/api/class/EventPersistStateData.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#is_migrating)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L45)is\_migrating

**is\_migrating: bool

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L43)model\_config

**model\_config: Undefined


---

# EventSystemInfoData<!-- -->

Data for the system info event.

## Index[**](#Index)

### Properties

* [**cpu\_info](https://crawlee.dev/python/python/api/class/EventSystemInfoData.md#cpu_info)
* [**memory\_info](https://crawlee.dev/python/python/api/class/EventSystemInfoData.md#memory_info)
* [**model\_config](https://crawlee.dev/python/python/api/class/EventSystemInfoData.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#cpu_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L54)cpu\_info

**cpu\_info: [CpuInfo](https://crawlee.dev/python/python/api/class/CpuInfo.md)

### [**](#memory_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L55)memory\_info

**memory\_info: [MemoryUsageInfo](https://crawlee.dev/python/python/api/class/MemoryUsageInfo.md)

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L52)model\_config

**model\_config: Undefined


---

# ExportDataCsvKwargs<!-- -->

Keyword arguments for dataset's `export_data_csv` method.

## Index[**](#Index)

### Properties

* [**delimiter](#delimiter)
* [**dialect](#dialect)
* [**doublequote](#doublequote)
* [**escapechar](#escapechar)
* [**lineterminator](#lineterminator)
* [**quotechar](#quotechar)
* [**quoting](#quoting)
* [**skipinitialspace](#skipinitialspace)
* [**strict](#strict)

## Properties<!-- -->[**](#Properties)

### [**](#delimiter)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L798)keyword-onlyoptionaldelimiter

**delimiter: NotRequired\[str]

A one-character string used to separate fields. Defaults to ','.

### [**](#dialect)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L795)keyword-onlyoptionaldialect

**dialect: NotRequired\[str]

Specifies a dialect to be used in CSV parsing and writing.

### [**](#doublequote)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L801)keyword-onlyoptionaldoublequote

**doublequote: NotRequired\[bool]

Controls how instances of `quotechar` inside a field should be quoted. When True, the character is doubled; when False, the `escapechar` is used as a prefix. Defaults to True.

### [**](#escapechar)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L805)keyword-onlyoptionalescapechar

**escapechar: NotRequired\[str]

A one-character string used to escape the delimiter if `quoting` is set to `QUOTE_NONE` and the `quotechar` if `doublequote` is False. Defaults to None, disabling escaping.

### [**](#lineterminator)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L809)keyword-onlyoptionallineterminator

**lineterminator: NotRequired\[str]

The string used to terminate lines produced by the writer. Defaults to '\r\n'.

### [**](#quotechar)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L812)keyword-onlyoptionalquotechar

**quotechar: NotRequired\[str]

A one-character string used to quote fields containing special characters, like the delimiter or quotechar, or fields containing new-line characters. Defaults to '"'.

### [**](#quoting)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L816)keyword-onlyoptionalquoting

**quoting: NotRequired\[int]

Controls when quotes should be generated by the writer and recognized by the reader. Can take any of the `QUOTE_*` constants, with a default of `QUOTE_MINIMAL`.

### [**](#skipinitialspace)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L820)keyword-onlyoptionalskipinitialspace

**skipinitialspace: NotRequired\[bool]

When True, spaces immediately following the delimiter are ignored. Defaults to False.

### [**](#strict)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L823)keyword-onlyoptionalstrict

**strict: NotRequired\[bool]

When True, raises an exception on bad CSV input. Defaults to False.


---

# ExportDataJsonKwargs<!-- -->

Keyword arguments for dataset's `export_data_json` method.

## Index[**](#Index)

### Properties

* [**allow\_nan](#allow_nan)
* [**check\_circular](#check_circular)
* [**cls](#cls)
* [**default](#default)
* [**ensure\_ascii](#ensure_ascii)
* [**indent](#indent)
* [**separators](#separators)
* [**skipkeys](#skipkeys)
* [**sort\_keys](#sort_keys)

## Properties<!-- -->[**](#Properties)

### [**](#allow_nan)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L770)keyword-onlyoptionalallow\_nan

**allow\_nan: NotRequired\[bool]

If False (default: True), raises a ValueError for out-of-range float values (nan, inf, -inf) to strictly comply with the JSON specification. If True, uses their JavaScript equivalents (NaN, Infinity, -Infinity).

### [**](#check_circular)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L766)keyword-onlyoptionalcheck\_circular

**check\_circular: NotRequired\[bool]

If False (default: True), skips the circular reference check for container types. A circular reference will result in a `RecursionError` or worse if unchecked.

### [**](#cls)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L774)keyword-onlyoptionalcls

**cls: NotRequired\[[type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[json.JSONEncoder]]

Allows specifying a custom JSON encoder.

### [**](#default)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L784)keyword-onlyoptionaldefault

**default: NotRequired\[Callable]

A function called for objects that can't be serialized otherwise. It should return a JSON-encodable version of the object or raise a `TypeError`.

### [**](#ensure_ascii)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L763)keyword-onlyoptionalensure\_ascii

**ensure\_ascii: NotRequired\[bool]

Determines if non-ASCII characters should be escaped in the output JSON string.

### [**](#indent)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L777)keyword-onlyoptionalindent

**indent: NotRequired\[int]

Specifies the number of spaces for indentation in the pretty-printed JSON output.

### [**](#separators)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L780)keyword-onlyoptionalseparators

**separators: NotRequired\[tuple\[str, str]]

A tuple of (item\_separator, key\_separator). The default is (', ', ': ') if indent is None and (',', ': ') otherwise.

### [**](#skipkeys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L759)keyword-onlyoptionalskipkeys

**skipkeys: NotRequired\[bool]

If True (default: False), dict keys that are not of a basic type (str, int, float, bool, None) will be skipped instead of raising a `TypeError`.

### [**](#sort_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L788)keyword-onlyoptionalsort\_keys

**sort\_keys: NotRequired\[bool]

Specifies whether the output JSON object should have keys sorted alphabetically.


---

# ExportToKwargs<!-- -->

Keyword arguments for dataset's `export_to` method.

## Index[**](#Index)

### Properties

* [**content\_type](https://crawlee.dev/python/python/api/class/ExportToKwargs.md#content_type)
* [**key](https://crawlee.dev/python/python/api/class/ExportToKwargs.md#key)
* [**to\_kvs\_configuration](https://crawlee.dev/python/python/api/class/ExportToKwargs.md#to_kvs_configuration)
* [**to\_kvs\_id](https://crawlee.dev/python/python/api/class/ExportToKwargs.md#to_kvs_id)
* [**to\_kvs\_name](https://crawlee.dev/python/python/api/class/ExportToKwargs.md#to_kvs_name)
* [**to\_kvs\_storage\_client](https://crawlee.dev/python/python/api/class/ExportToKwargs.md#to_kvs_storage_client)

## Properties<!-- -->[**](#Properties)

### [**](#content_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L740)content\_type

**content\_type: NotRequired\[Literal\[json, csv]]

The format in which to export the data. Either 'json' or 'csv'.

### [**](#key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L737)key

**key: Required\[str]

The key under which to save the data.

### [**](#to_kvs_configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L752)to\_kvs\_configuration

**to\_kvs\_configuration: NotRequired\[[Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)]

The configuration to use for saving the exported file.

### [**](#to_kvs_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L743)to\_kvs\_id

**to\_kvs\_id: NotRequired\[str]

ID of the key-value store to save the exported file.

### [**](#to_kvs_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L746)to\_kvs\_name

**to\_kvs\_name: NotRequired\[str]

Name of the key-value store to save the exported file.

### [**](#to_kvs_storage_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L749)to\_kvs\_storage\_client

**to\_kvs\_storage\_client: NotRequired\[[StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)]

The storage client to use for saving the exported file.


---

# ExtractLinksFunction<!-- -->

A function for extracting URLs to crawl based on elements selected by a given selector.

It extracts URLs from the current page and allows filtering through selectors and other options. You can also specify labels and user data to be associated with the newly created `Request` objects.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L462)\_\_call\_\_

* ****\_\_call\_\_**(\*, selector, attribute, label, user\_data, transform\_request\_function, limit, base\_url, strategy, include, exclude): Coroutine\[None, None, list\[[Request](https://crawlee.dev/python/python/api/class/Request.md)]]

- Call extract links function.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyselector: str = <!-- -->'a'

    A selector used to find the elements containing the links. The behaviour differs based on the crawler used:

    * `PlaywrightCrawler` supports CSS and XPath selectors.
    * `ParselCrawler` supports CSS selectors.
    * `BeautifulSoupCrawler` supports CSS selectors.

  * ##### optionalkeyword-onlyattribute: str = <!-- -->'href'

    Which node attribute to extract the links from.

  * ##### optionalkeyword-onlylabel: str | None = <!-- -->None

    Label for the newly created `Request` objects, used for request routing.

  * ##### optionalkeyword-onlyuser\_data: dict\[str, Any] | None = <!-- -->None

    User data to be provided to the newly created `Request` objects.

  * ##### optionalkeyword-onlytransform\_request\_function: Callable\[\[RequestOptions], [RequestOptions](https://crawlee.dev/python/python/api/class/RequestOptions.md) | [RequestTransformAction](https://crawlee.dev/python/python/api.md#RequestTransformAction)] | None = <!-- -->None

    A function that takes `RequestOptions` and returns either:

    * Modified `RequestOptions` to update the request configuration,
    * `'skip'` to exclude the request from being enqueued,
    * `'unchanged'` to use the original request options without modification.

  * ##### keyword-onlyoptionallimit: int

    Maximum number of requests to be enqueued.

  * ##### keyword-onlyoptionalbase\_url: str

    Base URL to be used for relative URLs.

  * ##### keyword-onlyoptionalstrategy: [EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)

    Enqueue strategy to be used for determining which links to extract and enqueue.

    Options: all: Enqueue every link encountered, regardless of the target domain. Use this option to ensure that all links, including those leading to external websites, are followed. same-domain: Enqueue links that share the same domain name as the current page, including any subdomains. This strategy is ideal for crawling within the same top-level domain while still allowing for subdomain exploration. same-hostname: Enqueue links only if they match the exact hostname of the current page. This is the default behavior and restricts the crawl to the current hostname, excluding subdomains. same-origin: Enqueue links that share the same origin as the current page. The origin is defined by the combination of protocol, domain, and port, ensuring a strict scope for the crawl.

  * ##### keyword-onlyoptionalinclude: Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]

    List of regular expressions or globs that URLs must match to be enqueued.

  * ##### keyword-onlyoptionalexclude: Sequence\[re.Pattern | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)]

    List of regular expressions or globs that URLs must not match to be enqueued.

  #### Returns Coroutine\[None, None, list\[[Request](https://crawlee.dev/python/python/api/class/Request.md)]]


---

# FailedImport<!-- -->

Represent a placeholder for a failed import.

## Index[**](#Index)

### Properties

* [**message](https://crawlee.dev/python/python/api/class/FailedImport.md#message)

## Properties<!-- -->[**](#Properties)

### [**](#message)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/try_import.py#L31)message

**message: str

The error message associated with the failed import.


---

# FileSystemDatasetClient<!-- -->

File system implementation of the dataset client.

This client persists dataset items to the file system as individual JSON files within a structured directory hierarchy following the pattern:

```
{STORAGE_DIR}/datasets/{DATASET_ID}/{ITEM_ID}.json
```

Each item is stored as a separate file, which allows for durability and the ability to recover after process termination. Dataset operations like filtering, sorting, and pagination are implemented by processing the stored files according to the requested parameters.

This implementation is ideal for long-running crawlers where data persistence is important, and for development environments where you want to easily inspect the collected data between runs.

### Hierarchy

* [DatasetClient](https://crawlee.dev/python/python/api/class/DatasetClient.md)
  * *FileSystemDatasetClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#__init__)
* [**drop](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#drop)
* [**get\_data](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#get_data)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#get_metadata)
* [**iterate\_items](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#iterate_items)
* [**open](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#purge)
* [**push\_data](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#push_data)

### Properties

* [**path\_to\_dataset](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#path_to_dataset)
* [**path\_to\_metadata](https://crawlee.dev/python/python/api/class/FileSystemDatasetClient.md#path_to_metadata)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L56)\_\_init\_\_

* ****\_\_init\_\_**(\*, metadata, path\_to\_dataset, lock): None

- Initialize a new instance.

  Preferably use the `FileSystemDatasetClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlymetadata: [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)
  * ##### keyword-onlypath\_to\_dataset: Path
  * ##### keyword-onlylock: asyncio.Lock

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L205)drop

* **async **drop**(): None

- Overrides [DatasetClient.drop](https://crawlee.dev/python/python/api/class/DatasetClient.md#drop)

  Drop the whole dataset and remove all its items.

  The backend method for the `Dataset.drop` call.

  ***

  #### Returns None

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L242)get\_data

* **async **get\_data**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden, flatten, view): [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

- Overrides [DatasetClient.get\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_data)

  Get data from the dataset with various filtering options.

  The backend method for the `Dataset.get_data` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyoffset: int = <!-- -->0
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->999\_999\_999\_999
  * ##### optionalkeyword-onlyclean: bool = <!-- -->False
  * ##### optionalkeyword-onlydesc: bool = <!-- -->False
  * ##### optionalkeyword-onlyfields: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyomit: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyunwind: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyskip\_empty: bool = <!-- -->False
  * ##### optionalkeyword-onlyskip\_hidden: bool = <!-- -->False
  * ##### optionalkeyword-onlyflatten: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyview: str | None = <!-- -->None

  #### Returns [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L76)get\_metadata

* **async **get\_metadata**(): [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

- Overrides [DatasetClient.get\_metadata](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_metadata)

  Get the metadata of the dataset.

  ***

  #### Returns [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

### [**](#iterate_items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L341)iterate\_items

* **async **iterate\_items**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden): AsyncIterator\[dict\[str, Any]]

- Overrides [DatasetClient.iterate\_items](https://crawlee.dev/python/python/api/class/DatasetClient.md#iterate_items)

  Iterate over the dataset items with filtering options.

  The backend method for the `Dataset.iterate_items` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyoffset: int = <!-- -->0
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->None
  * ##### optionalkeyword-onlyclean: bool = <!-- -->False
  * ##### optionalkeyword-onlydesc: bool = <!-- -->False
  * ##### optionalkeyword-onlyfields: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyomit: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyunwind: list\[str] | None = <!-- -->None
  * ##### optionalkeyword-onlyskip\_empty: bool = <!-- -->False
  * ##### optionalkeyword-onlyskip\_hidden: bool = <!-- -->False

  #### Returns AsyncIterator\[dict\[str, Any]]

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L90)open

* **async **open**(\*, id, name, alias, configuration): Self

- Open or create a file system dataset client.

  This method attempts to open an existing dataset from the file system. If a dataset with the specified ID or name exists, it loads the metadata from the stored files. If no existing dataset is found, a new one is created.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the dataset to open. If provided, searches for existing dataset by ID.

  * ##### keyword-onlyname: str | None

    The name of the dataset for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the dataset for unnamed (run scope) storages.

  * ##### keyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

    The configuration object containing storage directory settings.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L211)purge

* **async **purge**(): None

- Overrides [DatasetClient.purge](https://crawlee.dev/python/python/api/class/DatasetClient.md#purge)

  Purge all items from the dataset.

  The backend method for the `Dataset.purge` call.

  ***

  #### Returns None

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L223)push\_data

* **async **push\_data**(data): None

- Overrides [DatasetClient.push\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#push_data)

  Push data to the dataset.

  The backend method for the `Dataset.push_data` call.

  ***

  #### Parameters

  * ##### data: list\[Any] | dict\[str, Any]

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#path_to_dataset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L80)path\_to\_dataset

**path\_to\_dataset: Path

The full path to the dataset directory.

### [**](#path_to_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_dataset_client.py#L85)path\_to\_metadata

**path\_to\_metadata: Path

The full path to the dataset metadata file.


---

# FileSystemKeyValueStoreClient<!-- -->

File system implementation of the key-value store client.

This client persists data to the file system, making it suitable for scenarios where data needs to survive process restarts. Keys are mapped to file paths in a directory structure following the pattern:

```
{STORAGE_DIR}/key_value_stores/{STORE_ID}/{KEY}
```

Binary data is stored as-is, while JSON and text data are stored in human-readable format. The implementation automatically handles serialization based on the content type and maintains metadata about each record.

This implementation is ideal for long-running crawlers where persistence is important and for development environments where you want to easily inspect the stored data between runs.

### Hierarchy

* [KeyValueStoreClient](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md)
  * *FileSystemKeyValueStoreClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#__init__)
* [**delete\_value](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#delete_value)
* [**drop](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#drop)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#get_metadata)
* [**get\_public\_url](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#get_public_url)
* [**get\_value](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#get_value)
* [**iterate\_keys](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#iterate_keys)
* [**open](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#purge)
* [**record\_exists](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#record_exists)
* [**set\_value](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#set_value)

### Properties

* [**path\_to\_kvs](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#path_to_kvs)
* [**path\_to\_metadata](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md#path_to_metadata)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L56)\_\_init\_\_

* ****\_\_init\_\_**(\*, metadata, path\_to\_kvs, lock): None

- Initialize a new instance.

  Preferably use the `FileSystemKeyValueStoreClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlymetadata: [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)
  * ##### keyword-onlypath\_to\_kvs: Path
  * ##### keyword-onlylock: asyncio.Lock

  #### Returns None

### [**](#delete_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L344)delete\_value

* **async **delete\_value**(\*, key): None

- Overrides [KeyValueStoreClient.delete\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#delete_value)

  Delete a value from the key-value store by its key.

  The backend method for the `KeyValueStore.delete_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L204)drop

* **async **drop**(): None

- Overrides [KeyValueStoreClient.drop](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#drop)

  Drop the whole key-value store and remove all its values.

  The backend method for the `KeyValueStore.drop` call.

  ***

  #### Returns None

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L76)get\_metadata

* **async **get\_metadata**(): [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

- Overrides [KeyValueStoreClient.get\_metadata](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_metadata)

  Get the metadata of the key-value store.

  ***

  #### Returns [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

### [**](#get_public_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L428)get\_public\_url

* **async **get\_public\_url**(\*, key): str

- Overrides [KeyValueStoreClient.get\_public\_url](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_public_url)

  Return a file:// URL for the given key.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

    The key to get the public URL for.

  #### Returns str

  A file:// URL pointing to the file on the local filesystem.

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L224)get\_value

* **async **get\_value**(\*, key): [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

- Overrides [KeyValueStoreClient.get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_value)

  Retrieve the given record from the key-value store.

  The backend method for the `KeyValueStore.get_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

### [**](#iterate_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L367)iterate\_keys

* **async **iterate\_keys**(\*, exclusive\_start\_key, limit): AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

- Overrides [KeyValueStoreClient.iterate\_keys](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#iterate_keys)

  Iterate over all the existing keys in the key-value store.

  The backend method for the `KeyValueStore.iterate_keys` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyexclusive\_start\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->None

  #### Returns AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L90)open

* **async **open**(\*, id, name, alias, configuration): Self

- Open or create a file system key-value store client.

  This method attempts to open an existing key-value store from the file system. If a KVS with the specified ID or name exists, it loads the metadata from the stored files. If no existing store is found, a new one is created.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the key-value store to open. If provided, searches for existing store by ID.

  * ##### keyword-onlyname: str | None

    The name of the key-value store for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the key-value store for unnamed (run scope) storages.

  * ##### keyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

    The configuration object containing storage directory settings.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L211)purge

* **async **purge**(): None

- Overrides [KeyValueStoreClient.purge](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#purge)

  Purge all items from the key-value store.

  The backend method for the `KeyValueStore.purge` call.

  ***

  #### Returns None

### [**](#record_exists)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L442)record\_exists

* **async **record\_exists**(\*, key): bool

- Overrides [KeyValueStoreClient.record\_exists](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#record_exists)

  Check if a record with the given key exists in the key-value store.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

    The key to check for existence.

  #### Returns bool

  True if a record with the given key exists, False otherwise.

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L303)set\_value

* **async **set\_value**(\*, key, value, content\_type): None

- Overrides [KeyValueStoreClient.set\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#set_value)

  Set a value in the key-value store by its key.

  The backend method for the `KeyValueStore.set_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str
  * ##### keyword-onlyvalue: Any
  * ##### optionalkeyword-onlycontent\_type: str | None = <!-- -->None

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#path_to_kvs)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L80)path\_to\_kvs

**path\_to\_kvs: Path

The full path to the key-value store directory.

### [**](#path_to_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_key_value_store_client.py#L85)path\_to\_metadata

**path\_to\_metadata: Path

The full path to the key-value store metadata file.


---

# FileSystemRequestQueueClient<!-- -->

A file system implementation of the request queue client.

This client persists requests to the file system as individual JSON files, making it suitable for scenarios where data needs to survive process restarts. Each request is stored as a separate file in a directory structure following the pattern:

```
{STORAGE_DIR}/request_queues/{QUEUE_ID}/{REQUEST_ID}.json
```

The implementation uses `RecoverableState` to maintain ordering information, in-progress status, and request handling status. This allows for proper state recovery across process restarts without embedding metadata in individual request files. File system storage provides durability at the cost of slower I/O operations compared to memory only-based storage.

This implementation is ideal for long-running crawlers where persistence is important and for situations where you need to resume crawling after process termination.

### Hierarchy

* [RequestQueueClient](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)
  * *FileSystemRequestQueueClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#__init__)
* [**add\_batch\_of\_requests](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#add_batch_of_requests)
* [**drop](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#fetch_next_request)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#get_metadata)
* [**get\_request](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#get_request)
* [**is\_empty](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#is_empty)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#mark_request_as_handled)
* [**open](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#purge)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#reclaim_request)

### Properties

* [**path\_to\_metadata](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#path_to_metadata)
* [**path\_to\_rq](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md#path_to_rq)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L91)\_\_init\_\_

* ****\_\_init\_\_**(\*, metadata, path\_to\_rq, lock, recoverable\_state): None

- Initialize a new instance.

  Preferably use the `FileSystemRequestQueueClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlymetadata: [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)
  * ##### keyword-onlypath\_to\_rq: Path
  * ##### keyword-onlylock: asyncio.Lock
  * ##### keyword-onlyrecoverable\_state: [RecoverableState](https://crawlee.dev/python/python/api/class/RecoverableState.md)\[[RequestQueueState](https://crawlee.dev/python/python/api/class/RequestQueueState.md)]

  #### Returns None

### [**](#add_batch_of_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L323)add\_batch\_of\_requests

* **async **add\_batch\_of\_requests**(requests, \*, forefront): [AddRequestsResponse](https://crawlee.dev/python/python/api/class/AddRequestsResponse.md)

- Overrides [RequestQueueClient.add\_batch\_of\_requests](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#add_batch_of_requests)

  Add batch of requests to the queue.

  This method adds a batch of requests to the queue. Each request is processed based on its uniqueness (determined by `unique_key`). Duplicates will be identified but not re-added to the queue.

  ***

  #### Parameters

  * ##### requests: Sequence\[[Request](https://crawlee.dev/python/python/api/class/Request.md)]

    The collection of requests to add to the queue.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    Whether to put the added requests at the beginning (True) or the end (False) of the queue. When True, the requests will be processed sooner than previously added requests.

  #### Returns [AddRequestsResponse](https://crawlee.dev/python/python/api/class/AddRequestsResponse.md)

  A response object containing information about which requests were successfully processed and which failed (if any).

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L283)drop

* **async **drop**(): None

- Overrides [RequestQueueClient.drop](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#drop)

  Drop the whole request queue and remove all its values.

  The backend method for the `RequestQueue.drop` call.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L461)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#fetch_next_request)

  Return the next request in the queue to be processed.

  Once you successfully finish processing of the request, you need to call `RequestQueue.mark_request_as_handled` to mark the request as handled in the queue. If there was some error in processing the request, call `RequestQueue.reclaim_request` instead, so that the queue will give the request to some other consumer in another call to the `fetch_next_request` method.

  Note that the `None` return value does not mean the queue processing finished, it means there are currently no pending requests. To check whether all requests in queue were finished, use `RequestQueue.is_finished` instead.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The request or `None` if there are no more pending requests.

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L124)get\_metadata

* **async **get\_metadata**(): [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [RequestQueueClient.get\_metadata](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_metadata)

  Get the metadata of the request queue.

  ***

  #### Returns [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#get_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L448)get\_request

* **async **get\_request**(unique\_key): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.get\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_request)

  Retrieve a request from the queue.

  ***

  #### Parameters

  * ##### unique\_key: str

    Unique key of the request to retrieve.

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The retrieved request, or None, if it did not exist.

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L588)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestQueueClient.is\_empty](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#is_empty)

  Check if the request queue is empty.

  ***

  #### Returns bool

  True if the request queue is empty, False otherwise.

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L484)mark\_request\_as\_handled

* **async **mark\_request\_as\_handled**(request): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestQueueClient.mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#mark_request_as_handled)

  Mark a request as handled after successful processing.

  Handled requests will never again be returned by the `RequestQueue.fetch_next_request` method.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to mark as handled.

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

  Information about the queue operation. `None` if the given request was not in progress.

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L154)open

* **async **open**(\*, id, name, alias, configuration): Self

- Open or create a file system request queue client.

  This method attempts to open an existing request queue from the file system. If a queue with the specified ID or name exists, it loads the metadata and state from the stored files. If no existing queue is found, a new one is created.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the request queue to open. If provided, searches for existing queue by ID.

  * ##### keyword-onlyname: str | None

    The name of the request queue for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the request queue for unnamed (run scope) storages.

  * ##### keyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

    The configuration object containing storage directory settings.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L299)purge

* **async **purge**(): None

- Overrides [RequestQueueClient.purge](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#purge)

  Purge all items from the request queue.

  The backend method for the `RequestQueue.purge` call.

  ***

  #### Returns None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L527)reclaim\_request

* **async **reclaim\_request**(request, \*, forefront): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestQueueClient.reclaim\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#reclaim_request)

  Reclaim a failed request back to the queue.

  The request will be returned for processing later again by another call to `RequestQueue.fetch_next_request`.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to return to the queue.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    Whether to add the request to the head or the end of the queue.

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

  Information about the queue operation. `None` if the given request was not in progress.

## Properties<!-- -->[**](#Properties)

### [**](#path_to_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L133)path\_to\_metadata

**path\_to\_metadata: Path

The full path to the request queue metadata file.

### [**](#path_to_rq)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L128)path\_to\_rq

**path\_to\_rq: Path

The full path to the request queue directory.


---

# FileSystemStorageClient<!-- -->

File system implementation of the storage client.

This storage client provides access to datasets, key-value stores, and request queues that persist data to the local file system. Each storage type is implemented with its own specific file system client that stores data in a structured directory hierarchy.

Data is stored in JSON format in predictable file paths, making it easy to inspect and manipulate the stored data outside of the Crawlee application if needed.

All data persists between program runs but is limited to access from the local machine where the files are stored.

Warning: This storage client is not safe for concurrent access from multiple crawler processes. Use it only when running a single crawler process at a time.

### Hierarchy

* [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)
  * *FileSystemStorageClient*

## Index[**](#Index)

### Methods

* [**create\_dataset\_client](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md#create_dataset_client)
* [**create\_kvs\_client](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md#create_kvs_client)
* [**create\_rq\_client](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md#create_rq_client)
* [**get\_rate\_limit\_errors](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md#get_rate_limit_errors)
* [**get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md#get_storage_client_cache_key)

## Methods<!-- -->[**](#Methods)

### [**](#create_dataset_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_storage_client.py#L43)create\_dataset\_client

* **async **create\_dataset\_client**(\*, id, name, alias, configuration): [DatasetClient](https://crawlee.dev/python/python/api/class/DatasetClient.md)

- Overrides [StorageClient.create\_dataset\_client](https://crawlee.dev/python/python/api/class/StorageClient.md#create_dataset_client)

  Create a dataset client.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None
  * ##### optionalkeyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

  #### Returns [DatasetClient](https://crawlee.dev/python/python/api/class/DatasetClient.md)

### [**](#create_kvs_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_storage_client.py#L57)create\_kvs\_client

* **async **create\_kvs\_client**(\*, id, name, alias, configuration): [KeyValueStoreClient](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md)

- Overrides [StorageClient.create\_kvs\_client](https://crawlee.dev/python/python/api/class/StorageClient.md#create_kvs_client)

  Create a key-value store client.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None
  * ##### optionalkeyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

  #### Returns [KeyValueStoreClient](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md)

### [**](#create_rq_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_storage_client.py#L71)create\_rq\_client

* **async **create\_rq\_client**(\*, id, name, alias, configuration): [RequestQueueClient](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)

- Overrides [StorageClient.create\_rq\_client](https://crawlee.dev/python/python/api/class/StorageClient.md#create_rq_client)

  Create a request queue client.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None
  * ##### optionalkeyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

  #### Returns [RequestQueueClient](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)

### [**](#get_rate_limit_errors)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L74)get\_rate\_limit\_errors

* ****get\_rate\_limit\_errors**(): dict\[int, int]

- Inherited from [StorageClient.get\_rate\_limit\_errors](https://crawlee.dev/python/python/api/class/StorageClient.md#get_rate_limit_errors)

  Return statistics about rate limit errors encountered by the HTTP client in storage client.

  ***

  #### Returns dict\[int, int]

### [**](#get_storage_client_cache_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_storage_client.py#L38)get\_storage\_client\_cache\_key

* ****get\_storage\_client\_cache\_key**(configuration): Hashable

- Overrides [StorageClient.get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/StorageClient.md#get_storage_client_cache_key)

  Return a cache key that can differentiate between different storages of this and other clients.

  Can be based on configuration or on the client itself. By default, returns a module and name of the client class.

  ***

  #### Parameters

  * ##### configuration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

  #### Returns Hashable


---

# FinalStatistics<!-- -->

Statistics about a crawler run.

## Index[**](#Index)

### Methods

* [**\_\_str\_\_](https://crawlee.dev/python/python/api/class/FinalStatistics.md#__str__)
* [**to\_dict](https://crawlee.dev/python/python/api/class/FinalStatistics.md#to_dict)
* [**to\_table](https://crawlee.dev/python/python/api/class/FinalStatistics.md#to_table)

### Properties

* [**crawler\_runtime](https://crawlee.dev/python/python/api/class/FinalStatistics.md#crawler_runtime)
* [**request\_avg\_failed\_duration](https://crawlee.dev/python/python/api/class/FinalStatistics.md#request_avg_failed_duration)
* [**request\_avg\_finished\_duration](https://crawlee.dev/python/python/api/class/FinalStatistics.md#request_avg_finished_duration)
* [**request\_total\_duration](https://crawlee.dev/python/python/api/class/FinalStatistics.md#request_total_duration)
* [**requests\_failed](https://crawlee.dev/python/python/api/class/FinalStatistics.md#requests_failed)
* [**requests\_failed\_per\_minute](https://crawlee.dev/python/python/api/class/FinalStatistics.md#requests_failed_per_minute)
* [**requests\_finished](https://crawlee.dev/python/python/api/class/FinalStatistics.md#requests_finished)
* [**requests\_finished\_per\_minute](https://crawlee.dev/python/python/api/class/FinalStatistics.md#requests_finished_per_minute)
* [**requests\_total](https://crawlee.dev/python/python/api/class/FinalStatistics.md#requests_total)
* [**retry\_histogram](https://crawlee.dev/python/python/api/class/FinalStatistics.md#retry_histogram)

## Methods<!-- -->[**](#Methods)

### [**](#__str__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L51)\_\_str\_\_

* ****\_\_str\_\_**(): str

- #### Returns str

### [**](#to_dict)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L47)to\_dict

* ****to\_dict**(): dict\[str, (float | int) | list\[int]]

- #### Returns dict\[str, (float | int) | list\[int]]

### [**](#to_table)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L36)to\_table

* ****to\_table**(): str

- Print out the Final Statistics data as a table.

  ***

  #### Returns str

## Properties<!-- -->[**](#Properties)

### [**](#crawler_runtime)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L34)crawler\_runtime

**crawler\_runtime: timedelta

### [**](#request_avg_failed_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L28)request\_avg\_failed\_duration

**request\_avg\_failed\_duration: timedelta | None

### [**](#request_avg_finished_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L29)request\_avg\_finished\_duration

**request\_avg\_finished\_duration: timedelta | None

### [**](#request_total_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L32)request\_total\_duration

**request\_total\_duration: timedelta

### [**](#requests_failed)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L26)requests\_failed

**requests\_failed: int

### [**](#requests_failed_per_minute)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L31)requests\_failed\_per\_minute

**requests\_failed\_per\_minute: float

### [**](#requests_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L25)requests\_finished

**requests\_finished: int

### [**](#requests_finished_per_minute)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L30)requests\_finished\_per\_minute

**requests\_finished\_per\_minute: float

### [**](#requests_total)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L33)requests\_total

**requests\_total: int

### [**](#retry_histogram)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L27)retry\_histogram

**retry\_histogram: list\[int]


---

# FingerprintGenerator<!-- -->

A class for creating browser fingerprints that mimic browser fingerprints of real users.

### Hierarchy

* *FingerprintGenerator*
  * [BrowserforgeFingerprintGenerator](https://crawlee.dev/python/python/api/class/BrowserforgeFingerprintGenerator.md)

## Index[**](#Index)

### Methods

* [**generate](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md#generate)

## Methods<!-- -->[**](#Methods)

### [**](#generate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_fingerprint_generator.py#L17)generate

* ****generate**(): Fingerprint

- Overrides [FingerprintGenerator.generate](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md#generate)

  Generate browser fingerprints.

  This is experimental feature. Return type is temporarily set to `Fingerprint` from `browserforge`. This is subject to change and most likely it will change to custom `Fingerprint` class defined in this repo later.

  ***

  #### Returns Fingerprint


---

# GetDataKwargs<!-- -->

Keyword arguments for dataset's `get_data` method.

## Index[**](#Index)

### Properties

* [**clean](#clean)
* [**desc](#desc)
* [**fields](#fields)
* [**flatten](#flatten)
* [**limit](#limit)
* [**offset](#offset)
* [**omit](#omit)
* [**skip\_empty](#skip_empty)
* [**skip\_hidden](#skip_hidden)
* [**unwind](#unwind)
* [**view](#view)

## Properties<!-- -->[**](#Properties)

### [**](#clean)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L706)keyword-onlyoptionalclean

**clean: bool

Return only non-empty items and excludes hidden fields. Shortcut for `skip_hidden` and `skip_empty`.

### [**](#desc)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L709)keyword-onlyoptionaldesc

**desc: bool

Set to True to sort results in descending order.

### [**](#fields)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L712)keyword-onlyoptionalfields

**fields: list\[str]

Fields to include in each item. Sorts fields as specified if provided.

### [**](#flatten)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L727)keyword-onlyoptionalflatten

**flatten: list\[str]

Fields to be flattened in returned items.

### [**](#limit)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L703)keyword-onlyoptionallimit

**limit: int | None

The maximum number of items to retrieve. Unlimited if None.

### [**](#offset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L700)keyword-onlyoptionaloffset

**offset: int

Skips the specified number of items at the start.

### [**](#omit)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L715)keyword-onlyoptionalomit

**omit: list\[str]

Fields to exclude from each item.

### [**](#skip_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L721)keyword-onlyoptionalskip\_empty

**skip\_empty: bool

Excludes empty items from the results if True.

### [**](#skip_hidden)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L724)keyword-onlyoptionalskip\_hidden

**skip\_hidden: bool

Excludes fields starting with '#' if True.

### [**](#unwind)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L718)keyword-onlyoptionalunwind

**unwind: list\[str]

Unwinds items by a specified array field, turning each element into a separate item.

### [**](#view)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L730)keyword-onlyoptionalview

**view: str

Specifies the dataset view to be used.


---

# GetKeyValueStoreFromRequestHandlerFunction<!-- -->

A function for accessing a `KeyValueStore`.

It retrieves an instance of a `KeyValueStore` based on its ID or name.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L520)\_\_call\_\_

* ****\_\_call\_\_**(\*, id, name, alias): Coroutine\[None, None, [KeyValueStoreInterface](https://crawlee.dev/python/python/api/class/KeyValueStoreInterface.md)]

- Call dunder method.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None

    The ID of the `KeyValueStore` to get.

  * ##### optionalkeyword-onlyname: str | None = <!-- -->None

    The name of the `KeyValueStore` to get (global scope, named storage).

  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

    The alias of the `KeyValueStore` to get (run scope, unnamed storage).

  #### Returns Coroutine\[None, None, [KeyValueStoreInterface](https://crawlee.dev/python/python/api/class/KeyValueStoreInterface.md)]


---

# GetKeyValueStoreFunction<!-- -->

A function for accessing a `KeyValueStore`.

It retrieves an instance of a `KeyValueStore` based on its ID or name.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L498)\_\_call\_\_

* ****\_\_call\_\_**(\*, id, name, alias): Coroutine\[None, None, [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)]

- Call dunder method.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None

    The ID of the `KeyValueStore` to get.

  * ##### optionalkeyword-onlyname: str | None = <!-- -->None

    The name of the `KeyValueStore` to get (global scope, named storage).

  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

    The alias of the `KeyValueStore` to get (run scope, unnamed storage).

  #### Returns Coroutine\[None, None, [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)]


---

# Glob<!-- -->

Wraps a glob pattern (supports the `*`, `**`, `?` wildcards).

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/Glob.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/globs.py#L14)\_\_init\_\_

* ****\_\_init\_\_**(glob): None

- #### Parameters

  * ##### glob: str

  #### Returns None


---

# GotoOptions<!-- -->

Keyword arguments for Playwright's `Page.goto()` method.

## Index[**](#Index)

### Properties

* [**referer](https://crawlee.dev/python/python/api/class/GotoOptions.md#referer)
* [**wait\_until](https://crawlee.dev/python/python/api/class/GotoOptions.md#wait_until)

## Properties<!-- -->[**](#Properties)

### [**](#referer)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L74)referer

**referer: NotRequired\[str]

Referer header value.

### [**](#wait_until)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L71)wait\_until

**wait\_until: NotRequired\[Literal\[domcontentloaded, load, networkidle, commit]]

When to consider operation succeeded, defaults to 'load' event.


---

# HeaderGenerator<!-- -->

Generate realistic looking or browser-like HTTP headers.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/HeaderGenerator.md#__init__)
* [**get\_common\_headers](https://crawlee.dev/python/python/api/class/HeaderGenerator.md#get_common_headers)
* [**get\_random\_user\_agent\_header](https://crawlee.dev/python/python/api/class/HeaderGenerator.md#get_random_user_agent_header)
* [**get\_sec\_ch\_ua\_headers](https://crawlee.dev/python/python/api/class/HeaderGenerator.md#get_sec_ch_ua_headers)
* [**get\_specific\_headers](https://crawlee.dev/python/python/api/class/HeaderGenerator.md#get_specific_headers)
* [**get\_user\_agent\_header](https://crawlee.dev/python/python/api/class/HeaderGenerator.md#get_user_agent_header)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_header_generator.py#L29)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#get_common_headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_header_generator.py#L48)get\_common\_headers

* ****get\_common\_headers**(): [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

- Get common HTTP headers ("Accept", "Accept-Language").

  We do not modify the "Accept-Encoding", "Connection" and other headers. They should be included and handled by the HTTP client or browser.

  ***

  #### Returns [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#get_random_user_agent_header)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_header_generator.py#L57)get\_random\_user\_agent\_header

* ****get\_random\_user\_agent\_header**(): [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

- Get a random User-Agent header.

  ***

  #### Returns [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#get_sec_ch_ua_headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_header_generator.py#L73)get\_sec\_ch\_ua\_headers

* ****get\_sec\_ch\_ua\_headers**(\*, browser\_type): [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

- Get the sec-ch-ua headers based on the browser type.

  ***

  #### Parameters

  * ##### optionalkeyword-onlybrowser\_type: [SupportedBrowserType](https://crawlee.dev/python/python/api.md#SupportedBrowserType) = <!-- -->'chrome'

  #### Returns [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#get_specific_headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_header_generator.py#L35)get\_specific\_headers

* ****get\_specific\_headers**(header\_names, browser\_type): [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

- Return subset of headers based on the selected `header_names`.

  If no `header_names` are specified, full unfiltered headers are returned.

  ***

  #### Parameters

  * ##### optionalheader\_names: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[str] | None = <!-- -->None
  * ##### optionalbrowser\_type: [SupportedBrowserType](https://crawlee.dev/python/python/api.md#SupportedBrowserType) = <!-- -->'chrome'

  #### Returns [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#get_user_agent_header)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_header_generator.py#L62)get\_user\_agent\_header

* ****get\_user\_agent\_header**(\*, browser\_type): [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

- Get the User-Agent header based on the browser type.

  ***

  #### Parameters

  * ##### optionalkeyword-onlybrowser\_type: [SupportedBrowserType](https://crawlee.dev/python/python/api.md#SupportedBrowserType) = <!-- -->'chrome'

  #### Returns [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)


---

# HeaderGeneratorOptions<!-- -->

Collection of header related attributes that can be used by the fingerprint generator.

## Index[**](#Index)

### Properties

* [**browsers](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md#browsers)
* [**devices](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md#devices)
* [**http\_version](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md#http_version)
* [**locales](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md#locales)
* [**model\_config](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md#model_config)
* [**operating\_systems](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md#operating_systems)
* [**strict](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md#strict)

## Properties<!-- -->[**](#Properties)

### [**](#browsers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L36)browsers

**browsers: list\[[SupportedBrowserType](https://crawlee.dev/python/python/api.md#SupportedBrowserType)] | None

List of BrowserSpecifications to generate the headers for.

### [**](#devices)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L42)devices

**devices: list\[[SupportedDevices](https://crawlee.dev/python/python/api.md#SupportedDevices)] | None

List of devices to generate the headers for.

### [**](#http_version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L50)http\_version

**http\_version: [SupportedHttpVersion](https://crawlee.dev/python/python/api.md#SupportedHttpVersion) | None

HTTP version to be used for header generation (the headers differ depending on the version).

### [**](#locales)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L45)locales

**locales: list\[str] | None

List of at most 10 languages to include in the \[Accept-Language] (<https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language>) request header in the language format accepted by that header, for example `en`, `en-US` or `de`.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L34)model\_config

**model\_config: Undefined

### [**](#operating_systems)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L39)operating\_systems

**operating\_systems: list\[[SupportedOperatingSystems](https://crawlee.dev/python/python/api.md#SupportedOperatingSystems)] | None

List of operating systems to generate the headers for.

### [**](#strict)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L53)strict

**strict: bool | None

If true, the generator will throw an error if it cannot generate headers based on the input.


---

# HttpClient<!-- -->

An abstract base class for HTTP clients used in crawlers (`BasicCrawler` subclasses).

### Hierarchy

* *HttpClient*

  * [PlaywrightHttpClient](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md)
  * [CurlImpersonateHttpClient](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md)
  * [ImpitHttpClient](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md)
  * [HttpxHttpClient](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md)

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__init__)
* [**cleanup](https://crawlee.dev/python/python/api/class/HttpClient.md#cleanup)
* [**crawl](https://crawlee.dev/python/python/api/class/HttpClient.md#crawl)
* [**send\_request](https://crawlee.dev/python/python/api/class/HttpClient.md#send_request)
* [**stream](https://crawlee.dev/python/python/api/class/HttpClient.md#stream)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/HttpClient.md#active)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L201)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

- Initialize the client when entering the context manager.

  ***

  #### Returns [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L213)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, traceback): None

- Deinitialize the client and clean up resources when exiting the context manager.

  ***

  #### Parameters

  * ##### exc\_type: BaseException | None
  * ##### exc\_value: BaseException | None
  * ##### traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L79)\_\_init\_\_

* ****\_\_init\_\_**(\*, persist\_cookies\_per\_session): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypersist\_cookies\_per\_session: bool = <!-- -->True

    Whether to persist cookies per HTTP session.

  #### Returns None

### [**](#cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L193)cleanup

* **async **cleanup**(): None

- Overrides [HttpClient.cleanup](https://crawlee.dev/python/python/api/class/HttpClient.md#cleanup)

  Clean up resources used by the client.

  This method is called when the client is no longer needed and should be overridden in subclasses to perform any necessary cleanup such as closing connections, releasing file handles, or other resource deallocation.

  ***

  #### Returns None

### [**](#crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L100)crawl

* **async **crawl**(request, \*, session, proxy\_info, statistics, timeout): [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

- Overrides [HttpClient.crawl](https://crawlee.dev/python/python/api/class/HttpClient.md#crawl)

  Perform the crawling for a given request.

  This method is called from `crawler.run()`.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to be crawled.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlystatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md) | None = <!-- -->None

    The statistics object to register status codes.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

  The result of the crawling.

### [**](#send_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L128)send\_request

* **async **send\_request**(url, \*, method, headers, payload, session, proxy\_info, timeout): [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

- Overrides [HttpClient.send\_request](https://crawlee.dev/python/python/api/class/HttpClient.md#send_request)

  Send an HTTP request via the client.

  This method is called from `context.send_request()` helper.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  The HTTP response received from the server.

### [**](#stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L160)stream

* ****stream**(url, \*, method, headers, payload, session, proxy\_info, timeout): AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

- Overrides [HttpClient.stream](https://crawlee.dev/python/python/api/class/HttpClient.md#stream)

  Stream an HTTP request via the client.

  This method should be used for downloading potentially large data where you need to process the response body in chunks rather than loading it entirely into memory.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    The maximum time to wait for establishing the connection.

  #### Returns AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

  An async context manager yielding the HTTP response with streaming capabilities.

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L95)active

**active: bool

Indicate whether the context is active.


---

# HttpClientStatusCodeError<!-- -->

Raised when the response status code indicates an client error.

### Hierarchy

* [HttpStatusCodeError](https://crawlee.dev/python/python/api/class/HttpStatusCodeError.md)
  * *HttpClientStatusCodeError*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpClientStatusCodeError.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/errors.py#L64)\_\_init\_\_

* ****\_\_init\_\_**(message, status\_code): None

- Inherited from [HttpStatusCodeError.\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpStatusCodeError.md#__init__)

  #### Parameters

  * ##### message: str
  * ##### status\_code: int

  #### Returns None


---

# HttpCrawler<!-- -->

Specific version of generic `AbstractHttpCrawler`.

It uses a dummy parser that simply returns the HTTP response body as-is. Use this only if you know what you are doing. In most cases, using an HTML parser would be more beneficial. For such scenarios, consider using `BeautifulSoupCrawler`, `ParselCrawler`, or writing your own subclass of `AbstractHttpCrawler`.

### Usage

```
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext

crawler = HttpCrawler()

# Define the default request handler, which will be called for every request.
@crawler.router.default_handler
async def request_handler(context: HttpCrawlingContext) -> None:
    context.log.info(f'Processing {context.request.url} ...')

    # Extract data from the page.
    data = {
        'url': context.request.url,
        'response': (await context.http_response.read()).decode()[:100],
    }

    # Push the extracted data to the default dataset.
    await context.push_data(data)

await crawler.run(['https://crawlee.dev/'])
```

### Hierarchy

* [AbstractHttpCrawler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md)
  * *HttpCrawler*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpCrawler.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/HttpCrawler.md#add_requests)
* [**create\_parsed\_http\_crawler\_class](https://crawlee.dev/python/python/api/class/HttpCrawler.md#create_parsed_http_crawler_class)
* [**error\_handler](https://crawlee.dev/python/python/api/class/HttpCrawler.md#error_handler)
* [**export\_data](https://crawlee.dev/python/python/api/class/HttpCrawler.md#export_data)
* [**failed\_request\_handler](https://crawlee.dev/python/python/api/class/HttpCrawler.md#failed_request_handler)
* [**get\_data](https://crawlee.dev/python/python/api/class/HttpCrawler.md#get_data)
* [**get\_dataset](https://crawlee.dev/python/python/api/class/HttpCrawler.md#get_dataset)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/HttpCrawler.md#get_key_value_store)
* [**get\_request\_manager](https://crawlee.dev/python/python/api/class/HttpCrawler.md#get_request_manager)
* [**on\_skipped\_request](https://crawlee.dev/python/python/api/class/HttpCrawler.md#on_skipped_request)
* [**post\_navigation\_hook](https://crawlee.dev/python/python/api/class/HttpCrawler.md#post_navigation_hook)
* [**pre\_navigation\_hook](https://crawlee.dev/python/python/api/class/HttpCrawler.md#pre_navigation_hook)
* [**run](https://crawlee.dev/python/python/api/class/HttpCrawler.md#run)
* [**stop](https://crawlee.dev/python/python/api/class/HttpCrawler.md#stop)
* [**use\_state](https://crawlee.dev/python/python/api/class/HttpCrawler.md#use_state)

### Properties

* [**log](https://crawlee.dev/python/python/api/class/HttpCrawler.md#log)
* [**router](https://crawlee.dev/python/python/api/class/HttpCrawler.md#router)
* [**statistics](https://crawlee.dev/python/python/api/class/HttpCrawler.md#statistics)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_http/_http_crawler.py#L49)\_\_init\_\_

* ****\_\_init\_\_**(\*, request\_handler, statistics, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, concurrency\_settings, request\_handler\_timeout, abort\_on\_error, configure\_logging, statistics\_log\_format, keep\_alive, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id): None

- Overrides [AbstractHttpCrawler.\_\_init\_\_](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### keyword-onlyoptionalrequest\_handler: NotRequired\[Callable\[\[TCrawlingContext], Awaitable\[None]]]

    A callable responsible for handling requests.

  * ##### keyword-onlyoptionalstatistics: NotRequired\[Statistics\[TStatisticsState]]

    A custom `Statistics` instance, allowing the use of non-default configuration.

  * ##### keyword-onlyoptionalconfiguration: NotRequired\[Configuration]

    The `Configuration` instance. Some of its properties are used as defaults for the crawler.

  * ##### keyword-onlyoptionalevent\_manager: NotRequired\[EventManager]

    The event manager for managing events for the crawler and all its components.

  * ##### keyword-onlyoptionalstorage\_client: NotRequired\[StorageClient]

    The storage client for managing storages for the crawler and all its components.

  * ##### keyword-onlyoptionalrequest\_manager: NotRequired\[RequestManager]

    Manager of requests that should be processed by the crawler.

  * ##### keyword-onlyoptionalsession\_pool: NotRequired\[SessionPool]

    A custom `SessionPool` instance, allowing the use of non-default configuration.

  * ##### keyword-onlyoptionalproxy\_configuration: NotRequired\[ProxyConfiguration]

    HTTP proxy configuration used when making requests.

  * ##### keyword-onlyoptionalhttp\_client: NotRequired\[HttpClient]

    HTTP client used by `BasicCrawlingContext.send_request` method.

  * ##### keyword-onlyoptionalmax\_request\_retries: NotRequired\[int]

    Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.).

    This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

  * ##### keyword-onlyoptionalmax\_requests\_per\_crawl: NotRequired\[int | None]

    Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value.

  * ##### keyword-onlyoptionalmax\_session\_rotations: NotRequired\[int]

    Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request.

    The session rotations are not counted towards the `max_request_retries` limit.

  * ##### keyword-onlyoptionalmax\_crawl\_depth: NotRequired\[int | None]

    Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

  * ##### keyword-onlyoptionaluse\_session\_pool: NotRequired\[bool]

    Enable the use of a session pool for managing sessions during crawling.

  * ##### keyword-onlyoptionalretry\_on\_blocked: NotRequired\[bool]

    If True, the crawler attempts to bypass bot protections automatically.

  * ##### keyword-onlyoptionalconcurrency\_settings: NotRequired\[ConcurrencySettings]

    Settings to fine-tune concurrency levels.

  * ##### keyword-onlyoptionalrequest\_handler\_timeout: NotRequired\[timedelta]

    Maximum duration allowed for a single request handler to run.

  * ##### keyword-onlyoptionalabort\_on\_error: NotRequired\[bool]

    If True, the crawler stops immediately when any request handler error occurs.

  * ##### keyword-onlyoptionalconfigure\_logging: NotRequired\[bool]

    If True, the crawler will set up logging infrastructure automatically.

  * ##### keyword-onlyoptionalstatistics\_log\_format: NotRequired\[Literal\['table', 'inline']]

    If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

  * ##### keyword-onlyoptionalkeep\_alive: NotRequired\[bool]

    Flag that can keep crawler running even when there are no requests in queue.

  * ##### keyword-onlyoptionaladditional\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

    Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

  * ##### keyword-onlyoptionalignore\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

    HTTP status codes that are typically considered errors but should be treated as successful responses.

  * ##### keyword-onlyoptionalrespect\_robots\_txt\_file: NotRequired\[bool]

    If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`.

  * ##### keyword-onlyoptionalstatus\_message\_logging\_interval: NotRequired\[timedelta]

    Interval for logging the crawler status messages.

  * ##### keyword-onlyoptionalstatus\_message\_callback: NotRequired\[ Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]] ]

    Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

  * ##### keyword-onlyoptionalid: NotRequired\[int]

    Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

  #### Returns None

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L804)add\_requests

* **async **add\_requests**(requests, \*, forefront, batch\_size, wait\_time\_between\_batches, wait\_for\_all\_requests\_to\_be\_added, wait\_for\_all\_requests\_to\_be\_added\_timeout): None

- Inherited from [BasicCrawler.add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawler.md#add_requests)

  Add requests to the underlying request manager in batches.

  ***

  #### Parameters

  * ##### requests: Sequence\[str | Request]

    A list of requests to add to the queue.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    If True, add requests to the forefront of the queue.

  * ##### optionalkeyword-onlybatch\_size: int = <!-- -->1000

    The number of requests to add in one batch.

  * ##### optionalkeyword-onlywait\_time\_between\_batches: timedelta = <!-- -->timedelta(0)

    Time to wait between adding batches.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added: bool = <!-- -->False

    If True, wait for all requests to be added before returning.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added\_timeout: timedelta | None = <!-- -->None

    Timeout for waiting for all requests to be added.

  #### Returns None

### [**](#create_parsed_http_crawler_class)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_crawler.py#L93)create\_parsed\_http\_crawler\_class

* ****create\_parsed\_http\_crawler\_class**(static\_parser): type\[AbstractHttpCrawler\[ParsedHttpCrawlingContext\[TParseResult], TParseResult, TSelectResult]]

- Inherited from [AbstractHttpCrawler.create\_parsed\_http\_crawler\_class](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#create_parsed_http_crawler_class)

  Create a specific version of `AbstractHttpCrawler` class.

  This is a convenience factory method for creating a specific `AbstractHttpCrawler` subclass. While `AbstractHttpCrawler` allows its two generic parameters to be independent, this method simplifies cases where `TParseResult` is used for both generic parameters.

  ***

  #### Parameters

  * ##### static\_parser: AbstractHttpParser\[TParseResult, TSelectResult]

  #### Returns type\[AbstractHttpCrawler\[ParsedHttpCrawlingContext\[TParseResult], TParseResult, TSelectResult]]

### [**](#error_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L655)error\_handler

* ****error\_handler**(handler): ErrorHandler\[TCrawlingContext]

- Inherited from [BasicCrawler.error\_handler](https://crawlee.dev/python/python/api/class/BasicCrawler.md#error_handler)

  Register a function to handle errors occurring in request handlers.

  The error handler is invoked after a request handler error occurs and before a retry attempt.

  ***

  #### Parameters

  * ##### handler: ErrorHandler\[TCrawlingContext | BasicCrawlingContext]

  #### Returns ErrorHandler\[TCrawlingContext]

### [**](#export_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L893)export\_data

* **async **export\_data**(path, dataset\_id, dataset\_name, dataset\_alias, additional\_kwargs): None

- Inherited from [BasicCrawler.export\_data](https://crawlee.dev/python/python/api/class/BasicCrawler.md#export_data)

  Export all items from a Dataset to a JSON or CSV file.

  This method simplifies the process of exporting data collected during crawling. It automatically determines the export format based on the file extension (`.json` or `.csv`) and handles the conversion of `Dataset` items to the appropriate format.

  ***

  #### Parameters

  * ##### path: str | Path

    The destination file path. Must end with '.json' or '.csv'.

  * ##### optionaldataset\_id: str | None = <!-- -->None

    The ID of the Dataset to export from.

  * ##### optionaldataset\_name: str | None = <!-- -->None

    The name of the Dataset to export from (global scope, named storage).

  * ##### optionaldataset\_alias: str | None = <!-- -->None

    The alias of the Dataset to export from (run scope, unnamed storage).

  * ##### additional\_kwargs: Unpack\[ExportDataJsonKwargs | ExportDataCsvKwargs]

    Extra keyword arguments forwarded to the JSON/CSV exporter depending on the file format.

  #### Returns None

### [**](#failed_request_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L665)failed\_request\_handler

* ****failed\_request\_handler**(handler): FailedRequestHandler\[TCrawlingContext]

- Inherited from [BasicCrawler.failed\_request\_handler](https://crawlee.dev/python/python/api/class/BasicCrawler.md#failed_request_handler)

  Register a function to handle requests that exceed the maximum retry limit.

  The failed request handler is invoked when a request has failed all retry attempts.

  ***

  #### Parameters

  * ##### handler: FailedRequestHandler\[TCrawlingContext | BasicCrawlingContext]

  #### Returns FailedRequestHandler\[TCrawlingContext]

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L863)get\_data

* **async **get\_data**(dataset\_id, dataset\_name, dataset\_alias, kwargs): [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

- Inherited from [BasicCrawler.get\_data](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_data)

  Retrieve data from a `Dataset`.

  This helper method simplifies the process of retrieving data from a `Dataset`. It opens the specified one and then retrieves the data based on the provided parameters.

  ***

  #### Parameters

  * ##### optionaldataset\_id: str | None = <!-- -->None

    The ID of the `Dataset`.

  * ##### optionaldataset\_name: str | None = <!-- -->None

    The name of the `Dataset` (global scope, named storage).

  * ##### optionaldataset\_alias: str | None = <!-- -->None

    The alias of the `Dataset` (run scope, unnamed storage).

  * ##### kwargs: Unpack\[GetDataKwargs]

    Keyword arguments to be passed to the `Dataset.get_data()` method.

  #### Returns [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

  The retrieved data.

### [**](#get_dataset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L623)get\_dataset

* **async **get\_dataset**(\*, id, name, alias): [Dataset](https://crawlee.dev/python/python/api/class/Dataset.md)

- Inherited from [BasicCrawler.get\_dataset](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_dataset)

  Return the `Dataset` with the given ID or name. If none is provided, return the default one.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

  #### Returns [Dataset](https://crawlee.dev/python/python/api/class/Dataset.md)

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L639)get\_key\_value\_store

* **async **get\_key\_value\_store**(\*, id, name, alias): [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)

- Inherited from [BasicCrawler.get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_key_value_store)

  Return the `KeyValueStore` with the given ID or name. If none is provided, return the default KVS.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

  #### Returns [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)

### [**](#get_request_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L613)get\_request\_manager

* **async **get\_request\_manager**(): [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

- Inherited from [BasicCrawler.get\_request\_manager](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_request_manager)

  Return the configured request manager. If none is configured, open and return the default request queue.

  ***

  #### Returns [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

### [**](#on_skipped_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L675)on\_skipped\_request

* ****on\_skipped\_request**(callback): [SkippedRequestCallback](https://crawlee.dev/python/python/api.md#SkippedRequestCallback)

- Inherited from [BasicCrawler.on\_skipped\_request](https://crawlee.dev/python/python/api/class/BasicCrawler.md#on_skipped_request)

  Register a function to handle skipped requests.

  The skipped request handler is invoked when a request is skipped due to a collision or other reasons.

  ***

  #### Parameters

  * ##### callback: [SkippedRequestCallback](https://crawlee.dev/python/python/api.md#SkippedRequestCallback)

  #### Returns [SkippedRequestCallback](https://crawlee.dev/python/python/api.md#SkippedRequestCallback)

### [**](#post_navigation_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_crawler.py#L337)post\_navigation\_hook

* ****post\_navigation\_hook**(hook): None

- Inherited from [AbstractHttpCrawler.post\_navigation\_hook](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#post_navigation_hook)

  Register a hook to be called after each navigation.

  ***

  #### Parameters

  * ##### hook: Callable\[\[HttpCrawlingContext], Awaitable\[None]]

    A coroutine function to be called after each navigation.

  #### Returns None

### [**](#pre_navigation_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_crawler.py#L329)pre\_navigation\_hook

* ****pre\_navigation\_hook**(hook): None

- Inherited from [AbstractHttpCrawler.pre\_navigation\_hook](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#pre_navigation_hook)

  Register a hook to be called before each navigation.

  ***

  #### Parameters

  * ##### hook: Callable\[\[BasicCrawlingContext], Awaitable\[None]]

    A coroutine function to be called before each navigation.

  #### Returns None

### [**](#run)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L683)run

* **async **run**(requests, \*, purge\_request\_queue): [FinalStatistics](https://crawlee.dev/python/python/api/class/FinalStatistics.md)

- Inherited from [BasicCrawler.run](https://crawlee.dev/python/python/api/class/BasicCrawler.md#run)

  Run the crawler until all requests are processed.

  ***

  #### Parameters

  * ##### optionalrequests: Sequence\[str | Request] | None = <!-- -->None

    The requests to be enqueued before the crawler starts.

  * ##### optionalkeyword-onlypurge\_request\_queue: bool = <!-- -->True

    If this is `True` and the crawler is not being run for the first time, the default request queue will be purged.

  #### Returns [FinalStatistics](https://crawlee.dev/python/python/api/class/FinalStatistics.md)

### [**](#stop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L535)stop

* ****stop**(reason): None

- Inherited from [BasicCrawler.stop](https://crawlee.dev/python/python/api/class/BasicCrawler.md#stop)

  Set flag to stop crawler.

  This stops current crawler run regardless of whether all requests were finished.

  ***

  #### Parameters

  * ##### optionalreason: str = <!-- -->'Stop was called externally.'

    Reason for stopping that will be used in logs.

  #### Returns None

### [**](#use_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L852)use\_state

* **async **use\_state**(default\_value): dict\[str, JsonSerializable]

- Inherited from [BasicCrawler.use\_state](https://crawlee.dev/python/python/api/class/BasicCrawler.md#use_state)

  #### Parameters

  * ##### optionaldefault\_value: dict\[str, JsonSerializable] | None = <!-- -->None

  #### Returns dict\[str, JsonSerializable]

## Properties<!-- -->[**](#Properties)

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L511)log

**log: logging.Logger

Inherited from [BasicCrawler.log](https://crawlee.dev/python/python/api/class/BasicCrawler.md#log)

The logger used by the crawler.

### [**](#router)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L516)router

**router: Router\[TCrawlingContext]

Inherited from [BasicCrawler.router](https://crawlee.dev/python/python/api/class/BasicCrawler.md#router)

Overrides [BasicCrawler.router](https://crawlee.dev/python/python/api/class/BasicCrawler.md#router)

The `Router` used to handle each individual crawling request.

### [**](#statistics)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L531)statistics

**statistics: Statistics\[TStatisticsState]

Inherited from [BasicCrawler.statistics](https://crawlee.dev/python/python/api/class/BasicCrawler.md#statistics)

Statistics about the current (or last) crawler run.


---

# HttpCrawlerOptions<!-- -->

Arguments for the `AbstractHttpCrawler` constructor.

It is intended for typing forwarded `__init__` arguments in the subclasses.

### Hierarchy

* [BasicCrawlerOptions](https://crawlee.dev/python/python/api/class/BasicCrawlerOptions.md)
  * *HttpCrawlerOptions*

## Index[**](#Index)

### Properties

* [**abort\_on\_error](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#abort_on_error)
* [**additional\_http\_error\_status\_codes](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#additional_http_error_status_codes)
* [**concurrency\_settings](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#concurrency_settings)
* [**configuration](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#configuration)
* [**configure\_logging](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#configure_logging)
* [**event\_manager](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#event_manager)
* [**http\_client](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#http_client)
* [**id](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#id)
* [**ignore\_http\_error\_status\_codes](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#ignore_http_error_status_codes)
* [**keep\_alive](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#keep_alive)
* [**max\_crawl\_depth](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#max_crawl_depth)
* [**max\_request\_retries](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#max_request_retries)
* [**max\_requests\_per\_crawl](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#max_requests_per_crawl)
* [**max\_session\_rotations](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#max_session_rotations)
* [**navigation\_timeout](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#navigation_timeout)
* [**proxy\_configuration](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#proxy_configuration)
* [**request\_handler](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#request_handler)
* [**request\_handler\_timeout](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#request_handler_timeout)
* [**request\_manager](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#request_manager)
* [**respect\_robots\_txt\_file](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#respect_robots_txt_file)
* [**retry\_on\_blocked](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#retry_on_blocked)
* [**session\_pool](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#session_pool)
* [**statistics](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#statistics)
* [**statistics\_log\_format](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#statistics_log_format)
* [**status\_message\_callback](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#status_message_callback)
* [**status\_message\_logging\_interval](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#status_message_logging_interval)
* [**storage\_client](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#storage_client)
* [**use\_session\_pool](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md#use_session_pool)

## Properties<!-- -->[**](#Properties)

### [**](#abort_on_error)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L175)abort\_on\_error

**abort\_on\_error: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.abort\_on\_error

If True, the crawler stops immediately when any request handler error occurs.

### [**](#additional_http_error_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L189)additional\_http\_error\_status\_codes

**additional\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

Inherited from \_BasicCrawlerOptions.additional\_http\_error\_status\_codes

Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

### [**](#concurrency_settings)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L169)concurrency\_settings

**concurrency\_settings: NotRequired\[ConcurrencySettings]

Inherited from \_BasicCrawlerOptions.concurrency\_settings

Settings to fine-tune concurrency levels.

### [**](#configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L116)configuration

**configuration: NotRequired\[Configuration]

Inherited from \_BasicCrawlerOptions.configuration

The `Configuration` instance. Some of its properties are used as defaults for the crawler.

### [**](#configure_logging)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L178)configure\_logging

**configure\_logging: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.configure\_logging

If True, the crawler will set up logging infrastructure automatically.

### [**](#event_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L119)event\_manager

**event\_manager: NotRequired\[EventManager]

Inherited from \_BasicCrawlerOptions.event\_manager

The event manager for managing events for the crawler and all its components.

### [**](#http_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L134)http\_client

**http\_client: NotRequired\[HttpClient]

Inherited from \_BasicCrawlerOptions.http\_client

HTTP client used by `BasicCrawlingContext.send_request` method.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L216)id

**id: NotRequired\[int]

Inherited from \_BasicCrawlerOptions.id

Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

### [**](#ignore_http_error_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L192)ignore\_http\_error\_status\_codes

**ignore\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

Inherited from \_BasicCrawlerOptions.ignore\_http\_error\_status\_codes

HTTP status codes that are typically considered errors but should be treated as successful responses.

### [**](#keep_alive)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L186)keep\_alive

**keep\_alive: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.keep\_alive

Flag that can keep crawler running even when there are no requests in queue.

### [**](#max_crawl_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L156)max\_crawl\_depth

**max\_crawl\_depth: NotRequired\[int | None]

Inherited from \_BasicCrawlerOptions.max\_crawl\_depth

Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

### [**](#max_request_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L137)max\_request\_retries

**max\_request\_retries: NotRequired\[int]

Inherited from \_BasicCrawlerOptions.max\_request\_retries

Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.).

This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

### [**](#max_requests_per_crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L144)max\_requests\_per\_crawl

**max\_requests\_per\_crawl: NotRequired\[int | None]

Inherited from \_BasicCrawlerOptions.max\_requests\_per\_crawl

Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value.

### [**](#max_session_rotations)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L149)max\_session\_rotations

**max\_session\_rotations: NotRequired\[int]

Inherited from \_BasicCrawlerOptions.max\_session\_rotations

Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request.

The session rotations are not counted towards the `max_request_retries` limit.

### [**](#navigation_timeout)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_crawler.py#L46)navigation\_timeout

**navigation\_timeout: NotRequired\[timedelta | None]

Timeout for the HTTP request.

### [**](#proxy_configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L131)proxy\_configuration

**proxy\_configuration: NotRequired\[ProxyConfiguration]

Inherited from \_BasicCrawlerOptions.proxy\_configuration

HTTP proxy configuration used when making requests.

### [**](#request_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L224)request\_handler

**request\_handler: NotRequired\[Callable\[\[TCrawlingContext], Awaitable\[None]]]

Inherited from [\_BasicCrawlerOptionsGeneric.request\_handler](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptionsGeneric.md#request_handler)

A callable responsible for handling requests.

### [**](#request_handler_timeout)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L172)request\_handler\_timeout

**request\_handler\_timeout: NotRequired\[timedelta]

Inherited from \_BasicCrawlerOptions.request\_handler\_timeout

Maximum duration allowed for a single request handler to run.

### [**](#request_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L125)request\_manager

**request\_manager: NotRequired\[RequestManager]

Inherited from \_BasicCrawlerOptions.request\_manager

Manager of requests that should be processed by the crawler.

### [**](#respect_robots_txt_file)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L203)respect\_robots\_txt\_file

**respect\_robots\_txt\_file: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.respect\_robots\_txt\_file

If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`.

### [**](#retry_on_blocked)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L166)retry\_on\_blocked

**retry\_on\_blocked: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.retry\_on\_blocked

If True, the crawler attempts to bypass bot protections automatically.

### [**](#session_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L128)session\_pool

**session\_pool: NotRequired\[SessionPool]

Inherited from \_BasicCrawlerOptions.session\_pool

A custom `SessionPool` instance, allowing the use of non-default configuration.

### [**](#statistics)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L231)statistics

**statistics: NotRequired\[Statistics\[TStatisticsState]]

Inherited from [\_BasicCrawlerOptionsGeneric.statistics](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptionsGeneric.md#statistics)

A custom `Statistics` instance, allowing the use of non-default configuration.

### [**](#statistics_log_format)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L181)statistics\_log\_format

**statistics\_log\_format: NotRequired\[Literal\['table', 'inline']]

Inherited from \_BasicCrawlerOptions.statistics\_log\_format

If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

### [**](#status_message_callback)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L210)status\_message\_callback

**status\_message\_callback: NotRequired\[ Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]] ]

Inherited from \_BasicCrawlerOptions.status\_message\_callback

Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

### [**](#status_message_logging_interval)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L207)status\_message\_logging\_interval

**status\_message\_logging\_interval: NotRequired\[timedelta]

Inherited from \_BasicCrawlerOptions.status\_message\_logging\_interval

Interval for logging the crawler status messages.

### [**](#storage_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L122)storage\_client

**storage\_client: NotRequired\[StorageClient]

Inherited from \_BasicCrawlerOptions.storage\_client

The storage client for managing storages for the crawler and all its components.

### [**](#use_session_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L163)use\_session\_pool

**use\_session\_pool: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.use\_session\_pool

Enable the use of a session pool for managing sessions during crawling.


---

# HttpCrawlingContext<!-- -->

The crawling context used by the `AbstractHttpCrawler`.

### Hierarchy

* [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

* [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)

  * *HttpCrawlingContext*

    * [AdaptivePlaywrightPostNavCrawlingContext](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md)
    * [ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#create_modified_copy)
* [**from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#from_basic_crawling_context)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#add_requests)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#get_key_value_store)
* [**http\_response](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#http_response)
* [**log](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#log)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#request)
* [**send\_request](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#use_state)

## Methods<!-- -->[**](#Methods)

### [**](#__hash__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L674)\_\_hash\_\_

* ****\_\_hash\_\_**(): int

- Inherited from [BasicCrawlingContext.\_\_hash\_\_](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#__hash__)

  Return hash of the context. Each context is considered unique.

  ***

  #### Returns int

### [**](#create_modified_copy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L678)create\_modified\_copy

* ****create\_modified\_copy**(push\_data, add\_requests, get\_key\_value\_store): Self

- Inherited from [BasicCrawlingContext.create\_modified\_copy](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#create_modified_copy)

  Create a modified copy of the crawling context with specified changes.

  ***

  #### Parameters

  * ##### optionalpush\_data: PushDataFunction | None = <!-- -->None
  * ##### optionaladd\_requests: AddRequestsFunction | None = <!-- -->None
  * ##### optionalget\_key\_value\_store: GetKeyValueStoreFromRequestHandlerFunction | None = <!-- -->None

  #### Returns Self

### [**](#from_basic_crawling_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L22)from\_basic\_crawling\_context

* ****from\_basic\_crawling\_context**(context, http\_response): Self

- Initialize a new instance from an existing `BasicCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)
  * ##### http\_response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  #### Returns Self

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L27)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Overrides [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

  Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

## Properties<!-- -->[**](#Properties)

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L652)add\_requests

**add\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md)

Inherited from [BasicCrawlingContext.add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#add_requests)

Add requests crawling context helper function.

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L661)get\_key\_value\_store

**get\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md)

Inherited from [BasicCrawlingContext.get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_key_value_store)

Get key-value store crawling context helper function.

### [**](#http_response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L70)http\_response

**http\_response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

Inherited from [HttpCrawlingResult.http\_response](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md#http_response)

The HTTP response received from the server.

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L664)log

**log: logging.Logger

Inherited from [BasicCrawlingContext.log](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#log)

Logger instance.

### [**](#proxy_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L646)proxy\_info

**proxy\_info: ProxyInfo | None

Inherited from [BasicCrawlingContext.proxy\_info](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#proxy_info)

Proxy information for the current page being processed.

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L655)push\_data

**push\_data: [PushDataFunction](https://crawlee.dev/python/python/api/class/PushDataFunction.md)

Inherited from [BasicCrawlingContext.push\_data](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#push_data)

Push data crawling context helper function.

### [**](#register_deferred_cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L667)register\_deferred\_cleanup

**register\_deferred\_cleanup: Callable\[\[DeferredCleanupCallback], None]

Inherited from [BasicCrawlingContext.register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#register_deferred_cleanup)

Register an async callback to be called after request processing completes (including error handlers).

### [**](#request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L640)request

**request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

Inherited from [BasicCrawlingContext.request](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#request)

Request object for the current page being processed.

### [**](#send_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L649)send\_request

**send\_request: [SendRequestFunction](https://crawlee.dev/python/python/api/class/SendRequestFunction.md)

Inherited from [BasicCrawlingContext.send\_request](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#send_request)

Send request crawling context helper function.

### [**](#session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L643)session

**session: Session | None

Inherited from [BasicCrawlingContext.session](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#session)

Session object for the current page being processed.

### [**](#use_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L658)use\_state

**use\_state: [UseStateFunction](https://crawlee.dev/python/python/api/class/UseStateFunction.md)

Inherited from [BasicCrawlingContext.use\_state](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#use_state)

Use state crawling context helper function.


---

# HttpCrawlingResult<!-- -->

Result of an HTTP-only crawl.

Mainly for the purpose of composing specific crawling contexts (e.g. `BeautifulSoupCrawlingContext`, `ParselCrawlingContext`, ...).

### Hierarchy

* *HttpCrawlingResult*
  * [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md)

## Index[**](#Index)

### Properties

* [**http\_response](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md#http_response)

## Properties<!-- -->[**](#Properties)

### [**](#http_response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L70)http\_response

**http\_response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

The HTTP response received from the server.


---

# HttpHeaders<!-- -->

A dictionary-like object representing HTTP headers.

## Index[**](#Index)

### Methods

* [**\_\_delitem\_\_](https://crawlee.dev/python/python/api/class/HttpHeaders.md#__delitem__)
* [**\_\_getitem\_\_](https://crawlee.dev/python/python/api/class/HttpHeaders.md#__getitem__)
* [**\_\_iter\_\_](https://crawlee.dev/python/python/api/class/HttpHeaders.md#__iter__)
* [**\_\_len\_\_](https://crawlee.dev/python/python/api/class/HttpHeaders.md#__len__)
* [**\_\_or\_\_](https://crawlee.dev/python/python/api/class/HttpHeaders.md#__or__)
* [**\_\_ror\_\_](https://crawlee.dev/python/python/api/class/HttpHeaders.md#__ror__)
* [**\_\_setitem\_\_](https://crawlee.dev/python/python/api/class/HttpHeaders.md#__setitem__)

### Properties

* [**model\_config](https://crawlee.dev/python/python/api/class/HttpHeaders.md#model_config)

## Methods<!-- -->[**](#Methods)

### [**](#__delitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L84)\_\_delitem\_\_

* ****\_\_delitem\_\_**(key): None

- #### Parameters

  * ##### key: str

  #### Returns None

### [**](#__getitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L78)\_\_getitem\_\_

* ****\_\_getitem\_\_**(key): str

- #### Parameters

  * ##### key: str

  #### Returns str

### [**](#__iter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L97)\_\_iter\_\_

* ****\_\_iter\_\_**(): Iterator\[str]

- #### Returns Iterator\[str]

### [**](#__len__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L100)\_\_len\_\_

* ****\_\_len\_\_**(): int

- #### Returns int

### [**](#__or__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L87)\_\_or\_\_

* ****\_\_or\_\_**(other): [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

- Return a new instance of `HttpHeaders` combining this one with another one.

  ***

  #### Parameters

  * ##### other: [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

  #### Returns [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#__ror__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L92)\_\_ror\_\_

* ****\_\_ror\_\_**(other): [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

- Support reversed | operation (other | self).

  ***

  #### Parameters

  * ##### other: [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

  #### Returns [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#__setitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L81)\_\_setitem\_\_

* ****\_\_setitem\_\_**(key, value): None

- #### Parameters

  * ##### key: str
  * ##### value: str

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L66)model\_config

**model\_config: Undefined


---

# HttpResponse<!-- -->

Define the interface that any HTTP response object must implement.

## Index[**](#Index)

### Methods

* [**read](https://crawlee.dev/python/python/api/class/HttpResponse.md#read)
* [**read\_stream](https://crawlee.dev/python/python/api/class/HttpResponse.md#read_stream)

### Properties

* [**headers](https://crawlee.dev/python/python/api/class/HttpResponse.md#headers)
* [**http\_version](https://crawlee.dev/python/python/api/class/HttpResponse.md#http_version)
* [**status\_code](https://crawlee.dev/python/python/api/class/HttpResponse.md#status_code)

## Methods<!-- -->[**](#Methods)

### [**](#read)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L38)read

* **async **read**(): [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

- Read the entire content of the response body.

  This method loads the complete response body into memory at once. It should be used for responses received from regular HTTP requests (via `send_request` or `crawl` methods).

  ***

  #### Returns [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

### [**](#read_stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L48)read\_stream

* ****read\_stream**(): AsyncIterator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)]

- Iterate over the content of the response body in chunks.

  This method should be used for responses received from the `stream` method to process large response bodies without loading them entirely into memory. It allows for efficient processing of potentially large data by yielding chunks sequentially.

  ***

  #### Returns AsyncIterator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)]

## Properties<!-- -->[**](#Properties)

### [**](#headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L35)headers

**headers: [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

The HTTP headers received in the response.

### [**](#http_version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L27)http\_version

**http\_version: str

The HTTP version used in the response.

### [**](#status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L31)status\_code

**status\_code: int

The HTTP status code received from the server.


---

# HttpStatusCodeError<!-- -->

Raised when the response status code indicates an error.

### Hierarchy

* *HttpStatusCodeError*
  * [HttpClientStatusCodeError](https://crawlee.dev/python/python/api/class/HttpClientStatusCodeError.md)

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpStatusCodeError.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/errors.py#L64)\_\_init\_\_

* ****\_\_init\_\_**(message, status\_code): None

- Inherited from [HttpStatusCodeError.\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpStatusCodeError.md#__init__)

  #### Parameters

  * ##### message: str
  * ##### status\_code: int

  #### Returns None


---

# HttpxHttpClient<!-- -->

HTTP client based on the `HTTPX` library.

This client uses the `HTTPX` library to perform HTTP requests in crawlers (`BasicCrawler` subclasses) and to manage sessions, proxies, and error handling.

See the `HttpClient` class for more common information about HTTP clients.

### Usage

```
from crawlee.crawlers import HttpCrawler  # or any other HTTP client-based crawler
from crawlee.http_clients import HttpxHttpClient

http_client = HttpxHttpClient()
crawler = HttpCrawler(http_client=http_client)
```

### Hierarchy

* [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)
  * *HttpxHttpClient*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#__init__)
* [**cleanup](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#cleanup)
* [**crawl](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#crawl)
* [**send\_request](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#send_request)
* [**stream](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#stream)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md#active)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L201)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

- Inherited from [HttpClient.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aenter__)

  Initialize the client when entering the context manager.

  ***

  #### Returns [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L213)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, traceback): None

- Inherited from [HttpClient.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aexit__)

  Deinitialize the client and clean up resources when exiting the context manager.

  ***

  #### Parameters

  * ##### exc\_type: BaseException | None
  * ##### exc\_value: BaseException | None
  * ##### traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L107)\_\_init\_\_

* ****\_\_init\_\_**(\*, persist\_cookies\_per\_session, http1, http2, verify, header\_generator, async\_client\_kwargs): None

- Overrides [HttpClient.\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypersist\_cookies\_per\_session: bool = <!-- -->True

    Whether to persist cookies per HTTP session.

  * ##### optionalkeyword-onlyhttp1: bool = <!-- -->True

    Whether to enable HTTP/1.1 support.

  * ##### optionalkeyword-onlyhttp2: bool = <!-- -->True

    Whether to enable HTTP/2 support.

  * ##### optionalkeyword-onlyverify: (str | bool) | SSLContext = <!-- -->True

    SSL certificates used to verify the identity of requested hosts.

  * ##### optionalkeyword-onlyheader\_generator: [HeaderGenerator](https://crawlee.dev/python/python/api/class/HeaderGenerator.md) | None = <!-- -->\_DEFAULT\_HEADER\_GENERATOR

    Header generator instance to use for generating common headers.

  * ##### async\_client\_kwargs: Any

    Additional keyword arguments for `httpx.AsyncClient`.

  #### Returns None

### [**](#cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L349)cleanup

* **async **cleanup**(): None

- Overrides [HttpClient.cleanup](https://crawlee.dev/python/python/api/class/HttpClient.md#cleanup)

  Clean up resources used by the client.

  This method is called when the client is no longer needed and should be overridden in subclasses to perform any necessary cleanup such as closing connections, releasing file handles, or other resource deallocation.

  ***

  #### Returns None

### [**](#crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L143)crawl

* **async **crawl**(request, \*, session, proxy\_info, statistics, timeout): [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

- Overrides [HttpClient.crawl](https://crawlee.dev/python/python/api/class/HttpClient.md#crawl)

  Perform the crawling for a given request.

  This method is called from `crawler.run()`.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to be crawled.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlystatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md) | None = <!-- -->None

    The statistics object to register status codes.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

  The result of the crawling.

### [**](#send_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L184)send\_request

* **async **send\_request**(url, \*, method, headers, payload, session, proxy\_info, timeout): [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

- Overrides [HttpClient.send\_request](https://crawlee.dev/python/python/api/class/HttpClient.md#send_request)

  Send an HTTP request via the client.

  This method is called from `context.send_request()` helper.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  The HTTP response received from the server.

### [**](#stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L220)stream

* ****stream**(url, \*, method, headers, payload, session, proxy\_info, timeout): AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

- Overrides [HttpClient.stream](https://crawlee.dev/python/python/api/class/HttpClient.md#stream)

  Stream an HTTP request via the client.

  This method should be used for downloading potentially large data where you need to process the response body in chunks rather than loading it entirely into memory.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    The maximum time to wait for establishing the connection.

  #### Returns AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

  An async context manager yielding the HTTP response with streaming capabilities.

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L95)active

**active: bool

Inherited from [HttpClient.active](https://crawlee.dev/python/python/api/class/HttpClient.md#active)

Indicate whether the context is active.


---

# ImpitHttpClient<!-- -->

HTTP client based on the `impit` library.

This client uses the `impit` library to perform HTTP requests in crawlers (`BasicCrawler` subclasses) and to manage sessions, proxies, and error handling.

See the `HttpClient` class for more common information about HTTP clients.

### Usage

```
from crawlee.crawlers import HttpCrawler  # or any other HTTP client-based crawler
from crawlee.http_clients import ImpitHttpClient

http_client = ImpitHttpClient()
crawler = HttpCrawler(http_client=http_client)
```

### Hierarchy

* [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)
  * *ImpitHttpClient*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#__init__)
* [**cleanup](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#cleanup)
* [**crawl](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#crawl)
* [**send\_request](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#send_request)
* [**stream](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#stream)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md#active)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L201)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

- Inherited from [HttpClient.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aenter__)

  Initialize the client when entering the context manager.

  ***

  #### Returns [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L213)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, traceback): None

- Inherited from [HttpClient.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__aexit__)

  Deinitialize the client and clean up resources when exiting the context manager.

  ***

  #### Parameters

  * ##### exc\_type: BaseException | None
  * ##### exc\_value: BaseException | None
  * ##### traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L91)\_\_init\_\_

* ****\_\_init\_\_**(\*, persist\_cookies\_per\_session, http3, verify, browser, async\_client\_kwargs): None

- Overrides [HttpClient.\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypersist\_cookies\_per\_session: bool = <!-- -->True

    Whether to persist cookies per HTTP session.

  * ##### optionalkeyword-onlyhttp3: bool = <!-- -->False

    Whether to enable HTTP/3 support.

  * ##### optionalkeyword-onlyverify: bool = <!-- -->True

    SSL certificates used to verify the identity of requested hosts.

  * ##### optionalkeyword-onlybrowser: Browser | None = <!-- -->'firefox'

    Browser to impersonate.

  * ##### async\_client\_kwargs: Any

    Additional keyword arguments for `impit.AsyncClient`.

  #### Returns None

### [**](#cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L271)cleanup

* **async **cleanup**(): None

- Overrides [HttpClient.cleanup](https://crawlee.dev/python/python/api/class/HttpClient.md#cleanup)

  Clean up resources used by the HTTP client.

  ***

  #### Returns None

### [**](#crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L121)crawl

* **async **crawl**(request, \*, session, proxy\_info, statistics, timeout): [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

- Overrides [HttpClient.crawl](https://crawlee.dev/python/python/api/class/HttpClient.md#crawl)

  Perform the crawling for a given request.

  This method is called from `crawler.run()`.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to be crawled.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlystatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md) | None = <!-- -->None

    The statistics object to register status codes.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpCrawlingResult](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md)

  The result of the crawling.

### [**](#send_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L155)send\_request

* **async **send\_request**(url, \*, method, headers, payload, session, proxy\_info, timeout): [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

- Overrides [HttpClient.send\_request](https://crawlee.dev/python/python/api/class/HttpClient.md#send_request)

  Send an HTTP request via the client.

  This method is called from `context.send_request()` helper.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    Maximum time allowed to process the request.

  #### Returns [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  The HTTP response received from the server.

### [**](#stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L190)stream

* ****stream**(url, \*, method, headers, payload, session, proxy\_info, timeout): AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

- Overrides [HttpClient.stream](https://crawlee.dev/python/python/api/class/HttpClient.md#stream)

  Stream an HTTP request via the client.

  This method should be used for downloading potentially large data where you need to process the response body in chunks rather than loading it entirely into memory.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The data to be sent as the request body.

  * ##### optionalkeyword-onlysession: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None = <!-- -->None

    The session associated with the request.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The information about the proxy to be used.

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    The maximum time to wait for establishing the connection.

  #### Returns AbstractAsyncContextManager\[[HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

  An async context manager yielding the HTTP response with streaming capabilities.

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L95)active

**active: bool

Inherited from [HttpClient.active](https://crawlee.dev/python/python/api/class/HttpClient.md#active)

Indicate whether the context is active.


---

# ImportWrapper<!-- -->

A wrapper class for modules to handle attribute access for failed imports.

## Index[**](#Index)

### Methods

* [**\_\_getattribute\_\_](https://crawlee.dev/python/python/api/class/ImportWrapper.md#__getattribute__)

## Methods<!-- -->[**](#Methods)

### [**](#__getattribute__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/try_import.py#L38)\_\_getattribute\_\_

* ****\_\_getattribute\_\_**(name): Any

- #### Parameters

  * ##### name: str

  #### Returns Any


---

# JsonField<!-- -->

Uses JSONB for PostgreSQL and JSON for other databases.

## Index[**](#Index)

### Methods

* [**load\_dialect\_impl](https://crawlee.dev/python/python/api/class/JsonField.md#load_dialect_impl)

### Properties

* [**cache\_ok](https://crawlee.dev/python/python/api/class/JsonField.md#cache_ok)
* [**impl](https://crawlee.dev/python/python/api/class/JsonField.md#impl)

## Methods<!-- -->[**](#Methods)

### [**](#load_dialect_impl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L41)load\_dialect\_impl

* ****load\_dialect\_impl**(dialect): TypeEngine\[JSON | JSONB]

- Load the appropriate dialect implementation for the JSON type.

  ***

  #### Parameters

  * ##### dialect: Dialect

  #### Returns TypeEngine\[JSON | JSONB]

## Properties<!-- -->[**](#Properties)

### [**](#cache_ok)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L39)cache\_ok

**cache\_ok: Undefined

### [**](#impl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L38)impl

**impl: Undefined


---

