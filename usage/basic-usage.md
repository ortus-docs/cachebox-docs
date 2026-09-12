# Basic Usage

Every CacheBox provider — whether it's the built-in `CacheBoxProvider`, a `LuceeProvider`, a `BoxLangProvider`, or your own custom implementation — shares the same core, cache-agnostic API defined by the `ICacheProvider` interface. This means you can swap out the underlying caching engine without changing a single line of your application code.

This page covers the essential methods you will use day to day: `get()`, `set()`, and most importantly, `getOrSet()`.

## Getting a Cache Reference

You always start by asking the `CacheFactory` for a named cache (or just grab the default one):

```javascript
// The default cache
cache = cacheBox.getDefaultCache();

// Or a specific named cache
cache = cacheBox.getCache( "myCache" );
```

## get() / set()

The most basic operations are `get()` and `set()`:

```javascript
// Store an object for 20 minutes, with a 10 minute idle (last access) timeout
cache.set( "myKey", myComplexObject, 20, 10 );

// Retrieve it
myComplexObject = cache.get( "myKey" );
```

If the key does not exist or has expired, `get()` returns an empty/null result. That means the typical caching pattern looks like this:

```javascript
data = cache.get( "myKey" );

if ( isNull( data ) ) {
    // produce the data
    data = myService.getExpensiveData();
    // cache it
    cache.set( "myKey", data );
}
```

That pattern is so common that CacheBox gives you a single method that does it all for you, atomically: `getOrSet()`.

## getOrSet() — The Get-Or-Produce-And-Set Pattern

{% hint style="success" %}
`getOrSet()` is the single most useful method on any cache provider. It collapses the classic "check cache, if missing produce and store" pattern into one thread-safe call.
{% endhint %}

### Method Signature

```javascript
any function getOrSet(
    required any objectKey,
    required any produce,
    any timeout           = "",
    any lastAccessTimeout = "",
    any extra             = {}
)
```

| Argument            | Type     | Required | Default | Description                                                                                                        |
| ------------------- | -------- | -------- | ------- | ------------------------------------------------------------------------------------------------------------------- |
| `objectKey`         | any      | true     |         | The cache key to look up (and store to, if missing)                                                                 |
| `produce`           | any      | true     |         | A closure/UDF (no arguments) that is invoked **only** if the key is not found in the cache. Its return value is cached and returned |
| `timeout`           | any      | false    | `""`    | The timeout to use when storing the produced object (provider specific, usually minutes)                            |
| `lastAccessTimeout` | any      | false    | `""`    | The idle/last-access timeout to use when storing the produced object (provider specific)                            |
| `extra`             | any      | false    | `{}`    | A struct of extra name-value pairs passed through to the provider's `set()` operation                               |

### How It Works

1. CacheBox first checks if `objectKey` already exists in the cache. If it does, that value is returned immediately — your `produce` closure is **never called**.
2. If it does not exist, CacheBox acquires an exclusive lock scoped to that specific cache + key (so concurrent requests for the same missing key don't all stampede your data source at once).
3. Inside the lock, it double-checks the cache (in case another thread just produced it while you were waiting for the lock).
4. If it's still missing, it executes your `produce` closure, takes the result, stores it via `set()` using the `timeout`/`lastAccessTimeout`/`extra` you provided, and returns it.

This effectively gives you **cache stampede protection** for free.

### Usage Example

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
cache = cacheBox.getDefaultCache()

// Get the object from cache, or produce, cache and return it if missing
data = cache.getOrSet( "topSellingProducts", () => {
    return productService.getTopSellers()
}, 30, 15 )
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
cache = cacheBox.getDefaultCache();

// Get the object from cache, or produce, cache and return it if missing
data = cache.getOrSet( "topSellingProducts", () => {
    return productService.getTopSellers();
}, 30, 15 );
```
{% endtab %}
{% endtabs %}

You can also pass extra provider-specific arguments via the `extra` struct:

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
data = cache.getOrSet(
    objectKey = "topSellingProducts",
    produce = () => productService.getTopSellers(),
    timeout = 30,
    lastAccessTimeout = 15,
    extra = { "priority" : "high" }
)
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
data = cache.getOrSet(
    objectKey = "topSellingProducts",
    produce = () => productService.getTopSellers(),
    timeout = 30,
    lastAccessTimeout = 15,
    extra = { "priority" : "high" }
);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
`getOrSet()` is implemented once in `AbstractCacheBoxProvider` and inherited (or delegated to via `super.getOrSet()`) by every shipped provider — `CacheBoxProvider`, `CFProvider`, `LuceeProvider`, and `BoxLangProvider` — so it behaves consistently no matter which caching engine you are using.
{% endhint %}

## Other Common Operations

For the full list of methods available on every provider (`lookup()`, `clear()`, `clearAll()`, bulk/multi operations, metadata retrieval, and more) see the [ICacheProvider](../for-the-geeks/cachebox-architecture/icacheprovider.md) reference.
