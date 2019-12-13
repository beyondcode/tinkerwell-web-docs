# Cache

- [Cache Usage](#cache-usage)
    - [Obtaining A Cache Instance](#obtaining-a-cache-instance)
    - [Retrieving Items From The Cache](#retrieving-items-from-the-cache)
    - [Storing Items In The Cache](#storing-items-in-the-cache)
    - [Removing Items From The Cache](#removing-items-from-the-cache)
    - [Atomic Locks](#atomic-locks)
    - [The Cache Helper](#the-cache-helper)


<a name="cache-usage"></a>
## Cache Usage

<a name="obtaining-a-cache-instance"></a>
### Obtaining A Cache Instance

The `Illuminate\Contracts\Cache\Factory` and `Illuminate\Contracts\Cache\Repository` [contracts](/docs/contracts) provide access to Laravel's cache services. The `Factory` contract provides access to all cache drivers defined for your application. The `Repository` contract is typically an implementation of the default cache driver for your application as specified by your `cache` configuration file.

However, you may also use the `Cache` facade, which is what we will use throughout this documentation. The `Cache` facade provides convenient, terse access to the underlying implementations of the Laravel cache contracts:

```try-code
{
    mode: "cli",
    cliCode: `$value = Cache::get('key');`
}
```

    <?php

    namespace App\Http\Controllers;

    use Illuminate\Support\Facades\Cache;

    class UserController extends Controller
    {
        /**
         * Show a list of all users of the application.
         *
         * @return Response
         */
        public function index()
        {
            $value = Cache::get('key');

            //
        }
    }

#### Accessing Multiple Cache Stores

Using the `Cache` facade, you may access various cache stores via the `store` method. The key passed to the `store` method should correspond to one of the stores listed in the `stores` configuration array in your `cache` configuration file:

    $value = Cache::store('file')->get('foo');

    Cache::store('redis')->put('bar', 'baz', 600); // 10 Minutes

<a name="retrieving-items-from-the-cache"></a>
### Retrieving Items From The Cache

The `get` method on the `Cache` facade is used to retrieve items from the cache. If the item does not exist in the cache, `null` will be returned. If you wish, you may pass a second argument to the `get` method specifying the default value you wish to be returned if the item doesn't exist:

```try-code
{
    mode: "cli",
    cliCode: `$value = Cache::get('key', 'default');`
}
```

    $value = Cache::get('key');

    $value = Cache::get('key', 'default');

You may even pass a `Closure` as the default value. The result of the `Closure` will be returned if the specified item does not exist in the cache. Passing a Closure allows you to defer the retrieval of default values from a database or other external service:

```try-code
{
    mode: "cli",
    cliCode: `$value = Cache::get('key', function () {
    return time();
});`
}
```

    $value = Cache::get('key', function () {
        return DB::table(...)->get();
    });

#### Checking For Item Existence

The `has` method may be used to determine if an item exists in the cache. This method will return `false` if the value is `null`:

```try-code
{
    mode: "cli",
    cliCode: `if (Cache::has('key')) {
    echo "Cache has the key";
}`
}
```

    if (Cache::has('key')) {
        //
    }

#### Incrementing / Decrementing Values

The `increment` and `decrement` methods may be used to adjust the value of integer items in the cache. Both of these methods accept an optional second argument indicating the amount by which to increment or decrement the item's value:

```try-code
{
    mode: "cli",
    cliCode: `Cache::increment('key');

echo Cache::get('key').PHP_EOL;

Cache::increment('key', 5);

echo Cache::get('key').PHP_EOL;

Cache::decrement('key');

echo Cache::get('key').PHP_EOL;

Cache::decrement('key', 5);

echo Cache::get('key').PHP_EOL;
`
}
```

    Cache::increment('key');
    Cache::increment('key', $amount);
    Cache::decrement('key');
    Cache::decrement('key', $amount);

#### Retrieve & Store

Sometimes you may wish to retrieve an item from the cache, but also store a default value if the requested item doesn't exist. For example, you may wish to retrieve all users from the cache or, if they don't exist, retrieve them from the database and add them to the cache. You may do this using the `Cache::remember` method:

```try-code
{
    mode: "cli",
    cliCode: `$value = Cache::remember('users', $seconds = 60, function () {
    return time();
});

echo PHP_EOL;

echo Cache::get('users');
`
}
```

    $value = Cache::remember('users', $seconds, function () {
        return DB::table('users')->get();
    });

If the item does not exist in the cache, the `Closure` passed to the `remember` method will be executed and its result will be placed in the cache.

You may use the `rememberForever` method to retrieve an item from the cache or store it forever:

    $value = Cache::rememberForever('users', function () {
        return DB::table('users')->get();
    });

#### Retrieve & Delete

If you need to retrieve an item from the cache and then delete the item, you may use the `pull` method. Like the `get` method, `null` will be returned if the item does not exist in the cache:

```try-code
{
    mode: "cli",
    cliCode: `Cache::put('key', 'value', $seconds = 60);

$value = Cache::pull('key');

var_dump($value);

Cache::get('key');
`
}
```

    $value = Cache::pull('key');

<a name="storing-items-in-the-cache"></a>
### Storing Items In The Cache

You may use the `put` method on the `Cache` facade to store items in the cache:

```try-code
{
    mode: "cli",
    cliCode: `Cache::put('key', 'value', 60);

Cache::get('key');
`
}
```

    Cache::put('key', 'value', $seconds);

If the storage time is not passed to the `put` method, the item will be stored indefinitely:

    Cache::put('key', 'value');

Instead of passing the number of seconds as an integer, you may also pass a `DateTime` instance representing the expiration time of the cached item:

    Cache::put('key', 'value', now()->addMinutes(10));

#### Store If Not Present

The `add` method will only add the item to the cache if it does not already exist in the cache store. The method will return `true` if the item is actually added to the cache. Otherwise, the method will return `false`:

    Cache::add('key', 'value', $seconds);

#### Storing Items Forever

The `forever` method may be used to store an item in the cache permanently. Since these items will not expire, they must be manually removed from the cache using the `forget` method:

    Cache::forever('key', 'value');


<a name="removing-items-from-the-cache"></a>
### Removing Items From The Cache

You may remove items from the cache using the `forget` method:

```try-code
{
    mode: "cli",
    cliCode: `Cache::put('key', 'value', 60);

Cache::forget('key');

Cache::get('key');
`
}
```

    Cache::forget('key');

You may also remove items by providing a zero or negative TTL:

    Cache::put('key', 'value', 0);

    Cache::put('key', 'value', -5);

You may clear the entire cache using the `flush` method:

```try-code
{
    mode: "cli",
    cliCode: `Cache::put('key', 'value', 60);

Cache::flush();

Cache::get('key');
`
}
```

    Cache::flush();

<a name="the-cache-helper"></a>
### The Cache Helper

In addition to using the `Cache` facade or [cache contract](/docs/contracts), you may also use the global `cache` function to retrieve and store data via the cache. When the `cache` function is called with a single, string argument, it will return the value of the given key:

```try-code
{
    mode: "cli",
    cliCode: `Cache::put('key', 'value', 60);

cache('key');
`
}
```

    $value = cache('key');

If you provide an array of key / value pairs and an expiration time to the function, it will store values in the cache for the specified duration:

```try-code
{
    mode: "cli",
    cliCode: `cache(['key' => 'value'], 60);

cache('key');
`
}
```

    cache(['key' => 'value'], $seconds);

    cache(['key' => 'value'], now()->addMinutes(10));

When the `cache` function is called without any arguments, it returns an instance of the `Illuminate\Contracts\Cache\Factory` implementation, allowing you to call other caching methods:

```try-code
{
    mode: "cli",
    cliCode: `cache()->remember('users', 60, function () {
    return time();
});

cache('users');
`
}
```

    cache()->remember('users', $seconds, function () {
        return DB::table('users')->get();
    });


<a name="events"></a>
## Events

To execute code on every cache operation, you may listen for the [events](/docs/events) fired by the cache. Typically, you should place these event listeners within your `EventServiceProvider`:

    /**
     * The event listener mappings for the application.
     *
     * @var array
     */
    protected $listen = [
        'Illuminate\Cache\Events\CacheHit' => [
            'App\Listeners\LogCacheHit',
        ],

        'Illuminate\Cache\Events\CacheMissed' => [
            'App\Listeners\LogCacheMissed',
        ],

        'Illuminate\Cache\Events\KeyForgotten' => [
            'App\Listeners\LogKeyForgotten',
        ],

        'Illuminate\Cache\Events\KeyWritten' => [
            'App\Listeners\LogKeyWritten',
        ],
    ];
