# ProcessedRequest<!-- -->

Represents a processed request.

## Index[**](#Index)

### Properties

* [**id](https://crawlee.dev/python/python/api/class/ProcessedRequest.md#id)
* [**model\_config](https://crawlee.dev/python/python/api/class/ProcessedRequest.md#model_config)
* [**unique\_key](https://crawlee.dev/python/python/api/class/ProcessedRequest.md#unique_key)
* [**was\_already\_handled](https://crawlee.dev/python/python/api/class/ProcessedRequest.md#was_already_handled)
* [**was\_already\_present](https://crawlee.dev/python/python/api/class/ProcessedRequest.md#was_already_present)

## Properties<!-- -->[**](#Properties)

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L145)id

**id: str | None

Internal representation of the request by the storage client. Only some clients use id.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L143)model\_config

**model\_config: Undefined

### [**](#unique_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L148)unique\_key

**unique\_key: str

### [**](#was_already_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L150)was\_already\_handled

**was\_already\_handled: bool

### [**](#was_already_present)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L149)was\_already\_present

**was\_already\_present: bool


---

# ProxyConfiguration<!-- -->

Configures connection to a proxy server with the provided options.

Proxy servers are used to prevent target websites from blocking your crawlers based on IP address rate limits or blacklists. Setting proxy configuration in your crawlers automatically configures them to use the selected proxies for all connections. You can get information about the currently used proxy by inspecting the [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) property in your crawler's page function. There, you can inspect the proxy's URL and other attributes.

If you want to use your own proxies, use the ProxyConfigurationOptions.proxyUrls option. Your list of proxy URLs will be rotated by the configuration if this option is provided.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md#__init__)
* [**new\_proxy\_info](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md#new_proxy_info)
* [**new\_url](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md#new_url)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L68)\_\_init\_\_

* ****\_\_init\_\_**(\*, proxy\_urls, new\_url\_function, tiered\_proxy\_urls): None

- Initialize a new instance.

  Exactly one of `proxy_urls`, `tiered_proxy_urls` or `new_url_function` must be specified.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyproxy\_urls: list\[str | None] | None = <!-- -->None

    A list of URLs of proxies that will be rotated in a round-robin fashion

  * ##### optionalkeyword-onlynew\_url\_function: [\_NewUrlFunction](https://crawlee.dev/python/python/api/class/_NewUrlFunction.md) | None = <!-- -->None

    A function that returns a proxy URL for a given Request. This provides full control over the proxy selection mechanism.

  * ##### optionalkeyword-onlytiered\_proxy\_urls: list\[list\[str | None]] | None = <!-- -->None

    A list of URL tiers (where a tier is a list of proxy URLs). Crawlers will automatically try to use the lowest tier (smallest index) where blocking does not happen. The proxy URLs in the selected tier will be rotated in a round-robin fashion.

  #### Returns None

### [**](#new_proxy_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L114)new\_proxy\_info

* **async **new\_proxy\_info**(session\_id, request, proxy\_tier): [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None

- Return a new ProxyInfo object based on the configured proxy rotation strategy.

  ***

  #### Parameters

  * ##### session\_id: str | None

    Session identifier. If provided, same proxy URL will be returned for subsequent calls with this ID. Will be auto-generated for tiered proxies if not provided.

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

    Request object used for proxy rotation and tier selection. Required for tiered proxies to track retries and adjust tier accordingly.

  * ##### proxy\_tier: int | None

    Specific proxy tier to use. If not provided, will be automatically selected based on configuration.

  #### Returns [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None

### [**](#new_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L159)new\_url

* **async **new\_url**(session\_id, request, proxy\_tier): str | None

- Return a proxy URL string based on the configured proxy rotation strategy.

  ***

  #### Parameters

  * ##### optionalsession\_id: str | None = <!-- -->None

    Session identifier. If provided, same proxy URL will be returned for subsequent calls with this ID. Will be auto-generated for tiered proxies if not provided.

  * ##### optionalrequest: [Request](https://crawlee.dev/python/python/api/class/Request.md) | None = <!-- -->None

    Request object used for proxy rotation and tier selection. Required for tiered proxies to track retries and adjust tier accordingly.

  * ##### optionalproxy\_tier: int | None = <!-- -->None

    Specific proxy tier to use. If not provided, will be automatically selected based on configuration.

  #### Returns str | None


---

# ProxyError<!-- -->

Raised when a proxy is being blocked or malfunctions.

### Hierarchy

* [SessionError](https://crawlee.dev/python/python/api/class/SessionError.md)
  * *ProxyError*


---

# ProxyInfo<!-- -->

Provides information about a proxy connection that is used for requests.

## Index[**](#Index)

### Properties

* [**hostname](https://crawlee.dev/python/python/api/class/ProxyInfo.md#hostname)
* [**password](https://crawlee.dev/python/python/api/class/ProxyInfo.md#password)
* [**port](https://crawlee.dev/python/python/api/class/ProxyInfo.md#port)
* [**proxy\_tier](https://crawlee.dev/python/python/api/class/ProxyInfo.md#proxy_tier)
* [**scheme](https://crawlee.dev/python/python/api/class/ProxyInfo.md#scheme)
* [**session\_id](https://crawlee.dev/python/python/api/class/ProxyInfo.md#session_id)
* [**url](https://crawlee.dev/python/python/api/class/ProxyInfo.md#url)
* [**username](https://crawlee.dev/python/python/api/class/ProxyInfo.md#username)

## Properties<!-- -->[**](#Properties)

### [**](#hostname)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L35)hostname

**hostname: str

The hostname of the proxy.

### [**](#password)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L44)password

**password: str

The password for the proxy.

### [**](#port)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L38)port

**port: int

The proxy port.

### [**](#proxy_tier)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L51)proxy\_tier

**proxy\_tier: int | None

The tier of the proxy.

### [**](#scheme)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L32)scheme

**scheme: str

The scheme of the proxy.

### [**](#session_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L47)session\_id

**session\_id: str | None

The identifier of the used proxy session, if used. Using the same session ID guarantees getting the same proxy URL.

### [**](#url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L29)url

**url: str

The URL of the proxy.

### [**](#username)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/proxy_configuration.py#L41)username

**username: str

The username for the proxy.


---

# PushDataFunction<!-- -->

A function for pushing data to a `Dataset`.

It simplifies the process of adding data to a `Dataset`. It opens the specified one and pushes the provided data to it.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/PushDataFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L544)\_\_call\_\_

* ****\_\_call\_\_**(data, dataset\_id, dataset\_name, dataset\_alias): Coroutine\[None, None, None]

- Call dunder method.

  ***

  #### Parameters

  * ##### data: list\[dict\[str, Any]] | dict\[str, Any]

    The data to push to the `Dataset`.

  * ##### optionaldataset\_id: str | None = <!-- -->None

    The ID of the `Dataset` to push the data to.

  * ##### optionaldataset\_name: str | None = <!-- -->None

    The name of the `Dataset` to push the data to (global scope, named storage).

  * ##### optionaldataset\_alias: str | None = <!-- -->None

    The alias of the `Dataset` to push the data to (run scope, unnamed storage).

  #### Returns Coroutine\[None, None, None]


---

# PushDataFunctionCall<!-- -->

### Hierarchy

* [PushDataKwargs](https://crawlee.dev/python/python/api/class/PushDataKwargs.md)
  * *PushDataFunctionCall*

## Index[**](#Index)

### Properties

* [**data](https://crawlee.dev/python/python/api/class/PushDataFunctionCall.md#data)
* [**dataset\_alias](https://crawlee.dev/python/python/api/class/PushDataFunctionCall.md#dataset_alias)
* [**dataset\_id](https://crawlee.dev/python/python/api/class/PushDataFunctionCall.md#dataset_id)
* [**dataset\_name](https://crawlee.dev/python/python/api/class/PushDataFunctionCall.md#dataset_name)

## Properties<!-- -->[**](#Properties)

### [**](#data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L201)data

**data: list\[dict\[str, Any]] | dict\[str, Any]

### [**](#dataset_alias)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L204)dataset\_alias

**dataset\_alias: str | None

### [**](#dataset_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L202)dataset\_id

**dataset\_id: str | None

### [**](#dataset_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L203)dataset\_name

**dataset\_name: str | None


---

# PushDataKwargs<!-- -->

Keyword arguments for dataset's `push_data` method.

### Hierarchy

* *PushDataKwargs*
  * [PushDataFunctionCall](https://crawlee.dev/python/python/api/class/PushDataFunctionCall.md)


---

# Ratio<!-- -->

Represents ratio of memory.

## Index[**](#Index)

### Properties

* [**value](https://crawlee.dev/python/python/api/class/Ratio.md#value)

## Properties<!-- -->[**](#Properties)

### [**](#value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L178)value

**value: float


---

# RecoverableState<!-- -->

A class for managing persistent recoverable state using a Pydantic model.

This class facilitates state persistence to a `KeyValueStore`, allowing data to be saved and retrieved across migrations or restarts. It manages the loading, saving, and resetting of state data, with optional persistence capabilities.

The state is represented by a Pydantic model that can be serialized to and deserialized from JSON. The class automatically hooks into the event system to persist state when needed.

Type Parameters: TStateModel: A Pydantic BaseModel type that defines the structure of the state data. Typically, it should be inferred from the `default_state` constructor parameter.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RecoverableState.md#__init__)
* [**has\_persisted\_state](https://crawlee.dev/python/python/api/class/RecoverableState.md#has_persisted_state)
* [**initialize](https://crawlee.dev/python/python/api/class/RecoverableState.md#initialize)
* [**persist\_state](https://crawlee.dev/python/python/api/class/RecoverableState.md#persist_state)
* [**reset](https://crawlee.dev/python/python/api/class/RecoverableState.md#reset)
* [**teardown](https://crawlee.dev/python/python/api/class/RecoverableState.md#teardown)

### Properties

* [**current\_value](https://crawlee.dev/python/python/api/class/RecoverableState.md#current_value)
* [**is\_initialized](https://crawlee.dev/python/python/api/class/RecoverableState.md#is_initialized)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L34)\_\_init\_\_

* ****\_\_init\_\_**(\*, default\_state, persist\_state\_key, persistence\_enabled, persist\_state\_kvs\_name, persist\_state\_kvs\_id, persist\_state\_kvs\_factory, logger): None

- Initialize a new recoverable state object.

  ***

  #### Parameters

  * ##### keyword-onlydefault\_state: [TStateModel](https://crawlee.dev/python/python/api.md#TStateModel)

    The default state model instance to use when no persisted state is found. A deep copy is made each time the state is used.

  * ##### keyword-onlypersist\_state\_key: str

    The key under which the state is stored in the KeyValueStore

  * ##### optionalkeyword-onlypersistence\_enabled: Literal\[true, false, explicit\_only] = <!-- -->False

    Flag to enable or disable state persistence. Use 'explicit\_only' if you want to be able to save the state manually, but without any automatic persistence.

  * ##### optionalkeyword-onlypersist\_state\_kvs\_name: str | None = <!-- -->None

    The name of the KeyValueStore to use for persistence. If neither a name nor and id are supplied, the default store will be used.

  * ##### optionalkeyword-onlypersist\_state\_kvs\_id: str | None = <!-- -->None

    The identifier of the KeyValueStore to use for persistence. If neither a name nor and id are supplied, the default store will be used.

  * ##### optionalkeyword-onlypersist\_state\_kvs\_factory: Callable\[\[], Coroutine\[None, None, [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)]] | None = <!-- -->None

    Factory that can be awaited to create KeyValueStore to use for persistence. If not provided, a system-wide KeyValueStore will be used, based on service locator configuration.

  * ##### keyword-onlylogger: logging.Logger

    A logger instance for logging operations related to state persistence

  #### Returns None

### [**](#has_persisted_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L151)has\_persisted\_state

* **async **has\_persisted\_state**(): bool

- Check if there is any persisted state in the key-value store.

  ***

  #### Returns bool

### [**](#initialize)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L93)initialize

* **async **initialize**(): [TStateModel](https://crawlee.dev/python/python/api.md#TStateModel)

- Initialize the recoverable state.

  This method must be called before using the recoverable state. It loads the saved state if persistence is enabled and registers the object to listen for PERSIST\_STATE events.

  ***

  #### Returns [TStateModel](https://crawlee.dev/python/python/api.md#TStateModel)

  The loaded state model

### [**](#persist_state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L175)persist\_state

* **async **persist\_state**(event\_data): None

- Persist the current state to the KeyValueStore.

  This method is typically called in response to a PERSIST\_STATE event, but can also be called directly when needed.

  ***

  #### Parameters

  * ##### optionalevent\_data: [EventPersistStateData](https://crawlee.dev/python/python/api/class/EventPersistStateData.md) | None = <!-- -->None

    Optional data associated with a PERSIST\_STATE event

  #### Returns None

### [**](#reset)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L161)reset

* **async **reset**(): None

- Reset the state to the default values and clear any persisted state.

  Resets the current state to the default state and, if persistence is enabled, clears the persisted state from the KeyValueStore.

  ***

  #### Returns None

### [**](#teardown)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L121)teardown

* **async **teardown**(): None

- Clean up resources used by the recoverable state.

  If persistence is enabled, this method deregisters the object from PERSIST\_STATE events and persists the current state one last time.

  ***

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#current_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L139)current\_value

**current\_value: [TStateModel](https://crawlee.dev/python/python/api.md#TStateModel)

Get the current state.

### [**](#is_initialized)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recoverable_state.py#L147)is\_initialized

**is\_initialized: bool

Check if the state has already been initialized.


---

# RecurringTask<!-- -->

Class for creating and managing recurring tasks.

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/RecurringTask.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/RecurringTask.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RecurringTask.md#__init__)
* [**start](https://crawlee.dev/python/python/api/class/RecurringTask.md#start)
* [**stop](https://crawlee.dev/python/python/api/class/RecurringTask.md#stop)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recurring_task.py#L37)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): Self

- #### Returns Self

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recurring_task.py#L41)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recurring_task.py#L27)\_\_init\_\_

* ****\_\_init\_\_**(func, delay): None

- #### Parameters

  * ##### func: Callable
  * ##### delay: timedelta

  #### Returns None

### [**](#start)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recurring_task.py#L60)start

* ****start**(): None

- Start the recurring task execution.

  ***

  #### Returns None

### [**](#stop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/recurring_task.py#L68)stop

* **async **stop**(): None

- Stop the recurring task execution.

  ***

  #### Returns None


---

# RedisClientMixin<!-- -->

Mixin class for Redis clients.

This mixin provides common Redis operations and basic methods for Redis storage clients.

### Hierarchy

* *RedisClientMixin*

  * [RedisRequestQueueClient](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md)
  * [RedisDatasetClient](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md)
  * [RedisKeyValueStoreClient](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md)

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#__init__)

### Properties

* [**metadata\_key](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#metadata_key)
* [**redis](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#redis)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L49)\_\_init\_\_

* ****\_\_init\_\_**(storage\_name, storage\_id, redis): None

- #### Parameters

  * ##### storage\_name: str
  * ##### storage\_id: str
  * ##### redis: Redis

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#metadata_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L62)metadata\_key

**metadata\_key: str

Return the Redis key for the metadata of this storage.

### [**](#redis)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L57)redis

**redis: Redis

Return the Redis client instance.


---

# RedisDatasetClient<!-- -->

Redis implementation of the dataset client.

This client persists dataset items to Redis using JSON arrays for efficient storage and retrieval. Items are stored as JSON objects with automatic ordering preservation through Redis list operations.

The dataset data is stored in Redis using the following key pattern:

* `datasets:{name}:items` - Redis JSON array containing all dataset items.
* `datasets:{name}:metadata` - Redis JSON object containing dataset metadata.

Items must be JSON-serializable dictionaries. Single items or lists of items can be pushed to the dataset. The item ordering is preserved through Redis JSON array operations. All operations provide atomic consistency through Redis transactions and pipeline operations.

### Hierarchy

* [RedisClientMixin](https://crawlee.dev/python/python/api/class/RedisClientMixin.md)
* [DatasetClient](https://crawlee.dev/python/python/api/class/DatasetClient.md)
  * *RedisDatasetClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#__init__)
* [**drop](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#drop)
* [**get\_data](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#get_data)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#get_metadata)
* [**iterate\_items](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#iterate_items)
* [**open](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#purge)
* [**push\_data](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#push_data)

### Properties

* [**metadata\_key](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#metadata_key)
* [**redis](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md#redis)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L56)\_\_init\_\_

* ****\_\_init\_\_**(storage\_name, storage\_id, redis): None

- Overrides [RedisClientMixin.\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#__init__)

  Initialize a new instance.

  Preferably use the `RedisDatasetClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### storage\_name: str

    Internal storage name used for Redis keys.

  * ##### storage\_id: str

    Unique identifier for the dataset.

  * ##### redis: Redis

    Redis client instance.

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L114)drop

* **async **drop**(): None

- Overrides [DatasetClient.drop](https://crawlee.dev/python/python/api/class/DatasetClient.md#drop)

  Drop the whole dataset and remove all its items.

  The backend method for the `Dataset.drop` call.

  ***

  #### Returns None

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L144)get\_data

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

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L109)get\_metadata

* **async **get\_metadata**(): [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

- Overrides [DatasetClient.get\_metadata](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_metadata)

  Get the metadata of the dataset.

  ***

  #### Returns [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

### [**](#iterate_items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L228)iterate\_items

* **async **iterate\_items**(\*, offset, limit, clean, desc, fields, omit, unwind, skip\_empty, skip\_hidden): AsyncIterator\[dict\[str, Any]]

- Overrides [DatasetClient.iterate\_items](https://crawlee.dev/python/python/api/class/DatasetClient.md#iterate_items)

  Iterate over dataset items one by one.

  This method yields items individually instead of loading all items at once, which is more memory efficient for large datasets.

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

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L74)open

* **async **open**(\*, id, name, alias, redis): [RedisDatasetClient](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md)

- Open or create a new Redis dataset client.

  This method attempts to open an existing dataset from the Redis database. If a dataset with the specified ID or name exists, it loads the metadata from the database. If no existing store is found, a new one is created.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the dataset. If not provided, a random ID will be generated.

  * ##### keyword-onlyname: str | None

    The name of the dataset for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the dataset for unnamed (run scope) storages.

  * ##### keyword-onlyredis: Redis

    Redis client instance.

  #### Returns [RedisDatasetClient](https://crawlee.dev/python/python/api/class/RedisDatasetClient.md)

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L119)purge

* **async **purge**(): None

- Overrides [DatasetClient.purge](https://crawlee.dev/python/python/api/class/DatasetClient.md#purge)

  Purge all items from the dataset.

  The backend method for the `Dataset.purge` call.

  ***

  #### Returns None

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_dataset_client.py#L129)push\_data

* **async **push\_data**(data): None

- Overrides [DatasetClient.push\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#push_data)

  Push data to the dataset.

  The backend method for the `Dataset.push_data` call.

  ***

  #### Parameters

  * ##### data: list\[Any] | dict\[str, Any]

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#metadata_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L62)metadata\_key

**metadata\_key: str

Inherited from [RedisClientMixin.metadata\_key](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#metadata_key)

Return the Redis key for the metadata of this storage.

### [**](#redis)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L57)redis

**redis: Redis

Inherited from [RedisClientMixin.redis](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#redis)

Return the Redis client instance.


---

# RedisKeyValueStoreClient<!-- -->

Redis implementation of the key-value store client.

This client persists key-value data to Redis using hash data structures for efficient storage and retrieval. Keys are mapped to values with automatic content type detection and size tracking for metadata management.

The key-value store data is stored in Redis using the following key pattern:

* `key_value_stores:{name}:items` - Redis hash containing key-value pairs (values stored as binary data).
* `key_value_stores:{name}:metadata_items` - Redis hash containing metadata for each key.
* `key_value_stores:{name}:metadata` - Redis JSON object containing store metadata.

Values are serialized based on their type: JSON objects are stored as UTF-8 encoded JSON strings, text values as UTF-8 encoded strings, and binary data as-is. The implementation automatically handles content type detection and maintains metadata about each record including size and MIME type information.

All operations are atomic through Redis hash operations and pipeline transactions. The client supports concurrent access through Redis's built-in atomic operations for hash fields.

### Hierarchy

* [RedisClientMixin](https://crawlee.dev/python/python/api/class/RedisClientMixin.md)
* [KeyValueStoreClient](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md)
  * *RedisKeyValueStoreClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#__init__)
* [**delete\_value](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#delete_value)
* [**drop](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#drop)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#get_metadata)
* [**get\_public\_url](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#get_public_url)
* [**get\_value](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#get_value)
* [**iterate\_keys](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#iterate_keys)
* [**open](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#purge)
* [**record\_exists](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#record_exists)
* [**set\_value](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#set_value)

### Properties

* [**metadata\_key](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#metadata_key)
* [**redis](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md#redis)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L54)\_\_init\_\_

* ****\_\_init\_\_**(storage\_name, storage\_id, redis): None

- Overrides [RedisClientMixin.\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#__init__)

  Initialize a new instance.

  Preferably use the `RedisKeyValueStoreClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### storage\_name: str
  * ##### storage\_id: str
  * ##### redis: Redis

  #### Returns None

### [**](#delete_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L211)delete\_value

* **async **delete\_value**(\*, key): None

- Overrides [KeyValueStoreClient.delete\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#delete_value)

  Delete a value from the key-value store by its key.

  The backend method for the `KeyValueStore.delete_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L112)drop

* **async **drop**(): None

- Overrides [KeyValueStoreClient.drop](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#drop)

  Drop the whole key-value store and remove all its values.

  The backend method for the `KeyValueStore.drop` call.

  ***

  #### Returns None

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L107)get\_metadata

* **async **get\_metadata**(): [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

- Overrides [KeyValueStoreClient.get\_metadata](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_metadata)

  Get the metadata of the key-value store.

  ***

  #### Returns [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

### [**](#get_public_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L258)get\_public\_url

* **async **get\_public\_url**(\*, key): str

- Overrides [KeyValueStoreClient.get\_public\_url](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_public_url)

  Get the public URL for the given key.

  The backend method for the `KeyValueStore.get_public_url` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns str

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L165)get\_value

* **async **get\_value**(\*, key): [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

- Overrides [KeyValueStoreClient.get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_value)

  Retrieve the given record from the key-value store.

  The backend method for the `KeyValueStore.get_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

### [**](#iterate_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L218)iterate\_keys

* **async **iterate\_keys**(\*, exclusive\_start\_key, limit): AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

- Overrides [KeyValueStoreClient.iterate\_keys](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#iterate_keys)

  Iterate over all the existing keys in the key-value store.

  The backend method for the `KeyValueStore.iterate_keys` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyexclusive\_start\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->None

  #### Returns AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L72)open

* **async **open**(\*, id, name, alias, redis): [RedisKeyValueStoreClient](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md)

- Open or create a new Redis key-value store client.

  This method attempts to open an existing key-value store from the Redis database. If a store with the specified ID or name exists, it loads the metadata from the database. If no existing store is found, a new one is created.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the key-value store. If not provided, a random ID will be generated.

  * ##### keyword-onlyname: str | None

    The name of the key-value store for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the key-value store for unnamed (run scope) storages.

  * ##### keyword-onlyredis: Redis

    Redis client instance.

  #### Returns [RedisKeyValueStoreClient](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md)

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L117)purge

* **async **purge**(): None

- Overrides [KeyValueStoreClient.purge](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#purge)

  Purge all items from the key-value store.

  The backend method for the `KeyValueStore.purge` call.

  ***

  #### Returns None

### [**](#record_exists)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L263)record\_exists

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

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_key_value_store_client.py#L125)set\_value

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

### [**](#metadata_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L62)metadata\_key

**metadata\_key: str

Inherited from [RedisClientMixin.metadata\_key](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#metadata_key)

Return the Redis key for the metadata of this storage.

### [**](#redis)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L57)redis

**redis: Redis

Inherited from [RedisClientMixin.redis](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#redis)

Return the Redis client instance.


---

# RedisRequestQueueClient<!-- -->

Redis implementation of the request queue client.

This client persists requests to Redis using multiple data structures for efficient queue operations, deduplication, and concurrent access safety. Requests are stored with FIFO ordering and support both regular and forefront (high-priority) insertion modes.

The implementation uses Bloom filters for efficient request deduplication and Redis lists for queue operations. Request blocking and client coordination is handled through Redis hashes with timestamp-based expiration for stale request recovery.

The request queue data is stored in Redis using the following key patterns:

* `request_queues:{name}:queue` - Redis list for FIFO request ordering
* `request_queues:{name}:data` - Redis hash storing serialized Request objects by unique\_key
* `request_queues:{name}:in_progress` - Redis hash tracking requests currently being processed
* `request_queues:{name}:added_bloom_filter` - Bloom filter for added request deduplication (`bloom` dedup\_strategy)
* `request_queues:{name}:handled_bloom_filter` - Bloom filter for completed request tracking (`bloom` dedup\_strategy)
* `request_queues:{name}:pending_set` - Redis set for added request deduplication (`default` dedup\_strategy)
* `request_queues:{name}:handled_set` - Redis set for completed request tracking (`default` dedup\_strategy)
* `request_queues:{name}:metadata` - Redis JSON object containing queue metadata

Requests are serialized to JSON for storage and maintain proper FIFO ordering through Redis list operations. The implementation provides concurrent access safety through atomic Lua scripts, Bloom filter operations, and Redis's built-in atomicity guarantees for individual operations.

### Hierarchy

* [RedisClientMixin](https://crawlee.dev/python/python/api/class/RedisClientMixin.md)
* [RequestQueueClient](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)
  * *RedisRequestQueueClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#__init__)
* [**add\_batch\_of\_requests](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#add_batch_of_requests)
* [**drop](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#fetch_next_request)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#get_metadata)
* [**get\_request](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#get_request)
* [**is\_empty](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#is_empty)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#mark_request_as_handled)
* [**open](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#purge)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#reclaim_request)

### Properties

* [**metadata\_key](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#metadata_key)
* [**redis](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md#redis)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L89)\_\_init\_\_

* ****\_\_init\_\_**(storage\_name, storage\_id, redis, dedup\_strategy, bloom\_error\_rate): None

- Overrides [RedisClientMixin.\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#__init__)

  Initialize a new instance.

  Preferably use the `RedisRequestQueueClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### storage\_name: str
  * ##### storage\_id: str
  * ##### redis: Redis
  * ##### optionaldedup\_strategy: Literal\[default, bloom] = <!-- -->'default'
  * ##### optionalbloom\_error\_rate: float = <!-- -->1e-7

  #### Returns None

### [**](#add_batch_of_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L251)add\_batch\_of\_requests

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

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L219)drop

* **async **drop**(): None

- Overrides [RequestQueueClient.drop](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#drop)

  Drop the whole request queue and remove all its values.

  The backend method for the `RequestQueue.drop` call.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L359)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#fetch_next_request)

  Return the next request in the queue to be processed.

  Once you successfully finish processing of the request, you need to call `RequestQueue.mark_request_as_handled` to mark the request as handled in the queue. If there was some error in processing the request, call `RequestQueue.reclaim_request` instead, so that the queue will give the request to some other consumer in another call to the `fetch_next_request` method.

  Note that the `None` return value does not mean the queue processing finished, it means there are currently no pending requests. To check whether all requests in queue were finished, use `RequestQueue.is_finished` instead.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The request or `None` if there are no more pending requests.

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L214)get\_metadata

* **async **get\_metadata**(): [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [RequestQueueClient.get\_metadata](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_metadata)

  Get the metadata of the request queue.

  ***

  #### Returns [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#get_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L388)get\_request

* **async **get\_request**(unique\_key): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.get\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_request)

  Retrieve a request from the queue.

  ***

  #### Parameters

  * ##### unique\_key: str

    Unique key of the request to retrieve.

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The retrieved request, or None, if it did not exist.

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L483)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestQueueClient.is\_empty](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#is_empty)

  Check if the queue is empty.

  ***

  #### Returns bool

  True if the queue is empty, False otherwise.

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L398)mark\_request\_as\_handled

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

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L166)open

* **async **open**(\*, id, name, alias, redis, dedup\_strategy, bloom\_error\_rate): [RedisRequestQueueClient](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md)

- Open or create a new Redis request queue client.

  This method attempts to open an existing request queue from the Redis database. If a queue with the specified ID or name exists, it loads the metadata from the database. If no existing queue is found, a new one is created.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the request queue. If not provided, a random ID will be generated.

  * ##### keyword-onlyname: str | None

    The name of the dataset for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the dataset for unnamed (run scope) storages.

  * ##### keyword-onlyredis: Redis

    Redis client instance.

  * ##### optionalkeyword-onlydedup\_strategy: Literal\[default, bloom] = <!-- -->'default'

    Strategy for request queue deduplication. Options are:

    * 'default': Uses Redis sets for exact deduplication.
    * 'bloom': Uses Redis Bloom filters for probabilistic deduplication with lower memory usage. When using this approach, there is a possibility 1e-7 that requests will be skipped in the queue.

  * ##### optionalkeyword-onlybloom\_error\_rate: float = <!-- -->1e-7

    Desired false positive rate for Bloom filter deduplication. Only relevant if `dedup_strategy` is set to 'bloom'.

  #### Returns [RedisRequestQueueClient](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md)

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L231)purge

* **async **purge**(): None

- Overrides [RequestQueueClient.purge](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#purge)

  Purge all items from the request queue.

  The backend method for the `RequestQueue.purge` call.

  ***

  #### Returns None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_request_queue_client.py#L437)reclaim\_request

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

### [**](#metadata_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L62)metadata\_key

**metadata\_key: str

Inherited from [RedisClientMixin.metadata\_key](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#metadata_key)

Return the Redis key for the metadata of this storage.

### [**](#redis)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_client_mixin.py#L57)redis

**redis: Redis

Inherited from [RedisClientMixin.redis](https://crawlee.dev/python/python/api/class/RedisClientMixin.md#redis)

Return the Redis client instance.


---

# RedisStorageClient<!-- -->

Redis implementation of the storage client.

This storage client provides access to datasets, key-value stores, and request queues that persist data to a Redis database v8.0+. Each storage type uses Redis-specific data structures and key patterns for efficient storage and retrieval.

The client accepts either a Redis connection string or a pre-configured Redis client instance. Exactly one of these parameters must be provided during initialization.

Storage types use the following Redis data structures:

* **Datasets**: Redis JSON arrays for item storage with metadata in JSON objects
* **Key-value stores**: Redis hashes for key-value pairs with separate metadata storage
* **Request queues**: Redis lists for FIFO queuing, hashes for request data and in-progress tracking, and Bloom filters for request deduplication

Warning

This is an experimental feature. The behavior and interface may change in future versions.

### Hierarchy

* [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)
  * *RedisStorageClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RedisStorageClient.md#__init__)
* [**create\_dataset\_client](https://crawlee.dev/python/python/api/class/RedisStorageClient.md#create_dataset_client)
* [**create\_kvs\_client](https://crawlee.dev/python/python/api/class/RedisStorageClient.md#create_kvs_client)
* [**create\_rq\_client](https://crawlee.dev/python/python/api/class/RedisStorageClient.md#create_rq_client)
* [**get\_rate\_limit\_errors](https://crawlee.dev/python/python/api/class/RedisStorageClient.md#get_rate_limit_errors)
* [**get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/RedisStorageClient.md#get_storage_client_cache_key)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_storage_client.py#L39)\_\_init\_\_

* ****\_\_init\_\_**(\*, connection\_string, redis, queue\_dedup\_strategy, queue\_bloom\_error\_rate): None

- Initialize the Redis storage client.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyconnection\_string: str | None = <!-- -->None

    Redis connection string (e.g., "redis\://localhost:6379"). Supports standard Redis URL format with optional database selection.

  * ##### optionalkeyword-onlyredis: Redis | None = <!-- -->None

    Pre-configured Redis client instance.

  * ##### optionalkeyword-onlyqueue\_dedup\_strategy: Literal\[default, bloom] = <!-- -->'default'

    Strategy for request queue deduplication. Options are:

    * 'default': Uses Redis sets for exact deduplication.
    * 'bloom': Uses Redis Bloom filters for probabilistic deduplication with lower memory usage. When using this approach, approximately 1 in 1e-7 requests will be falsely considered duplicate.

  * ##### optionalkeyword-onlyqueue\_bloom\_error\_rate: float = <!-- -->1e-7

    Desired false positive rate for Bloom filter deduplication. Only relevant if `queue_dedup_strategy` is set to 'bloom'.

  #### Returns None

### [**](#create_dataset_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_storage_client.py#L87)create\_dataset\_client

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

### [**](#create_kvs_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_storage_client.py#L108)create\_kvs\_client

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

### [**](#create_rq_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_redis/_storage_client.py#L129)create\_rq\_client

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

### [**](#get_storage_client_cache_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_storage_client.py#L33)get\_storage\_client\_cache\_key

* ****get\_storage\_client\_cache\_key**(configuration): Hashable

- Inherited from [StorageClient.get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/StorageClient.md#get_storage_client_cache_key)

  Return a cache key that can differentiate between different storages of this and other clients.

  Can be based on configuration or on the client itself. By default, returns a module and name of the client class.

  ***

  #### Parameters

  * ##### configuration: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md)

  #### Returns Hashable


---

# RenderingTypePrediction<!-- -->

Rendering type recommendation with detection probability recommendation.

## Index[**](#Index)

### Properties

* [**detection\_probability\_recommendation](https://crawlee.dev/python/python/api/class/RenderingTypePrediction.md#detection_probability_recommendation)
* [**rendering\_type](https://crawlee.dev/python/python/api/class/RenderingTypePrediction.md#rendering_type)

## Properties<!-- -->[**](#Properties)

### [**](#detection_probability_recommendation)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L54)detection\_probability\_recommendation

**detection\_probability\_recommendation: float

Recommended rendering detection probability. Expected values between 0-1.

Zero represents absolute confidence in `rendering_type` recommendation. One represents no confidence in `rendering_type` recommendation.

### [**](#rendering_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L52)rendering\_type

**rendering\_type: [RenderingType](https://crawlee.dev/python/python/api.md#RenderingType)

Recommended rendering type.


---

# RenderingTypePredictor<!-- -->

Stores rendering type for previously crawled URLs and predicts the rendering type for unvisited urls.

### Hierarchy

* *RenderingTypePredictor*
  * [DefaultRenderingTypePredictor](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md)

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#__init__)
* [**clear](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#clear)
* [**initialize](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#initialize)
* [**predict](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#predict)
* [**store\_result](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md#store_result)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L99)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md)

- Initialize the predictor upon entering the context manager.

  ***

  #### Returns [RenderingTypePredictor](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L104)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Clear the predictor upon exiting the context manager.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L65)\_\_init\_\_

* ****\_\_init\_\_**(): None

- Initialize a new instance.

  ***

  #### Returns None

### [**](#clear)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L93)clear

* **async **clear**(): None

- Clear and release additional resources used by the predictor.

  ***

  #### Returns None

### [**](#initialize)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L87)initialize

* **async **initialize**(): None

- Initialize additional resources required for the predictor operation.

  ***

  #### Returns None

### [**](#predict)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L71)predict

* ****predict**(request): [RenderingTypePrediction](https://crawlee.dev/python/python/api/class/RenderingTypePrediction.md)

- Get `RenderingTypePrediction` based on the input request.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    `Request` instance for which the prediction is made.

  #### Returns [RenderingTypePrediction](https://crawlee.dev/python/python/api/class/RenderingTypePrediction.md)

### [**](#store_result)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L79)store\_result

* ****store\_result**(request, rendering\_type): None

- Store prediction results and retrain the model.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    Used request.

  * ##### rendering\_type: [RenderingType](https://crawlee.dev/python/python/api.md#RenderingType)

    Known suitable `RenderingType`.

  #### Returns None


---

# RenderingTypePredictorState<!-- -->

## Index[**](#Index)

### Properties

* [**labels\_coefficients](https://crawlee.dev/python/python/api/class/RenderingTypePredictorState.md#labels_coefficients)
* [**model](https://crawlee.dev/python/python/api/class/RenderingTypePredictorState.md#model)
* [**model\_config](https://crawlee.dev/python/python/api/class/RenderingTypePredictorState.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#labels_coefficients)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L44)labels\_coefficients

**labels\_coefficients: defaultdict\[str, float]

### [**](#model)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L37)model

**model: LogisticRegression

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_adaptive_playwright/_rendering_type_predictor.py#L35)model\_config

**model\_config: Undefined


---

# Request<!-- -->

Represents a request in the Crawlee framework, containing the necessary information for crawling operations.

The `Request` class is one of the core components in Crawlee, utilized by various components such as request providers, HTTP clients, crawlers, and more. It encapsulates the essential data for executing web requests, including the URL, HTTP method, headers, payload, and user data. The user data allows custom information to be stored and persisted throughout the request lifecycle, including its retries.

Key functionalities include managing the request's identifier (`id`), unique key (`unique_key`) that is used for request deduplication, controlling retries, handling state management, and enabling configuration for session rotation and proxy handling.

The recommended way to create a new instance is by using the `Request.from_url` constructor, which automatically generates a unique key and identifier based on the URL and request parameters.

### Usage

```
from crawlee import Request

request = Request.from_url('https://crawlee.dev')
```

### Hierarchy

* *Request*
  * [RequestWithLock](https://crawlee.dev/python/python/api/class/RequestWithLock.md)

## Index[**](#Index)

### Methods

* [**crawl\_depth](https://crawlee.dev/python/python/api/class/Request.md#crawl_depth)
* [**enqueue\_strategy](https://crawlee.dev/python/python/api/class/Request.md#enqueue_strategy)
* [**forefront](https://crawlee.dev/python/python/api/class/Request.md#forefront)
* [**from\_url](https://crawlee.dev/python/python/api/class/Request.md#from_url)
* [**get\_query\_param\_from\_url](https://crawlee.dev/python/python/api/class/Request.md#get_query_param_from_url)
* [**last\_proxy\_tier](https://crawlee.dev/python/python/api/class/Request.md#last_proxy_tier)
* [**session\_rotation\_count](https://crawlee.dev/python/python/api/class/Request.md#session_rotation_count)
* [**state](https://crawlee.dev/python/python/api/class/Request.md#state)

### Properties

* [**crawl\_depth](https://crawlee.dev/python/python/api/class/Request.md#crawl_depth)
* [**crawlee\_data](https://crawlee.dev/python/python/api/class/Request.md#crawlee_data)
* [**enqueue\_strategy](https://crawlee.dev/python/python/api/class/Request.md#enqueue_strategy)
* [**forefront](https://crawlee.dev/python/python/api/class/Request.md#forefront)
* [**handled\_at](https://crawlee.dev/python/python/api/class/Request.md#handled_at)
* [**label](https://crawlee.dev/python/python/api/class/Request.md#label)
* [**last\_proxy\_tier](https://crawlee.dev/python/python/api/class/Request.md#last_proxy_tier)
* [**loaded\_url](https://crawlee.dev/python/python/api/class/Request.md#loaded_url)
* [**max\_retries](https://crawlee.dev/python/python/api/class/Request.md#max_retries)
* [**method](https://crawlee.dev/python/python/api/class/Request.md#method)
* [**model\_config](https://crawlee.dev/python/python/api/class/Request.md#model_config)
* [**no\_retry](https://crawlee.dev/python/python/api/class/Request.md#no_retry)
* [**payload](https://crawlee.dev/python/python/api/class/Request.md#payload)
* [**retry\_count](https://crawlee.dev/python/python/api/class/Request.md#retry_count)
* [**session\_id](https://crawlee.dev/python/python/api/class/Request.md#session_id)
* [**session\_rotation\_count](https://crawlee.dev/python/python/api/class/Request.md#session_rotation_count)
* [**state](https://crawlee.dev/python/python/api/class/Request.md#state)
* [**unique\_key](https://crawlee.dev/python/python/api/class/Request.md#unique_key)
* [**url](https://crawlee.dev/python/python/api/class/Request.md#url)
* [**was\_already\_handled](https://crawlee.dev/python/python/api/class/Request.md#was_already_handled)

## Methods<!-- -->[**](#Methods)

### [**](#crawl_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L374)crawl\_depth

* ****crawl\_depth**(new\_value): None

- #### Parameters

  * ##### new\_value: int

  #### Returns None

### [**](#enqueue_strategy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L406)enqueue\_strategy

* ****enqueue\_strategy**(new\_enqueue\_strategy): None

- #### Parameters

  * ##### new\_enqueue\_strategy: [EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)

  #### Returns None

### [**](#forefront)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L424)forefront

* ****forefront**(new\_value): None

- #### Parameters

  * ##### new\_value: bool

  #### Returns None

### [**](#from_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L243)from\_url

* ****from\_url**(url, \*, method, headers, payload, label, session\_id, unique\_key, keep\_url\_fragment, use\_extended\_unique\_key, always\_enqueue, enqueue\_strategy, max\_retries, kwargs): Self

- Create a new `Request` instance from a URL.

  This is recommended constructor for creating new `Request` instances. It generates a `Request` object from a given URL with additional options to customize HTTP method, payload, unique key, and other request properties. If no `unique_key` or `id` is provided, they are computed automatically based on the URL, method and payload. It depends on the `keep_url_fragment` and `use_extended_unique_key` flags.

  ***

  #### Parameters

  * ##### url: str

    The URL of the request.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method of the request.

  * ##### optionalkeyword-onlyheaders: ([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None = <!-- -->None

    The HTTP headers of the request.

  * ##### optionalkeyword-onlypayload: ([HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | str) | None = <!-- -->None

    The data to be sent as the request body. Typically used with 'POST' or 'PUT' requests.

  * ##### optionalkeyword-onlylabel: str | None = <!-- -->None

    A custom label to differentiate between request types. This is stored in `user_data`, and it is used for request routing (different requests go to different handlers).

  * ##### optionalkeyword-onlysession\_id: str | None = <!-- -->None

    ID of a specific `Session` to which the request will be strictly bound. If the session becomes unavailable when the request is processed, a `RequestCollisionError` will be raised.

  * ##### optionalkeyword-onlyunique\_key: str | None = <!-- -->None

    A unique key identifying the request. If not provided, it is automatically computed based on the URL and other parameters. Requests with the same `unique_key` are treated as identical.

  * ##### optionalkeyword-onlykeep\_url\_fragment: bool = <!-- -->False

    Determines whether the URL fragment (e.g., `` `section` ``) should be included in the `unique_key` computation. This is only relevant when `unique_key` is not provided.

  * ##### optionalkeyword-onlyuse\_extended\_unique\_key: bool = <!-- -->False

    Determines whether to include the HTTP method, ID Session and payload in the `unique_key` computation. This is only relevant when `unique_key` is not provided.

  * ##### optionalkeyword-onlyalways\_enqueue: bool = <!-- -->False

    If set to `True`, the request will be enqueued even if it is already present in the queue. Using this is not allowed when a custom `unique_key` is also provided and will result in a `ValueError`.

  * ##### optionalkeyword-onlyenqueue\_strategy: [EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy) | None = <!-- -->None

    The strategy that will be used for enqueuing the request.

  * ##### optionalkeyword-onlymax\_retries: int | None = <!-- -->None

    Maximum number of retries for this request. Allows to override the global `max_request_retries` option of `BasicCrawler`.

  * ##### kwargs: Any

  #### Returns Self

### [**](#get_query_param_from_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L344)get\_query\_param\_from\_url

* ****get\_query\_param\_from\_url**(param, \*, default): str | None

- Get the value of a specific query parameter from the URL.

  ***

  #### Parameters

  * ##### param: str
  * ##### optionalkeyword-onlydefault: str | None = <!-- -->None

  #### Returns str | None

### [**](#last_proxy_tier)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L415)last\_proxy\_tier

* ****last\_proxy\_tier**(new\_value): None

- #### Parameters

  * ##### new\_value: int

  #### Returns None

### [**](#session_rotation_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L397)session\_rotation\_count

* ****session\_rotation\_count**(new\_session\_rotation\_count): None

- #### Parameters

  * ##### new\_session\_rotation\_count: int

  #### Returns None

### [**](#state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L383)state

* ****state**(new\_state): None

- #### Parameters

  * ##### new\_state: [RequestState](https://crawlee.dev/python/python/api/class/RequestState.md)

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#crawl_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L369)crawl\_depth

**crawl\_depth: int

The depth of the request in the crawl tree.

### [**](#crawlee_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L360)crawlee\_data

**crawlee\_data: [CrawleeRequestData](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md)

Crawlee-specific configuration stored in the `user_data`.

### [**](#enqueue_strategy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L401)enqueue\_strategy

**enqueue\_strategy: [EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)

The strategy that was used for enqueuing the request.

### [**](#forefront)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L419)forefront

**forefront: bool

Indicate whether the request should be enqueued at the front of the queue.

### [**](#handled_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L239)handled\_at

**handled\_at: datetime | None

Timestamp when the request was handled.

### [**](#label)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L350)label

**label: str | None

A string used to differentiate between arbitrary request types.

### [**](#last_proxy_tier)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L410)last\_proxy\_tier

**last\_proxy\_tier: int | None

The last proxy tier used to process the request.

### [**](#loaded_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L236)loaded\_url

**loaded\_url: str | None

URL of the web page that was loaded. This can differ from the original URL in case of redirects.

### [**](#max_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L387)max\_retries

**max\_retries: int | None

Crawlee-specific limit on the number of retries of the request.

### [**](#method)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L187)method

**method: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod)

HTTP request method.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L169)model\_config

**model\_config: Undefined

### [**](#no_retry)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L233)no\_retry

**no\_retry: bool

If set to `True`, the request will not be retried in case of failure.

### [**](#payload)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L190)payload

**payload: [HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | None

HTTP request payload.

### [**](#retry_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L230)retry\_count

**retry\_count: int

Number of times the request has been retried.

### [**](#session_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L355)session\_id

**session\_id: str | None

The ID of the bound session, if there is any.

### [**](#session_rotation_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L392)session\_rotation\_count

**session\_rotation\_count: int | None

Crawlee-specific number of finished session rotations for the request.

### [**](#state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L378)state

**state: [RequestState](https://crawlee.dev/python/python/api/class/RequestState.md)

Crawlee-specific request handling state.

### [**](#unique_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L171)unique\_key

**unique\_key: str

A unique key identifying the request. Two requests with the same `unique_key` are considered as pointing to the same URL.

If `unique_key` is not provided, then it is automatically generated by normalizing the URL. For example, the URL of `HTTP://www.EXAMPLE.com/something/` will produce the `unique_key` of `http://www.example.com/something`.

Pass an arbitrary non-empty text value to the `unique_key` property to override the default behavior and specify which URLs shall be considered equal.

### [**](#url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L183)url

**url: str

The URL of the web page to crawl. Must be a valid HTTP or HTTPS URL, and may include query parameters and fragments.

### [**](#was_already_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L428)was\_already\_handled

**was\_already\_handled: bool

Indicates whether the request was handled.


---

# RequestCollisionError<!-- -->

Raised when a request cannot be processed due to a conflict with required resources.


---

# RequestDb<!-- -->

Requests table for request queues.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *RequestDb*

## Index[**](#Index)

### Properties

* [**\_\_table\_args\_\_](https://crawlee.dev/python/python/api/class/RequestDb.md#__table_args__)
* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/RequestDb.md#__tablename__)
* [**client\_key](https://crawlee.dev/python/python/api/class/RequestDb.md#client_key)
* [**data](https://crawlee.dev/python/python/api/class/RequestDb.md#data)
* [**is\_handled](https://crawlee.dev/python/python/api/class/RequestDb.md#is_handled)
* [**queue](https://crawlee.dev/python/python/api/class/RequestDb.md#queue)
* [**request\_id](https://crawlee.dev/python/python/api/class/RequestDb.md#request_id)
* [**request\_queue\_id](https://crawlee.dev/python/python/api/class/RequestDb.md#request_queue_id)
* [**sequence\_number](https://crawlee.dev/python/python/api/class/RequestDb.md#sequence_number)
* [**storage\_id](https://crawlee.dev/python/python/api/class/RequestDb.md#storage_id)
* [**time\_blocked\_until](https://crawlee.dev/python/python/api/class/RequestDb.md#time_blocked_until)

## Properties<!-- -->[**](#Properties)

### [**](#__table_args__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L206)\_\_table\_args\_\_

**\_\_table\_args\_\_: Undefined

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L205)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#client_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L241)client\_key

**client\_key: Mapped\[str | None]

Identifier of the client that has currently locked this request for processing.

### [**](#data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L229)data

**data: Mapped\[str]

JSON-serialized Request object.

### [**](#is_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L235)is\_handled

**is\_handled: Mapped\[bool]

Processing status flag.

### [**](#queue)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L245)queue

**queue: Mapped\[[RequestQueueMetadataDb](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md)]

### [**](#request_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L221)request\_id

**request\_id: Mapped\[int]

Unique identifier for the request representing the unique\_key.

### [**](#request_queue_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L224)request\_queue\_id

**request\_queue\_id: Mapped\[str]

Foreign key to metadata request queue record.

### [**](#sequence_number)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L232)sequence\_number

**sequence\_number: Mapped\[int]

Ordering sequence: negative for forefront, positive for regular.

### [**](#storage_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L247)storage\_id

**storage\_id: Undefined

Alias for request\_queue\_id to match SqlClientMixin expectations.

### [**](#time_blocked_until)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L238)time\_blocked\_until

**time\_blocked\_until: Mapped\[datetime | None]

Timestamp until which this request is considered blocked for processing by other clients.


---

# RequestHandlerError<!-- -->

Wraps an exception thrown from a request handler (router) and extends it with crawling context.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RequestHandlerError.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/errors.py#L79)\_\_init\_\_

* ****\_\_init\_\_**(wrapped\_exception, crawling\_context): None

- #### Parameters

  * ##### wrapped\_exception: Exception
  * ##### crawling\_context: [TCrawlingContext](https://crawlee.dev/python/python/api.md#TCrawlingContext)

  #### Returns None


---

# RequestHandlerRunResult<!-- -->

Record of calls to storage-related context helpers.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RequestHandlerRunResult.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/RequestHandlerRunResult.md#add_requests)
* [**apply\_request\_changes](https://crawlee.dev/python/python/api/class/RequestHandlerRunResult.md#apply_request_changes)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/RequestHandlerRunResult.md#get_key_value_store)
* [**push\_data](https://crawlee.dev/python/python/api/class/RequestHandlerRunResult.md#push_data)

### Properties

* [**request](https://crawlee.dev/python/python/api/class/RequestHandlerRunResult.md#request)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L267)\_\_init\_\_

* ****\_\_init\_\_**(\*, key\_value\_store\_getter, request): None

- #### Parameters

  * ##### keyword-onlykey\_value\_store\_getter: [GetKeyValueStoreFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFunction.md)
  * ##### keyword-onlyrequest: [Request](https://crawlee.dev/python/python/api/class/Request.md)

  #### Returns None

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L285)add\_requests

* **async **add\_requests**(requests, rq\_id, rq\_name, rq\_alias, \*, limit, base\_url, strategy, include, exclude): None

- Track a call to the `add_requests` context helper.

  ***

  #### Parameters

  * ##### requests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]

  * ##### optionalrq\_id: str | None = <!-- -->None

  * ##### optionalrq\_name: str | None = <!-- -->None

  * ##### optionalrq\_alias: str | None = <!-- -->None

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

  #### Returns None

### [**](#apply_request_changes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L334)apply\_request\_changes

* ****apply\_request\_changes**(target): None

- Apply tracked changes from handler copy to original request.

  ***

  #### Parameters

  * ##### target: [Request](https://crawlee.dev/python/python/api/class/Request.md)

  #### Returns None

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L320)get\_key\_value\_store

* **async **get\_key\_value\_store**(\*, id, name, alias): [KeyValueStoreInterface](https://crawlee.dev/python/python/api/class/KeyValueStoreInterface.md)

- #### Parameters

  * ##### optionalkeyword-onlyid: str | None = <!-- -->None
  * ##### optionalkeyword-onlyname: str | None = <!-- -->None
  * ##### optionalkeyword-onlyalias: str | None = <!-- -->None

  #### Returns [KeyValueStoreInterface](https://crawlee.dev/python/python/api/class/KeyValueStoreInterface.md)

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L301)push\_data

* **async **push\_data**(data, dataset\_id, dataset\_name, dataset\_alias): None

- Track a call to the `push_data` context helper.

  ***

  #### Parameters

  * ##### data: list\[dict\[str, Any]] | dict\[str, Any]
  * ##### optionaldataset\_id: str | None = <!-- -->None
  * ##### optionaldataset\_name: str | None = <!-- -->None
  * ##### optionaldataset\_alias: str | None = <!-- -->None

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L282)request

**request: [Request](https://crawlee.dev/python/python/api/class/Request.md)


---

# RequestList<!-- -->

Represents a (potentially very large) list of URLs to crawl.

### Hierarchy

* [RequestLoader](https://crawlee.dev/python/python/api/class/RequestLoader.md)
  * *RequestList*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RequestList.md#__init__)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestList.md#fetch_next_request)
* [**get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestList.md#get_handled_count)
* [**get\_total\_count](https://crawlee.dev/python/python/api/class/RequestList.md#get_total_count)
* [**is\_empty](https://crawlee.dev/python/python/api/class/RequestList.md#is_empty)
* [**is\_finished](https://crawlee.dev/python/python/api/class/RequestList.md#is_finished)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestList.md#mark_request_as_handled)
* [**to\_tandem](https://crawlee.dev/python/python/api/class/RequestList.md#to_tandem)

### Properties

* [**name](https://crawlee.dev/python/python/api/class/RequestList.md#name)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L35)\_\_init\_\_

* ****\_\_init\_\_**(requests, name, persist\_state\_key, persist\_requests\_key): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalrequests: (Iterable\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)] | AsyncIterable\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]) | None = <!-- -->None

    The request objects (or their string representations) to be added to the provider.

  * ##### optionalname: str | None = <!-- -->None

    A name of the request list.

  * ##### optionalpersist\_state\_key: str | None = <!-- -->None

    A key for persisting the progress information of the RequestList. If you do not pass a key but pass a `name`, a key will be derived using the name. Otherwise, state will not be persisted.

  * ##### optionalpersist\_requests\_key: str | None = <!-- -->None

    A key for persisting the request data loaded from the `requests` iterator. If specified, the request data will be stored in the KeyValueStore to make sure that they don't change over time. This is useful if the `requests` iterator pulls the data dynamically.

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L166)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestLoader.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestLoader.md#fetch_next_request)

  Return the next request to be processed, or `None` if there are no more pending requests.

  The method should return `None` if and only if `is_finished` would return `True`. In other cases, the method should wait until a request appears.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

### [**](#get_handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L148)get\_handled\_count

* **async **get\_handled\_count**(): int

- Overrides [RequestLoader.get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_handled_count)

  Get the number of requests in the loader that have been handled.

  ***

  #### Returns int

### [**](#get_total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L152)get\_total\_count

* **async **get\_total\_count**(): int

- Overrides [RequestLoader.get\_total\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_total_count)

  Get an offline approximation of the total number of requests in the loader (i.e. pending + handled).

  ***

  #### Returns int

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L156)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestLoader.is\_empty](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_empty)

  Return True if there are no more requests in the loader (there might still be unfinished requests).

  ***

  #### Returns bool

### [**](#is_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L161)is\_finished

* **async **is\_finished**(): bool

- Overrides [RequestLoader.is\_finished](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_finished)

  Return True if all requests have been handled.

  ***

  #### Returns bool

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L188)mark\_request\_as\_handled

* **async **mark\_request\_as\_handled**(request): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestLoader.mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestLoader.md#mark_request_as_handled)

  Mark a request as handled after a successful processing (or after giving up retrying).

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

### [**](#to_tandem)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L56)to\_tandem

* **async **to\_tandem**(request\_manager): [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)

- Inherited from [RequestLoader.to\_tandem](https://crawlee.dev/python/python/api/class/RequestLoader.md#to_tandem)

  Combine the loader with a request manager to support adding and reclaiming requests.

  ***

  #### Parameters

  * ##### optionalrequest\_manager: RequestManager | None = <!-- -->None

    Request manager to combine the loader with. If None is given, the default request queue is used.

  #### Returns [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)

## Properties<!-- -->[**](#Properties)

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L144)name

**name: str | None


---

# RequestListData<!-- -->

## Index[**](#Index)

### Properties

* [**requests](https://crawlee.dev/python/python/api/class/RequestListData.md#requests)

## Properties<!-- -->[**](#Properties)

### [**](#requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L28)requests

**requests: list\[[Request](https://crawlee.dev/python/python/api/class/Request.md)]


---

# RequestListState<!-- -->

## Index[**](#Index)

### Properties

* [**in\_progress](https://crawlee.dev/python/python/api/class/RequestListState.md#in_progress)
* [**model\_config](https://crawlee.dev/python/python/api/class/RequestListState.md#model_config)
* [**next\_index](https://crawlee.dev/python/python/api/class/RequestListState.md#next_index)
* [**next\_unique\_key](https://crawlee.dev/python/python/api/class/RequestListState.md#next_unique_key)

## Properties<!-- -->[**](#Properties)

### [**](#in_progress)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L24)in\_progress

**in\_progress: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[str]

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L20)model\_config

**model\_config: Undefined

### [**](#next_index)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L22)next\_index

**next\_index: int

### [**](#next_unique_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_list.py#L23)next\_unique\_key

**next\_unique\_key: str | None


---

# RequestLoader<!-- -->

An abstract class defining the interface for classes that provide access to a read-only stream of requests.

Request loaders are used to manage and provide access to a storage of crawling requests.

Key responsibilities:

* Fetching the next request to be processed.
* Marking requests as successfully handled after processing.
* Managing state information such as the total and handled request counts.

### Hierarchy

* *RequestLoader*

  * [RequestList](https://crawlee.dev/python/python/api/class/RequestList.md)
  * [SitemapRequestLoader](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md)
  * [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

## Index[**](#Index)

### Methods

* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestLoader.md#fetch_next_request)
* [**get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_handled_count)
* [**get\_total\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_total_count)
* [**is\_empty](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_empty)
* [**is\_finished](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_finished)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestLoader.md#mark_request_as_handled)
* [**to\_tandem](https://crawlee.dev/python/python/api/class/RequestLoader.md#to_tandem)

## Methods<!-- -->[**](#Methods)

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L45)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestLoader.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestLoader.md#fetch_next_request)

  Return the next request to be processed, or `None` if there are no more pending requests.

  The method should return `None` if and only if `is_finished` would return `True`. In other cases, the method should wait until a request appears.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

### [**](#get_handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L29)get\_handled\_count

* **async **get\_handled\_count**(): int

- Overrides [RequestLoader.get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_handled_count)

  Get the number of requests in the loader that have been handled.

  ***

  #### Returns int

### [**](#get_total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L33)get\_total\_count

* **async **get\_total\_count**(): int

- Overrides [RequestLoader.get\_total\_count](https://crawlee.dev/python/python/api/class/RequestLoader.md#get_total_count)

  Get an offline approximation of the total number of requests in the loader (i.e. pending + handled).

  ***

  #### Returns int

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L37)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestLoader.is\_empty](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_empty)

  Return True if there are no more requests in the loader (there might still be unfinished requests).

  ***

  #### Returns bool

### [**](#is_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L41)is\_finished

* **async **is\_finished**(): bool

- Overrides [RequestLoader.is\_finished](https://crawlee.dev/python/python/api/class/RequestLoader.md#is_finished)

  Return True if all requests have been handled.

  ***

  #### Returns bool

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L53)mark\_request\_as\_handled

* **async **mark\_request\_as\_handled**(request): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestLoader.mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestLoader.md#mark_request_as_handled)

  Mark a request as handled after a successful processing (or after giving up retrying).

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

### [**](#to_tandem)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L56)to\_tandem

* **async **to\_tandem**(request\_manager): [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)

- Combine the loader with a request manager to support adding and reclaiming requests.

  ***

  #### Parameters

  * ##### optionalrequest\_manager: [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md) | None = <!-- -->None

    Request manager to combine the loader with. If None is given, the default request queue is used.

  #### Returns [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)


---

# RequestManager<!-- -->

Base class that extends `RequestLoader` with the capability to enqueue new requests and reclaim failed ones.

### Hierarchy

* [RequestLoader](https://crawlee.dev/python/python/api/class/RequestLoader.md)

  * *RequestManager*

    * [RequestQueue](https://crawlee.dev/python/python/api/class/RequestQueue.md)
    * [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)

## Index[**](#Index)

### Methods

* [**add\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#add_request)
* [**add\_requests](https://crawlee.dev/python/python/api/class/RequestManager.md#add_requests)
* [**drop](https://crawlee.dev/python/python/api/class/RequestManager.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#fetch_next_request)
* [**get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_handled_count)
* [**get\_total\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_total_count)
* [**is\_empty](https://crawlee.dev/python/python/api/class/RequestManager.md#is_empty)
* [**is\_finished](https://crawlee.dev/python/python/api/class/RequestManager.md#is_finished)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestManager.md#mark_request_as_handled)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#reclaim_request)
* [**to\_tandem](https://crawlee.dev/python/python/api/class/RequestManager.md#to_tandem)

## Methods<!-- -->[**](#Methods)

### [**](#add_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager.py#L26)add\_request

* **async **add\_request**(request, \*, forefront): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestManager.add\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#add_request)

  Add a single request to the manager and store it in underlying resource client.

  ***

  #### Parameters

  * ##### request: str | [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request object (or its string representation) to be added to the manager.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    Determines whether the request should be added to the beginning (if True) or the end (if False) of the manager.

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

  Information about the request addition to the manager or None if the request was not added.

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager.py#L43)add\_requests

* **async **add\_requests**(requests, \*, forefront, batch\_size, wait\_time\_between\_batches, wait\_for\_all\_requests\_to\_be\_added, wait\_for\_all\_requests\_to\_be\_added\_timeout): None

- Overrides [RequestManager.add\_requests](https://crawlee.dev/python/python/api/class/RequestManager.md#add_requests)

  Add requests to the manager in batches.

  ***

  #### Parameters

  * ##### requests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]

    Requests to enqueue.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    If True, add requests to the beginning of the queue.

  * ##### optionalkeyword-onlybatch\_size: int = <!-- -->1000

    The number of requests to add in one batch.

  * ##### optionalkeyword-onlywait\_time\_between\_batches: timedelta = <!-- -->timedelta(seconds=1)

    Time to wait between adding batches.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added: bool = <!-- -->False

    If True, wait for all requests to be added before returning.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added\_timeout: timedelta | None = <!-- -->None

    Timeout for waiting for all requests to be added.

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager.py#L22)drop

* **async **drop**(): None

- Overrides [Storage.drop](https://crawlee.dev/python/python/api/class/Storage.md#drop)

  Remove persistent state either from the Apify Cloud storage or from the local database.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L45)fetch\_next\_request

* **async **fetch\_next\_request**(): Request | None

- Overrides [RequestManager.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#fetch_next_request)

  Return the next request to be processed, or `None` if there are no more pending requests.

  The method should return `None` if and only if `is_finished` would return `True`. In other cases, the method should wait until a request appears.

  ***

  #### Returns Request | None

### [**](#get_handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L29)get\_handled\_count

* **async **get\_handled\_count**(): int

- Overrides [RequestManager.get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_handled_count)

  Get the number of requests in the loader that have been handled.

  ***

  #### Returns int

### [**](#get_total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L33)get\_total\_count

* **async **get\_total\_count**(): int

- Overrides [RequestManager.get\_total\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_total_count)

  Get an offline approximation of the total number of requests in the loader (i.e. pending + handled).

  ***

  #### Returns int

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L37)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestManager.is\_empty](https://crawlee.dev/python/python/api/class/RequestManager.md#is_empty)

  Return True if there are no more requests in the loader (there might still be unfinished requests).

  ***

  #### Returns bool

### [**](#is_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L41)is\_finished

* **async **is\_finished**(): bool

- Overrides [RequestManager.is\_finished](https://crawlee.dev/python/python/api/class/RequestManager.md#is_finished)

  Return True if all requests have been handled.

  ***

  #### Returns bool

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L53)mark\_request\_as\_handled

* **async **mark\_request\_as\_handled**(request): ProcessedRequest | None

- Overrides [RequestManager.mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestManager.md#mark_request_as_handled)

  Mark a request as handled after a successful processing (or after giving up retrying).

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

  #### Returns ProcessedRequest | None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager.py#L71)reclaim\_request

* **async **reclaim\_request**(request, \*, forefront): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestManager.reclaim\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#reclaim_request)

  Reclaims a failed request back to the source, so that it can be returned for processing later again.

  It is possible to modify the request data by supplying an updated request as a parameter.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)
  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

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

# RequestManagerTandem<!-- -->

Implements a tandem behaviour for a pair of `RequestLoader` and `RequestManager`.

In this scenario, the contents of the "loader" get transferred into the "manager", allowing processing the requests from both sources and also enqueueing new requests (not possible with plain `RequestManager`).

### Hierarchy

* [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)
  * *RequestManagerTandem*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#__init__)
* [**add\_request](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#add_request)
* [**add\_requests](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#add_requests)
* [**drop](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#fetch_next_request)
* [**get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#get_handled_count)
* [**get\_total\_count](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#get_total_count)
* [**is\_empty](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#is_empty)
* [**is\_finished](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#is_finished)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#mark_request_as_handled)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#reclaim_request)
* [**to\_tandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md#to_tandem)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L31)\_\_init\_\_

* ****\_\_init\_\_**(request\_loader, request\_manager): None

- #### Parameters

  * ##### request\_loader: [RequestLoader](https://crawlee.dev/python/python/api/class/RequestLoader.md)
  * ##### request\_manager: [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)

  #### Returns None

### [**](#add_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L52)add\_request

* **async **add\_request**(request, \*, forefront): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestManager.add\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#add_request)

  Add a single request to the manager and store it in underlying resource client.

  ***

  #### Parameters

  * ##### request: str | [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request object (or its string representation) to be added to the manager.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    Determines whether the request should be added to the beginning (if True) or the end (if False) of the manager.

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

  Information about the request addition to the manager or None if the request was not added.

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L56)add\_requests

* **async **add\_requests**(requests, \*, forefront, batch\_size, wait\_time\_between\_batches, wait\_for\_all\_requests\_to\_be\_added, wait\_for\_all\_requests\_to\_be\_added\_timeout): None

- Overrides [RequestManager.add\_requests](https://crawlee.dev/python/python/api/class/RequestManager.md#add_requests)

  Add requests to the manager in batches.

  ***

  #### Parameters

  * ##### requests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]

    Requests to enqueue.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    If True, add requests to the beginning of the queue.

  * ##### optionalkeyword-onlybatch\_size: int = <!-- -->1000

    The number of requests to add in one batch.

  * ##### optionalkeyword-onlywait\_time\_between\_batches: timedelta = <!-- -->timedelta(seconds=1)

    Time to wait between adding batches.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added: bool = <!-- -->False

    If True, wait for all requests to be added before returning.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added\_timeout: timedelta | None = <!-- -->None

    Timeout for waiting for all requests to be added.

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L110)drop

* **async **drop**(): None

- Overrides [Storage.drop](https://crawlee.dev/python/python/api/class/Storage.md#drop)

  Remove persistent state either from the Apify Cloud storage or from the local database.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L76)fetch\_next\_request

* **async **fetch\_next\_request**(): Request | None

- Overrides [RequestManager.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#fetch_next_request)

  Return the next request to be processed, or `None` if there are no more pending requests.

  The method should return `None` if and only if `is_finished` would return `True`. In other cases, the method should wait until a request appears.

  ***

  #### Returns Request | None

### [**](#get_handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L36)get\_handled\_count

* **async **get\_handled\_count**(): int

- Overrides [RequestManager.get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_handled_count)

  Get the number of requests in the loader that have been handled.

  ***

  #### Returns int

### [**](#get_total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L40)get\_total\_count

* **async **get\_total\_count**(): int

- Overrides [RequestManager.get\_total\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_total_count)

  Get an offline approximation of the total number of requests in the loader (i.e. pending + handled).

  ***

  #### Returns int

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L44)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestManager.is\_empty](https://crawlee.dev/python/python/api/class/RequestManager.md#is_empty)

  Return True if there are no more requests in the loader (there might still be unfinished requests).

  ***

  #### Returns bool

### [**](#is_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L48)is\_finished

* **async **is\_finished**(): bool

- Overrides [RequestManager.is\_finished](https://crawlee.dev/python/python/api/class/RequestManager.md#is_finished)

  Return True if all requests have been handled.

  ***

  #### Returns bool

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L106)mark\_request\_as\_handled

* **async **mark\_request\_as\_handled**(request): ProcessedRequest | None

- Overrides [RequestManager.mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestManager.md#mark_request_as_handled)

  Mark a request as handled after a successful processing (or after giving up retrying).

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

  #### Returns ProcessedRequest | None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_manager_tandem.py#L102)reclaim\_request

* **async **reclaim\_request**(request, \*, forefront): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestManager.reclaim\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#reclaim_request)

  Reclaims a failed request back to the source, so that it can be returned for processing later again.

  It is possible to modify the request data by supplying an updated request as a parameter.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)
  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

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

# RequestOptions<!-- -->

Options that can be used to customize request creation.

This type exactly matches the parameters of `Request.from_url` method.

## Index[**](#Index)

### Properties

* [**always\_enqueue](https://crawlee.dev/python/python/api/class/RequestOptions.md#always_enqueue)
* [**enqueue\_strategy](https://crawlee.dev/python/python/api/class/RequestOptions.md#enqueue_strategy)
* [**headers](https://crawlee.dev/python/python/api/class/RequestOptions.md#headers)
* [**id](https://crawlee.dev/python/python/api/class/RequestOptions.md#id)
* [**keep\_url\_fragment](https://crawlee.dev/python/python/api/class/RequestOptions.md#keep_url_fragment)
* [**label](https://crawlee.dev/python/python/api/class/RequestOptions.md#label)
* [**max\_retries](https://crawlee.dev/python/python/api/class/RequestOptions.md#max_retries)
* [**method](https://crawlee.dev/python/python/api/class/RequestOptions.md#method)
* [**no\_retry](https://crawlee.dev/python/python/api/class/RequestOptions.md#no_retry)
* [**payload](https://crawlee.dev/python/python/api/class/RequestOptions.md#payload)
* [**session\_id](https://crawlee.dev/python/python/api/class/RequestOptions.md#session_id)
* [**unique\_key](https://crawlee.dev/python/python/api/class/RequestOptions.md#unique_key)
* [**url](https://crawlee.dev/python/python/api/class/RequestOptions.md#url)
* [**use\_extended\_unique\_key](https://crawlee.dev/python/python/api/class/RequestOptions.md#use_extended_unique_key)
* [**user\_data](https://crawlee.dev/python/python/api/class/RequestOptions.md#user_data)

## Properties<!-- -->[**](#Properties)

### [**](#always_enqueue)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L137)always\_enqueue

**always\_enqueue: NotRequired\[bool]

### [**](#enqueue_strategy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L140)enqueue\_strategy

**enqueue\_strategy: NotRequired\[[EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)]

### [**](#headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L129)headers

**headers: NotRequired\[([HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md) | dict\[str, str]) | None]

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L134)id

**id: NotRequired\[str | None]

### [**](#keep_url_fragment)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L135)keep\_url\_fragment

**keep\_url\_fragment: NotRequired\[bool]

### [**](#label)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L131)label

**label: NotRequired\[str | None]

### [**](#max_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L141)max\_retries

**max\_retries: NotRequired\[int | None]

### [**](#method)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L128)method

**method: NotRequired\[[HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod)]

### [**](#no_retry)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L139)no\_retry

**no\_retry: NotRequired\[bool]

### [**](#payload)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L130)payload

**payload: NotRequired\[([HttpPayload](https://crawlee.dev/python/python/api.md#HttpPayload) | str) | None]

### [**](#session_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L132)session\_id

**session\_id: NotRequired\[str | None]

### [**](#unique_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L133)unique\_key

**unique\_key: NotRequired\[str | None]

### [**](#url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L127)url

**url: Required\[str]

### [**](#use_extended_unique_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L136)use\_extended\_unique\_key

**use\_extended\_unique\_key: NotRequired\[bool]

### [**](#user_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L138)user\_data

**user\_data: NotRequired\[dict\[str, JsonSerializable]]


---

# RequestProcessingRecord<!-- -->

Tracks information about the processing of a request.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RequestProcessingRecord.md#__init__)
* [**finish](https://crawlee.dev/python/python/api/class/RequestProcessingRecord.md#finish)
* [**run](https://crawlee.dev/python/python/api/class/RequestProcessingRecord.md#run)

### Properties

* [**retry\_count](https://crawlee.dev/python/python/api/class/RequestProcessingRecord.md#retry_count)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L34)\_\_init\_\_

* ****\_\_init\_\_**(): None

- #### Returns None

### [**](#finish)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L45)finish

* ****finish**(): timedelta

- Mark the job as finished.

  ***

  #### Returns timedelta

### [**](#run)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L39)run

* ****run**(): int

- Mark the job as started.

  ***

  #### Returns int

## Properties<!-- -->[**](#Properties)

### [**](#retry_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/statistics/_statistics.py#L54)retry\_count

**retry\_count: int

Number of times the job has been retried.


---

# RequestQueue<!-- -->

Request queue is a storage for managing HTTP requests.

The request queue class serves as a high-level interface for organizing and managing HTTP requests during web crawling. It provides methods for adding, retrieving, and manipulating requests throughout the crawling lifecycle, abstracting away the underlying storage implementation details.

Request queue maintains the state of each URL to be crawled, tracking whether it has been processed, is currently being handled, or is waiting in the queue. Each URL in the queue is uniquely identified by a `unique_key` property, which prevents duplicate processing unless explicitly configured otherwise.

The class supports both breadth-first and depth-first crawling strategies through its `forefront` parameter when adding requests. It also provides mechanisms for error handling and request reclamation when processing fails.

You can open a request queue using the `open` class method, specifying either a name or ID to identify the queue. The underlying storage implementation is determined by the configured storage client.

### Usage

```
from crawlee.storages import RequestQueue

# Open a request queue
rq = await RequestQueue.open(name='my-queue')

# Add a request
await rq.add_request('https://example.com')

# Process requests
request = await rq.fetch_next_request()
if request:
    try:
        # Process the request
        # ...
        await rq.mark_request_as_handled(request)
    except Exception:
        await rq.reclaim_request(request)
```

### Hierarchy

* [RequestManager](https://crawlee.dev/python/python/api/class/RequestManager.md)
* [Storage](https://crawlee.dev/python/python/api/class/Storage.md)
  * *RequestQueue*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RequestQueue.md#__init__)
* [**add\_request](https://crawlee.dev/python/python/api/class/RequestQueue.md#add_request)
* [**add\_requests](https://crawlee.dev/python/python/api/class/RequestQueue.md#add_requests)
* [**drop](https://crawlee.dev/python/python/api/class/RequestQueue.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestQueue.md#fetch_next_request)
* [**get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestQueue.md#get_handled_count)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/RequestQueue.md#get_metadata)
* [**get\_request](https://crawlee.dev/python/python/api/class/RequestQueue.md#get_request)
* [**get\_total\_count](https://crawlee.dev/python/python/api/class/RequestQueue.md#get_total_count)
* [**is\_empty](https://crawlee.dev/python/python/api/class/RequestQueue.md#is_empty)
* [**is\_finished](https://crawlee.dev/python/python/api/class/RequestQueue.md#is_finished)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestQueue.md#mark_request_as_handled)
* [**open](https://crawlee.dev/python/python/api/class/RequestQueue.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/RequestQueue.md#purge)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/RequestQueue.md#reclaim_request)
* [**to\_tandem](https://crawlee.dev/python/python/api/class/RequestQueue.md#to_tandem)

### Properties

* [**id](https://crawlee.dev/python/python/api/class/RequestQueue.md#id)
* [**name](https://crawlee.dev/python/python/api/class/RequestQueue.md#name)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L74)\_\_init\_\_

* ****\_\_init\_\_**(client, id, name): None

- Initialize a new instance.

  Preferably use the `RequestQueue.open` constructor to create a new instance.

  ***

  #### Parameters

  * ##### client: [RequestQueueClient](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)

    An instance of a storage client.

  * ##### id: str

    The unique identifier of the storage.

  * ##### name: str | None

    The name of the storage, if available.

  #### Returns None

### [**](#add_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L156)add\_request

* **async **add\_request**(request, \*, forefront): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestManager.add\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#add_request)

  Add a single request to the manager and store it in underlying resource client.

  ***

  #### Parameters

  * ##### request: str | [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request object (or its string representation) to be added to the manager.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    Determines whether the request should be added to the beginning (if True) or the end (if False) of the manager.

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

  Information about the request addition to the manager or None if the request was not added.

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L180)add\_requests

* **async **add\_requests**(requests, \*, forefront, batch\_size, wait\_time\_between\_batches, wait\_for\_all\_requests\_to\_be\_added, wait\_for\_all\_requests\_to\_be\_added\_timeout): None

- Overrides [RequestManager.add\_requests](https://crawlee.dev/python/python/api/class/RequestManager.md#add_requests)

  Add requests to the manager in batches.

  ***

  #### Parameters

  * ##### requests: Sequence\[str | [Request](https://crawlee.dev/python/python/api/class/Request.md)]

    Requests to enqueue.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    If True, add requests to the beginning of the queue.

  * ##### optionalkeyword-onlybatch\_size: int = <!-- -->1000

    The number of requests to add in one batch.

  * ##### optionalkeyword-onlywait\_time\_between\_batches: timedelta = <!-- -->timedelta(seconds=1)

    Time to wait between adding batches.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added: bool = <!-- -->False

    If True, wait for all requests to be added before returning.

  * ##### optionalkeyword-onlywait\_for\_all\_requests\_to\_be\_added\_timeout: timedelta | None = <!-- -->None

    Timeout for waiting for all requests to be added.

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L144)drop

* **async **drop**(): None

- Overrides [Storage.drop](https://crawlee.dev/python/python/api/class/Storage.md#drop)

  Remove persistent state either from the Apify Cloud storage or from the local database.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L230)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestManager.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#fetch_next_request)

  Return the next request in the queue to be processed.

  Once you successfully finish processing of the request, you need to call `RequestQueue.mark_request_as_handled` to mark the request as handled in the queue. If there was some error in processing the request, call `RequestQueue.reclaim_request` instead, so that the queue will give the request to some other consumer in another call to the `fetch_next_request` method.

  Note that the `None` return value does not mean the queue processing finished, it means there are currently no pending requests. To check whether all requests in queue were finished, use `RequestQueue.is_finished` instead.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The next request to process, or `None` if there are no more pending requests.

### [**](#get_handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L108)get\_handled\_count

* **async **get\_handled\_count**(): int

- Overrides [RequestManager.get\_handled\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_handled_count)

  Get the number of requests in the loader that have been handled.

  ***

  #### Returns int

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L104)get\_metadata

* **async **get\_metadata**(): ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [Storage.get\_metadata](https://crawlee.dev/python/python/api/class/Storage.md#get_metadata)

  Get the storage metadata.

  ***

  #### Returns ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#get_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L247)get\_request

* **async **get\_request**(unique\_key): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Retrieve a specific request from the queue by its ID.

  ***

  #### Parameters

  * ##### unique\_key: str

    Unique key of the request to retrieve.

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The request with the specified ID, or `None` if no such request exists.

### [**](#get_total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L113)get\_total\_count

* **async **get\_total\_count**(): int

- Overrides [RequestManager.get\_total\_count](https://crawlee.dev/python/python/api/class/RequestManager.md#get_total_count)

  Get an offline approximation of the total number of requests in the loader (i.e. pending + handled).

  ***

  #### Returns int

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L295)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestManager.is\_empty](https://crawlee.dev/python/python/api/class/RequestManager.md#is_empty)

  Check if the request queue is empty.

  An empty queue means that there are no requests currently in the queue, either pending or being processed. However, this does not necessarily mean that the crawling operation is finished, as there still might be tasks that could add additional requests to the queue.

  ***

  #### Returns bool

  True if the request queue is empty, False otherwise.

### [**](#is_finished)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L307)is\_finished

* **async **is\_finished**(): bool

- Overrides [RequestManager.is\_finished](https://crawlee.dev/python/python/api/class/RequestManager.md#is_finished)

  Check if the request queue is finished.

  A finished queue means that all requests in the queue have been processed (the queue is empty) and there are no more tasks that could add additional requests to the queue. This is the definitive way to check if a crawling operation is complete.

  ***

  #### Returns bool

  True if the request queue is finished (empty and no pending add operations), False otherwise.

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L258)mark\_request\_as\_handled

* **async **mark\_request\_as\_handled**(request): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestManager.mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestManager.md#mark_request_as_handled)

  Mark a request as handled after successful processing.

  This method should be called after a request has been successfully processed. Once marked as handled, the request will be removed from the queue and will not be returned in subsequent calls to `fetch_next_request` method.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to mark as handled.

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

  Information about the queue operation.

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L119)open

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

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L152)purge

* **async **purge**(): None

- Overrides [Storage.purge](https://crawlee.dev/python/python/api/class/Storage.md#purge)

  Purge the storage, removing all items from the underlying storage client.

  This method does not remove the storage itself, e.g. don't remove the metadata, but clears all items within it.

  ***

  #### Returns None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L273)reclaim\_request

* **async **reclaim\_request**(request, \*, forefront): [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

- Overrides [RequestManager.reclaim\_request](https://crawlee.dev/python/python/api/class/RequestManager.md#reclaim_request)

  Reclaim a failed request back to the queue for later processing.

  If a request fails during processing, this method can be used to return it to the queue. The request will be returned for processing again in a subsequent call to `RequestQueue.fetch_next_request`.

  ***

  #### Parameters

  * ##### request: [Request](https://crawlee.dev/python/python/api/class/Request.md)

    The request to return to the queue.

  * ##### optionalkeyword-onlyforefront: bool = <!-- -->False

    If true, the request will be added to the beginning of the queue. Otherwise, it will be added to the end.

  #### Returns [ProcessedRequest](https://crawlee.dev/python/python/api/class/ProcessedRequest.md) | None

  Information about the queue operation.

### [**](#to_tandem)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/request_loaders/_request_loader.py#L56)to\_tandem

* **async **to\_tandem**(request\_manager): [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)

- Inherited from [RequestLoader.to\_tandem](https://crawlee.dev/python/python/api/class/RequestLoader.md#to_tandem)

  Combine the loader with a request manager to support adding and reclaiming requests.

  ***

  #### Parameters

  * ##### optionalrequest\_manager: RequestManager | None = <!-- -->None

    Request manager to combine the loader with. If None is given, the default request queue is used.

  #### Returns [RequestManagerTandem](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md)

## Properties<!-- -->[**](#Properties)

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L95)id

**id: str

Overrides [Storage.id](https://crawlee.dev/python/python/api/class/Storage.md#id)

Get the storage ID.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_request_queue.py#L100)name

**name: str | None

Overrides [Storage.name](https://crawlee.dev/python/python/api/class/Storage.md#name)

Get the storage name.


---

# RequestQueueClient<!-- -->

An abstract class for request queue resource clients.

These clients are specific to the type of resource they manage and operate under a designated storage client, like a memory storage client.

### Hierarchy

* *RequestQueueClient*

  * [MemoryRequestQueueClient](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md)
  * [FileSystemRequestQueueClient](https://crawlee.dev/python/python/api/class/FileSystemRequestQueueClient.md)
  * [SqlRequestQueueClient](https://crawlee.dev/python/python/api/class/SqlRequestQueueClient.md)
  * [RedisRequestQueueClient](https://crawlee.dev/python/python/api/class/RedisRequestQueueClient.md)

## Index[**](#Index)

### Methods

* [**add\_batch\_of\_requests](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#add_batch_of_requests)
* [**drop](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#fetch_next_request)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_metadata)
* [**get\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_request)
* [**is\_empty](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#is_empty)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#mark_request_as_handled)
* [**purge](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#purge)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#reclaim_request)

## Methods<!-- -->[**](#Methods)

### [**](#add_batch_of_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L39)add\_batch\_of\_requests

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

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L25)drop

* **async **drop**(): None

- Overrides [RequestQueueClient.drop](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#drop)

  Drop the whole request queue and remove all its values.

  The backend method for the `RequestQueue.drop` call.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L77)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#fetch_next_request)

  Return the next request in the queue to be processed.

  Once you successfully finish processing of the request, you need to call `RequestQueue.mark_request_as_handled` to mark the request as handled in the queue. If there was some error in processing the request, call `RequestQueue.reclaim_request` instead, so that the queue will give the request to some other consumer in another call to the `fetch_next_request` method.

  Note that the `None` return value does not mean the queue processing finished, it means there are currently no pending requests. To check whether all requests in queue were finished, use `RequestQueue.is_finished` instead.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The request or `None` if there are no more pending requests.

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L21)get\_metadata

* **async **get\_metadata**(): [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [RequestQueueClient.get\_metadata](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_metadata)

  Get the metadata of the request queue.

  ***

  #### Returns [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#get_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L66)get\_request

* **async **get\_request**(unique\_key): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.get\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_request)

  Retrieve a request from the queue.

  ***

  #### Parameters

  * ##### unique\_key: str

    Unique key of the request to retrieve.

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The retrieved request, or None, if it did not exist.

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L126)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestQueueClient.is\_empty](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#is_empty)

  Check if the request queue is empty.

  ***

  #### Returns bool

  True if the request queue is empty, False otherwise.

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L94)mark\_request\_as\_handled

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

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L32)purge

* **async **purge**(): None

- Overrides [RequestQueueClient.purge](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#purge)

  Purge all items from the request queue.

  The backend method for the `RequestQueue.purge` call.

  ***

  #### Returns None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_request_queue_client.py#L107)reclaim\_request

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

# RequestQueueMetadata<!-- -->

Model for a request queue metadata.

### Hierarchy

* [StorageMetadata](https://crawlee.dev/python/python/api/class/StorageMetadata.md)
  * *RequestQueueMetadata*

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#accessed_at)
* [**created\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#created_at)
* [**had\_multiple\_clients](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#had_multiple_clients)
* [**handled\_request\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#handled_request_count)
* [**id](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#id)
* [**model\_config](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#model_config)
* [**modified\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#name)
* [**pending\_request\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#pending_request_count)
* [**total\_request\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md#total_request_count)

## Properties<!-- -->[**](#Properties)

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L31)accessed\_at

**accessed\_at: Annotated\[datetime, Field(alias='accessedAt')]

Inherited from [StorageMetadata.accessed\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#accessed_at)

The timestamp when the storage was last accessed.

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L34)created\_at

**created\_at: Annotated\[datetime, Field(alias='createdAt')]

Inherited from [StorageMetadata.created\_at](https://crawlee.dev/python/python/api/class/StorageMetadata.md#created_at)

The timestamp when the storage was created.

### [**](#had_multiple_clients)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L64)had\_multiple\_clients

**had\_multiple\_clients: bool

Indicates whether the queue has been accessed by multiple clients (consumers).

### [**](#handled_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L67)handled\_request\_count

**handled\_request\_count: int

The number of requests that have been handled from the queue.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L25)id

**id: Annotated\[str, Field(alias='id')]

Inherited from [StorageMetadata.id](https://crawlee.dev/python/python/api/class/StorageMetadata.md#id)

The unique identifier of the storage.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L62)model\_config

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

### [**](#pending_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L70)pending\_request\_count

**pending\_request\_count: int

The number of requests that are still pending in the queue.

### [**](#total_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L73)total\_request\_count

**total\_request\_count: int

The total number of requests that have been added to the queue.


---

# RequestQueueMetadataBufferDb<!-- -->

Buffer table for deferred request queue metadata updates to reduce concurrent access issues.

### Hierarchy

* [MetadataBufferDb](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md)
* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *RequestQueueMetadataBufferDb*

## Index[**](#Index)

### Properties

* [**\_\_table\_args\_\_](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#__table_args__)
* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#__tablename__)
* [**accessed\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#accessed_at)
* [**client\_id](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#client_id)
* [**delta\_handled\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#delta_handled_count)
* [**delta\_pending\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#delta_pending_count)
* [**delta\_total\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#delta_total_count)
* [**id](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#id)
* [**modified\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#modified_at)
* [**need\_recalc](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#need_recalc)
* [**request\_queue\_id](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#request_queue_id)
* [**storage\_id](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md#storage_id)

## Properties<!-- -->[**](#Properties)

### [**](#__table_args__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L328)\_\_table\_args\_\_

**\_\_table\_args\_\_: Undefined

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L326)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L286)accessed\_at

**accessed\_at: Mapped\[datetime]

Inherited from [MetadataBufferDb.accessed\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#accessed_at)

New accessed\_at timestamp, if being updated.

### [**](#client_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L334)client\_id

**client\_id: Mapped\[str]

Identifier of the client making this update.

### [**](#delta_handled_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L338)delta\_handled\_count

**delta\_handled\_count: Mapped\[int | None]

Delta for handled\_request\_count.

### [**](#delta_pending_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L341)delta\_pending\_count

**delta\_pending\_count: Mapped\[int | None]

Delta for pending\_request\_count.

### [**](#delta_total_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L344)delta\_total\_count

**delta\_total\_count: Mapped\[int | None]

Delta for total\_request\_count.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L282)id

**id: Mapped\[int]

Inherited from [MetadataBufferDb.id](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#id)

Auto-increment primary key for ordering.

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L289)modified\_at

**modified\_at: Mapped\[datetime | None]

Inherited from [MetadataBufferDb.modified\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#modified_at)

New modified\_at timestamp, if being updated.

### [**](#need_recalc)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L347)need\_recalc

**need\_recalc: Mapped\[bool]

Flag indicating that counters need recalculation from actual data.

### [**](#request_queue_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L331)request\_queue\_id

**request\_queue\_id: Mapped\[str]

ID of the request queue being updated.

### [**](#storage_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L350)storage\_id

**storage\_id: Undefined

Alias for request\_queue\_id to match SqlClientMixin expectations.


---

# RequestQueueMetadataDb<!-- -->

Metadata table for request queues.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
* [StorageMetadataDb](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md)
  * *RequestQueueMetadataDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#__tablename__)
* [**accessed\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#accessed_at)
* [**buffer\_locked\_until](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#buffer_locked_until)
* [**created\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#created_at)
* [**had\_multiple\_clients](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#had_multiple_clients)
* [**handled\_request\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#handled_request_count)
* [**id](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#id)
* [**internal\_name](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#internal_name)
* [**modified\_at](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#name)
* [**pending\_request\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#pending_request_count)
* [**request\_queue\_id](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#request_queue_id)
* [**requests](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#requests)
* [**state](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#state)
* [**total\_request\_count](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md#total_request_count)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L97)\_\_tablename\_\_

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

### [**](#had_multiple_clients)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L102)had\_multiple\_clients

**had\_multiple\_clients: Mapped\[bool]

Flag indicating if multiple clients have accessed this queue.

### [**](#handled_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L105)handled\_request\_count

**handled\_request\_count: Mapped\[int]

Number of requests processed.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L123)id

**id: Undefined

Alias for request\_queue\_id to match Pydantic expectations.

### [**](#internal_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L55)internal\_name

**internal\_name: Mapped\[str]

Inherited from [StorageMetadataDb.internal\_name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#internal_name)

Internal unique name for a storage instance based on a name or alias.

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L67)modified\_at

**modified\_at: Mapped\[datetime]

Inherited from [StorageMetadataDb.modified\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#modified_at)

Last modification datetime.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L58)name

**name: Mapped\[str | None]

Inherited from [StorageMetadataDb.name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#name)

Human-readable name. None becomes 'default' in database to enforce uniqueness.

### [**](#pending_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L108)pending\_request\_count

**pending\_request\_count: Mapped\[int]

Number of requests waiting to be processed.

### [**](#request_queue_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L99)request\_queue\_id

**request\_queue\_id: Mapped\[str]

Unique identifier for the request queue.

### [**](#requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L115)requests

**requests: Mapped\[list\[[RequestDb](https://crawlee.dev/python/python/api/class/RequestDb.md)]]

### [**](#state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L119)state

**state: Mapped\[[RequestQueueStateDb](https://crawlee.dev/python/python/api/class/RequestQueueStateDb.md)]

### [**](#total_request_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L111)total\_request\_count

**total\_request\_count: Mapped\[int]

Total number of requests ever added to this queue.


---

# RequestQueueState<!-- -->

State model for the `FileSystemRequestQueueClient`.

## Index[**](#Index)

### Properties

* [**forefront\_requests](https://crawlee.dev/python/python/api/class/RequestQueueState.md#forefront_requests)
* [**forefront\_sequence\_counter](https://crawlee.dev/python/python/api/class/RequestQueueState.md#forefront_sequence_counter)
* [**handled\_requests](https://crawlee.dev/python/python/api/class/RequestQueueState.md#handled_requests)
* [**in\_progress\_requests](https://crawlee.dev/python/python/api/class/RequestQueueState.md#in_progress_requests)
* [**regular\_requests](https://crawlee.dev/python/python/api/class/RequestQueueState.md#regular_requests)
* [**sequence\_counter](https://crawlee.dev/python/python/api/class/RequestQueueState.md#sequence_counter)

## Properties<!-- -->[**](#Properties)

### [**](#forefront_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L49)forefront\_requests

**forefront\_requests: dict\[str, int]

Mapping of forefront request unique keys to their sequence numbers.

### [**](#forefront_sequence_counter)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L46)forefront\_sequence\_counter

**forefront\_sequence\_counter: int

Counter for forefront request ordering.

### [**](#handled_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L58)handled\_requests

**handled\_requests: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[str]

Set of request unique keys that have been handled.

### [**](#in_progress_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L55)in\_progress\_requests

**in\_progress\_requests: [set](https://crawlee.dev/python/python/api/class/SessionCookies.md#set)\[str]

Set of request unique keys currently being processed.

### [**](#regular_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L52)regular\_requests

**regular\_requests: dict\[str, int]

Mapping of regular request unique keys to their sequence numbers.

### [**](#sequence_counter)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_file_system/_request_queue_client.py#L43)sequence\_counter

**sequence\_counter: int

Counter for regular request ordering.


---

# RequestQueueStateDb<!-- -->

State table for request queues.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *RequestQueueStateDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/RequestQueueStateDb.md#__tablename__)
* [**forefront\_sequence\_counter](https://crawlee.dev/python/python/api/class/RequestQueueStateDb.md#forefront_sequence_counter)
* [**queue](https://crawlee.dev/python/python/api/class/RequestQueueStateDb.md#queue)
* [**request\_queue\_id](https://crawlee.dev/python/python/api/class/RequestQueueStateDb.md#request_queue_id)
* [**sequence\_counter](https://crawlee.dev/python/python/api/class/RequestQueueStateDb.md#sequence_counter)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L254)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#forefront_sequence_counter)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L264)forefront\_sequence\_counter

**forefront\_sequence\_counter: Mapped\[int]

Counter for forefront request ordering (negative).

### [**](#queue)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L268)queue

**queue: Mapped\[[RequestQueueMetadataDb](https://crawlee.dev/python/python/api/class/RequestQueueMetadataDb.md)]

### [**](#request_queue_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L256)request\_queue\_id

**request\_queue\_id: Mapped\[str]

Foreign key to metadata request queue record.

### [**](#sequence_counter)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L261)sequence\_counter

**sequence\_counter: Mapped\[int]

Counter for regular request ordering (positive).


---

# RequestState<!-- -->

Crawlee-specific request handling state.

## Index[**](#Index)

### Properties

* [**AFTER\_NAV](https://crawlee.dev/python/python/api/class/RequestState.md#AFTER_NAV)
* [**BEFORE\_NAV](https://crawlee.dev/python/python/api/class/RequestState.md#BEFORE_NAV)
* [**DONE](https://crawlee.dev/python/python/api/class/RequestState.md#DONE)
* [**ERROR](https://crawlee.dev/python/python/api/class/RequestState.md#ERROR)
* [**ERROR\_HANDLER](https://crawlee.dev/python/python/api/class/RequestState.md#ERROR_HANDLER)
* [**REQUEST\_HANDLER](https://crawlee.dev/python/python/api/class/RequestState.md#REQUEST_HANDLER)
* [**SKIPPED](https://crawlee.dev/python/python/api/class/RequestState.md#SKIPPED)
* [**UNPROCESSED](https://crawlee.dev/python/python/api/class/RequestState.md#UNPROCESSED)

## Properties<!-- -->[**](#Properties)

### [**](#AFTER_NAV)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L26)AFTER\_NAV

**AFTER\_NAV: Undefined

### [**](#BEFORE_NAV)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L25)BEFORE\_NAV

**BEFORE\_NAV: Undefined

### [**](#DONE)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L28)DONE

**DONE: Undefined

### [**](#ERROR)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L30)ERROR

**ERROR: Undefined

### [**](#ERROR_HANDLER)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L29)ERROR\_HANDLER

**ERROR\_HANDLER: Undefined

### [**](#REQUEST_HANDLER)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L27)REQUEST\_HANDLER

**REQUEST\_HANDLER: Undefined

### [**](#SKIPPED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L31)SKIPPED

**SKIPPED: Undefined

### [**](#UNPROCESSED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L24)UNPROCESSED

**UNPROCESSED: Undefined


---

# RequestWithLock<!-- -->

A crawling request with information about locks.

### Hierarchy

* [Request](https://crawlee.dev/python/python/api/class/Request.md)
  * *RequestWithLock*

## Index[**](#Index)

### Methods

* [**from\_url](https://crawlee.dev/python/python/api/class/RequestWithLock.md#from_url)
* [**get\_query\_param\_from\_url](https://crawlee.dev/python/python/api/class/RequestWithLock.md#get_query_param_from_url)

### Properties

* [**crawl\_depth](https://crawlee.dev/python/python/api/class/RequestWithLock.md#crawl_depth)
* [**crawlee\_data](https://crawlee.dev/python/python/api/class/RequestWithLock.md#crawlee_data)
* [**enqueue\_strategy](https://crawlee.dev/python/python/api/class/RequestWithLock.md#enqueue_strategy)
* [**forefront](https://crawlee.dev/python/python/api/class/RequestWithLock.md#forefront)
* [**handled\_at](https://crawlee.dev/python/python/api/class/RequestWithLock.md#handled_at)
* [**label](https://crawlee.dev/python/python/api/class/RequestWithLock.md#label)
* [**last\_proxy\_tier](https://crawlee.dev/python/python/api/class/RequestWithLock.md#last_proxy_tier)
* [**loaded\_url](https://crawlee.dev/python/python/api/class/RequestWithLock.md#loaded_url)
* [**lock\_expires\_at](https://crawlee.dev/python/python/api/class/RequestWithLock.md#lock_expires_at)
* [**max\_retries](https://crawlee.dev/python/python/api/class/RequestWithLock.md#max_retries)
* [**method](https://crawlee.dev/python/python/api/class/RequestWithLock.md#method)
* [**model\_config](https://crawlee.dev/python/python/api/class/RequestWithLock.md#model_config)
* [**no\_retry](https://crawlee.dev/python/python/api/class/RequestWithLock.md#no_retry)
* [**payload](https://crawlee.dev/python/python/api/class/RequestWithLock.md#payload)
* [**retry\_count](https://crawlee.dev/python/python/api/class/RequestWithLock.md#retry_count)
* [**session\_id](https://crawlee.dev/python/python/api/class/RequestWithLock.md#session_id)
* [**session\_rotation\_count](https://crawlee.dev/python/python/api/class/RequestWithLock.md#session_rotation_count)
* [**state](https://crawlee.dev/python/python/api/class/RequestWithLock.md#state)
* [**unique\_key](https://crawlee.dev/python/python/api/class/RequestWithLock.md#unique_key)
* [**url](https://crawlee.dev/python/python/api/class/RequestWithLock.md#url)
* [**was\_already\_handled](https://crawlee.dev/python/python/api/class/RequestWithLock.md#was_already_handled)

## Methods<!-- -->[**](#Methods)

### [**](#from_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L243)from\_url

* ****from\_url**(url, \*, method, headers, payload, label, session\_id, unique\_key, keep\_url\_fragment, use\_extended\_unique\_key, always\_enqueue, enqueue\_strategy, max\_retries, kwargs): Self

- Inherited from [Request.from\_url](https://crawlee.dev/python/python/api/class/Request.md#from_url)

  Create a new `Request` instance from a URL.

  This is recommended constructor for creating new `Request` instances. It generates a `Request` object from a given URL with additional options to customize HTTP method, payload, unique key, and other request properties. If no `unique_key` or `id` is provided, they are computed automatically based on the URL, method and payload. It depends on the `keep_url_fragment` and `use_extended_unique_key` flags.

  ***

  #### Parameters

  * ##### url: str

    The URL of the request.

  * ##### optionalkeyword-onlymethod: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) = <!-- -->'GET'

    The HTTP method of the request.

  * ##### optionalkeyword-onlyheaders: HttpHeaders | dict\[str, str] | None = <!-- -->None

    The HTTP headers of the request.

  * ##### optionalkeyword-onlypayload: HttpPayload | str | None = <!-- -->None

    The data to be sent as the request body. Typically used with 'POST' or 'PUT' requests.

  * ##### optionalkeyword-onlylabel: str | None = <!-- -->None

    A custom label to differentiate between request types. This is stored in `user_data`, and it is used for request routing (different requests go to different handlers).

  * ##### optionalkeyword-onlysession\_id: str | None = <!-- -->None

    ID of a specific `Session` to which the request will be strictly bound. If the session becomes unavailable when the request is processed, a `RequestCollisionError` will be raised.

  * ##### optionalkeyword-onlyunique\_key: str | None = <!-- -->None

    A unique key identifying the request. If not provided, it is automatically computed based on the URL and other parameters. Requests with the same `unique_key` are treated as identical.

  * ##### optionalkeyword-onlykeep\_url\_fragment: bool = <!-- -->False

    Determines whether the URL fragment (e.g., `` `section` ``) should be included in the `unique_key` computation. This is only relevant when `unique_key` is not provided.

  * ##### optionalkeyword-onlyuse\_extended\_unique\_key: bool = <!-- -->False

    Determines whether to include the HTTP method, ID Session and payload in the `unique_key` computation. This is only relevant when `unique_key` is not provided.

  * ##### optionalkeyword-onlyalways\_enqueue: bool = <!-- -->False

    If set to `True`, the request will be enqueued even if it is already present in the queue. Using this is not allowed when a custom `unique_key` is also provided and will result in a `ValueError`.

  * ##### optionalkeyword-onlyenqueue\_strategy: EnqueueStrategy | None = <!-- -->None

    The strategy that will be used for enqueuing the request.

  * ##### optionalkeyword-onlymax\_retries: int | None = <!-- -->None

    Maximum number of retries for this request. Allows to override the global `max_request_retries` option of `BasicCrawler`.

  * ##### kwargs: Any

  #### Returns Self

### [**](#get_query_param_from_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L344)get\_query\_param\_from\_url

* ****get\_query\_param\_from\_url**(param, \*, default): str | None

- Inherited from [Request.get\_query\_param\_from\_url](https://crawlee.dev/python/python/api/class/Request.md#get_query_param_from_url)

  Get the value of a specific query parameter from the URL.

  ***

  #### Parameters

  * ##### param: str
  * ##### optionalkeyword-onlydefault: str | None = <!-- -->None

  #### Returns str | None

## Properties<!-- -->[**](#Properties)

### [**](#crawl_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L369)crawl\_depth

**crawl\_depth: int

Inherited from [Request.crawl\_depth](https://crawlee.dev/python/python/api/class/Request.md#crawl_depth)

Overrides [Request.crawl\_depth](https://crawlee.dev/python/python/api/class/Request.md#crawl_depth)

The depth of the request in the crawl tree.

### [**](#crawlee_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L360)crawlee\_data

**crawlee\_data: [CrawleeRequestData](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md)

Inherited from [Request.crawlee\_data](https://crawlee.dev/python/python/api/class/Request.md#crawlee_data)

Crawlee-specific configuration stored in the `user_data`.

### [**](#enqueue_strategy)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L401)enqueue\_strategy

**enqueue\_strategy: [EnqueueStrategy](https://crawlee.dev/python/python/api.md#EnqueueStrategy)

Inherited from [Request.enqueue\_strategy](https://crawlee.dev/python/python/api/class/Request.md#enqueue_strategy)

Overrides [Request.enqueue\_strategy](https://crawlee.dev/python/python/api/class/Request.md#enqueue_strategy)

The strategy that was used for enqueuing the request.

### [**](#forefront)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L419)forefront

**forefront: bool

Inherited from [Request.forefront](https://crawlee.dev/python/python/api/class/Request.md#forefront)

Overrides [Request.forefront](https://crawlee.dev/python/python/api/class/Request.md#forefront)

Indicate whether the request should be enqueued at the front of the queue.

### [**](#handled_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L239)handled\_at

**handled\_at: Annotated\[datetime | None, Field(alias='handledAt')]

Inherited from [Request.handled\_at](https://crawlee.dev/python/python/api/class/Request.md#handled_at)

Timestamp when the request was handled.

### [**](#label)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L350)label

**label: str | None

Inherited from [Request.label](https://crawlee.dev/python/python/api/class/Request.md#label)

A string used to differentiate between arbitrary request types.

### [**](#last_proxy_tier)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L410)last\_proxy\_tier

**last\_proxy\_tier: int | None

Inherited from [Request.last\_proxy\_tier](https://crawlee.dev/python/python/api/class/Request.md#last_proxy_tier)

Overrides [Request.last\_proxy\_tier](https://crawlee.dev/python/python/api/class/Request.md#last_proxy_tier)

The last proxy tier used to process the request.

### [**](#loaded_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L236)loaded\_url

**loaded\_url: Annotated\[str | None, BeforeValidator(validate\_http\_url), Field(alias='loadedUrl')]

Inherited from [Request.loaded\_url](https://crawlee.dev/python/python/api/class/Request.md#loaded_url)

URL of the web page that was loaded. This can differ from the original URL in case of redirects.

### [**](#lock_expires_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L436)lock\_expires\_at

**lock\_expires\_at: datetime

The timestamp when the lock expires.

### [**](#max_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L387)max\_retries

**max\_retries: int | None

Inherited from [Request.max\_retries](https://crawlee.dev/python/python/api/class/Request.md#max_retries)

Crawlee-specific limit on the number of retries of the request.

### [**](#method)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L187)method

**method: Annotated\[HttpMethod, Field(frozen=True)]

Inherited from [Request.method](https://crawlee.dev/python/python/api/class/Request.md#method)

HTTP request method.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L169)model\_config

**model\_config: Undefined

Inherited from [Request.model\_config](https://crawlee.dev/python/python/api/class/Request.md#model_config)

### [**](#no_retry)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L233)no\_retry

**no\_retry: Annotated\[bool, Field(alias='noRetry')]

Inherited from [Request.no\_retry](https://crawlee.dev/python/python/api/class/Request.md#no_retry)

If set to `True`, the request will not be retried in case of failure.

### [**](#payload)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L190)payload

**payload: Annotated\[ HttpPayload | None, BeforeValidator(lambda v: v.encode() if isinstance(v, str) else v), PlainSerializer(lambda v: v.decode() if isinstance(v, bytes) else v), Field(frozen=True), ]

Inherited from [Request.payload](https://crawlee.dev/python/python/api/class/Request.md#payload)

HTTP request payload.

### [**](#retry_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L230)retry\_count

**retry\_count: Annotated\[int, Field(alias='retryCount')]

Inherited from [Request.retry\_count](https://crawlee.dev/python/python/api/class/Request.md#retry_count)

Number of times the request has been retried.

### [**](#session_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L355)session\_id

**session\_id: str | None

Inherited from [Request.session\_id](https://crawlee.dev/python/python/api/class/Request.md#session_id)

The ID of the bound session, if there is any.

### [**](#session_rotation_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L392)session\_rotation\_count

**session\_rotation\_count: int | None

Inherited from [Request.session\_rotation\_count](https://crawlee.dev/python/python/api/class/Request.md#session_rotation_count)

Overrides [Request.session\_rotation\_count](https://crawlee.dev/python/python/api/class/Request.md#session_rotation_count)

Crawlee-specific number of finished session rotations for the request.

### [**](#state)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L378)state

**state: [RequestState](https://crawlee.dev/python/python/api/class/RequestState.md)

Inherited from [Request.state](https://crawlee.dev/python/python/api/class/Request.md#state)

Overrides [Request.state](https://crawlee.dev/python/python/api/class/Request.md#state)

Crawlee-specific request handling state.

### [**](#unique_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L171)unique\_key

**unique\_key: Annotated\[str, Field(alias='uniqueKey', frozen=True)]

Inherited from [Request.unique\_key](https://crawlee.dev/python/python/api/class/Request.md#unique_key)

A unique key identifying the request. Two requests with the same `unique_key` are considered as pointing to the same URL.

If `unique_key` is not provided, then it is automatically generated by normalizing the URL. For example, the URL of `HTTP://www.EXAMPLE.com/something/` will produce the `unique_key` of `http://www.example.com/something`.

Pass an arbitrary non-empty text value to the `unique_key` property to override the default behavior and specify which URLs shall be considered equal.

### [**](#url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L183)url

**url: Annotated\[str, BeforeValidator(validate\_http\_url), Field(frozen=True)]

Inherited from [Request.url](https://crawlee.dev/python/python/api/class/Request.md#url)

The URL of the web page to crawl. Must be a valid HTTP or HTTPS URL, and may include query parameters and fragments.

### [**](#was_already_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L428)was\_already\_handled

**was\_already\_handled: bool

Inherited from [Request.was\_already\_handled](https://crawlee.dev/python/python/api/class/Request.md#was_already_handled)

Indicates whether the request was handled.


---

# RobotsTxtFile<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#__init__)
* [**find](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#find)
* [**from\_content](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#from_content)
* [**get\_crawl\_delay](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#get_crawl_delay)
* [**get\_sitemaps](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#get_sitemaps)
* [**is\_allowed](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#is_allowed)
* [**load](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#load)
* [**parse\_sitemaps](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#parse_sitemaps)
* [**parse\_urls\_from\_sitemaps](https://crawlee.dev/python/python/api/class/RobotsTxtFile.md#parse_urls_from_sitemaps)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L23)\_\_init\_\_

* ****\_\_init\_\_**(url, robots, http\_client, proxy\_info): None

- #### Parameters

  * ##### url: str
  * ##### robots: Protego
  * ##### optionalhttp\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md) | None = <!-- -->None
  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

  #### Returns None

### [**](#find)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L43)find

* **async **find**(url, http\_client, proxy\_info): Self

- Determine the location of a robots.txt file for a URL and fetch it.

  ***

  #### Parameters

  * ##### url: str

    The URL whose domain will be used to find the corresponding robots.txt file.

  * ##### http\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

    Optional `ProxyInfo` to be used when fetching the robots.txt file. If None, no proxy is used.

  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The `HttpClient` instance used to perform the network request for fetching the robots.txt file.

  #### Returns Self

### [**](#from_content)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L32)from\_content

* **async **from\_content**(url, content): Self

- Create a `RobotsTxtFile` instance from the given content.

  ***

  #### Parameters

  * ##### url: str

    The URL associated with the robots.txt file.

  * ##### content: str

    The raw string content of the robots.txt file to be parsed.

  #### Returns Self

### [**](#get_crawl_delay)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L96)get\_crawl\_delay

* ****get\_crawl\_delay**(user\_agent): int | None

- Get the crawl delay for the given user agent.

  ***

  #### Parameters

  * ##### optionaluser\_agent: str = <!-- -->'\*'

    The user-agent string to check the crawl delay for. Defaults to '\*' which matches any user-agent.

  #### Returns int | None

### [**](#get_sitemaps)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L92)get\_sitemaps

* ****get\_sitemaps**(): list\[str]

- Get the list of sitemaps urls from the robots.txt file.

  ***

  #### Returns list\[str]

### [**](#is_allowed)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L80)is\_allowed

* ****is\_allowed**(url, user\_agent): bool

- Check if the given URL is allowed for the given user agent.

  ***

  #### Parameters

  * ##### url: str

    The URL to check against the robots.txt rules.

  * ##### optionaluser\_agent: str = <!-- -->'\*'

    The user-agent string to check permissions for. Defaults to '\*' which matches any user-agent.

  #### Returns bool

### [**](#load)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L55)load

* **async **load**(url, http\_client, proxy\_info): Self

- Load the robots.txt file for a given URL.

  ***

  #### Parameters

  * ##### url: str

    The direct URL of the robots.txt file to be loaded.

  * ##### http\_client: [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)

    The `HttpClient` instance used to perform the network request for fetching the robots.txt file.

  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    Optional `ProxyInfo` to be used when fetching the robots.txt file. If None, no proxy is used.

  #### Returns Self

### [**](#parse_sitemaps)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L106)parse\_sitemaps

* **async **parse\_sitemaps**(): [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

- Parse the sitemaps from the robots.txt file and return a `Sitemap` instance.

  ***

  #### Returns [Sitemap](https://crawlee.dev/python/python/api/class/Sitemap.md)

### [**](#parse_urls_from_sitemaps)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/robots.py#L114)parse\_urls\_from\_sitemaps

* **async **parse\_urls\_from\_sitemaps**(): list\[str]

- Parse the sitemaps in the robots.txt file and return a list URLs.

  ***

  #### Returns list\[str]


---

