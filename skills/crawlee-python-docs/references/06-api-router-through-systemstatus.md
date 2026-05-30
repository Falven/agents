# Router<!-- -->

A request dispatching system that routes requests to registered handlers based on their labels.

The `Router` allows you to define and register request handlers for specific labels. When a request is received, the router invokes the corresponding `request_handler` based on the request's `label`. If no matching handler is found, the default handler is used.

### Usage

```
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext
from crawlee.router import Router

router = Router[HttpCrawlingContext]()


# Handler for requests without a matching label handler
@router.default_handler
async def default_handler(context: HttpCrawlingContext) -> None:
    context.log.info(f'Request without label {context.request.url} ...')


# Handler for category requests
@router.handler(label='category')
async def category_handler(context: HttpCrawlingContext) -> None:
    context.log.info(f'Category request {context.request.url} ...')


# Handler for product requests
@router.handler(label='product')
async def product_handler(context: HttpCrawlingContext) -> None:
    context.log.info(f'Product {context.request.url} ...')


async def main() -> None:
    crawler = HttpCrawler(request_handler=router)
    await crawler.run()
```

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/Router.md#__call__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/Router.md#__init__)
* [**default\_handler](https://crawlee.dev/python/python/api/class/Router.md#default_handler)
* [**handler](https://crawlee.dev/python/python/api/class/Router.md#handler)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/router.py#L94)\_\_call\_\_

* **async **\_\_call\_\_**(context): None

- Invoke a request handler that matches the request label (or the default).

  ***

  #### Parameters

  * ##### context: [TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/router.py#L59)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#default_handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/router.py#L63)default\_handler

* ****default\_handler**(handler): [RequestHandler](https://crawlee.dev/python/python/api.md#RequestHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

- Register a default request handler.

  The default request handler is invoked for requests that have either no label or a label for which we have no matching handler.

  ***

  #### Parameters

  * ##### handler: [RequestHandler](https://crawlee.dev/python/python/api.md#RequestHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

  #### Returns [RequestHandler](https://crawlee.dev/python/python/api.md#RequestHandler)\[[TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)]

### [**](#handler)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/router.py#L76)handler

* ****handler**(label): Callable\[\[RequestHandler\[TCrawlingContext]], Callable\[\[TCrawlingContext], Awaitable]]

- Register a request handler based on a label.

  This decorator registers a request handler for a specific label. The handler will be invoked only for requests that have the exact same label.

  ***

  #### Parameters

  * ##### label: str

  #### Returns Callable\[\[RequestHandler\[TCrawlingContext]], Callable\[\[TCrawlingContext], Awaitable]]


---

# ScreenOptions<!-- -->

## Index[**](#Index)

### Properties

* [**max\_height](https://crawlee.dev/python/python/api/class/ScreenOptions.md#max_height)
* [**max\_width](https://crawlee.dev/python/python/api/class/ScreenOptions.md#max_width)
* [**min\_height](https://crawlee.dev/python/python/api/class/ScreenOptions.md#min_height)
* [**min\_width](https://crawlee.dev/python/python/api/class/ScreenOptions.md#min_width)
* [**model\_config](https://crawlee.dev/python/python/api/class/ScreenOptions.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#max_height)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L27)max\_height

**max\_height: float | None

Maximal screen height constraint for the fingerprint generator.

### [**](#max_width)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L21)max\_width

**max\_width: float | None

Maximal screen width constraint for the fingerprint generator.

### [**](#min_height)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L24)min\_height

**min\_height: float | None

Minimal screen height constraint for the fingerprint generator.

### [**](#min_width)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L18)min\_width

**min\_width: float | None

Minimal screen width constraint for the fingerprint generator.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_types.py#L14)model\_config

**model\_config: Undefined

Defines the screen constrains for the fingerprint generator.


---

# SendRequestFunction<!-- -->

A function for sending HTTP requests.

It simplifies the process of sending HTTP requests. It is implemented by the crawling context and is used within request handlers to send additional HTTP requests to target URLs.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/SendRequestFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L571)\_\_call\_\_

* ****\_\_call\_\_**(url, \*, method, payload, headers): Coroutine\[None, None, [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

- Call send request function.

  ***

  #### Parameters

  * ##### url: str

    The URL to send the request to.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method to use.

  * ##### optionalkeyword-onlypayload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None = <!-- -->None

    The payload to include in the request.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The headers to include in the request.

  #### Returns Coroutine\[None, None, [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)]

  The HTTP response received from the server.


---

# ServiceConflictError<!-- -->

Raised when attempting to reassign a service in service container that is already in use.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ServiceConflictError.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/errors.py#L48)\_\_init\_\_

* ****\_\_init\_\_**(service, new\_value, existing\_value): None

- #### Parameters

  * ##### service: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)
  * ##### new\_value: object
  * ##### existing\_value: object

  #### Returns None


---

# ServiceLocator<!-- -->

Service locator for managing the services used by Crawlee.

All services are initialized to its default value lazily.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ServiceLocator.md#__init__)
* [**get\_configuration](https://crawlee.dev/python/python/api/class/ServiceLocator.md#get_configuration)
* [**get\_event\_manager](https://crawlee.dev/python/python/api/class/ServiceLocator.md#get_event_manager)
* [**get\_storage\_client](https://crawlee.dev/python/python/api/class/ServiceLocator.md#get_storage_client)
* [**set\_configuration](https://crawlee.dev/python/python/api/class/ServiceLocator.md#set_configuration)
* [**set\_event\_manager](https://crawlee.dev/python/python/api/class/ServiceLocator.md#set_event_manager)
* [**set\_storage\_client](https://crawlee.dev/python/python/api/class/ServiceLocator.md#set_storage_client)

### Properties

* [**global\_storage\_instance\_manager](https://crawlee.dev/python/python/api/class/ServiceLocator.md#global_storage_instance_manager)
* [**storage\_instance\_manager](https://crawlee.dev/python/python/api/class/ServiceLocator.md#storage_instance_manager)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L28)\_\_init\_\_

* ****\_\_init\_\_**(configuration, event\_manager, storage\_client): None

- #### Parameters

  * ##### optionalconfiguration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None
  * ##### optionalevent\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md) | None = <!-- -->None
  * ##### optionalstorage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md) | None = <!-- -->None

  #### Returns None

### [**](#get_configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L38)get\_configuration

* ****get\_configuration**(): [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

- Get the configuration.

  ***

  #### Returns [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

### [**](#get_event_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L63)get\_event\_manager

* ****get\_event\_manager**(): [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

- Get the event manager.

  ***

  #### Returns [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

### [**](#get_storage_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L93)get\_storage\_client

* ****get\_storage\_client**(): [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)

- Get the storage client.

  ***

  #### Returns [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)

### [**](#set_configuration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L46)set\_configuration

* ****set\_configuration**(configuration): None

- Set the configuration.

  ***

  #### Parameters

  * ##### configuration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

    The configuration to set.

  #### Returns None

### [**](#set_event_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L76)set\_event\_manager

* ****set\_event\_manager**(event\_manager): None

- Set the event manager.

  ***

  #### Parameters

  * ##### event\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)

    The event manager to set.

  #### Returns None

### [**](#set_storage_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L106)set\_storage\_client

* ****set\_storage\_client**(storage\_client): None

- Set the storage client.

  ***

  #### Parameters

  * ##### storage\_client: [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)

    The storage client to set.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#global_storage_instance_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L26)global\_storage\_instance\_manager

**global\_storage\_instance\_manager: [StorageInstanceManager](https://crawlee.dev/python/python/api/class/StorageInstanceManager.md) | None

### [**](#storage_instance_manager)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_service_locator.py#L124)storage\_instance\_manager

**storage\_instance\_manager: [StorageInstanceManager](https://crawlee.dev/python/python/api/class/StorageInstanceManager.md)

Get the storage instance manager. It is global manager shared by all instances of ServiceLocator.


---

# Session<!-- -->

Represent a single user session, managing cookies, error states, and usage limits.

A `Session` simulates a specific user with attributes like cookies, IP (via proxy), and potentially a unique browser fingerprint. It maintains its internal state, which can include custom user data (e.g., authorization tokens or headers) and tracks its usability through metrics such as error score, usage count, and expiration.

## Index[**](#Index)

### Methods

* [**\_\_eq\_\_](https://crawlee.dev/python/python/api/class/Session.md#__eq__)
* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/Session.md#__hash__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/Session.md#__init__)
* [**\_\_repr\_\_](https://crawlee.dev/python/python/api/class/Session.md#__repr__)
* [**from\_model](https://crawlee.dev/python/python/api/class/Session.md#from_model)
* [**get\_state](https://crawlee.dev/python/python/api/class/Session.md#get_state)
* [**is\_blocked\_status\_code](https://crawlee.dev/python/python/api/class/Session.md#is_blocked_status_code)
* [**mark\_bad](https://crawlee.dev/python/python/api/class/Session.md#mark_bad)
* [**mark\_good](https://crawlee.dev/python/python/api/class/Session.md#mark_good)
* [**retire](https://crawlee.dev/python/python/api/class/Session.md#retire)

### Properties

* [**cookies](https://crawlee.dev/python/python/api/class/Session.md#cookies)
* [**error\_score](https://crawlee.dev/python/python/api/class/Session.md#error_score)
* [**expires\_at](https://crawlee.dev/python/python/api/class/Session.md#expires_at)
* [**id](https://crawlee.dev/python/python/api/class/Session.md#id)
* [**is\_blocked](https://crawlee.dev/python/python/api/class/Session.md#is_blocked)
* [**is\_expired](https://crawlee.dev/python/python/api/class/Session.md#is_expired)
* [**is\_max\_usage\_count\_reached](https://crawlee.dev/python/python/api/class/Session.md#is_max_usage_count_reached)
* [**is\_usable](https://crawlee.dev/python/python/api/class/Session.md#is_usable)
* [**usage\_count](https://crawlee.dev/python/python/api/class/Session.md#usage_count)
* [**user\_data](https://crawlee.dev/python/python/api/class/Session.md#user_data)

## Methods<!-- -->[**](#Methods)

### [**](#__eq__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L86)\_\_eq\_\_

* ****\_\_eq\_\_**(other): bool

- Compare two sessions for equality.

  ***

  #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__hash__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L92)\_\_hash\_\_

* ****\_\_hash\_\_**(): int

- Return hash based on the session state.

  ***

  #### Returns int

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L34)\_\_init\_\_

* ****\_\_init\_\_**(\*, id, max\_age, user\_data, max\_error\_score, error\_score\_decrement, created\_at, usage\_count, max\_usage\_count, error\_score, cookies, blocked\_status\_codes): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None

    Unique identifier for the session, autogenerated if not provided.

  * ##### optionalkeyword-onlymax\_age: timedelta = <!-- -->timedelta(minutes=50)

    Time duration after which the session expires.

  * ##### optionalkeyword-onlyuser\_data: dict | None = <!-- -->None

    Custom user data associated with the session.

  * ##### optionalkeyword-onlymax\_error\_score: float = <!-- -->3.0

    Threshold score beyond which the session is considered blocked.

  * ##### optionalkeyword-onlyerror\_score\_decrement: float = <!-- -->0.5

    Value by which the error score is decremented on successful operations.

  * ##### optionalkeyword-onlycreated\_at: datetime | None = <!-- -->None

    Timestamp when the session was created, defaults to current UTC time if not provided.

  * ##### optionalkeyword-onlyusage\_count: int = <!-- -->0

    Number of times the session has been used.

  * ##### optionalkeyword-onlymax\_usage\_count: int = <!-- -->50

    Maximum allowable uses of the session before it is considered expired.

  * ##### optionalkeyword-onlyerror\_score: float = <!-- -->0.0

    Current error score of the session.

  * ##### optionalkeyword-onlycookies: ((([SessionCookies](https://crawlee.dev/python/python/api/class/SessionCookies.md) | CookieJar) | dict\[str, str]) | list\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]) | None = <!-- -->None

    Cookies associated with the session.

  * ##### optionalkeyword-onlyblocked\_status\_codes: list | None = <!-- -->None

    HTTP status codes that indicate a session should be blocked.

  #### Returns None

### [**](#__repr__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L82)\_\_repr\_\_

* ****\_\_repr\_\_**(): str

- Get a string representation.

  ***

  #### Returns str

### [**](#from_model)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L77)from\_model

* ****from\_model**(model): [Session](https://crawlee.dev/python/python/api/class/Session.md)

- Initialize a new instance from a `SessionModel`.

  ***

  #### Parameters

  * ##### model: [SessionModel](https://crawlee.dev/python/python/api/class/SessionModel.md)

  #### Returns [Session](https://crawlee.dev/python/python/api/class/Session.md)

### [**](#get_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L170)get\_state

* ****get\_state**(\*: , as\_dict?
  <!-- -->
  : bool): [SessionModel](https://crawlee.dev/python/python/api/class/SessionModel.md) | dict
* ****get\_state**(\*: , as\_dict: Literal\[true]): dict
* ****get\_state**(\*: , as\_dict: Literal\[false]): [SessionModel](https://crawlee.dev/python/python/api/class/SessionModel.md)

- Retrieve the current state of the session either as a model or as a dictionary.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyas\_dict: bool = <!-- -->False

  #### Returns [SessionModel](https://crawlee.dev/python/python/api/class/SessionModel.md) | dict

### [**](#is_blocked_status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L221)is\_blocked\_status\_code

* ****is\_blocked\_status\_code**(\*, status\_code, ignore\_http\_error\_status\_codes): bool

- Evaluate whether a session should be retired based on the received HTTP status code.

  ***

  #### Parameters

  * ##### keyword-onlystatus\_code: int

    The HTTP status code received from a server response.

  * ##### optionalkeyword-onlyignore\_http\_error\_status\_codes: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[int] | None = <!-- -->None

    Optional status codes to allow suppression of codes from `blocked_status_codes`.

  #### Returns bool

  True if the session should be retired, False otherwise.

### [**](#mark_bad)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L202)mark\_bad

* ****mark\_bad**(): None

- Mark the session as bad after an unsuccessful session usage.

  ***

  #### Returns None

### [**](#mark_good)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L191)mark\_good

* ****mark\_good**(): None

- Mark the session as good. Should be called after a successful session usage.

  ***

  #### Returns None

### [**](#retire)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L211)retire

* ****retire**(): None

- Retire the session by setting the error score to the maximum value.

  This method should be used if the session usage was unsuccessful and you are sure that it is because of the session configuration and not any external matters. For example when server returns 403 status code. If the session does not work due to some external factors as server error such as 5XX you probably want to use `mark_bad` method.

  ***

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#cookies)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L125)cookies

**cookies: [SessionCookies](https://crawlee.dev/python/python/api/class/SessionCookies.md)

Get the cookies.

### [**](#error_score)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L130)error\_score

**error\_score: float

Get the current error score.

### [**](#expires_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L140)expires\_at

**expires\_at: datetime

Get the expiration datetime of the session.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L115)id

**id: str

Get the session ID.

### [**](#is_blocked)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L145)is\_blocked

**is\_blocked: bool

Indicate whether the session is blocked based on the error score..

### [**](#is_expired)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L150)is\_expired

**is\_expired: bool

Indicate whether the session is expired based on the current time.

### [**](#is_max_usage_count_reached)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L155)is\_max\_usage\_count\_reached

**is\_max\_usage\_count\_reached: bool

Indicate whether the session has reached its maximum usage limit.

### [**](#is_usable)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L160)is\_usable

**is\_usable: bool

Determine if the session is usable for next requests.

### [**](#usage_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L135)usage\_count

**usage\_count: float

Get the current usage count.

### [**](#user_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session.py#L120)user\_data

**user\_data: dict

Get the user data.


---

# SessionCookies<!-- -->

Storage cookies for session with browser-compatible serialization and deserialization.

## Index[**](#Index)

### Methods

* [**\_\_bool\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__bool__)
* [**\_\_deepcopy\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__deepcopy__)
* [**\_\_eq\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__eq__)
* [**\_\_getitem\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__getitem__)
* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__hash__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__init__)
* [**\_\_iter\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__iter__)
* [**\_\_len\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__len__)
* [**\_\_repr\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__repr__)
* [**\_\_setitem\_\_](https://crawlee.dev/python/python/api/class/SessionCookies.md#__setitem__)
* [**get\_cookies\_as\_dicts](https://crawlee.dev/python/python/api/class/SessionCookies.md#get_cookies_as_dicts)
* [**get\_cookies\_as\_playwright\_format](https://crawlee.dev/python/python/api/class/SessionCookies.md#get_cookies_as_playwright_format)
* [**set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)
* [**set\_cookies](https://crawlee.dev/python/python/api/class/SessionCookies.md#set_cookies)
* [**set\_cookies\_from\_playwright\_format](https://crawlee.dev/python/python/api/class/SessionCookies.md#set_cookies_from_playwright_format)
* [**store\_cookie](https://crawlee.dev/python/python/api/class/SessionCookies.md#store_cookie)
* [**store\_cookies](https://crawlee.dev/python/python/api/class/SessionCookies.md#store_cookies)

### Properties

* [**jar](https://crawlee.dev/python/python/api/class/SessionCookies.md#jar)

## Methods<!-- -->[**](#Methods)

### [**](#__bool__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L257)\_\_bool\_\_

* ****\_\_bool\_\_**(): bool

- #### Returns bool

### [**](#__deepcopy__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L231)\_\_deepcopy\_\_

* ****\_\_deepcopy\_\_**(memo): [SessionCookies](https://crawlee.dev/python/python/api/class/SessionCookies.md)

- #### Parameters

  * ##### memo: dict\[int, Any] | None

  #### Returns [SessionCookies](https://crawlee.dev/python/python/api/class/SessionCookies.md)

### [**](#__eq__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L262)\_\_eq\_\_

* ****\_\_eq\_\_**(other): bool

- #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__getitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L242)\_\_getitem\_\_

* ****\_\_getitem\_\_**(name): str | None

- #### Parameters

  * ##### name: str

  #### Returns str | None

### [**](#__hash__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L274)\_\_hash\_\_

* ****\_\_hash\_\_**(): int

- Return hash based on the cookies key attributes.

  ***

  #### Returns int

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L63)\_\_init\_\_

* ****\_\_init\_\_**(cookies): None

- #### Parameters

  * ##### optionalcookies: ((([SessionCookies](https://crawlee.dev/python/python/api/class/SessionCookies.md) | CookieJar) | dict\[str, str]) | list\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]) | None = <!-- -->None

  #### Returns None

### [**](#__iter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L248)\_\_iter\_\_

* ****\_\_iter\_\_**(): Iterator\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]

- #### Returns Iterator\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]

### [**](#__len__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L236)\_\_len\_\_

* ****\_\_len\_\_**(): int

- #### Returns int

### [**](#__repr__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L251)\_\_repr\_\_

* ****\_\_repr\_\_**(): str

- #### Returns str

### [**](#__setitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L239)\_\_setitem\_\_

* ****\_\_setitem\_\_**(name, value): None

- #### Parameters

  * ##### name: str
  * ##### value: str

  #### Returns None

### [**](#get_cookies_as_dicts)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L188)get\_cookies\_as\_dicts

* ****get\_cookies\_as\_dicts**(): list\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]

- Convert cookies to a list with `CookieParam` dicts.

  ***

  #### Returns list\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]

### [**](#get_cookies_as_playwright_format)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L220)get\_cookies\_as\_playwright\_format

* ****get\_cookies\_as\_playwright\_format**(): list\[[PlaywrightCookieParam](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md)]

- Get cookies in playwright format.

  ***

  #### Returns list\[[PlaywrightCookieParam](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md)]

### [**](#set)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L88)set

* ****set**(name, value, \*, domain, path, expires, http\_only, secure, same\_site, \_kwargs): None

- Create and store a cookie with modern browser attributes.

  ***

  #### Parameters

  * ##### name: str

    Cookie name.

  * ##### value: str

    Cookie value.

  * ##### optionalkeyword-onlydomain: str = <!-- -->''

    Cookie domain.

  * ##### optionalkeyword-onlypath: str = <!-- -->'/'

    Cookie path.

  * ##### optionalkeyword-onlyexpires: int | None = <!-- -->None

    Cookie expiration timestamp.

  * ##### optionalkeyword-onlyhttp\_only: bool = <!-- -->False

    Whether cookie is HTTP-only.

  * ##### optionalkeyword-onlysecure: bool = <!-- -->False

    Whether cookie requires secure context.

  * ##### optionalkeyword-onlysame\_site: Literal\[Lax, None, Strict] | None = <!-- -->None

    SameSite cookie attribute value.

  * ##### \_kwargs: Any

  #### Returns None

### [**](#set_cookies)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L210)set\_cookies

* ****set\_cookies**(cookie\_dicts): None

- Create and store cookies from their dictionary representations.

  ***

  #### Parameters

  * ##### cookie\_dicts: list\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]

    List of dictionaries where each dict represents cookie parameters.

  #### Returns None

### [**](#set_cookies_from_playwright_format)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L224)set\_cookies\_from\_playwright\_format

* ****set\_cookies\_from\_playwright\_format**(pw\_cookies): None

- Set cookies from playwright format.

  ***

  #### Parameters

  * ##### pw\_cookies: list\[[PlaywrightCookieParam](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md)]

  #### Returns None

### [**](#store_cookie)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L192)store\_cookie

* ****store\_cookie**(cookie): None

- Store a Cookie object in the session cookie jar.

  ***

  #### Parameters

  * ##### cookie: Cookie

    The Cookie object to store in the jar.

  #### Returns None

### [**](#store_cookies)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L200)store\_cookies

* ****store\_cookies**(cookies): None

- Store multiple cookie objects in the session cookie jar.

  ***

  #### Parameters

  * ##### cookies: list\[Cookie]

    A list of cookie objects to store in the jar.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#jar)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L84)jar

**jar: CookieJar

The cookie jar instance.


---

# SessionError<!-- -->

Errors of `SessionError` type will trigger a session rotation.

This error doesn't respect the `max_request_retries` option and has a separate limit of `max_session_rotations`.

### Hierarchy

* *SessionError*
  * [ProxyError](https://crawlee.dev/python/python/api/class/ProxyError.md)


---

# SessionModel<!-- -->

Model for a Session object.

## Index[**](#Index)

### Properties

* [**blocked\_status\_codes](https://crawlee.dev/python/python/api/class/SessionModel.md#blocked_status_codes)
* [**cookies](https://crawlee.dev/python/python/api/class/SessionModel.md#cookies)
* [**created\_at](https://crawlee.dev/python/python/api/class/SessionModel.md#created_at)
* [**error\_score](https://crawlee.dev/python/python/api/class/SessionModel.md#error_score)
* [**error\_score\_decrement](https://crawlee.dev/python/python/api/class/SessionModel.md#error_score_decrement)
* [**id](https://crawlee.dev/python/python/api/class/SessionModel.md#id)
* [**max\_age](https://crawlee.dev/python/python/api/class/SessionModel.md#max_age)
* [**max\_error\_score](https://crawlee.dev/python/python/api/class/SessionModel.md#max_error_score)
* [**max\_usage\_count](https://crawlee.dev/python/python/api/class/SessionModel.md#max_usage_count)
* [**model\_config](https://crawlee.dev/python/python/api/class/SessionModel.md#model_config)
* [**usage\_count](https://crawlee.dev/python/python/api/class/SessionModel.md#usage_count)
* [**user\_data](https://crawlee.dev/python/python/api/class/SessionModel.md#user_data)

## Properties<!-- -->[**](#Properties)

### [**](#blocked_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L35)blocked\_status\_codes

**blocked\_status\_codes: list\[int]

### [**](#cookies)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L34)cookies

**cookies: list\[[CookieParam](https://crawlee.dev/python/python/api/class/CookieParam.md)]

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L30)created\_at

**created\_at: datetime

### [**](#error_score)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L33)error\_score

**error\_score: float

### [**](#error_score_decrement)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L29)error\_score\_decrement

**error\_score\_decrement: float

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L25)id

**id: str

### [**](#max_age)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L26)max\_age

**max\_age: timedelta

### [**](#max_error_score)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L28)max\_error\_score

**max\_error\_score: float

### [**](#max_usage_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L32)max\_usage\_count

**max\_usage\_count: int

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L23)model\_config

**model\_config: Undefined

### [**](#usage_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L31)usage\_count

**usage\_count: int

### [**](#user_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L27)user\_data

**user\_data: dict


---

# SessionPool<!-- -->

A pool of sessions that are managed, rotated, and persisted based on usage and age.

It ensures effective session management by maintaining a pool of sessions and rotating them based on usage count, expiration time, or custom rules. It provides methods to retrieve sessions, manage their lifecycle, and optionally persist the state to enable recovery.

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/SessionPool.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/SessionPool.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SessionPool.md#__init__)
* [**\_\_repr\_\_](https://crawlee.dev/python/python/api/class/SessionPool.md#__repr__)
* [**add\_session](https://crawlee.dev/python/python/api/class/SessionPool.md#add_session)
* [**get\_session](https://crawlee.dev/python/python/api/class/SessionPool.md#get_session)
* [**get\_session\_by\_id](https://crawlee.dev/python/python/api/class/SessionPool.md#get_session_by_id)
* [**get\_state](https://crawlee.dev/python/python/api/class/SessionPool.md#get_state)
* [**reset\_store](https://crawlee.dev/python/python/api/class/SessionPool.md#reset_store)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/SessionPool.md#active)
* [**retired\_session\_count](https://crawlee.dev/python/python/api/class/SessionPool.md#retired_session_count)
* [**session\_count](https://crawlee.dev/python/python/api/class/SessionPool.md#session_count)
* [**usable\_session\_count](https://crawlee.dev/python/python/api/class/SessionPool.md#usable_session_count)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L110)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md)

- Initialize the pool upon entering the context manager.

  ***

  #### Returns [SessionPool](https://crawlee.dev/python/python/api/class/SessionPool.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L130)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Deinitialize the pool upon exiting the context manager.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L36)\_\_init\_\_

* ****\_\_init\_\_**(\*, max\_pool\_size, create\_session\_settings, create\_session\_function, event\_manager, persistence\_enabled, persist\_state\_kvs\_name, persist\_state\_key): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlymax\_pool\_size: int = <!-- -->1000

    Maximum number of sessions to maintain in the pool. You can add more sessions to the pool by using the `add_session` method.

  * ##### optionalkeyword-onlycreate\_session\_settings: dict | None = <!-- -->None

    Settings for creating new session instances. If None, default settings will be used. Do not set it if you are providing a `create_session_function`.

  * ##### optionalkeyword-onlycreate\_session\_function: [CreateSessionFunctionType](https://crawlee.dev/python/python/api.md#CreateSessionFunctionType) | None = <!-- -->None

    A callable to create new session instances. If None, a default session settings will be used. Do not set it if you are providing `create_session_settings`.

  * ##### optionalkeyword-onlyevent\_manager: [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md) | None = <!-- -->None

    The event manager to handle events like persist state.

  * ##### optionalkeyword-onlypersistence\_enabled: bool = <!-- -->False

    Flag to enable or disable state persistence of the pool.

  * ##### optionalkeyword-onlypersist\_state\_kvs\_name: str | None = <!-- -->None

    The name of the `KeyValueStore` used for state persistence.

  * ##### optionalkeyword-onlypersist\_state\_key: str = <!-- -->'CRAWLEE\_SESSION\_POOL\_STATE'

    The key under which the session pool's state is stored in the `KeyValueStore`.

  #### Returns None

### [**](#__repr__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L86)\_\_repr\_\_

* ****\_\_repr\_\_**(): str

- Get a string representation.

  ***

  #### Returns str

### [**](#add_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L163)add\_session

* ****add\_session**(session): None

- Add an externally created session to the pool.

  This is intended only for the cases when you want to add a session that was created outside of the pool. Otherwise, the pool will create new sessions automatically.

  ***

  #### Parameters

  * ##### session: [Session](https://crawlee.dev/python/python/api/class/Session.md)

    The session to add to the pool.

  #### Returns None

### [**](#get_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L180)get\_session

* **async **get\_session**(): [Session](https://crawlee.dev/python/python/api/class/Session.md)

- Retrieve a random session from the pool.

  This method first ensures the session pool is at its maximum capacity. If the random session is not usable, retired sessions are removed and a new session is created and returned.

  ***

  #### Returns [Session](https://crawlee.dev/python/python/api/class/Session.md)

  The session object.

### [**](#get_session_by_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L200)get\_session\_by\_id

* **async **get\_session\_by\_id**(session\_id): [Session](https://crawlee.dev/python/python/api/class/Session.md) | None

- Retrieve a session by ID from the pool.

  This method first ensures the session pool is at its maximum capacity. It then tries to retrieve a specific session by ID. If the session is not found or not usable, `None` is returned.

  ***

  #### Parameters

  * ##### session\_id: str

    The ID of the session to retrieve.

  #### Returns [Session](https://crawlee.dev/python/python/api/class/Session.md) | None

  The session object if found and usable, otherwise `None`.

### [**](#get_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L155)get\_state

* ****get\_state**(\*: , as\_dict?
  <!-- -->
  : bool): [SessionPoolModel](https://crawlee.dev/python/python/api/class/SessionPoolModel.md) | dict
* ****get\_state**(\*: , as\_dict: Literal\[true]): dict
* ****get\_state**(\*: , as\_dict: Literal\[false]): [SessionPoolModel](https://crawlee.dev/python/python/api/class/SessionPoolModel.md)

- Retrieve the current state of the pool either as a model or as a dictionary.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyas\_dict: bool = <!-- -->False

  #### Returns [SessionPoolModel](https://crawlee.dev/python/python/api/class/SessionPoolModel.md) | dict

### [**](#reset_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L225)reset\_store

* **async **reset\_store**(): None

- Reset the KVS where the pool state is persisted.

  ***

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L106)active

**active: bool

Indicate whether the context is active.

### [**](#retired_session_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L101)retired\_session\_count

**retired\_session\_count: int

Get the number of sessions that are no longer usable.

### [**](#session_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L91)session\_count

**session\_count: int

Get the total number of sessions currently maintained in the pool.

### [**](#usable_session_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_session_pool.py#L96)usable\_session\_count

**usable\_session\_count: int

Get the number of sessions that are currently usable.


---

# SessionPoolModel<!-- -->

Model for a SessionPool object.

## Index[**](#Index)

### Properties

* [**max\_pool\_size](https://crawlee.dev/python/python/api/class/SessionPoolModel.md#max_pool_size)
* [**model\_config](https://crawlee.dev/python/python/api/class/SessionPoolModel.md#model_config)
* [**retired\_session\_count](https://crawlee.dev/python/python/api/class/SessionPoolModel.md#retired_session_count)
* [**session\_count](https://crawlee.dev/python/python/api/class/SessionPoolModel.md#session_count)
* [**sessions](https://crawlee.dev/python/python/api/class/SessionPoolModel.md#sessions)
* [**usable\_session\_count](https://crawlee.dev/python/python/api/class/SessionPoolModel.md#usable_session_count)

## Properties<!-- -->[**](#Properties)

### [**](#max_pool_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L43)max\_pool\_size

**max\_pool\_size: int

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L41)model\_config

**model\_config: Undefined

### [**](#retired_session_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L80)retired\_session\_count

**retired\_session\_count: int

Get the number of sessions that are no longer usable.

### [**](#session_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L68)session\_count

**session\_count: int

Get the total number of sessions currently maintained in the pool.

### [**](#sessions)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L45)sessions

**sessions: dict\[str, [Session](https://crawlee.dev/python/python/api/class/Session.md)]

### [**](#usable_session_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_models.py#L74)usable\_session\_count

**usable\_session\_count: int

Get the number of sessions that are currently usable.


---

# SharedTimeout<!-- -->

Keeps track of a time budget shared by multiple independent async operations.

Provides a reusable, non-reentrant context manager interface.

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/SharedTimeout.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/SharedTimeout.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SharedTimeout.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/time.py#L52)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): timedelta

- #### Returns timedelta

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/time.py#L61)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/time.py#L47)\_\_init\_\_

* ****\_\_init\_\_**(timeout): None

- #### Parameters

  * ##### timeout: timedelta

  #### Returns None


---

# Sitemap<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/Sitemap.md#__init__)
* [**from\_xml\_string](https://crawlee.dev/python/python/api/class/Sitemap.md#from_xml_string)
* [**load](https://crawlee.dev/python/python/api/class/Sitemap.md#load)
* [**parse](https://crawlee.dev/python/python/api/class/Sitemap.md#parse)
* [**try\_common\_names](https://crawlee.dev/python/python/api/class/Sitemap.md#try_common_names)

### Properties

* [**urls](https://crawlee.dev/python/python/api/class/Sitemap.md#urls)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L384)\_\_init\_\_

* ****\_\_init\_\_**(urls): None

- #### Parameters

  * ##### urls: list\[str]

  #### Returns None

### [**](#from_xml_string)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L412)from\_xml\_string

* **async **from\_xml\_string**(content): [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

- #### Parameters

  * ##### content: str

  #### Returns [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

### [**](#load)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L398)load

* **async **load**(urls, http\_client, proxy\_info, parse\_sitemap\_options): [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

- #### Parameters

  * ##### urls: str | list\[str]
  * ##### http\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)
  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None
  * ##### optionalparse\_sitemap\_options: [ParseSitemapOptions](https://crawlee.dev/python/python/api/class/ParseSitemapOptions.md) | None = <!-- -->None

  #### Returns [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

### [**](#parse)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L416)parse

* **async **parse**(sources, http\_client, proxy\_info, parse\_sitemap\_options): [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

- #### Parameters

  * ##### sources: list\[[SitemapSource](https://crawlee.dev/python/python/api/class/SitemapSource.md)]
  * ##### optionalhttp\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md) | None = <!-- -->None
  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None
  * ##### optionalparse\_sitemap\_options: [ParseSitemapOptions](https://crawlee.dev/python/python/api/class/ParseSitemapOptions.md) | None = <!-- -->None

  #### Returns [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

### [**](#try_common_names)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L392)try\_common\_names

* **async **try\_common\_names**(url, http\_client, proxy\_info): [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

- #### Parameters

  * ##### url: str
  * ##### http\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)
  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

  #### Returns [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

## Properties<!-- -->[**](#Properties)

### [**](#urls)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L388)urls

**urls: list\[str]


---

# SitemapRequestLoader<!-- -->

A request loader that reads URLs from sitemap(s).

The loader is designed to handle sitemaps that follow the format described in the Sitemaps protocol (<https://www.sitemaps.org/protocol.html>). It supports both XML and plain text sitemap formats. Note that HTML pages containing links are not supported - those should be handled by regular crawlers and the `enqueue_links` functionality.

The loader fetches and parses sitemaps in the background, allowing crawling to start before all URLs are loaded. It supports filtering URLs using glob and regex patterns.

The loader supports state persistence, allowing it to resume from where it left off after interruption when a `persist_state_key` is provided during initialization.

### Hierarchy

* [RequestLoader](https://crawlee.dev/python/python/api/class/RequestLoader.md)
  * *SitemapRequestLoader*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#__init__)
* [**abort\_loading](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#abort_loading)
* [**close](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#close)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#fetch_next_request)
* [**get\_handled\_count](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#get_handled_count)
* [**get\_total\_count](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#get_total_count)
* [**is\_empty](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#is_empty)
* [**is\_finished](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#is_finished)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#mark_request_as_handled)
* [**start](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#start)
* [**to\_tandem](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md#to_tandem)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L376)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [SitemapRequestLoader](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md)

- Enter the context manager.

  ***

  #### Returns [SitemapRequestLoader](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L381)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Exit the context manager.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L106)\_\_init\_\_

* ****\_\_init\_\_**(sitemap\_urls, http\_client, \*, proxy\_info, include, exclude, max\_buffer\_size, persist\_state\_key, transform\_request\_function): None

- Initialize the sitemap request loader.

  ***

  #### Parameters

  * ##### sitemap\_urls: list\[str]

    Configuration options for the loader.

  * ##### http\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

    the instance of `HttpClient` to use for fetching sitemaps.

  * ##### optionalkeyword-onlyproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    Optional proxy to use for fetching sitemaps.

  * ##### optionalkeyword-onlyinclude: list\[re.Pattern\[Any] | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)] | None = <!-- -->None

    List of glob or regex patterns to include URLs.

  * ##### optionalkeyword-onlyexclude: list\[re.Pattern\[Any] | [Glob](https://crawlee.dev/python/python/api/class/Glob.md)] | None = <!-- -->None

    List of glob or regex patterns to exclude URLs.

  * ##### optionalkeyword-onlymax\_buffer\_size: int = <!-- -->200

    Maximum number of URLs to buffer in memory.

  * ##### optionalkeyword-onlypersist\_state\_key: str | None = <!-- -->None

    A key for persisting the loader's state in the KeyValueStore. When provided, allows resuming from where it left off after interruption. If None, no state persistence occurs.

  * ##### optionalkeyword-onlytransform\_request\_function: Callable\[\[RequestOptions], [RequestOptions](https://crawlee.dev/python/python/api/class/RequestOptions.md) | [RequestTransformAction](https://crawlee.dev/python/python/api.md#RequestTransformAction)] | None = <!-- -->None

    An optional function to transform requests generated by the loader. It receives `RequestOptions` with `url` and should return either modified `RequestOptions` or a `RequestTransformAction`.

  #### Returns None

### [**](#abort_loading)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L358)abort\_loading

* **async **abort\_loading**(): None

- Abort the sitemap loading process.

  ***

  #### Returns None

### [**](#close)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L371)close

* **async **close**(): None

- Close the request loader.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L315)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestLoader.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestLoader.md#fetch_next_request)

  Fetch the next request to process.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

### [**](#get_handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L297)get\_handled\_count

* **async **get\_handled\_count**(): int

- Overrides [RequestLoader.get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_handled_count)

  Return the number of URLs that have been handled.

  ***

  #### Returns int

### [**](#get_total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L291)get\_total\_count

* **async **get\_total\_count**(): int

- Overrides [RequestLoader.get\_total\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_total_count)

  Return the total number of URLs found so far.

  ***

  #### Returns int

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L303)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestLoader.is\_empty](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_empty)

  Check if there are no more URLs to process.

  ***

  #### Returns bool

### [**](#is_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L309)is\_finished

* **async **is\_finished**(): bool

- Overrides [RequestLoader.is\_finished](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_finished)

  Check if all URLs have been processed.

  ***

  #### Returns bool

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L350)mark\_request\_as\_handled

* **async **mark\_request\_as\_handled**(request): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestLoader.mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestLoader.md#mark_request_as_handled)

  Mark a request as successfully handled.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

### [**](#start)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L365)start

* **async **start**(): None

- Start the sitemap loading process.

  ***

  #### Returns None

### [**](#to_tandem)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L56)to\_tandem

* **async **to\_tandem**(request\_manager): [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)

- Inherited from [RequestLoader.to\_tandem](https://crawlee.dev/python/python/api/class/RequestLoader.md#to_tandem)

  Combine the loader with a request manager to support adding and reclaiming requests.

  ***

  #### Parameters

  * ##### optionalrequest\_manager: RequestManager | None = <!-- -->None

    Request manager to combine the loader with. If None is given, the default request queue is used.

  #### Returns [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)


---

# SitemapRequestLoaderState<!-- -->

State model for persisting sitemap request loader data.

The crawler processes one sitemap at a time. The current sitemap is stored in `in_progress_sitemap_url`. The `parse_sitemap` function parses the sitemap and returns elements as an async iterator. Each element retrieved from the iterator is processed based on its type. If the element is a `NestedSitemap`, its URL is added to `pending_sitemap_urls` if it hasn't been processed yet (not in `processed_sitemap_urls`). If the element is a `SitemapUrl`, the system checks whether it already exists in `current_sitemap_processed_urls`. If it exists, the loader was restarted from a saved state and the URL is skipped.

If the URL is new, it is first added to `url_queue`, then to `current_sitemap_processed_urls`, and `total_count` is incremented by 1. When all elements from the current sitemap iterator have been processed, `in_progress_sitemap_url` is set to `None`, the sitemap URL is added to `processed_sitemap_urls`, and `current_sitemap_processed_urls` is cleared. The next sitemap is retrieved from `pending_sitemap_urls`, skipping any URLs that already exist in `processed_sitemap_urls`. If `pending_sitemap_urls` is empty, `completed` is set to `True`.

When `fetch_next_request` is called, a URL is extracted from `url_queue` and placed in `in_progress`. When `mark_request_as_handled` is called for the extracted URL, it is removed from `in_progress` and `handled_count` is incremented by 1.

During initial startup or restart after persistence, state validation occurs in `_get_state`. If both `pending_sitemap_urls` and `in_progress_sitemap_url` are empty and `completed` is False, this indicates a fresh start. In this case, `self._sitemap_urls` are moved to `pending_sitemap_urls`. Otherwise, the system is restarting from a persisted state. If `in_progress` contains any URLs, they are moved back to `url_queue` and `in_progress` is cleared.

## Index[**](#Index)

### Properties

* [**completed](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#completed)
* [**current\_sitemap\_processed\_urls](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#current_sitemap_processed_urls)
* [**handled\_count](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#handled_count)
* [**in\_progress](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#in_progress)
* [**in\_progress\_sitemap\_url](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#in_progress_sitemap_url)
* [**model\_config](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#model_config)
* [**pending\_sitemap\_urls](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#pending_sitemap_urls)
* [**processed\_sitemap\_urls](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#processed_sitemap_urls)
* [**total\_count](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#total_count)
* [**url\_queue](https://crawlee.dev/python/python/api/class/SitemapRequestLoaderState.md#url_queue)

## Properties<!-- -->[**](#Properties)

### [**](#completed)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L80)completed

**completed: bool

Whether all sitemaps have been fully processed.

### [**](#current_sitemap_processed_urls)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L74)current\_sitemap\_processed\_urls

**current\_sitemap\_processed\_urls: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[str]

URLs from the current sitemap that have been added to the queue.

### [**](#handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L86)handled\_count

**handled\_count: int

Number of URLs that have been successfully handled.

### [**](#in_progress)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L65)in\_progress

**in\_progress: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[str]

Set of request URLs currently being processed.

### [**](#in_progress_sitemap_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L71)in\_progress\_sitemap\_url

**in\_progress\_sitemap\_url: str | None

The sitemap URL currently being processed.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L60)model\_config

**model\_config: Undefined

### [**](#pending_sitemap_urls)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L68)pending\_sitemap\_urls

**pending\_sitemap\_urls: deque\[str]

Queue of sitemap URLs that need to be fetched and processed.

### [**](#processed_sitemap_urls)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L77)processed\_sitemap\_urls

**processed\_sitemap\_urls: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[str]

Set of processed sitemap URLs.

### [**](#total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L83)total\_count

**total\_count: int

Total number of URLs found and added to the queue from all processed sitemaps.

### [**](#url_queue)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_sitemap_request_loader.py#L62)url\_queue

**url\_queue: deque\[str]

Queue of URLs extracted from sitemaps and ready for processing.


---

# SitemapSource<!-- -->

## Index[**](#Index)

### Properties

* [**content](https://crawlee.dev/python/python/api/class/SitemapSource.md#content)
* [**depth](https://crawlee.dev/python/python/api/class/SitemapSource.md#depth)
* [**type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)
* [**url](https://crawlee.dev/python/python/api/class/SitemapSource.md#url)

## Properties<!-- -->[**](#Properties)

### [**](#content)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L64)content

**content: NotRequired\[str]

### [**](#depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L65)depth

**depth: NotRequired\[int]

### [**](#type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L62)type

**type: Literal\[url, raw]

### [**](#url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L63)url

**url: NotRequired\[str]


---

# SitemapUrl<!-- -->

## Index[**](#Index)

### Properties

* [**changefreq](https://crawlee.dev/python/python/api/class/SitemapUrl.md#changefreq)
* [**lastmod](https://crawlee.dev/python/python/api/class/SitemapUrl.md#lastmod)
* [**loc](https://crawlee.dev/python/python/api/class/SitemapUrl.md#loc)
* [**origin\_sitemap\_url](https://crawlee.dev/python/python/api/class/SitemapUrl.md#origin_sitemap_url)
* [**priority](https://crawlee.dev/python/python/api/class/SitemapUrl.md#priority)

## Properties<!-- -->[**](#Properties)

### [**](#changefreq)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L43)changefreq

**changefreq: str | None

### [**](#lastmod)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L42)lastmod

**lastmod: datetime | None

### [**](#loc)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L41)loc

**loc: str

### [**](#origin_sitemap_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L45)origin\_sitemap\_url

**origin\_sitemap\_url: str | None

### [**](#priority)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L44)priority

**priority: float | None


---

# Snapshotter<!-- -->

Monitors and logs system resource usage at predefined intervals for performance optimization.

The class monitors and records the state of various system resources (CPU, memory, event loop, and client API) at predefined intervals. This continuous monitoring helps in identifying resource overloads and ensuring optimal performance of the application. It is utilized in the `AutoscaledPool` module to adjust task allocation dynamically based on the current demand and system load.

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/Snapshotter.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/Snapshotter.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/Snapshotter.md#__init__)
* [**from\_config](https://crawlee.dev/python/python/api/class/Snapshotter.md#from_config)
* [**get\_client\_sample](https://crawlee.dev/python/python/api/class/Snapshotter.md#get_client_sample)
* [**get\_cpu\_sample](https://crawlee.dev/python/python/api/class/Snapshotter.md#get_cpu_sample)
* [**get\_event\_loop\_sample](https://crawlee.dev/python/python/api/class/Snapshotter.md#get_event_loop_sample)
* [**get\_memory\_sample](https://crawlee.dev/python/python/api/class/Snapshotter.md#get_memory_sample)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/Snapshotter.md#active)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L159)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [Snapshotter](https://crawlee.dev/python/python/api/class/Snapshotter.md)

- Start capturing snapshots at configured intervals.

  ***

  #### Returns [Snapshotter](https://crawlee.dev/python/python/api/class/Snapshotter.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L176)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Stop all resource capturing.

  This method stops capturing snapshots of system resources (CPU, memory, event loop, and client information). It should be called to terminate resource capturing when it is no longer needed.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L72)\_\_init\_\_

* ****\_\_init\_\_**(\*, max\_used\_cpu\_ratio, max\_used\_memory\_ratio, max\_event\_loop\_delay, max\_client\_errors, max\_memory\_size): None

- Initialize a new instance.

  In most cases, you should use the `from_config` constructor to create a new instance based on the provided configuration.

  ***

  #### Parameters

  * ##### keyword-onlymax\_used\_cpu\_ratio: float

    Sets the ratio, defining the maximum CPU usage. When the CPU usage is higher than the provided ratio, the CPU is considered overloaded.

  * ##### keyword-onlymax\_used\_memory\_ratio: float

    Sets the ratio, defining the maximum ratio of memory usage. When the memory usage is higher than the provided ratio of `max_memory_size`, the memory is considered overloaded.

  * ##### keyword-onlymax\_event\_loop\_delay: timedelta

    Sets the maximum delay of the event loop. When the delay is higher than the provided value, the event loop is considered overloaded.

  * ##### keyword-onlymax\_client\_errors: int

    Sets the maximum number of client errors (HTTP 429). When the number of client errors is higher than the provided number, the client is considered overloaded.

  * ##### keyword-onlymax\_memory\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md) | [Ratio](https://crawlee.dev/python/python/api/class/Ratio.md)

    Sets the maximum amount of system memory to be used by the `AutoscaledPool`. When of type `ByteSize` then it is used as fixed memory size. When of type `Ratio` then it allows for dynamic memory scaling based on the available system memory.

  #### Returns None

### [**](#from_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L119)from\_config

* ****from\_config**(config): [Snapshotter](https://crawlee.dev/python/python/api/class/Snapshotter.md)

- Initialize a new instance based on the provided `Configuration`.

  ***

  #### Parameters

  * ##### optionalconfig: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

    The `Configuration` instance. Uses the global (default) one if not provided.

  #### Returns [Snapshotter](https://crawlee.dev/python/python/api/class/Snapshotter.md)

### [**](#get_client_sample)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L240)get\_client\_sample

* ****get\_client\_sample**(duration): list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

- Return a sample of the latest client snapshots.

  ***

  #### Parameters

  * ##### optionalduration: timedelta | None = <!-- -->None

    The duration of the sample from the latest snapshot. If omitted, it returns a full history.

  #### Returns list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

  A sample of client snapshots.

### [**](#get_cpu_sample)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L227)get\_cpu\_sample

* ****get\_cpu\_sample**(duration): list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

- Return a sample of the latest CPU snapshots.

  ***

  #### Parameters

  * ##### optionalduration: timedelta | None = <!-- -->None

    The duration of the sample from the latest snapshot. If omitted, it returns a full history.

  #### Returns list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

  A sample of CPU snapshots.

### [**](#get_event_loop_sample)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L214)get\_event\_loop\_sample

* ****get\_event\_loop\_sample**(duration): list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

- Return a sample of the latest event loop snapshots.

  ***

  #### Parameters

  * ##### optionalduration: timedelta | None = <!-- -->None

    The duration of the sample from the latest snapshot. If omitted, it returns a full history.

  #### Returns list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

  A sample of event loop snapshots.

### [**](#get_memory_sample)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L201)get\_memory\_sample

* ****get\_memory\_sample**(duration): list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

- Return a sample of the latest memory snapshots.

  ***

  #### Parameters

  * ##### optionalduration: timedelta | None = <!-- -->None

    The duration of the sample from the latest snapshot. If omitted, it returns a full history.

  #### Returns list\[[Snapshot](https://crawlee.dev/python/python/api.md#Snapshot)]

  A sample of memory snapshots.

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L155)active

**active: bool

Indicate whether the context is active.


---

# SortedSnapshotList<!-- -->

A list that maintains sorted order by `created_at` attribute for snapshot objects.

## Index[**](#Index)

### Methods

* [**add](https://crawlee.dev/python/python/api/class/SortedSnapshotList.md#add)

## Methods<!-- -->[**](#Methods)

### [**](#add)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/snapshotter.py#L39)add

* ****add**(item): None

- Add an item to the list maintaining sorted order by `created_at` using binary search.

  ***

  #### Parameters

  * ##### item: [T](https://crawlee.dev/python/python/api.md#T)

  #### Returns None


---

# SqlClientMixin<!-- -->

Mixin class for SQL clients.

This mixin provides common SQL operations and basic methods for SQL storage clients.

### Hierarchy

* *SqlClientMixin*

  * [SqlRequestQueueClient](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md)
  * [SqlDatasetClient](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md)
  * [SqlKeyValueStoreClient](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md)

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#__init__)
* [**get\_session](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#get_session)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L78)\_\_init\_\_

* ****\_\_init\_\_**(\*, id, storage\_client): None

- #### Parameters

  * ##### keyword-onlyid: str
  * ##### keyword-onlystorage\_client: [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

  #### Returns None

### [**](#get_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L197)get\_session

* **async **get\_session**(\*, with\_simple\_commit): AsyncIterator\[AsyncSession]

- Create a new SQLAlchemy session for this storage.

  ***

  #### Parameters

  * ##### optionalkeyword-onlywith\_simple\_commit: bool = <!-- -->False

  #### Returns AsyncIterator\[AsyncSession]


---

# SqlDatasetClient<!-- -->

SQL implementation of the dataset client.

This client persists dataset items to a SQL database using two tables for storage and retrieval. Items are stored as JSON with automatic ordering preservation.

The dataset data is stored in SQL database tables following the pattern:

* `datasets` table: Contains dataset metadata (id, name, timestamps, item\_count)
* `dataset_records` table: Contains individual items with JSON data and auto-increment ordering
* `dataset_metadata_buffer` table: Buffers metadata updates for performance optimization

Items are stored as a JSON object in SQLite and as JSONB in PostgreSQL. These objects must be JSON-serializable. The `item_id` auto-increment primary key ensures insertion order is preserved. All operations are wrapped in database transactions with CASCADE deletion support.

### Hierarchy

* [SqlClientMixin](https://crawlee.dev/python/python/api/class/SqlClientMixin.md)
* [DatasetClient](https://crawlee.dev/python/python/api/class/DatasetClient.md)
  * *SqlDatasetClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#__init__)
* [**drop](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#drop)
* [**get\_data](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#get_data)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#get_metadata)
* [**get\_session](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#get_session)
* [**iterate\_items](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#iterate_items)
* [**open](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#purge)
* [**push\_data](https://crawlee.dev/python/python/api/class/SqlDatasetClient.md#push_data)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L70)\_\_init\_\_

* ****\_\_init\_\_**(\*, id, storage\_client): None

- Overrides [SqlClientMixin.\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#__init__)

  Initialize a new instance.

  Preferably use the `SqlDatasetClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlyid: str
  * ##### keyword-onlystorage\_client: [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L122)drop

* **async **drop**(): None

- Overrides [DatasetClient.drop](https://crawlee.dev/python/python/api/class/DatasetClient.md#drop)

  Delete this dataset and all its items from the database.

  This operation is irreversible. Uses CASCADE deletion to remove all related items.

  ***

  #### Returns None

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L161)get\_data

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

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L116)get\_metadata

* **async **get\_metadata**(): [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

- Overrides [DatasetClient.get\_metadata](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_metadata)

  Get the metadata of the dataset.

  ***

  #### Returns [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

### [**](#get_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L197)get\_session

* **async **get\_session**(\*, with\_simple\_commit): AsyncIterator\[AsyncSession]

- Inherited from [SqlClientMixin.get\_session](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#get_session)

  Create a new SQLAlchemy session for this storage.

  ***

  #### Parameters

  * ##### optionalkeyword-onlywith\_simple\_commit: bool = <!-- -->False

  #### Returns AsyncIterator\[AsyncSession]

### [**](#iterate_items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L208)iterate\_items

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

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L83)open

* **async **open**(\*, id, name, alias, storage\_client): Self

- Open an existing dataset or create a new one.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the dataset to open. If provided, searches for existing dataset by ID.

  * ##### keyword-onlyname: str | None

    The name of the dataset for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the dataset for unnamed (run scope) storages.

  * ##### keyword-onlystorage\_client: [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

    The SQL storage client instance.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L131)purge

* **async **purge**(): None

- Overrides [DatasetClient.purge](https://crawlee.dev/python/python/api/class/DatasetClient.md#purge)

  Remove all items from this dataset while keeping the dataset structure.

  Resets item\_count to 0 and deletes all records from dataset\_records table.

  ***

  #### Returns None

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_dataset_client.py#L147)push\_data

* **async **push\_data**(data): None

- Overrides [DatasetClient.push\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#push_data)

  Push data to the dataset.

  The backend method for the `Dataset.push_data` call.

  ***

  #### Parameters

  * ##### data: list\[Any] | dict\[str, Any]

  #### Returns None


---

# SqlKeyValueStoreClient<!-- -->

SQL implementation of the key-value store client.

This client persists key-value data to a SQL database with transaction support and concurrent access safety. Keys are mapped to rows in database tables with proper indexing for efficient retrieval.

The key-value store data is stored in SQL database tables following the pattern:

* `key_value_stores` table: Contains store metadata (id, name, timestamps)
* `key_value_store_records` table: Contains individual key-value pairs with binary value storage, content type, and size information
* `key_value_store_metadata_buffer` table: Buffers metadata updates for performance optimization

Values are serialized based on their type: JSON objects are stored as formatted JSON, text values as UTF-8 encoded strings, and binary data as-is in the `LargeBinary` column. The implementation automatically handles content type detection and maintains metadata about each record including size and MIME type information.

All database operations are wrapped in transactions with proper error handling and rollback mechanisms. The client supports atomic upsert operations and handles race conditions when multiple clients access the same store using composite primary keys (key\_value\_store\_id, key).

### Hierarchy

* [SqlClientMixin](https://crawlee.dev/python/python/api/class/SqlClientMixin.md)
* [KeyValueStoreClient](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md)
  * *SqlKeyValueStoreClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#__init__)
* [**delete\_value](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#delete_value)
* [**drop](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#drop)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#get_metadata)
* [**get\_public\_url](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#get_public_url)
* [**get\_session](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#get_session)
* [**get\_value](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#get_value)
* [**iterate\_keys](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#iterate_keys)
* [**open](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#purge)
* [**record\_exists](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#record_exists)
* [**set\_value](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md#set_value)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L74)\_\_init\_\_

* ****\_\_init\_\_**(\*, storage\_client, id): None

- Overrides [SqlClientMixin.\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#__init__)

  Initialize a new instance.

  Preferably use the `SqlKeyValueStoreClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlystorage\_client: [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)
  * ##### keyword-onlyid: str

  #### Returns None

### [**](#delete_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L238)delete\_value

* **async **delete\_value**(\*, key): None

- Overrides [KeyValueStoreClient.delete\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#delete_value)

  Delete a value from the key-value store by its key.

  The backend method for the `KeyValueStore.delete_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L130)drop

* **async **drop**(): None

- Overrides [KeyValueStoreClient.drop](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#drop)

  Delete this key-value store and all its records from the database.

  This operation is irreversible. Uses CASCADE deletion to remove all related records.

  ***

  #### Returns None

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L124)get\_metadata

* **async **get\_metadata**(): [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

- Overrides [KeyValueStoreClient.get\_metadata](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_metadata)

  Get the metadata of the key-value store.

  ***

  #### Returns [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

### [**](#get_public_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L300)get\_public\_url

* **async **get\_public\_url**(\*, key): str

- Overrides [KeyValueStoreClient.get\_public\_url](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_public_url)

  Get the public URL for the given key.

  The backend method for the `KeyValueStore.get_public_url` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns str

### [**](#get_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L197)get\_session

* **async **get\_session**(\*, with\_simple\_commit): AsyncIterator\[AsyncSession]

- Inherited from [SqlClientMixin.get\_session](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#get_session)

  Create a new SQLAlchemy session for this storage.

  ***

  #### Parameters

  * ##### optionalkeyword-onlywith\_simple\_commit: bool = <!-- -->False

  #### Returns AsyncIterator\[AsyncSession]

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L191)get\_value

* **async **get\_value**(\*, key): [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

- Overrides [KeyValueStoreClient.get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_value)

  Retrieve the given record from the key-value store.

  The backend method for the `KeyValueStore.get_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

### [**](#iterate_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L252)iterate\_keys

* **async **iterate\_keys**(\*, exclusive\_start\_key, limit): AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

- Overrides [KeyValueStoreClient.iterate\_keys](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#iterate_keys)

  Iterate over all the existing keys in the key-value store.

  The backend method for the `KeyValueStore.iterate_keys` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyexclusive\_start\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->None

  #### Returns AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L87)open

* **async **open**(\*, id, name, alias, storage\_client): Self

- Open or create a SQL key-value store client.

  This method attempts to open an existing key-value store from the SQL database. If a KVS with the specified ID or name exists, it loads the metadata from the database. If no existing store is found, a new one is created.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the key-value store to open. If provided, searches for existing store by ID.

  * ##### keyword-onlyname: str | None

    The name of the key-value store for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the key-value store for unnamed (run scope) storages.

  * ##### keyword-onlystorage\_client: [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

    The SQL storage client used to access the database.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L139)purge

* **async **purge**(): None

- Overrides [KeyValueStoreClient.purge](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#purge)

  Remove all items from this key-value store while keeping the key-value store structure.

  Remove all records from key\_value\_store\_records table.

  ***

  #### Returns None

### [**](#record_exists)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L287)record\_exists

* **async **record\_exists**(\*, key): bool

- Overrides [KeyValueStoreClient.record\_exists](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#record_exists)

  Check if a record with the given key exists in the key-value store.

  The backend method for the `KeyValueStore.record_exists` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

    The key to check for existence.

  #### Returns bool

  True if a record with the given key exists, False otherwise.

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_key_value_store_client.py#L149)set\_value

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


---

# SqlRequestQueueClient<!-- -->

SQL implementation of the request queue client.

This client persists requests to a SQL database with transaction handling and concurrent access safety. Requests are stored with sequence-based ordering and efficient querying capabilities.

The implementation uses negative sequence numbers for forefront (high-priority) requests and positive sequence numbers for regular requests, allowing for efficient single-query ordering. A cache mechanism reduces database queries.

The request queue data is stored in SQL database tables following the pattern:

* `request_queues` table: Contains queue metadata (id, name, timestamps, request counts, multi-client flag)
* `request_queue_records` table: Contains individual requests with JSON data, unique keys for deduplication, sequence numbers for ordering, and processing status flags
* `request_queue_state` table: Maintains counters for sequence numbers to ensure proper ordering of requests.
* `request_queue_metadata_buffer` table: Buffers metadata updates for performance optimization

Requests are serialized to JSON for storage and maintain proper ordering through sequence numbers. The implementation provides concurrent access safety through transaction handling, locking mechanisms, and optimized database indexes for efficient querying.

### Hierarchy

* [SqlClientMixin](https://crawlee.dev/python/python/api/class/SqlClientMixin.md)
* [RequestQueueClient](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)
  * *SqlRequestQueueClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#__init__)
* [**add\_batch\_of\_requests](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#add_batch_of_requests)
* [**drop](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#fetch_next_request)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#get_metadata)
* [**get\_request](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#get_request)
* [**get\_session](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#get_session)
* [**is\_empty](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#is_empty)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#mark_request_as_handled)
* [**open](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#purge)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md#reclaim_request)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L103)\_\_init\_\_

* ****\_\_init\_\_**(\*, id, storage\_client): None

- Overrides [SqlClientMixin.\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#__init__)

  Initialize a new instance.

  Preferably use the `SqlRequestQueueClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlyid: str
  * ##### keyword-onlystorage\_client: [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

  #### Returns None

### [**](#add_batch_of_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L207)add\_batch\_of\_requests

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

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L175)drop

* **async **drop**(): None

- Overrides [RequestQueueClient.drop](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#drop)

  Delete this request queue and all its records from the database.

  This operation is irreversible. Uses CASCADE deletion to remove all related records.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L419)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#fetch_next_request)

  Return the next request in the queue to be processed.

  Once you successfully finish processing of the request, you need to call `RequestQueue.mark_request_as_handled` to mark the request as handled in the queue. If there was some error in processing the request, call `RequestQueue.reclaim_request` instead, so that the queue will give the request to some other consumer in another call to the `fetch_next_request` method.

  Note that the `None` return value does not mean the queue processing finished, it means there are currently no pending requests. To check whether all requests in queue were finished, use `RequestQueue.is_finished` instead.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The request or `None` if there are no more pending requests.

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L167)get\_metadata

* **async **get\_metadata**(): [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [RequestQueueClient.get\_metadata](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_metadata)

  Get the metadata of the request queue.

  ***

  #### Returns [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#get_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L399)get\_request

* **async **get\_request**(unique\_key): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.get\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_request)

  Retrieve a request from the queue.

  ***

  #### Parameters

  * ##### unique\_key: str

    Unique key of the request to retrieve.

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The retrieved request, or None, if it did not exist.

### [**](#get_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L197)get\_session

* **async **get\_session**(\*, with\_simple\_commit): AsyncIterator\[AsyncSession]

- Inherited from [SqlClientMixin.get\_session](https://crawlee.dev/python/python/api/class/SqlClientMixin.md#get_session)

  Create a new SQLAlchemy session for this storage.

  ***

  #### Parameters

  * ##### optionalkeyword-onlywith\_simple\_commit: bool = <!-- -->False

  #### Returns AsyncIterator\[AsyncSession]

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L597)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestQueueClient.is\_empty](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#is_empty)

  Check if the request queue is empty.

  ***

  #### Returns bool

  True if the request queue is empty, False otherwise.

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L507)mark\_request\_as\_handled

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

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L125)open

* **async **open**(\*, id, name, alias, storage\_client): Self

- Open an existing request queue or create a new one.

  This method first tries to find an existing queue by ID or name. If found, it returns a client for that queue. If not found, it creates a new queue with the specified parameters.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the request queue to open. Takes precedence over name.

  * ##### keyword-onlyname: str | None

    The name of the request queue for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the request queue for unnamed (run scope) storages.

  * ##### keyword-onlystorage\_client: [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

    The SQL storage client used to access the database.

  #### Returns Self

  An instance for the opened or created request queue.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L186)purge

* **async **purge**(): None

- Overrides [RequestQueueClient.purge](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#purge)

  Remove all items from this dataset while keeping the dataset structure.

  Resets pending\_request\_count and handled\_request\_count to 0 and deletes all records from request\_queue\_records table.

  ***

  #### Returns None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_request_queue_client.py#L539)reclaim\_request

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


---

# SqlStorageClient<!-- -->

SQL implementation of the storage client.

This storage client provides access to datasets, key-value stores, and request queues that persist data to a SQL database using SQLAlchemy 2+. Each storage type uses two tables: one for metadata and one for records.

The client accepts either a database connection string or a pre-configured AsyncEngine. If neither is provided, it creates a default SQLite database 'crawlee.db' in the storage directory.

Database schema is automatically created during initialization. SQLite databases receive performance optimizations including WAL mode and increased cache size.

Warning

This is an experimental feature. The behavior and interface may change in future versions.

### Hierarchy

* [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)
  * *SqlStorageClient*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#__init__)
* [**close](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#close)
* [**create\_dataset\_client](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#create_dataset_client)
* [**create\_kvs\_client](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#create_kvs_client)
* [**create\_rq\_client](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#create_rq_client)
* [**create\_session](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#create_session)
* [**get\_dialect\_name](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#get_dialect_name)
* [**get\_rate\_limit\_errors](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#get_rate_limit_errors)
* [**get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#get_storage_client_cache_key)
* [**initialize](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#initialize)

### Properties

* [**engine](https://crawlee.dev/python/python/api/class/SqlStorageClient.md#engine)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L88)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

- Async context manager entry.

  ***

  #### Returns [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L92)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Async context manager exit.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L57)\_\_init\_\_

* ****\_\_init\_\_**(\*, connection\_string, engine): None

- Initialize the SQL storage client.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyconnection\_string: str | None = <!-- -->None

    Database connection string (e.g., "sqlite+aiosqlite:///crawlee.db"). If not provided, defaults to SQLite database in the storage directory.

  * ##### optionalkeyword-onlyengine: AsyncEngine | None = <!-- -->None

    Pre-configured AsyncEngine instance. If provided, connection\_string is ignored.

  #### Returns None

### [**](#close)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L157)close

* **async **close**(): None

- Close the database connection pool.

  ***

  #### Returns None

### [**](#create_dataset_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L178)create\_dataset\_client

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

### [**](#create_kvs_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L200)create\_kvs\_client

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

### [**](#create_rq_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L222)create\_rq\_client

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

### [**](#create_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L167)create\_session

* ****create\_session**(): AsyncSession

- Create a new database session.

  ***

  #### Returns AsyncSession

  A new AsyncSession instance.

### [**](#get_dialect_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L108)get\_dialect\_name

* ****get\_dialect\_name**(): str | None

- Get the database dialect name.

  ***

  #### Returns str | None

### [**](#get_rate_limit_errors)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L74)get\_rate\_limit\_errors

* ****get\_rate\_limit\_errors**(): dict\[int, int]

- Inherited from [StorageClient.get\_rate\_limit\_errors](https://crawlee.dev/python/python/api/class/StorageClient.md#get_rate_limit_errors)

  Return statistics about rate limit errors encountered by the HTTP client in storage client.

  ***

  #### Returns dict\[int, int]

### [**](#get_storage_client_cache_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L33)get\_storage\_client\_cache\_key

* ****get\_storage\_client\_cache\_key**(configuration): Hashable

- Inherited from [StorageClient.get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/StorageClient.md#get_storage_client_cache_key)

  Return a cache key that can differentiate between different storages of this and other clients.

  Can be based on configuration or on the client itself. By default, returns a module and name of the client class.

  ***

  #### Parameters

  * ##### configuration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

  #### Returns Hashable

### [**](#initialize)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L112)initialize

* **async **initialize**(configuration): None

- Initialize the database schema.

  This method creates all necessary tables if they don't exist. Should be called before using the storage client.

  ***

  #### Parameters

  * ##### configuration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#engine)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_storage_client.py#L102)engine

**engine: AsyncEngine

Get the SQLAlchemy AsyncEngine instance.


---

# Statistics<!-- -->

A class for collecting, tracking, and logging runtime statistics for requests.

It is designed to record information such as request durations, retries, successes, and failures, enabling analysis of crawler performance. The collected statistics are persisted to a `KeyValueStore`, ensuring they remain available across crawler migrations, abortions, and restarts. This persistence allows for tracking and evaluation of crawler behavior over its lifecycle.

### Hierarchy

* *Statistics*
  * [\_NonPersistentStatistics](https://crawlee.dev/python/python/api/class/_NonPersistentStatistics.md)

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__init__)
* [**calculate](https://crawlee.dev/python/python/api/class/Statistics.md#calculate)
* [**record\_request\_processing\_failure](https://crawlee.dev/python/python/api/class/Statistics.md#record_request_processing_failure)
* [**record\_request\_processing\_finish](https://crawlee.dev/python/python/api/class/Statistics.md#record_request_processing_finish)
* [**record\_request\_processing\_start](https://crawlee.dev/python/python/api/class/Statistics.md#record_request_processing_start)
* [**register\_status\_code](https://crawlee.dev/python/python/api/class/Statistics.md#register_status_code)
* [**replace\_state\_model](https://crawlee.dev/python/python/api/class/Statistics.md#replace_state_model)
* [**reset](https://crawlee.dev/python/python/api/class/Statistics.md#reset)
* [**with\_default\_state](https://crawlee.dev/python/python/api/class/Statistics.md#with_default_state)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/Statistics.md#active)
* [**state](https://crawlee.dev/python/python/api/class/Statistics.md#state)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L158)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): Self

- Overrides [Statistics.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__aenter__)

  Subscribe to events and start collecting statistics.

  ***

  #### Returns Self

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L180)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Overrides [Statistics.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/Statistics.md#__aexit__)

  Stop collecting statistics.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L71)\_\_init\_\_

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

- Calculate the current statistics.

  ***

  #### Returns [FinalStatistics](https://crawlee.dev/python/python/api/class/FinalStatistics.md)

### [**](#record_request_processing_failure)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L244)record\_request\_processing\_failure

* ****record\_request\_processing\_failure**(request\_id\_or\_key): None

- Mark a request as failed.

  ***

  #### Parameters

  * ##### request\_id\_or\_key: str

  #### Returns None

### [**](#record_request_processing_finish)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L222)record\_request\_processing\_finish

* ****record\_request\_processing\_finish**(request\_id\_or\_key): None

- Mark a request as finished.

  ***

  #### Parameters

  * ##### request\_id\_or\_key: str

  #### Returns None

### [**](#record_request_processing_start)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L215)record\_request\_processing\_start

* ****record\_request\_processing\_start**(request\_id\_or\_key): None

- Mark a request as started.

  ***

  #### Parameters

  * ##### request\_id\_or\_key: str

  #### Returns None

### [**](#register_status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L208)register\_status\_code

* ****register\_status\_code**(code): None

- Increment the number of times a status code has been received.

  ***

  #### Parameters

  * ##### code: int

  #### Returns None

### [**](#replace_state_model)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L113)replace\_state\_model

* ****replace\_state\_model**(state\_model): [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[TNewStatisticsState](https://crawlee.dev/python/python/api.md#TNewStatisticsState)]

- Create near copy of the `Statistics` with replaced `state_model`.

  ***

  #### Parameters

  * ##### state\_model: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[[TNewStatisticsState](https://crawlee.dev/python/python/api.md#TNewStatisticsState)]

  #### Returns [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[TNewStatisticsState](https://crawlee.dev/python/python/api.md#TNewStatisticsState)]

### [**](#reset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L277)reset

* **async **reset**(): None

- Reset the statistics to their defaults and remove any persistent state.

  ***

  #### Returns None

### [**](#with_default_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L127)with\_default\_state

* ****with\_default\_state**(\*, persistence\_enabled, persist\_state\_kvs\_name, persist\_state\_key, persist\_state\_kvs\_factory, log\_message, periodic\_message\_logger, log\_interval, statistics\_log\_format, save\_error\_snapshots): [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[StatisticsState](https://crawlee.dev/python/python/api/class/StatisticsState.md)]

- Initialize a new instance with default state model `StatisticsState`.

  ***

  #### Parameters

  * ##### optionalkeyword-onlypersistence\_enabled: bool = <!-- -->False
  * ##### optionalkeyword-onlypersist\_state\_kvs\_name: str | None = <!-- -->None
  * ##### optionalkeyword-onlypersist\_state\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlypersist\_state\_kvs\_factory: Callable\[\[], Coroutine\[None, None, [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)]] | None = <!-- -->None
  * ##### optionalkeyword-onlylog\_message: str = <!-- -->'Statistics'
  * ##### optionalkeyword-onlyperiodic\_message\_logger: Logger | None = <!-- -->None
  * ##### optionalkeyword-onlylog\_interval: timedelta = <!-- -->timedelta(minutes=1)
  * ##### optionalkeyword-onlystatistics\_log\_format: Literal\[table, inline] = <!-- -->'table'
  * ##### optionalkeyword-onlysave\_error\_snapshots: bool = <!-- -->False

  #### Returns [Statistics](https://crawlee.dev/python/python/api/class/Statistics.md)\[[StatisticsState](https://crawlee.dev/python/python/api/class/StatisticsState.md)]

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L154)active

**active: bool

Indicate whether the context is active.

### [**](#state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L204)state

**state: [TStatisticsState](https://crawlee.dev/python/python/api.md#TStatisticsState)


---

# StatisticsState<!-- -->

Statistic data about a crawler run.

### Hierarchy

* *StatisticsState*
  * [AdaptivePlaywrightCrawlerStatisticState](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlerStatisticState.md)

## Index[**](#Index)

### Methods

* [**crawler\_runtime](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime)
* [**crawler\_runtime\_for\_serialization](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime_for_serialization)
* [**model\_post\_init](https://crawlee.dev/python/python/api/class/StatisticsState.md#model_post_init)

### Properties

* [**crawler\_finished\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_finished_at)
* [**crawler\_last\_started\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_last_started_at)
* [**crawler\_runtime](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime)
* [**crawler\_started\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_started_at)
* [**model\_config](https://crawlee.dev/python/python/api/class/StatisticsState.md#model_config)
* [**request\_avg\_failed\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_avg_failed_duration)
* [**request\_avg\_finished\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_avg_finished_duration)
* [**request\_max\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_max_duration)
* [**request\_min\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_min_duration)
* [**request\_retry\_histogram](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_retry_histogram)
* [**request\_total\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_total_duration)
* [**request\_total\_failed\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_total_failed_duration)
* [**request\_total\_finished\_duration](https://crawlee.dev/python/python/api/class/StatisticsState.md#request_total_finished_duration)
* [**requests\_failed](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_failed)
* [**requests\_failed\_per\_minute](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_failed_per_minute)
* [**requests\_finished](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_finished)
* [**requests\_finished\_per\_minute](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_finished_per_minute)
* [**requests\_retries](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_retries)
* [**requests\_total](https://crawlee.dev/python/python/api/class/StatisticsState.md#requests_total)
* [**stats\_id](https://crawlee.dev/python/python/api/class/StatisticsState.md#stats_id)
* [**stats\_persisted\_at](https://crawlee.dev/python/python/api/class/StatisticsState.md#stats_persisted_at)

## Methods<!-- -->[**](#Methods)

### [**](#crawler_runtime)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L121)crawler\_runtime

* ****crawler\_runtime**(value): None

- Inherited from [StatisticsState.crawler\_runtime](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime)

  Overrides [StatisticsState.crawler\_runtime](https://crawlee.dev/python/python/api/class/StatisticsState.md#crawler_runtime)

  #### Parameters

  * ##### value: timedelta

  #### Returns None

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

### [**](#crawler_finished_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L79)crawler\_finished\_at

**crawler\_finished\_at: datetime | None

### [**](#crawler_last_started_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L78)crawler\_last\_started\_at

**crawler\_last\_started\_at: datetime | None

### [**](#crawler_runtime)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L114)crawler\_runtime

**crawler\_runtime: timedelta

### [**](#crawler_started_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L77)crawler\_started\_at

**crawler\_started\_at: datetime | None

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L61)model\_config

**model\_config: Undefined

### [**](#request_avg_failed_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L145)request\_avg\_failed\_duration

**request\_avg\_failed\_duration: timedelta | None

### [**](#request_avg_finished_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L150)request\_avg\_finished\_duration

**request\_avg\_finished\_duration: timedelta | None

### [**](#request_max_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L70)request\_max\_duration

**request\_max\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms) | None

### [**](#request_min_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L69)request\_min\_duration

**request\_min\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms) | None

### [**](#request_retry_histogram)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L97)request\_retry\_histogram

**request\_retry\_histogram: dict\[int, int]

### [**](#request_total_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L140)request\_total\_duration

**request\_total\_duration: timedelta

### [**](#request_total_failed_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L71)request\_total\_failed\_duration

**request\_total\_failed\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms)

### [**](#request_total_finished_duration)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L74)request\_total\_finished\_duration

**request\_total\_finished\_duration: [timedelta\_ms](https://crawlee.dev/python/python/api.md#timedelta_ms)

### [**](#requests_failed)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L65)requests\_failed

**requests\_failed: int

### [**](#requests_failed_per_minute)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L67)requests\_failed\_per\_minute

**requests\_failed\_per\_minute: float

### [**](#requests_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L64)requests\_finished

**requests\_finished: int

### [**](#requests_finished_per_minute)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L68)requests\_finished\_per\_minute

**requests\_finished\_per\_minute: float

### [**](#requests_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L66)requests\_retries

**requests\_retries: int

### [**](#requests_total)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L155)requests\_total

**requests\_total: int

### [**](#stats_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L62)stats\_id

**stats\_id: int | None

### [**](#stats_persisted_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_models.py#L94)stats\_persisted\_at

**stats\_persisted\_at: datetime | None


---

# Storage<!-- -->

Base class for storages.

### Hierarchy

* *Storage*

  * [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)
  * [RequestQueue](https://crawlee.dev/python/python/api/class/RequestQueue.md)
  * [Dataset](https://crawlee.dev/python/python/api/class/Dataset.md)

## Index[**](#Index)

### Methods

* [**drop](https://crawlee.dev/python/python/api/class/Storage.md#drop)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/Storage.md#get_metadata)
* [**open](https://crawlee.dev/python/python/api/class/Storage.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/Storage.md#purge)

### Properties

* [**id](https://crawlee.dev/python/python/api/class/Storage.md#id)
* [**name](https://crawlee.dev/python/python/api/class/Storage.md#name)

## Methods<!-- -->[**](#Methods)

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_base.py#L57)drop

* **async **drop**(): None

- Overrides [Storage.drop](https://crawlee.dev/python/python/api/class/Storage.md#drop)

  Drop the storage, removing it from the underlying storage client and clearing the cache.

  ***

  #### Returns None

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_base.py#L29)get\_metadata

* **async **get\_metadata**(): ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [Storage.get\_metadata](https://crawlee.dev/python/python/api/class/Storage.md#get_metadata)

  Get the storage metadata.

  ***

  #### Returns ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_base.py#L34)open

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

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_base.py#L61)purge

* **async **purge**(): None

- Overrides [Storage.purge](https://crawlee.dev/python/python/api/class/Storage.md#purge)

  Purge the storage, removing all items from the underlying storage client.

  This method does not remove the storage itself, e.g. don't remove the metadata, but clears all items within it.

  ***

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_base.py#L20)id

**id: str

Get the storage ID.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_base.py#L25)name

**name: str | None

Get the storage name.


---

# StorageClient<!-- -->

Base class for storage clients.

The `StorageClient` serves as an abstract base class that defines the interface for accessing Crawlee's storage types: datasets, key-value stores, and request queues. It provides methods to open clients for each of these storage types and handles common functionality.

Storage clients implementations can be provided for various backends (file system, memory, databases, various cloud providers, etc.) to support different use cases from development to production environments.

Each storage client implementation is responsible for ensuring proper initialization, data persistence (where applicable), and consistent access patterns across all storage types it supports.

### Hierarchy

* *StorageClient*

  * [MemoryStorageClient](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md)
  * [FileSystemStorageClient](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md)
  * [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md)
  * [RedisStorageClient](https://crawlee.dev/python/python/api/class/RedisStorageClient.md)

## Index[**](#Index)

### Methods

* [**create\_dataset\_client](https://crawlee.dev/python/python/api/class/StorageClient.md#create_dataset_client)
* [**create\_kvs\_client](https://crawlee.dev/python/python/api/class/StorageClient.md#create_kvs_client)
* [**create\_rq\_client](https://crawlee.dev/python/python/api/class/StorageClient.md#create_rq_client)
* [**get\_rate\_limit\_errors](https://crawlee.dev/python/python/api/class/StorageClient.md#get_rate_limit_errors)
* [**get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/StorageClient.md#get_storage_client_cache_key)

## Methods<!-- -->[**](#Methods)

### [**](#create_dataset_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L42)create\_dataset\_client

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

### [**](#create_kvs_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L53)create\_kvs\_client

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

### [**](#create_rq_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L64)create\_rq\_client

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

- Return statistics about rate limit errors encountered by the HTTP client in storage client.

  ***

  #### Returns dict\[int, int]

### [**](#get_storage_client_cache_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L33)get\_storage\_client\_cache\_key

* ****get\_storage\_client\_cache\_key**(configuration): Hashable

- Overrides [StorageClient.get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/StorageClient.md#get_storage_client_cache_key)

  Return a cache key that can differentiate between different storages of this and other clients.

  Can be based on configuration or on the client itself. By default, returns a module and name of the client class.

  ***

  #### Parameters

  * ##### configuration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

  #### Returns Hashable


---

# StorageInstanceManager<!-- -->

Manager for caching and managing storage instances.

This class centralizes the caching logic for all storage types (Dataset, KeyValueStore, RequestQueue) and provides a unified interface for opening and managing storage instances.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/StorageInstanceManager.md#__init__)
* [**clear\_cache](https://crawlee.dev/python/python/api/class/StorageInstanceManager.md#clear_cache)
* [**open\_storage\_instance](https://crawlee.dev/python/python/api/class/StorageInstanceManager.md#open_storage_instance)
* [**remove\_from\_cache](https://crawlee.dev/python/python/api/class/StorageInstanceManager.md#remove_from_cache)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L79)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#clear_cache)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L203)clear\_cache

* ****clear\_cache**(): None

- Clear all cached storage instances.

  ***

  #### Returns None

### [**](#open_storage_instance)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L83)open\_storage\_instance

* **async **open\_storage\_instance**(\*, id, name, alias, client\_opener\_coro, storage\_client\_cache\_key): [T](https://crawlee.dev/python/python/api.md#T)

- Open a storage instance with caching support.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    Storage ID.

  * ##### keyword-onlyname: str | None

    Storage name. (global scope, persists across runs). Name can only contain letters "a" through "z", the digits "0" through "9", and the hyphen ("-") but only in the middle of the string (e.g. "my-value-1").

  * ##### keyword-onlyalias: str | None

    Storage alias (run scope, creates unnamed storage).

  * ##### keyword-onlyclient\_opener\_coro: [ClientOpenerCoro](https://crawlee.dev/python/python/api.md#ClientOpenerCoro)

    Coroutine to open the storage client when storage instance not found in cache.

  * ##### optionalkeyword-onlystorage\_client\_cache\_key: Hashable = <!-- -->''

    Additional optional key from storage client to differentiate cache entries.

  #### Returns [T](https://crawlee.dev/python/python/api.md#T)

  The storage instance.

### [**](#remove_from_cache)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_storage_instance_manager.py#L195)remove\_from\_cache

* ****remove\_from\_cache**(storage\_instance): None

- Remove a storage instance from the cache.

  ***

  #### Parameters

  * ##### storage\_instance: [Storage](https://crawlee.dev/python/python/api/class/Storage.md)

    The storage instance to remove.

  #### Returns None


---

# StorageMetadata<!-- -->

Represents the base model for storage metadata.

It contains common fields shared across all specific storage types.

### Hierarchy

* *StorageMetadata*

  * [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)
  * [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)
  * [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#accessed_at)
* [**created\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#created_at)
* [**id](https://crawlee.dev/python/python/api/class/StorageMetadata.md#id)
* [**model\_config](https://crawlee.dev/python/python/api/class/StorageMetadata.md#model_config)
* [**modified\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/StorageMetadata.md#name)

## Properties<!-- -->[**](#Properties)

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L31)accessed\_at

**accessed\_at: datetime

The timestamp when the storage was last accessed.

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L34)created\_at

**created\_at: datetime

The timestamp when the storage was created.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L25)id

**id: str

The unique identifier of the storage.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L23)model\_config

**model\_config: Undefined

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L37)modified\_at

**modified\_at: datetime

The timestamp when the storage was last modified.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L28)name

**name: str | None

The name of the storage.


---

# StorageMetadataDb<!-- -->

Base database model for storage metadata.

### Hierarchy

* *StorageMetadataDb*

  * [DatasetMetadataDb](https://crawlee.dev/python/python/api/class/DatasetMetadataDb.md)
  * [RequestQueueMetadataDb](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md)
  * [KeyValueStoreMetadataDb](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md)

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#accessed_at)
* [**buffer\_locked\_until](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#buffer_locked_until)
* [**created\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#created_at)
* [**internal\_name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#internal_name)
* [**modified\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#name)

## Properties<!-- -->[**](#Properties)

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L61)accessed\_at

**accessed\_at: Mapped\[datetime]

Last access datetime for usage tracking.

### [**](#buffer_locked_until)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L70)buffer\_locked\_until

**buffer\_locked\_until: Mapped\[datetime | None]

Timestamp until which buffer processing is locked for this storage. NULL = unlocked.

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L64)created\_at

**created\_at: Mapped\[datetime]

Creation datetime.

### [**](#internal_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L55)internal\_name

**internal\_name: Mapped\[str]

Internal unique name for a storage instance based on a name or alias.

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L67)modified\_at

**modified\_at: Mapped\[datetime]

Last modification datetime.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L58)name

**name: Mapped\[str | None]

Human-readable name. None becomes 'default' in database to enforce uniqueness.


---

# SubCrawlerRun<!-- -->

## Index[**](#Index)

### Properties

* [**exception](https://crawlee.dev/python/python/api/class/SubCrawlerRun.md#exception)
* [**result](https://crawlee.dev/python/python/api/class/SubCrawlerRun.md#result)

## Properties<!-- -->[**](#Properties)

### [**](#exception)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L502)exception

**exception: Exception | None

### [**](#result)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_adaptive_playwright_crawler.py#L501)result

**result: [RequestHandlerRunResult](https://crawlee.dev/python/python/api/class/RequestHandlerRunResult.md) | None


---

# SystemInfo<!-- -->

Represent the current status of the system.

## Index[**](#Index)

### Methods

* [**\_\_str\_\_](https://crawlee.dev/python/python/api/class/SystemInfo.md#__str__)

### Properties

* [**client\_info](https://crawlee.dev/python/python/api/class/SystemInfo.md#client_info)
* [**cpu\_info](https://crawlee.dev/python/python/api/class/SystemInfo.md#cpu_info)
* [**created\_at](https://crawlee.dev/python/python/api/class/SystemInfo.md#created_at)
* [**event\_loop\_info](https://crawlee.dev/python/python/api/class/SystemInfo.md#event_loop_info)
* [**is\_system\_idle](https://crawlee.dev/python/python/api/class/SystemInfo.md#is_system_idle)
* [**memory\_info](https://crawlee.dev/python/python/api/class/SystemInfo.md#memory_info)

## Methods<!-- -->[**](#Methods)

### [**](#__str__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L62)\_\_str\_\_

* ****\_\_str\_\_**(): str

- Get a string representation of the system info.

  ***

  #### Returns str

## Properties<!-- -->[**](#Properties)

### [**](#client_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L46)client\_info

**client\_info: [LoadRatioInfo](https://crawlee.dev/python/python/api/class/LoadRatioInfo.md)

The client load ratio.

### [**](#cpu_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L37)cpu\_info

**cpu\_info: [LoadRatioInfo](https://crawlee.dev/python/python/api/class/LoadRatioInfo.md)

The CPU load ratio.

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L49)created\_at

**created\_at: datetime

The time at which the system load information was measured.

### [**](#event_loop_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L43)event\_loop\_info

**event\_loop\_info: [LoadRatioInfo](https://crawlee.dev/python/python/api/class/LoadRatioInfo.md)

The event loop load ratio.

### [**](#is_system_idle)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L53)is\_system\_idle

**is\_system\_idle: bool

Indicate whether the system is currently idle or overloaded.

### [**](#memory_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L40)memory\_info

**memory\_info: [LoadRatioInfo](https://crawlee.dev/python/python/api/class/LoadRatioInfo.md)

The memory load ratio.


---

