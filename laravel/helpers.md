# Helpers

- [Introduction](#introduction)
- [Available Methods](#available-methods)

<a name="introduction"></a>
## Introduction

Laravel includes a variety of global "helper" PHP functions. Many of these functions are used by the framework itself; however, you are free to use them in your own applications if you find them convenient.

<a name="available-methods"></a>
## Available Methods

### Arrays & Objects

<div class="collection-method-list" markdown="1">

[Arr::add](#method-array-add)
[Arr::collapse](#method-array-collapse)
[Arr::divide](#method-array-divide)
[Arr::dot](#method-array-dot)
[Arr::except](#method-array-except)
[Arr::first](#method-array-first)
[Arr::flatten](#method-array-flatten)
[Arr::forget](#method-array-forget)
[Arr::get](#method-array-get)
[Arr::has](#method-array-has)
[Arr::isAssoc](#method-array-isassoc)
[Arr::last](#method-array-last)
[Arr::only](#method-array-only)
[Arr::pluck](#method-array-pluck)
[Arr::prepend](#method-array-prepend)
[Arr::pull](#method-array-pull)
[Arr::random](#method-array-random)
[Arr::set](#method-array-set)
[Arr::sort](#method-array-sort)
[Arr::sortRecursive](#method-array-sort-recursive)
[Arr::where](#method-array-where)
[Arr::wrap](#method-array-wrap)
[data_fill](#method-data-fill)
[data_get](#method-data-get)
[data_set](#method-data-set)
[head](#method-head)
[last](#method-last)
</div>

### Paths

<div class="collection-method-list" markdown="1">

[app_path](#method-app-path)
[base_path](#method-base-path)
[config_path](#method-config-path)
[database_path](#method-database-path)
[mix](#method-mix)
[public_path](#method-public-path)
[resource_path](#method-resource-path)
[storage_path](#method-storage-path)

</div>

### Strings

<div class="collection-method-list" markdown="1">

[\__](#method-__)
[class_basename](#method-class-basename)
[e](#method-e)
[preg_replace_array](#method-preg-replace-array)
[Str::after](#method-str-after)
[Str::afterLast](#method-str-after-last)
[Str::before](#method-str-before)
[Str::beforeLast](#method-str-before-last)
[Str::camel](#method-camel-case)
[Str::contains](#method-str-contains)
[Str::containsAll](#method-str-contains-all)
[Str::endsWith](#method-ends-with)
[Str::finish](#method-str-finish)
[Str::is](#method-str-is)
[Str::kebab](#method-kebab-case)
[Str::limit](#method-str-limit)
[Str::orderedUuid](#method-str-ordered-uuid)
[Str::plural](#method-str-plural)
[Str::random](#method-str-random)
[Str::replaceArray](#method-str-replace-array)
[Str::replaceFirst](#method-str-replace-first)
[Str::replaceLast](#method-str-replace-last)
[Str::singular](#method-str-singular)
[Str::slug](#method-str-slug)
[Str::snake](#method-snake-case)
[Str::start](#method-str-start)
[Str::startsWith](#method-starts-with)
[Str::studly](#method-studly-case)
[Str::title](#method-title-case)
[Str::uuid](#method-str-uuid)
[Str::words](#method-str-words)
[trans](#method-trans)
[trans_choice](#method-trans-choice)

</div>

### URLs

<div class="collection-method-list" markdown="1">

[action](#method-action)
[asset](#method-asset)
[route](#method-route)
[secure_asset](#method-secure-asset)
[secure_url](#method-secure-url)
[url](#method-url)

</div>

### Miscellaneous

<div class="collection-method-list" markdown="1">

[abort](#method-abort)
[abort_if](#method-abort-if)
[abort_unless](#method-abort-unless)
[app](#method-app)
[auth](#method-auth)
[back](#method-back)
[bcrypt](#method-bcrypt)
[blank](#method-blank)
[broadcast](#method-broadcast)
[cache](#method-cache)
[class_uses_recursive](#method-class-uses-recursive)
[collect](#method-collect)
[config](#method-config)
[cookie](#method-cookie)
[csrf_field](#method-csrf-field)
[csrf_token](#method-csrf-token)
[dd](#method-dd)
[decrypt](#method-decrypt)
[dispatch](#method-dispatch)
[dispatch_now](#method-dispatch-now)
[dump](#method-dump)
[encrypt](#method-encrypt)
[env](#method-env)
[event](#method-event)
[factory](#method-factory)
[filled](#method-filled)
[info](#method-info)
[logger](#method-logger)
[method_field](#method-method-field)
[now](#method-now)
[old](#method-old)
[optional](#method-optional)
[policy](#method-policy)
[redirect](#method-redirect)
[report](#method-report)
[request](#method-request)
[rescue](#method-rescue)
[resolve](#method-resolve)
[response](#method-response)
[retry](#method-retry)
[session](#method-session)
[tap](#method-tap)
[throw_if](#method-throw-if)
[throw_unless](#method-throw-unless)
[today](#method-today)
[trait_uses_recursive](#method-trait-uses-recursive)
[transform](#method-transform)
[validator](#method-validator)
[value](#method-value)
[view](#method-view)
[with](#method-with)

</div>

<a name="method-listing"></a>
## Method Listing

<a name="arrays"></a>
## Arrays & Objects

<a name="method-array-add"></a>
#### `Arr::add()` 

The `Arr::add` method adds a given key / value pair to an array if the given key doesn't already exist in the array or is set to `null`:

```try-code
{
    mode: 'cli',
    cliCode: `$array = Arr::add(['name' => 'Desk', 'price' => null], 'price', 100);
`
}
```

    use Illuminate\Support\Arr;

    $array = Arr::add(['name' => 'Desk'], 'price', 100);

    // ['name' => 'Desk', 'price' => 100]

    $array = Arr::add(['name' => 'Desk', 'price' => null], 'price', 100);

    // ['name' => 'Desk', 'price' => 100]


<a name="method-array-collapse"></a>
#### `Arr::collapse()` 

The `Arr::collapse` method collapses an array of arrays into a single array:

```try-code
{
    mode: 'cli',
    cliCode: `
 $array = Arr::collapse([[1, 2, 3], [4, 5, 6], [7, 8, 9]]);
`
}
```

    use Illuminate\Support\Arr;

    $array = Arr::collapse([[1, 2, 3], [4, 5, 6], [7, 8, 9]]);

    // [1, 2, 3, 4, 5, 6, 7, 8, 9]

<a name="method-array-divide"></a>
#### `Arr::divide()` 

The `Arr::divide` method returns two arrays, one containing the keys, and the other containing the values of the given array:

```try-code
{
    mode: 'cli',
    cliCode: `
 [$keys, $values] = Arr::divide(['name' => 'Desk']);
`
}
```

    use Illuminate\Support\Arr;

    [$keys, $values] = Arr::divide(['name' => 'Desk']);

    // $keys: ['name']

    // $values: ['Desk']

<a name="method-array-dot"></a>
#### `Arr::dot()` 

The `Arr::dot` method flattens a multi-dimensional array into a single level array that uses "dot" notation to indicate depth:

```try-code
{
    mode: 'cli',
    cliCode: `
 $array = ['products' => ['desk' => ['price' => 100]]];

 $flattened = Arr::dot($array);
`
}
```

    use Illuminate\Support\Arr;

    $array = ['products' => ['desk' => ['price' => 100]]];

    $flattened = Arr::dot($array);

    // ['products.desk.price' => 100]

<a name="method-array-except"></a>
#### `Arr::except()` 

The `Arr::except` method removes the given key / value pairs from an array:

```try-code
{
    mode: 'cli',
    cliCode: `
 $array = ['name' => 'Desk', 'price' => 100];

 $filtered = Arr::except($array, ['price']);
`
}
```

    use Illuminate\Support\Arr;

    $array = ['name' => 'Desk', 'price' => 100];

    $filtered = Arr::except($array, ['price']);

    // ['name' => 'Desk']

<a name="method-array-first"></a>
#### `Arr::first()` 

The `Arr::first` method returns the first element of an array passing a given truth test:

```try-code
{
    mode: 'cli',
    cliCode: `
 $array = [100, 200, 300];

 $first = Arr::first($array, function ($value, $key) {
  return $value >= 150;
 });
`
}
```

    use Illuminate\Support\Arr;

    $array = [100, 200, 300];

    $first = Arr::first($array, function ($value, $key) {
        return $value >= 150;
    });

    // 200

A default value may also be passed as the third parameter to the method. This value will be returned if no value passes the truth test:

    use Illuminate\Support\Arr;

    $first = Arr::first($array, $callback, $default);

<a name="method-array-flatten"></a>
#### `Arr::flatten()` 

The `Arr::flatten` method flattens a multi-dimensional array into a single level array:

```try-code
{
    mode: 'cli',
    cliCode: `
 $array = ['name' => 'Joe', 'languages' => ['PHP', 'Ruby']];

 $flattened = Arr::flatten($array);
`
}
```

    use Illuminate\Support\Arr;

    $array = ['name' => 'Joe', 'languages' => ['PHP', 'Ruby']];

    $flattened = Arr::flatten($array);

    // ['Joe', 'PHP', 'Ruby']

<a name="method-array-forget"></a>
#### `Arr::forget()` 

The `Arr::forget` method removes a given key / value pair from a deeply nested array using "dot" notation:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['products' => ['desk' => ['price' => 100]]];

 Arr::forget($array, 'products.desk');
`
}
```

    use Illuminate\Support\Arr;

    $array = ['products' => ['desk' => ['price' => 100]]];

    Arr::forget($array, 'products.desk');

    // ['products' => []]

<a name="method-array-get"></a>
#### `Arr::get()` 

The `Arr::get` method retrieves a value from a deeply nested array using "dot" notation:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['products' => ['desk' => ['price' => 100]]];

 $price = Arr::get($array, 'products.desk.price');
`
}
```

    use Illuminate\Support\Arr;

    $array = ['products' => ['desk' => ['price' => 100]]];

    $price = Arr::get($array, 'products.desk.price');

    // 100

The `Arr::get` method also accepts a default value, which will be returned if the specific key is not found:

    use Illuminate\Support\Arr;

    $discount = Arr::get($array, 'products.desk.discount', 0);

    // 0

<a name="method-array-has"></a>
#### `Arr::has()` 

The `Arr::has` method checks whether a given item or items exists in an array using "dot" notation:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['product' => ['name' => 'Desk', 'price' => 100]];

 $contains = Arr::has($array, 'product.name');
`
}
```

    use Illuminate\Support\Arr;

    $array = ['product' => ['name' => 'Desk', 'price' => 100]];

    $contains = Arr::has($array, 'product.name');

    // true

    $contains = Arr::has($array, ['product.price', 'product.discount']);

    // false
 
<a name="method-array-isassoc"></a>
#### `Arr::isAssoc()` 

The `Arr::isAssoc` returns `true` if the given array is an associative array. An array is considered "associative" if it doesn't have sequential numerical keys beginning with zero:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $isAssoc = Arr::isAssoc(['product' => ['name' => 'Desk', 'price' => 100]]);
`
}
```

    use Illuminate\Support\Arr;

    $isAssoc = Arr::isAssoc(['product' => ['name' => 'Desk', 'price' => 100]]);

    // true

    $isAssoc = Arr::isAssoc([1, 2, 3]);

    // false

<a name="method-array-last"></a>
#### `Arr::last()` 

The `Arr::last` method returns the last element of an array passing a given truth test:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = [100, 200, 300, 110];

 $last = Arr::last($array, function ($value, $key) {
  return $value >= 150;
 });
`
}
```

    use Illuminate\Support\Arr;

    $array = [100, 200, 300, 110];

    $last = Arr::last($array, function ($value, $key) {
        return $value >= 150;
    });

    // 300

A default value may be passed as the third argument to the method. This value will be returned if no value passes the truth test:

    use Illuminate\Support\Arr;

    $last = Arr::last($array, $callback, $default);

<a name="method-array-only"></a>
#### `Arr::only()` 

The `Arr::only` method returns only the specified key / value pairs from the given array:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['name' => 'Desk', 'price' => 100, 'orders' => 10];

 $slice = Arr::only($array, ['name', 'price']);
`
}
```

    use Illuminate\Support\Arr;

    $array = ['name' => 'Desk', 'price' => 100, 'orders' => 10];

    $slice = Arr::only($array, ['name', 'price']);

    // ['name' => 'Desk', 'price' => 100]

<a name="method-array-pluck"></a>
#### `Arr::pluck()` 

The `Arr::pluck` method retrieves all of the values for a given key from an array:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = [
  ['developer' => ['id' => 1, 'name' => 'Taylor']],
  ['developer' => ['id' => 2, 'name' => 'Abigail']],
 ];

 $names = Arr::pluck($array, 'developer.name');
`
}
```

    use Illuminate\Support\Arr;

    $array = [
        ['developer' => ['id' => 1, 'name' => 'Taylor']],
        ['developer' => ['id' => 2, 'name' => 'Abigail']],
    ];

    $names = Arr::pluck($array, 'developer.name');

    // ['Taylor', 'Abigail']

You may also specify how you wish the resulting list to be keyed:

    use Illuminate\Support\Arr;

    $names = Arr::pluck($array, 'developer.name', 'developer.id');

    // [1 => 'Taylor', 2 => 'Abigail']

<a name="method-array-prepend"></a>
#### `Arr::prepend()` 

The `Arr::prepend` method will push an item onto the beginning of an array:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['one', 'two', 'three', 'four'];

 $array = Arr::prepend($array, 'zero');
`
}
```

    use Illuminate\Support\Arr;

    $array = ['one', 'two', 'three', 'four'];

    $array = Arr::prepend($array, 'zero');

    // ['zero', 'one', 'two', 'three', 'four']

If needed, you may specify the key that should be used for the value:

    use Illuminate\Support\Arr;

    $array = ['price' => 100];

    $array = Arr::prepend($array, 'Desk', 'name');

    // ['name' => 'Desk', 'price' => 100]

<a name="method-array-pull"></a>
#### `Arr::pull()` 

The `Arr::pull` method returns and removes a key / value pair from an array:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['name' => 'Desk', 'price' => 100];

 $name = Arr::pull($array, 'name');
`
}
```

    use Illuminate\Support\Arr;

    $array = ['name' => 'Desk', 'price' => 100];

    $name = Arr::pull($array, 'name');

    // $name: Desk

    // $array: ['price' => 100]

A default value may be passed as the third argument to the method. This value will be returned if the key doesn't exist:

    use Illuminate\Support\Arr;

    $value = Arr::pull($array, $key, $default);

<a name="method-array-random"></a>
#### `Arr::random()` 

The `Arr::random` method returns a random value from an array:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = [1, 2, 3, 4, 5];

 $random = Arr::random($array);
`
}
```

    use Illuminate\Support\Arr;

    $array = [1, 2, 3, 4, 5];

    $random = Arr::random($array);

    // 4 - (retrieved randomly)

You may also specify the number of items to return as an optional second argument. Note that providing this argument will return an array, even if only one item is desired:

    use Illuminate\Support\Arr;

    $items = Arr::random($array, 2);

    // [2, 5] - (retrieved randomly)

<a name="method-array-set"></a>
#### `Arr::set()` 

The `Arr::set` method sets a value within a deeply nested array using "dot" notation:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['products' => ['desk' => ['price' => 100]]];

 Arr::set($array, 'products.desk.price', 200);
`
}
```

    use Illuminate\Support\Arr;

    $array = ['products' => ['desk' => ['price' => 100]]];

    Arr::set($array, 'products.desk.price', 200);

    // ['products' => ['desk' => ['price' => 200]]]

<a name="method-array-sort"></a>
#### `Arr::sort()` 

The `Arr::sort` method sorts an array by its values:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = ['Desk', 'Table', 'Chair'];

 $sorted = Arr::sort($array);
`
}
```

    use Illuminate\Support\Arr;

    $array = ['Desk', 'Table', 'Chair'];

    $sorted = Arr::sort($array);

    // ['Chair', 'Desk', 'Table']

You may also sort the array by the results of the given Closure:

    use Illuminate\Support\Arr;

    $array = [
        ['name' => 'Desk'],
        ['name' => 'Table'],
        ['name' => 'Chair'],
    ];

    $sorted = array_values(Arr::sort($array, function ($value) {
        return $value['name'];
    }));

    /*
        [
            ['name' => 'Chair'],
            ['name' => 'Desk'],
            ['name' => 'Table'],
        ]
    */

<a name="method-array-sort-recursive"></a>
#### `Arr::sortRecursive()` 

The `Arr::sortRecursive` method recursively sorts an array using the `sort` function for numeric sub=arrays and `ksort` for associative sub-arrays:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = [
  ['Roman', 'Taylor', 'Li'],
  ['PHP', 'Ruby', 'JavaScript'],
  ['one' => 1, 'two' => 2, 'three' => 3],
 ];

 $sorted = Arr::sortRecursive($array);
`
}
```

    use Illuminate\Support\Arr;

    $array = [
        ['Roman', 'Taylor', 'Li'],
        ['PHP', 'Ruby', 'JavaScript'],
        ['one' => 1, 'two' => 2, 'three' => 3],
    ];

    $sorted = Arr::sortRecursive($array);

    /*
        [
            ['JavaScript', 'PHP', 'Ruby'],
            ['one' => 1, 'three' => 3, 'two' => 2],
            ['Li', 'Roman', 'Taylor'],
        ]
    */

<a name="method-array-where"></a>
#### `Arr::where()` 

The `Arr::where` method filters an array using the given Closure:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $array = [100, '200', 300, '400', 500];

 $filtered = Arr::where($array, function ($value, $key) {
  return is_string($value);
 });
`
}
```

    use Illuminate\Support\Arr;

    $array = [100, '200', 300, '400', 500];

    $filtered = Arr::where($array, function ($value, $key) {
        return is_string($value);
    });

    // [1 => '200', 3 => '400']

<a name="method-array-wrap"></a>
#### `Arr::wrap()` 

The `Arr::wrap` method wraps the given value in an array. If the given value is already an array it will not be changed:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Arr;

 $string = 'Laravel';

 $array = Arr::wrap($string);
`
}
```

    use Illuminate\Support\Arr;

    $string = 'Laravel';

    $array = Arr::wrap($string);

    // ['Laravel']

If the given value is null, an empty array will be returned:

    use Illuminate\Support\Arr;

    $nothing = null;

    $array = Arr::wrap($nothing);

    // []

<a name="method-data-fill"></a>
#### `data_fill()` 

The `data_fill` function sets a missing value within a nested array or object using "dot" notation:

```try-code
{
    mode: 'cli',
    cliCode: `$data = ['products' => ['desk' => ['price' => 100]]];

 data_fill($data, 'products.desk.price', 200);
`
}
```

    $data = ['products' => ['desk' => ['price' => 100]]];

    data_fill($data, 'products.desk.price', 200);

    // ['products' => ['desk' => ['price' => 100]]]

    data_fill($data, 'products.desk.discount', 10);

    // ['products' => ['desk' => ['price' => 100, 'discount' => 10]]]

This function also accepts asterisks as wildcards and will fill the target accordingly:

    $data = [
        'products' => [
            ['name' => 'Desk 1', 'price' => 100],
            ['name' => 'Desk 2'],
        ],
    ];

    data_fill($data, 'products.*.price', 200);

    /*
        [
            'products' => [
                ['name' => 'Desk 1', 'price' => 100],
                ['name' => 'Desk 2', 'price' => 200],
            ],
        ]
    */

<a name="method-data-get"></a>
#### `data_get()` 

The `data_get` function retrieves a value from a nested array or object using "dot" notation:

```try-code
{
    mode: 'cli',
    cliCode: `$data = ['products' => ['desk' => ['price' => 100]]];

 $price = data_get($data, 'products.desk.price');
`
}
```

    $data = ['products' => ['desk' => ['price' => 100]]];

    $price = data_get($data, 'products.desk.price');

    // 100

The `data_get` function also accepts a default value, which will be returned if the specified key is not found:

    $discount = data_get($data, 'products.desk.discount', 0);

    // 0

The function also accepts wildcards using asterisks, which may target any key of the array or object:

    $data = [
        'product-one' => ['name' => 'Desk 1', 'price' => 100],
        'product-two' => ['name' => 'Desk 2', 'price' => 150],
    ];

    data_get($data, '*.name');

    // ['Desk 1', 'Desk 2'];

<a name="method-data-set"></a>
#### `data_set()` 

The `data_set` function sets a value within a nested array or object using "dot" notation:

```try-code
{
    mode: 'cli',
    cliCode: `$data = ['products' => ['desk' => ['price' => 100]]];

 data_set($data, 'products.desk.price', 200);
`
}
```

    $data = ['products' => ['desk' => ['price' => 100]]];

    data_set($data, 'products.desk.price', 200);

    // ['products' => ['desk' => ['price' => 200]]]

This function also accepts wildcards and will set values on the target accordingly:

    $data = [
        'products' => [
            ['name' => 'Desk 1', 'price' => 100],
            ['name' => 'Desk 2', 'price' => 150],
        ],
    ];

    data_set($data, 'products.*.price', 200);

    /*
        [
            'products' => [
                ['name' => 'Desk 1', 'price' => 200],
                ['name' => 'Desk 2', 'price' => 200],
            ],
        ]
    */

By default, any existing values are overwritten. If you wish to only set a value if it doesn't exist, you may pass `false` as the fourth argument:

    $data = ['products' => ['desk' => ['price' => 100]]];

    data_set($data, 'products.desk.price', 200, false);

    // ['products' => ['desk' => ['price' => 100]]]

<a name="method-head"></a>
#### `head()` 

The `head` function returns the first element in the given array:

```try-code
{
    mode: 'cli',
    cliCode: `$array = [100, 200, 300];

 $first = head($array);
`
}
```

    $array = [100, 200, 300];

    $first = head($array);

    // 100

<a name="method-last"></a>
#### `last()` 

The `last` function returns the last element in the given array:

```try-code
{
    mode: 'cli',
    cliCode: `$array = [100, 200, 300];

 $last = last($array);
`
}
```

    $array = [100, 200, 300];

    $last = last($array);

    // 300

<a name="paths"></a>
## Paths

<a name="method-app-path"></a>
#### `app_path()` 

The `app_path` function returns the fully qualified path to the `app` directory. You may also use the `app_path` function to generate a fully qualified path to a file relative to the application directory:

```try-code
{
    mode: 'cli',
    cliCode: `$path = app_path();

 $path = app_path('Http/Controllers/Controller.php');
`
}
```

    $path = app_path();

    $path = app_path('Http/Controllers/Controller.php');

<a name="method-base-path"></a>
#### `base_path()` 

The `base_path` function returns the fully qualified path to the project root. You may also use the `base_path` function to generate a fully qualified path to a given file relative to the project root directory:

```try-code
{
    mode: 'cli',
    cliCode: `$path = base_path();

 $path = base_path('vendor/bin');
`
}
```

    $path = base_path();

    $path = base_path('vendor/bin');

<a name="method-config-path"></a>
#### `config_path()` 

The `config_path` function returns the fully qualified path to the `config` directory. You may also use the `config_path` function to generate a fully qualified path to a given file within the application's configuration directory:

```try-code
{
    mode: 'cli',
    cliCode: `$path = config_path();

 $path = config_path('app.php');
`
}
```

    $path = config_path();

    $path = config_path('app.php');

<a name="method-database-path"></a>
#### `database_path()` 

The `database_path` function returns the fully qualified path to the `database` directory. You may also use the `database_path` function to generate a fully qualified path to a given file within the database directory:

```try-code
{
    mode: 'cli',
    cliCode: `$path = database_path();

 $path = database_path('factories/UserFactory.php');
`
}
```

    $path = database_path();

    $path = database_path('factories/UserFactory.php');

<a name="method-mix"></a>
#### `mix()` 

The `mix` function returns the path to a [versioned Mix file](/docs/mix):

```try-code
{
    mode: 'cli',
    cliCode: `$path = mix('css/app.css');
`
}
```

    $path = mix('css/app.css');

<a name="method-public-path"></a>
#### `public_path()` 

The `public_path` function returns the fully qualified path to the `public` directory. You may also use the `public_path` function to generate a fully qualified path to a given file within the public directory:

```try-code
{
    mode: 'cli',
    cliCode: `$path = public_path();

 $path = public_path('css/app.css');
`
}
```

    $path = public_path();

    $path = public_path('css/app.css');

<a name="method-resource-path"></a>
#### `resource_path()` 

The `resource_path` function returns the fully qualified path to the `resources` directory. You may also use the `resource_path` function to generate a fully qualified path to a given file within the resources directory:

```try-code
{
    mode: 'cli',
    cliCode: `$path = resource_path();

 $path = resource_path('sass/app.scss');
`
}
```

    $path = resource_path();

    $path = resource_path('sass/app.scss');

<a name="method-storage-path"></a>
#### `storage_path()` 

The `storage_path` function returns the fully qualified path to the `storage` directory. You may also use the `storage_path` function to generate a fully qualified path to a given file within the storage directory:

```try-code
{
    mode: 'cli',
    cliCode: `$path = storage_path();

 $path = storage_path('app/file.txt');
`
}
```

    $path = storage_path();

    $path = storage_path('app/file.txt');

<a name="strings"></a>
## Strings

<a name="method-__"></a>
#### `__()` 

The `__` function translates the given translation string or translation key using your [localization files](/docs/localization):

```try-code
{
    mode: 'cli',
    cliCode: `echo __('Welcome to our application');

 echo __('messages.welcome');
`
}
```

    echo __('Welcome to our application');

    echo __('messages.welcome');

If the specified translation string or key does not exist, the `__` function will return the given value. So, using the example above, the `__` function would return `messages.welcome` if that translation key does not exist.

<a name="method-class-basename"></a>
#### `class_basename()` 

The `class_basename` function returns the class name of the given class with the class' namespace removed:

```try-code
{
    mode: 'cli',
    cliCode: `$class = class_basename('Foo\Bar\Baz');
`
}
```

    $class = class_basename('Foo\Bar\Baz');

    // Baz

<a name="method-e"></a>
#### `e()` 

The `e` function runs PHP's `htmlspecialchars` function with the `double_encode` option set to `true` by default:

```try-code
{
    mode: 'cli',
    cliCode: `echo e('<html>foo</html>');
`
}
```

    echo e('<html>foo</html>');

    // &lt;html&gt;foo&lt;/html&gt;

<a name="method-preg-replace-array"></a>
#### `preg_replace_array()` 

The `preg_replace_array` function replaces a given pattern in the string sequentially using an array:

```try-code
{
    mode: 'cli',
    cliCode: `$string = 'The event will take place between :start and :end';

 $replaced = preg_replace_array('/:[a-z_]+/', ['8:30', '9:00'], $string);
`
}
```

    $string = 'The event will take place between :start and :end';

    $replaced = preg_replace_array('/:[a-z_]+/', ['8:30', '9:00'], $string);

    // The event will take place between 8:30 and 9:00

<a name="method-str-after"></a>
#### `Str::after()` 

The `Str::after` method returns everything after the given value in a string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $slice = Str::after('This is my name', 'This is');
`
}
```

    use Illuminate\Support\Str;

    $slice = Str::after('This is my name', 'This is');

    // ' my name'

<a name="method-str-after-last"></a>
#### `Str::afterLast()` 

The `Str::afterLast` method returns everything after the last occurrence of the given value in a string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $slice = Str::afterLast('App\Http\Controllers\Controller', '\\');
`
}
```

    use Illuminate\Support\Str;

    $slice = Str::afterLast('App\Http\Controllers\Controller', '\\');

    // 'Controller'

<a name="method-str-before"></a>
#### `Str::before()` 

The `Str::before` method returns everything before the given value in a string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $slice = Str::before('This is my name', 'my name');
`
}
```

    use Illuminate\Support\Str;

    $slice = Str::before('This is my name', 'my name');

    // 'This is '

<a name="method-str-before-last"></a>
#### `Str::beforeLast()` 

The `Str::beforeLast` method returns everything before the last occurrence of the given value in a string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $slice = Str::beforeLast('This is my name', 'is');
`
}
```

    use Illuminate\Support\Str;

    $slice = Str::beforeLast('This is my name', 'is');

    // 'This '

<a name="method-camel-case"></a>
#### `Str::camel()` 

The `Str::camel` method converts the given string to `camelCase`:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $converted = Str::camel('foo_bar');
`
}
```

    use Illuminate\Support\Str;

    $converted = Str::camel('foo_bar');

    // fooBar

<a name="method-str-contains"></a>
#### `Str::contains()` 

The `Str::contains` method determines if the given string contains the given value (case sensitive):

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $contains = Str::contains('This is my name', 'my');
`
}
```

    use Illuminate\Support\Str;

    $contains = Str::contains('This is my name', 'my');

    // true

You may also pass an array of values to determine if the given string contains any of the values:

    use Illuminate\Support\Str;

    $contains = Str::contains('This is my name', ['my', 'foo']);

    // true

<a name="method-str-contains-all"></a>
#### `Str::containsAll()` 

The `Str::containsAll` method determines if the given string contains all array values:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $containsAll = Str::containsAll('This is my name', ['my', 'name']);
`
}
```

    use Illuminate\Support\Str;

    $containsAll = Str::containsAll('This is my name', ['my', 'name']);

    // true

<a name="method-ends-with"></a>
#### `Str::endsWith()` 

The `Str::endsWith` method determines if the given string ends with the given value:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $result = Str::endsWith('This is my name', 'name');
`
}
```

    use Illuminate\Support\Str;

    $result = Str::endsWith('This is my name', 'name');

    // true


You may also pass an array of values to determine if the given string ends with any of the given values:

    use Illuminate\Support\Str;

    $result = Str::endsWith('This is my name', ['name', 'foo']);

    // true
    
    $result = Str::endsWith('This is my name', ['this', 'foo']);
    
    // false

<a name="method-str-finish"></a>
#### `Str::finish()` 

The `Str::finish` method adds a single instance of the given value to a string if it does not already end with the value:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $adjusted = Str::finish('this/string', '/');
`
}
```

    use Illuminate\Support\Str;

    $adjusted = Str::finish('this/string', '/');

    // this/string/

    $adjusted = Str::finish('this/string/', '/');

    // this/string/

<a name="method-str-is"></a>
#### `Str::is()` 

The `Str::is` method determines if a given string matches a given pattern. Asterisks may be used to indicate wildcards:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $matches = Str::is('foo*', 'foobar');
`
}
```

    use Illuminate\Support\Str;

    $matches = Str::is('foo*', 'foobar');

    // true

    $matches = Str::is('baz*', 'foobar');

    // false

<a name="method-kebab-case"></a>
#### `Str::kebab()` 

The `Str::kebab` method converts the given string to `kebab-case`:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $converted = Str::kebab('fooBar');
`
}
```

    use Illuminate\Support\Str;

    $converted = Str::kebab('fooBar');

    // foo-bar

<a name="method-str-limit"></a>
#### `Str::limit()` 

The `Str::limit` method truncates the given string at the specified length:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $truncated = Str::limit('The quick brown fox jumps over the lazy dog', 20);
`
}
```

    use Illuminate\Support\Str;

    $truncated = Str::limit('The quick brown fox jumps over the lazy dog', 20);

    // The quick brown fox...

You may also pass a third argument to change the string that will be appended to the end:

    use Illuminate\Support\Str;

    $truncated = Str::limit('The quick brown fox jumps over the lazy dog', 20, ' (...)');

    // The quick brown fox (...)

<a name="method-str-ordered-uuid"></a>
#### `Str::orderedUuid()` 

The `Str::orderedUuid` method generates a "timestamp first" UUID that may be efficiently stored in an indexed database column:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 return (string) Str::orderedUuid();
`
}
```

    use Illuminate\Support\Str;

    return (string) Str::orderedUuid();

<a name="method-str-plural"></a>
#### `Str::plural()` 

The `Str::plural` method converts a string to its plural form. This function currently only supports the English language:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $plural = Str::plural('car');
`
}
```

    use Illuminate\Support\Str;

    $plural = Str::plural('car');

    // cars

    $plural = Str::plural('child');

    // children

You may provide an integer as a second argument to the function to retrieve the singular or plural form of the string:

    use Illuminate\Support\Str;

    $plural = Str::plural('child', 2);

    // children

    $plural = Str::plural('child', 1);

    // child

<a name="method-str-random"></a>
#### `Str::random()` 

The `Str::random` method generates a random string of the specified length. This function uses PHP's `random_bytes` function:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $random = Str::random(40);
`
}
```

    use Illuminate\Support\Str;

    $random = Str::random(40);

<a name="method-str-replace-array"></a>
#### `Str::replaceArray()` 

The `Str::replaceArray` method replaces a given value in the string sequentially using an array:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $string = 'The event will take place between ? and ?';

 $replaced = Str::replaceArray('?', ['8:30', '9:00'], $string);
`
}
```

    use Illuminate\Support\Str;

    $string = 'The event will take place between ? and ?';

    $replaced = Str::replaceArray('?', ['8:30', '9:00'], $string);

    // The event will take place between 8:30 and 9:00

<a name="method-str-replace-first"></a>
#### `Str::replaceFirst()` 

The `Str::replaceFirst` method replaces the first occurrence of a given value in a string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $replaced = Str::replaceFirst('the', 'a', 'the quick brown fox jumps over the lazy dog');
`
}
```

    use Illuminate\Support\Str;

    $replaced = Str::replaceFirst('the', 'a', 'the quick brown fox jumps over the lazy dog');

    // a quick brown fox jumps over the lazy dog

<a name="method-str-replace-last"></a>
#### `Str::replaceLast()` 

The `Str::replaceLast` method replaces the last occurrence of a given value in a string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

 $replaced = Str::replaceLast('the', 'a', 'the quick brown fox jumps over the lazy dog');
`
}
```

    use Illuminate\Support\Str;

    $replaced = Str::replaceLast('the', 'a', 'the quick brown fox jumps over the lazy dog');

    // the quick brown fox jumps over a lazy dog

<a name="method-str-singular"></a>
#### `Str::singular()` 

The `Str::singular` method converts a string to its singular form. This function currently only supports the English language:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::singular('cars');
`
}
```

    use Illuminate\Support\Str;

    $singular = Str::singular('cars');

    // car

    $singular = Str::singular('children');

    // child

<a name="method-str-slug"></a>
#### `Str::slug()` 

The `Str::slug` method generates a URL friendly "slug" from the given string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::slug('Laravel 5 Framework', '-');
`
}
```

    use Illuminate\Support\Str;

    $slug = Str::slug('Laravel 5 Framework', '-');

    // laravel-5-framework

<a name="method-snake-case"></a>
#### `Str::snake()` 

The `Str::snake` method converts the given string to `snake_case`:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::snake('fooBar');
`
}
```

    use Illuminate\Support\Str;

    $converted = Str::snake('fooBar');

    // foo_bar

<a name="method-str-start"></a>
#### `Str::start()` 

The `Str::start` method adds a single instance of the given value to a string if it does not already start with the value:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::start('this/string', '/');
`
}
```

    use Illuminate\Support\Str;

    $adjusted = Str::start('this/string', '/');

    // /this/string

    $adjusted = Str::start('/this/string', '/');

    // /this/string

<a name="method-starts-with"></a>
#### `Str::startsWith()` 

The `Str::startsWith` method determines if the given string begins with the given value:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::startsWith('This is my name', 'This');
`
}
```

    use Illuminate\Support\Str;

    $result = Str::startsWith('This is my name', 'This');

    // true

<a name="method-studly-case"></a>
#### `Str::studly()` 

The `Str::studly` method converts the given string to `StudlyCase`:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::studly('foo_bar');
`
}
```

    use Illuminate\Support\Str;

    $converted = Str::studly('foo_bar');

    // FooBar

<a name="method-title-case"></a>
#### `Str::title()` 

The `Str::title` method converts the given string to `Title Case`:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::title('a nice title uses the correct case');
`
}
```

    use Illuminate\Support\Str;

    $converted = Str::title('a nice title uses the correct case');

    // A Nice Title Uses The Correct Case

<a name="method-str-uuid"></a>
#### `Str::uuid()` 

The `Str::uuid` method generates a UUID (version 4):

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

(string) Str::uuid();
`
}
```

    use Illuminate\Support\Str;

    return (string) Str::uuid();

<a name="method-str-words"></a>
#### `Str::words()` 

The `Str::words` method limits the number of words in a string:

```try-code
{
    mode: 'cli',
    cliCode: `use Illuminate\Support\Str;

Str::words('Perfectly balanced, as all things should be.', 3, ' >>>');
`
}
```

    use Illuminate\Support\Str;

    return Str::words('Perfectly balanced, as all things should be.', 3, ' >>>');
    
    // Perfectly balanced, as >>>

<a name="method-trans"></a>
#### `trans()` 

The `trans` function translates the given translation key using your [localization files](/docs/localization):

```try-code
{
    mode: 'cli',
    cliCode: `echo trans('messages.welcome');
`
}
```

    echo trans('messages.welcome');

If the specified translation key does not exist, the `trans` function will return the given key. So, using the example above, the `trans` function would return `messages.welcome` if the translation key does not exist.

<a name="method-trans-choice"></a>
#### `trans_choice()` 

The `trans_choice` function translates the given translation key with inflection:

```try-code
{
    mode: 'cli',
    cliCode: `echo trans_choice('messages.notifications', $unreadCount);
`
}
```

    echo trans_choice('messages.notifications', $unreadCount);

If the specified translation key does not exist, the `trans_choice` function will return the given key. So, using the example above, the `trans_choice` function would return `messages.notifications` if the translation key does not exist.

<a name="urls"></a>
## URLs

<a name="method-action"></a>
#### `action()` 

The `action` function generates a URL for the given controller action. You do not need to pass the full namespace of the controller. Instead, pass the controller class name relative to the `App\Http\Controllers` namespace:

```try-code
{
    mode: 'cli',
    cliCode: `$url = action('HomeController@index');

 $url = action([HomeController::class, 'index']);
`
}
```

    $url = action('HomeController@index');

    $url = action([HomeController::class, 'index']);

If the method accepts route parameters, you may pass them as the second argument to the method:

    $url = action('UserController@profile', ['id' => 1]);

<a name="method-asset"></a>
#### `asset()` 

The `asset` function generates a URL for an asset using the current scheme of the request (HTTP or HTTPS):

```try-code
{
    mode: 'cli',
    cliCode: `$url = asset('img/photo.jpg');
`
}
```

    $url = asset('img/photo.jpg');

You can configure the asset URL host by setting the `ASSET_URL` variable in your `.env` file. This can be useful if you host your assets on an external service like Amazon S3:

    // ASSET_URL=http://example.com/assets

    $url = asset('img/photo.jpg'); // http://example.com/assets/img/photo.jpg

<a name="method-route"></a>
#### `route()` 

The `route` function generates a URL for the given named route:

    $url = route('routeName');

If the route accepts parameters, you may pass them as the second argument to the method:

    $url = route('routeName', ['id' => 1]);

By default, the `route` function generates an absolute URL. If you wish to generate a relative URL, you may pass `false` as the third argument:

    $url = route('routeName', ['id' => 1], false);

<a name="method-secure-asset"></a>
#### `secure_asset()` 

The `secure_asset` function generates a URL for an asset using HTTPS:

```try-code
{
    mode: 'cli',
    cliCode: `$url = secure_asset('img/photo.jpg');
`
}
```

    $url = secure_asset('img/photo.jpg');

<a name="method-secure-url"></a>
#### `secure_url()` 

The `secure_url` function generates a fully qualified HTTPS URL to the given path:

```try-code
{
    mode: 'cli',
    cliCode: `$url = secure_url('user/profile');

 $url = secure_url('user/profile', [1]);
`
}
```

    $url = secure_url('user/profile');

    $url = secure_url('user/profile', [1]);

<a name="method-url"></a>
#### `url()` 

The `url` function generates a fully qualified URL to the given path:

```try-code
{
    mode: 'cli',
    cliCode: `$url = url('user/profile');

 $url = url('user/profile', [1]);
`
}
```

    $url = url('user/profile');

    $url = url('user/profile', [1]);

If no path is provided, a `Illuminate\Routing\UrlGenerator` instance is returned:

    $current = url()->current();

    $full = url()->full();

    $previous = url()->previous();

<a name="miscellaneous"></a>
## Miscellaneous

<a name="method-abort"></a>
#### `abort()` 

The `abort` function throws [an HTTP exception](/docs/errors#http-exceptions) which will be rendered by the [exception handler](/docs/errors#the-exception-handler):

```try-code
{
    mode: 'cli',
    cliCode: `abort(403);
`
}
```

    abort(403);

You may also provide the exception's response text and custom response headers:

    abort(403, 'Unauthorized.', $headers);

<a name="method-abort-if"></a>
#### `abort_if()` 

The `abort_if` function throws an HTTP exception if a given boolean expression evaluates to `true`:

```try-code
{
    mode: 'cli',
    cliCode: `abort_if(! Auth::user()->isAdmin(), 403);
`
}
```

    abort_if(! Auth::user()->isAdmin(), 403);

Like the `abort` method, you may also provide the exception's response text as the third argument and an array of custom response headers as the fourth argument.

<a name="method-abort-unless"></a>
#### `abort_unless()` 

The `abort_unless` function throws an HTTP exception if a given boolean expression evaluates to `false`:

```try-code
{
    mode: 'cli',
    cliCode: `abort_unless(Auth::user()->isAdmin(), 403);
`
}
```

    abort_unless(Auth::user()->isAdmin(), 403);

Like the `abort` method, you may also provide the exception's response text as the third argument and an array of custom response headers as the fourth argument.

<a name="method-app"></a>
#### `app()` 

The `app` function returns the [service container](/docs/container) instance:

    $container = app();

You may pass a class or interface name to resolve it from the container:

    $api = app('HelpSpot\API');

<a name="method-auth"></a>
#### `auth()` 

The `auth` function returns an [authenticator](/docs/authentication) instance. You may use it instead of the `Auth` facade for convenience:

```try-code
{
    mode: 'cli',
    cliCode: `$user = auth()->user();
`
}
```

    $user = auth()->user();

If needed, you may specify which guard instance you would like to access:

    $user = auth('admin')->user();

<a name="method-back"></a>
#### `back()` 

The `back` function generates a [redirect HTTP response](/docs/responses#redirects) to the user's previous location:

    return back($status = 302, $headers = [], $fallback = false);

    return back();

<a name="method-bcrypt"></a>
#### `bcrypt()` 

The `bcrypt` function [hashes](/docs/hashing) the given value using Bcrypt. You may use it as an alternative to the `Hash` facade:


    $password = bcrypt('my-secret-password');

<a name="method-blank"></a>
#### `blank()` 

The `blank` function returns whether the given value is "blank":

```try-code
{
    mode: 'cli',
    cliCode: `blank(collect());
`
}
```

    blank('');
    blank('   ');
    blank(null);
    blank(collect());

    // true

    blank(0);
    blank(true);
    blank(false);

    // false

For the inverse of `blank`, see the [`filled`](#method-filled) method.

<a name="method-broadcast"></a>
#### `broadcast()` 

The `broadcast` function [broadcasts](/docs/broadcasting) the given [event](/docs/events) to its listeners:

    broadcast(new UserRegistered($user));

<a name="method-cache"></a>
#### `cache()` 

The `cache` function may be used to get values from the [cache](/docs/cache). If the given key does not exist in the cache, an optional default value will be returned:

```try-code
{
    mode: 'cli',
    cliCode: `cache('key', 'default');
`
}
```

    $value = cache('key');

    $value = cache('key', 'default');

You may add items to the cache by passing an array of key / value pairs to the function. You should also pass the number of seconds or duration the cached value should be considered valid:

    cache(['key' => 'value'], 300);

    cache(['key' => 'value'], now()->addSeconds(10));

<a name="method-class-uses-recursive"></a>
#### `class_uses_recursive()` 

The `class_uses_recursive` function returns all traits used by a class, including traits used by all of its parent classes:

```try-code
{
    mode: 'cli',
    cliCode: `$traits = class_uses_recursive(App\User::class);
`
}
```

    $traits = class_uses_recursive(App\User::class);

<a name="method-collect"></a>
#### `collect()` 

The `collect` function creates a [collection](/docs/collections) instance from the given value:

```try-code
{
    mode: 'cli',
    cliCode: `collect(['taylor', 'abigail']);
`
}
```

    $collection = collect(['taylor', 'abigail']);

<a name="method-config"></a>
#### `config()` 

The `config` function gets the value of a [configuration](/docs/configuration) variable. The configuration values may be accessed using "dot" syntax, which includes the name of the file and the option you wish to access. A default value may be specified and is returned if the configuration option does not exist:

```try-code
{
    mode: 'cli',
    cliCode: `$value = config('app.timezone');

config('app.timezone', $default);
`
}
```

    $value = config('app.timezone');

    $value = config('app.timezone', $default);

You may set configuration variables at runtime by passing an array of key / value pairs:

    config(['app.debug' => true]);

<a name="method-cookie"></a>
#### `cookie()` 

The `cookie` function creates a new [cookie](/docs/requests#cookies) instance:

```try-code
{
    mode: 'cli',
    cliCode: `cookie('name', 'value', $minutes);
`
}
```

    $cookie = cookie('name', 'value', $minutes);

<a name="method-csrf-field"></a>
#### `csrf_field()` 

The `csrf_field` function generates an HTML `hidden` input field containing the value of the CSRF token. For example, using [Blade syntax](/docs/blade):

    {{ csrf_field() }}

<a name="method-csrf-token"></a>
#### `csrf_token()` 

The `csrf_token` function retrieves the value of the current CSRF token:

```try-code
{
    mode: 'cli',
    cliCode: `csrf_token();
`
}
```

    $token = csrf_token();

<a name="method-dd"></a>
#### `dd()` 

The `dd` function dumps the given variables and ends execution of the script:

```

    dd($value);

    dd($value1, $value2, $value3, ...);

If you do not want to halt the execution of your script, use the [`dump`](#method-dump) function instead.

<a name="method-decrypt"></a>
#### `decrypt()` 

The `decrypt` function decrypts the given value using Laravel's [encrypter](/docs/encryption):

```try-code
{
    mode: 'cli',
    cliCode: `$decrypted = decrypt($encrypted_value);
`
}
```

    $decrypted = decrypt($encrypted_value);

<a name="method-dispatch"></a>
#### `dispatch()` 

The `dispatch` function pushes the given [job](/docs/queues#creating-jobs) onto the Laravel [job queue](/docs/queues):


    dispatch(new App\Jobs\SendEmails);

<a name="method-dispatch-now"></a>
#### `dispatch_now()` 

The `dispatch_now` function runs the given [job](/docs/queues#creating-jobs) immediately and returns the value from its `handle` method:


    $result = dispatch_now(new App\Jobs\SendEmails);

<a name="method-dump"></a>
#### `dump()` 

The `dump` function dumps the given variables:

    dump($value);

    dump($value1, $value2, $value3, ...);

If you want to stop executing the script after dumping the variables, use the [`dd`](#method-dd) function instead.

<a name="method-encrypt"></a>
#### `encrypt()` 

The `encrypt` function encrypts the given value using Laravel's [encrypter](/docs/encryption):


    $encrypted = encrypt($unencrypted_value);

<a name="method-env"></a>
#### `env()` 

The `env` function retrieves the value of an [environment variable](/docs/configuration#environment-configuration) or returns a default value:

```try-code
{
    mode: 'cli',
    cliCode: `env('APP_ENV');
`
}
```

    $env = env('APP_ENV');

    // Returns 'production' if APP_ENV is not set...
    $env = env('APP_ENV', 'production');

> {note} If you execute the `config:cache` command during your deployment process, you should be sure that you are only calling the `env` function from within your configuration files. Once the configuration has been cached, the `.env` file will not be loaded and all calls to the `env` function will return `null`.

<a name="method-event"></a>
#### `event()` 

The `event` function dispatches the given [event](/docs/events) to its listeners:


    event(new UserRegistered($user));

<a name="method-factory"></a>
#### `factory()` 

The `factory` function creates a model factory builder for a given class, name, and amount. It can be used while [testing](/docs/database-testing#writing-factories) or [seeding](/docs/seeding#using-model-factories):

    $user = factory(App\User::class)->make();

<a name="method-filled"></a>
#### `filled()` 

The `filled` function returns whether the given value is not "blank":

```try-code
{
    mode: 'cli',
    cliCode: `filled(0);
`
}
```

    filled(0);
    filled(true);
    filled(false);

    // true

    filled('');
    filled('   ');
    filled(null);
    filled(collect());

    // false

For the inverse of `filled`, see the [`blank`](#method-blank) method.

<a name="method-info"></a>
#### `info()` 

The `info` function will write information to the [log](/docs/logging):


    info('Some helpful information!');

An array of contextual data may also be passed to the function:

    info('User login attempt failed.', ['id' => $user->id]);

<a name="method-logger"></a>
#### `logger()` 

The `logger` function can be used to write a `debug` level message to the [log](/docs/logging):


    logger('Debug message');

An array of contextual data may also be passed to the function:

    logger('User has logged in.', ['id' => $user->id]);

A [logger](/docs/errors#logging) instance will be returned if no value is passed to the function:

    logger()->error('You are not allowed here.');

<a name="method-method-field"></a>
#### `method_field()` 

The `method_field` function generates an HTML `hidden` input field containing the spoofed value of the form's HTTP verb. For example, using [Blade syntax](/docs/blade):


    <form method="POST">
        {{ method_field('DELETE') }}
    </form>

<a name="method-now"></a>
#### `now()` 

The `now` function creates a new `Illuminate\Support\Carbon` instance for the current time:

```try-code
{
    mode: 'cli',
    cliCode: `now();
`
}
```

    $now = now();

<a name="method-old"></a>
#### `old()` 

The `old` function [retrieves](/docs/requests#retrieving-input) an [old input](/docs/requests#old-input) value flashed into the session:

    $value = old('value');

    $value = old('value', 'default');

<a name="method-optional"></a>
#### `optional()` 

The `optional` function accepts any argument and allows you to access properties or call methods on that object. If the given object is `null`, properties and methods will return `null` instead of causing an error:

```try-code
{
    mode: 'cli',
    cliCode: `optional(User::find(1))->name;
`
}
```

    return optional($user->address)->street;

    {!! old('name', optional($user)->name) !!}

The `optional` function also accepts a Closure as its second argument. The Closure will be invoked if the value provided as the first argument is not null:

    return optional(User::find($id), function ($user) {
        return new DummyUser;
    });

<a name="method-policy"></a>
#### `policy()` 

The `policy` method retrieves a [policy](/docs/authorization#creating-policies) instance for a given class:

    $policy = policy(App\User::class);

<a name="method-redirect"></a>
#### `redirect()` 

The `redirect` function returns a [redirect HTTP response](/docs/responses#redirects), or returns the redirector instance if called with no arguments:


    return redirect($to = null, $status = 302, $headers = [], $secure = null);

    return redirect('/home');

    return redirect()->route('route.name');

<a name="method-report"></a>
#### `report()` 

The `report` function will report an exception using your [exception handler](/docs/errors#the-exception-handler)'s `report` method:

    report($e);

<a name="method-request"></a>
#### `request()` 

The `request` function returns the current [request](/docs/requests) instance or obtains an input item:

```try-code
{
    mode: 'cli',
    cliCode: `request();`
}
```

    $request = request();

    $value = request('key', $default);

<a name="method-rescue"></a>
#### `rescue()` 

The `rescue` function executes the given Closure and catches any exceptions that occur during its execution. All exceptions that are caught will be sent to your [exception handler](/docs/errors#the-exception-handler)'s `report` method; however, the request will continue processing:

    return rescue(function () {
        return $this->method();
    });

You may also pass a second argument to the `rescue` function. This argument will be the "default" value that should be returned if an exception occurs while executing the Closure:

    return rescue(function () {
        return $this->method();
    }, false);

    return rescue(function () {
        return $this->method();
    }, function () {
        return $this->failure();
    });

<a name="method-resolve"></a>
#### `resolve()` 

The `resolve` function resolves a given class or interface name to its instance using the [service container](/docs/container):

    $api = resolve('HelpSpot\API');

<a name="method-response"></a>
#### `response()` 

The `response` function creates a [response](/docs/responses) instance or obtains an instance of the response factory:

```try-code
{
    mode: 'cli',
    cliCode: `response('Hello World', 200, $headers);`
}
```

    return response('Hello World', 200, $headers);

    return response()->json(['foo' => 'bar'], 200, $headers);

<a name="method-retry"></a>
#### `retry()` 

The `retry` function attempts to execute the given callback until the given maximum attempt threshold is met. If the callback does not throw an exception, its return value will be returned. If the callback throws an exception, it will automatically be retried. If the maximum attempt count is exceeded, the exception will be thrown:

```try-code
{
    mode: 'cli',
    cliCode: `return retry(5, function () {
  // Attempt 5 times while resting 100ms in between attempts...
 }, 100);
`
}
```

    return retry(5, function () {
        // Attempt 5 times while resting 100ms in between attempts...
    }, 100);

<a name="method-session"></a>
#### `session()` 

The `session` function may be used to get or set [session](/docs/session) values:

    $value = session('key');

You may set values by passing an array of key / value pairs to the function:

    session(['chairs' => 7, 'instruments' => 3]);

The session store will be returned if no value is passed to the function:

    $value = session()->get('key');

    session()->put('key', $value);

<a name="method-tap"></a>
#### `tap()` 

The `tap` function accepts two arguments: an arbitrary `$value` and a Closure. The `$value` will be passed to the Closure and then be returned by the `tap` function. The return value of the Closure is irrelevant:

    $user = tap(User::first(), function ($user) {
        $user->name = 'taylor';

        $user->save();
    });

If no Closure is passed to the `tap` function, you may call any method on the given `$value`. The return value of the method you call will always be `$value`, regardless of what the method actually returns in its definition. For example, the Eloquent `update` method typically returns an integer. However, we can force the method to return the model itself by chaining the `update` method call through the `tap` function:

    $user = tap($user)->update([
        'name' => $name,
        'email' => $email,
    ]);

To add a `tap` method to a class, you may add the `Illuminate\Support\Traits\Tappable` trait to the class. The `tap` method of this trait accepts a Closure as its only argument. The object instance itself will be passed to the Closure and then be returned by the `tap` method:

    return $user->tap(function ($user) {
        //
    });

<a name="method-throw-if"></a>
#### `throw_if()` 

The `throw_if` function throws the given exception if a given boolean expression evaluates to `true`:

    throw_if(! Auth::user()->isAdmin(), AuthorizationException::class);

    throw_if(
        ! Auth::user()->isAdmin(),
        AuthorizationException::class,
        'You are not allowed to access this page'
    );

<a name="method-throw-unless"></a>
#### `throw_unless()` 

The `throw_unless` function throws the given exception if a given boolean expression evaluates to `false`:

    throw_unless(Auth::user()->isAdmin(), AuthorizationException::class);

    throw_unless(
        Auth::user()->isAdmin(),
        AuthorizationException::class,
        'You are not allowed to access this page'
    );

<a name="method-today"></a>
#### `today()` 

The `today` function creates a new `Illuminate\Support\Carbon` instance for the current date:

```try-code
{
    mode: 'cli',
    cliCode: `today();
`
}
```

    $today = today();

<a name="method-trait-uses-recursive"></a>
#### `trait_uses_recursive()` 

The `trait_uses_recursive` function returns all traits used by a trait:

```try-code
{
    mode: 'cli',
    cliCode: `trait_uses_recursive(\Illuminate\Notifications\Notifiable::class);
`
}
```

    $traits = trait_uses_recursive(\Illuminate\Notifications\Notifiable::class);

<a name="method-transform"></a>
#### `transform()` 

The `transform` function executes a `Closure` on a given value if the value is not [blank](#method-blank) and returns the result of the `Closure`:

    $callback = function ($value) {
        return $value * 2;
    };

    $result = transform(5, $callback);

    // 10

A default value or `Closure` may also be passed as the third parameter to the method. This value will be returned if the given value is blank:

    $result = transform(null, $callback, 'The value is blank');

    // The value is blank

<a name="method-validator"></a>
#### `validator()` 

The `validator` function creates a new [validator](/docs/validation) instance with the given arguments. You may use it instead of the `Validator` facade for convenience:

    $validator = validator($data, $rules, $messages);

<a name="method-value"></a>
#### `value()` 

The `value` function returns the value it is given. However, if you pass a `Closure` to the function, the `Closure` will be executed then its result will be returned:


    $result = value(true);

    // true

    $result = value(function () {
        return false;
    });

    // false

<a name="method-view"></a>
#### `view()` 

The `view` function retrieves a [view](/docs/views) instance:

    return view('auth.login');

<a name="method-with"></a>
#### `with()` 

The `with` function returns the value it is given. If a `Closure` is passed as the second argument to the function, the `Closure` will be executed and its result will be returned:

    $callback = function ($value) {
        return (is_numeric($value)) ? $value * 2 : 0;
    };

    $result = with(5, $callback);

    // 10

    $result = with(null, $callback);

    // 0

    $result = with(5, null);

    // 5
