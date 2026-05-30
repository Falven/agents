# SystemStatus<!-- -->

Provides a simple interface for evaluating system resource usage from snapshots collected by `Snapshotter`.

This class aggregates and interprets snapshots from a Snapshotter instance to evaluate the current and historical status of system resources like CPU, memory, event loop, and client API usage. It exposes two methods `get_current_system_info` and `get_historical_system_info`. The system information is computed using a weighted average of overloaded messages in the snapshots, with the weights being the time intervals between the snapshots. Each resource is computed separately, and the system is considered as overloaded whenever at least one resource is overloaded.

`get_current_system_info` returns a `SystemInfo` data structure that represents the current status of the system. The length of the current timeframe in seconds is configurable by the `max_snapshot_age` option and represents the max age of snapshots to be considered for the computation.

`SystemStatus.get_historical_system_info` returns a `SystemInfo` that represents the long-term status of the system. It considers the full snapshot history available in the `Snapshotter` instance.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/SystemStatus.md#__init__)
* [**get\_current\_system\_info](https://crawlee.dev/python/python/api/class/SystemStatus.md#get_current_system_info)
* [**get\_historical\_system\_info](https://crawlee.dev/python/python/api/class/SystemStatus.md#get_historical_system_info)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/system_status.py#L39)\_\_init\_\_

* ****\_\_init\_\_**(snapshotter, \*, max\_snapshot\_age, cpu\_overload\_threshold, memory\_overload\_threshold, event\_loop\_overload\_threshold, client\_overload\_threshold): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### snapshotter: [Snapshotter](https://crawlee.dev/python/python/api/class/Snapshotter.md)

    The `Snapshotter` instance to be queried for `SystemStatus`.

  * ##### optionalkeyword-onlymax\_snapshot\_age: timedelta = <!-- -->timedelta(seconds=5)

    Defines max age of snapshots used in the `SystemStatus.get_current_system_info` measurement.

  * ##### optionalkeyword-onlycpu\_overload\_threshold: float = <!-- -->0.4

    Sets the threshold of overloaded snapshots in the CPU sample. If the sample exceeds this threshold, the system will be considered overloaded.

  * ##### optionalkeyword-onlymemory\_overload\_threshold: float = <!-- -->0.2

    Sets the threshold of overloaded snapshots in the memory sample. If the sample exceeds this threshold, the system will be considered overloaded.

  * ##### optionalkeyword-onlyevent\_loop\_overload\_threshold: float = <!-- -->0.6

    Sets the threshold of overloaded snapshots in the event loop sample. If the sample exceeds this threshold, the system will be considered overloaded.

  * ##### optionalkeyword-onlyclient\_overload\_threshold: float = <!-- -->0.3

    Sets the threshold of overloaded snapshots in the Client sample. If the sample exceeds this threshold, the system will be considered overloaded.

  #### Returns None

### [**](#get_current_system_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/system_status.py#L71)get\_current\_system\_info

* ****get\_current\_system\_info**(): [SystemInfo](https://crawlee.dev/python/python/api/class/SystemInfo.md)

- Retrieve and evaluates the current status of system resources.

  Considers snapshots within the `_max_snapshot_age` timeframe and determines if the system is currently overloaded based on predefined thresholds for each resource type.

  ***

  #### Returns [SystemInfo](https://crawlee.dev/python/python/api/class/SystemInfo.md)

  An object representing the current system status.

### [**](#get_historical_system_info)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/system_status.py#L82)get\_historical\_system\_info

* ****get\_historical\_system\_info**(): [SystemInfo](https://crawlee.dev/python/python/api/class/SystemInfo.md)

- Retrieve and evaluates the historical status of system resources.

  Considers the entire history of snapshots from the Snapshotter to assess long-term system performance and determines if the system has been historically overloaded.

  ***

  #### Returns [SystemInfo](https://crawlee.dev/python/python/api/class/SystemInfo.md)

  An object representing the historical system status.


---

# TimerResult<!-- -->

## Index[**](#Index)

### Properties

* [**cpu](https://crawlee.dev/python/python/api/class/TimerResult.md#cpu)
* [**wall](https://crawlee.dev/python/python/api/class/TimerResult.md#wall)

## Properties<!-- -->[**](#Properties)

### [**](#cpu)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/time.py#L22)cpu

**cpu: float | None

### [**](#wall)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/time.py#L21)wall

**wall: float | None


---

# UnprocessedRequest<!-- -->

Represents an unprocessed request.

## Index[**](#Index)

### Properties

* [**method](https://crawlee.dev/python/python/api/class/UnprocessedRequest.md#method)
* [**model\_config](https://crawlee.dev/python/python/api/class/UnprocessedRequest.md#model_config)
* [**unique\_key](https://crawlee.dev/python/python/api/class/UnprocessedRequest.md#unique_key)
* [**url](https://crawlee.dev/python/python/api/class/UnprocessedRequest.md#url)

## Properties<!-- -->[**](#Properties)

### [**](#method)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L161)method

**method: [HttpMethod](https://crawlee.dev/python/python/api.md#HttpMethod) | None

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L157)model\_config

**model\_config: Undefined

### [**](#unique_key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L159)unique\_key

**unique\_key: str

### [**](#url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L160)url

**url: str


---

# UserData<!-- -->

Represents the `user_data` part of a Request.

Apart from the well-known attributes (`label` and `__crawlee`), it can also contain arbitrary JSON-compatible values.

## Index[**](#Index)

### Methods

* [**\_\_delitem\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__delitem__)
* [**\_\_eq\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__eq__)
* [**\_\_getitem\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__getitem__)
* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__hash__)
* [**\_\_iter\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__iter__)
* [**\_\_len\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__len__)
* [**\_\_setitem\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__setitem__)

### Properties

* [**\_\_pydantic\_extra\_\_](https://crawlee.dev/python/python/api/class/UserData.md#__pydantic_extra__)
* [**crawlee\_data](https://crawlee.dev/python/python/api/class/UserData.md#crawlee_data)
* [**label](https://crawlee.dev/python/python/api/class/UserData.md#label)
* [**model\_config](https://crawlee.dev/python/python/api/class/UserData.md#model_config)

## Methods<!-- -->[**](#Methods)

### [**](#__delitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L93)\_\_delitem\_\_

* ****\_\_delitem\_\_**(key): None

- #### Parameters

  * ##### key: str

  #### Returns None

### [**](#__eq__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L102)\_\_eq\_\_

* ****\_\_eq\_\_**(other): bool

- #### Parameters

  * ##### other: object

  #### Returns bool

### [**](#__getitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L81)\_\_getitem\_\_

* ****\_\_getitem\_\_**(key): JsonSerializable

- #### Parameters

  * ##### key: str

  #### Returns JsonSerializable

### [**](#__hash__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L111)\_\_hash\_\_

* ****\_\_hash\_\_**(): int

- Return hash based on the model fields.

  ***

  #### Returns int

### [**](#__iter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L96)\_\_iter\_\_

* ****\_\_iter\_\_**(): Iterator\[str]

- #### Returns Iterator\[str]

### [**](#__len__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L99)\_\_len\_\_

* ****\_\_len\_\_**(): int

- #### Returns int

### [**](#__setitem__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L84)\_\_setitem\_\_

* ****\_\_setitem\_\_**(key, value): None

- #### Parameters

  * ##### key: str
  * ##### value: JsonSerializable

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#__pydantic_extra__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L73)\_\_pydantic\_extra\_\_

**\_\_pydantic\_extra\_\_: dict\[str, JsonSerializable]

### [**](#crawlee_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L75)crawlee\_data

**crawlee\_data: [CrawleeRequestData](https://crawlee.dev/python/python/api/class/CrawleeRequestData.md) | None

Crawlee-specific configuration stored in the `user_data`.

### [**](#label)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L78)label

**label: str | None

Label used for request routing.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_request.py#L72)model\_config

**model\_config: Undefined


---

# UserDefinedErrorHandlerError<!-- -->

Wraps an exception thrown from an user-defined error handler.

### Hierarchy

* *UserDefinedErrorHandlerError*
  * [UserHandlerTimeoutError](https://crawlee.dev/python/python/api/class/UserHandlerTimeoutError.md)


---

# UserHandlerTimeoutError<!-- -->

Raised when a router fails due to user raised timeout. This is different from user-defined handler timing out.

### Hierarchy

* [UserDefinedErrorHandlerError](https://crawlee.dev/python/python/api/class/UserDefinedErrorHandlerError.md)
  * *UserHandlerTimeoutError*


---

# UseStateFunction<!-- -->

A function for managing state within the crawling context.

It allows the use of persistent state across multiple crawls.

Warning

This is an experimental feature. The behavior and interface may change in future versions.

## Index[**](#Index)

### Methods

* [**\_\_call\_\_](https://crawlee.dev/python/python/api/class/UseStateFunction.md#__call__)

## Methods<!-- -->[**](#Methods)

### [**](#__call__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L617)\_\_call\_\_

* ****\_\_call\_\_**(default\_value): Coroutine\[None, None, dict\[str, JsonSerializable]]

- Call dunder method.

  ***

  #### Parameters

  * ##### optionaldefault\_value: dict\[str, JsonSerializable] | None = <!-- -->None

    The default value to initialize the state if it is not already set.

  #### Returns Coroutine\[None, None, dict\[str, JsonSerializable]]

  The current state.


---

# VersionDb<!-- -->

Table for storing the database schema version.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *VersionDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/VersionDb.md#__tablename__)
* [**version](https://crawlee.dev/python/python/api/class/VersionDb.md#version)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L274)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L276)version

**version: Mapped\[str]


---

# Event<!-- -->

Names of all possible events that can be emitted using an `EventManager`.

## Index[**](#Index)

### Enumeration members

* [**ABORTING](https://crawlee.dev/python/python/api/enum/Event.md#ABORTING)
* [**BROWSER\_CLOSED](https://crawlee.dev/python/python/api/enum/Event.md#BROWSER_CLOSED)
* [**BROWSER\_LAUNCHED](https://crawlee.dev/python/python/api/enum/Event.md#BROWSER_LAUNCHED)
* [**BROWSER\_RETIRED](https://crawlee.dev/python/python/api/enum/Event.md#BROWSER_RETIRED)
* [**CRAWLER\_STATUS](https://crawlee.dev/python/python/api/enum/Event.md#CRAWLER_STATUS)
* [**EXIT](https://crawlee.dev/python/python/api/enum/Event.md#EXIT)
* [**MIGRATING](https://crawlee.dev/python/python/api/enum/Event.md#MIGRATING)
* [**PAGE\_CLOSED](https://crawlee.dev/python/python/api/enum/Event.md#PAGE_CLOSED)
* [**PAGE\_CREATED](https://crawlee.dev/python/python/api/enum/Event.md#PAGE_CREATED)
* [**PERSIST\_STATE](https://crawlee.dev/python/python/api/enum/Event.md#PERSIST_STATE)
* [**SESSION\_RETIRED](https://crawlee.dev/python/python/api/enum/Event.md#SESSION_RETIRED)
* [**SYSTEM\_INFO](https://crawlee.dev/python/python/api/enum/Event.md#SYSTEM_INFO)

## Enumeration members<!-- -->[**](<#Enumeration members>)

### [**](#ABORTING)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L22)ABORTING

**ABORTING: 'aborting'

### [**](#BROWSER_CLOSED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L31)BROWSER\_CLOSED

**BROWSER\_CLOSED: 'browserClosed'

### [**](#BROWSER_LAUNCHED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L29)BROWSER\_LAUNCHED

**BROWSER\_LAUNCHED: 'browserLaunched'

### [**](#BROWSER_RETIRED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L30)BROWSER\_RETIRED

**BROWSER\_RETIRED: 'browserRetired'

### [**](#CRAWLER_STATUS)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L36)CRAWLER\_STATUS

**CRAWLER\_STATUS: 'crawlerStatus'

### [**](#EXIT)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L23)EXIT

**EXIT: 'exit'

### [**](#MIGRATING)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L21)MIGRATING

**MIGRATING: 'migrating'

### [**](#PAGE_CLOSED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L33)PAGE\_CLOSED

**PAGE\_CLOSED: 'pageClosed'

### [**](#PAGE_CREATED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L32)PAGE\_CREATED

**PAGE\_CREATED: 'pageCreated'

### [**](#PERSIST_STATE)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L19)PERSIST\_STATE

**PERSIST\_STATE: 'persistState'

### [**](#SESSION_RETIRED)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L26)SESSION\_RETIRED

**SESSION\_RETIRED: 'sessionRetired'

### [**](#SYSTEM_INFO)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_types.py#L20)SYSTEM\_INFO

**SYSTEM\_INFO: 'systemInfo'


---

* [](https://crawlee.dev/python/python)
* Changelog

Version: 1.6

On this page

