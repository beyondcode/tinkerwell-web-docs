# Blade Templates

- [Introduction](#introduction)
- [Displaying Data](#displaying-data)
    - [Blade & JavaScript Frameworks](#blade-and-javascript-frameworks)
- [Control Structures](#control-structures)
    - [If Statements](#if-statements)
    - [Switch Statements](#switch-statements)
    - [Loops](#loops)
    - [The Loop Variable](#the-loop-variable)
    - [Comments](#comments)
    - [PHP](#php)
- [Extending Blade](#extending-blade)
    - [Custom If Statements](#custom-if-statements)

<a name="introduction"></a>
## Introduction

Blade is the simple, yet powerful templating engine provided with Laravel. Unlike other popular PHP templating engines, Blade does not restrict you from using plain PHP code in your views. In fact, all Blade views are compiled into plain PHP code and cached until they are modified, meaning Blade adds essentially zero overhead to your application. Blade view files use the `.blade.php` file extension and are typically stored in the `resources/views` directory.

<a name="displaying-data"></a>
## Displaying Data

You may display data passed to your Blade views by wrapping the variable in curly braces. For example, given the following route:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', ['name' => 'Samantha']);
    }
}
`,
    viewCode: "Hello, {{ $name }}."
}
```

    Route::get('greeting', function () {
        return view('welcome', ['name' => 'Samantha']);
    });

You may display the contents of the `name` variable like so:

    Hello, {{ $name }}.


You are not limited to displaying the contents of the variables passed to the view. You may also echo the results of any PHP function. In fact, you can put any PHP code you wish inside of a Blade echo statement:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: "The current UNIX timestamp is {{ time() }}."
}
```

    The current UNIX timestamp is {{ time() }}.

#### Displaying Unescaped Data

By default, Blade `{{ }}` statements are automatically sent through PHP's `htmlspecialchars` function to prevent XSS attacks. If you do not want your data to be escaped, you may use the following syntax:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', ['name' => 'Unescaped']);
    }
}
`,
    viewCode: "Hello, {!! $name !!}."
}
```

    Hello, {!! $name !!}.

> {note} Be very careful when echoing content that is supplied by users of your application. Always use the escaped, double curly brace syntax to prevent XSS attacks when displaying user supplied data.

#### Rendering JSON

Sometimes you may pass an array to your view with the intention of rendering it as JSON in order to initialize a JavaScript variable. For example:

    <script>
        var app = <?php echo json_encode($array); ?>;
    </script>

However, instead of manually calling `json_encode`, you may use the `@json` Blade directive. The `@json` directive accepts the same arguments as PHP's `json_encode` function:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', [
            'array' => [
                'data' => 'goes here',
                'status' => 'json encoded',
            ]
        ]);
    }
}
`,
    viewCode: `<pre>
  var app = @json($array, JSON_PRETTY_PRINT);
</pre>`
}
```

    <script>
        var app = @json($array);

        var app = @json($array, JSON_PRETTY_PRINT);
    </script>

> {note} You should only use the `@json` directive to render existing variables as JSON. The Blade templating is based on regular expressions and attempts to pass a complex expression to the directive may cause unexpected failures.

The `@json` directive is also useful for seeding Vue components or `data-*` attributes:

    <example-component :some-prop='@json($array)'></example-component>

> {note} Using `@json` in element attributes requires that it be surrounded by single quotes.

#### HTML Entity Encoding

By default, Blade (and the Laravel `e` helper) will double encode HTML entities. If you would like to disable double encoding, call the `Blade::withoutDoubleEncoding` method from the `boot` method of your `AppServiceProvider`:

    <?php

    namespace App\Providers;

    use Illuminate\Support\Facades\Blade;
    use Illuminate\Support\ServiceProvider;

    class AppServiceProvider extends ServiceProvider
    {
        /**
         * Bootstrap any application services.
         *
         * @return void
         */
        public function boot()
        {
            Blade::withoutDoubleEncoding();
        }
    }

<a name="blade-and-javascript-frameworks"></a>
### Blade & JavaScript Frameworks

Since many JavaScript frameworks also use "curly" braces to indicate a given expression should be displayed in the browser, you may use the `@` symbol to inform the Blade rendering engine an expression should remain untouched. For example:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: `<h1>Laravel</h1>

Hello, @{{ name }}.`
}
```

    <h1>Laravel</h1>

    Hello, @{{ name }}.

In this example, the `@` symbol will be removed by Blade; however, `{{ name }}` expression will remain untouched by the Blade engine, allowing it to instead be rendered by your JavaScript framework.

#### The `@verbatim` Directive

If you are displaying JavaScript variables in a large portion of your template, you may wrap the HTML in the `@verbatim` directive so that you do not have to prefix each Blade echo statement with an `@` symbol:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: `@verbatim
    <div class="container">
        Hello, {{ name }}.
    </div>
@endverbatim`
}
```

    @verbatim
        <div class="container">
            Hello, {{ name }}.
        </div>
    @endverbatim

<a name="control-structures"></a>
## Control Structures

In addition to template inheritance and displaying data, Blade also provides convenient shortcuts for common PHP control structures, such as conditional statements and loops. These shortcuts provide a very clean, terse way of working with PHP control structures, while also remaining familiar to their PHP counterparts.

<a name="if-statements"></a>
### If Statements

You may construct `if` statements using the `@if`, `@elseif`, `@else`, and `@endif` directives. These directives function identically to their PHP counterparts:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', [
            'records' => [1,] // <-- change me
        ]);
    }
}
`,
    viewCode: `@if (count($records) === 1)
    I have one record!
@elseif (count($records) > 1)
    I have multiple records!
@else
    I don't have any records!
@endif`
}
```

    @if (count($records) === 1)
        I have one record!
    @elseif (count($records) > 1)
        I have multiple records!
    @else
        I don't have any records!
    @endif

For convenience, Blade also provides an `@unless` directive:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: `@unless (Auth::check())
    You are not signed in.
@endunless`
}
```

    @unless (Auth::check())
        You are not signed in.
    @endunless

In addition to the conditional directives already discussed, the `@isset` and `@empty` directives may be used as convenient shortcuts for their respective PHP functions:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', [
            'records' => true,
        ]);
    }
}
`,
    viewCode: `@isset($records)
    Records is defined and is not null
@endisset`
}
```

    @isset($records)
        // $records is defined and is not null...
    @endisset

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', [
            'records' => [],
        ]);
    }
}
`,
    viewCode: `@empty($records)
    $records is "empty"...
@endempty`
}
```

    @empty($records)
        // $records is "empty"...
    @endempty

#### Authentication Directives

The `@auth` and `@guest` directives may be used to quickly determine if the current user is authenticated or is a guest:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        // Store and login a user
        $user = User::create([
          'name' => 'Marcel',
          'email' => 'marcel@beyondco.de',
          'password' => 'test',
        ]);

        // Comment this out to trigger the @guest directive
        Auth::login($user);

        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: `@auth
    The user is authenticated...
@endauth

@guest
    The user is not authenticated...
@endguest`
}
```

    @auth
        // The user is authenticated...
    @endauth

    @guest
        // The user is not authenticated...
    @endguest

If needed, you may specify the [authentication guard](/docs/authentication) that should be checked when using the `@auth` and `@guest` directives:

    @auth('admin')
        // The user is authenticated...
    @endauth

    @guest('admin')
        // The user is not authenticated...
    @endguest

<a name="switch-statements"></a>
### Switch Statements

Switch statements can be constructed using the `@switch`, `@case`, `@break`, `@default` and `@endswitch` directives:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', [
            'i' => 1 // <-- Change me to trigger other cases
        ]);
    }
}
`,
    viewCode: `@switch($i)
    @case(1)
        First case...
        @break

    @case(2)
        Second case...
        @break

    @default
        Default case...
@endswitch`
}
```

    @switch($i)
        @case(1)
            First case...
            @break

        @case(2)
            Second case...
            @break

        @default
            Default case...
    @endswitch

<a name="loops"></a>
### Loops

In addition to conditional statements, Blade provides simple directives for working with PHP's loop structures. Again, each of these directives functions identically to their PHP counterparts:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: `@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}<br>
@endfor`
}
```

    @for ($i = 0; $i < 10; $i++)
        The current value is {{ $i }}
    @endfor

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        // Insert two users
        User::create([
          'name' => 'Marcel',
          'email' => 'marcel@beyondco.de',
          'password' => 'test',
        ]);

        User::create([
          'name' => 'Sebastian',
          'email' => 'sebastian@beyondco.de',
          'password' => 'test',
        ]);

        return view('__tinker__::tinkerwell', [
            'users' => User::all()
        ]);
    }
}
`,
    viewCode: `@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach`
}
```

    @foreach ($users as $user)
        <p>This is user {{ $user->id }}</p>
    @endforeach

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        // Insert two users
        User::create([
          'name' => 'Marcel',
          'email' => 'marcel@beyondco.de',
          'password' => 'test',
        ]);

        User::create([
          'name' => 'Sebastian',
          'email' => 'sebastian@beyondco.de',
          'password' => 'test',
        ]);

        return view('__tinker__::tinkerwell', [
            'users' => User::all()
        ]);
    }
}
`,
    viewCode: `@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse`
}
```

    @forelse ($users as $user)
        <li>{{ $user->name }}</li>
    @empty
        <p>No users</p>
    @endforelse

When using loops you may also end the loop or skip the current iteration:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        // Insert two users
        User::create([
          'name' => 'Marcel',
          'email' => 'marcel@beyondco.de',
          'password' => 'test',
        ]);

        User::create([
          'name' => 'Sebastian',
          'email' => 'sebastian@beyondco.de',
          'password' => 'test',
        ]);

        return view('__tinker__::tinkerwell', [
            'users' => User::all()
        ]);
    }
}
`,
    viewCode: `@foreach ($users as $user)
    @if ($user->id == 1)
        @continue
    @endif

    <li>{{ $user->name }}</li>
@endforeach`
}
```

    @foreach ($users as $user)
        @if ($user->type == 1)
            @continue
        @endif

        <li>{{ $user->name }}</li>

        @if ($user->number == 5)
            @break
        @endif
    @endforeach

You may also include the condition with the directive declaration in one line:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        // Insert two users
        User::create([
          'name' => 'Marcel',
          'email' => 'marcel@beyondco.de',
          'password' => 'test',
        ]);

        User::create([
          'name' => 'Sebastian',
          'email' => 'sebastian@beyondco.de',
          'password' => 'test',
        ]);

        return view('__tinker__::tinkerwell', [
            'users' => User::all()
        ]);
    }
}
`,
    viewCode: `@foreach ($users as $user)
    @continue($user->id == 1)

    <li>{{ $user->name }}</li>
@endforeach`
}
```

    @foreach ($users as $user)
        @continue($user->type == 1)

        <li>{{ $user->name }}</li>

        @break($user->number == 5)
    @endforeach

<a name="the-loop-variable"></a>
### The Loop Variable

When looping, a `$loop` variable will be available inside of your loop. This variable provides access to some useful bits of information such as the current loop index and whether this is the first or last iteration through the loop:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        // Insert two users
        User::create([
          'name' => 'Marcel',
          'email' => 'marcel@beyondco.de',
          'password' => 'test',
        ]);

        User::create([
          'name' => 'Julia',
          'email' => 'julia@beyondco.de',
          'password' => 'test',
        ]);

        User::create([
          'name' => 'Sebastian',
          'email' => 'sebastian@beyondco.de',
          'password' => 'test',
        ]);

        return view('__tinker__::tinkerwell', [
            'users' => User::all()
        ]);
    }
}
`,
    viewCode: `@foreach ($users as $user)
    @if ($loop->first)
        This is the first iteration.
    @endif

    @if ($loop->last)
        This is the last iteration.
    @endif

    <p>This is user {{ $user->id }}</p>
@endforeach`
}
```

    @foreach ($users as $user)
        @if ($loop->first)
            This is the first iteration.
        @endif

        @if ($loop->last)
            This is the last iteration.
        @endif

        <p>This is user {{ $user->id }}</p>
    @endforeach

If you are in a nested loop, you may access the parent loop's `$loop` variable via the `parent` property:

    @foreach ($users as $user)
        @foreach ($user->posts as $post)
            @if ($loop->parent->first)
                This is first iteration of the parent loop.
            @endif
        @endforeach
    @endforeach

The `$loop` variable also contains a variety of other useful properties:

Property  | Description
------------- | -------------
`$loop->index`  |  The index of the current loop iteration (starts at 0).
`$loop->iteration`  |  The current loop iteration (starts at 1).
`$loop->remaining`  |  The iterations remaining in the loop.
`$loop->count`  |  The total number of items in the array being iterated.
`$loop->first`  |  Whether this is the first iteration through the loop.
`$loop->last`  |  Whether this is the last iteration through the loop.
`$loop->even`  |  Whether this is an even iteration through the loop.
`$loop->odd`  |  Whether this is an odd iteration through the loop.
`$loop->depth`  |  The nesting level of the current loop.
`$loop->parent`  |  When in a nested loop, the parent's loop variable.

<a name="comments"></a>
### Comments

Blade also allows you to define comments in your views. However, unlike HTML comments, Blade comments are not included in the HTML returned by your application:

    {{-- This comment will not be present in the rendered HTML --}}

<a name="php"></a>
### PHP

In some situations, it's useful to embed PHP code into your views. You can use the Blade `@php` directive to execute a block of plain PHP within your template:


```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: `@php
    echo time();
@endphp`
}
```

    @php
        //
    @endphp


<a name="extending-blade"></a>
## Extending Blade

Blade allows you to define your own custom directives using the `directive` method. When the Blade compiler encounters the custom directive, it will call the provided callback with the expression that the directive contains.

The following example creates a `@datetime($var)` directive which formats a given `$var`, which should be an instance of `DateTime`:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;
use Illuminate\\Support\\Facades\\Blade;
use Illuminate\\Support\\ServiceProvider;

class BladeServiceProvider extends ServiceProvider
{
  public function boot()
  {
    Blade::directive('datetime', function ($expression) {
        return "<?php echo ($expression)->format('m/d/Y H:i'); ?>";
    });
  }
}

App::register(BladeServiceProvider::class);

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell', [
            'var' => now()
        ]);
    }
}
`,
    viewCode: `@datetime($var)`
}
```

    <?php

    namespace App\Providers;

    use Illuminate\Support\Facades\Blade;
    use Illuminate\Support\ServiceProvider;

    class AppServiceProvider extends ServiceProvider
    {
        /**
         * Register any application services.
         *
         * @return void
         */
        public function register()
        {
            //
        }

        /**
         * Bootstrap any application services.
         *
         * @return void
         */
        public function boot()
        {
            Blade::directive('datetime', function ($expression) {
                return "<?php echo ($expression)->format('m/d/Y H:i'); ?>";
            });
        }
    }

As you can see, we will chain the `format` method onto whatever expression is passed into the directive. So, in this example, the final PHP generated by this directive will be:

    <?php echo ($var)->format('m/d/Y H:i'); ?>

<a name="custom-if-statements"></a>
### Custom If Statements

Programming a custom directive is sometimes more complex than necessary when defining simple, custom conditional statements. For that reason, Blade provides a `Blade::if` method which allows you to quickly define custom conditional directives using Closures. For example, let's define a custom conditional that checks the current application environment. We may do this in the `boot` method of our `AppServiceProvider`:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Http\\Request;
use Illuminate\\Support\\Facades\\Blade;
use Illuminate\\Support\\ServiceProvider;

class BladeServiceProvider extends ServiceProvider
{
  public function boot()
  {
    Blade::if('env', function ($environment) {
        return app()->environment($environment);
    });
  }
}

App::register(BladeServiceProvider::class);

class TinkerwellController
{
    public function index(Request $request) {
        return view('__tinker__::tinkerwell');
    }
}
`,
    viewCode: `@env('local')
    The application is in the local environment...
@elseenv('testing')
    The application is in the testing environment...
@else
    The application is not in the local or testing environment...
@endenv

@unlessenv('production')
    The application is not in the production environment...
@endenv`
}
```

    use Illuminate\Support\Facades\Blade;

    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        Blade::if('env', function ($environment) {
            return app()->environment($environment);
        });
    }

Once the custom conditional has been defined, we can easily use it on our templates:

    @env('local')
        // The application is in the local environment...
    @elseenv('testing')
        // The application is in the testing environment...
    @else
        // The application is not in the local or testing environment...
    @endenv

    @unlessenv('production')
        // The application is not in the production environment...
    @endenv
