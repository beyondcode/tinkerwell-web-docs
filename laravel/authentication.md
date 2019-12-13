# Authentication

- [Authentication Quickstart](#authentication-quickstart)
    - [Retrieving The Authenticated User](#retrieving-the-authenticated-user)
- [Logging Out](#logging-out)
- [Events](#events)

<a name="retrieving-the-authenticated-user"></a>
### Retrieving The Authenticated User

You may access the authenticated user via the `Auth` facade:

```try-code
{
    mode: "cli",
    cliCode: `use Illuminate\\Support\\Facades\\Auth;
// Store and login a user
$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

Auth::login($user);

// Get the currently authenticated user...
$user = Auth::user();
`
}
```

    use Illuminate\Support\Facades\Auth;

    // Get the currently authenticated user...
    $user = Auth::user();

    // Get the currently authenticated user's ID...
    $id = Auth::id();

Alternatively, once a user is authenticated, you may access the authenticated user via an `Illuminate\Http\Request` instance. Remember, type-hinted classes will automatically be injected into your controller methods:

```try-code
{
    mode: "http",
    controllerCode: `use Illuminate\\Support\\Facades\\Auth;
use Illuminate\\Http\\Request;

// Store and login a user
$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

Auth::login($user);

class TinkerwellController
{
    public function index(Request $request) {
        dump($request->user());
    }
}
`,
    viewCode: "{{-- not needed --}}"
}
```

    <?php

    namespace App\Http\Controllers;

    use Illuminate\Http\Request;

    class ProfileController extends Controller
    {
        /**
         * Update the user's profile.
         *
         * @param  Request  $request
         * @return Response
         */
        public function update(Request $request)
        {
            // $request->user() returns an instance of the authenticated user...
        }
    }

#### Determining If The Current User Is Authenticated

To determine if the user is already logged into your application, you may use the `check` method on the `Auth` facade, which will return `true` if the user is authenticated:

```try-code
{
    mode: "cli",
    cliCode: `use Illuminate\\Support\\Facades\\Auth;

var_dump(Auth::check());

// Store and login a user
$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

Auth::login($user);

var_dump(Auth::check());
`
}
```

    use Illuminate\Support\Facades\Auth;

    if (Auth::check()) {
        // The user is logged in...
    }


#### Logging Out

To log users out of your application, you may use the `logout` method on the `Auth` facade. This will clear the authentication information in the user's session:

```try-code
{
    mode: "cli",
    cliCode: `use Illuminate\\Support\\Facades\\Auth;

// Store and login a user
$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

Auth::login($user);

var_dump(Auth::check());

Auth::logout();

var_dump(Auth::check());
`
}
```

    Auth::logout();

<a name="other-authentication-methods"></a>
### Other Authentication Methods

#### Authenticate A User Instance

If you need to log an existing user instance into your application, you may call the `login` method with the user instance. The given object must be an implementation of the `Illuminate\Contracts\Auth\Authenticatable` [contract](/docs/contracts). The `App\User` model included with Laravel already implements this interface:

```try-code
{
    mode: "cli",
    cliCode: `use Illuminate\\Support\\Facades\\Auth;
// Store and login a user
$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

Auth::login($user);

// Get the currently authenticated user...
$user = Auth::user();
`
}
```

    Auth::login($user);

    // Login and "remember" the given user...
    Auth::login($user, true);

You may specify the guard instance you would like to use:

    Auth::guard('admin')->login($user);

#### Authenticate A User By ID

To log a user into the application by their ID, you may use the `loginUsingId` method. This method accepts the primary key of the user you wish to authenticate:

```try-code
{
    mode: "cli",
    cliCode: `use Illuminate\\Support\\Facades\\Auth;
// Store and login a user
$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

Auth::loginUsingId($user->id);

// Get the currently authenticated user...
$user = Auth::user();
`
}
```

    Auth::loginUsingId(1);

    // Login and "remember" the given user...
    Auth::loginUsingId(1, true);

