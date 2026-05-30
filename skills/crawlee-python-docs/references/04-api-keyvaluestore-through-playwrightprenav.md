# KeyValueStore<!-- -->

Key-value store is a storage for reading and writing data records with unique key identifiers.

The key-value store class acts as a high-level interface for storing, retrieving, and managing data records identified by unique string keys. It abstracts away the underlying storage implementation details, allowing you to work with the same API regardless of whether data is stored in memory, on disk, or in the cloud.

Each data record is associated with a specific MIME content type, allowing storage of various data formats such as JSON, text, images, HTML snapshots or any binary data. This class is commonly used to store inputs, outputs, and other artifacts of crawler operations.

You can instantiate a key-value store using the `open` class method, which will create a store with the specified name or id. The underlying storage implementation is determined by the configured storage client.

### Usage

```
from crawlee.storages import KeyValueStore

# Open a named key-value store
kvs = await KeyValueStore.open(name='my-store')

# Store and retrieve data
await kvs.set_value('product-1234.json', [{'name': 'Smartphone', 'price': 799.99}])
product = await kvs.get_value('product-1234')
```

### Hierarchy

* [Storage](https://crawlee.dev/python/python/api/class/Storage.md)
  * *KeyValueStore*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/KeyValueStore.md#__init__)
* [**delete\_value](https://crawlee.dev/python/python/api/class/KeyValueStore.md#delete_value)
* [**drop](https://crawlee.dev/python/python/api/class/KeyValueStore.md#drop)
* [**get\_auto\_saved\_value](https://crawlee.dev/python/python/api/class/KeyValueStore.md#get_auto_saved_value)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/KeyValueStore.md#get_metadata)
* [**get\_public\_url](https://crawlee.dev/python/python/api/class/KeyValueStore.md#get_public_url)
* [**get\_value](https://crawlee.dev/python/python/api/class/KeyValueStore.md#get_value)
* [**iterate\_keys](https://crawlee.dev/python/python/api/class/KeyValueStore.md#iterate_keys)
* [**list\_keys](https://crawlee.dev/python/python/api/class/KeyValueStore.md#list_keys)
* [**open](https://crawlee.dev/python/python/api/class/KeyValueStore.md#open)
* [**persist\_autosaved\_values](https://crawlee.dev/python/python/api/class/KeyValueStore.md#persist_autosaved_values)
* [**purge](https://crawlee.dev/python/python/api/class/KeyValueStore.md#purge)
* [**record\_exists](https://crawlee.dev/python/python/api/class/KeyValueStore.md#record_exists)
* [**set\_value](https://crawlee.dev/python/python/api/class/KeyValueStore.md#set_value)

### Properties

* [**id](https://crawlee.dev/python/python/api/class/KeyValueStore.md#id)
* [**name](https://crawlee.dev/python/python/api/class/KeyValueStore.md#name)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L78)\_\_init\_\_

* ****\_\_init\_\_**(client, id, name): None

- Initialize a new instance.

  Preferably use the `KeyValueStore.open` constructor to create a new instance.

  ***

  #### Parameters

  * ##### client: [KeyValueStoreClient](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md)

    An instance of a storage client.

  * ##### id: str

    The unique identifier of the storage.

  * ##### name: str | None

    The name of the storage, if available.

  #### Returns None

### [**](#delete_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L188)delete\_value

* **async **delete\_value**(key): None

- Delete a value from the KVS.

  ***

  #### Parameters

  * ##### key: str

    Key of the record to delete.

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L140)drop

* **async **drop**(): None

- Overrides [Storage.drop](https://crawlee.dev/python/python/api/class/Storage.md#drop)

  Drop the storage, removing it from the underlying storage client and clearing the cache.

  ***

  #### Returns None

### [**](#get_auto_saved_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L262)get\_auto\_saved\_value

* **async **get\_auto\_saved\_value**(key, default\_value): dict\[str, JsonSerializable]

- Get a value from KVS that will be automatically saved on changes.

  ***

  #### Parameters

  * ##### key: str

    Key of the record, to store the value.

  * ##### optionaldefault\_value: dict\[str, JsonSerializable] | None = <!-- -->None

    Value to be used if the record does not exist yet. Should be a dictionary.

  #### Returns dict\[str, JsonSerializable]

  Return the value of the key.

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L108)get\_metadata

* **async **get\_metadata**(): ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [Storage.get\_metadata](https://crawlee.dev/python/python/api/class/Storage.md#get_metadata)

  Get the storage metadata.

  ***

  #### Returns ([DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md) | [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)) | [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#get_public_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L251)get\_public\_url

* **async **get\_public\_url**(key): str

- Get the public URL for the given key.

  ***

  #### Parameters

  * ##### key: str

    Key of the record for which URL is required.

  #### Returns str

  The public URL for the given key.

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L160)get\_value

* **async **get\_value**(key: str, default\_value?
  <!-- -->
  : [T](https://crawlee.dev/python/python/api.md#T) | None): [T](https://crawlee.dev/python/python/api.md#T) | None
* **async **get\_value**(key: str): Any
* **async **get\_value**(key: str, default\_value: [T](https://crawlee.dev/python/python/api.md#T)): [T](https://crawlee.dev/python/python/api.md#T)
* **async **get\_value**(key: str, default\_value?
  <!-- -->
  : [T](https://crawlee.dev/python/python/api.md#T) | None): [T](https://crawlee.dev/python/python/api.md#T) | None

- Get a value from the KVS.

  ***

  #### Parameters

  * ##### key: str

    Key of the record to retrieve.

  * ##### optionaldefault\_value: [T](https://crawlee.dev/python/python/api.md#T) | None = <!-- -->None

    Default value returned in case the record does not exist.

  #### Returns [T](https://crawlee.dev/python/python/api.md#T) | None

  The value associated with the given key. `default_value` is used in case the record does not exist.

### [**](#iterate_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L196)iterate\_keys

* **async **iterate\_keys**(exclusive\_start\_key, limit): AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

- Iterate over the existing keys in the KVS.

  ***

  #### Parameters

  * ##### optionalexclusive\_start\_key: str | None = <!-- -->None

    Key to start the iteration from.

  * ##### optionallimit: int | None = <!-- -->None

    Maximum number of keys to return. None means no limit.

  #### Returns AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

### [**](#list_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L216)list\_keys

* **async **list\_keys**(exclusive\_start\_key, limit): list\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

- List all the existing keys in the KVS.

  It uses client's `iterate_keys` method to get the keys.

  ***

  #### Parameters

  * ##### optionalexclusive\_start\_key: str | None = <!-- -->None

    Key to start the iteration from.

  * ##### optionallimit: int = <!-- -->1000

    Maximum number of keys to return.

  #### Returns list\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

  A list of keys in the KVS.

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L113)open

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

### [**](#persist_autosaved_values)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L299)persist\_autosaved\_values

* **async **persist\_autosaved\_values**(): None

- Force autosaved values to be saved without waiting for an event in Event Manager.

  ***

  #### Returns None

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L148)purge

* **async **purge**(): None

- Overrides [Storage.purge](https://crawlee.dev/python/python/api/class/Storage.md#purge)

  Purge the storage, removing all items from the underlying storage client.

  This method does not remove the storage itself, e.g. don't remove the metadata, but clears all items within it.

  ***

  #### Returns None

### [**](#record_exists)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L240)record\_exists

* **async **record\_exists**(key): bool

- Check if a record with the given key exists in the key-value store.

  ***

  #### Parameters

  * ##### key: str

    Key of the record to check for existence.

  #### Returns bool

  True if a record with the given key exists, False otherwise.

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L173)set\_value

* **async **set\_value**(key, value, content\_type): None

- Set a value in the KVS.

  ***

  #### Parameters

  * ##### key: str

    Key of the record to set.

  * ##### value: Any

    Value to set.

  * ##### optionalcontent\_type: str | None = <!-- -->None

    The MIME content type string.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L99)id

**id: str

Overrides [Storage.id](https://crawlee.dev/python/python/api/class/Storage.md#id)

Get the storage ID.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storages/_key_value_store.py#L104)name

**name: str | None

Overrides [Storage.name](https://crawlee.dev/python/python/api/class/Storage.md#name)

Get the storage name.


---

# KeyValueStoreChangeRecords<!-- -->

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/KeyValueStoreChangeRecords.md#__init__)
* [**get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreChangeRecords.md#get_value)
* [**set\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreChangeRecords.md#set_value)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L236)\_\_init\_\_

* ****\_\_init\_\_**(actual\_key\_value\_store): None

- #### Parameters

  * ##### actual\_key\_value\_store: [KeyValueStore](https://crawlee.dev/python/python/api/class/KeyValueStore.md)

  #### Returns None

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L257)get\_value

* **async **get\_value**(key: str, default\_value?
  <!-- -->
  : [T](https://crawlee.dev/python/python/api.md#T) | None): [T](https://crawlee.dev/python/python/api.md#T) | None
* **async **get\_value**(key: str): Any
* **async **get\_value**(key: str, default\_value: [T](https://crawlee.dev/python/python/api.md#T)): [T](https://crawlee.dev/python/python/api.md#T)
* **async **get\_value**(key: str, default\_value?
  <!-- -->
  : [T](https://crawlee.dev/python/python/api.md#T) | None): [T](https://crawlee.dev/python/python/api.md#T) | None

- #### Parameters

  * ##### key: str
  * ##### optionaldefault\_value: [T](https://crawlee.dev/python/python/api.md#T) | None = <!-- -->None

  #### Returns [T](https://crawlee.dev/python/python/api.md#T) | None

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L240)set\_value

* **async **set\_value**(key, value, content\_type): None

- #### Parameters

  * ##### key: str
  * ##### value: Any
  * ##### optionalcontent\_type: str | None = <!-- -->None

  #### Returns None


---

# KeyValueStoreClient<!-- -->

An abstract class for key-value store (KVS) storage clients.

Key-value stores clients provide an interface for accessing and manipulating KVS storage. They handle operations like getting, setting, deleting KVS values across different storage backends.

Storage clients are specific to the type of storage they manage (`Dataset`, `KeyValueStore`, `RequestQueue`), and can operate with various storage systems including memory, file system, databases, and cloud storage solutions.

This abstract class defines the interface that all specific KVS clients must implement.

### Hierarchy

* *KeyValueStoreClient*

  * [MemoryKeyValueStoreClient](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md)
  * [FileSystemKeyValueStoreClient](https://crawlee.dev/python/python/api/class/FileSystemKeyValueStoreClient.md)
  * [SqlKeyValueStoreClient](https://crawlee.dev/python/python/api/class/SqlKeyValueStoreClient.md)
  * [RedisKeyValueStoreClient](https://crawlee.dev/python/python/api/class/RedisKeyValueStoreClient.md)

## Index[**](#Index)

### Methods

* [**delete\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#delete_value)
* [**drop](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#drop)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_metadata)
* [**get\_public\_url](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_public_url)
* [**get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_value)
* [**iterate\_keys](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#iterate_keys)
* [**purge](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#purge)
* [**record\_exists](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#record_exists)
* [**set\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#set_value)

## Methods<!-- -->[**](#Methods)

### [**](#delete_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L60)delete\_value

* **async **delete\_value**(\*, key): None

- Overrides [KeyValueStoreClient.delete\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#delete_value)

  Delete a value from the key-value store by its key.

  The backend method for the `KeyValueStore.delete_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L32)drop

* **async **drop**(): None

- Overrides [KeyValueStoreClient.drop](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#drop)

  Drop the whole key-value store and remove all its values.

  The backend method for the `KeyValueStore.drop` call.

  ***

  #### Returns None

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L28)get\_metadata

* **async **get\_metadata**(): [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

- Overrides [KeyValueStoreClient.get\_metadata](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_metadata)

  Get the metadata of the key-value store.

  ***

  #### Returns [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

### [**](#get_public_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L83)get\_public\_url

* **async **get\_public\_url**(\*, key): str

- Overrides [KeyValueStoreClient.get\_public\_url](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_public_url)

  Get the public URL for the given key.

  The backend method for the `KeyValueStore.get_public_url` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns str

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L46)get\_value

* **async **get\_value**(\*, key): [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

- Overrides [KeyValueStoreClient.get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_value)

  Retrieve the given record from the key-value store.

  The backend method for the `KeyValueStore.get_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

### [**](#iterate_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L67)iterate\_keys

* **async **iterate\_keys**(\*, exclusive\_start\_key, limit): AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

- Overrides [KeyValueStoreClient.iterate\_keys](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#iterate_keys)

  Iterate over all the existing keys in the key-value store.

  The backend method for the `KeyValueStore.iterate_keys` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyexclusive\_start\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->None

  #### Returns AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L39)purge

* **async **purge**(): None

- Overrides [KeyValueStoreClient.purge](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#purge)

  Purge all items from the key-value store.

  The backend method for the `KeyValueStore.purge` call.

  ***

  #### Returns None

### [**](#record_exists)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L90)record\_exists

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

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_base/_key_value_store_client.py#L53)set\_value

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

# KeyValueStoreInterface<!-- -->

The (limited) part of the `KeyValueStore` interface that should be accessible from a request handler.

## Index[**](#Index)

### Methods

* [**get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreInterface.md#get_value)
* [**set\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreInterface.md#set_value)

## Methods<!-- -->[**](#Methods)

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L219)get\_value

* **async **get\_value**(key: str, default\_value?
  <!-- -->
  : [T](https://crawlee.dev/python/python/api.md#T) | None): [T](https://crawlee.dev/python/python/api.md#T) | None
* **async **get\_value**(key: str): Any
* **async **get\_value**(key: str, default\_value: [T](https://crawlee.dev/python/python/api.md#T)): [T](https://crawlee.dev/python/python/api.md#T)
* **async **get\_value**(key: str, default\_value?
  <!-- -->
  : [T](https://crawlee.dev/python/python/api.md#T) | None): [T](https://crawlee.dev/python/python/api.md#T) | None

- #### Parameters

  * ##### key: str
  * ##### optionaldefault\_value: [T](https://crawlee.dev/python/python/api.md#T) | None = <!-- -->None

  #### Returns [T](https://crawlee.dev/python/python/api.md#T) | None

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L221)set\_value

* **async **set\_value**(key, value, content\_type): None

- #### Parameters

  * ##### key: str
  * ##### value: Any
  * ##### optionalcontent\_type: str | None = <!-- -->None

  #### Returns None


---

# KeyValueStoreMetadata<!-- -->

Model for a key-value store metadata.

### Hierarchy

* [StorageMetadata](https://crawlee.dev/python/python/api/class/StorageMetadata.md)
  * *KeyValueStoreMetadata*

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md#accessed_at)
* [**created\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md#created_at)
* [**id](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md#id)
* [**model\_config](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md#model_config)
* [**modified\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md#name)

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

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L55)model\_config

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

# KeyValueStoreMetadataBufferDb<!-- -->

Buffer table for deferred key-value store metadata updates to reduce concurrent access issues.

### Hierarchy

* [MetadataBufferDb](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md)
* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *KeyValueStoreMetadataBufferDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md#__tablename__)
* [**accessed\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md#accessed_at)
* [**id](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md#id)
* [**key\_value\_store\_id](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md#key_value_store_id)
* [**modified\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md#modified_at)
* [**storage\_id](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md#storage_id)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L296)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L286)accessed\_at

**accessed\_at: Mapped\[datetime]

Inherited from [MetadataBufferDb.accessed\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#accessed_at)

New accessed\_at timestamp, if being updated.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L282)id

**id: Mapped\[int]

Inherited from [MetadataBufferDb.id](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#id)

Auto-increment primary key for ordering.

### [**](#key_value_store_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L299)key\_value\_store\_id

**key\_value\_store\_id: Mapped\[str]

ID of the key-value store being updated.

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L289)modified\_at

**modified\_at: Mapped\[datetime | None]

Inherited from [MetadataBufferDb.modified\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#modified_at)

New modified\_at timestamp, if being updated.

### [**](#storage_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L302)storage\_id

**storage\_id: Undefined

Alias for key\_value\_store\_id to match SqlClientMixin expectations.


---

# KeyValueStoreMetadataDb<!-- -->

Metadata table for key-value stores.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
* [StorageMetadataDb](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md)
  * *KeyValueStoreMetadataDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#__tablename__)
* [**accessed\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#accessed_at)
* [**buffer\_locked\_until](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#buffer_locked_until)
* [**created\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#created_at)
* [**id](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#id)
* [**internal\_name](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#internal_name)
* [**key\_value\_store\_id](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#key_value_store_id)
* [**modified\_at](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#modified_at)
* [**name](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#name)
* [**records](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md#records)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L130)\_\_tablename\_\_

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

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L140)id

**id: Undefined

Alias for key\_value\_store\_id to match Pydantic expectations.

### [**](#internal_name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L55)internal\_name

**internal\_name: Mapped\[str]

Inherited from [StorageMetadataDb.internal\_name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#internal_name)

Internal unique name for a storage instance based on a name or alias.

### [**](#key_value_store_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L132)key\_value\_store\_id

**key\_value\_store\_id: Mapped\[str]

Unique identifier for the key-value store.

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L67)modified\_at

**modified\_at: Mapped\[datetime]

Inherited from [StorageMetadataDb.modified\_at](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#modified_at)

Last modification datetime.

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L58)name

**name: Mapped\[str | None]

Inherited from [StorageMetadataDb.name](https://crawlee.dev/python/python/api/class/StorageMetadataDb.md#name)

Human-readable name. None becomes 'default' in database to enforce uniqueness.

### [**](#records)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L136)records

**records: Mapped\[list\[[KeyValueStoreRecordDb](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md)]]


---

# KeyValueStoreRecord<!-- -->

Model for a key-value store record.

### Hierarchy

* [KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)
  * *KeyValueStoreRecord*

## Index[**](#Index)

### Properties

* [**content\_type](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md#content_type)
* [**key](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md#key)
* [**model\_config](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md#model_config)
* [**size](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md#size)
* [**value](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md#value)

## Properties<!-- -->[**](#Properties)

### [**](#content_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L89)content\_type

**content\_type: Annotated\[str, Field(alias='contentType')]

Inherited from [KeyValueStoreRecordMetadata.content\_type](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#content_type)

The MIME type of the record.

Describe the format and type of data stored in the record, following the MIME specification.

### [**](#key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L83)key

**key: Annotated\[str, Field(alias='key')]

Inherited from [KeyValueStoreRecordMetadata.key](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#key)

The key of the record.

A unique identifier for the record in the key-value store.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L103)model\_config

**model\_config: Undefined

Overrides [KeyValueStoreRecordMetadata.model\_config](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#model_config)

### [**](#size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L95)size

**size: Annotated\[int | None, Field(alias='size', default=None)]

Inherited from [KeyValueStoreRecordMetadata.size](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#size)

The size of the record in bytes.

### [**](#value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L105)value

**value: [KvsValueType](https://crawlee.dev/python/python/api.md#KvsValueType)

The value of the record.


---

# KeyValueStoreRecordDb<!-- -->

Records table for key-value stores.

### Hierarchy

* [Base](https://crawlee.dev/python/python/api/class/Base.md)
  * *KeyValueStoreRecordDb*

## Index[**](#Index)

### Properties

* [**\_\_tablename\_\_](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#__tablename__)
* [**content\_type](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#content_type)
* [**key](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#key)
* [**key\_value\_store\_id](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#key_value_store_id)
* [**kvs](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#kvs)
* [**size](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#size)
* [**storage\_id](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#storage_id)
* [**value](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordDb.md#value)

## Properties<!-- -->[**](#Properties)

### [**](#__tablename__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L147)\_\_tablename\_\_

**\_\_tablename\_\_: Undefined

### [**](#content_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L164)content\_type

**content\_type: Mapped\[str]

MIME type for proper value deserialization.

### [**](#key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L158)key

**key: Mapped\[str]

The key part of the key-value pair.

### [**](#key_value_store_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L149)key\_value\_store\_id

**key\_value\_store\_id: Mapped\[str]

Foreign key to metadata key-value store record.

### [**](#kvs)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L171)kvs

**kvs: Mapped\[[KeyValueStoreMetadataDb](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataDb.md)]

### [**](#size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L167)size

**size: Mapped\[int | None]

Size of stored value in bytes.

### [**](#storage_id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L173)storage\_id

**storage\_id: Undefined

Alias for key\_value\_store\_id to match SqlClientMixin expectations.

### [**](#value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L161)value

**value: Mapped\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)]

Value stored as binary data to support any content type.


---

# KeyValueStoreRecordMetadata<!-- -->

Model for a key-value store record metadata.

### Hierarchy

* *KeyValueStoreRecordMetadata*
  * [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md)

## Index[**](#Index)

### Properties

* [**content\_type](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#content_type)
* [**key](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#key)
* [**model\_config](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#model_config)
* [**size](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md#size)

## Properties<!-- -->[**](#Properties)

### [**](#content_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L89)content\_type

**content\_type: str

The MIME type of the record.

Describe the format and type of data stored in the record, following the MIME specification.

### [**](#key)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L83)key

**key: str

The key of the record.

A unique identifier for the record in the key-value store.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L81)model\_config

**model\_config: Undefined

### [**](#size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/models.py#L95)size

**size: int | None

The size of the record in bytes.


---

# KeyValueStoreValue<!-- -->

## Index[**](#Index)

### Properties

* [**content](https://crawlee.dev/python/python/api/class/KeyValueStoreValue.md#content)
* [**content\_type](https://crawlee.dev/python/python/api/class/KeyValueStoreValue.md#content_type)

## Properties<!-- -->[**](#Properties)

### [**](#content)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L231)content

**content: Any

### [**](#content_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L232)content\_type

**content\_type: str | None


---

# LoadRatioInfo<!-- -->

Represent the load ratio of a resource.

## Index[**](#Index)

### Properties

* [**actual\_ratio](https://crawlee.dev/python/python/api/class/LoadRatioInfo.md#actual_ratio)
* [**is\_overloaded](https://crawlee.dev/python/python/api/class/LoadRatioInfo.md#is_overloaded)
* [**limit\_ratio](https://crawlee.dev/python/python/api/class/LoadRatioInfo.md#limit_ratio)

## Properties<!-- -->[**](#Properties)

### [**](#actual_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L24)actual\_ratio

**actual\_ratio: float

The actual ratio of overloaded and non-overloaded samples.

### [**](#is_overloaded)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L28)is\_overloaded

**is\_overloaded: bool

Indicate whether the resource is currently overloaded.

### [**](#limit_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L20)limit\_ratio

**limit\_ratio: float

The maximum ratio of overloaded and non-overloaded samples. If the actual ratio exceeds this value, the resource is considered as overloaded.


---

# LocalEventManager<!-- -->

Event manager for local environments.

It extends the `EventManager` to emit `SystemInfo` events at regular intervals. The `LocalEventManager` is intended to be used in local environments, where the system metrics are required managing the `Snapshotter` and `AutoscaledPool`.

### Hierarchy

* [EventManager](https://crawlee.dev/python/python/api/class/EventManager.md)
  * *LocalEventManager*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/LocalEventManager.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/LocalEventManager.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/LocalEventManager.md#__init__)
* [**emit](https://crawlee.dev/python/python/api/class/LocalEventManager.md#emit)
* [**from\_config](https://crawlee.dev/python/python/api/class/LocalEventManager.md#from_config)
* [**off](https://crawlee.dev/python/python/api/class/LocalEventManager.md#off)
* [**on](https://crawlee.dev/python/python/api/class/LocalEventManager.md#on)
* [**wait\_for\_all\_listeners\_to\_complete](https://crawlee.dev/python/python/api/class/LocalEventManager.md#wait_for_all_listeners_to_complete)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/LocalEventManager.md#active)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_local_event_manager.py#L72)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [LocalEventManager](https://crawlee.dev/python/python/api/class/LocalEventManager.md)

- Overrides [EventManager.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/EventManager.md#__aenter__)

  Initialize the local event manager upon entering the async context.

  It starts emitting system info events at regular intervals.

  ***

  #### Returns [LocalEventManager](https://crawlee.dev/python/python/api/class/LocalEventManager.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_local_event_manager.py#L84)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Overrides [EventManager.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/EventManager.md#__aexit__)

  Close the local event manager upon exiting the async context.

  It stops emitting system info events and closes the event manager.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_local_event_manager.py#L34)\_\_init\_\_

* ****\_\_init\_\_**(system\_info\_interval, \*, persist\_state\_interval, close\_timeout): None

- Overrides [EventManager.\_\_init\_\_](https://crawlee.dev/python/python/api/class/EventManager.md#__init__)

  Initialize a new instance.

  In most cases, you should use the `from_config` constructor to create a new instance based on the provided configuration.

  ***

  #### Parameters

  * ##### optionalsystem\_info\_interval: timedelta = <!-- -->timedelta(seconds=1)

    Interval at which `SystemInfo` events are emitted.

  * ##### keyword-onlyoptionalpersist\_state\_interval: timedelta

    Interval between emitted `PersistState` events to maintain state persistence.

  * ##### keyword-onlyoptionalclose\_timeout: timedelta | None

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

- Inherited from [EventManager.emit](https://crawlee.dev/python/python/api/class/EventManager.md#emit)

  Emit an event with the associated data to all registered listeners.

  ***

  #### Parameters

  * ##### keyword-onlyevent: [Event](https://crawlee.dev/python/python/api/enum/Event.md)

    The event which will be emitted.

  * ##### keyword-onlyevent\_data: [EventData](https://crawlee.dev/python/python/api.md#EventData)

    The data which will be passed to the event listeners.

  #### Returns None

### [**](#from_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_local_event_manager.py#L59)from\_config

* ****from\_config**(config): [LocalEventManager](https://crawlee.dev/python/python/api/class/LocalEventManager.md)

- Initialize a new instance based on the provided `Configuration`.

  ***

  #### Parameters

  * ##### optionalconfig: [Configuration](https://crawlee.dev/python/python/api/class/Configuration.md) | None = <!-- -->None

    The `Configuration` instance. Uses the global (default) one if not provided.

  #### Returns [LocalEventManager](https://crawlee.dev/python/python/api/class/LocalEventManager.md)

### [**](#off)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L210)off

* ****off**(\*, event, listener): None

- Inherited from [EventManager.off](https://crawlee.dev/python/python/api/class/EventManager.md#off)

  Remove a specific listener or all listeners for an event.

  ***

  #### Parameters

  * ##### keyword-onlyevent: [Event](https://crawlee.dev/python/python/api/enum/Event.md)

    The Actor event for which to remove listeners.

  * ##### optionalkeyword-onlylistener: EventListener\[Any] | None = <!-- -->None

    The listener which is supposed to be removed. If not passed, all listeners of this event are removed.

  #### Returns None

### [**](#on)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L160)on

* ****on**(\*: , event: [Event](https://crawlee.dev/python/python/api/enum/Event.md), listener: EventListener\[Any]): None
* ****on**(\*: , event: Literal\[Event.PERSIST\_STATE], listener: EventListener\[EventPersistStateData]): None
* ****on**(\*: , event: Literal\[Event.SYSTEM\_INFO], listener: EventListener\[EventSystemInfoData]): None
* ****on**(\*: , event: Literal\[Event.MIGRATING], listener: EventListener\[EventMigratingData]): None
* ****on**(\*: , event: Literal\[Event.ABORTING], listener: EventListener\[EventAbortingData]): None
* ****on**(\*: , event: Literal\[Event.EXIT], listener: EventListener\[EventExitData]): None
* ****on**(\*: , event: Literal\[Event.CRAWLER\_STATUS], listener: EventListener\[EventCrawlerStatusData]): None
* ****on**(\*: , event: [Event](https://crawlee.dev/python/python/api/enum/Event.md), listener: EventListener\[None]): None

- Inherited from [EventManager.on](https://crawlee.dev/python/python/api/class/EventManager.md#on)

  Register an event listener for a specific event.

  ***

  #### Parameters

  * ##### keyword-onlyevent: [Event](https://crawlee.dev/python/python/api/enum/Event.md)

    The event for which to listen to.

  * ##### keyword-onlylistener: EventListener\[Any]

    The function (sync or async) which is to be called when the event is emitted.

  #### Returns None

### [**](#wait_for_all_listeners_to_complete)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L252)wait\_for\_all\_listeners\_to\_complete

* **async **wait\_for\_all\_listeners\_to\_complete**(\*, timeout): None

- Inherited from [EventManager.wait\_for\_all\_listeners\_to\_complete](https://crawlee.dev/python/python/api/class/EventManager.md#wait_for_all_listeners_to_complete)

  Wait for all currently executing event listeners to complete.

  ***

  #### Parameters

  * ##### optionalkeyword-onlytimeout: timedelta | None = <!-- -->None

    The maximum time to wait for the event listeners to finish. If they do not complete within the specified timeout, they will be canceled.

  #### Returns None

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/events/_event_manager.py#L100)active

**active: bool

Inherited from [EventManager.active](https://crawlee.dev/python/python/api/class/EventManager.md#active)

Indicate whether the context is active.


---

# MemoryDatasetClient<!-- -->

Memory implementation of the dataset client.

This client stores dataset items in memory using Python lists and dictionaries. No data is persisted between process runs, meaning all stored data is lost when the program terminates. This implementation is primarily useful for testing, development, and short-lived crawler operations where persistent storage is not required.

The memory implementation provides fast access to data but is limited by available memory and does not support data sharing across different processes. It supports all dataset operations including sorting, filtering, and pagination, but performs them entirely in memory.

### Hierarchy

* [DatasetClient](https://crawlee.dev/python/python/api/class/DatasetClient.md)
  * *MemoryDatasetClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#__init__)
* [**drop](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#drop)
* [**get\_data](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#get_data)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#get_metadata)
* [**iterate\_items](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#iterate_items)
* [**open](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#purge)
* [**push\_data](https://crawlee.dev/python/python/api/class/MemoryDatasetClient.md#push_data)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L33)\_\_init\_\_

* ****\_\_init\_\_**(\*, metadata): None

- Initialize a new instance.

  Preferably use the `MemoryDatasetClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlymetadata: [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L98)drop

* **async **drop**(): None

- Overrides [DatasetClient.drop](https://crawlee.dev/python/python/api/class/DatasetClient.md#drop)

  Drop the whole dataset and remove all its items.

  The backend method for the `Dataset.drop` call.

  ***

  #### Returns None

### [**](#get_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L135)get\_data

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

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L48)get\_metadata

* **async **get\_metadata**(): [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

- Overrides [DatasetClient.get\_metadata](https://crawlee.dev/python/python/api/class/DatasetClient.md#get_metadata)

  Get the metadata of the dataset.

  ***

  #### Returns [DatasetMetadata](https://crawlee.dev/python/python/api/class/DatasetMetadata.md)

### [**](#iterate_items)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L194)iterate\_items

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

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L52)open

* **async **open**(\*, id, name, alias): Self

- Open or create a new memory dataset client.

  This method creates a new in-memory dataset instance. Unlike persistent storage implementations, memory datasets don't check for existing datasets with the same name or ID since all data exists only in memory and is lost when the process terminates.

  Alias does not have any effect on the memory storage client implementation, because unnamed storages are supported by default, since data are not persisted.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the dataset. If not provided, a random ID will be generated.

  * ##### keyword-onlyname: str | None

    The name of the dataset for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the dataset for unnamed (run scope) storages.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L107)purge

* **async **purge**(): None

- Overrides [DatasetClient.purge](https://crawlee.dev/python/python/api/class/DatasetClient.md#purge)

  Purge all items from the dataset.

  The backend method for the `Dataset.purge` call.

  ***

  #### Returns None

### [**](#push_data)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_dataset_client.py#L116)push\_data

* **async **push\_data**(data): None

- Overrides [DatasetClient.push\_data](https://crawlee.dev/python/python/api/class/DatasetClient.md#push_data)

  Push data to the dataset.

  The backend method for the `Dataset.push_data` call.

  ***

  #### Parameters

  * ##### data: list\[Any] | dict\[str, Any]

  #### Returns None


---

# MemoryInfo<!-- -->

Information about system memory.

### Hierarchy

* [MemoryUsageInfo](https://crawlee.dev/python/python/api/class/MemoryUsageInfo.md)
  * *MemoryInfo*

## Index[**](#Index)

### Properties

* [**current\_size](https://crawlee.dev/python/python/api/class/MemoryInfo.md#current_size)
* [**model\_config](https://crawlee.dev/python/python/api/class/MemoryInfo.md#model_config)
* [**system\_wide\_used\_size](https://crawlee.dev/python/python/api/class/MemoryInfo.md#system_wide_used_size)
* [**total\_size](https://crawlee.dev/python/python/api/class/MemoryInfo.md#total_size)

## Properties<!-- -->[**](#Properties)

### [**](#current_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L64)current\_size

**current\_size: Annotated\[ ByteSize, PlainValidator(ByteSize.validate), PlainSerializer(lambda size: size.bytes), Field(alias='currentSize'), ]

Inherited from [MemoryUsageInfo.current\_size](https://crawlee.dev/python/python/api/class/MemoryUsageInfo.md#current_size)

Memory usage of the current Python process and its children.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L90)model\_config

**model\_config: Undefined

Overrides [MemoryUsageInfo.model\_config](https://crawlee.dev/python/python/api/class/MemoryUsageInfo.md#model_config)

### [**](#system_wide_used_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L97)system\_wide\_used\_size

**system\_wide\_used\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

Total memory used by all processes system-wide (including non-crawlee processes).

### [**](#total_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L92)total\_size

**total\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

Total memory available in the system.


---

# MemoryKeyValueStoreClient<!-- -->

Memory implementation of the key-value store client.

This client stores data in memory as Python dictionaries. No data is persisted between process runs, meaning all stored data is lost when the program terminates. This implementation is primarily useful for testing, development, and short-lived crawler operations where persistence is not required.

The memory implementation provides fast access to data but is limited by available memory and does not support data sharing across different processes.

### Hierarchy

* [KeyValueStoreClient](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md)
  * *MemoryKeyValueStoreClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#__init__)
* [**delete\_value](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#delete_value)
* [**drop](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#drop)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#get_metadata)
* [**get\_public\_url](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#get_public_url)
* [**get\_value](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#get_value)
* [**iterate\_keys](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#iterate_keys)
* [**open](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#purge)
* [**record\_exists](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#record_exists)
* [**set\_value](https://crawlee.dev/python/python/api/class/MemoryKeyValueStoreClient.md#set_value)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L31)\_\_init\_\_

* ****\_\_init\_\_**(\*, metadata): None

- Initialize a new instance.

  Preferably use the `MemoryKeyValueStoreClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlymetadata: [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

  #### Returns None

### [**](#delete_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L129)delete\_value

* **async **delete\_value**(\*, key): None

- Overrides [KeyValueStoreClient.delete\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#delete_value)

  Delete a value from the key-value store by its key.

  The backend method for the `KeyValueStore.delete_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns None

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L95)drop

* **async **drop**(): None

- Overrides [KeyValueStoreClient.drop](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#drop)

  Drop the whole key-value store and remove all its values.

  The backend method for the `KeyValueStore.drop` call.

  ***

  #### Returns None

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L46)get\_metadata

* **async **get\_metadata**(): [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

- Overrides [KeyValueStoreClient.get\_metadata](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_metadata)

  Get the metadata of the key-value store.

  ***

  #### Returns [KeyValueStoreMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadata.md)

### [**](#get_public_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L164)get\_public\_url

* **async **get\_public\_url**(\*, key): str

- Overrides [KeyValueStoreClient.get\_public\_url](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_public_url)

  Get the public URL for the given key.

  The backend method for the `KeyValueStore.get_public_url` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns str

### [**](#get_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L105)get\_value

* **async **get\_value**(\*, key): [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

- Overrides [KeyValueStoreClient.get\_value](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#get_value)

  Retrieve the given record from the key-value store.

  The backend method for the `KeyValueStore.get_value` call.

  ***

  #### Parameters

  * ##### keyword-onlykey: str

  #### Returns [KeyValueStoreRecord](https://crawlee.dev/python/python/api/class/KeyValueStoreRecord.md) | None

### [**](#iterate_keys)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L135)iterate\_keys

* **async **iterate\_keys**(\*, exclusive\_start\_key, limit): AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

- Overrides [KeyValueStoreClient.iterate\_keys](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#iterate_keys)

  Iterate over all the existing keys in the key-value store.

  The backend method for the `KeyValueStore.iterate_keys` call.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyexclusive\_start\_key: str | None = <!-- -->None
  * ##### optionalkeyword-onlylimit: int | None = <!-- -->None

  #### Returns AsyncIterator\[[KeyValueStoreRecordMetadata](https://crawlee.dev/python/python/api/class/KeyValueStoreRecordMetadata.md)]

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L50)open

* **async **open**(\*, id, name, alias): Self

- Open or create a new memory key-value store client.

  This method creates a new in-memory key-value store instance. Unlike persistent storage implementations, memory KVS don't check for existing stores with the same name or ID since all data exists only in memory and is lost when the process terminates.

  Alias does not have any effect on the memory storage client implementation, because unnamed storages are supported by default, since data are not persisted.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the key-value store. If not provided, a random ID will be generated.

  * ##### keyword-onlyname: str | None

    The name of the key-value store for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the key-value store for unnamed (run scope) storages.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L100)purge

* **async **purge**(): None

- Overrides [KeyValueStoreClient.purge](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md#purge)

  Purge all items from the key-value store.

  The backend method for the `KeyValueStore.purge` call.

  ***

  #### Returns None

### [**](#record_exists)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L168)record\_exists

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

### [**](#set_value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_key_value_store_client.py#L112)set\_value

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

# MemoryRequestQueueClient<!-- -->

Memory implementation of the request queue client.

No data is persisted between process runs, which means all requests are lost when the program terminates. This implementation is primarily useful for testing, development, and short-lived crawler runs where persistence is not required.

This client provides fast access to request data but is limited by available memory and does not support data sharing across different processes.

### Hierarchy

* [RequestQueueClient](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)
  * *MemoryRequestQueueClient*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#__init__)
* [**add\_batch\_of\_requests](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#add_batch_of_requests)
* [**drop](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#drop)
* [**fetch\_next\_request](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#fetch_next_request)
* [**get\_metadata](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#get_metadata)
* [**get\_request](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#get_request)
* [**is\_empty](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#is_empty)
* [**mark\_request\_as\_handled](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#mark_request_as_handled)
* [**open](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#open)
* [**purge](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#purge)
* [**reclaim\_request](https://crawlee.dev/python/python/api/class/MemoryRequestQueueClient.md#reclaim_request)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L34)\_\_init\_\_

* ****\_\_init\_\_**(\*, metadata): None

- Initialize a new instance.

  Preferably use the `MemoryRequestQueueClient.open` class method to create a new instance.

  ***

  #### Parameters

  * ##### keyword-onlymetadata: [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

  #### Returns None

### [**](#add_batch_of_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L141)add\_batch\_of\_requests

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

### [**](#drop)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L111)drop

* **async **drop**(): None

- Overrides [RequestQueueClient.drop](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#drop)

  Drop the whole request queue and remove all its values.

  The backend method for the `RequestQueue.drop` call.

  ***

  #### Returns None

### [**](#fetch_next_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L232)fetch\_next\_request

* **async **fetch\_next\_request**(): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.fetch\_next\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#fetch_next_request)

  Return the next request in the queue to be processed.

  Once you successfully finish processing of the request, you need to call `RequestQueue.mark_request_as_handled` to mark the request as handled in the queue. If there was some error in processing the request, call `RequestQueue.reclaim_request` instead, so that the queue will give the request to some other consumer in another call to the `fetch_next_request` method.

  Note that the `None` return value does not mean the queue processing finished, it means there are currently no pending requests. To check whether all requests in queue were finished, use `RequestQueue.is_finished` instead.

  ***

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The request or `None` if there are no more pending requests.

### [**](#get_metadata)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L58)get\_metadata

* **async **get\_metadata**(): [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

- Overrides [RequestQueueClient.get\_metadata](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_metadata)

  Get the metadata of the request queue.

  ***

  #### Returns [RequestQueueMetadata](https://crawlee.dev/python/python/api/class/RequestQueueMetadata.md)

### [**](#get_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L251)get\_request

* **async **get\_request**(unique\_key): [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

- Overrides [RequestQueueClient.get\_request](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#get_request)

  Retrieve a request from the queue.

  ***

  #### Parameters

  * ##### unique\_key: str

    Unique key of the request to retrieve.

  #### Returns [Request](https://crawlee.dev/python/python/api/class/Request.md) | None

  The retrieved request, or None, if it did not exist.

### [**](#is_empty)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L317)is\_empty

* **async **is\_empty**(): bool

- Overrides [RequestQueueClient.is\_empty](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#is_empty)

  Check if the queue is empty.

  ***

  #### Returns bool

  True if the queue is empty, False otherwise.

### [**](#mark_request_as_handled)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L256)mark\_request\_as\_handled

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

### [**](#open)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L62)open

* **async **open**(\*, id, name, alias): Self

- Open or create a new memory request queue client.

  This method creates a new in-memory request queue instance. Unlike persistent storage implementations, memory queues don't check for existing queues with the same name or ID since all data exists only in memory and is lost when the process terminates.

  Alias does not have any effect on the memory storage client implementation, because unnamed storages are supported by default, since data are not persisted.

  ***

  #### Parameters

  * ##### keyword-onlyid: str | None

    The ID of the request queue. If not provided, a random ID will be generated.

  * ##### keyword-onlyname: str | None

    The name of the request queue for named (global scope) storages.

  * ##### keyword-onlyalias: str | None

    The alias of the request queue for unnamed (run scope) storages.

  #### Returns Self

  An instance for the opened or created storage client.

### [**](#purge)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L126)purge

* **async **purge**(): None

- Overrides [RequestQueueClient.purge](https://crawlee.dev/python/python/api/class/RequestQueueClient.md#purge)

  Purge all items from the request queue.

  The backend method for the `RequestQueue.purge` call.

  ***

  #### Returns None

### [**](#reclaim_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_request_queue_client.py#L288)reclaim\_request

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

# MemorySnapshot<!-- -->

A snapshot of memory usage.

## Index[**](#Index)

### Properties

* [**created\_at](https://crawlee.dev/python/python/api/class/MemorySnapshot.md#created_at)
* [**current\_size](https://crawlee.dev/python/python/api/class/MemorySnapshot.md#current_size)
* [**is\_overloaded](https://crawlee.dev/python/python/api/class/MemorySnapshot.md#is_overloaded)
* [**max\_memory\_size](https://crawlee.dev/python/python/api/class/MemorySnapshot.md#max_memory_size)
* [**max\_used\_memory\_ratio](https://crawlee.dev/python/python/api/class/MemorySnapshot.md#max_used_memory_ratio)
* [**system\_wide\_memory\_size](https://crawlee.dev/python/python/api/class/MemorySnapshot.md#system_wide_memory_size)
* [**system\_wide\_used\_size](https://crawlee.dev/python/python/api/class/MemorySnapshot.md#system_wide_used_size)

## Properties<!-- -->[**](#Properties)

### [**](#created_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L111)created\_at

**created\_at: datetime

The time at which the system load information was measured.

### [**](#current_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L96)current\_size

**current\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

Memory usage of the current Python process and its children.

### [**](#is_overloaded)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L115)is\_overloaded

**is\_overloaded: bool

Indicate whether the memory is considered as overloaded.

### [**](#max_memory_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L102)max\_memory\_size

**max\_memory\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

The maximum memory that can be used by `AutoscaledPool`.

### [**](#max_used_memory_ratio)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L108)max\_used\_memory\_ratio

**max\_used\_memory\_ratio: float

The maximum acceptable ratio of `current_size` to `max_memory_size`.

### [**](#system_wide_memory_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L105)system\_wide\_memory\_size

**system\_wide\_memory\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md) | None

Total memory available in the whole system.

### [**](#system_wide_used_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_autoscaling/_types.py#L99)system\_wide\_used\_size

**system\_wide\_used\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md) | None

Memory usage of all processes, system-wide.


---

# MemoryStorageClient<!-- -->

Memory implementation of the storage client.

This storage client provides access to datasets, key-value stores, and request queues that store all data in memory using Python data structures (lists and dictionaries). No data is persisted between process runs, meaning all stored data is lost when the program terminates.

The memory implementation provides fast access to data but is limited by available memory and does not support data sharing across different processes. All storage operations happen entirely in memory with no disk operations.

The memory storage client is useful for testing and development environments, or short-lived crawler operations where persistence is not required.

### Hierarchy

* [StorageClient](https://crawlee.dev/python/python/api/class/StorageClient.md)
  * *MemoryStorageClient*

## Index[**](#Index)

### Methods

* [**create\_dataset\_client](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md#create_dataset_client)
* [**create\_kvs\_client](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md#create_kvs_client)
* [**create\_rq\_client](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md#create_rq_client)
* [**get\_rate\_limit\_errors](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md#get_rate_limit_errors)
* [**get\_storage\_client\_cache\_key](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md#get_storage_client_cache_key)

## Methods<!-- -->[**](#Methods)

### [**](#create_dataset_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_storage_client.py#L31)create\_dataset\_client

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

### [**](#create_kvs_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_storage_client.py#L45)create\_kvs\_client

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

### [**](#create_rq_client)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_memory/_storage_client.py#L59)create\_rq\_client

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

# MemoryUsageInfo<!-- -->

Information about the memory usage.

### Hierarchy

* *MemoryUsageInfo*
  * [MemoryInfo](https://crawlee.dev/python/python/api/class/MemoryInfo.md)

## Index[**](#Index)

### Properties

* [**current\_size](https://crawlee.dev/python/python/api/class/MemoryUsageInfo.md#current_size)
* [**model\_config](https://crawlee.dev/python/python/api/class/MemoryUsageInfo.md#model_config)

## Properties<!-- -->[**](#Properties)

### [**](#current_size)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L64)current\_size

**current\_size: [ByteSize](https://crawlee.dev/python/python/api/class/ByteSize.md)

Memory usage of the current Python process and its children.

### [**](#model_config)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/system.py#L62)model\_config

**model\_config: Undefined


---

# MetadataBufferDb<!-- -->

Base model for metadata update buffer tables.

### Hierarchy

* *MetadataBufferDb*

  * [KeyValueStoreMetadataBufferDb](https://crawlee.dev/python/python/api/class/KeyValueStoreMetadataBufferDb.md)
  * [DatasetMetadataBufferDb](https://crawlee.dev/python/python/api/class/DatasetMetadataBufferDb.md)
  * [RequestQueueMetadataBufferDb](https://crawlee.dev/python/python/api/class/RequestQueueMetadataBufferDb.md)

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#accessed_at)
* [**id](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#id)
* [**modified\_at](https://crawlee.dev/python/python/api/class/MetadataBufferDb.md#modified_at)

## Properties<!-- -->[**](#Properties)

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L286)accessed\_at

**accessed\_at: Mapped\[datetime]

New accessed\_at timestamp, if being updated.

### [**](#id)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L282)id

**id: Mapped\[int]

Auto-increment primary key for ordering.

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_db_models.py#L289)modified\_at

**modified\_at: Mapped\[datetime | None]

New modified\_at timestamp, if being updated.


---

# MetadataUpdateParams<!-- -->

Parameters for updating metadata.

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/MetadataUpdateParams.md#accessed_at)
* [**modified\_at](https://crawlee.dev/python/python/api/class/MetadataUpdateParams.md#modified_at)

## Properties<!-- -->[**](#Properties)

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L48)accessed\_at

**accessed\_at: NotRequired\[datetime]

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L49)modified\_at

**modified\_at: NotRequired\[datetime]


---

# MetadataUpdateParams<!-- -->

Parameters for updating metadata.

## Index[**](#Index)

### Properties

* [**accessed\_at](https://crawlee.dev/python/python/api/class/MetadataUpdateParams.md#accessed_at)
* [**modified\_at](https://crawlee.dev/python/python/api/class/MetadataUpdateParams.md#modified_at)

## Properties<!-- -->[**](#Properties)

### [**](#accessed_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L48)accessed\_at

**accessed\_at: NotRequired\[datetime]

### [**](#modified_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/storage_clients/_sql/_client_mixin.py#L49)modified\_at

**modified\_at: NotRequired\[datetime]


---

# NestedSitemap<!-- -->

## Index[**](#Index)

### Properties

* [**loc](https://crawlee.dev/python/python/api/class/NestedSitemap.md#loc)
* [**origin\_sitemap\_url](https://crawlee.dev/python/python/api/class/NestedSitemap.md#origin_sitemap_url)

## Properties<!-- -->[**](#Properties)

### [**](#loc)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L50)loc

**loc: str

### [**](#origin_sitemap_url)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L51)origin\_sitemap\_url

**origin\_sitemap\_url: str | None


---

# NoParser<!-- -->

A no-op parser that returns raw response content without any processing.

This is useful when you only need the raw response data and don't require HTML parsing, link extraction, or content selection functionality.

### Hierarchy

* [AbstractHttpParser](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md)
  * *NoParser*

## Index[**](#Index)

### Methods

* [**find\_links](https://crawlee.dev/python/python/api/class/NoParser.md#find_links)
* [**is\_blocked](https://crawlee.dev/python/python/api/class/NoParser.md#is_blocked)
* [**is\_matching\_selector](https://crawlee.dev/python/python/api/class/NoParser.md#is_matching_selector)
* [**parse](https://crawlee.dev/python/python/api/class/NoParser.md#parse)
* [**parse\_text](https://crawlee.dev/python/python/api/class/NoParser.md#parse_text)
* [**select](https://crawlee.dev/python/python/api/class/NoParser.md#select)

## Methods<!-- -->[**](#Methods)

### [**](#find_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_http/_http_parser.py#L46)find\_links

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

### [**](#is_blocked)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_http/_http_parser.py#L38)is\_blocked

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

### [**](#is_matching_selector)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_http/_http_parser.py#L42)is\_matching\_selector

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

### [**](#parse)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_http/_http_parser.py#L26)parse

* **async **parse**(response): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse)

  Parse HTTP response.

  ***

  #### Parameters

  * ##### response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

    HTTP response to be parsed.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed HTTP response.

### [**](#parse_text)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_http/_http_parser.py#L30)parse\_text

* **async **parse\_text**(text): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse\_text](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse_text)

  Parse text containing html.

  ***

  #### Parameters

  * ##### text: str

    String containing html.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed text.

### [**](#select)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_http/_http_parser.py#L34)select

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

# PageSnapshot<!-- -->

Snapshot of a crawled page.

## Index[**](#Index)

### Methods

* [**\_\_bool\_\_](https://crawlee.dev/python/python/api/class/PageSnapshot.md#__bool__)

### Properties

* [**html](https://crawlee.dev/python/python/api/class/PageSnapshot.md#html)
* [**screenshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md#screenshot)

## Methods<!-- -->[**](#Methods)

### [**](#__bool__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L603)\_\_bool\_\_

* ****\_\_bool\_\_**(): bool

- #### Returns bool

## Properties<!-- -->[**](#Properties)

### [**](#html)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L600)html

**html: str | None

HTML content of the page.

### [**](#screenshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L597)screenshot

**screenshot: [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes) | None

Screenshot of the page format.


---

# ParsedHttpCrawlingContext<!-- -->

The crawling context used by `AbstractHttpCrawler`.

It provides access to key objects as well as utility functions for handling crawling tasks.

### Hierarchy

* [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md)

  * *ParsedHttpCrawlingContext*

    * [AdaptivePlaywrightCrawlingContext](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md)
    * [BeautifulSoupCrawlingContext](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md)
    * [ParselCrawlingContext](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md)

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#create_modified_copy)
* [**from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#from_basic_crawling_context)
* [**from\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#from_http_crawling_context)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#add_requests)
* [**enqueue\_links](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#enqueue_links)
* [**extract\_links](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#extract_links)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#get_key_value_store)
* [**http\_response](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#http_response)
* [**log](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#log)
* [**parsed\_content](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#parsed_content)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#request)
* [**send\_request](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md#use_state)

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

- Initialize a new instance from an existing `HttpCrawlingContext`.

  ***

  #### Parameters

  * ##### context: [HttpCrawlingContext](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md)
  * ##### parsed\_content: [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)
  * ##### enqueue\_links: [EnqueueLinksFunction](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)
  * ##### extract\_links: [ExtractLinksFunction](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md)

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

### [**](#enqueue_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L41)enqueue\_links

**enqueue\_links: [EnqueueLinksFunction](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)

### [**](#extract_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L42)extract\_links

**extract\_links: [ExtractLinksFunction](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md)

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

# ParselCrawler<!-- -->

A web crawler for performing HTTP requests and parsing HTML/XML content.

The `ParselCrawler` builds on top of the `AbstractHttpCrawler`, which means it inherits all of its features. It specifies its own parser `ParselParser` which is used to parse `HttpResponse`. `ParselParser` uses following library for parsing: <https://pypi.org/project/parsel/>

The HTTP client-based crawlers are ideal for websites that do not require JavaScript execution. However, if you need to execute client-side JavaScript, consider using browser-based crawler like the `PlaywrightCrawler`.

### Usage

```
from crawlee.crawlers import ParselCrawler, ParselCrawlingContext

crawler = ParselCrawler()

# Define the default request handler, which will be called for every request.
@crawler.router.default_handler
async def request_handler(context: ParselCrawlingContext) -> None:
    context.log.info(f'Processing {context.request.url} ...')

    # Extract data from the page.
    data = {
        'url': context.request.url,
        'title': context.selector.css('title').get(),
    }

    # Push the extracted data to the default dataset.
    await context.push_data(data)

await crawler.run(['https://crawlee.dev/'])
```

### Hierarchy

* [AbstractHttpCrawler](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md)
  * *ParselCrawler*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/ParselCrawler.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/ParselCrawler.md#add_requests)
* [**create\_parsed\_http\_crawler\_class](https://crawlee.dev/python/python/api/class/ParselCrawler.md#create_parsed_http_crawler_class)
* [**error\_handler](https://crawlee.dev/python/python/api/class/ParselCrawler.md#error_handler)
* [**export\_data](https://crawlee.dev/python/python/api/class/ParselCrawler.md#export_data)
* [**failed\_request\_handler](https://crawlee.dev/python/python/api/class/ParselCrawler.md#failed_request_handler)
* [**get\_data](https://crawlee.dev/python/python/api/class/ParselCrawler.md#get_data)
* [**get\_dataset](https://crawlee.dev/python/python/api/class/ParselCrawler.md#get_dataset)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/ParselCrawler.md#get_key_value_store)
* [**get\_request\_manager](https://crawlee.dev/python/python/api/class/ParselCrawler.md#get_request_manager)
* [**on\_skipped\_request](https://crawlee.dev/python/python/api/class/ParselCrawler.md#on_skipped_request)
* [**post\_navigation\_hook](https://crawlee.dev/python/python/api/class/ParselCrawler.md#post_navigation_hook)
* [**pre\_navigation\_hook](https://crawlee.dev/python/python/api/class/ParselCrawler.md#pre_navigation_hook)
* [**run](https://crawlee.dev/python/python/api/class/ParselCrawler.md#run)
* [**stop](https://crawlee.dev/python/python/api/class/ParselCrawler.md#stop)
* [**use\_state](https://crawlee.dev/python/python/api/class/ParselCrawler.md#use_state)

### Properties

* [**log](https://crawlee.dev/python/python/api/class/ParselCrawler.md#log)
* [**router](https://crawlee.dev/python/python/api/class/ParselCrawler.md#router)
* [**statistics](https://crawlee.dev/python/python/api/class/ParselCrawler.md#statistics)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_crawler.py#L57)\_\_init\_\_

* ****\_\_init\_\_**(\*, navigation\_timeout, request\_handler, statistics, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, concurrency\_settings, request\_handler\_timeout, abort\_on\_error, configure\_logging, statistics\_log\_format, keep\_alive, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id): None

- Overrides [AbstractHttpCrawler.\_\_init\_\_](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

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

# ParselCrawlingContext<!-- -->

The crawling context used by the `ParselCrawler`.

It provides access to key objects as well as utility functions for handling crawling tasks.

### Hierarchy

* [ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)
  * *ParselCrawlingContext*

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#create_modified_copy)
* [**from\_basic\_crawling\_context](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#from_basic_crawling_context)
* [**from\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#from_http_crawling_context)
* [**from\_parsed\_http\_crawling\_context](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#from_parsed_http_crawling_context)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#get_snapshot)
* [**html\_to\_text](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#html_to_text)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#add_requests)
* [**enqueue\_links](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#enqueue_links)
* [**extract\_links](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#extract_links)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#get_key_value_store)
* [**http\_response](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#http_response)
* [**log](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#log)
* [**parsed\_content](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#parsed_content)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#request)
* [**selector](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#selector)
* [**send\_request](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md#use_state)

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

### [**](#from_parsed_http_crawling_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_crawling_context.py#L26)from\_parsed\_http\_crawling\_context

* ****from\_parsed\_http\_crawling\_context**(context): Self

- Create a new context from an existing `ParsedHttpCrawlingContext[Selector]`.

  ***

  #### Parameters

  * ##### context: [ParsedHttpCrawlingContext](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md)\[Selector]

  #### Returns Self

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_abstract_http/_http_crawling_context.py#L27)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Inherited from [HttpCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md#get_snapshot)

  Overrides [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

  Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

### [**](#html_to_text)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_crawling_context.py#L30)html\_to\_text

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

### [**](#selector)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_crawling_context.py#L21)selector

**selector: Selector

Convenience alias.

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

# ParselParser<!-- -->

Parser for parsing HTTP response using Parsel.

### Hierarchy

* [AbstractHttpParser](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md)
  * *ParselParser*

## Index[**](#Index)

### Methods

* [**find\_links](https://crawlee.dev/python/python/api/class/ParselParser.md#find_links)
* [**is\_blocked](https://crawlee.dev/python/python/api/class/ParselParser.md#is_blocked)
* [**is\_matching\_selector](https://crawlee.dev/python/python/api/class/ParselParser.md#is_matching_selector)
* [**parse](https://crawlee.dev/python/python/api/class/ParselParser.md#parse)
* [**parse\_text](https://crawlee.dev/python/python/api/class/ParselParser.md#parse_text)
* [**select](https://crawlee.dev/python/python/api/class/ParselParser.md#select)

## Methods<!-- -->[**](#Methods)

### [**](#find_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_parser.py#L40)find\_links

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

### [**](#is_matching_selector)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_parser.py#L36)is\_matching\_selector

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

### [**](#parse)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_parser.py#L23)parse

* **async **parse**(response): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse)

  Parse HTTP response.

  ***

  #### Parameters

  * ##### response: [HttpResponse](https://crawlee.dev/python/python/api/class/HttpResponse.md)

    HTTP response to be parsed.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed HTTP response.

### [**](#parse_text)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_parser.py#L28)parse\_text

* **async **parse\_text**(text): [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

- Overrides [AbstractHttpParser.parse\_text](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md#parse_text)

  Parse text containing html.

  ***

  #### Parameters

  * ##### text: str

    String containing html.

  #### Returns [TParseResult](https://crawlee.dev/python/python/api.md#TParseResult)

  Parsed text.

### [**](#select)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_parsel/_parsel_parser.py#L32)select

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

# ParseSitemapOptions<!-- -->

## Index[**](#Index)

### Properties

* [**emit\_nested\_sitemaps](https://crawlee.dev/python/python/api/class/ParseSitemapOptions.md#emit_nested_sitemaps)
* [**max\_depth](https://crawlee.dev/python/python/api/class/ParseSitemapOptions.md#max_depth)
* [**sitemap\_retries](https://crawlee.dev/python/python/api/class/ParseSitemapOptions.md#sitemap_retries)
* [**timeout](https://crawlee.dev/python/python/api/class/ParseSitemapOptions.md#timeout)

## Properties<!-- -->[**](#Properties)

### [**](#emit_nested_sitemaps)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L55)emit\_nested\_sitemaps

**emit\_nested\_sitemaps: bool

### [**](#max_depth)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L56)max\_depth

**max\_depth: int

### [**](#sitemap_retries)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L57)sitemap\_retries

**sitemap\_retries: int

### [**](#timeout)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_utils/sitemap.py#L58)timeout

**timeout: timedelta | None


---

# PatchedFingerprintGenerator<!-- -->

Browserforge `FingerprintGenerator` that contains patches not accepted in upstream repo.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/PatchedFingerprintGenerator.md#__init__)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_browserforge_adapter.py#L157)\_\_init\_\_

* ****\_\_init\_\_**(\*, screen, strict, mock\_webrtc, slim, header\_kwargs): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyscreen: Screen | None = <!-- -->None

    Screen constraints for the generated fingerprint.

  * ##### optionalkeyword-onlystrict: bool = <!-- -->False

    Whether to raise an exception if the constraints are too strict.

  * ##### optionalkeyword-onlymock\_webrtc: bool = <!-- -->False

    Whether to mock WebRTC when injecting the fingerprint.

  * ##### optionalkeyword-onlyslim: bool = <!-- -->False

    Disables performance-heavy evasions when injecting the fingerprint.

  * ##### header\_kwargs: Undefined

  #### Returns None


---

# PatchedHeaderGenerator<!-- -->

Browserforge `HeaderGenerator` that contains patches specific for our usage of the generator.

## Index[**](#Index)

### Methods

* [**generate](https://crawlee.dev/python/python/api/class/PatchedHeaderGenerator.md#generate)

## Methods<!-- -->[**](#Methods)

### [**](#generate)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/fingerprint_suite/_browserforge_adapter.py#L56)generate

* ****generate**(\*, browser, os, device, locale, http\_version, user\_agent, strict, request\_dependent\_headers): dict\[str, str]

- Generate HTTP headers based on the specified parameters.

  For detailed description of the original method see: `browserforge.headers.generator.HeaderGenerator.generate` This patched version of the method adds additional quality checks on the output of the original method. It tries to generate headers several times until they match the requirements.

  ***

  #### Parameters

  * ##### optionalkeyword-onlybrowser: Iterable\[str | Browser] | None = <!-- -->None
  * ##### optionalkeyword-onlyos: ListOrString | None = <!-- -->None
  * ##### optionalkeyword-onlydevice: ListOrString | None = <!-- -->None
  * ##### optionalkeyword-onlylocale: ListOrString | None = <!-- -->None
  * ##### optionalkeyword-onlyhttp\_version: Literal\[1, 2] | None = <!-- -->None
  * ##### optionalkeyword-onlyuser\_agent: ListOrString | None = <!-- -->None
  * ##### optionalkeyword-onlystrict: bool | None = <!-- -->None
  * ##### optionalkeyword-onlyrequest\_dependent\_headers: dict\[str, str] | None = <!-- -->None

  #### Returns dict\[str, str]

  A generated headers.


---

# PlaywrightBrowserController<!-- -->

Controller for managing Playwright browser instances and their pages.

It provides methods to control browser instances, manage their pages, and handle context-specific configurations. It enforces limits on the number of open pages and tracks their state.

### Hierarchy

* [BrowserController](https://crawlee.dev/python/python/api/class/BrowserController.md)
  * *PlaywrightBrowserController*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#__init__)
* [**close](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#close)
* [**new\_page](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#new_page)

### Properties

* [**AUTOMATION\_LIBRARY](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#AUTOMATION_LIBRARY)
* [**browser\_type](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#browser_type)
* [**has\_free\_capacity](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#has_free_capacity)
* [**idle\_time](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#idle_time)
* [**is\_browser\_connected](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#is_browser_connected)
* [**last\_page\_opened\_at](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#last_page_opened_at)
* [**pages](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#pages)
* [**pages\_count](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#pages_count)
* [**total\_opened\_pages](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md#total_opened_pages)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L57)\_\_init\_\_

* ****\_\_init\_\_**(browser, \*, max\_open\_pages\_per\_browser, use\_incognito\_pages, header\_generator, fingerprint\_generator): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### browser: Browser | [PlaywrightPersistentBrowser](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md)

    The browser instance to control.

  * ##### optionalkeyword-onlymax\_open\_pages\_per\_browser: int = <!-- -->20

    The maximum number of pages that can be open at the same time.

  * ##### optionalkeyword-onlyuse\_incognito\_pages: bool = <!-- -->False

    By default pages share the same browser context. If set to True each page uses its own context that is destroyed once the page is closed or crashes.

  * ##### optionalkeyword-onlyheader\_generator: [HeaderGenerator](https://crawlee.dev/python/python/api/class/HeaderGenerator.md) | None = <!-- -->\_DEFAULT\_HEADER\_GENERATOR

    An optional `HeaderGenerator` instance used to generate and manage HTTP headers for requests made by the browser. By default, a predefined header generator is used. Set to `None` to disable automatic header modifications.

  * ##### optionalkeyword-onlyfingerprint\_generator: [FingerprintGenerator](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md) | None = <!-- -->None

    An optional instance of implementation of `FingerprintGenerator` that is used to generate browser fingerprints together with consistent headers.

  #### Returns None

### [**](#close)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L207)close

* **async **close**(\*, force): None

- Overrides [BrowserController.close](https://crawlee.dev/python/python/api/class/BrowserController.md#close)

  Close the browser.

  ***

  #### Parameters

  * ##### optionalkeyword-onlyforce: bool = <!-- -->False

    Whether to force close all open pages before closing the browser.

  #### Returns None

### [**](#new_page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L153)new\_page

* **async **new\_page**(browser\_new\_context\_options, proxy\_info): Page

- Overrides [BrowserController.new\_page](https://crawlee.dev/python/python/api/class/BrowserController.md#new_page)

  Create a new page with the given context options.

  ***

  #### Parameters

  * ##### optionalbrowser\_new\_context\_options: Mapping\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>.

  * ##### optionalproxy\_info: [ProxyInfo](https://crawlee.dev/python/python/api/class/ProxyInfo.md) | None = <!-- -->None

    The proxy configuration to use for the new page.

  #### Returns Page

  Page: The newly created page.

## Properties<!-- -->[**](#Properties)

### [**](#AUTOMATION_LIBRARY)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L54)AUTOMATION\_LIBRARY

**AUTOMATION\_LIBRARY: str | None

Overrides [BrowserController.AUTOMATION\_LIBRARY](https://crawlee.dev/python/python/api/class/BrowserController.md#AUTOMATION_LIBRARY)

The name of the automation library that the controller is using.

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L149)browser\_type

**browser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)

Overrides [BrowserController.browser\_type](https://crawlee.dev/python/python/api/class/BrowserController.md#browser_type)

Return the type of the browser.

### [**](#has_free_capacity)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L139)has\_free\_capacity

**has\_free\_capacity: bool

Overrides [BrowserController.has\_free\_capacity](https://crawlee.dev/python/python/api/class/BrowserController.md#has_free_capacity)

Return if the browser has free capacity to open a new page.

### [**](#idle_time)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L134)idle\_time

**idle\_time: timedelta

Overrides [BrowserController.idle\_time](https://crawlee.dev/python/python/api/class/BrowserController.md#idle_time)

Return the idle time of the browser controller.

### [**](#is_browser_connected)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L144)is\_browser\_connected

**is\_browser\_connected: bool

Overrides [BrowserController.is\_browser\_connected](https://crawlee.dev/python/python/api/class/BrowserController.md#is_browser_connected)

Return if the browser is closed.

### [**](#last_page_opened_at)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L129)last\_page\_opened\_at

**last\_page\_opened\_at: datetime

Overrides [BrowserController.last\_page\_opened\_at](https://crawlee.dev/python/python/api/class/BrowserController.md#last_page_opened_at)

Return the time when the last page was opened.

### [**](#pages)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L114)pages

**pages: list\[Page]

Overrides [BrowserController.pages](https://crawlee.dev/python/python/api/class/BrowserController.md#pages)

Return the list of opened pages.

### [**](#pages_count)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L124)pages\_count

**pages\_count: int

Overrides [BrowserController.pages\_count](https://crawlee.dev/python/python/api/class/BrowserController.md#pages_count)

Return the number of currently open pages.

### [**](#total_opened_pages)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_controller.py#L119)total\_opened\_pages

**total\_opened\_pages: int

Overrides [BrowserController.total\_opened\_pages](https://crawlee.dev/python/python/api/class/BrowserController.md#total_opened_pages)

Return the total number of pages opened since the browser was launched.


---

# PlaywrightBrowserPlugin<!-- -->

A plugin for managing Playwright automation library.

It is a plugin designed to manage browser instances using the Playwright automation library. It acts as a factory for creating new browser instances and provides a unified interface for interacting with different browser types (chromium, firefox, webkit and chrome). This class integrates configuration options for browser launches (headless mode, executable paths, sandboxing, ...). It also manages browser contexts and the number of pages open within each browser instance, ensuring that resource limits are respected.

### Hierarchy

* [BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md)
  * *PlaywrightBrowserPlugin*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#__init__)
* [**new\_browser](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#new_browser)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#active)
* [**AUTOMATION\_LIBRARY](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#AUTOMATION_LIBRARY)
* [**browser\_launch\_options](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#browser_launch_options)
* [**browser\_new\_context\_options](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#browser_new_context_options)
* [**browser\_type](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#browser_type)
* [**max\_open\_pages\_per\_browser](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md#max_open_pages_per_browser)

## Methods<!-- -->[**](#Methods)

### [**](#__aenter__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L153)\_\_aenter\_\_

* **async **\_\_aenter\_\_**(): [BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md)

- Overrides [BrowserPlugin.\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#__aenter__)

  Enter the context manager and initialize the browser plugin.

  ***

  #### Returns [BrowserPlugin](https://crawlee.dev/python/python/api/class/BrowserPlugin.md)

### [**](#__aexit__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L162)\_\_aexit\_\_

* **async **\_\_aexit\_\_**(exc\_type, exc\_value, exc\_traceback): None

- Overrides [BrowserPlugin.\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#__aexit__)

  Exit the context manager and close the browser plugin.

  ***

  #### Parameters

  * ##### exc\_type: [type](https://crawlee.dev/python/python/api/class/SitemapSource.md#type)\[BaseException] | None
  * ##### exc\_value: BaseException | None
  * ##### exc\_traceback: TracebackType | None

  #### Returns None

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L44)\_\_init\_\_

* ****\_\_init\_\_**(\*, browser\_type, user\_data\_dir, browser\_launch\_options, browser\_new\_context\_options, max\_open\_pages\_per\_browser, use\_incognito\_pages, fingerprint\_generator): None

- Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlybrowser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType) = <!-- -->'chromium'

    The type of browser to launch:

    * 'chromium', 'firefox', 'webkit': Use Playwright-managed browsers
    * 'chrome': Use your locally installed Google Chrome browser. Requires Google Chrome to be installed on the system.

  * ##### optionalkeyword-onlyuser\_data\_dir: (str | Path) | None = <!-- -->None

    Path to a User Data Directory, which stores browser session data like cookies and local storage.

  * ##### optionalkeyword-onlybrowser\_launch\_options: dict\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser launch method. These options are provided directly to Playwright's `browser_type.launch` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch>.

  * ##### optionalkeyword-onlybrowser\_new\_context\_options: dict\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>.

  * ##### optionalkeyword-onlymax\_open\_pages\_per\_browser: int = <!-- -->20

    The maximum number of pages that can be opened in a single browser instance. Once reached, a new browser instance will be launched to handle the excess.

  * ##### optionalkeyword-onlyuse\_incognito\_pages: bool = <!-- -->False

    By default pages share the same browser context. If set to True each page uses its own context that is destroyed once the page is closed or crashes.

  * ##### optionalkeyword-onlyfingerprint\_generator: [FingerprintGenerator](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md) | None = <!-- -->None

    An optional instance of implementation of `FingerprintGenerator` that is used to generate browser fingerprints together with consistent headers.

  #### Returns None

### [**](#new_browser)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L177)new\_browser

* **async **new\_browser**(): [BrowserController](https://crawlee.dev/python/python/api/class/BrowserController.md)

- Overrides [BrowserPlugin.new\_browser](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#new_browser)

  Create a new browser instance.

  ***

  #### Returns [BrowserController](https://crawlee.dev/python/python/api/class/BrowserController.md)

  A new browser instance wrapped in a controller.

## Properties<!-- -->[**](#Properties)

### [**](#active)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L117)active

**active: bool

Overrides [BrowserPlugin.active](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#active)

Indicate whether the context is active.

### [**](#AUTOMATION_LIBRARY)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L42)AUTOMATION\_LIBRARY

**AUTOMATION\_LIBRARY: str | None

Overrides [BrowserPlugin.AUTOMATION\_LIBRARY](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#AUTOMATION_LIBRARY)

The name of the automation library that the plugin is managing.

### [**](#browser_launch_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L127)browser\_launch\_options

**browser\_launch\_options: Mapping\[str, Any]

Overrides [BrowserPlugin.browser\_launch\_options](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#browser_launch_options)

Return the options for the `browser.launch` method.

Keyword arguments to pass to the browser launch method. These options are provided directly to Playwright's `browser_type.launch` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch>.

### [**](#browser_new_context_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L138)browser\_new\_context\_options

**browser\_new\_context\_options: Mapping\[str, Any]

Overrides [BrowserPlugin.browser\_new\_context\_options](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#browser_new_context_options)

Return the options for the `browser.new_context` method.

Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>.

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L122)browser\_type

**browser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)

Overrides [BrowserPlugin.browser\_type](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#browser_type)

Return the browser type name.

### [**](#max_open_pages_per_browser)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser_plugin.py#L149)max\_open\_pages\_per\_browser

**max\_open\_pages\_per\_browser: int

Overrides [BrowserPlugin.max\_open\_pages\_per\_browser](https://crawlee.dev/python/python/api/class/BrowserPlugin.md#max_open_pages_per_browser)

Return the maximum number of pages that can be opened in a single browser.


---

# PlaywrightCookieParam<!-- -->

Cookie parameters in Playwright format with camelCase naming.

## Index[**](#Index)

### Properties

* [**domain](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#domain)
* [**expires](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#expires)
* [**httpOnly](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#httpOnly)
* [**name](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#name)
* [**partitionKey](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#partitionKey)
* [**path](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#path)
* [**sameSite](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#sameSite)
* [**secure](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#secure)
* [**value](https://crawlee.dev/python/python/api/class/PlaywrightCookieParam.md#value)

## Properties<!-- -->[**](#Properties)

### [**](#domain)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L50)domain

**domain: NotRequired\[str]

### [**](#expires)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L54)expires

**expires: NotRequired\[float]

### [**](#httpOnly)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L53)httpOnly

**httpOnly: NotRequired\[bool]

### [**](#name)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L48)name

**name: NotRequired\[str]

### [**](#partitionKey)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L56)partitionKey

**partitionKey: NotRequired\[str | None]

### [**](#path)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L51)path

**path: NotRequired\[str]

### [**](#sameSite)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L55)sameSite

**sameSite: NotRequired\[Literal\[Lax, None, Strict]]

### [**](#secure)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L52)secure

**secure: NotRequired\[bool]

### [**](#value)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/sessions/_cookies.py#L49)value

**value: NotRequired\[str]


---

# PlaywrightCrawler<!-- -->

A web crawler that leverages the `Playwright` browser automation library.

The `PlaywrightCrawler` builds on top of the `BasicCrawler`, which means it inherits all of its features. On top of that it provides a high level web crawling interface on top of the `Playwright` library. To be more specific, it uses the Crawlee's `BrowserPool` to manage the Playwright's browser instances and the pages they open. You can create your own `BrowserPool` instance and pass it to the `PlaywrightCrawler` constructor, or let the crawler create a new instance with the default settings.

This crawler is ideal for crawling websites that require JavaScript execution, as it uses real browsers to download web pages and extract data. For websites that do not require JavaScript, consider using one of the HTTP client-based crawlers, such as the `HttpCrawler`, `ParselCrawler`, or `BeautifulSoupCrawler`. They use raw HTTP requests, which means they are much faster.

### Usage

```
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext

crawler = PlaywrightCrawler()

# Define the default request handler, which will be called for every request.
@crawler.router.default_handler
async def request_handler(context: PlaywrightCrawlingContext) -> None:
    context.log.info(f'Processing {context.request.url} ...')

    # Extract data from the page.
    data = {
        'url': context.request.url,
        'title': await context.page.title(),
        'response': (await context.response.text())[:100],
    }

    # Push the extracted data to the default dataset.
    await context.push_data(data)

await crawler.run(['https://crawlee.dev/'])
```

### Hierarchy

* [BasicCrawler](https://crawlee.dev/python/python/api/class/BasicCrawler.md)
  * *PlaywrightCrawler*

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#__init__)
* [**add\_requests](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#add_requests)
* [**error\_handler](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#error_handler)
* [**export\_data](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#export_data)
* [**failed\_request\_handler](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#failed_request_handler)
* [**get\_data](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#get_data)
* [**get\_dataset](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#get_dataset)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#get_key_value_store)
* [**get\_request\_manager](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#get_request_manager)
* [**on\_skipped\_request](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#on_skipped_request)
* [**post\_navigation\_hook](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#post_navigation_hook)
* [**pre\_navigation\_hook](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#pre_navigation_hook)
* [**run](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#run)
* [**stop](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#stop)
* [**use\_state](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#use_state)

### Properties

* [**log](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#log)
* [**router](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#router)
* [**statistics](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#statistics)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L101)\_\_init\_\_

* ****\_\_init\_\_**(\*, browser\_pool, browser\_type, user\_data\_dir, browser\_launch\_options, browser\_new\_context\_options, goto\_options, fingerprint\_generator, headless, use\_incognito\_pages, navigation\_timeout, request\_handler, statistics, configuration, event\_manager, storage\_client, request\_manager, session\_pool, proxy\_configuration, http\_client, max\_request\_retries, max\_requests\_per\_crawl, max\_session\_rotations, max\_crawl\_depth, use\_session\_pool, retry\_on\_blocked, concurrency\_settings, request\_handler\_timeout, abort\_on\_error, configure\_logging, statistics\_log\_format, keep\_alive, additional\_http\_error\_status\_codes, ignore\_http\_error\_status\_codes, respect\_robots\_txt\_file, status\_message\_logging\_interval, status\_message\_callback, id): None

- Overrides [BasicCrawler.\_\_init\_\_](https://crawlee.dev/python/python/api/class/BasicCrawler.md#__init__)

  Initialize a new instance.

  ***

  #### Parameters

  * ##### optionalkeyword-onlybrowser\_pool: [BrowserPool](https://crawlee.dev/python/python/api/class/BrowserPool.md) | None = <!-- -->None

    A `BrowserPool` instance to be used for launching the browsers and getting pages.

  * ##### optionalkeyword-onlybrowser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType) | None = <!-- -->None

    The type of browser to launch:

    * 'chromium', 'firefox', 'webkit': Use Playwright-managed browsers
    * 'chrome': Use your locally installed Google Chrome browser. Requires Google Chrome to be installed on the system. This option should not be used if `browser_pool` is provided.

  * ##### optionalkeyword-onlyuser\_data\_dir: (str | Path) | None = <!-- -->None

    Path to a user data directory, which stores browser session data like cookies and local storage.

  * ##### optionalkeyword-onlybrowser\_launch\_options: Mapping\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser launch method. These options are provided directly to Playwright's `browser_type.launch` method. For more details, refer to the [Playwright documentation](https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch). This option should not be used if `browser_pool` is provided.

  * ##### optionalkeyword-onlybrowser\_new\_context\_options: Mapping\[str, Any] | None = <!-- -->None

    Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the [Playwright documentation](https://playwright.dev/python/docs/api/class-browser#browser-new-context). This option should not be used if `browser_pool` is provided.

  * ##### optionalkeyword-onlygoto\_options: [GotoOptions](https://crawlee.dev/python/python/api/class/GotoOptions.md) | None = <!-- -->None

    Additional options to pass to Playwright's `Page.goto()` method. The `timeout` option is not supported, use `navigation_timeout` instead.

  * ##### optionalkeyword-onlyfingerprint\_generator: ([FingerprintGenerator](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md) | None) | Literal\[default] = <!-- -->'default'

    An optional instance of implementation of `FingerprintGenerator` that is used to generate browser fingerprints together with consistent headers.

  * ##### optionalkeyword-onlyheadless: bool | None = <!-- -->None

    Whether to run the browser in headless mode. This option should not be used if `browser_pool` is provided.

  * ##### optionalkeyword-onlyuse\_incognito\_pages: bool | None = <!-- -->None

    By default pages share the same browser context. If set to True each page uses its own context that is destroyed once the page is closed or crashes. This option should not be used if `browser_pool` is provided.

  * ##### optionalkeyword-onlynavigation\_timeout: timedelta | None = <!-- -->None

    Timeout for navigation (the process between opening a Playwright page and calling the request handler)

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

### [**](#post_navigation_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L553)post\_navigation\_hook

* ****post\_navigation\_hook**(hook): None

- Register a hook to be called after each navigation.

  ***

  #### Parameters

  * ##### hook: Callable\[\[PlaywrightPostNavCrawlingContext], Awaitable\[None]]

    A coroutine function to be called after each navigation.

  #### Returns None

### [**](#pre_navigation_hook)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L545)pre\_navigation\_hook

* ****pre\_navigation\_hook**(hook): None

- Register a hook to be called before each navigation.

  ***

  #### Parameters

  * ##### hook: Callable\[\[PlaywrightPreNavCrawlingContext], Awaitable\[None]]

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

# PlaywrightCrawlerOptions<!-- -->

Arguments for the `AbstractHttpCrawler` constructor.

It is intended for typing forwarded `__init__` arguments in the subclasses.

### Hierarchy

* [\_PlaywrightCrawlerAdditionalOptions](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md)
* [BasicCrawlerOptions](https://crawlee.dev/python/python/api/class/BasicCrawlerOptions.md)
  * *PlaywrightCrawlerOptions*

## Index[**](#Index)

### Properties

* [**abort\_on\_error](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#abort_on_error)
* [**additional\_http\_error\_status\_codes](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#additional_http_error_status_codes)
* [**browser\_launch\_options](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#browser_launch_options)
* [**browser\_new\_context\_options](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#browser_new_context_options)
* [**browser\_pool](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#browser_pool)
* [**browser\_type](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#browser_type)
* [**concurrency\_settings](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#concurrency_settings)
* [**configuration](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#configuration)
* [**configure\_logging](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#configure_logging)
* [**event\_manager](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#event_manager)
* [**headless](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#headless)
* [**http\_client](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#http_client)
* [**id](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#id)
* [**ignore\_http\_error\_status\_codes](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#ignore_http_error_status_codes)
* [**keep\_alive](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#keep_alive)
* [**max\_crawl\_depth](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#max_crawl_depth)
* [**max\_request\_retries](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#max_request_retries)
* [**max\_requests\_per\_crawl](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#max_requests_per_crawl)
* [**max\_session\_rotations](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#max_session_rotations)
* [**proxy\_configuration](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#proxy_configuration)
* [**request\_handler](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#request_handler)
* [**request\_handler\_timeout](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#request_handler_timeout)
* [**request\_manager](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#request_manager)
* [**respect\_robots\_txt\_file](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#respect_robots_txt_file)
* [**retry\_on\_blocked](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#retry_on_blocked)
* [**session\_pool](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#session_pool)
* [**statistics](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#statistics)
* [**statistics\_log\_format](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#statistics_log_format)
* [**status\_message\_callback](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#status_message_callback)
* [**status\_message\_logging\_interval](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#status_message_logging_interval)
* [**storage\_client](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#storage_client)
* [**use\_session\_pool](https://crawlee.dev/python/python/api/class/PlaywrightCrawlerOptions.md#use_session_pool)

## Properties<!-- -->[**](#Properties)

### [**](#abort_on_error)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L175)abort\_on\_error

**abort\_on\_error: NotRequired\[bool]

Inherited from \_BasicCrawlerOptions.abort\_on\_error

If True, the crawler stops immediately when any request handler error occurs.

### [**](#additional_http_error_status_codes)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_basic/_basic_crawler.py#L189)additional\_http\_error\_status\_codes

**additional\_http\_error\_status\_codes: NotRequired\[Iterable\[int]]

Inherited from \_BasicCrawlerOptions.additional\_http\_error\_status\_codes

Additional HTTP status codes to treat as errors, triggering automatic retries when encountered.

### [**](#browser_launch_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L597)browser\_launch\_options

**browser\_launch\_options: NotRequired\[Mapping\[str, Any]]

Inherited from [\_PlaywrightCrawlerAdditionalOptions.browser\_launch\_options](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_launch_options)

Keyword arguments to pass to the browser launch method. These options are provided directly to Playwright's `browser_type.launch` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch>. This option should not be used if `browser_pool` is provided.

### [**](#browser_new_context_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L603)browser\_new\_context\_options

**browser\_new\_context\_options: NotRequired\[Mapping\[str, Any]]

Inherited from [\_PlaywrightCrawlerAdditionalOptions.browser\_new\_context\_options](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_new_context_options)

Keyword arguments to pass to the browser new context method. These options are provided directly to Playwright's `browser.new_context` method. For more details, refer to the Playwright documentation: <https://playwright.dev/python/docs/api/class-browser#browser-new-context>. This option should not be used if `browser_pool` is provided.

### [**](#browser_pool)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L588)browser\_pool

**browser\_pool: NotRequired\[BrowserPool]

Inherited from [\_PlaywrightCrawlerAdditionalOptions.browser\_pool](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_pool)

A `BrowserPool` instance to be used for launching the browsers and getting pages.

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L591)browser\_type

**browser\_type: NotRequired\[BrowserType]

Inherited from [\_PlaywrightCrawlerAdditionalOptions.browser\_type](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#browser_type)

The type of browser to launch:

* 'chromium', 'firefox', 'webkit': Use Playwright-managed browsers
* 'chrome': Use your locally installed Google Chrome browser. Requires Google Chrome to be installed on the system. This option should not be used if `browser_pool` is provided.

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

### [**](#headless)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawler.py#L609)headless

**headless: NotRequired\[bool]

Inherited from [\_PlaywrightCrawlerAdditionalOptions.headless](https://crawlee.dev/python/python/api/class/_PlaywrightCrawlerAdditionalOptions.md#headless)

Whether to run the browser in headless mode. This option should not be used if `browser_pool` is provided.

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

# PlaywrightCrawlingContext<!-- -->

The crawling context used by the `PlaywrightCrawler`.

It provides access to key objects as well as utility functions for handling crawling tasks.

### Hierarchy

* [PlaywrightPostNavCrawlingContext](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md)
  * *PlaywrightCrawlingContext*

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#create_modified_copy)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#add_requests)
* [**block\_requests](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#block_requests)
* [**enqueue\_links](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#enqueue_links)
* [**extract\_links](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#extract_links)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#get_key_value_store)
* [**goto\_options](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#goto_options)
* [**infinite\_scroll](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#infinite_scroll)
* [**log](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#log)
* [**page](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#page)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#request)
* [**response](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#response)
* [**send\_request](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md#use_state)

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

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L32)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Inherited from [PlaywrightPreNavCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#get_snapshot)

  Overrides [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

  Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

## Properties<!-- -->[**](#Properties)

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L652)add\_requests

**add\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md)

Inherited from [BasicCrawlingContext.add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#add_requests)

Add requests crawling context helper function.

### [**](#block_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L26)block\_requests

**block\_requests: [BlockRequestsFunction](https://crawlee.dev/python/python/api/class/BlockRequestsFunction.md)

Inherited from [PlaywrightPreNavCrawlingContext.block\_requests](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#block_requests)

Blocks network requests matching specified URL patterns.

### [**](#enqueue_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawling_context.py#L24)enqueue\_links

**enqueue\_links: [EnqueueLinksFunction](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)

The Playwright `EnqueueLinksFunction` implementation.

### [**](#extract_links)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawling_context.py#L27)extract\_links

**extract\_links: [ExtractLinksFunction](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md)

The Playwright `ExtractLinksFunction` implementation.

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L661)get\_key\_value\_store

**get\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md)

Inherited from [BasicCrawlingContext.get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_key_value_store)

Get key-value store crawling context helper function.

### [**](#goto_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L29)goto\_options

**goto\_options: [GotoOptions](https://crawlee.dev/python/python/api/class/GotoOptions.md)

Inherited from [PlaywrightPreNavCrawlingContext.goto\_options](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#goto_options)

Additional options to pass to Playwright's `Page.goto()` method. The `timeout` option is not supported.

### [**](#infinite_scroll)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_crawling_context.py#L30)infinite\_scroll

**infinite\_scroll: Callable\[\[], Awaitable\[None]]

A function to perform infinite scrolling on the page. This scrolls to the bottom, triggering the loading of additional content if present.

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L664)log

**log: logging.Logger

Inherited from [BasicCrawlingContext.log](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#log)

Logger instance.

### [**](#page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L23)page

**page: Page

Inherited from [PlaywrightPreNavCrawlingContext.page](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#page)

The Playwright `Page` object for the current page.

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

### [**](#response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_post_nav_crawling_context.py#L22)response

**response: Response

Inherited from [PlaywrightPostNavCrawlingContext.response](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#response)

The Playwright `Response` object containing the response details for the current URL.

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

# PlaywrightHttpClient<!-- -->

HTTP client based on the Playwright library.

This client uses the Playwright library to perform HTTP requests in crawlers (`BasicCrawler` subclasses) and to manage sessions, proxies, and error handling.

See the `HttpClient` class for more common information about HTTP clients.

Note: This class is pre-designated for use in `PlaywrightCrawler` only

### Hierarchy

* [HttpClient](https://crawlee.dev/python/python/api/class/HttpClient.md)
  * *PlaywrightHttpClient*

## Index[**](#Index)

### Methods

* [**\_\_aenter\_\_](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#__aenter__)
* [**\_\_aexit\_\_](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#__aexit__)
* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#__init__)
* [**cleanup](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#cleanup)
* [**crawl](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#crawl)
* [**send\_request](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#send_request)
* [**stream](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#stream)

### Properties

* [**active](https://crawlee.dev/python/python/api/class/PlaywrightHttpClient.md#active)

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

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_http_client.py#L50)\_\_init\_\_

* ****\_\_init\_\_**(): None

- Overrides [HttpClient.\_\_init\_\_](https://crawlee.dev/python/python/api/class/HttpClient.md#__init__)

  Initialize a new instance.

  ***

  #### Returns None

### [**](#cleanup)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_http_client.py#L115)cleanup

* **async **cleanup**(): None

- Overrides [HttpClient.cleanup](https://crawlee.dev/python/python/api/class/HttpClient.md#cleanup)

  Clean up resources used by the client.

  This method is called when the client is no longer needed and should be overridden in subclasses to perform any necessary cleanup such as closing connections, releasing file handles, or other resource deallocation.

  ***

  #### Returns None

### [**](#crawl)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_http_client.py#L55)crawl

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

### [**](#send_request)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_http_client.py#L67)send\_request

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

### [**](#stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_http_client.py#L102)stream

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

# PlaywrightHttpResponse<!-- -->

Wrapper class for playwright `Response` and `APIResponse` objects to implement `HttpResponse` protocol.

## Index[**](#Index)

### Methods

* [**from\_playwright\_response](https://crawlee.dev/python/python/api/class/PlaywrightHttpResponse.md#from_playwright_response)
* [**read](https://crawlee.dev/python/python/api/class/PlaywrightHttpResponse.md#read)
* [**read\_stream](https://crawlee.dev/python/python/api/class/PlaywrightHttpResponse.md#read_stream)

### Properties

* [**headers](https://crawlee.dev/python/python/api/class/PlaywrightHttpResponse.md#headers)
* [**http\_version](https://crawlee.dev/python/python/api/class/PlaywrightHttpResponse.md#http_version)
* [**status\_code](https://crawlee.dev/python/python/api/class/PlaywrightHttpResponse.md#status_code)

## Methods<!-- -->[**](#Methods)

### [**](#from_playwright_response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L55)from\_playwright\_response

* **async **from\_playwright\_response**(response, protocol): Self

- #### Parameters

  * ##### response: Response | APIResponse
  * ##### protocol: str

  #### Returns Self

### [**](#read)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L46)read

* **async **read**(): [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

- #### Returns [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

### [**](#read_stream)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L49)read\_stream

* **async **read\_stream**(): AsyncGenerator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes), None]

- #### Returns AsyncGenerator\[[bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes), None]

## Properties<!-- -->[**](#Properties)

### [**](#headers)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L43)headers

**headers: [HttpHeaders](https://crawlee.dev/python/python/api/class/HttpHeaders.md)

### [**](#http_version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L41)http\_version

**http\_version: str

### [**](#status_code)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_types.py#L42)status\_code

**status\_code: int


---

# PlaywrightPersistentBrowser<!-- -->

A wrapper for Playwright's `Browser` that operates with a persistent context.

It utilizes Playwright's persistent browser context feature, maintaining user data across sessions. While it follows the same interface as Playwright's `Browser` class, there is no abstract base class enforcing this. There is a limitation that only a single persistent context is allowed.

## Index[**](#Index)

### Methods

* [**\_\_init\_\_](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#__init__)
* [**close](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#close)
* [**is\_connected](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#is_connected)
* [**new\_browser\_cdp\_session](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#new_browser_cdp_session)
* [**new\_context](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#new_context)
* [**new\_page](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#new_page)
* [**start\_tracing](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#start_tracing)
* [**stop\_tracing](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#stop_tracing)

### Properties

* [**browser\_type](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#browser_type)
* [**contexts](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#contexts)
* [**version](https://crawlee.dev/python/python/api/class/PlaywrightPersistentBrowser.md#version)

## Methods<!-- -->[**](#Methods)

### [**](#__init__)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L32)\_\_init\_\_

* ****\_\_init\_\_**(browser\_type, user\_data\_dir, browser\_launch\_options): None

- #### Parameters

  * ##### browser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)
  * ##### user\_data\_dir: (str | Path) | None
  * ##### browser\_launch\_options: dict\[str, Any]

  #### Returns None

### [**](#close)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L85)close

* **async **close**(kwargs): None

- Close browser by closing its context.

  ***

  #### Parameters

  * ##### kwargs: Any

  #### Returns None

### [**](#is_connected)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L54)is\_connected

* ****is\_connected**(): bool

- #### Returns bool

### [**](#new_browser_cdp_session)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L103)new\_browser\_cdp\_session

* **async **new\_browser\_cdp\_session**(): CDPSession

- #### Returns CDPSession

### [**](#new_context)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L57)new\_context

* **async **new\_context**(context\_options): BrowserContext

- Create persistent context instead of regular one. Merge launch options with context options.

  ***

  #### Parameters

  * ##### context\_options: Any

  #### Returns BrowserContext

### [**](#new_page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L99)new\_page

* **async **new\_page**(kwargs): Page

- #### Parameters

  * ##### kwargs: Any

  #### Returns Page

### [**](#start_tracing)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L106)start\_tracing

* **async **start\_tracing**(kwargs): None

- #### Parameters

  * ##### kwargs: Any

  #### Returns None

### [**](#stop_tracing)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L109)stop\_tracing

* **async **stop\_tracing**(kwargs): [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

- #### Parameters

  * ##### kwargs: Any

  #### Returns [bytes](https://crawlee.dev/python/python/api/class/ByteSize.md#bytes)

## Properties<!-- -->[**](#Properties)

### [**](#browser_type)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L47)browser\_type

**browser\_type: [BrowserType](https://crawlee.dev/python/python/api.md#BrowserType)

### [**](#contexts)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L51)contexts

**contexts: list\[BrowserContext]

### [**](#version)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/browsers/_playwright_browser.py#L96)version

**version: str


---

# PlaywrightPostNavCrawlingContext<!-- -->

The post navigation crawling context used by the `PlaywrightCrawler`.

It provides access to the `Page` and `Response` objects, after the navigation to the URL is performed.

### Hierarchy

* [PlaywrightPreNavCrawlingContext](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md)
  * *PlaywrightPostNavCrawlingContext*
    * [PlaywrightCrawlingContext](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md)

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#create_modified_copy)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#add_requests)
* [**block\_requests](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#block_requests)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#get_key_value_store)
* [**goto\_options](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#goto_options)
* [**log](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#log)
* [**page](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#page)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#request)
* [**response](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#response)
* [**send\_request](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md#use_state)

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

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L32)get\_snapshot

* **async **get\_snapshot**(): [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

- Inherited from [PlaywrightPreNavCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#get_snapshot)

  Overrides [BasicCrawlingContext.get\_snapshot](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_snapshot)

  Get snapshot of crawled page.

  ***

  #### Returns [PageSnapshot](https://crawlee.dev/python/python/api/class/PageSnapshot.md)

## Properties<!-- -->[**](#Properties)

### [**](#add_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L652)add\_requests

**add\_requests: [AddRequestsFunction](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md)

Inherited from [BasicCrawlingContext.add\_requests](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#add_requests)

Add requests crawling context helper function.

### [**](#block_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L26)block\_requests

**block\_requests: [BlockRequestsFunction](https://crawlee.dev/python/python/api/class/BlockRequestsFunction.md)

Inherited from [PlaywrightPreNavCrawlingContext.block\_requests](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#block_requests)

Blocks network requests matching specified URL patterns.

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L661)get\_key\_value\_store

**get\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md)

Inherited from [BasicCrawlingContext.get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_key_value_store)

Get key-value store crawling context helper function.

### [**](#goto_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L29)goto\_options

**goto\_options: [GotoOptions](https://crawlee.dev/python/python/api/class/GotoOptions.md)

Inherited from [PlaywrightPreNavCrawlingContext.goto\_options](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#goto_options)

Additional options to pass to Playwright's `Page.goto()` method. The `timeout` option is not supported.

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L664)log

**log: logging.Logger

Inherited from [BasicCrawlingContext.log](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#log)

Logger instance.

### [**](#page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L23)page

**page: Page

Inherited from [PlaywrightPreNavCrawlingContext.page](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#page)

The Playwright `Page` object for the current page.

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

### [**](#response)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_post_nav_crawling_context.py#L22)response

**response: Response

The Playwright `Response` object containing the response details for the current URL.

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

# PlaywrightPreNavCrawlingContext<!-- -->

The pre navigation crawling context used by the `PlaywrightCrawler`.

It provides access to the `Page` object, before the navigation to the URL is performed.

### Hierarchy

* [BasicCrawlingContext](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md)
  * *PlaywrightPreNavCrawlingContext*
    * [PlaywrightPostNavCrawlingContext](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md)

## Index[**](#Index)

### Methods

* [**\_\_hash\_\_](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#__hash__)
* [**create\_modified\_copy](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#create_modified_copy)
* [**get\_snapshot](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#get_snapshot)

### Properties

* [**add\_requests](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#add_requests)
* [**block\_requests](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#block_requests)
* [**get\_key\_value\_store](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#get_key_value_store)
* [**goto\_options](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#goto_options)
* [**log](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#log)
* [**page](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#page)
* [**proxy\_info](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#proxy_info)
* [**push\_data](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#push_data)
* [**register\_deferred\_cleanup](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#register_deferred_cleanup)
* [**request](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#request)
* [**send\_request](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#send_request)
* [**session](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#session)
* [**use\_state](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#use_state)

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

### [**](#get_snapshot)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L32)get\_snapshot

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

### [**](#block_requests)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L26)block\_requests

**block\_requests: [BlockRequestsFunction](https://crawlee.dev/python/python/api/class/BlockRequestsFunction.md)

Blocks network requests matching specified URL patterns.

### [**](#get_key_value_store)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L661)get\_key\_value\_store

**get\_key\_value\_store: [GetKeyValueStoreFromRequestHandlerFunction](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFromRequestHandlerFunction.md)

Inherited from [BasicCrawlingContext.get\_key\_value\_store](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#get_key_value_store)

Get key-value store crawling context helper function.

### [**](#goto_options)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L29)goto\_options

**goto\_options: [GotoOptions](https://crawlee.dev/python/python/api/class/GotoOptions.md)

Additional options to pass to Playwright's `Page.goto()` method. The `timeout` option is not supported.

### [**](#log)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/_types.py#L664)log

**log: logging.Logger

Inherited from [BasicCrawlingContext.log](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md#log)

Logger instance.

### [**](#page)[**](https://github.com/apify/crawlee-python/blob/cc7b676c8a439641c98ee04dca6115e7348bb39b//src/crawlee/crawlers/_playwright/_playwright_pre_nav_crawling_context.py#L23)page

**page: Page

The Playwright `Page` object for the current page.

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

