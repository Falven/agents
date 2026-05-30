# \_AsyncSession<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_AsyncSession.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L53)\_\_init\_\_

* ****\_\_init\_\_**(args, kwargs): None

- #### Parameters

  * ##### args: Any
  * ##### kwargs: Any

  #### Returns None


---

# \_AutoscaledPoolRun<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_AutoscaledPoolRun.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L29)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None


---

# \_BasicCrawlerOptions<!-- -->

Non-generic options the `BasicCrawler` constructor.

### Hierarchy

* *\_BasicCrawlerOptions*
  * [BasicCrawlerOptions](https://crawlee.dev/python/python/api/class/BasicCrawlerOptions.md)

## Index[**](#Index)

### Properties

* [**abort\_on\_error](#abort_on_error)
* [**additional\_http\_error\_status\_codes](#additional_http_error_status_codes)
* [**concurrency\_settings](#concurrency_settings)
* [**configuration](#configuration)
* [**configure\_logging](#configure_logging)
* [**event\_manager](#event_manager)
* [**http\_client](#http_client)
* [**id](#id)
* [**ignore\_http\_error\_status\_codes](#ignore_http_error_status_codes)
* [**keep\_alive](#keep_alive)
* [**max\_crawl\_depth](#max_crawl_depth)
* [**max\_request\_retries](#max_request_retries)
* [**max\_requests\_per\_crawl](#max_requests_per_crawl)
* [**max\_session\_rotations](#max_session_rotations)
* [**proxy\_configuration](#proxy_configuration)
* [**request\_handler\_timeout](#request_handler_timeout)
* [**request\_manager](#request_manager)
* [**respect\_robots\_txt\_file](#respect_robots_txt_file)
* [**retry\_on\_blocked](#retry_on_blocked)
* [**session\_pool](#session_pool)
* [**statistics\_log\_format](#statistics_log_format)
* [**status\_message\_callback](#status_message_callback)
* [**status\_message\_logging\_interval](#status_message_logging_interval)
* [**storage\_client](#storage_client)
* [**use\_session\_pool](#use_session_pool)

## Properties<!-- -->[**](#Properties)

### [**](#abort_on_error)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L175)keyword-onlyoptionalabort\_on\_error

**abort\_on\_error: NotRequired\[bool]

If True, the crawler stops immediately when any request handler error occurs.

### [**](#additional_http_error_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L189)keyword-onlyoptionaladditional\_http\_error\_status\_codes

**additional\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

### [**](#concurrency_settings)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L169)keyword-onlyoptionalconcurrency\_settings

**concurrency\_settings: NotRequired\[[ConcurrencySettings](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md)]

Settings to fine-tune concurrency levels.

### [**](#configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L116)keyword-onlyoptionalconfiguration

**configuration: NotRequired\[[Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)]

The `Configuration` instance. Some of its properties are used as defaults for the crawler.

### [**](#configure_logging)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L178)keyword-onlyoptionalconfigure\_logging

**configure\_logging: NotRequired\[bool]

If True, the crawler will set up logging infrastructure automatically.

### [**](#event_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L119)keyword-onlyoptionalevent\_manager

**event\_manager: NotRequired\[[EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)]

The event manager for managing events for the crawler and all its components.

### [**](#http_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L134)keyword-onlyoptionalhttp\_client

**http\_client: NotRequired\[[HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)]

HTTP client used by `BasicCrawlingContext.send_request` method.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L216)keyword-onlyoptionalid

**id: NotRequired\[int]

Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

### [**](#ignore_http_error_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L192)keyword-onlyoptionalignore\_http\_error\_status\_codes

**ignore\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

HTTP status codes that are typically considered errors but should be treated as successful responses.

### [**](#keep_alive)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L186)keyword-onlyoptionalkeep\_alive

**keep\_alive: NotRequired\[bool]

Flag that can keep crawler running even when there are no requests in queue.

### [**](#max_crawl_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L156)keyword-onlyoptionalmax\_crawl\_depth

**max\_crawl\_depth: NotRequired\[int | None]

Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

### [**](#max_request_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L137)keyword-onlyoptionalmax\_request\_retries

**max\_request\_retries: NotRequired\[int]

Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.).

This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

### [**](#max_requests_per_crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L144)keyword-onlyoptionalmax\_requests\_per\_crawl

**max\_requests\_per\_crawl: NotRequired\[int | None]

Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value.

### [**](#max_session_rotations)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L149)keyword-onlyoptionalmax\_session\_rotations

**max\_session\_rotations: NotRequired\[int]

Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request.

The session rotations are not counted towards the `max_request_retries` limit.

### [**](#proxy_configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L131)keyword-onlyoptionalproxy\_configuration

**proxy\_configuration: NotRequired\[[ProxyConfiguration](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md)]

HTTP proxy configuration used when making requests.

### [**](#request_handler_timeout)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L172)keyword-onlyoptionalrequest\_handler\_timeout

**request\_handler\_timeout: NotRequired\[timedelta]

Maximum duration allowed for a single request handler to run.

### [**](#request_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L125)keyword-onlyoptionalrequest\_manager

**request\_manager: NotRequired\[[RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)]

Manager of requests that should be processed by the crawler.

### [**](#respect_robots_txt_file)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L203)keyword-onlyoptionalrespect\_robots\_txt\_file

**respect\_robots\_txt\_file: NotRequired\[bool]

If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`.

### [**](#retry_on_blocked)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L166)keyword-onlyoptionalretry\_on\_blocked

**retry\_on\_blocked: NotRequired\[bool]

If True, the crawler attempts to bypass bot protections automatically.

### [**](#session_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L128)keyword-onlyoptionalsession\_pool

**session\_pool: NotRequired\[[SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md)]

A custom `SessionPool` instance, allowing the use of non-default configuration.

### [**](#statistics_log_format)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L181)keyword-onlyoptionalstatistics\_log\_format

**statistics\_log\_format: NotRequired\[Literal\[table, inline]]

If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

### [**](#status_message_callback)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L210)keyword-onlyoptionalstatus\_message\_callback

**status\_message\_callback: NotRequired\[Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]]]

Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

### [**](#status_message_logging_interval)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L207)keyword-onlyoptionalstatus\_message\_logging\_interval

**status\_message\_logging\_interval: NotRequired\[timedelta]

Interval for logging the crawler status messages.

### [**](#storage_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L122)keyword-onlyoptionalstorage\_client

**storage\_client: NotRequired\[[StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)]

The storage client for managing storages for the crawler and all its components.

### [**](#use_session_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L163)keyword-onlyoptionaluse\_session\_pool

**use\_session\_pool: NotRequired\[bool]

Enable the use of a session pool for managing sessions during crawling.


---

# \_BasicCrawlerOptionsGeneric<!-- -->

Generic options the `BasicCrawler` constructor.

### Hierarchy

* *\_BasicCrawlerOptionsGeneric*
  * [BasicCrawlerOptions](https://crawlee.dev/python/python/api/class/BasicCrawlerOptions.md)

## Index[**](#Index)

### Properties

* [**request\_handler](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptionsGeneric.md#request_handler)
* [**statistics](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptionsGeneric.md#statistics)

## Properties<!-- -->[**](#Properties)

### [**](#request_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L224)request\_handler

**request\_handler: NotRequired\[Callable\[\[TCrawlingContext], Awaitable\[None]]]

A callable responsible for handling requests.

### [**](#statistics)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L231)statistics

**statistics: NotRequired\[[Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[TStatisticsState](https://crawlee.dev/python/python/api.md#TStatisticsState)]]

A custom `Statistics` instance, allowing the use of non-default configuration.


---

# \_ClientCacheEntry<!-- -->

Type definition for client cache entries.

## Index[**](#Index)

### Properties

* [**client](https://crawlee.dev/python/python/api/class/_ClientCacheEntry.md#client)
* [**cookie\_jar](https://crawlee.dev/python/python/api/class/_ClientCacheEntry.md#cookie_jar)

## Properties<!-- -->[**](#Properties)

### [**](#client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L36)client

**client: AsyncClient

### [**](#cookie_jar)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L37)cookie\_jar

**cookie\_jar: CookieJar | None


---

# \_CurlImpersonateResponse<!-- -->

Adapter class for `curl_cffi.requests.Response` to conform to the `HttpResponse` protocol.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_CurlImpersonateResponse.md#__init__)
* [**read](https://crawlee.dev/python/python/api/class/_CurlImpersonateResponse.md#read)
* [**read\_stream](https://crawlee.dev/python/python/api/class/_CurlImpersonateResponse.md#read_stream)

### Properties

* [**headers](https://crawlee.dev/python/python/api/class/_CurlImpersonateResponse.md#headers)
* [**http\_version](https://crawlee.dev/python/python/api/class/_CurlImpersonateResponse.md#http_version)
* [**status\_code](https://crawlee.dev/python/python/api/class/_CurlImpersonateResponse.md#status_code)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L61)\_\_init\_\_

* ****\_\_init\_\_**(response): None

- #### Parameters

  * ##### response: Response

  #### Returns None

### [**](#read)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L91)read

* **async **read**(): [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

- #### Returns [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

### [**](#read_stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L97)read\_stream

* **async **read\_stream**(): AsyncGenerator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes), None]

- #### Returns AsyncGenerator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes), None]

## Properties<!-- -->[**](#Properties)

### [**](#headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L88)headers

**headers: [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#http_version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L65)http\_version

**http\_version: str

### [**](#status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L84)status\_code

**status\_code: int


---

# \_DatasetMetadataUpdateParams<!-- -->

Parameters for updating dataset metadata.

## Index[**](#Index)

### Properties

* [**delta\_item\_count](https://crawlee.dev/python/python/api/class/_DatasetMetadataUpdateParams.md#delta_item_count)
* [**new\_item\_count](https://crawlee.dev/python/python/api/class/_DatasetMetadataUpdateParams.md#new_item_count)

## Properties<!-- -->[**](#Properties)

### [**](#delta_item_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L36)delta\_item\_count

**delta\_item\_count: NotRequired\[int]

### [**](#new_item_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L35)new\_item\_count

**new\_item\_count: NotRequired\[int]


---

# \_DatasetMetadataUpdateParams<!-- -->

Parameters for updating dataset metadata.

## Index[**](#Index)

### Properties

* [**delta\_item\_count](https://crawlee.dev/python/python/api/class/_DatasetMetadataUpdateParams.md#delta_item_count)
* [**new\_item\_count](https://crawlee.dev/python/python/api/class/_DatasetMetadataUpdateParams.md#new_item_count)

## Properties<!-- -->[**](#Properties)

### [**](#delta_item_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L36)delta\_item\_count

**delta\_item\_count: NotRequired\[int]

### [**](#new_item_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L35)new\_item\_count

**new\_item\_count: NotRequired\[int]


---

# \_EmptyCookies<!-- -->

## Index[**](#Index)

### Methods

* [**get\_cookies\_for\_curl](https://crawlee.dev/python/python/api/class/_EmptyCookies.md#get_cookies_for_curl)
* [**update\_cookies\_from\_curl](https://crawlee.dev/python/python/api/class/_EmptyCookies.md#update_cookies_from_curl)

## Methods<!-- -->[**](#Methods)

### [**](#get_cookies_for_curl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L43)get\_cookies\_for\_curl

* ****get\_cookies\_for\_curl**(request): list\[CurlMorsel]

- #### Parameters

  * ##### request: CurlRequest

  #### Returns list\[CurlMorsel]

### [**](#update_cookies_from_curl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_curl_impersonate.py#L47)update\_cookies\_from\_curl

* ****update\_cookies\_from\_curl**(morsels): None

- #### Parameters

  * ##### morsels: list\[CurlMorsel]

  #### Returns None


---

# \_HttpxResponse<!-- -->

Adapter class for `httpx.Response` to conform to the `HttpResponse` protocol.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_HttpxResponse.md#__init__)
* [**read](https://crawlee.dev/python/python/api/class/_HttpxResponse.md#read)
* [**read\_stream](https://crawlee.dev/python/python/api/class/_HttpxResponse.md#read_stream)

### Properties

* [**headers](https://crawlee.dev/python/python/api/class/_HttpxResponse.md#headers)
* [**http\_version](https://crawlee.dev/python/python/api/class/_HttpxResponse.md#http_version)
* [**status\_code](https://crawlee.dev/python/python/api/class/_HttpxResponse.md#status_code)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L35)\_\_init\_\_

* ****\_\_init\_\_**(response): None

- #### Parameters

  * ##### response: httpx.Response

  #### Returns None

### [**](#read)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L50)read

* **async **read**(): [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

- #### Returns [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

### [**](#read_stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L55)read\_stream

* **async **read\_stream**(): AsyncIterator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)]

- #### Returns AsyncIterator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)]

## Properties<!-- -->[**](#Properties)

### [**](#headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L47)headers

**headers: [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#http_version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L39)http\_version

**http\_version: str

### [**](#status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L43)status\_code

**status\_code: int


---

# \_HttpxTransport<!-- -->

HTTP transport adapter that stores response cookies in a `Session`.

This transport adapter modifies the handling of HTTP requests to update the session cookies based on the response cookies, ensuring that the cookies are stored in the session object rather than the `HTTPX` client itself.

## Index[**](#Index)

### Async Resource Clients

* [**handle\_async\_request](https://crawlee.dev/python/python/api/class/_HttpxTransport.md#handle_async_request)

## Async Resource Clients<!-- -->[**](<#Async Resource Clients>)

### [**](#handle_async_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_httpx.py#L72)handle\_async\_request

* **async **handle\_async\_request**(request): httpx.Response

- #### Parameters

  * ##### request: httpx.Request

  #### Returns httpx.Response


---

# \_ImpitResponse<!-- -->

Adapter class for `impit.Response` to conform to the `HttpResponse` protocol.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_ImpitResponse.md#__init__)
* [**read](https://crawlee.dev/python/python/api/class/_ImpitResponse.md#read)
* [**read\_stream](https://crawlee.dev/python/python/api/class/_ImpitResponse.md#read_stream)

### Properties

* [**headers](https://crawlee.dev/python/python/api/class/_ImpitResponse.md#headers)
* [**http\_version](https://crawlee.dev/python/python/api/class/_ImpitResponse.md#http_version)
* [**status\_code](https://crawlee.dev/python/python/api/class/_ImpitResponse.md#status_code)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L43)\_\_init\_\_

* ****\_\_init\_\_**(response): None

- #### Parameters

  * ##### response: Response

  #### Returns None

### [**](#read)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L58)read

* **async **read**(): [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

- #### Returns [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

### [**](#read_stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L63)read\_stream

* **async **read\_stream**(): AsyncIterator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)]

- #### Returns AsyncIterator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)]

## Properties<!-- -->[**](#Properties)

### [**](#headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L55)headers

**headers: [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#http_version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L47)http\_version

**http\_version: str

### [**](#status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_impit.py#L51)status\_code

**status\_code: int


---

# \_Middleware<!-- -->

Helper wrapper class to make the middleware easily observable by open telemetry instrumentation.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_Middleware.md#__init__)
* [**action](https://crawlee.dev/python/python/api/class/_Middleware.md#action)
* [**cleanup](https://crawlee.dev/python/python/api/class/_Middleware.md#cleanup)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_context_pipeline.py#L27)\_\_init\_\_

* ****\_\_init\_\_**(middleware, input\_context): None

- #### Parameters

  * ##### middleware: Callable\[\[TCrawlingContext], AsyncGenerator\[[TMiddlewareCrawlingContext](https://crawlee.dev/python/python/api.md#TMiddlewareCrawlingContext), Exception | None]]
  * ##### input\_context: [TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)

  #### Returns None

### [**](#action)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_context_pipeline.py#L39)action

* **async **action**(): [TMiddlewareCrawlingContext](https://crawlee.dev/python/python/api.md#TMiddlewareCrawlingContext)

- #### Returns [TMiddlewareCrawlingContext](https://crawlee.dev/python/python/api.md#TMiddlewareCrawlingContext)

### [**](#cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_context_pipeline.py#L43)cleanup

* **async **cleanup**(final\_consumer\_exception): None

- #### Parameters

  * ##### final\_consumer\_exception: Exception | None

  #### Returns None


---

# \_NewUrlFunction<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/_NewUrlFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L264)\_\_call\_\_

* ****\_\_call\_\_**(session\_id, request): (str | None) | Awaitable\[str | None]

- #### Parameters

  * ##### optionalsession\_id: str | None = <!-- -->None
  * ##### optionalrequest: [Request](https://crawlee.dev/python/python/api/class/Request.md) | None = <!-- -->None

  #### Returns (str | None) | Awaitable\[str | None]


---

# \_NonPersistentStatistics<!-- -->

Statistics compliant object that is not supposed to do anything when entering/exiting context.

To be used in sub crawlers.

### Hierarchy

* [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)
  * *\_NonPersistentStatistics*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#__init__)
* [**calculate](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#calculate)
* [**record\_request\_processing\_failure](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#record_request_processing_failure)
* [**record\_request\_processing\_finish](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#record_request_processing_finish)
* [**record\_request\_processing\_start](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#record_request_processing_start)
* [**register\_status\_code](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#register_status_code)
* [**replace\_state\_model](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#replace_state_model)
* [**reset](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#reset)
* [**with\_default\_state](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#with_default_state)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#active)
* [**state](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md#state)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L66)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): Self

- Overrides [Statistics.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__aenter__)

  Subscribe to events and start collecting statistics.

  ***

  #### Returns Self

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L71)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Overrides [Statistics.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__aexit__)

  Stop collecting statistics.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L63)\_\_init\_\_

* ****\_\_init\_\_**(\*, persistence\_enabled, persist\_state\_kvs\_name, persist\_state\_key, persist\_state\_kvs\_factory, log\_message, periodic\_message\_logger, log\_interval, state\_model, statistics\_log\_format, save\_error\_snapshots): None

- Overrides [Statistics.\_\_init\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__init__)

  #### Parameters

  * ##### optionalkeyword-onlypersistence\_enabled: bool | Literal\[explicit\_only] = <!-- -->False
  * ##### optionalkeyword-onlypersist\_state\_kvs\_name: str | None = <!-- -->None
  * ##### optionalkeyword-onlypersist\_state\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlypersist\_state\_kvs\_factory: Callable\[\[], Coroutine\[None, None, [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)]] | None = <!-- -->None
  * ##### optionalkeyword-onlylog\_message: str = <!-- -->'Statistics'
  * ##### optionalkeyword-onlyperiodic\_message\_logger: Logger | None = <!-- -->None
  * ##### optionalkeyword-onlylog\_interval: timedelta = <!-- -->timedelta(minutes=1)
  * ##### keyword-onlystate\_model: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[[TStatisticsState](https://crawlee.dev/python/python/api.md#TStatisticsState)]
  * ##### optionalkeyword-onlystatistics\_log\_format: Literal\[table, inline] = <!-- -->'table'
  * ##### optionalkeyword-onlysave\_error\_snapshots: bool = <!-- -->False

  #### Returns None

### [**](#calculate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L258)calculate

* ****calculate**(): [FinalStatistics](https://crawlee.dev/python/python/api/class/FinalStatistics.md)

- Inherited from [Statistics.calculate](https://crawlee.dev/python/python/api/class/Statistics.md#calculate)

  Calculate the current statistics.

  ***

  #### Returns [FinalStatistics](https://crawlee.dev/python/python/api/class/FinalStatistics.md)

### [**](#record_request_processing_failure)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L244)record\_request\_processing\_failure

* ****record\_request\_processing\_failure**(request\_id\_or\_key): None

- Inherited from [Statistics.record\_request\_processing\_failure](https://crawlee.dev/python/python/api/class/Statistics.md#record_request_processing_failure)

  Mark a request as failed.

  ***

  #### Parameters

  * ##### request\_id\_or\_key: str

  #### Returns None

### [**](#record_request_processing_finish)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L222)record\_request\_processing\_finish

* ****record\_request\_processing\_finish**(request\_id\_or\_key): None

- Inherited from [Statistics.record\_request\_processing\_finish](https://crawlee.dev/python/python/api/class/Statistics.md#record_request_processing_finish)

  Mark a request as finished.

  ***

  #### Parameters

  * ##### request\_id\_or\_key: str

  #### Returns None

### [**](#record_request_processing_start)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L215)record\_request\_processing\_start

* ****record\_request\_processing\_start**(request\_id\_or\_key): None

- Inherited from [Statistics.record\_request\_processing\_start](https://crawlee.dev/python/python/api/class/Statistics.md#record_request_processing_start)

  Mark a request as started.

  ***

  #### Parameters

  * ##### request\_id\_or\_key: str

  #### Returns None

### [**](#register_status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L208)register\_status\_code

* ****register\_status\_code**(code): None

- Inherited from [Statistics.register\_status\_code](https://crawlee.dev/python/python/api/class/Statistics.md#register_status_code)

  Increment the number of times a status code has been received.

  ***

  #### Parameters

  * ##### code: int

  #### Returns None

### [**](#replace_state_model)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L113)replace\_state\_model

* ****replace\_state\_model**(state\_model): Statistics\[TNewStatisticsState]

- Inherited from [Statistics.replace\_state\_model](https://crawlee.dev/python/python/api/class/Statistics.md#replace_state_model)

  Create near copy of the `Statistics` with replaced `state_model`.

  ***

  #### Parameters

  * ##### state\_model: type\[TNewStatisticsState]

  #### Returns Statistics\[TNewStatisticsState]

### [**](#reset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L277)reset

* **async **reset**(): None

- Inherited from [Statistics.reset](https://crawlee.dev/python/python/api/class/Statistics.md#reset)

  Reset the statistics to their defaults and remove any persistent state.

  ***

  #### Returns None

### [**](#with_default_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L127)with\_default\_state

* ****with\_default\_state**(\*, persistence\_enabled, persist\_state\_kvs\_name, persist\_state\_key, persist\_state\_kvs\_factory, log\_message, periodic\_message\_logger, log\_interval, statistics\_log\_format, save\_error\_snapshots): Statistics\[StatisticsState]

- Inherited from [Statistics.with\_default\_state](https://crawlee.dev/python/python/api/class/Statistics.md#with_default_state)

  Initialize a new instance with default state model `StatisticsState`.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypersistence\_enabled: bool = <!-- -->False
  * ##### optionalkeyword-onlypersist\_state\_kvs\_name: str | None = <!-- -->None
  * ##### optionalkeyword-onlypersist\_state\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlypersist\_state\_kvs\_factory: Callable\[\[], Coroutine\[None, None, KeyValueStore]] | None = <!-- -->None
  * ##### optionalkeyword-onlylog\_message: str = <!-- -->'Statistics'
  * ##### optionalkeyword-onlyperiodic\_message\_logger: Logger | None = <!-- -->None
  * ##### optionalkeyword-onlylog\_interval: timedelta = <!-- -->timedelta(minutes=1)
  * ##### optionalkeyword-onlystatistics\_log\_format: Literal\['table', 'inline'] = <!-- -->'table'
  * ##### optionalkeyword-onlysave\_error\_snapshots: bool = <!-- -->False

  #### Returns Statistics\[StatisticsState]

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L154)active

**active: bool

Inherited from [Statistics.active](https://crawlee.dev/python/python/api/class/Statistics.md#active)

Indicate whether the context is active.

### [**](#state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L204)state

**state: [TStatisticsState](https://crawlee.dev/python/python/api.md#TStatisticsState)

Inherited from [Statistics.state](https://crawlee.dev/python/python/api/class/Statistics.md#state)


---

# \_PlaywrightCrawlerAdditionalOptions<!-- -->

Additional arguments for the `PlaywrightCrawler` constructor.

It is intended for typing forwarded `__init__` arguments in the subclasses. All arguments are `BasicCrawlerOptions` + `_PlaywrightCrawlerAdditionalOptions`

### Hierarchy

* *\_PlaywrightCrawlerAdditionalOptions*
  * [PlaywrightCrawlerOptions](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md)

## Index[**](#Index)

### Properties

* [**browser\_launch\_options](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_launch_options)
* [**browser\_new\_context\_options](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_new_context_options)
* [**browser\_pool](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_pool)
* [**browser\_type](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_type)
* [**headless](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#headless)

## Properties<!-- -->[**](#Properties)

### [**](#browser_launch_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L597)browser\_launch\_options

**browser\_launch\_options: NotRequired\[Mapping\[str, Any]]

Keyword arguments to pass to the browser launch method. These options are provided directly to Playwright's `browser_type.launch` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch>. This option should not be used if `browser_pool` is provided.

### [**](#browser_new_context_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L603)browser\_new\_context\_options

**browser\_new\_context\_options: NotRequired\[Mapping\[str, Any]]

Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>. This option should not be used if `browser_pool` is provided.

### [**](#browser_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L588)browser\_pool

**browser\_pool: NotRequired\[[BrowserPool](https://crawlee.dev/python/python/api/class/BrowserPool.md)]

A `BrowserPool` instance to be used for launching the browsers and getting pages.

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L591)browser\_type

**browser\_type: NotRequired\[[BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)]

The type of browser to launch:

* 'chromium', 'firefox', 'webkit': Use Playwright-managed browsers
* 'chrome': Use your locally installed Google Chrome browser. Requires Google Chrome to be installed on the system. This option should not be used if `browser_pool` is provided.

### [**](#headless)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L609)headless

**headless: NotRequired\[bool]

Whether to run the browser in headless mode. This option should not be used if `browser_pool` is provided.


---

# \_ProxyTierTracker<!-- -->

Tracks the state of currently used proxy tiers and their error frequency for individual crawled domains.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_ProxyTierTracker.md#__init__)
* [**add\_error](https://crawlee.dev/python/python/api/class/_ProxyTierTracker.md#add_error)
* [**get\_tier\_urls](https://crawlee.dev/python/python/api/class/_ProxyTierTracker.md#get_tier_urls)
* [**predict\_tier](https://crawlee.dev/python/python/api/class/_ProxyTierTracker.md#predict_tier)

### Properties

* [**all\_urls](https://crawlee.dev/python/python/api/class/_ProxyTierTracker.md#all_urls)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L227)\_\_init\_\_

* ****\_\_init\_\_**(tiered\_proxy\_urls): None

- #### Parameters

  * ##### tiered\_proxy\_urls: list\[list\[URL | None]]

  #### Returns None

### [**](#add_error)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L239)add\_error

* ****add\_error**(domain, tier): None

- #### Parameters

  * ##### domain: str
  * ##### tier: int

  #### Returns None

### [**](#get_tier_urls)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L236)get\_tier\_urls

* ****get\_tier\_urls**(tier\_number): Sequence\[URL | None]

- #### Parameters

  * ##### tier\_number: int

  #### Returns Sequence\[URL | None]

### [**](#predict_tier)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L242)predict\_tier

* ****predict\_tier**(domain): int

- #### Parameters

  * ##### domain: str

  #### Returns int

## Properties<!-- -->[**](#Properties)

### [**](#all_urls)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L233)all\_urls

**all\_urls: Sequence\[URL | None]


---

# \_QueueMetadataUpdateParams<!-- -->

Parameters for updating queue metadata.

## Index[**](#Index)

### Properties

* [**delta\_handled\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#delta_handled_request_count)
* [**delta\_pending\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#delta_pending_request_count)
* [**delta\_total\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#delta_total_request_count)
* [**new\_handled\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#new_handled_request_count)
* [**new\_pending\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#new_pending_request_count)
* [**new\_total\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#new_total_request_count)
* [**recalculate](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#recalculate)
* [**update\_had\_multiple\_clients](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#update_had_multiple_clients)

## Properties<!-- -->[**](#Properties)

### [**](#delta_handled_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L47)delta\_handled\_request\_count

**delta\_handled\_request\_count: NotRequired\[int]

### [**](#delta_pending_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L48)delta\_pending\_request\_count

**delta\_pending\_request\_count: NotRequired\[int]

### [**](#delta_total_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L49)delta\_total\_request\_count

**delta\_total\_request\_count: NotRequired\[int]

### [**](#new_handled_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L44)new\_handled\_request\_count

**new\_handled\_request\_count: NotRequired\[int]

### [**](#new_pending_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L45)new\_pending\_request\_count

**new\_pending\_request\_count: NotRequired\[int]

### [**](#new_total_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L46)new\_total\_request\_count

**new\_total\_request\_count: NotRequired\[int]

### [**](#recalculate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L50)recalculate

**recalculate: NotRequired\[bool]

### [**](#update_had_multiple_clients)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L51)update\_had\_multiple\_clients

**update\_had\_multiple\_clients: NotRequired\[bool]


---

# \_QueueMetadataUpdateParams<!-- -->

Parameters for updating queue metadata.

## Index[**](#Index)

### Properties

* [**delta\_handled\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#delta_handled_request_count)
* [**delta\_pending\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#delta_pending_request_count)
* [**delta\_total\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#delta_total_request_count)
* [**new\_handled\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#new_handled_request_count)
* [**new\_pending\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#new_pending_request_count)
* [**new\_total\_request\_count](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#new_total_request_count)
* [**recalculate](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#recalculate)
* [**update\_had\_multiple\_clients](https://crawlee.dev/python/python/api/class/_QueueMetadataUpdateParams.md#update_had_multiple_clients)

## Properties<!-- -->[**](#Properties)

### [**](#delta_handled_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L47)delta\_handled\_request\_count

**delta\_handled\_request\_count: NotRequired\[int]

### [**](#delta_pending_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L48)delta\_pending\_request\_count

**delta\_pending\_request\_count: NotRequired\[int]

### [**](#delta_total_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L49)delta\_total\_request\_count

**delta\_total\_request\_count: NotRequired\[int]

### [**](#new_handled_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L44)new\_handled\_request\_count

**new\_handled\_request\_count: NotRequired\[int]

### [**](#new_pending_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L45)new\_pending\_request\_count

**new\_pending\_request\_count: NotRequired\[int]

### [**](#new_total_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L46)new\_total\_request\_count

**new\_total\_request\_count: NotRequired\[int]

### [**](#recalculate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L50)recalculate

**recalculate: NotRequired\[bool]

### [**](#update_had_multiple_clients)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L51)update\_had\_multiple\_clients

**update\_had\_multiple\_clients: NotRequired\[bool]


---

# \_SitemapItem<!-- -->

## Index[**](#Index)

### Properties

* [**changefreq](https://crawlee.dev/python/python/api/class/_SitemapItem.md#changefreq)
* [**lastmod](https://crawlee.dev/python/python/api/class/_SitemapItem.md#lastmod)
* [**loc](https://crawlee.dev/python/python/api/class/_SitemapItem.md#loc)
* [**priority](https://crawlee.dev/python/python/api/class/_SitemapItem.md#priority)
* [**type](https://crawlee.dev/python/python/api/class/_SitemapItem.md#type)
* [**url](https://crawlee.dev/python/python/api/class/_SitemapItem.md#url)

## Properties<!-- -->[**](#Properties)

### [**](#changefreq)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L73)changefreq

**changefreq: str | None

### [**](#lastmod)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L72)lastmod

**lastmod: datetime | None

### [**](#loc)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L70)loc

**loc: str

### [**](#priority)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L74)priority

**priority: float | None

### [**](#type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L69)type

**type: Literal\[url, sitemap\_url]

### [**](#url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L71)url

**url: str


---

# \_StorageCache<!-- -->

Cache for storage instances.

## Index[**](#Index)

### Methods

* [**remove\_from\_cache](https://crawlee.dev/python/python/api/class/_StorageCache.md#remove_from_cache)

### Properties

* [**by\_alias](https://crawlee.dev/python/python/api/class/_StorageCache.md#by_alias)
* [**by\_id](https://crawlee.dev/python/python/api/class/_StorageCache.md#by_id)
* [**by\_name](https://crawlee.dev/python/python/api/class/_StorageCache.md#by_name)

## Methods<!-- -->[**](#Methods)

### [**](#remove_from_cache)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L40)remove\_from\_cache

* ****remove\_from\_cache**(storage\_instance): None

- Remove a storage instance from the cache.

  ***

  #### Parameters

  * ##### storage\_instance: [Storage](https://crawlee.dev/python/python/api/class/Storage.md)

    The storage instance to remove.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#by_alias)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L35)by\_alias

**by\_alias: defaultdict\[[type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[[Storage](https://crawlee.dev/python/python/api/class/Storage.md)], defaultdict\[str, defaultdict\[Hashable, [Storage](https://crawlee.dev/python/python/api/class/Storage.md)]]]

Cache for storage instances by alias. Example: by\_alias\[Dataset]\['some\_alias']\['some\_additional\_cache\_key']

### [**](#by_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L25)by\_id

**by\_id: defaultdict\[[type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[[Storage](https://crawlee.dev/python/python/api/class/Storage.md)], defaultdict\[str, defaultdict\[Hashable, [Storage](https://crawlee.dev/python/python/api/class/Storage.md)]]]

Cache for storage instances by ID. Example: by\_id\[Dataset]\['some\_id']\['some\_additional\_cache\_key'].

### [**](#by_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L30)by\_name

**by\_name: defaultdict\[[type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[[Storage](https://crawlee.dev/python/python/api/class/Storage.md)], defaultdict\[str, defaultdict\[Hashable, [Storage](https://crawlee.dev/python/python/api/class/Storage.md)]]]

Cache for storage instances by name. Example: by\_name\[Dataset]\['some\_name']\['some\_additional\_cache\_key']


---

# \_TxtSitemapParser<!-- -->

Parser for plaintext sitemaps that processes data as a stream.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_TxtSitemapParser.md#__init__)
* [**close](https://crawlee.dev/python/python/api/class/_TxtSitemapParser.md#close)
* [**flush](https://crawlee.dev/python/python/api/class/_TxtSitemapParser.md#flush)
* [**process\_chunk](https://crawlee.dev/python/python/api/class/_TxtSitemapParser.md#process_chunk)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L135)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#close)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L161)close

* ****close**(): None

- Clean up resources.

  ***

  #### Returns None

### [**](#flush)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L153)flush

* **async **flush**(): AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]

- Process any remaining data in the buffer, yielding items one by one.

  ***

  #### Returns AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]

### [**](#process_chunk)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L138)process\_chunk

* **async **process\_chunk**(chunk): AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]

- Process a chunk of text data and yield items one by one.

  ***

  #### Parameters

  * ##### chunk: str

  #### Returns AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]


---

# \_XMLSaxSitemapHandler<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_XMLSaxSitemapHandler.md#__init__)
* [**characters](https://crawlee.dev/python/python/api/class/_XMLSaxSitemapHandler.md#characters)
* [**endElement](https://crawlee.dev/python/python/api/class/_XMLSaxSitemapHandler.md#endElement)
* [**startElement](https://crawlee.dev/python/python/api/class/_XMLSaxSitemapHandler.md#startElement)

### Properties

* [**items](https://crawlee.dev/python/python/api/class/_XMLSaxSitemapHandler.md#items)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L78)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#characters)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L99)characters

* ****characters**(content): None

- #### Parameters

  * ##### content: str

  #### Returns None

### [**](#endElement)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L104)endElement

* ****endElement**(name): None

- #### Parameters

  * ##### name: str

  #### Returns None

### [**](#startElement)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L91)startElement

* ****startElement**(name, attrs): None

- #### Parameters

  * ##### name: str
  * ##### attrs: AttributesImpl

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L87)items

**items: list\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md)]


---

# \_XmlSitemapParser<!-- -->

Parser for XML sitemaps using SAX to process data as a stream.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/_XmlSitemapParser.md#__init__)
* [**close](https://crawlee.dev/python/python/api/class/_XmlSitemapParser.md#close)
* [**flush](https://crawlee.dev/python/python/api/class/_XmlSitemapParser.md#flush)
* [**process\_chunk](https://crawlee.dev/python/python/api/class/_XmlSitemapParser.md#process_chunk)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L169)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#close)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L201)close

* ****close**(): None

- Clean up resources.

  ***

  #### Returns None

### [**](#flush)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L188)flush

* **async **flush**(): AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]

- Process any remaining data in the buffer, yielding items one by one.

  ***

  #### Returns AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]

### [**](#process_chunk)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L174)process\_chunk

* **async **process\_chunk**(chunk): AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]

- Process a chunk of XML data and yield items one by one.

  ***

  #### Parameters

  * ##### chunk: str

  #### Returns AsyncGenerator\[[\_SitemapItem](https://crawlee.dev/python/python/api/class/_SitemapItem.md), None]


---

# AbortError<!-- -->

Raised when an AutoscaledPool run is aborted. Not for direct use.


---

# AbstractHttpCrawler<!-- -->

A web crawler for performing HTTP requests.

The `AbstractHttpCrawler` builds on top of the `BasicCrawler`, inheriting all its features. Additionally, it implements HTTP communication using HTTP clients. The class allows integration with any HTTP client that implements the `HttpClient` interface, provided as an input parameter to the constructor.

`AbstractHttpCrawler` is a generic class intended to be used with a specific parser for parsing HTTP responses and the expected type of `TCrawlingContext` available to the user function. Examples of specific versions include `BeautifulSoupCrawler`, `ParselCrawler`, and `HttpCrawler`.

HTTP client-based crawlers are ideal for websites that do not require JavaScript execution. For websites that require client-side JavaScript execution, consider using a browser-based crawler like the `PlaywrightCrawler`.

### Hierarchy

* [BasicCrawler](https://crawlee.dev/python/python/api/class/BasicCrawler.md)

  * *AbstractHttpCrawler*

    * [HttpCrawler](https://crawlee.dev/python/python/api/class/HttpCrawler.md)
    * [BeautifulSoupCrawler](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md)
    * [ParselCrawler](https://crawlee.dev/python/python/api/class/ParselCrawler.md)

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#add_requests)
* [**create\_parsed\_http\_crawler\_class](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#create_parsed_http_crawler_class)
* [**error\_handler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#error_handler)
* [**export\_data](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#export_data)
* [**failed\_request\_handler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#failed_request_handler)
* [**get\_data](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#get_data)
* [**get\_dataset](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#get_dataset)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#get_key_value_store)
* [**get\_request\_manager](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#get_request_manager)
* [**on\_skipped\_request](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#on_skipped_request)
* [**post\_navigation\_hook](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#post_navigation_hook)
* [**pre\_navigation\_hook](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#pre_navigation_hook)
* [**run](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#run)
* [**stop](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#stop)
* [**use\_state](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#use_state)

### Properties

* [**log](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#log)
* [**router](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#router)
* [**statistics](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#statistics)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_crawler.py#L70)\_\_init\_\_

* ****\_\_init\_\_**(\*, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, request\_handler, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, concurrency\_settings, request\_handler\_timeout, statistics, abort\_on\_error, keep\_alive, configure\_logging, statistics\_log\_format, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id, \_context\_pipeline, \_additional\_context\_managers, \_logger): None

- Overrides [BasicCrawler.\_\_init\_\_](https://crawlee.dev/python/python/api/class/BasicCrawler.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

    The `Configuration` instance. Some of its properties are used as defaults for the crawler.

  * ##### optionalkeyword-onlyevent\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md) | None = <!-- -->None

    The event manager for managing events for the crawler and all its components.

  * ##### optionalkeyword-onlystorage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None = <!-- -->None

    The storage client for managing storages for the crawler and all its components.

  * ##### optionalkeyword-onlyrequest\_manager: [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md) | None = <!-- -->None

    Manager of requests that should be processed by the crawler.

  * ##### optionalkeyword-onlysession\_pool: [SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md) | None = <!-- -->None

    A custom `SessionPool` instance, allowing the use of non-default configuration.

  * ##### optionalkeyword-onlyproxy\_configuration: [ProxyConfiguration](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md) | None = <!-- -->None

    HTTP proxy configuration used when making requests.

  * ##### optionalkeyword-onlyhttp\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md) | None = <!-- -->None

    HTTP client used by `BasicCrawlingContext.send_request` method.

  * ##### optionalkeyword-onlyrequest\_handler: Callable\[\[TCrawlingContext], Awaitable\[None]] | None = <!-- -->None

    A callable responsible for handling requests.

  * ##### optionalkeyword-onlymax\_request\_retries: int = <!-- -->3

    Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.). This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

  * ##### optionalkeyword-onlymax\_requests\_per\_crawl: int | None = <!-- -->None

    Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value. If used together with `keep_alive`, then the crawler will be kept alive only until `max_requests_per_crawl` is achieved.

  * ##### optionalkeyword-onlymax\_session\_rotations: int = <!-- -->10

    Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request. The session rotations are not counted towards the `max_request_retries` limit.

  * ##### optionalkeyword-onlymax\_crawl\_depth: int | None = <!-- -->None

    Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

  * ##### optionalkeyword-onlyuse\_session\_pool: bool = <!-- -->True

    Enable the use of a session pool for managing sessions during crawling.

  * ##### optionalkeyword-onlyretry\_on\_blocked: bool = <!-- -->True

    If True, the crawler attempts to bypass bot protections automatically.

  * ##### optionalkeyword-onlyadditional\_http\_error\_status\_codes: Iterable\[int] | None = <!-- -->None

    Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

  * ##### optionalkeyword-onlyignore\_http\_error\_status\_codes: Iterable\[int] | None = <!-- -->None

    HTTP status codes that are typically considered errors but should be treated as successful responses.

  * ##### optionalkeyword-onlyconcurrency\_settings: [ConcurrencySettings](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md) | None = <!-- -->None

    Settings to fine-tune concurrency levels.

  * ##### optionalkeyword-onlyrequest\_handler\_timeout: timedelta = <!-- -->timedelta(minutes=1)

    Maximum duration allowed for a single request handler to run.

  * ##### optionalkeyword-onlystatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[TStatisticsState](https://crawlee.dev/python/python/api.md#TStatisticsState)] | None = <!-- -->None

    A custom `Statistics` instance, allowing the use of non-default configuration.

  * ##### optionalkeyword-onlyabort\_on\_error: bool = <!-- -->False

    If True, the crawler stops immediately when any request handler error occurs.

  * ##### optionalkeyword-onlykeep\_alive: bool = <!-- -->False

    If True, it will keep crawler alive even if there are no requests in queue. Use `crawler.stop()` to exit the crawler.

  * ##### optionalkeyword-onlyconfigure\_logging: bool = <!-- -->True

    If True, the crawler will set up logging infrastructure automatically.

  * ##### optionalkeyword-onlystatistics\_log\_format: Literal\[table, inline] = <!-- -->'table'

    If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

  * ##### optionalkeyword-onlyrespect\_robots\_txt\_file: bool = <!-- -->False

    If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`

  * ##### optionalkeyword-onlystatus\_message\_logging\_interval: timedelta = <!-- -->timedelta(seconds=10)

    Interval for logging the crawler status messages.

  * ##### optionalkeyword-onlystatus\_message\_callback: Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]] | None = <!-- -->None

    Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

  * ##### optionalkeyword-onlyid: int | None = <!-- -->None

    Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

  * ##### optionalkeyword-only\_context\_pipeline: [ContextPipeline](https://crawlee.dev/python/python/api/class/ContextPipeline.md)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)] | None = <!-- -->None

    Enables extending the request lifecycle and modifying the crawling context. Intended for use by subclasses rather than direct instantiation of `BasicCrawler`.

  * ##### optionalkeyword-only\_additional\_context\_managers: Sequence\[AbstractAsyncContextManager] | None = <!-- -->None

    Additional context managers used throughout the crawler lifecycle. Intended for use by subclasses rather than direct instantiation of `BasicCrawler`.

  * ##### optionalkeyword-only\_logger: logging.Logger | None = <!-- -->None

    A logger instance, typically provided by a subclass, for consistent logging labels. Intended for use by subclasses rather than direct instantiation of `BasicCrawler`.

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

* ****create\_parsed\_http\_crawler\_class**(static\_parser): [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[[AbstractHttpCrawler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md)\[[ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[[TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)], [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult), [TSelectResult](https://crawlee.dev/python/python/api.md#TSelectResult)]]

- Create a specific version of `AbstractHttpCrawler` class.

  This is a convenience factory method for creating a specific `AbstractHttpCrawler` subclass. While `AbstractHttpCrawler` allows its two generic parameters to be independent, this method simplifies cases where `TParseResult` is used for both generic parameters.

  ***

  #### Parameters

  * ##### static\_parser: [AbstractHttpParser](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md)\[[TParseResult](https://crawlee.dev/python/python/api.md#TParseResult), [TSelectResult](https://crawlee.dev/python/python/api.md#TSelectResult)]

  #### Returns [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[[AbstractHttpCrawler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md)\[[ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[[TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)], [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult), [TSelectResult](https://crawlee.dev/python/python/api.md#TSelectResult)]]

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

- Register a hook to be called after each navigation.

  ***

  #### Parameters

  * ##### hook: Callable\[\[HttpCrawlingContext], Awaitable\[None]]

    A coroutine function to be called after each navigation.

  #### Returns None

### [**](#pre_navigation_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_crawler.py#L329)pre\_navigation\_hook

* ****pre\_navigation\_hook**(hook): None

- Register a hook to be called before each navigation.

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

# AbstractHttpParser<!-- -->

Parser used for parsing HTTP response and inspecting parsed result to find links or detect blocking.

### Hierarchy

* *AbstractHttpParser*

  * [NoParser](https://crawlee.dev/python/python/api/class/NoParser.md)
  * [BeautifulSoupParser](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md)
  * [ParselParser](https://crawlee.dev/python/python/api/class/ParselParser.md)

## Index[**](#Index)

### Methods

* [**find\_links](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#find_links)
* [**is\_blocked](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#is_blocked)
* [**is\_matching\_selector](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#is_matching_selector)
* [**parse](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse)
* [**parse\_text](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse_text)
* [**select](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#select)

## Methods<!-- -->[**](#Methods)

### [**](#find_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_parser.py#L96)find\_links

* ****find\_links**(parsed\_content, selector, attribute): Iterable\[str]

- Overrides [AbstractHttpParser.find\_links](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#find_links)

  Find all links in result using selector.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Parsed HTTP response. Result of `parse` method.

  * ##### selector: str

    String used to define matching pattern for finding links.

  * ##### attribute: str

    Which node attribute to extract the links from.

  #### Returns Iterable\[str]

  Iterable of strings that contain found links.

### [**](#is_blocked)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_parser.py#L56)is\_blocked

* ****is\_blocked**(parsed\_content): [BlockedInfo](https://crawlee.dev/python/python/api/class/BlockedInfo.md)

- Overrides [AbstractHttpParser.is\_blocked](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#is_blocked)

  Detect if blocked and return BlockedInfo with additional information.

  Default implementation that expects `is_matching_selector` abstract method to be implemented. Override this method if your parser has different way of blockage detection.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Parsed HTTP response. Result of `parse` method.

  #### Returns [BlockedInfo](https://crawlee.dev/python/python/api/class/BlockedInfo.md)

  `BlockedInfo` object that contains non-empty string description of reason if blockage was detected. Empty string in reason signifies no blockage detected.

### [**](#is_matching_selector)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_parser.py#L84)is\_matching\_selector

* ****is\_matching\_selector**(parsed\_content, selector): bool

- Overrides [AbstractHttpParser.is\_matching\_selector](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#is_matching_selector)

  Find if selector has match in parsed content.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Parsed HTTP response. Result of `parse` method.

  * ##### selector: str

    String used to define matching pattern.

  #### Returns bool

  True if selector has match in parsed content.

### [**](#parse)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_parser.py#L23)parse

* **async **parse**(response): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse)

  Parse HTTP response.

  ***

  #### Parameters

  * ##### response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

    HTTP response to be parsed.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed HTTP response.

### [**](#parse_text)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_parser.py#L34)parse\_text

* **async **parse\_text**(text): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse\_text](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse_text)

  Parse text containing html.

  ***

  #### Parameters

  * ##### text: str

    String containing html.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed text.

### [**](#select)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_parser.py#L45)select

* **async **select**(parsed\_content, selector): Sequence\[[TSelectResult](https://crawlee.dev/python/python/api.md#TSelectResult)]

- Overrides [AbstractHttpParser.select](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#select)

  Use css selector to select page element and return it.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Content where the page element will be located.

  * ##### selector: str

    Css selector used to locate desired html element.

  #### Returns Sequence\[[TSelectResult](https://crawlee.dev/python/python/api.md#TSelectResult)]

  Selected element.


---

# AdaptiveContextError<!-- -->


---

# AdaptivePlaywrightCrawler<!-- -->

An adaptive web crawler capable of using both static HTTP request based crawling and browser based crawling.

It uses a more limited crawling context interface so that it is able to switch to HTTP-only crawling when it detects that it may bring a performance benefit. It uses specific implementation of `AbstractHttpCrawler` and `PlaywrightCrawler`.

### Usage

```
from crawlee.crawlers import AdaptivePlaywrightCrawler, AdaptivePlaywrightCrawlingContext

crawler = AdaptivePlaywrightCrawler.with_beautifulsoup_static_parser(
    max_requests_per_crawl=10,  # Limit the max requests per crawl.
    playwright_crawler_specific_kwargs={'browser_type': 'chromium'},
)

@crawler.router.default_handler
async def request_handler_for_label(context: AdaptivePlaywrightCrawlingContext) -> None:
    # Do some processing using `parsed_content`
    context.log.info(context.parsed_content.title)

    # Locate element h2 within 5 seconds
    h2 = await context.query_selector_one('h2', timedelta(milliseconds=5000))
    # Do stuff with element found by the selector
    context.log.info(h2)

    # Find more links and enqueue them.
    await context.enqueue_links()
    # Save some data.
    await context.push_data({'Visited url': context.request.url})

await crawler.run(['https://crawlee.dev/'])
```

### Hierarchy

* [BasicCrawler](https://crawlee.dev/python/python/api/class/BasicCrawler.md)
  * *AdaptivePlaywrightCrawler*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#add_requests)
* [**error\_handler](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#error_handler)
* [**export\_data](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#export_data)
* [**failed\_request\_handler](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#failed_request_handler)
* [**get\_data](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#get_data)
* [**get\_dataset](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#get_dataset)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#get_key_value_store)
* [**get\_request\_manager](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#get_request_manager)
* [**on\_skipped\_request](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#on_skipped_request)
* [**post\_navigation\_hook](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#post_navigation_hook)
* [**pre\_navigation\_hook](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#pre_navigation_hook)
* [**run](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#run)
* [**stop](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#stop)
* [**track\_browser\_request\_handler\_runs](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#track_browser_request_handler_runs)
* [**track\_http\_only\_request\_handler\_runs](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#track_http_only_request_handler_runs)
* [**track\_rendering\_type\_mispredictions](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#track_rendering_type_mispredictions)
* [**use\_state](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#use_state)
* [**with\_beautifulsoup\_static\_parser](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#with_beautifulsoup_static_parser)
* [**with\_parsel\_static\_parser](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#with_parsel_static_parser)

### Properties

* [**log](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#log)
* [**router](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#router)
* [**statistics](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#statistics)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L119)\_\_init\_\_

* ****\_\_init\_\_**(\*, static\_parser, rendering\_type\_predictor, result\_checker, result\_comparator, playwright\_crawler\_specific\_kwargs, statistics, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, concurrency\_settings, request\_handler\_timeout, abort\_on\_error, configure\_logging, statistics\_log\_format, keep\_alive, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id): None

- Overrides [BasicCrawler.\_\_init\_\_](https://crawlee.dev/python/python/api/class/BasicCrawler.md#__init__)

  Initialize a new instance. Recommended way to create instance is to call factory methods.

  Recommended factory methods: `with_beautifulsoup_static_parser`, `with_parsel_static_parser`.

  ***

  #### Parameters

  * ##### keyword-onlystatic\_parser: [AbstractHttpParser](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult), [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

    Implementation of `AbstractHttpParser`. Parser that will be used for static crawling.

  * ##### optionalkeyword-onlyrendering\_type\_predictor: [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md) | None = <!-- -->None

    Object that implements RenderingTypePredictor and is capable of predicting which rendering method should be used. If None, then `DefaultRenderingTypePredictor` is used.

  * ##### optionalkeyword-onlyresult\_checker: Callable\[\[RequestHandlerRunResult], bool] | None = <!-- -->None

    Function that evaluates whether crawling result is valid or not.

  * ##### optionalkeyword-onlyresult\_comparator: Callable\[\[RequestHandlerRunResult, RequestHandlerRunResult], bool] | None = <!-- -->None

    Function that compares two crawling results and decides whether they are equivalent.

  * ##### optionalkeyword-onlyplaywright\_crawler\_specific\_kwargs: [\_PlaywrightCrawlerAdditionalOptions](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md) | None = <!-- -->None

    `PlaywrightCrawler` only kwargs that are passed to the sub crawler.

  * ##### optionalkeyword-onlystatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[AdaptivePlaywrightCrawlerStatisticState](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md)] | None = <!-- -->None

    A custom `Statistics[AdaptivePlaywrightCrawlerStatisticState]` instance, allowing the use of non-default configuration.

  * ##### keyword-onlyoptionalconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

    The `Configuration` instance. Some of its properties are used as defaults for the crawler.

  * ##### keyword-onlyoptionalevent\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

    The event manager for managing events for the crawler and all its components.

  * ##### keyword-onlyoptionalstorage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)

    The storage client for managing storages for the crawler and all its components.

  * ##### keyword-onlyoptionalrequest\_manager: [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

    Manager of requests that should be processed by the crawler.

  * ##### keyword-onlyoptionalsession\_pool: [SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md)

    A custom `SessionPool` instance, allowing the use of non-default configuration.

  * ##### keyword-onlyoptionalproxy\_configuration: [ProxyConfiguration](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md)

    HTTP proxy configuration used when making requests.

  * ##### keyword-onlyoptionalhttp\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

    HTTP client used by `BasicCrawlingContext.send_request` method.

  * ##### keyword-onlyoptionalmax\_request\_retries: int

    Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.).

    This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

  * ##### keyword-onlyoptionalmax\_requests\_per\_crawl: int | None

    Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value.

  * ##### keyword-onlyoptionalmax\_session\_rotations: int

    Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request.

    The session rotations are not counted towards the `max_request_retries` limit.

  * ##### keyword-onlyoptionalmax\_crawl\_depth: int | None

    Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

  * ##### keyword-onlyoptionaluse\_session\_pool: bool

    Enable the use of a session pool for managing sessions during crawling.

  * ##### keyword-onlyoptionalretry\_on\_blocked: bool

    If True, the crawler attempts to bypass bot protections automatically.

  * ##### keyword-onlyoptionalconcurrency\_settings: [ConcurrencySettings](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md)

    Settings to fine-tune concurrency levels.

  * ##### keyword-onlyoptionalrequest\_handler\_timeout: timedelta

    Maximum duration allowed for a single request handler to run.

  * ##### keyword-onlyoptionalabort\_on\_error: bool

    If True, the crawler stops immediately when any request handler error occurs.

  * ##### keyword-onlyoptionalconfigure\_logging: bool

    If True, the crawler will set up logging infrastructure automatically.

  * ##### keyword-onlyoptionalstatistics\_log\_format: Literal\[table, inline]

    If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

  * ##### keyword-onlyoptionalkeep\_alive: bool

    Flag that can keep crawler running even when there are no requests in queue.

  * ##### keyword-onlyoptionaladditional\_http\_error\_status\_codes: Iterable\[int]

    Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

  * ##### keyword-onlyoptionalignore\_http\_error\_status\_codes: Iterable\[int]

    HTTP status codes that are typically considered errors but should be treated as successful responses.

  * ##### keyword-onlyoptionalrespect\_robots\_txt\_file: bool

    If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`.

  * ##### keyword-onlyoptionalstatus\_message\_logging\_interval: timedelta

    Interval for logging the crawler status messages.

  * ##### keyword-onlyoptionalstatus\_message\_callback: Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]]

    Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

  * ##### keyword-onlyoptionalid: int

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

### [**](#post_navigation_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L463)post\_navigation\_hook

* ****post\_navigation\_hook**(hook, \*, playwright\_only): Callable\[\[Callable\[\[AdaptivePlaywrightPostNavCrawlingContext], Awaitable\[None]]], None]

- Post navigation hooks for adaptive crawler are delegated to sub crawlers.

  Optionally parametrized decorator. Hooks are wrapped in context that handles possibly missing `page` and `response` objects by raising `AdaptiveContextError`.

  ***

  #### Parameters

  * ##### optionalhook: Callable\[\[AdaptivePlaywrightPostNavCrawlingContext], Awaitable\[None]] | None = <!-- -->None
  * ##### optionalkeyword-onlyplaywright\_only: bool = <!-- -->False

  #### Returns Callable\[\[Callable\[\[AdaptivePlaywrightPostNavCrawlingContext], Awaitable\[None]]], None]

### [**](#pre_navigation_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L438)pre\_navigation\_hook

* ****pre\_navigation\_hook**(hook, \*, playwright\_only): Callable\[\[Callable\[\[AdaptivePlaywrightPreNavCrawlingContext], Awaitable\[None]]], None]

- Pre navigation hooks for adaptive crawler are delegated to sub crawlers.

  Optionally parametrized decorator. Hooks are wrapped in context that handles possibly missing `page` object by raising `AdaptiveContextError`.

  ***

  #### Parameters

  * ##### optionalhook: Callable\[\[AdaptivePlaywrightPreNavCrawlingContext], Awaitable\[None]] | None = <!-- -->None
  * ##### optionalkeyword-onlyplaywright\_only: bool = <!-- -->False

  #### Returns Callable\[\[Callable\[\[AdaptivePlaywrightPreNavCrawlingContext], Awaitable\[None]]], None]

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

### [**](#track_browser_request_handler_runs)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L492)track\_browser\_request\_handler\_runs

* ****track\_browser\_request\_handler\_runs**(): None

- #### Returns None

### [**](#track_http_only_request_handler_runs)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L489)track\_http\_only\_request\_handler\_runs

* ****track\_http\_only\_request\_handler\_runs**(): None

- #### Returns None

### [**](#track_rendering_type_mispredictions)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L495)track\_rendering\_type\_mispredictions

* ****track\_rendering\_type\_mispredictions**(): None

- #### Returns None

### [**](#use_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L852)use\_state

* **async **use\_state**(default\_value): dict\[str, JsonSerializable]

- Inherited from [BasicCrawler.use\_state](https://crawlee.dev/python/python/api/class/BasicCrawler.md#use_state)

  #### Parameters

  * ##### optionaldefault\_value: dict\[str, JsonSerializable] | None = <!-- -->None

  #### Returns dict\[str, JsonSerializable]

### [**](#with_beautifulsoup_static_parser)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L235)with\_beautifulsoup\_static\_parser

* ****with\_beautifulsoup\_static\_parser**(rendering\_type\_predictor, result\_checker, result\_comparator, parser\_type, playwright\_crawler\_specific\_kwargs, statistics, \*, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, concurrency\_settings, request\_handler\_timeout, abort\_on\_error, configure\_logging, statistics\_log\_format, keep\_alive, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id): [AdaptivePlaywrightCrawler](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md)\[[ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[BeautifulSoup], BeautifulSoup, Tag]

- Create `AdaptivePlaywrightCrawler` that uses `BeautifulSoup` for parsing static content.

  ***

  #### Parameters

  * ##### optionalrendering\_type\_predictor: [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md) | None = <!-- -->None

  * ##### optionalresult\_checker: Callable\[\[RequestHandlerRunResult], bool] | None = <!-- -->None

  * ##### optionalresult\_comparator: Callable\[\[RequestHandlerRunResult, RequestHandlerRunResult], bool] | None = <!-- -->None

  * ##### optionalparser\_type: [BeautifulSoupParserType](https://crawlee.dev/python/python/api.md#BeautifulSoupParserType) = <!-- -->'lxml'

  * ##### optionalplaywright\_crawler\_specific\_kwargs: [\_PlaywrightCrawlerAdditionalOptions](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md) | None = <!-- -->None

  * ##### optionalstatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[StatisticsState](https://crawlee.dev/python/python/api/class/StatisticsState.md)] | None = <!-- -->None

  * ##### keyword-onlyoptionalconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

    The `Configuration` instance. Some of its properties are used as defaults for the crawler.

  * ##### keyword-onlyoptionalevent\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

    The event manager for managing events for the crawler and all its components.

  * ##### keyword-onlyoptionalstorage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)

    The storage client for managing storages for the crawler and all its components.

  * ##### keyword-onlyoptionalrequest\_manager: [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

    Manager of requests that should be processed by the crawler.

  * ##### keyword-onlyoptionalsession\_pool: [SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md)

    A custom `SessionPool` instance, allowing the use of non-default configuration.

  * ##### keyword-onlyoptionalproxy\_configuration: [ProxyConfiguration](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md)

    HTTP proxy configuration used when making requests.

  * ##### keyword-onlyoptionalhttp\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

    HTTP client used by `BasicCrawlingContext.send_request` method.

  * ##### keyword-onlyoptionalmax\_request\_retries: int

    Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.).

    This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

  * ##### keyword-onlyoptionalmax\_requests\_per\_crawl: int | None

    Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value.

  * ##### keyword-onlyoptionalmax\_session\_rotations: int

    Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request.

    The session rotations are not counted towards the `max_request_retries` limit.

  * ##### keyword-onlyoptionalmax\_crawl\_depth: int | None

    Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

  * ##### keyword-onlyoptionaluse\_session\_pool: bool

    Enable the use of a session pool for managing sessions during crawling.

  * ##### keyword-onlyoptionalretry\_on\_blocked: bool

    If True, the crawler attempts to bypass bot protections automatically.

  * ##### keyword-onlyoptionalconcurrency\_settings: [ConcurrencySettings](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md)

    Settings to fine-tune concurrency levels.

  * ##### keyword-onlyoptionalrequest\_handler\_timeout: timedelta

    Maximum duration allowed for a single request handler to run.

  * ##### keyword-onlyoptionalabort\_on\_error: bool

    If True, the crawler stops immediately when any request handler error occurs.

  * ##### keyword-onlyoptionalconfigure\_logging: bool

    If True, the crawler will set up logging infrastructure automatically.

  * ##### keyword-onlyoptionalstatistics\_log\_format: Literal\[table, inline]

    If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

  * ##### keyword-onlyoptionalkeep\_alive: bool

    Flag that can keep crawler running even when there are no requests in queue.

  * ##### keyword-onlyoptionaladditional\_http\_error\_status\_codes: Iterable\[int]

    Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

  * ##### keyword-onlyoptionalignore\_http\_error\_status\_codes: Iterable\[int]

    HTTP status codes that are typically considered errors but should be treated as successful responses.

  * ##### keyword-onlyoptionalrespect\_robots\_txt\_file: bool

    If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`.

  * ##### keyword-onlyoptionalstatus\_message\_logging\_interval: timedelta

    Interval for logging the crawler status messages.

  * ##### keyword-onlyoptionalstatus\_message\_callback: Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]]

    Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

  * ##### keyword-onlyoptionalid: int

    Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

  #### Returns [AdaptivePlaywrightCrawler](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md)\[[ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[BeautifulSoup], BeautifulSoup, Tag]

### [**](#with_parsel_static_parser)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L261)with\_parsel\_static\_parser

* ****with\_parsel\_static\_parser**(rendering\_type\_predictor, result\_checker, result\_comparator, playwright\_crawler\_specific\_kwargs, statistics, \*, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, concurrency\_settings, request\_handler\_timeout, abort\_on\_error, configure\_logging, statistics\_log\_format, keep\_alive, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id): [AdaptivePlaywrightCrawler](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md)\[[ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[Selector], Selector, Selector]

- Create `AdaptivePlaywrightCrawler` that uses `Parcel` for parsing static content.

  ***

  #### Parameters

  * ##### optionalrendering\_type\_predictor: [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md) | None = <!-- -->None

  * ##### optionalresult\_checker: Callable\[\[RequestHandlerRunResult], bool] | None = <!-- -->None

  * ##### optionalresult\_comparator: Callable\[\[RequestHandlerRunResult, RequestHandlerRunResult], bool] | None = <!-- -->None

  * ##### optionalplaywright\_crawler\_specific\_kwargs: [\_PlaywrightCrawlerAdditionalOptions](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md) | None = <!-- -->None

  * ##### optionalstatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[StatisticsState](https://crawlee.dev/python/python/api/class/StatisticsState.md)] | None = <!-- -->None

  * ##### keyword-onlyoptionalconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

    The `Configuration` instance. Some of its properties are used as defaults for the crawler.

  * ##### keyword-onlyoptionalevent\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

    The event manager for managing events for the crawler and all its components.

  * ##### keyword-onlyoptionalstorage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)

    The storage client for managing storages for the crawler and all its components.

  * ##### keyword-onlyoptionalrequest\_manager: [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

    Manager of requests that should be processed by the crawler.

  * ##### keyword-onlyoptionalsession\_pool: [SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md)

    A custom `SessionPool` instance, allowing the use of non-default configuration.

  * ##### keyword-onlyoptionalproxy\_configuration: [ProxyConfiguration](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md)

    HTTP proxy configuration used when making requests.

  * ##### keyword-onlyoptionalhttp\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

    HTTP client used by `BasicCrawlingContext.send_request` method.

  * ##### keyword-onlyoptionalmax\_request\_retries: int

    Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.).

    This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

  * ##### keyword-onlyoptionalmax\_requests\_per\_crawl: int | None

    Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value.

  * ##### keyword-onlyoptionalmax\_session\_rotations: int

    Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request.

    The session rotations are not counted towards the `max_request_retries` limit.

  * ##### keyword-onlyoptionalmax\_crawl\_depth: int | None

    Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

  * ##### keyword-onlyoptionaluse\_session\_pool: bool

    Enable the use of a session pool for managing sessions during crawling.

  * ##### keyword-onlyoptionalretry\_on\_blocked: bool

    If True, the crawler attempts to bypass bot protections automatically.

  * ##### keyword-onlyoptionalconcurrency\_settings: [ConcurrencySettings](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md)

    Settings to fine-tune concurrency levels.

  * ##### keyword-onlyoptionalrequest\_handler\_timeout: timedelta

    Maximum duration allowed for a single request handler to run.

  * ##### keyword-onlyoptionalabort\_on\_error: bool

    If True, the crawler stops immediately when any request handler error occurs.

  * ##### keyword-onlyoptionalconfigure\_logging: bool

    If True, the crawler will set up logging infrastructure automatically.

  * ##### keyword-onlyoptionalstatistics\_log\_format: Literal\[table, inline]

    If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

  * ##### keyword-onlyoptionalkeep\_alive: bool

    Flag that can keep crawler running even when there are no requests in queue.

  * ##### keyword-onlyoptionaladditional\_http\_error\_status\_codes: Iterable\[int]

    Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

  * ##### keyword-onlyoptionalignore\_http\_error\_status\_codes: Iterable\[int]

    HTTP status codes that are typically considered errors but should be treated as successful responses.

  * ##### keyword-onlyoptionalrespect\_robots\_txt\_file: bool

    If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`.

  * ##### keyword-onlyoptionalstatus\_message\_logging\_interval: timedelta

    Interval for logging the crawler status messages.

  * ##### keyword-onlyoptionalstatus\_message\_callback: Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]]

    Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

  * ##### keyword-onlyoptionalid: int

    Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

  #### Returns [AdaptivePlaywrightCrawler](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md)\[[ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[Selector], Selector, Selector]

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

# AdaptivePlaywrightCrawlerStatisticState<!-- -->

Statistic data about a crawler run with additional information related to adaptive crawling.

### Hierarchy

* [StatisticsState](https://crawlee.dev/python/python/api/class/StatisticsState.md)
  * *AdaptivePlaywrightCrawlerStatisticState*

## Index[**](#Index)

### Methods

* [**crawler\_runtime\_for\_serialization](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#crawler_runtime_for_serialization)
* [**model\_post\_init](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#model_post_init)

### Properties

* [**browser\_request\_handler\_runs](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#browser_request_handler_runs)
* [**crawler\_finished\_at](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#crawler_finished_at)
* [**crawler\_last\_started\_at](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#crawler_last_started_at)
* [**crawler\_runtime](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#crawler_runtime)
* [**crawler\_started\_at](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#crawler_started_at)
* [**http\_only\_request\_handler\_runs](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#http_only_request_handler_runs)
* [**model\_config](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#model_config)
* [**rendering\_type\_mispredictions](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#rendering_type_mispredictions)
* [**request\_avg\_failed\_duration](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_avg_failed_duration)
* [**request\_avg\_finished\_duration](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_avg_finished_duration)
* [**request\_max\_duration](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_max_duration)
* [**request\_min\_duration](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_min_duration)
* [**request\_retry\_histogram](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_retry_histogram)
* [**request\_total\_duration](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_total_duration)
* [**request\_total\_failed\_duration](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_total_failed_duration)
* [**request\_total\_finished\_duration](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#request_total_finished_duration)
* [**requests\_failed](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#requests_failed)
* [**requests\_failed\_per\_minute](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#requests_failed_per_minute)
* [**requests\_finished](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#requests_finished)
* [**requests\_finished\_per\_minute](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#requests_finished_per_minute)
* [**requests\_retries](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#requests_retries)
* [**requests\_total](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#requests_total)
* [**stats\_id](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#stats_id)
* [**stats\_persisted\_at](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md#stats_persisted_at)

## Methods<!-- -->[**](#Methods)

### [**](#crawler_runtime_for_serialization)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L132)crawler\_runtime\_for\_serialization

* ****crawler\_runtime\_for\_serialization**(): timedelta

- Inherited from [StatisticsState.crawler\_runtime\_for\_serialization](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime_for_serialization)

  #### Returns timedelta

### [**](#model_post_init)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L110)model\_post\_init

* ****model\_post\_init**(\_\_context): None

- Inherited from [StatisticsState.model\_post\_init](https://crawlee.dev/python/python/api/class/StatisticsState.md#model_post_init)

  #### Parameters

  * ##### \_\_context: Any

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#browser_request_handler_runs)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler_statistics.py#L20)browser\_request\_handler\_runs

**browser\_request\_handler\_runs: int

Number representing how many times browser based crawling was used.

### [**](#crawler_finished_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L79)crawler\_finished\_at

**crawler\_finished\_at: datetime | None

Inherited from [StatisticsState.crawler\_finished\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_finished_at)

### [**](#crawler_last_started_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L78)crawler\_last\_started\_at

**crawler\_last\_started\_at: datetime | None

Inherited from [StatisticsState.crawler\_last\_started\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_last_started_at)

### [**](#crawler_runtime)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L114)crawler\_runtime

* ****crawler\_runtime**(value): None

- Inherited from [StatisticsState.crawler\_runtime](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime)

  Overrides [StatisticsState.crawler\_runtime](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime)

  #### Parameters

  * ##### value: timedelta

  #### Returns None

### [**](#crawler_started_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L77)crawler\_started\_at

**crawler\_started\_at: datetime | None

Inherited from [StatisticsState.crawler\_started\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_started_at)

### [**](#http_only_request_handler_runs)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler_statistics.py#L17)http\_only\_request\_handler\_runs

**http\_only\_request\_handler\_runs: int

Number representing how many times static http based crawling was used.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler_statistics.py#L15)model\_config

**model\_config: Undefined

Overrides [StatisticsState.model\_config](https://crawlee.dev/python/python/api/class/StatisticsState.md#model_config)

### [**](#rendering_type_mispredictions)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler_statistics.py#L23)rendering\_type\_mispredictions

**rendering\_type\_mispredictions: int

Number representing how many times the predictor gave incorrect prediction.

### [**](#request_avg_failed_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L145)request\_avg\_failed\_duration

**request\_avg\_failed\_duration: timedelta | None

Inherited from [StatisticsState.request\_avg\_failed\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_avg_failed_duration)

### [**](#request_avg_finished_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L150)request\_avg\_finished\_duration

**request\_avg\_finished\_duration: timedelta | None

Inherited from [StatisticsState.request\_avg\_finished\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_avg_finished_duration)

### [**](#request_max_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L70)request\_max\_duration

**request\_max\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms) | None

Inherited from [StatisticsState.request\_max\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_max_duration)

### [**](#request_min_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L69)request\_min\_duration

**request\_min\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms) | None

Inherited from [StatisticsState.request\_min\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_min_duration)

### [**](#request_retry_histogram)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L97)request\_retry\_histogram

**request\_retry\_histogram: dict\[int, int]

Inherited from [StatisticsState.request\_retry\_histogram](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_retry_histogram)

### [**](#request_total_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L140)request\_total\_duration

**request\_total\_duration: timedelta

Inherited from [StatisticsState.request\_total\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_total_duration)

### [**](#request_total_failed_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L71)request\_total\_failed\_duration

**request\_total\_failed\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms)

Inherited from [StatisticsState.request\_total\_failed\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_total_failed_duration)

### [**](#request_total_finished_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L74)request\_total\_finished\_duration

**request\_total\_finished\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms)

Inherited from [StatisticsState.request\_total\_finished\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_total_finished_duration)

### [**](#requests_failed)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L65)requests\_failed

**requests\_failed: int

Inherited from [StatisticsState.requests\_failed](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_failed)

### [**](#requests_failed_per_minute)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L67)requests\_failed\_per\_minute

**requests\_failed\_per\_minute: float

Inherited from [StatisticsState.requests\_failed\_per\_minute](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_failed_per_minute)

### [**](#requests_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L64)requests\_finished

**requests\_finished: int

Inherited from [StatisticsState.requests\_finished](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_finished)

### [**](#requests_finished_per_minute)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L68)requests\_finished\_per\_minute

**requests\_finished\_per\_minute: float

Inherited from [StatisticsState.requests\_finished\_per\_minute](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_finished_per_minute)

### [**](#requests_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L66)requests\_retries

**requests\_retries: int

Inherited from [StatisticsState.requests\_retries](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_retries)

### [**](#requests_total)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L155)requests\_total

**requests\_total: int

Inherited from [StatisticsState.requests\_total](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_total)

### [**](#stats_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L62)stats\_id

**stats\_id: int | None

Inherited from [StatisticsState.stats\_id](https://crawlee.dev/python/python/api/class/StatisticsState.md#stats_id)

### [**](#stats_persisted_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L94)stats\_persisted\_at

**stats\_persisted\_at: datetime | None

Inherited from [StatisticsState.stats\_persisted\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#stats_persisted_at)


---

# AdaptivePlaywrightCrawlingContext<!-- -->

### Hierarchy

* [ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)
  * *AdaptivePlaywrightCrawlingContext*

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#create_modified_copy)
* [**from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#from_basic_crawling_context)
* [**from\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#from_http_crawling_context)
* [**from\_parsed\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#from_parsed_http_crawling_context)
* [**from\_playwright\_crawling\_context](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#from_playwright_crawling_context)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#get_snapshot)
* [**parse\_with\_static\_parser](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#parse_with_static_parser)
* [**query\_selector\_all](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#query_selector_all)
* [**query\_selector\_one](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#query_selector_one)
* [**wait\_for\_selector](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#wait_for_selector)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#add_requests)
* [**enqueue\_links](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#enqueue_links)
* [**extract\_links](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#extract_links)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#get_key_value_store)
* [**http\_response](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#http_response)
* [**infinite\_scroll](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#infinite_scroll)
* [**log](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#log)
* [**page](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#page)
* [**parsed\_content](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#parsed_content)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#request)
* [**response](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#response)
* [**send\_request](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#use_state)

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

- Inherited from [HttpCrawlingContext.from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#from_basic_crawling_context)

  Initialize a new instance from an existing `BasicCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)
  * ##### http\_response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  #### Returns Self

### [**](#from_http_crawling_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L45)from\_http\_crawling\_context

* ****from\_http\_crawling\_context**(context, parsed\_content, enqueue\_links, extract\_links): Self

- Inherited from [ParsedHttpCrawlingContext.from\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#from_http_crawling_context)

  Initialize a new instance from an existing `HttpCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md)
  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)
  * ##### enqueue\_links: [EnqueueLinksFunction](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)
  * ##### extract\_links: [ExtractLinksFunction](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md)

  #### Returns Self

### [**](#from_parsed_http_crawling_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L170)from\_parsed\_http\_crawling\_context

* ****from\_parsed\_http\_crawling\_context**(context, parser): [AdaptivePlaywrightCrawlingContext](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult), [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

- Initialize a new instance from an existing `ParsedHttpCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult)]
  * ##### parser: [AbstractHttpParser](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult), [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

  #### Returns [AdaptivePlaywrightCrawlingContext](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult), [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

### [**](#from_playwright_crawling_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L179)from\_playwright\_crawling\_context

* **async **from\_playwright\_crawling\_context**(context, parser): [AdaptivePlaywrightCrawlingContext](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult), [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

- Initialize a new instance from an existing `PlaywrightCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [PlaywrightCrawlingContext](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md)
  * ##### parser: [AbstractHttpParser](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult), [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

  #### Returns [AdaptivePlaywrightCrawlingContext](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md)\[[TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult), [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L27)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Inherited from [HttpCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#get_snapshot)

  Overrides [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

  Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

### [**](#parse_with_static_parser)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L149)parse\_with\_static\_parser

* **async **parse\_with\_static\_parser**(selector, timeout): [TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult)

- Parse whole page with static parser. If `selector` argument is used, wait for selector first.

  If element is not found within timeout, TimeoutError is raised.

  ***

  #### Parameters

  * ##### optionalselector: str | None = <!-- -->None

    css selector to be used to locate specific element on page.

  * ##### optionaltimeout: timedelta = <!-- -->timedelta(seconds=5)

    timeout that defines how long the function wait for the selector to appear.

  #### Returns [TStaticParseResult](https://crawlee.dev/python/python/api.md#TStaticParseResult)

  Result of used static parser `parse_text` method.

### [**](#query_selector_all)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L111)query\_selector\_all

* **async **query\_selector\_all**(selector, timeout): Sequence\[[TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

- Locate element by css selector and return all elements found.

  If element is not found within timeout, `TimeoutError` is raised.

  ***

  #### Parameters

  * ##### selector: str

    Css selector to be used to locate specific element on page.

  * ##### optionaltimeout: timedelta = <!-- -->timedelta(seconds=5)

    Timeout that defines how long the function wait for the selector to appear.

  #### Returns Sequence\[[TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult)]

  List of results of used static parser `select` method.

### [**](#query_selector_one)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L93)query\_selector\_one

* **async **query\_selector\_one**(selector, timeout): [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult) | None

- Locate element by css selector and return first element found.

  If element is not found within timeout, `TimeoutError` is raised.

  ***

  #### Parameters

  * ##### selector: str

    Css selector to be used to locate specific element on page.

  * ##### optionaltimeout: timedelta = <!-- -->timedelta(seconds=5)

    Timeout that defines how long the function wait for the selector to appear.

  #### Returns [TStaticSelectResult](https://crawlee.dev/python/python/api.md#TStaticSelectResult) | None

  Result of used static parser `select` method.

### [**](#wait_for_selector)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L80)wait\_for\_selector

* **async **wait\_for\_selector**(selector, timeout): None

- Locate element by css selector and return `None` once it is found.

  If element is not found within timeout, `TimeoutError` is raised.

  ***

  #### Parameters

  * ##### selector: str

    Css selector to be used to locate specific element on page.

  * ##### optionaltimeout: timedelta = <!-- -->timedelta(seconds=5)

    Timeout that defines how long the function wait for the selector to appear.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L652)add\_requests

**add\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md)

Inherited from [BasicCrawlingContext.add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#add_requests)

Add requests crawling context helper function.

### [**](#enqueue_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L41)enqueue\_links

**enqueue\_links: [EnqueueLinksFunction](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)

Inherited from [ParsedHttpCrawlingContext.enqueue\_links](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#enqueue_links)

### [**](#extract_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L42)extract\_links

**extract\_links: [ExtractLinksFunction](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md)

Inherited from [ParsedHttpCrawlingContext.extract\_links](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#extract_links)

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L661)get\_key\_value\_store

**get\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md)

Inherited from [BasicCrawlingContext.get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_key_value_store)

Get key-value store crawling context helper function.

### [**](#http_response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/http_clients/_base.py#L70)http\_response

**http\_response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

Inherited from [HttpCrawlingResult.http\_response](https://crawlee.dev/python/python/api/class/HttpCrawlingResult.md#http_response)

The HTTP response received from the server.

### [**](#infinite_scroll)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L60)infinite\_scroll

**infinite\_scroll: Callable\[\[], Awaitable\[None]]

A function to perform infinite scrolling on the page.

This scrolls to the bottom, triggering the loading of additional content if present. Raises `AdaptiveContextError` if accessed during static crawling.

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L664)log

**log: logging.Logger

Inherited from [BasicCrawlingContext.log](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#log)

Logger instance.

### [**](#page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L50)page

**page: Page

The Playwright `Page` object for the current page.

Raises `AdaptiveContextError` if accessed during static crawling.

### [**](#parsed_content)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L40)parsed\_content

**parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

Inherited from [ParsedHttpCrawlingContext.parsed\_content](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#parsed_content)

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

### [**](#response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L71)response

**response: Response

The Playwright `Response` object containing the response details for the current URL.

Raises `AdaptiveContextError` if accessed during static crawling.

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

# AdaptivePlaywrightPostNavCrawlingContext<!-- -->

A wrapper around HttpCrawlingContext or AdaptivePlaywrightCrawlingContext.

Trying to access `page` on this context will raise AdaptiveContextError if wrapped context is HttpCrawlingContext.

### Hierarchy

* [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md)
  * *AdaptivePlaywrightPostNavCrawlingContext*

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#create_modified_copy)
* [**from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#from_basic_crawling_context)
* [**from\_post\_navigation\_context](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#from_post_navigation_context)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#add_requests)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#get_key_value_store)
* [**http\_response](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#http_response)
* [**log](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#log)
* [**page](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#page)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#request)
* [**response](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#response)
* [**send\_request](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPostNavCrawlingContext.md#use_state)

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

- Inherited from [HttpCrawlingContext.from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#from_basic_crawling_context)

  Initialize a new instance from an existing `BasicCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)
  * ##### http\_response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  #### Returns Self

### [**](#from_post_navigation_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L284)from\_post\_navigation\_context

* **async **from\_post\_navigation\_context**(context): Self

- Initialize a new instance from an existing post-navigation context.

  ***

  #### Parameters

  * ##### context: [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md) | [PlaywrightPostNavCrawlingContext](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md)

  #### Returns Self

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L27)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Inherited from [HttpCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#get_snapshot)

  Overrides [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

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

### [**](#page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L264)page

**page: Page

The Playwright `Page` object for the current page.

Raises `AdaptiveContextError` if accessed during static crawling.

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

### [**](#response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L274)response

**response: Response

The Playwright `Response` object containing the response details for the current URL.

Raises `AdaptiveContextError` if accessed during static crawling.

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

# AdaptivePlaywrightPreNavCrawlingContext<!-- -->

A wrapper around BasicCrawlingContext or AdaptivePlaywrightCrawlingContext.

Trying to access `page` on this context will raise AdaptiveContextError if wrapped context is BasicCrawlingContext.

### Hierarchy

* [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)
  * *AdaptivePlaywrightPreNavCrawlingContext*

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#create_modified_copy)
* [**from\_pre\_navigation\_context](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#from_pre_navigation_context)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#add_requests)
* [**block\_requests](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#block_requests)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#get_key_value_store)
* [**goto\_options](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#goto_options)
* [**log](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#log)
* [**page](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#page)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#request)
* [**send\_request](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md#use_state)

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

### [**](#from_pre_navigation_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L236)from\_pre\_navigation\_context

* ****from\_pre\_navigation\_context**(context): Self

- Initialize a new instance from an existing pre-navigation `BasicCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)

  #### Returns Self

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L670)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Inherited from [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

  Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

## Properties<!-- -->[**](#Properties)

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L652)add\_requests

**add\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md)

Inherited from [BasicCrawlingContext.add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#add_requests)

Add requests crawling context helper function.

### [**](#block_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L215)block\_requests

**block\_requests: [BlockRequestsFunction](https://crawlee.dev/python/python/api/class/BlockRequestsFunction.md) | None

Blocks network requests matching specified URL patterns.

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L661)get\_key\_value\_store

**get\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md)

Inherited from [BasicCrawlingContext.get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_key_value_store)

Get key-value store crawling context helper function.

### [**](#goto_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L218)goto\_options

**goto\_options: [GotoOptions](https://crawlee.dev/python/python/api/class/GotoOptions.md) | None

Additional options to pass to Playwright's `Page.goto()` method. The `timeout` option is not supported.

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L664)log

**log: logging.Logger

Inherited from [BasicCrawlingContext.log](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#log)

Logger instance.

### [**](#page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawling_context.py#L222)page

**page: Page

The Playwright `Page` object for the current page.

Raises `AdaptiveContextError` if accessed during static crawling.

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

# AddRequestsFunction<!-- -->

Function for adding requests to the `RequestManager`, with optional filtering.

It simplifies the process of adding requests to the `RequestManager`. It automatically opens the specified one and adds the provided requests.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L351)\_\_call\_\_

* ****\_\_call\_\_**(requests, rq\_id, rq\_name, rq\_alias, \*, limit, base\_url, strategy, include, exclude): Coroutine\[None, None, None]

- Call dunder method.

  ***

  #### Parameters

  * ##### requests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]

    Requests to be added to the `RequestManager`.

  * ##### optionalrq\_id: str | None = <!-- -->None

    ID of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

  * ##### optionalrq\_name: str | None = <!-- -->None

    Name of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

  * ##### optionalrq\_alias: str | None = <!-- -->None

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

# AddRequestsKwargs<!-- -->

Keyword arguments for the `add_requests` methods.

### Hierarchy

* [EnqueueLinksKwargs](https://crawlee.dev/python/python/api/class/EnqueueLinksKwargs.md)
  * *AddRequestsKwargs*

## Index[**](#Index)

### Properties

* [**base\_url](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#base_url)
* [**exclude](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#exclude)
* [**include](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#include)
* [**limit](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#limit)
* [**requests](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#requests)
* [**rq\_alias](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#rq_alias)
* [**rq\_id](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#rq_id)
* [**rq\_name](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#rq_name)
* [**strategy](https://crawlee.dev/python/python/api/class/AddRequestsKwargs.md#strategy)

## Properties<!-- -->[**](#Properties)

### [**](#base_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L153)base\_url

**base\_url: NotRequired\[str]

Inherited from EnqueueLinksKwargs.base\_url

Base URL to be used for relative URLs.

### [**](#exclude)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L174)exclude

**exclude: NotRequired\[Sequence\[re.Pattern | Glob]]

Inherited from EnqueueLinksKwargs.exclude

List of regular expressions or globs that URLs must not match to be enqueued.

### [**](#include)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L171)include

**include: NotRequired\[Sequence\[re.Pattern | Glob]]

Inherited from EnqueueLinksKwargs.include

List of regular expressions or globs that URLs must match to be enqueued.

### [**](#limit)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L150)limit

**limit: NotRequired\[int]

Inherited from EnqueueLinksKwargs.limit

Maximum number of requests to be enqueued.

### [**](#requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L181)requests

**requests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]

Requests to be added to the `RequestManager`.

### [**](#rq_alias)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L191)rq\_alias

**rq\_alias: str | None

Alias of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

### [**](#rq_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L184)rq\_id

**rq\_id: str | None

ID of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

### [**](#rq_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L187)rq\_name

**rq\_name: str | None

Name of the `RequestQueue` to add the requests to. Only one of `rq_id`, `rq_name` or `rq_alias` can be provided.

### [**](#strategy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L156)strategy

**strategy: NotRequired\[EnqueueStrategy]

Inherited from EnqueueLinksKwargs.strategy

Enqueue strategy to be used for determining which links to extract and enqueue.

Options: all: Enqueue every link encountered, regardless of the target domain. Use this option to ensure that all links, including those leading to external websites, are followed. same-domain: Enqueue links that share the same domain name as the current page, including any subdomains. This strategy is ideal for crawling within the same top-level domain while still allowing for subdomain exploration. same-hostname: Enqueue links only if they match the exact hostname of the current page. This is the default behavior and restricts the crawl to the current hostname, excluding subdomains. same-origin: Enqueue links that share the same origin as the current page. The origin is defined by the combination of protocol, domain, and port, ensuring a strict scope for the crawl.


---

# AddRequestsResponse<!-- -->

Model for a response to add requests to a queue.

Contains detailed information about the processing results when adding multiple requests to a queue. This includes which requests were successfully processed and which ones encountered issues during processing.

## Index[**](#Index)

### Properties

* [**model\_config](https://crawlee.dev/python/python/api/class/AddRequestsResponse.md#model_config)
* [**processed\_requests](https://crawlee.dev/python/python/api/class/AddRequestsResponse.md#processed_requests)
* [**unprocessed\_requests](https://crawlee.dev/python/python/api/class/AddRequestsResponse.md#unprocessed_requests)

## Properties<!-- -->[**](#Properties)

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L173)model\_config

**model\_config: Undefined

### [**](#processed_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L175)processed\_requests

**processed\_requests: list\[[ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md)]

Successfully processed requests, including information about whether they were already present in the queue and whether they had been handled previously.

### [**](#unprocessed_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L179)unprocessed\_requests

**unprocessed\_requests: list\[[UnprocessedRequest](https://crawlee.dev/python/python/api/class/UnprocessedRequest.md)]

Requests that could not be processed, typically due to validation errors or other issues.


---

# AutosavedValue<!-- -->

## Index[**](#Index)

### Properties

* [**root](https://crawlee.dev/python/python/api/class/AutosavedValue.md#root)

## Properties<!-- -->[**](#Properties)

### [**](#root)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L36)root

**root: dict\[str, JsonSerializable]


---

# AutoscaledPool<!-- -->

Manages a pool of asynchronous resource-intensive tasks that are executed in parallel.

The pool only starts new tasks if there is enough free CPU and memory available. If an exception is thrown in any of the tasks, it is propagated and the pool is stopped.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/AutoscaledPool.md#__init__)
* [**abort](https://crawlee.dev/python/python/api/class/AutoscaledPool.md#abort)
* [**pause](https://crawlee.dev/python/python/api/class/AutoscaledPool.md#pause)
* [**resume](https://crawlee.dev/python/python/api/class/AutoscaledPool.md#resume)
* [**run](https://crawlee.dev/python/python/api/class/AutoscaledPool.md#run)

### Properties

* [**current\_concurrency](https://crawlee.dev/python/python/api/class/AutoscaledPool.md#current_concurrency)
* [**desired\_concurrency](https://crawlee.dev/python/python/api/class/AutoscaledPool.md#desired_concurrency)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L64)\_\_init\_\_

* ****\_\_init\_\_**(\*, system\_status, concurrency\_settings, run\_task\_function, is\_task\_ready\_function, is\_finished\_function): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### keyword-onlysystem\_status: [SystemStatus](https://crawlee.dev/python/python/api/class/SystemStatus.md)

    Provides data about system utilization (load).

  * ##### optionalkeyword-onlyconcurrency\_settings: [ConcurrencySettings](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md) | None = <!-- -->None

    Settings of concurrency levels.

  * ##### keyword-onlyrun\_task\_function: Callable\[\[], Awaitable]

    A function that performs an asynchronous resource-intensive task.

  * ##### keyword-onlyis\_task\_ready\_function: Callable\[\[], Awaitable\[bool]]

    A function that indicates whether `run_task_function` should be called. This function is called every time there is free capacity for a new task and it should indicate whether it should start a new task or not by resolving to either `True` or `False`. Besides its obvious use, it is also useful for task throttling to save resources.

  * ##### keyword-onlyis\_finished\_function: Callable\[\[], Awaitable\[bool]]

    A function that is called only when there are no tasks to be processed. If it resolves to `True` then the pool's run finishes. Being called only when there are no tasks being processed means that as long as `is_task_ready_function` keeps resolving to `True`, `is_finished_function` will never be called. To abort a run, use the `abort` method.

  #### Returns None

### [**](#abort)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L155)abort

* **async **abort**(): None

- Interrupt the autoscaled pool and all the tasks in progress.

  ***

  #### Returns None

### [**](#pause)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L163)pause

* ****pause**(): None

- Pause the autoscaled pool so that it does not start new tasks.

  ***

  #### Returns None

### [**](#resume)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L167)resume

* ****resume**(): None

- Resume a paused autoscaled pool so that it continues starting new tasks.

  ***

  #### Returns None

### [**](#run)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L105)run

* **async **run**(): None

- Start the autoscaled pool and return when all tasks are completed and `is_finished_function` returns True.

  If there is an exception in one of the tasks, it will be re-raised.

  ***

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#current_concurrency)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L177)current\_concurrency

**current\_concurrency: int

The number of concurrent tasks in progress.

### [**](#desired_concurrency)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/autoscaled_pool.py#L172)desired\_concurrency

**desired\_concurrency: int

The current desired concurrency, possibly updated by the pool according to system load.


---

# AwareDateTime<!-- -->

Custom SQLAlchemy type for timezone-aware datetime handling.

Ensures all datetime values are timezone-aware by adding UTC timezone to naive datetime values from databases that don't store timezone information.

## Index[**](#Index)

### Methods

* [**process\_result\_value](https://crawlee.dev/python/python/api/class/AwareDateTime.md#process_result_value)

### Properties

* [**cache\_ok](https://crawlee.dev/python/python/api/class/AwareDateTime.md#cache_ok)
* [**impl](https://crawlee.dev/python/python/api/class/AwareDateTime.md#impl)

## Methods<!-- -->[**](#Methods)

### [**](#process_result_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L28)process\_result\_value

* ****process\_result\_value**(value, dialect): datetime | None

- Add UTC timezone to naive datetime values.

  ***

  #### Parameters

  * ##### value: datetime | None
  * ##### dialect: Dialect

  #### Returns datetime | None

## Properties<!-- -->[**](#Properties)

### [**](#cache_ok)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L25)cache\_ok

**cache\_ok: Undefined

### [**](#impl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L24)impl

**impl: Undefined


---

# Base<!-- -->

Base class for all database models for correct type annotations.

### Hierarchy

* *Base*

  * [DatasetMetadataDb](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md)
  * [RequestQueueMetadataDb](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md)
  * [KeyValueStoreMetadataDb](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md)
  * [KeyValueStoreRecordDb](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md)
  * [DatasetItemDb](https://crawlee.dev/python/python/api/class/DatasetItemDb.md)
  * [RequestDb](https://crawlee.dev/python/python/api/class/RequestDb.md)
  * [RequestQueueStateDb](https://crawlee.dev/python/python/api/class/RequestQueueStateDb.md)
  * [VersionDb](https://crawlee.dev/python/python/api/class/VersionDb.md)
  * [KeyValueStoreMetadataBufferDb](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md)
  * [DatasetMetadataBufferDb](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md)
  * [RequestQueueMetadataBufferDb](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md)


---

# BasicCrawler<!-- -->

A basic web crawler providing a framework for crawling websites.

The `BasicCrawler` provides a low-level functionality for crawling websites, allowing users to define their own page download and data extraction logic. It is designed mostly to be subclassed by crawlers with specific purposes. In most cases, you will want to use a more specialized crawler, such as `HttpCrawler`, `BeautifulSoupCrawler`, `ParselCrawler`, or `PlaywrightCrawler`. If you are an advanced user and want full control over the crawling process, you can subclass the `BasicCrawler` and implement the request-handling logic yourself.

The crawling process begins with URLs provided by a `RequestProvider` instance. Each request is then handled by a user-defined `request_handler` function, which processes the page and extracts the data.

The `BasicCrawler` includes several common features for crawling, such as:

* automatic scaling based on the system resources,
* retries for failed requests,
* session management,
* statistics tracking,
* request routing via labels,
* proxy rotation,
* direct storage interaction helpers,
* and more.

### Hierarchy

* *BasicCrawler*

  * [PlaywrightCrawler](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md)
  * [AdaptivePlaywrightCrawler](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md)
  * [AbstractHttpCrawler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md)

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/BasicCrawler.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawler.md#add_requests)
* [**error\_handler](https://crawlee.dev/python/python/api/class/BasicCrawler.md#error_handler)
* [**export\_data](https://crawlee.dev/python/python/api/class/BasicCrawler.md#export_data)
* [**failed\_request\_handler](https://crawlee.dev/python/python/api/class/BasicCrawler.md#failed_request_handler)
* [**get\_data](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_data)
* [**get\_dataset](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_dataset)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_key_value_store)
* [**get\_request\_manager](https://crawlee.dev/python/python/api/class/BasicCrawler.md#get_request_manager)
* [**on\_skipped\_request](https://crawlee.dev/python/python/api/class/BasicCrawler.md#on_skipped_request)
* [**router](https://crawlee.dev/python/python/api/class/BasicCrawler.md#router)
* [**run](https://crawlee.dev/python/python/api/class/BasicCrawler.md#run)
* [**stop](https://crawlee.dev/python/python/api/class/BasicCrawler.md#stop)
* [**use\_state](https://crawlee.dev/python/python/api/class/BasicCrawler.md#use_state)

### Properties

* [**log](https://crawlee.dev/python/python/api/class/BasicCrawler.md#log)
* [**router](https://crawlee.dev/python/python/api/class/BasicCrawler.md#router)
* [**statistics](https://crawlee.dev/python/python/api/class/BasicCrawler.md#statistics)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L275)\_\_init\_\_

* ****\_\_init\_\_**(\*, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, request\_handler, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, concurrency\_settings, request\_handler\_timeout, statistics, abort\_on\_error, keep\_alive, configure\_logging, statistics\_log\_format, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id, \_context\_pipeline, \_additional\_context\_managers, \_logger): None

- Overrides [BasicCrawler.\_\_init\_\_](https://crawlee.dev/python/python/api/class/BasicCrawler.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

    The `Configuration` instance. Some of its properties are used as defaults for the crawler.

  * ##### optionalkeyword-onlyevent\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md) | None = <!-- -->None

    The event manager for managing events for the crawler and all its components.

  * ##### optionalkeyword-onlystorage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None = <!-- -->None

    The storage client for managing storages for the crawler and all its components.

  * ##### optionalkeyword-onlyrequest\_manager: [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md) | None = <!-- -->None

    Manager of requests that should be processed by the crawler.

  * ##### optionalkeyword-onlysession\_pool: [SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md) | None = <!-- -->None

    A custom `SessionPool` instance, allowing the use of non-default configuration.

  * ##### optionalkeyword-onlyproxy\_configuration: [ProxyConfiguration](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md) | None = <!-- -->None

    HTTP proxy configuration used when making requests.

  * ##### optionalkeyword-onlyhttp\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md) | None = <!-- -->None

    HTTP client used by `BasicCrawlingContext.send_request` method.

  * ##### optionalkeyword-onlyrequest\_handler: Callable\[\[TCrawlingContext], Awaitable\[None]] | None = <!-- -->None

    A callable responsible for handling requests.

  * ##### optionalkeyword-onlymax\_request\_retries: int = <!-- -->3

    Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.). This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

  * ##### optionalkeyword-onlymax\_requests\_per\_crawl: int | None = <!-- -->None

    Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value. If used together with `keep_alive`, then the crawler will be kept alive only until `max_requests_per_crawl` is achieved.

  * ##### optionalkeyword-onlymax\_session\_rotations: int = <!-- -->10

    Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request. The session rotations are not counted towards the `max_request_retries` limit.

  * ##### optionalkeyword-onlymax\_crawl\_depth: int | None = <!-- -->None

    Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

  * ##### optionalkeyword-onlyuse\_session\_pool: bool = <!-- -->True

    Enable the use of a session pool for managing sessions during crawling.

  * ##### optionalkeyword-onlyretry\_on\_blocked: bool = <!-- -->True

    If True, the crawler attempts to bypass bot protections automatically.

  * ##### optionalkeyword-onlyadditional\_http\_error\_status\_codes: Iterable\[int] | None = <!-- -->None

    Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

  * ##### optionalkeyword-onlyignore\_http\_error\_status\_codes: Iterable\[int] | None = <!-- -->None

    HTTP status codes that are typically considered errors but should be treated as successful responses.

  * ##### optionalkeyword-onlyconcurrency\_settings: [ConcurrencySettings](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md) | None = <!-- -->None

    Settings to fine-tune concurrency levels.

  * ##### optionalkeyword-onlyrequest\_handler\_timeout: timedelta = <!-- -->timedelta(minutes=1)

    Maximum duration allowed for a single request handler to run.

  * ##### optionalkeyword-onlystatistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[TStatisticsState](https://crawlee.dev/python/python/api.md#TStatisticsState)] | None = <!-- -->None

    A custom `Statistics` instance, allowing the use of non-default configuration.

  * ##### optionalkeyword-onlyabort\_on\_error: bool = <!-- -->False

    If True, the crawler stops immediately when any request handler error occurs.

  * ##### optionalkeyword-onlykeep\_alive: bool = <!-- -->False

    If True, it will keep crawler alive even if there are no requests in queue. Use `crawler.stop()` to exit the crawler.

  * ##### optionalkeyword-onlyconfigure\_logging: bool = <!-- -->True

    If True, the crawler will set up logging infrastructure automatically.

  * ##### optionalkeyword-onlystatistics\_log\_format: Literal\[table, inline] = <!-- -->'table'

    If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

  * ##### optionalkeyword-onlyrespect\_robots\_txt\_file: bool = <!-- -->False

    If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`

  * ##### optionalkeyword-onlystatus\_message\_logging\_interval: timedelta = <!-- -->timedelta(seconds=10)

    Interval for logging the crawler status messages.

  * ##### optionalkeyword-onlystatus\_message\_callback: Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]] | None = <!-- -->None

    Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

  * ##### optionalkeyword-onlyid: int | None = <!-- -->None

    Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

  * ##### optionalkeyword-only\_context\_pipeline: [ContextPipeline](https://crawlee.dev/python/python/api/class/ContextPipeline.md)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)] | None = <!-- -->None

    Enables extending the request lifecycle and modifying the crawling context. Intended for use by subclasses rather than direct instantiation of `BasicCrawler`.

  * ##### optionalkeyword-only\_additional\_context\_managers: Sequence\[AbstractAsyncContextManager] | None = <!-- -->None

    Additional context managers used throughout the crawler lifecycle. Intended for use by subclasses rather than direct instantiation of `BasicCrawler`.

  * ##### optionalkeyword-only\_logger: logging.Logger | None = <!-- -->None

    A logger instance, typically provided by a subclass, for consistent logging labels. Intended for use by subclasses rather than direct instantiation of `BasicCrawler`.

  #### Returns None

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L804)add\_requests

* **async **add\_requests**(requests, \*, forefront, batch\_size, wait\_time\_between\_batches, wait\_for\_all\_requests\_to\_be\_added, wait\_for\_all\_requests\_to\_be\_added\_timeout): None

- Add requests to the underlying request manager in batches.

  ***

  #### Parameters

  * ##### requests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]

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

### [**](#error_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L655)error\_handler

* ****error\_handler**(handler): [ErrorHandler](https://crawlee.dev/python/python/api.md#ErrorHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

- Register a function to handle errors occurring in request handlers.

  The error handler is invoked after a request handler error occurs and before a retry attempt.

  ***

  #### Parameters

  * ##### handler: [ErrorHandler](https://crawlee.dev/python/python/api.md#ErrorHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext) | [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)]

  #### Returns [ErrorHandler](https://crawlee.dev/python/python/api.md#ErrorHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

### [**](#export_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L893)export\_data

* **async **export\_data**(path, dataset\_id, dataset\_name, dataset\_alias): None

- Export all items from a Dataset to a JSON or CSV file.

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

  #### Returns None

### [**](#failed_request_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L665)failed\_request\_handler

* ****failed\_request\_handler**(handler): [FailedRequestHandler](https://crawlee.dev/python/python/api.md#FailedRequestHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

- Register a function to handle requests that exceed the maximum retry limit.

  The failed request handler is invoked when a request has failed all retry attempts.

  ***

  #### Parameters

  * ##### handler: [FailedRequestHandler](https://crawlee.dev/python/python/api.md#FailedRequestHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext) | [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)]

  #### Returns [FailedRequestHandler](https://crawlee.dev/python/python/api.md#FailedRequestHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L863)get\_data

* **async **get\_data**(dataset\_id, dataset\_name, dataset\_alias, \*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden, flatten, view): [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

- Retrieve data from a `Dataset`.

  This helper method simplifies the process of retrieving data from a `Dataset`. It opens the specified one and then retrieves the data based on the provided parameters.

  ***

  #### Parameters

  * ##### optionaldataset\_id: str | None = <!-- -->None

    The ID of the `Dataset`.

  * ##### optionaldataset\_name: str | None = <!-- -->None

    The name of the `Dataset` (global scope, named storage).

  * ##### optionaldataset\_alias: str | None = <!-- -->None

    The alias of the `Dataset` (run scope, unnamed storage).

  * ##### keyword-onlyoptionaloffset: int

    Skips the specified number of items at the start.

  * ##### keyword-onlyoptionallimit: int | None

    The maximum number of items to retrieve. Unlimited if None.

  * ##### keyword-onlyoptionalclean: bool

    Return only non-empty items and excludes hidden fields. Shortcut for `skip_hidden` and `skip_empty`.

  * ##### keyword-onlyoptionaldesc: bool

    Set to True to sort results in descending order.

  * ##### keyword-onlyoptionalfields: list\[str]

    Fields to include in each item. Sorts fields as specified if provided.

  * ##### keyword-onlyoptionalomit: list\[str]

    Fields to exclude from each item.

  * ##### keyword-onlyoptionalunwind: list\[str]

    Unwinds items by a specified array field, turning each element into a separate item.

  * ##### keyword-onlyoptionalskip\_empty: bool

    Excludes empty items from the results if True.

  * ##### keyword-onlyoptionalskip\_hidden: bool

    Excludes fields starting with '#' if True.

  * ##### keyword-onlyoptionalflatten: list\[str]

    Fields to be flattened in returned items.

  * ##### keyword-onlyoptionalview: str

    Specifies the dataset view to be used.

  #### Returns [DatasetItemsListPage](https://crawlee.dev/python/python/api/class/DatasetItemsListPage.md)

  The retrieved data.

### [**](#get_dataset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L623)get\_dataset

* **async **get\_dataset**(\*, id, name, alias): [Dataset](https://crawlee.dev/python/python/api/class/Dataset.md)

- Return the `Dataset` with the given ID or name. If none is provided, return the default one.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

  #### Returns [Dataset](https://crawlee.dev/python/python/api/class/Dataset.md)

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L639)get\_key\_value\_store

* **async **get\_key\_value\_store**(\*, id, name, alias): [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)

- Return the `KeyValueStore` with the given ID or name. If none is provided, return the default KVS.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

  #### Returns [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)

### [**](#get_request_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L613)get\_request\_manager

* **async **get\_request\_manager**(): [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

- Return the configured request manager. If none is configured, open and return the default request queue.

  ***

  #### Returns [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

### [**](#on_skipped_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L675)on\_skipped\_request

* ****on\_skipped\_request**(callback): [SkippedRequestCallback](https://crawlee.dev/python/python/api.md#SkippedRequestCallback)

- Register a function to handle skipped requests.

  The skipped request handler is invoked when a request is skipped due to a collision or other reasons.

  ***

  #### Parameters

  * ##### callback: [SkippedRequestCallback](https://crawlee.dev/python/python/api.md#SkippedRequestCallback)

  #### Returns [SkippedRequestCallback](https://crawlee.dev/python/python/api.md#SkippedRequestCallback)

### [**](#router)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L524)router

* ****router**(router): None

- #### Parameters

  * ##### router: [Router](https://crawlee.dev/python/python/api/class/Router.md)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

  #### Returns None

### [**](#run)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L683)run

* **async **run**(requests, \*, purge\_request\_queue): [FinalStatistics](https://crawlee.dev/python/python/api/class/FinalStatistics.md)

- Run the crawler until all requests are processed.

  ***

  #### Parameters

  * ##### optionalrequests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)] | None = <!-- -->None

    The requests to be enqueued before the crawler starts.

  * ##### optionalkeyword-onlypurge\_request\_queue: bool = <!-- -->True

    If this is `True` and the crawler is not being run for the first time, the default request queue will be purged.

  #### Returns [FinalStatistics](https://crawlee.dev/python/python/api/class/FinalStatistics.md)

### [**](#stop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L535)stop

* ****stop**(reason): None

- Set flag to stop crawler.

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

The logger used by the crawler.

### [**](#router)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L516)router

**router: [Router](https://crawlee.dev/python/python/api/class/Router.md)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

The `Router` used to handle each individual crawling request.

### [**](#statistics)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L531)statistics

**statistics: [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[TStatisticsState](https://crawlee.dev/python/python/api.md#TStatisticsState)]

Statistics about the current (or last) crawler run.


---

# BasicCrawlerOptions<!-- -->

Arguments for the `BasicCrawler` constructor.

It is intended for typing forwarded `__init__` arguments in the subclasses.

### Hierarchy

* [\_BasicCrawlerOptionsGeneric](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptionsGeneric.md)

* [\_BasicCrawlerOptions](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptions.md)

  * *BasicCrawlerOptions*

    * [PlaywrightCrawlerOptions](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md)
    * [HttpCrawlerOptions](https://crawlee.dev/python/python/api/class/HttpCrawlerOptions.md)

## Index[**](#Index)

### Properties

* [**abort\_on\_error](#abort_on_error)
* [**additional\_http\_error\_status\_codes](#additional_http_error_status_codes)
* [**concurrency\_settings](#concurrency_settings)
* [**configuration](#configuration)
* [**configure\_logging](#configure_logging)
* [**event\_manager](#event_manager)
* [**http\_client](#http_client)
* [**id](#id)
* [**ignore\_http\_error\_status\_codes](#ignore_http_error_status_codes)
* [**keep\_alive](#keep_alive)
* [**max\_crawl\_depth](#max_crawl_depth)
* [**max\_request\_retries](#max_request_retries)
* [**max\_requests\_per\_crawl](#max_requests_per_crawl)
* [**max\_session\_rotations](#max_session_rotations)
* [**proxy\_configuration](#proxy_configuration)
* [**request\_handler](#request_handler)
* [**request\_handler\_timeout](#request_handler_timeout)
* [**request\_manager](#request_manager)
* [**respect\_robots\_txt\_file](#respect_robots_txt_file)
* [**retry\_on\_blocked](#retry_on_blocked)
* [**session\_pool](#session_pool)
* [**statistics](#statistics)
* [**statistics\_log\_format](#statistics_log_format)
* [**status\_message\_callback](#status_message_callback)
* [**status\_message\_logging\_interval](#status_message_logging_interval)
* [**storage\_client](#storage_client)
* [**use\_session\_pool](#use_session_pool)

## Properties<!-- -->[**](#Properties)

### [**](#abort_on_error)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L175)keyword-onlyoptionalabort\_on\_error

**abort\_on\_error: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.abort\_on\_error

If True, the crawler stops immediately when any request handler error occurs.

### [**](#additional_http_error_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L189)keyword-onlyoptionaladditional\_http\_error\_status\_codes

**additional\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

Inherited from \_BasicCrawlerOptions.additional\_http\_error\_status\_codes

Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

### [**](#concurrency_settings)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L169)keyword-onlyoptionalconcurrency\_settings

**concurrency\_settings: NotRequired\[ConcurrencySettings]

Inherited from \_BasicCrawlerOptions.concurrency\_settings

Settings to fine-tune concurrency levels.

### [**](#configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L116)keyword-onlyoptionalconfiguration

**configuration: NotRequired\[Configuration]

Inherited from \_BasicCrawlerOptions.configuration

The `Configuration` instance. Some of its properties are used as defaults for the crawler.

### [**](#configure_logging)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L178)keyword-onlyoptionalconfigure\_logging

**configure\_logging: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.configure\_logging

If True, the crawler will set up logging infrastructure automatically.

### [**](#event_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L119)keyword-onlyoptionalevent\_manager

**event\_manager: NotRequired\[EventManager]

Inherited from \_BasicCrawlerOptions.event\_manager

The event manager for managing events for the crawler and all its components.

### [**](#http_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L134)keyword-onlyoptionalhttp\_client

**http\_client: NotRequired\[HttpClient]

Inherited from \_BasicCrawlerOptions.http\_client

HTTP client used by `BasicCrawlingContext.send_request` method.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L216)keyword-onlyoptionalid

**id: NotRequired\[int]

Inherited from \_BasicCrawlerOptions.id

Identifier used for crawler state tracking. Use the same id across multiple crawlers to share state between them.

### [**](#ignore_http_error_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L192)keyword-onlyoptionalignore\_http\_error\_status\_codes

**ignore\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

Inherited from \_BasicCrawlerOptions.ignore\_http\_error\_status\_codes

HTTP status codes that are typically considered errors but should be treated as successful responses.

### [**](#keep_alive)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L186)keyword-onlyoptionalkeep\_alive

**keep\_alive: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.keep\_alive

Flag that can keep crawler running even when there are no requests in queue.

### [**](#max_crawl_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L156)keyword-onlyoptionalmax\_crawl\_depth

**max\_crawl\_depth: NotRequired\[int | None]

Inherited from \_BasicCrawlerOptions.max\_crawl\_depth

Specifies the maximum crawl depth. If set, the crawler will stop processing links beyond this depth. The crawl depth starts at 0 for initial requests and increases with each subsequent level of links. Requests at the maximum depth will still be processed, but no new links will be enqueued from those requests. If not set, crawling continues without depth restrictions.

### [**](#max_request_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L137)keyword-onlyoptionalmax\_request\_retries

**max\_request\_retries: NotRequired\[int]

Inherited from \_BasicCrawlerOptions.max\_request\_retries

Specifies the maximum number of retries allowed for a request if its processing fails. This includes retries due to navigation errors or errors thrown from user-supplied functions (`request_handler`, `pre_navigation_hooks` etc.).

This limit does not apply to retries triggered by session rotation (see `max_session_rotations`).

### [**](#max_requests_per_crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L144)keyword-onlyoptionalmax\_requests\_per\_crawl

**max\_requests\_per\_crawl: NotRequired\[int | None]

Inherited from \_BasicCrawlerOptions.max\_requests\_per\_crawl

Maximum number of pages to open during a crawl. The crawl stops upon reaching this limit. Setting this value can help avoid infinite loops in misconfigured crawlers. `None` means no limit. Due to concurrency settings, the actual number of pages visited may slightly exceed this value.

### [**](#max_session_rotations)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L149)keyword-onlyoptionalmax\_session\_rotations

**max\_session\_rotations: NotRequired\[int]

Inherited from \_BasicCrawlerOptions.max\_session\_rotations

Maximum number of session rotations per request. The crawler rotates the session if a proxy error occurs or if the website blocks the request.

The session rotations are not counted towards the `max_request_retries` limit.

### [**](#proxy_configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L131)keyword-onlyoptionalproxy\_configuration

**proxy\_configuration: NotRequired\[ProxyConfiguration]

Inherited from \_BasicCrawlerOptions.proxy\_configuration

HTTP proxy configuration used when making requests.

### [**](#request_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L224)keyword-onlyoptionalrequest\_handler

**request\_handler: NotRequired\[Callable\[\[TCrawlingContext], Awaitable\[None]]]

Inherited from [\_BasicCrawlerOptionsGeneric.request\_handler](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptionsGeneric.md#request_handler)

A callable responsible for handling requests.

### [**](#request_handler_timeout)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L172)keyword-onlyoptionalrequest\_handler\_timeout

**request\_handler\_timeout: NotRequired\[timedelta]

Inherited from \_BasicCrawlerOptions.request\_handler\_timeout

Maximum duration allowed for a single request handler to run.

### [**](#request_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L125)keyword-onlyoptionalrequest\_manager

**request\_manager: NotRequired\[RequestManager]

Inherited from \_BasicCrawlerOptions.request\_manager

Manager of requests that should be processed by the crawler.

### [**](#respect_robots_txt_file)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L203)keyword-onlyoptionalrespect\_robots\_txt\_file

**respect\_robots\_txt\_file: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.respect\_robots\_txt\_file

If set to `True`, the crawler will automatically try to fetch the robots.txt file for each domain, and skip those that are not allowed. This also prevents disallowed URLs to be added via `EnqueueLinksFunction`.

### [**](#retry_on_blocked)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L166)keyword-onlyoptionalretry\_on\_blocked

**retry\_on\_blocked: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.retry\_on\_blocked

If True, the crawler attempts to bypass bot protections automatically.

### [**](#session_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L128)keyword-onlyoptionalsession\_pool

**session\_pool: NotRequired\[SessionPool]

Inherited from \_BasicCrawlerOptions.session\_pool

A custom `SessionPool` instance, allowing the use of non-default configuration.

### [**](#statistics)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L231)keyword-onlyoptionalstatistics

**statistics: NotRequired\[Statistics\[TStatisticsState]]

Inherited from [\_BasicCrawlerOptionsGeneric.statistics](https://crawlee.dev/python/python/api/class/_BasicCrawlerOptionsGeneric.md#statistics)

A custom `Statistics` instance, allowing the use of non-default configuration.

### [**](#statistics_log_format)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L181)keyword-onlyoptionalstatistics\_log\_format

**statistics\_log\_format: NotRequired\[Literal\['table', 'inline']]

Inherited from \_BasicCrawlerOptions.statistics\_log\_format

If 'table', displays crawler statistics as formatted tables in logs. If 'inline', outputs statistics as plain text log messages.

### [**](#status_message_callback)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L210)keyword-onlyoptionalstatus\_message\_callback

**status\_message\_callback: NotRequired\[ Callable\[\[StatisticsState, StatisticsState | None, str], Awaitable\[str | None]] ]

Inherited from \_BasicCrawlerOptions.status\_message\_callback

Allows overriding the default status message. The default status message is provided in the parameters. Returning `None` suppresses the status message.

### [**](#status_message_logging_interval)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L207)keyword-onlyoptionalstatus\_message\_logging\_interval

**status\_message\_logging\_interval: NotRequired\[timedelta]

Inherited from \_BasicCrawlerOptions.status\_message\_logging\_interval

Interval for logging the crawler status messages.

### [**](#storage_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L122)keyword-onlyoptionalstorage\_client

**storage\_client: NotRequired\[StorageClient]

Inherited from \_BasicCrawlerOptions.storage\_client

The storage client for managing storages for the crawler and all its components.

### [**](#use_session_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L163)keyword-onlyoptionaluse\_session\_pool

**use\_session\_pool: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.use\_session\_pool

Enable the use of a session pool for managing sessions during crawling.


---

# BasicCrawlingContext<!-- -->

Basic crawling context.

It represents the fundamental crawling context used by the `BasicCrawler`. It is extended by more specific crawlers to provide additional functionality.

### Hierarchy

* *BasicCrawlingContext*

  * [PlaywrightPreNavCrawlingContext](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md)
  * [AdaptivePlaywrightPreNavCrawlingContext](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md)
  * [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md)

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#create_modified_copy)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#add_requests)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_key_value_store)
* [**log](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#log)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#request)
* [**send\_request](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#use_state)

## Methods<!-- -->[**](#Methods)

### [**](#__hash__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L674)\_\_hash\_\_

* ****\_\_hash\_\_**(): int

- Return hash of the context. Each context is considered unique.

  ***

  #### Returns int

### [**](#create_modified_copy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L678)create\_modified\_copy

* ****create\_modified\_copy**(push\_data, add\_requests, get\_key\_value\_store): Self

- Create a modified copy of the crawling context with specified changes.

  ***

  #### Parameters

  * ##### optionalpush\_data: [PushDataFunction](https://crawlee.dev/python/python/api/class/PushDataFunction.md) | None = <!-- -->None
  * ##### optionaladd\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md) | None = <!-- -->None
  * ##### optionalget\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md) | None = <!-- -->None

  #### Returns Self

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L670)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

## Properties<!-- -->[**](#Properties)

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L652)add\_requests

**add\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md)

Add requests crawling context helper function.

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L661)get\_key\_value\_store

**get\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md)

Get key-value store crawling context helper function.

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L664)log

**log: logging.Logger

Logger instance.

### [**](#proxy_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L646)proxy\_info

**proxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None

Proxy information for the current page being processed.

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L655)push\_data

**push\_data: [PushDataFunction](https://crawlee.dev/python/python/api/class/PushDataFunction.md)

Push data crawling context helper function.

### [**](#register_deferred_cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L667)register\_deferred\_cleanup

**register\_deferred\_cleanup: Callable\[\[DeferredCleanupCallback], None]

Register an async callback to be called after request processing completes (including error handlers).

### [**](#request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L640)request

**request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

Request object for the current page being processed.

### [**](#send_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L649)send\_request

**send\_request: [SendRequestFunction](https://crawlee.dev/python/python/api/class/SendRequestFunction.md)

Send request crawling context helper function.

### [**](#session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L643)session

**session: [Session](https://crawlee.dev/python/python/api/class/Session.md) | None

Session object for the current page being processed.

### [**](#use_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L658)use\_state

**use\_state: [UseStateFunction](https://crawlee.dev/python/python/api/class/UseStateFunction.md)

Use state crawling context helper function.


---

# BeautifulSoupCrawler<!-- -->

A web crawler for performing HTTP requests and parsing HTML/XML content.

The `BeautifulSoupCrawler` builds on top of the `AbstractHttpCrawler`, which means it inherits all of its features. It specifies its own parser `BeautifulSoupParser` which is used to parse `HttpResponse`. `BeautifulSoupParser` uses following library for parsing: <https://pypi.org/project/beautifulsoup4/>

The HTTP client-based crawlers are ideal for websites that do not require JavaScript execution. However, if you need to execute client-side JavaScript, consider using browser-based crawler like the `PlaywrightCrawler`.

### Usage

```
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext

crawler = BeautifulSoupCrawler()

# Define the default request handler, which will be called for every request.
@crawler.router.default_handler
async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
    context.log.info(f'Processing {context.request.url} ...')

    # Extract data from the page.
    data = {
        'url': context.request.url,
        'title': context.soup.title.string if context.soup.title else None,
    }

    # Push the extracted data to the default dataset.
    await context.push_data(data)

await crawler.run(['https://crawlee.dev/'])
```

### Hierarchy

* [AbstractHttpCrawler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md)
  * *BeautifulSoupCrawler*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#add_requests)
* [**create\_parsed\_http\_crawler\_class](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#create_parsed_http_crawler_class)
* [**error\_handler](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#error_handler)
* [**export\_data](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#export_data)
* [**failed\_request\_handler](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#failed_request_handler)
* [**get\_data](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#get_data)
* [**get\_dataset](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#get_dataset)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#get_key_value_store)
* [**get\_request\_manager](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#get_request_manager)
* [**on\_skipped\_request](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#on_skipped_request)
* [**post\_navigation\_hook](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#post_navigation_hook)
* [**pre\_navigation\_hook](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#pre_navigation_hook)
* [**run](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#run)
* [**stop](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#stop)
* [**use\_state](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#use_state)

### Properties

* [**log](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#log)
* [**router](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#router)
* [**statistics](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md#statistics)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_crawler.py#L57)\_\_init\_\_

* ****\_\_init\_\_**(\*, parser, navigation\_timeout, request\_handler, statistics, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, concurrency\_settings, request\_handler\_timeout, abort\_on\_error, configure\_logging, statistics\_log\_format, keep\_alive, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id): None

- Overrides [AbstractHttpCrawler.\_\_init\_\_](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyparser: [BeautifulSoupParserType](https://crawlee.dev/python/python/api.md#BeautifulSoupParserType) = <!-- -->'lxml'

    The type of parser that should be used by `BeautifulSoup`.

  * ##### keyword-onlyoptionalnavigation\_timeout: timedelta | None

    Timeout for the HTTP request.

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

# BeautifulSoupCrawlingContext<!-- -->

The crawling context used by the `BeautifulSoupCrawler`.

It provides access to key objects as well as utility functions for handling crawling tasks.

### Hierarchy

* [ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)
  * *BeautifulSoupCrawlingContext*

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#create_modified_copy)
* [**from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#from_basic_crawling_context)
* [**from\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#from_http_crawling_context)
* [**from\_parsed\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#from_parsed_http_crawling_context)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#get_snapshot)
* [**html\_to\_text](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#html_to_text)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#add_requests)
* [**enqueue\_links](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#enqueue_links)
* [**extract\_links](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#extract_links)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#get_key_value_store)
* [**http\_response](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#http_response)
* [**log](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#log)
* [**parsed\_content](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#parsed_content)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#request)
* [**send\_request](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#session)
* [**soup](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#soup)
* [**use\_state](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md#use_state)

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

- Inherited from [HttpCrawlingContext.from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#from_basic_crawling_context)

  Initialize a new instance from an existing `BasicCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)
  * ##### http\_response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

  #### Returns Self

### [**](#from_http_crawling_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L45)from\_http\_crawling\_context

* ****from\_http\_crawling\_context**(context, parsed\_content, enqueue\_links, extract\_links): Self

- Inherited from [ParsedHttpCrawlingContext.from\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#from_http_crawling_context)

  Initialize a new instance from an existing `HttpCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md)
  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)
  * ##### enqueue\_links: [EnqueueLinksFunction](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)
  * ##### extract\_links: [ExtractLinksFunction](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md)

  #### Returns Self

### [**](#from_parsed_http_crawling_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_crawling_context.py#L26)from\_parsed\_http\_crawling\_context

* ****from\_parsed\_http\_crawling\_context**(context): Self

- Initialize a new instance from an existing `ParsedHttpCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[BeautifulSoup]

  #### Returns Self

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L27)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Inherited from [HttpCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#get_snapshot)

  Overrides [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

  Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

### [**](#html_to_text)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_crawling_context.py#L30)html\_to\_text

* ****html\_to\_text**(): str

- Convert the parsed HTML content to newline-separated plain text without tags.

  ***

  #### Returns str

## Properties<!-- -->[**](#Properties)

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L652)add\_requests

**add\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md)

Inherited from [BasicCrawlingContext.add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#add_requests)

Add requests crawling context helper function.

### [**](#enqueue_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L41)enqueue\_links

**enqueue\_links: [EnqueueLinksFunction](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)

Inherited from [ParsedHttpCrawlingContext.enqueue\_links](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#enqueue_links)

### [**](#extract_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L42)extract\_links

**extract\_links: [ExtractLinksFunction](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md)

Inherited from [ParsedHttpCrawlingContext.extract\_links](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#extract_links)

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

### [**](#parsed_content)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L40)parsed\_content

**parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

Inherited from [ParsedHttpCrawlingContext.parsed\_content](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#parsed_content)

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

### [**](#soup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_crawling_context.py#L21)soup

**soup: BeautifulSoup

Convenience alias.

### [**](#use_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L658)use\_state

**use\_state: [UseStateFunction](https://crawlee.dev/python/python/api/class/UseStateFunction.md)

Inherited from [BasicCrawlingContext.use\_state](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#use_state)

Use state crawling context helper function.


---

# BeautifulSoupParser<!-- -->

Parser for parsing HTTP response using `BeautifulSoup`.

### Hierarchy

* [AbstractHttpParser](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md)
  * *BeautifulSoupParser*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md#__init__)
* [**find\_links](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md#find_links)
* [**is\_blocked](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md#is_blocked)
* [**is\_matching\_selector](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md#is_matching_selector)
* [**parse](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md#parse)
* [**parse\_text](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md#parse_text)
* [**select](https://crawlee.dev/python/python/api/class/BeautifulSoupParser.md#select)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_parser.py#L22)\_\_init\_\_

* ****\_\_init\_\_**(parser): None

- #### Parameters

  * ##### optionalparser: [BeautifulSoupParserType](https://crawlee.dev/python/python/api.md#BeautifulSoupParserType) = <!-- -->'lxml'

  #### Returns None

### [**](#find_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_parser.py#L43)find\_links

* ****find\_links**(parsed\_content, selector, attribute): Iterable\[str]

- Overrides [AbstractHttpParser.find\_links](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#find_links)

  Find all links in result using selector.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Parsed HTTP response. Result of `parse` method.

  * ##### selector: str

    String used to define matching pattern for finding links.

  * ##### attribute: str

    Which node attribute to extract the links from.

  #### Returns Iterable\[str]

  Iterable of strings that contain found links.

### [**](#is_blocked)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_abstract_http_parser.py#L56)is\_blocked

* ****is\_blocked**(parsed\_content): [BlockedInfo](https://crawlee.dev/python/python/api/class/BlockedInfo.md)

- Inherited from [AbstractHttpParser.is\_blocked](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#is_blocked)

  Detect if blocked and return BlockedInfo with additional information.

  Default implementation that expects `is_matching_selector` abstract method to be implemented. Override this method if your parser has different way of blockage detection.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Parsed HTTP response. Result of `parse` method.

  #### Returns [BlockedInfo](https://crawlee.dev/python/python/api/class/BlockedInfo.md)

  `BlockedInfo` object that contains non-empty string description of reason if blockage was detected. Empty string in reason signifies no blockage detected.

### [**](#is_matching_selector)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_parser.py#L35)is\_matching\_selector

* ****is\_matching\_selector**(parsed\_content, selector): bool

- Overrides [AbstractHttpParser.is\_matching\_selector](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#is_matching_selector)

  Find if selector has match in parsed content.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Parsed HTTP response. Result of `parse` method.

  * ##### selector: str

    String used to define matching pattern.

  #### Returns bool

  True if selector has match in parsed content.

### [**](#parse)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_parser.py#L26)parse

* **async **parse**(response): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse)

  Parse HTTP response.

  ***

  #### Parameters

  * ##### response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

    HTTP response to be parsed.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed HTTP response.

### [**](#parse_text)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_parser.py#L31)parse\_text

* **async **parse\_text**(text): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse\_text](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse_text)

  Parse text containing html.

  ***

  #### Parameters

  * ##### text: str

    String containing html.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed text.

### [**](#select)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_beautifulsoup/_beautifulsoup_parser.py#L39)select

* **async **select**(parsed\_content, selector): Sequence\[[TSelectResult](https://crawlee.dev/python/python/api.md#TSelectResult)]

- Overrides [AbstractHttpParser.select](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#select)

  Use css selector to select page element and return it.

  ***

  #### Parameters

  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

    Content where the page element will be located.

  * ##### selector: str

    Css selector used to locate desired html element.

  #### Returns Sequence\[[TSelectResult](https://crawlee.dev/python/python/api.md#TSelectResult)]

  Selected element.


---

# BlockedInfo<!-- -->

Information about whether the crawling is blocked. If reason is empty, then it means it is not blocked.

## Index[**](#Index)

### Methods

* [**\_\_bool\_\_](https://crawlee.dev/python/python/api/class/BlockedInfo.md#__bool__)

### Properties

* [**reason](https://crawlee.dev/python/python/api/class/BlockedInfo.md#reason)

## Methods<!-- -->[**](#Methods)

### [**](#__bool__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_types.py#L12)\_\_bool\_\_

* ****\_\_bool\_\_**(): bool

- No reason means no blocking.

  ***

  #### Returns bool

## Properties<!-- -->[**](#Properties)

### [**](#reason)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_types.py#L10)reason

**reason: str


---

# BlockRequestsFunction<!-- -->

A function for blocking unwanted HTTP requests during page loads in PlaywrightCrawler.

It simplifies the process of blocking specific HTTP requests during page navigation. The function allows blocking both default resource types (like images, fonts, stylesheets) and custom URL patterns.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/BlockRequestsFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L26)\_\_call\_\_

* **async **\_\_call\_\_**(url\_patterns, extra\_url\_patterns): None

- Call dunder method.

  ***

  #### Parameters

  * ##### optionalurl\_patterns: list\[str] | None = <!-- -->None

    List of URL patterns to block. If None, uses default patterns.

  * ##### optionalextra\_url\_patterns: list\[str] | None = <!-- -->None

    Additional URL patterns to append to the main patterns list.

  #### Returns None


---

# BrowserController<!-- -->

An abstract base class for managing browser instance and their pages.

### Hierarchy

* *BrowserController*
  * [PlaywrightBrowserController](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md)

## Index[**](#Index)

### Methods

* [**close](https://crawlee.dev/python/python/api/class/BrowserController.md#close)
* [**new\_page](https://crawlee.dev/python/python/api/class/BrowserController.md#new_page)

### Properties

* [**AUTOMATION\_LIBRARY](https://crawlee.dev/python/python/api/class/BrowserController.md#AUTOMATION_LIBRARY)
* [**browser\_type](https://crawlee.dev/python/python/api/class/BrowserController.md#browser_type)
* [**has\_free\_capacity](https://crawlee.dev/python/python/api/class/BrowserController.md#has_free_capacity)
* [**idle\_time](https://crawlee.dev/python/python/api/class/BrowserController.md#idle_time)
* [**is\_browser\_connected](https://crawlee.dev/python/python/api/class/BrowserController.md#is_browser_connected)
* [**last\_page\_opened\_at](https://crawlee.dev/python/python/api/class/BrowserController.md#last_page_opened_at)
* [**pages](https://crawlee.dev/python/python/api/class/BrowserController.md#pages)
* [**pages\_count](https://crawlee.dev/python/python/api/class/BrowserController.md#pages_count)
* [**total\_opened\_pages](https://crawlee.dev/python/python/api/class/BrowserController.md#total_opened_pages)

## Methods<!-- -->[**](#Methods)

### [**](#close)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L89)close

* **async **close**(\*, force): None

- Close the browser.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyforce: bool = <!-- -->False

    Whether to force close all open pages before closing the browser.

  #### Returns None

### [**](#new_page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L68)new\_page

* **async **new\_page**(browser\_new\_context\_options, proxy\_info): Page

- Create a new page with the given context options.

  ***

  #### Parameters

  * ##### optionalbrowser\_new\_context\_options: Mapping\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>.

  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The proxy configuration to use for the new page.

  #### Returns Page

  Page: The newly created page.

## Properties<!-- -->[**](#Properties)

### [**](#AUTOMATION_LIBRARY)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L24)AUTOMATION\_LIBRARY

**AUTOMATION\_LIBRARY: str | None

The name of the automation library that the controller is using.

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L64)browser\_type

**browser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)

Return the type of the browser.

### [**](#has_free_capacity)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L54)has\_free\_capacity

**has\_free\_capacity: bool

Return if the browser has free capacity to open a new page.

### [**](#idle_time)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L49)idle\_time

**idle\_time: timedelta

Return the idle time of the browser controller.

### [**](#is_browser_connected)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L59)is\_browser\_connected

**is\_browser\_connected: bool

Return if the browser is closed.

### [**](#last_page_opened_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L44)last\_page\_opened\_at

**last\_page\_opened\_at: datetime

Return the time when the last page was opened.

### [**](#pages)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L29)pages

**pages: list\[Page]

Return the list of opened pages.

### [**](#pages_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L39)pages\_count

**pages\_count: int

Return the number of currently open pages.

### [**](#total_opened_pages)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_controller.py#L34)total\_opened\_pages

**total\_opened\_pages: int

Return the total number of pages opened since the browser was launched.


---

# BrowserforgeFingerprintGenerator<!-- -->

`FingerprintGenerator` adapter for fingerprint generator from `browserforge`.

`browserforge` is a browser header and fingerprint generator: <https://github.com/daijro/browserforge>

### Hierarchy

* [FingerprintGenerator](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md)
  * *BrowserforgeFingerprintGenerator*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/BrowserforgeFingerprintGenerator.md#__init__)
* [**generate](https://crawlee.dev/python/python/api/class/BrowserforgeFingerprintGenerator.md#generate)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_browserforge_adapter.py#L187)\_\_init\_\_

* ****\_\_init\_\_**(\*, header\_options, screen\_options, mock\_web\_rtc, slim): None

- Initialize a new instance.

  All generator options are optional. If any value is not specified, then `None` is set in the options. Default values for options set to `None` are implementation detail of used fingerprint generator. Specific default values should not be relied upon. Use explicit values if it matters for your use case.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyheader\_options: [HeaderGeneratorOptions](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md) | None = <!-- -->None

    Collection of header related attributes that can be used by the fingerprint generator.

  * ##### optionalkeyword-onlyscreen\_options: [ScreenOptions](https://crawlee.dev/python/python/api/class/ScreenOptions.md) | None = <!-- -->None

    Defines the screen constrains for the fingerprint generator.

  * ##### optionalkeyword-onlymock\_web\_rtc: bool | None = <!-- -->None

    Whether to mock WebRTC when injecting the fingerprint.

  * ##### optionalkeyword-onlyslim: bool | None = <!-- -->None

    Disables performance-heavy evasions when injecting the fingerprint.

  #### Returns None

### [**](#generate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_browserforge_adapter.py#L227)generate

* ****generate**(): Fingerprint

- Overrides [FingerprintGenerator.generate](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md#generate)

  Generate browser fingerprints.

  This is experimental feature. Return type is temporarily set to `Fingerprint` from `browserforge`. This is subject to change and most likely it will change to custom `Fingerprint` class defined in this repo later.

  ***

  #### Returns Fingerprint


---

# BrowserforgeHeaderGenerator<!-- -->

`HeaderGenerator` adapter for fingerprint generator from `browserforge`.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/BrowserforgeHeaderGenerator.md#__init__)
* [**generate](https://crawlee.dev/python/python/api/class/BrowserforgeHeaderGenerator.md#generate)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_browserforge_adapter.py#L245)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#generate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_browserforge_adapter.py#L248)generate

* ****generate**(browser\_type): dict\[str, str]

- Generate headers.

  ***

  #### Parameters

  * ##### optionalbrowser\_type: [SupportedBrowserType](https://crawlee.dev/python/python/api.md#SupportedBrowserType) = <!-- -->'chrome'

  #### Returns dict\[str, str]


---

# BrowserPlugin<!-- -->

An abstract base class for browser plugins.

Browser plugins act as wrappers around browser automation tools like Playwright, providing a unified interface for interacting with browsers.

### Hierarchy

* *BrowserPlugin*
  * [PlaywrightBrowserPlugin](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md)

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#__aexit__)
* [**new\_browser](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#new_browser)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#active)
* [**AUTOMATION\_LIBRARY](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#AUTOMATION_LIBRARY)
* [**browser\_launch\_options](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#browser_launch_options)
* [**browser\_new\_context\_options](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#browser_new_context_options)
* [**browser\_type](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#browser_type)
* [**max\_open\_pages\_per\_browser](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#max_open_pages_per_browser)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L65)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md)

- Overrides [BrowserPlugin.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#__aenter__)

  Enter the context manager and initialize the browser plugin.

  ***

  #### Returns [BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L73)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Overrides [BrowserPlugin.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#__aexit__)

  Exit the context manager and close the browser plugin.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#new_browser)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L86)new\_browser

* **async **new\_browser**(): [BrowserController](https://crawlee.dev/python/python/api/class/BrowserController.md)

- Overrides [BrowserPlugin.new\_browser](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#new_browser)

  Create a new browser instance.

  ***

  #### Returns [BrowserController](https://crawlee.dev/python/python/api/class/BrowserController.md)

  A new browser instance wrapped in a controller.

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L31)active

**active: bool

Indicate whether the context is active.

### [**](#AUTOMATION_LIBRARY)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L26)AUTOMATION\_LIBRARY

**AUTOMATION\_LIBRARY: str | None

The name of the automation library that the plugin is managing.

### [**](#browser_launch_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L41)browser\_launch\_options

**browser\_launch\_options: Mapping\[str, Any]

Return the options for the `browser.launch` method.

Keyword arguments to pass to the browser launch method. These options are provided directly to Playwright's `browser_type.launch` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch>.

### [**](#browser_new_context_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L51)browser\_new\_context\_options

**browser\_new\_context\_options: Mapping\[str, Any]

Return the options for the `browser.new_context` method.

Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>.

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L36)browser\_type

**browser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)

Return the browser type name.

### [**](#max_open_pages_per_browser)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_plugin.py#L61)max\_open\_pages\_per\_browser

**max\_open\_pages\_per\_browser: int

Return the maximum number of pages that can be opened in a single browser.


---

# BrowserPool<!-- -->

Manage a pool of browsers and pages, handling their lifecycle and resource allocation.

The `BrowserPool` is responsible for opening and closing browsers, managing pages within those browsers, and handling the overall lifecycle of these resources. It provides flexible configuration via constructor options, which include various hooks that allow for the insertion of custom behavior at different stages of the browser and page lifecycles.

The browsers in the pool can be in one of three states: active, inactive, or closed.

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/BrowserPool.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/BrowserPool.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/BrowserPool.md#__init__)
* [**new\_page](https://crawlee.dev/python/python/api/class/BrowserPool.md#new_page)
* [**new\_page\_with\_each\_plugin](https://crawlee.dev/python/python/api/class/BrowserPool.md#new_page_with_each_plugin)
* [**post\_page\_close\_hook](https://crawlee.dev/python/python/api/class/BrowserPool.md#post_page_close_hook)
* [**post\_page\_create\_hook](https://crawlee.dev/python/python/api/class/BrowserPool.md#post_page_create_hook)
* [**pre\_page\_close\_hook](https://crawlee.dev/python/python/api/class/BrowserPool.md#pre_page_close_hook)
* [**pre\_page\_create\_hook](https://crawlee.dev/python/python/api/class/BrowserPool.md#pre_page_create_hook)
* [**with\_default\_plugin](https://crawlee.dev/python/python/api/class/BrowserPool.md#with_default_plugin)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/BrowserPool.md#active)
* [**active\_browsers](https://crawlee.dev/python/python/api/class/BrowserPool.md#active_browsers)
* [**inactive\_browsers](https://crawlee.dev/python/python/api/class/BrowserPool.md#inactive_browsers)
* [**pages](https://crawlee.dev/python/python/api/class/BrowserPool.md#pages)
* [**plugins](https://crawlee.dev/python/python/api/class/BrowserPool.md#plugins)
* [**total\_pages\_count](https://crawlee.dev/python/python/api/class/BrowserPool.md#total_pages_count)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L199)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [BrowserPool](https://crawlee.dev/python/python/api/class/BrowserPool.md)

- Enter the context manager and initialize all browser plugins.

  ***

  #### Returns [BrowserPool](https://crawlee.dev/python/python/api/class/BrowserPool.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L223)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Exit the context manager and close all browser plugins.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L48)\_\_init\_\_

* ****\_\_init\_\_**(plugins, \*, operation\_timeout, browser\_inactive\_threshold, identify\_inactive\_browsers\_interval, close\_inactive\_browsers\_interval, retire\_browser\_after\_page\_count): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalplugins: Sequence\[[BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md)] | None = <!-- -->None

    Browser plugins serve as wrappers around various browser automation libraries, providing a consistent interface across different libraries.

  * ##### optionalkeyword-onlyoperation\_timeout: timedelta = <!-- -->timedelta(seconds=15)

    Operations of the underlying automation libraries, such as launching a browser or opening a new page, can sometimes get stuck. To prevent `BrowserPool` from becoming unresponsive, we add a timeout to these operations.

  * ##### optionalkeyword-onlybrowser\_inactive\_threshold: timedelta = <!-- -->timedelta(seconds=10)

    The period of inactivity after which a browser is considered as inactive.

  * ##### optionalkeyword-onlyidentify\_inactive\_browsers\_interval: timedelta = <!-- -->timedelta(seconds=20)

    The period of inactivity after which a browser is considered as retired.

  * ##### optionalkeyword-onlyclose\_inactive\_browsers\_interval: timedelta = <!-- -->timedelta(seconds=30)

    The interval at which the pool checks for inactive browsers and closes them. The browser is considered as inactive if it has no active pages and has been idle for the specified period. The browser is considered as retired if it has no active pages and has total pages count greater than or equal to `retire_browser_after_page_count`.

  * ##### optionalkeyword-onlyretire\_browser\_after\_page\_count: int = <!-- -->100

    The maximum number of processed pages after which the browser is considered as retired.

  #### Returns None

### [**](#new_page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L251)new\_page

* **async **new\_page**(\*, page\_id, browser\_plugin, proxy\_info): [CrawleePage](https://crawlee.dev/python/python/api/class/CrawleePage.md)

- Open a new page in a browser using the specified or a random browser plugin.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypage\_id: str | None = <!-- -->None

    The ID to assign to the new page. If not provided, a random ID is generated.

  * ##### optionalkeyword-onlybrowser\_plugin: [BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md) | None = <!-- -->None

    browser\_plugin: The browser plugin to use for creating the new page. If not provided, the next plugin in the rotation is used.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The proxy configuration to use for the new page.

  #### Returns [CrawleePage](https://crawlee.dev/python/python/api/class/CrawleePage.md)

  The newly created browser page.

### [**](#new_page_with_each_plugin)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L281)new\_page\_with\_each\_plugin

* **async **new\_page\_with\_each\_plugin**(): Sequence\[[CrawleePage](https://crawlee.dev/python/python/api/class/CrawleePage.md)]

- Create a new page with each browser plugin in the pool.

  This method is useful for running scripts in multiple environments simultaneously, typically for testing or website analysis. Each page is created using a different browser plugin, allowing you to interact with various browser types concurrently.

  ***

  #### Returns Sequence\[[CrawleePage](https://crawlee.dev/python/python/api/class/CrawleePage.md)]

  A list of newly created pages, one for each plugin in the pool.

### [**](#post_page_close_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L437)post\_page\_close\_hook

* ****post\_page\_close\_hook**(hook): Callable\[\[str, BrowserController], Awaitable\[None]]

- Register a hook to be called right after a page is closed.

  The hook receives the page ID and the `BrowserController`. Use it for cleanup or logging after a page's lifecycle ends.

  ***

  #### Parameters

  * ##### hook: Callable\[\[str, BrowserController], Awaitable\[None]]

  #### Returns Callable\[\[str, BrowserController], Awaitable\[None]]

### [**](#post_page_create_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L413)post\_page\_create\_hook

* ****post\_page\_create\_hook**(hook): Callable\[\[CrawleePage, BrowserController], Awaitable\[None]]

- Register a hook to be called right after a new page is created.

  The hook receives the newly created `CrawleePage` and the `BrowserController`. Use it to apply changes to all pages, such as injecting scripts or configuring request interception.

  ***

  #### Parameters

  * ##### hook: Callable\[\[CrawleePage, BrowserController], Awaitable\[None]]

  #### Returns Callable\[\[CrawleePage, BrowserController], Awaitable\[None]]

### [**](#pre_page_close_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L425)pre\_page\_close\_hook

* ****pre\_page\_close\_hook**(hook): Callable\[\[CrawleePage, BrowserController], Awaitable\[None]]

- Register a hook to be called just before a page is closed.

  The hook receives the `CrawleePage` and the `BrowserController`. Use it to collect last-second data, such as taking a screenshot or saving page state before the page is destroyed.

  ***

  #### Parameters

  * ##### hook: Callable\[\[CrawleePage, BrowserController], Awaitable\[None]]

  #### Returns Callable\[\[CrawleePage, BrowserController], Awaitable\[None]]

### [**](#pre_page_create_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L398)pre\_page\_create\_hook

* ****pre\_page\_create\_hook**(hook): Callable\[\[str, BrowserController, dict\[str, Any], ProxyInfo | None], Awaitable\[None]]

- Register a hook to be called just before a new page is created.

  The hook receives the page ID, `BrowserController`, `browser_new_context_options`, and `ProxyInfo`. Note that depending on the `BrowserController` implementation, `browser_new_context_options` may not apply to every page individually. For example, `PlaywrightBrowserController` with `` `use_incognito_pages=False` `` shares a single context across all pages, so the options are applied only when the context is first created.

  ***

  #### Parameters

  * ##### hook: Callable\[\[str, BrowserController, dict\[str, Any], ProxyInfo | None], Awaitable\[None]]

  #### Returns Callable\[\[str, BrowserController, dict\[str, Any], ProxyInfo | None], Awaitable\[None]]

### [**](#with_default_plugin)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L113)with\_default\_plugin

* ****with\_default\_plugin**(\*, browser\_type, user\_data\_dir, browser\_launch\_options, browser\_new\_context\_options, headless, fingerprint\_generator, use\_incognito\_pages, kwargs): [BrowserPool](https://crawlee.dev/python/python/api/class/BrowserPool.md)

- Initialize a new instance with a single `PlaywrightBrowserPlugin` configured with the provided options.

  ***

  #### Parameters

  * ##### optionalkeyword-onlybrowser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType) | None = <!-- -->None

    The type of browser to launch:

    * 'chromium', 'firefox', 'webkit': Use Playwright-managed browsers
    * 'chrome': Use your locally installed Google Chrome browser. Requires Google Chrome to be installed on the system.

  * ##### optionalkeyword-onlyuser\_data\_dir: (str | Path) | None = <!-- -->None

    Path to a user data directory, which stores browser session data like cookies and local storage.

  * ##### optionalkeyword-onlybrowser\_launch\_options: Mapping\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser launch method. These options are provided directly to Playwright's `browser_type.launch` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch>.

  * ##### optionalkeyword-onlybrowser\_new\_context\_options: Mapping\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>.

  * ##### optionalkeyword-onlyheadless: bool | None = <!-- -->None

    Whether to run the browser in headless mode.

  * ##### optionalkeyword-onlyfingerprint\_generator: [FingerprintGenerator](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md) | None = <!-- -->None

    An optional instance of implementation of `FingerprintGenerator` that is used to generate browser fingerprints together with consistent headers.

  * ##### optionalkeyword-onlyuse\_incognito\_pages: bool | None = <!-- -->False

    By default pages share the same browser context. If set to True each page uses its own context that is destroyed once the page is closed or crashes.

  * ##### kwargs: Any

    Additional arguments for default constructor.

  #### Returns [BrowserPool](https://crawlee.dev/python/python/api/class/BrowserPool.md)

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L195)active

**active: bool

Indicate whether the context is active.

### [**](#active_browsers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L175)active\_browsers

**active\_browsers: Sequence\[[BrowserController](https://crawlee.dev/python/python/api/class/BrowserController.md)]

Return the active browsers in the pool.

### [**](#inactive_browsers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L180)inactive\_browsers

**inactive\_browsers: Sequence\[[BrowserController](https://crawlee.dev/python/python/api/class/BrowserController.md)]

Return the inactive browsers in the pool.

### [**](#pages)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L185)pages

**pages: Mapping\[str, [CrawleePage](https://crawlee.dev/python/python/api/class/CrawleePage.md)]

Return the pages in the pool.

### [**](#plugins)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L170)plugins

**plugins: Sequence\[[BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md)]

Return the browser plugins.

### [**](#total_pages_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_browser_pool.py#L190)total\_pages\_count

**total\_pages\_count: int

Return the total number of pages opened since the browser pool was launched.


---

# ByteSize<!-- -->

Represents a byte size.

## Index[**](#Index)

### Methods

* [**\_\_add\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__add__)
* [**\_\_eq\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__eq__)
* [**\_\_ge\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__ge__)
* [**\_\_gt\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__gt__)
* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__hash__)
* [**\_\_le\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__le__)
* [**\_\_lt\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__lt__)
* [**\_\_mul\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__mul__)
* [**\_\_post\_init\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__post_init__)
* [**\_\_rmul\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__rmul__)
* [**\_\_str\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__str__)
* [**\_\_sub\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__sub__)
* [**\_\_truediv\_\_](https://crawlee.dev/python/python/api/class/ByteSize.md#__truediv__)
* [**from\_gb](https://crawlee.dev/python/python/api/class/ByteSize.md#from_gb)
* [**from\_kb](https://crawlee.dev/python/python/api/class/ByteSize.md#from_kb)
* [**from\_mb](https://crawlee.dev/python/python/api/class/ByteSize.md#from_mb)
* [**from\_tb](https://crawlee.dev/python/python/api/class/ByteSize.md#from_tb)
* [**to\_gb](https://crawlee.dev/python/python/api/class/ByteSize.md#to_gb)
* [**to\_kb](https://crawlee.dev/python/python/api/class/ByteSize.md#to_kb)
* [**to\_mb](https://crawlee.dev/python/python/api/class/ByteSize.md#to_mb)
* [**to\_tb](https://crawlee.dev/python/python/api/class/ByteSize.md#to_tb)
* [**validate](https://crawlee.dev/python/python/api/class/ByteSize.md#validate)

### Properties

* [**bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

## Methods<!-- -->[**](#Methods)

### [**](#__add__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L100)\_\_add\_\_

* ****\_\_add\_\_**(other): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### other: object

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#__eq__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L71)\_\_eq\_\_

* ****\_\_eq\_\_**(other): bool

- #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__ge__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L95)\_\_ge\_\_

* ****\_\_ge\_\_**(other): bool

- #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__gt__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L90)\_\_gt\_\_

* ****\_\_gt\_\_**(other): bool

- #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__hash__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L76)\_\_hash\_\_

* ****\_\_hash\_\_**(): int

- Return hash based on the bytes value.

  ***

  #### Returns int

### [**](#__le__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L85)\_\_le\_\_

* ****\_\_le\_\_**(other): bool

- #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__lt__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L80)\_\_lt\_\_

* ****\_\_lt\_\_**(other): bool

- #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__mul__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L113)\_\_mul\_\_

* ****\_\_mul\_\_**(other): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### other: object

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#__post_init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L18)\_\_post\_init\_\_

* ****\_\_post\_init\_\_**(): None

- #### Returns None

### [**](#__rmul__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L127)\_\_rmul\_\_

* ****\_\_rmul\_\_**(other): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### other: object

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#__str__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L60)\_\_str\_\_

* ****\_\_str\_\_**(): str

- #### Returns str

### [**](#__sub__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L105)\_\_sub\_\_

* ****\_\_sub\_\_**(other): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### other: object

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#__truediv__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L119)\_\_truediv\_\_

* ****\_\_truediv\_\_**(other): float

- #### Parameters

  * ##### other: object

  #### Returns float

### [**](#from_gb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L41)from\_gb

* ****from\_gb**(gb): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### gb: float

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#from_kb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L33)from\_kb

* ****from\_kb**(kb): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### kb: float

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#from_mb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L37)from\_mb

* ****from\_mb**(mb): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### mb: float

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#from_tb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L45)from\_tb

* ****from\_tb**(tb): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### tb: float

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

### [**](#to_gb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L54)to\_gb

* ****to\_gb**(): float

- #### Returns float

### [**](#to_kb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L48)to\_kb

* ****to\_kb**(): float

- #### Returns float

### [**](#to_mb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L51)to\_mb

* ****to\_mb**(): float

- #### Returns float

### [**](#to_tb)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L57)to\_tb

* ****to\_tb**(): float

- #### Returns float

### [**](#validate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L23)validate

* ****validate**(value): [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

- #### Parameters

  * ##### value: Any

  #### Returns [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

## Properties<!-- -->[**](#Properties)

### [**](#bytes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/byte_size.py#L16)bytes

**bytes: int


---

# ClientSnapshot<!-- -->

Snapshot of the state of the client.

## Index[**](#Index)

### Properties

* [**created\_at](https://crawlee.dev/python/python/api/class/ClientSnapshot.md#created_at)
* [**error\_count](https://crawlee.dev/python/python/api/class/ClientSnapshot.md#error_count)
* [**is\_overloaded](https://crawlee.dev/python/python/api/class/ClientSnapshot.md#is_overloaded)
* [**max\_error\_count](https://crawlee.dev/python/python/api/class/ClientSnapshot.md#max_error_count)
* [**new\_error\_count](https://crawlee.dev/python/python/api/class/ClientSnapshot.md#new_error_count)

## Properties<!-- -->[**](#Properties)

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L162)created\_at

**created\_at: datetime

The time at which the system load information was measured.

### [**](#error_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L153)error\_count

**error\_count: int

The number of errors (HTTP 429) that occurred.

### [**](#is_overloaded)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L166)is\_overloaded

**is\_overloaded: bool

Indicate whether the client is considered as overloaded.

### [**](#max_error_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L159)max\_error\_count

**max\_error\_count: int

The maximum number of errors that is considered acceptable.

### [**](#new_error_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L156)new\_error\_count

**new\_error\_count: int

The number of new errors (HTTP 429) that occurred since the last snapshot.


---

# ConcurrencySettings<!-- -->

Concurrency settings for AutoscaledPool.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L108)\_\_init\_\_

* ****\_\_init\_\_**(min\_concurrency, max\_concurrency, max\_tasks\_per\_minute, desired\_concurrency): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalmin\_concurrency: int = <!-- -->1

    The minimum number of tasks running in parallel. If you set this value too high with respect to the available system memory and CPU, your code might run extremely slow or crash.

  * ##### optionalmax\_concurrency: int = <!-- -->100

    The maximum number of tasks running in parallel.

  * ##### optionalmax\_tasks\_per\_minute: float = <!-- -->float('inf')

    The maximum number of tasks per minute the pool can run. By default, this is set to infinity, but you can pass any positive, non-zero number.

  * ##### optionaldesired\_concurrency: int = <!-- -->10

    The desired number of tasks that should be running parallel on the start of the pool, if there is a large enough supply of them. By default, it is `min_concurrency`.

  #### Returns None


---

# Configuration<!-- -->

Configuration settings for the Crawlee project.

This class stores common configurable parameters for Crawlee. Default values are provided for all settings, so typically, no adjustments are necessary. However, you may modify settings for specific use cases, such as changing the default storage directory, the default storage IDs, the timeout for internal operations, and more.

Settings can also be configured via environment variables, prefixed with `CRAWLEE_`.

## Index[**](#Index)

### Methods

* [**get\_global\_configuration](https://crawlee.dev/python/python/api/class/Configuration.md#get_global_configuration)

### Properties

* [**available\_memory\_ratio](https://crawlee.dev/python/python/api/class/Configuration.md#available_memory_ratio)
* [**default\_browser\_path](https://crawlee.dev/python/python/api/class/Configuration.md#default_browser_path)
* [**disable\_browser\_sandbox](https://crawlee.dev/python/python/api/class/Configuration.md#disable_browser_sandbox)
* [**headless](https://crawlee.dev/python/python/api/class/Configuration.md#headless)
* [**internal\_timeout](https://crawlee.dev/python/python/api/class/Configuration.md#internal_timeout)
* [**log\_level](https://crawlee.dev/python/python/api/class/Configuration.md#log_level)
* [**max\_client\_errors](https://crawlee.dev/python/python/api/class/Configuration.md#max_client_errors)
* [**max\_event\_loop\_delay](https://crawlee.dev/python/python/api/class/Configuration.md#max_event_loop_delay)
* [**max\_used\_cpu\_ratio](https://crawlee.dev/python/python/api/class/Configuration.md#max_used_cpu_ratio)
* [**max\_used\_memory\_ratio](https://crawlee.dev/python/python/api/class/Configuration.md#max_used_memory_ratio)
* [**memory\_mbytes](https://crawlee.dev/python/python/api/class/Configuration.md#memory_mbytes)
* [**model\_config](https://crawlee.dev/python/python/api/class/Configuration.md#model_config)
* [**persist\_state\_interval](https://crawlee.dev/python/python/api/class/Configuration.md#persist_state_interval)
* [**purge\_on\_start](https://crawlee.dev/python/python/api/class/Configuration.md#purge_on_start)
* [**storage\_dir](https://crawlee.dev/python/python/api/class/Configuration.md#storage_dir)
* [**system\_info\_interval](https://crawlee.dev/python/python/api/class/Configuration.md#system_info_interval)

## Methods<!-- -->[**](#Methods)

### [**](#get_global_configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L216)get\_global\_configuration

* ****get\_global\_configuration**(): Self

- Retrieve the global instance of the configuration.

  Mostly for the backwards compatibility. It is recommended to use the `service_locator.get_configuration()` instead.

  ***

  #### Returns Self

## Properties<!-- -->[**](#Properties)

### [**](#available_memory_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L174)available\_memory\_ratio

**available\_memory\_ratio: float

The maximum proportion of system memory to use. If `memory_mbytes` is not provided, this ratio is used to calculate the maximum memory. This option is utilized by the `Snapshotter` and supports the dynamic system memory scaling.

### [**](#default_browser_path)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L38)default\_browser\_path

**default\_browser\_path: str | None

Specifies the path to the browser executable. Currently primarily for Playwright-based features. This option is passed directly to Playwright's `browser_type.launch` method as `executable_path` argument. For more details, refer to the Playwright documentation: <https://playwright.dev/docs/api/class-browsertype#browser-type-launch>.

### [**](#disable_browser_sandbox)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L53)disable\_browser\_sandbox

**disable\_browser\_sandbox: bool

Disables the sandbox for the browser. Currently primarily for Playwright-based features. This option is passed directly to Playwright's `browser_type.launch` method as `chromium_sandbox`. For more details, refer to the Playwright documentation: <https://playwright.dev/docs/api/class-browsertype#browser-type-launch>.

### [**](#headless)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L200)headless

**headless: bool

Whether to run the browser in headless mode. Currently primarily for Playwright-based features. This option is passed directly to Playwright's `browser_type.launch` method as `headless`. For more details, refer to the Playwright documentation: <https://playwright.dev/docs/api/class-browsertype#browser-type-launch>.

### [**](#internal_timeout)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L35)internal\_timeout

**internal\_timeout: timedelta | None

Timeout for the internal asynchronous operations.

### [**](#log_level)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L67)log\_level

**log\_level: [LogLevel](https://crawlee.dev/python/python/api.md#LogLevel)

The logging level.

### [**](#max_client_errors)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L150)max\_client\_errors

**max\_client\_errors: int

The maximum number of client errors (HTTP 429) allowed before the system is considered overloaded. This option is used by the `Snapshotter`.

### [**](#max_event_loop_delay)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L138)max\_event\_loop\_delay

**max\_event\_loop\_delay: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms)

The maximum event loop delay. If the event loop delay exceeds this value, it is considered overloaded. This option is used by the `Snapshotter`.

### [**](#max_used_cpu_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L114)max\_used\_cpu\_ratio

**max\_used\_cpu\_ratio: float

The maximum CPU usage ratio. If the CPU usage exceeds this value, the system is considered overloaded. This option is used by the `Snapshotter`.

### [**](#max_used_memory_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L126)max\_used\_memory\_ratio

**max\_used\_memory\_ratio: float

The maximum memory usage ratio. If the memory usage exceeds this ratio, it is considered overloaded. This option is used by the `Snapshotter`.

### [**](#memory_mbytes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L162)memory\_mbytes

**memory\_mbytes: int | None

The maximum used memory in megabytes. This option is utilized by the `Snapshotter`.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L33)model\_config

**model\_config: Undefined

### [**](#persist_state_interval)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L90)persist\_state\_interval

**persist\_state\_interval: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms)

Interval at which `PersistState` events are emitted. The event ensures the state persistence during the crawler run. This option is utilized by the `EventManager`.

### [**](#purge_on_start)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L79)purge\_on\_start

**purge\_on\_start: bool

Whether to purge the storage on the start. This option is utilized by the storage clients.

### [**](#storage_dir)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L189)storage\_dir

**storage\_dir: str

The path to the storage directory. This option is utilized by the storage clients.

### [**](#system_info_interval)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/configuration.py#L102)system\_info\_interval

**system\_info\_interval: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms)

Interval at which `SystemInfo` events are emitted. The event represents the current status of the system. This option is utilized by the `LocalEventManager`.


---

# ContextPipeline<!-- -->

Encapsulates the logic of gradually enhancing the crawling context with additional information and utilities.

The enhancement is done by a chain of middlewares that are added to the pipeline after it's creation.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/ContextPipeline.md#__call__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ContextPipeline.md#__init__)
* [**compose](https://crawlee.dev/python/python/api/class/ContextPipeline.md#compose)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_context_pipeline.py#L82)\_\_call\_\_

* **async **\_\_call\_\_**(crawling\_context, final\_context\_consumer): None

- Run a crawling context through the middleware chain and pipe it into a consumer function.

  Exceptions from the consumer function are wrapped together with the final crawling context.

  ***

  #### Parameters

  * ##### crawling\_context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)
  * ##### final\_context\_consumer: Callable\[\[TCrawlingContext], Awaitable\[None]]

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_context_pipeline.py#L63)\_\_init\_\_

* ****\_\_init\_\_**(\*, \_middleware, \_parent): None

- #### Parameters

  * ##### optionalkeyword-only\_middleware: Callable\[\[TCrawlingContext], AsyncGenerator\[[TMiddlewareCrawlingContext](https://crawlee.dev/python/python/api.md#TMiddlewareCrawlingContext), Exception | None]] | None = <!-- -->None
  * ##### optionalkeyword-only\_parent: [ContextPipeline](https://crawlee.dev/python/python/api/class/ContextPipeline.md)\[[BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)] | None = <!-- -->None

  #### Returns None

### [**](#compose)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_context_pipeline.py#L125)compose

* ****compose**(middleware): [ContextPipeline](https://crawlee.dev/python/python/api/class/ContextPipeline.md)\[[TMiddlewareCrawlingContext](https://crawlee.dev/python/python/api.md#TMiddlewareCrawlingContext)]

- Add a middleware to the pipeline.

  The middleware should yield exactly once, and it should yield an (optionally) extended crawling context object. The part before the yield can be used for initialization and the part after it for cleanup.

  ***

  #### Parameters

  * ##### middleware: Callable\[\[TCrawlingContext], AsyncGenerator\[[TMiddlewareCrawlingContext](https://crawlee.dev/python/python/api.md#TMiddlewareCrawlingContext), None]]

  #### Returns [ContextPipeline](https://crawlee.dev/python/python/api/class/ContextPipeline.md)\[[TMiddlewareCrawlingContext](https://crawlee.dev/python/python/api.md#TMiddlewareCrawlingContext)]

  The extended pipeline instance, providing a fluent interface


---

# ContextPipelineFinalizationError<!-- -->

Wraps an exception thrown in the finalization step of a context pipeline middleware.

We may not have the complete context at this point, so only `BasicCrawlingContext` is provided.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ContextPipelineFinalizationError.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/errors.py#L105)\_\_init\_\_

* ****\_\_init\_\_**(wrapped\_exception, crawling\_context): None

- #### Parameters

  * ##### wrapped\_exception: Exception
  * ##### crawling\_context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)

  #### Returns None


---

# ContextPipelineInitializationError<!-- -->

Wraps an exception thrown in the initialization step of a context pipeline middleware.

We may not have the complete context at this point, so only `BasicCrawlingContext` is provided.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ContextPipelineInitializationError.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/errors.py#L92)\_\_init\_\_

* ****\_\_init\_\_**(wrapped\_exception, crawling\_context): None

- #### Parameters

  * ##### wrapped\_exception: Exception
  * ##### crawling\_context: [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)

  #### Returns None


---

# ContextPipelineInterruptedError<!-- -->

May be thrown in the initialization phase of a middleware to signal that the request should not be processed.


---

# CookieParam<!-- -->

Dictionary representation of cookies for `SessionCookies.set` method.

## Index[**](#Index)

### Properties

* [**domain](https://crawlee.dev/python/python/api/class/CookieParam.md#domain)
* [**expires](https://crawlee.dev/python/python/api/class/CookieParam.md#expires)
* [**http\_only](https://crawlee.dev/python/python/api/class/CookieParam.md#http_only)
* [**name](https://crawlee.dev/python/python/api/class/CookieParam.md#name)
* [**path](https://crawlee.dev/python/python/api/class/CookieParam.md#path)
* [**same\_site](https://crawlee.dev/python/python/api/class/CookieParam.md#same_site)
* [**secure](https://crawlee.dev/python/python/api/class/CookieParam.md#secure)
* [**value](https://crawlee.dev/python/python/api/class/CookieParam.md#value)

## Properties<!-- -->[**](#Properties)

### [**](#domain)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L26)domain

**domain: NotRequired\[str]

Domain for which the cookie is set.

### [**](#expires)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L38)expires

**expires: NotRequired\[int]

Expiration date for the cookie, None for a session cookie.

### [**](#http_only)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L35)http\_only

**http\_only: NotRequired\[bool]

Set the `HttpOnly` flag for the cookie.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L20)name

**name: Required\[str]

Cookie name.

### [**](#path)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L29)path

**path: NotRequired\[str]

Path on the specified domain for which the cookie is set.

### [**](#same_site)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L41)same\_site

**same\_site: NotRequired\[Literal\[Lax, None, Strict]]

Set the `SameSite` attribute for the cookie.

### [**](#secure)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L32)secure

**secure: NotRequired\[bool]

Set the `Secure` flag for the cookie.

### [**](#value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L23)value

**value: Required\[str]

Cookie value.


---

# CpuInfo<!-- -->

Information about the CPU usage.

## Index[**](#Index)

### Properties

* [**model\_config](https://crawlee.dev/python/python/api/class/CpuInfo.md#model_config)
* [**used\_ratio](https://crawlee.dev/python/python/api/class/CpuInfo.md#used_ratio)

## Properties<!-- -->[**](#Properties)

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L39)model\_config

**model\_config: Undefined

### [**](#used_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L41)used\_ratio

**used\_ratio: float

The ratio of CPU currently in use, represented as a float between 0 and 1.


---

# CpuSnapshot<!-- -->

A snapshot of CPU usage.

## Index[**](#Index)

### Properties

* [**created\_at](https://crawlee.dev/python/python/api/class/CpuSnapshot.md#created_at)
* [**is\_overloaded](https://crawlee.dev/python/python/api/class/CpuSnapshot.md#is_overloaded)
* [**max\_used\_ratio](https://crawlee.dev/python/python/api/class/CpuSnapshot.md#max_used_ratio)
* [**used\_ratio](https://crawlee.dev/python/python/api/class/CpuSnapshot.md#used_ratio)

## Properties<!-- -->[**](#Properties)

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L83)created\_at

**created\_at: datetime

The time at which the system load information was measured.

### [**](#is_overloaded)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L87)is\_overloaded

**is\_overloaded: bool

Indicate whether the CPU is considered as overloaded.

### [**](#max_used_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L80)max\_used\_ratio

**max\_used\_ratio: float

The maximum ratio of CPU that is considered acceptable.

### [**](#used_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L77)used\_ratio

**used\_ratio: float

The ratio of CPU currently in use.


---

# CrawleeLogFormatter<!-- -->

Log formatter that prints out the log message nicely formatted, with colored level and stringified extra fields.

It formats the log records so that they:

* start with the level (colorized, and padded to 5 chars so that it is nicely aligned)
* then have the actual log message, if it's multiline then it's nicely indented
* then have the stringified extra log fields
* then, if an exception is a part of the log record, prints the formatted exception.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/CrawleeLogFormatter.md#__init__)
* [**format](https://crawlee.dev/python/python/api/class/CrawleeLogFormatter.md#format)

### Properties

* [**empty\_record](https://crawlee.dev/python/python/api/class/CrawleeLogFormatter.md#empty_record)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_log_config.py#L100)\_\_init\_\_

* ****\_\_init\_\_**(include\_logger\_name, args, kwargs): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalinclude\_logger\_name: bool = <!-- -->True

    Include logger name at the beginning of the log line.

  * ##### args: Any

    Arguments passed to the parent class.

  * ##### kwargs: Any

    Keyword arguments passed to the parent class.

  #### Returns None

### [**](#format)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_log_config.py#L124)format

* ****format**(record): str

- Format the log record nicely.

  This formats the log record so that it:

  * starts with the level (colorized, and padded to 5 chars so that it is nicely aligned)
  * then has the actual log message, if it's multiline then it's nicely indented
  * then has the stringified extra log fields
  * then, if an exception is a part of the log record, prints the formatted exception.

  ***

  #### Parameters

  * ##### record: logging.LogRecord

  #### Returns str

## Properties<!-- -->[**](#Properties)

### [**](#empty_record)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_log_config.py#L98)empty\_record

**empty\_record: Undefined


---

# CrawleePage<!-- -->

Represents a page object within a browser, with additional metadata for tracking and management.

## Index[**](#Index)

### Properties

* [**browser\_type](https://crawlee.dev/python/python/api/class/CrawleePage.md#browser_type)
* [**id](https://crawlee.dev/python/python/api/class/CrawleePage.md#id)
* [**page](https://crawlee.dev/python/python/api/class/CrawleePage.md#page)

## Properties<!-- -->[**](#Properties)

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_types.py#L17)browser\_type

**browser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_types.py#L16)id

**id: str

### [**](#page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_types.py#L18)page

**page: Page


---

# CrawleeRequestData<!-- -->

Crawlee-specific configuration stored in the `user_data`.

## Index[**](#Index)

### Properties

* [**crawl\_depth](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#crawl_depth)
* [**enqueue\_strategy](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#enqueue_strategy)
* [**forefront](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#forefront)
* [**last\_proxy\_tier](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#last_proxy_tier)
* [**max\_retries](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#max_retries)
* [**session\_id](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#session_id)
* [**session\_rotation\_count](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#session_rotation_count)
* [**skip\_navigation](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#skip_navigation)
* [**state](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md#state)

## Properties<!-- -->[**](#Properties)

### [**](#crawl_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L58)crawl\_depth

**crawl\_depth: int

The depth of the request in the crawl tree.

### [**](#enqueue_strategy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L41)enqueue\_strategy

**enqueue\_strategy: [EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy) | None

The strategy that was used for enqueuing the request.

### [**](#forefront)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L55)forefront

**forefront: bool

Indicate whether the request should be enqueued at the front of the queue.

### [**](#last_proxy_tier)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L52)last\_proxy\_tier

**last\_proxy\_tier: int | None

The last proxy tier used to process the request.

### [**](#max_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L37)max\_retries

**max\_retries: int | None

Maximum number of retries for this request. Allows to override the global `max_request_retries` option of `BasicCrawler`.

### [**](#session_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L61)session\_id

**session\_id: str | None

ID of a session to which the request is bound.

### [**](#session_rotation_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L47)session\_rotation\_count

**session\_rotation\_count: int | None

The number of finished session rotations for this request.

### [**](#skip_navigation)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L50)skip\_navigation

**skip\_navigation: bool

### [**](#state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L44)state

**state: [RequestState](https://crawlee.dev/python/python/api/class/RequestState.md)

Describes the request's current lifecycle state.


---

# CrawlerInstrumentor<!-- -->

Helper class for instrumenting crawlers with OpenTelemetry.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/CrawlerInstrumentor.md#__init__)
* [**instrumentation\_dependencies](https://crawlee.dev/python/python/api/class/CrawlerInstrumentor.md#instrumentation_dependencies)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/otel/crawler_instrumentor.py#L28)\_\_init\_\_

* ****\_\_init\_\_**(\*, instrument\_classes, request\_handling\_instrumentation): None

- Initialize the instrumentor.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyinstrument\_classes: list\[[type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)] | None = <!-- -->None

    List of classes to be instrumented - all their public methods and coroutines will be wrapped by generic instrumentation wrapper that will create spans for them.

  * ##### optionalkeyword-onlyrequest\_handling\_instrumentation: bool = <!-- -->True

    When `True`, the most relevant methods in the request handling pipeline will be instrumented. When `False`, no request handling instrumentation will be done.

  #### Returns None

### [**](#instrumentation_dependencies)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/otel/crawler_instrumentor.py#L120)instrumentation\_dependencies

* ****instrumentation\_dependencies**(): list\[str]

- Return a list of python packages with versions that will be instrumented.

  ***

  #### Returns list\[str]


---

