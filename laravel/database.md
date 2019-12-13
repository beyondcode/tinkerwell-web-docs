# Database: Getting Started

- [Running Raw SQL Queries](#running-queries)
- [Listening For Query Events](#listening-for-query-events)
- [Database Transactions](#database-transactions)


<a name="running-queries"></a>
## Running Raw SQL Queries

Once you have configured your database connection, you may run queries using the `DB` facade. The `DB` facade provides methods for each type of query: `select`, `update`, `insert`, `delete`, and `statement`.

#### Running A Select Query

To run a basic query, you may use the `select` method on the `DB` facade:

```try-code
{
    mode: "cli",
    cliCode: `$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

DB::select('select * from users where name = ?', ['Marcel']);
`
}
```

    <?php

    namespace App\Http\Controllers;

    use App\Http\Controllers\Controller;
    use Illuminate\Support\Facades\DB;

    class UserController extends Controller
    {
        /**
         * Show a list of all of the application's users.
         *
         * @return Response
         */
        public function index()
        {
            $users = DB::select('select * from users where active = ?', [1]);

            return view('user.index', ['users' => $users]);
        }
    }

The first argument passed to the `select` method is the raw SQL query, while the second argument is any parameter bindings that need to be bound to the query. Typically, these are the values of the `where` clause constraints. Parameter binding provides protection against SQL injection.

The `select` method will always return an `array` of results. Each result within the array will be a PHP `stdClass` object, allowing you to access the values of the results:

    foreach ($users as $user) {
        echo $user->name;
    }

#### Using Named Bindings

Instead of using `?` to represent your parameter bindings, you may execute a query using named bindings:


```try-code
{
    mode: "cli",
    cliCode: `$user = User::create([
  'name' => 'Marcel',
  'email' => 'marcel@beyondco.de',
  'password' => 'test',
]);

DB::select('select * from users where id = :id', ['id' => 1]);
`
}
```

    $results = DB::select('select * from users where id = :id', ['id' => 1]);

#### Running An Insert Statement

To execute an `insert` statement, you may use the `insert` method on the `DB` facade. Like `select`, this method takes the raw SQL query as its first argument and bindings as its second argument:

```try-code
{
    mode: "cli",
    cliCode: `DB::insert('insert into users (name, email, password) values (?, ?, ?)', ['Marcel', 'marcel@beyondco.de', 'test']);
`
}
```

    DB::insert('insert into users (id, name) values (?, ?)', [1, 'Dayle']);

#### Running An Update Statement

The `update` method should be used to update existing records in the database. The number of rows affected by the statement will be returned:

    $affected = DB::update('update users set votes = 100 where name = ?', ['John']);

#### Running A Delete Statement

The `delete` method should be used to delete records from the database. Like `update`, the number of rows affected will be returned:

```try-code
{
    mode: "cli",
    cliCode: `DB::insert('insert into users (name, email, password) values (?, ?, ?)', ['Marcel', 'marcel@beyondco.de', 'test']);

DB::delete('delete from users');

DB::select('select * from users');
`
}
```

    $deleted = DB::delete('delete from users');

#### Running A General Statement

Some database statements do not return any value. For these types of operations, you may use the `statement` method on the `DB` facade:

    DB::statement('drop table users');

<a name="listening-for-query-events"></a>
## Listening For Query Events

If you would like to receive each SQL query executed by your application, you may use the `listen` method. This method is useful for logging queries or debugging. You may register your query listener in a [service provider](/docs/providers):

```try-code
{
    mode: "cli",
    cliCode: `DB::listen(function ($query) {
    echo $query->sql . PHP_EOL;
});

DB::insert('insert into users (name, email, password) values (?, ?, ?)', ['Marcel', 'marcel@beyondco.de', 'test']);
`
}
```

    <?php

    namespace App\Providers;

    use Illuminate\Support\Facades\DB;
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
            DB::listen(function ($query) {
                // $query->sql
                // $query->bindings
                // $query->time
            });
        }
    }

<a name="database-transactions"></a>
## Database Transactions

You may use the `transaction` method on the `DB` facade to run a set of operations within a database transaction. If an exception is thrown within the transaction `Closure`, the transaction will automatically be rolled back. If the `Closure` executes successfully, the transaction will automatically be committed. You don't need to worry about manually rolling back or committing while using the `transaction` method:

    DB::transaction(function () {
        DB::table('users')->update(['votes' => 1]);

        DB::table('posts')->delete();
    });

#### Handling Deadlocks

The `transaction` method accepts an optional second argument which defines the number of times a transaction should be reattempted when a deadlock occurs. Once these attempts have been exhausted, an exception will be thrown:

    DB::transaction(function () {
        DB::table('users')->update(['votes' => 1]);

        DB::table('posts')->delete();
    }, 5);

#### Manually Using Transactions

If you would like to begin a transaction manually and have complete control over rollbacks and commits, you may use the `beginTransaction` method on the `DB` facade:

    DB::beginTransaction();

You can rollback the transaction via the `rollBack` method:

    DB::rollBack();

Lastly, you can commit a transaction via the `commit` method:

    DB::commit();

> {tip} The `DB` facade's transaction methods control the transactions for both the [query builder](/docs/{{version}}/queries) and [Eloquent ORM](/docs/{{version}}/eloquent).
