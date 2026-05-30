# Upgrading to v0.x

This page summarizes the breaking changes between Crawlee for Python zero-based versions.

## Upgrading to v0.6[​](#upgrading-to-v06 "Direct link to Upgrading to v0.6")

This section summarizes the breaking changes between v0.5.x and v0.6.0.

### HttpCrawlerOptions[​](#httpcrawleroptions "Direct link to HttpCrawlerOptions")

* Removed `HttpCrawlerOptions` - which contained options from `BasicCrawlerOptions` and unique options `additional_http_error_status_codes` and `ignore_http_error_status_codes`. Both of the unique options were added to `BasicCrawlerOptions` instead.

### HttpClient[​](#httpclient "Direct link to HttpClient")

* The signature of the `HttpClient` class has been updated. The constructor parameters `additional_http_error_status_codes` and `ignore_http_error_status_codes` have been removed and are now only available in `BasicCrawlerOptions`.
* The method `_raise_for_error_status_code` has been removed from `HttpClient`. Its logic has been moved to the `BasicCrawler` class.

### SessionCookies[​](#sessioncookies "Direct link to SessionCookies")

* Replaces the `dict` used for cookie storage in `Session.cookies` with a new `SessionCookies` class. `SessionCookies` uses `CookieJar`, which enables support for multiple domains.

### PlaywrightCrawler and PlaywrightBrowserPlugin[​](#playwrightcrawler-and-playwrightbrowserplugin "Direct link to PlaywrightCrawler and PlaywrightBrowserPlugin")

* `PlaywrightCrawler` now use a persistent browser context instead of the standard browser context.
* Added `user_data_dir` parameter for `PlaywrightCrawler` and `PlaywrightBrowserPlugin` to specify the directory for the persistent context. If not provided, a temporary directory will be created automatically.

### Configuration[​](#configuration "Direct link to Configuration")

The `Configuration` fields `chrome_executable_path`, `xvfb`, and `verbose_log` have been removed. The `chrome_executable_path` and `xvfb` fields were unused, while `verbose_log` can be replaced by setting `log_level` to `DEBUG`.

### CLI dependencies[​](#cli-dependencies "Direct link to CLI dependencies")

CLI dependencies have been moved to optional dependencies. If you need the CLI, install `crawlee[cli]`

### Abstract base classes[​](#abstract-base-classes "Direct link to Abstract base classes")

We decided to move away from [Hungarian notation](https://en.wikipedia.org/wiki/Hungarian_notation) and remove all the `Base` prefixes from the abstract classes. It includes the following public classes:

* `BaseStorageClient` -> `StorageClient`
* `BaseBrowserController` -> `BrowserController`
* `BaseBrowserPlugin` -> `BrowserPlugin`

### EnqueueStrategy[​](#enqueuestrategy "Direct link to EnqueueStrategy")

The `EnqueueStrategy` has been changed from an enum to a string literal type. All its values and their meaning remain unchanged.

## Upgrading to v0.5[​](#upgrading-to-v05 "Direct link to Upgrading to v0.5")

This section summarizes the breaking changes between v0.4.x and v0.5.0.

### Crawlers & CrawlingContexts[​](#crawlers--crawlingcontexts "Direct link to Crawlers & CrawlingContexts")

* All crawler and crawling context classes have been consolidated into a single sub-package called `crawlers`.
* The affected classes include: `AbstractHttpCrawler`, `AbstractHttpParser`, `BasicCrawler`, `BasicCrawlerOptions`, `BasicCrawlingContext`, `BeautifulSoupCrawler`, `BeautifulSoupCrawlingContext`, `BeautifulSoupParserType`, `ContextPipeline`, `HttpCrawler`, `HttpCrawlerOptions`, `HttpCrawlingContext`, `HttpCrawlingResult`, `ParsedHttpCrawlingContext`, `ParselCrawler`, `ParselCrawlingContext`, `PlaywrightCrawler`, `PlaywrightCrawlingContext`, `PlaywrightPreNavCrawlingContext`.

Example update:

```
- from crawlee.beautifulsoup_crawler import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
+ from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
```

### Storage clients[​](#storage-clients "Direct link to Storage clients")

* All storage client classes have been moved into a single sub-package called `storage_clients`.
* The affected classes include: `MemoryStorageClient`, `BaseStorageClient`.

Example update:

```
- from crawlee.memory_storage_client import MemoryStorageClient
+ from crawlee.storage_clients import MemoryStorageClient
```

### CurlImpersonateHttpClient[​](#curlimpersonatehttpclient "Direct link to CurlImpersonateHttpClient")

* The `CurlImpersonateHttpClient` changed its import location.

Example update:

```
- from crawlee.http_clients.curl_impersonate import CurlImpersonateHttpClient
+ from crawlee.http_clients import CurlImpersonateHttpClient
```

### BeautifulSoupParser[​](#beautifulsoupparser "Direct link to BeautifulSoupParser")

* Renamed `BeautifulSoupParser` to `BeautifulSoupParserType`. Probably used only in type hints. Please replace previous usages of `BeautifulSoupParser` by `BeautifulSoupParserType`.
* `BeautifulSoupParser` is now a new class that is used in refactored class `BeautifulSoupCrawler`.

### Service locator[​](#service-locator "Direct link to Service locator")

* The `crawlee.service_container` was completely refactored and renamed to `crawlee.service_locator`.
* You can use it to set the configuration, event manager or storage client globally. Or you can pass them to your crawler instance directly and it will use the service locator under the hood.

### Statistics[​](#statistics "Direct link to Statistics")

* The `crawlee.statistics.Statistics` class do not accept an event manager as an input argument anymore. It uses the default, global one.
* If you want to set your custom event manager, do it either via the service locator or pass it to the crawler.

### Request[​](#request "Direct link to Request")

* The properties `json_` and `order_no` were removed. They were there only for the internal purpose of the memory storage client, you should not need them.

### Request storages and loaders[​](#request-storages-and-loaders "Direct link to Request storages and loaders")

* The `request_provider` parameter of `BasicCrawler.__init__` has been renamed to `request_manager`

* The `BasicCrawler.get_request_provider` method has been renamed to `BasicCrawler.get_request_manager` and it does not accept the `id` and `name` arguments anymore
  <!-- -->
  * If using a specific request queue is desired, pass it as the `request_manager` on `BasicCrawler` creation

* The `RequestProvider` interface has been renamed to `RequestManager` and moved to the `crawlee.request_loaders` package

* `RequestList` has been moved to the `crawlee.request_loaders` package

* `RequestList` does not support `.drop()`, `.reclaim_request()`, `.add_request()` and `add_requests_batched()` anymore

  <!-- -->

  * It implements the new `RequestLoader` interface instead of `RequestManager`
  * `RequestManagerTandem` with a `RequestQueue` should be used to enable passing a `RequestList` (or any other `RequestLoader` implementation) as a `request_manager`, `await list.to_tandem()` can be used as a shortcut

### PlaywrightCrawler[​](#playwrightcrawler "Direct link to PlaywrightCrawler")

* The `PlaywrightPreNavigationContext` was renamed to `PlaywrightPreNavCrawlingContext`.

* The input arguments in `PlaywrightCrawler.__init__` have been renamed:

  <!-- -->

  * `browser_options` is now `browser_launch_options`,
  * `page_options` is now `browser_new_context_options`.

* These argument renaming changes have also been applied to `BrowserPool`, `PlaywrightBrowserPlugin`, and `PlaywrightBrowserController`.

## Upgrading to v0.4[​](#upgrading-to-v04 "Direct link to Upgrading to v0.4")

This section summarizes the breaking changes between v0.3.x and v0.4.0.

### Request model[​](#request-model "Direct link to Request model")

* The `Request.query_params` field has been removed. Please add query parameters directly to the URL, which was possible before as well, and is now the only supported approach.
* The `Request.payload` and `Request.data` fields have been consolidated. Now, only `Request.payload` remains, and it should be used for all payload data in requests.

### Extended unique key computation[​](#extended-unique-key-computation "Direct link to Extended unique key computation")

* The computation of `extended_unique_key` now includes HTTP headers. While this change impacts the behavior, the interface remains the same.

## Upgrading to v0.3[​](#upgrading-to-v03 "Direct link to Upgrading to v0.3")

This section summarizes the breaking changes between v0.2.x and v0.3.0.

### Public and private interface declaration[​](#public-and-private-interface-declaration "Direct link to Public and private interface declaration")

In previous versions, the majority of the package was fully public, including many elements intended for internal use only. With the release of v0.3, we have clearly defined the public and private interface of the package. As a result, some imports have been updated (see below). If you are importing something now designated as private, we recommend reconsidering its use or discussing your use case with us in the discussions/issues.

Here is a list of the updated public imports:

```
- from crawlee.enqueue_strategy import EnqueueStrategy
+ from crawlee import EnqueueStrategy
```

```
- from crawlee.models import Request
+ from crawlee import Request
```

```
- from crawlee.basic_crawler import Router
+ from crawlee.router import Router
```

### Request queue[​](#request-queue "Direct link to Request queue")

There were internal changes that should not affect the intended usage:

* The unused `BaseRequestQueueClient.list_requests()` method was removed
* `RequestQueue` internals were updated to match the "Request Queue V2" implementation in Crawlee for JS

### Service container[​](#service-container "Direct link to Service container")

A new module, `crawlee.service_container`, was added to allow management of "global instances" - currently it contains `Configuration`, `EventManager` and `BaseStorageClient`. The module also replaces the `StorageClientManager` static class. It is likely that its interface will change in the future. If your use case requires working with it, please get in touch - we'll be glad to hear any feedback.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/upgrading/upgrading_to_v0x.md)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/upgrading.md)

[Upgrading](https://crawlee.dev/python/python/docs/upgrading.md)

[Next](https://crawlee.dev/python/python/docs/upgrading/upgrading-to-v1.md)

[Upgrading to v1](https://crawlee.dev/python/python/docs/upgrading/upgrading-to-v1.md)


---

* [](https://crawlee.dev/python/python)
* [Upgrading](https://crawlee.dev/python/python/docs/upgrading.md)
* Upgrading to v1

Version: 1.6

On this page

# Upgrading to v1

This page summarizes the breaking changes between Crawlee for Python v0.6 and v1.0.

## Terminology change: "browser" in different contexts[​](#terminology-change-browser-in-different-contexts "Direct link to Terminology change: \"browser\" in different contexts")

The word "browser" is now used distinctly in two contexts:

* **Playwright context** - Refers to Playwright-supported browsers (`chromium`, `firefox`, `webkit`, `edge`).
* **Fingerprinting context** - Refers to browsers supported by fingerprint generation (`chrome`, `firefox`, `safari`, `edge`).

The type of `HeaderGeneratorOptions.browsers` has changed accordingly:

**Before (v0.6):**

```
from crawlee.fingerprint_suite import HeaderGeneratorOptions

HeaderGeneratorOptions(browsers=['chromium'])
HeaderGeneratorOptions(browsers=['webkit'])
```

**Now (v1.0):**

```
from crawlee.fingerprint_suite import HeaderGeneratorOptions

HeaderGeneratorOptions(browsers=['chrome'])
HeaderGeneratorOptions(browsers=['safari'])
```

## New default HTTP client[​](#new-default-http-client "Direct link to New default HTTP client")

Crawlee v1.0 now uses `ImpitHttpClient` (based on [impit](https://apify.github.io/impit/) library) as the **default HTTP client**, replacing `HttpxHttpClient` (based on [httpx](https://www.python-httpx.org/) library).

If you want to keep using `HttpxHttpClient`, install Crawlee with `httpx` extra, e.g. using pip:

```
pip install 'crawlee[httpx]'
```

And then provide the HTTP client explicitly to the crawler:

```
from crawlee.crawlers import HttpCrawler
from crawlee.http_clients import HttpxHttpClient

client = HttpxHttpClient()
crawler = HttpCrawler(http_client=client)
```

See the [HTTP clients guide](https://crawlee.dev/python/python/docs/guides/http-clients.md) for all options.

## Changes in storages[​](#changes-in-storages "Direct link to Changes in storages")

In Crawlee v1.0, the `Dataset`, `KeyValueStore`, and `RequestQueue` storage APIs have been updated for consistency and simplicity. Below is a detailed overview of what's new, what's changed, and what's been removed.

See the [Storages guide](https://crawlee.dev/python/python/docs/guides/storages.md) for more details.

### Dataset[​](#dataset "Direct link to Dataset")

The `Dataset` API now includes several new methods, such as:

* `get_metadata` - retrieves metadata information for the dataset.
* `purge` - completely clears the dataset, including all items (keeps the metadata only).
* `list_items` - returns the dataset's items in a list format.

Some older methods have been removed or replaced:

* `from_storage_object` constructor has been removed. You should now use the `open` method with either a `name` or `id` parameter.
* `get_info` method and the `storage_object` property have been replaced by the new `get_metadata` method.
* `set_metadata` method has been removed.
* `write_to_json` and `write_to_csv` methods have been removed; instead, use the `export_to` method for exporting data in different formats.

### Key-value store[​](#key-value-store "Direct link to Key-value store")

The `KeyValueStore` API now includes several new methods, such as:

* `get_metadata` - retrieves metadata information for the key-value store.
* `purge` - completely clears the key-value store, removing all keys and values (keeps the metadata only).
* `delete_value` - deletes a specific key and its associated value.
* `list_keys` - lists all keys in the key-value store.

Some older methods have been removed or replaced:

* `from_storage_object` - removed; use the `open` method with either a `name` or `id` instead.
* `get_info` and `storage_object` - replaced by the new `get_metadata` method.
* `set_metadata` method has been removed.

### Request queue[​](#request-queue "Direct link to Request queue")

The `RequestQueue` API now includes several new methods, such as:

* `get_metadata` - retrieves metadata information for the request queue.
* `purge` - completely clears the request queue, including all pending and processed requests (keeps the metadata only).
* `add_requests` - replaces the previous `add_requests_batched` method, offering the same functionality under a simpler name.

Some older methods have been removed or replaced:

* `from_storage_object` - removed; use the `open` method with either a `name` or `id` instead.
* `get_info` and `storage_object` - replaced by the new `get_metadata` method.
* `get_request` has argument `unique_key` instead of `request_id` as the `id` field was removed from the `Request`.
* `set_metadata` method has been removed.

Some changes in the related model classes:

* `resource_directory` in `RequestQueueMetadata` - removed; use the corresponding `path_to_*` property instead.
* `stats` field in `RequestQueueMetadata` - removed as it was unused.
* `RequestQueueHead` - replaced by `RequestQueueHeadWithLocks`.

## New architecture of storage clients[​](#new-architecture-of-storage-clients "Direct link to New architecture of storage clients")

In v1.0, the storage client system has been completely reworked to simplify implementation and make custom storage clients easier to write.

See the [Storage clients guide](https://crawlee.dev/python/python/docs/guides/storage-clients.md) for more details.

### New dedicated storage clients[​](#new-dedicated-storage-clients "Direct link to New dedicated storage clients")

Previously, `MemoryStorageClient` handled both in-memory storage and optional file system persistence. This has now been split into two distinct storage clients:

* **`MemoryStorageClient`** - Stores all data in memory only.
* **`FileSystemStorageClient`** - Persists data on the file system, with in-memory caching for better performance.

**Before (v0.6):**

```
from crawlee.configuration import Configuration
from crawlee.storage_clients import MemoryStorageClient

# In-memory only
configuration = Configuration(persist_storage=False)
storage_client = MemoryStorageClient.from_config(configuration)

# File-system persistence
configuration = Configuration(persist_storage=True)
storage_client = MemoryStorageClient.from_config(configuration)
```

**Now (v1.0):**

```
from crawlee.storage_clients import MemoryStorageClient, FileSystemStorageClient

# In-memory only
storage_client = MemoryStorageClient()

# File-system persistence
storage_client = FileSystemStorageClient()
```

### Registering a storage client[​](#registering-a-storage-client "Direct link to Registering a storage client")

The way you register a storage client remains unchanged:

```
from crawlee import service_locator
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset

# Create custom storage client
storage_client = MemoryStorageClient()

# Then register it globally
service_locator.set_storage_client(storage_client)

# Or use it for a single crawler only
crawler = ParselCrawler(storage_client=storage_client)

# Or use it for a single storage only
dataset = await Dataset.open(
    name='my-dataset',
    storage_client=storage_client,
)
```

### Instance caching[​](#instance-caching "Direct link to Instance caching")

Instance caching of `Dataset.open`, `KeyValueStore.open`, and `RequestQueue.open` now return the same instance for the same arguments. Direct calls to `StorageClient.open_*` always return new instances.

### Writing custom storage clients[​](#writing-custom-storage-clients "Direct link to Writing custom storage clients")

The interface for custom storage clients has been simplified:

* One storage client per storage type (`RequestQueue`, `KeyValueStore`, `Dataset`).
* Collection storage clients have been removed.
* The number of methods that have to be implemented have been reduced.

## ServiceLocator changes[​](#servicelocator-changes "Direct link to ServiceLocator changes")

### ServiceLocator is stricter with registering services[​](#servicelocator-is-stricter-with-registering-services "Direct link to ServiceLocator is stricter with registering services")

You can register the services just once, and you can no longer override already registered services.

**Before (v0.6):**

```
from crawlee import service_locator
from crawlee.storage_clients import MemoryStorageClient

service_locator.set_storage_client(MemoryStorageClient())
service_locator.set_storage_client(MemoryStorageClient())
```

**Now (v1.0):**

```
from crawlee import service_locator
from crawlee.storage_clients import MemoryStorageClient

service_locator.set_storage_client(MemoryStorageClient())
service_locator.set_storage_client(MemoryStorageClient())  # Raises an error
```

### BasicCrawler has its own instance of ServiceLocator to track its own services[​](#basiccrawler-has-its-own-instance-of-servicelocator-to-track-its-own-services "Direct link to BasicCrawler has its own instance of ServiceLocator to track its own services")

Explicitly passed services to the crawler can be different the global ones accessible in `crawlee.service_locator`. `BasicCrawler` no longer causes the global services in `service_locator` to be set to the crawler's explicitly passed services.

**Before (v0.6):**

```
from crawlee import service_locator
from crawlee.crawlers import BasicCrawler
from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset


async def main() -> None:
    custom_storage_client = MemoryStorageClient()
    crawler = BasicCrawler(storage_client=custom_storage_client)

    assert service_locator.get_storage_client() is custom_storage_client
    assert await crawler.get_dataset() is await Dataset.open()
```

**Now (v1.0):**

```
from crawlee import service_locator
from crawlee.crawlers import BasicCrawler
from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset


async def main() -> None:
    custom_storage_client = MemoryStorageClient()
    crawler = BasicCrawler(storage_client=custom_storage_client)

    assert service_locator.get_storage_client() is not custom_storage_client
    assert await crawler.get_dataset() is not await Dataset.open()
```

This allows two crawlers with different services at the same time.

**Now (v1.0):**

```
from crawlee.crawlers import BasicCrawler
from crawlee.storage_clients import MemoryStorageClient, FileSystemStorageClient
from crawlee.configuration import Configuration
from crawlee.events import LocalEventManager

custom_configuration_1 = Configuration()
custom_event_manager_1 = LocalEventManager.from_config(custom_configuration_1)
custom_storage_client_1 = MemoryStorageClient()

custom_configuration_2 = Configuration()
custom_event_manager_2 = LocalEventManager.from_config(custom_configuration_2)
custom_storage_client_2 = FileSystemStorageClient()

crawler_1 = BasicCrawler(
    configuration=custom_configuration_1,
    event_manager=custom_event_manager_1,
    storage_client=custom_storage_client_1,
)

crawler_2 = BasicCrawler(
    configuration=custom_configuration_2,
    event_manager=custom_event_manager_2,
    storage_client=custom_storage_client_2,
  )

# use crawlers without runtime crash...
```

## Other smaller updates[​](#other-smaller-updates "Direct link to Other smaller updates")

There are more smaller updates.

### Python version support[​](#python-version-support "Direct link to Python version support")

We drop support for Python 3.9. The minimum supported version is now Python 3.10.

### Changes in Configuration[​](#changes-in-configuration "Direct link to Changes in Configuration")

The fields `persist_storage` and `persist_metadata` have been removed from the `Configuration`. Persistence is now determined only by which storage client class you use.

### Changes in Request[​](#changes-in-request "Direct link to Changes in Request")

`Request` objects no longer have `id` field and all its usages have been transferred to `unique_key` field.

### Changes in HttpResponse[​](#changes-in-httpresponse "Direct link to Changes in HttpResponse")

The method `HttpResponse.read` is now asynchronous. This affects all HTTP-based crawlers.

**Before (v0.6):**

```
from crawlee.crawlers import ParselCrawler, ParselCrawlingContext

async def main() -> None:
    crawler = ParselCrawler()

    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        content = context.http_response.read()
        # ...

    await crawler.run(['https://crawlee.dev/'])
```

**Now (v1.0):**

```
from crawlee.crawlers import ParselCrawler, ParselCrawlingContext

async def main() -> None:
    crawler = ParselCrawler()

    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        content = await context.http_response.read()
        # ...

    await crawler.run(['https://crawlee.dev/'])
```

### New storage naming restrictions[​](#new-storage-naming-restrictions "Direct link to New storage naming restrictions")

We've introduced naming restrictions for storages to ensure compatibility with Apify Platform requirements and prevent potential conflicts. Storage names may include only letters (a–z, A–Z), digits (0–9), and hyphens (-), with hyphens allowed only in the middle of the name (for example, my-storage-1).

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/upgrading/upgrading_to_v1.md)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/upgrading/upgrading-to-v0x.md)

[Upgrading to v0.x](https://crawlee.dev/python/python/docs/upgrading/upgrading-to-v0x.md)

[Next](https://crawlee.dev/python/python/docs/changelog.md)

[Changelog](https://crawlee.dev/python/python/docs/changelog.md)


---

