# Validation

- [Introduction](#introduction)
- [Available Validation Rules](#available-validation-rules)
- [Conditionally Adding Rules](#conditionally-adding-rules)
- [Validating Arrays](#validating-arrays)
- [Custom Validation Rules](#custom-validation-rules)
    - [Using Rule Objects](#using-rule-objects)
    - [Using Closures](#using-closures)
    - [Using Extensions](#using-extensions)
    - [Implicit Extensions](#implicit-extensions)

<a name="introduction"></a>
## Introduction

Laravel provides several different approaches to validate your application's incoming data. By default, Laravel's base controller class uses a `ValidatesRequests` trait which provides a convenient method to validate incoming HTTP request with a variety of powerful validation rules.

<a name="available-validation-rules"></a>
## Available Validation Rules

Below is a list of all available validation rules and their function:
<div class="collection-method-list" markdown="1">

[Accepted](#rule-accepted)
[Active URL](#rule-active-url)
[After (Date)](#rule-after)
[After Or Equal (Date)](#rule-after-or-equal)
[Alpha](#rule-alpha)
[Alpha Dash](#rule-alpha-dash)
[Alpha Numeric](#rule-alpha-num)
[Array](#rule-array)
[Bail](#rule-bail)
[Before (Date)](#rule-before)
[Before Or Equal (Date)](#rule-before-or-equal)
[Between](#rule-between)
[Boolean](#rule-boolean)
[Confirmed](#rule-confirmed)
[Date](#rule-date)
[Date Equals](#rule-date-equals)
[Date Format](#rule-date-format)
[Different](#rule-different)
[Digits](#rule-digits)
[Digits Between](#rule-digits-between)
[Dimensions (Image Files)](#rule-dimensions)
[Distinct](#rule-distinct)
[E-Mail](#rule-email)
[Ends With](#rule-ends-with)
[Exists (Database)](#rule-exists)
[File](#rule-file)
[Filled](#rule-filled)
[Greater Than](#rule-gt)
[Greater Than Or Equal](#rule-gte)
[Image (File)](#rule-image)
[In](#rule-in)
[In Array](#rule-in-array)
[Integer](#rule-integer)
[IP Address](#rule-ip)
[JSON](#rule-json)
[Less Than](#rule-lt)
[Less Than Or Equal](#rule-lte)
[Max](#rule-max)
[MIME Types](#rule-mimetypes)
[MIME Type By File Extension](#rule-mimes)
[Min](#rule-min)
[Not In](#rule-not-in)
[Not Regex](#rule-not-regex)
[Nullable](#rule-nullable)
[Numeric](#rule-numeric)
[Password](#rule-password)
[Present](#rule-present)
[Regular Expression](#rule-regex)
[Required](#rule-required)
[Required If](#rule-required-if)
[Required Unless](#rule-required-unless)
[Required With](#rule-required-with)
[Required With All](#rule-required-with-all)
[Required Without](#rule-required-without)
[Required Without All](#rule-required-without-all)
[Same](#rule-same)
[Size](#rule-size)
[Sometimes](#conditionally-adding-rules)
[Starts With](#rule-starts-with)
[String](#rule-string)
[Timezone](#rule-timezone)
[Unique (Database)](#rule-unique)
[URL](#rule-url)
[UUID](#rule-uuid)

</div>

<a name="rule-accepted"></a>
#### accepted

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => true
];

$validator = Validator::make($data, [
    'field' => 'accepted',
]);

$validator->passes();
`
}
```

The field under validation must be _yes_, _on_, _1_, or _true_. This is useful for validating "Terms of Service" acceptance.

<a name="rule-active-url"></a>
#### active_url

The field under validation must have a valid A or AAAA record according to the `dns_get_record` PHP function. The hostname of the provided URL is extracted using the `parse_url` PHP function before being passed to `dns_get_record`.

<a name="rule-after"></a>
#### after:_date_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '2020-01-01'
];

$validator = Validator::make($data, [
    'field' => 'after:2019-12-13',
]);

$validator->passes();
`
}
```

The field under validation must be a value after a given date. The dates will be passed into the `strtotime` PHP function:

    'start_date' => 'required|date|after:tomorrow'

Instead of passing a date string to be evaluated by `strtotime`, you may specify another field to compare against the date:

    'finish_date' => 'required|date|after:start_date'

<a name="rule-after-or-equal"></a>
#### after\_or\_equal:_date_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '2019-12-13'
];

$validator = Validator::make($data, [
    'field' => 'after_or_equal:2019-12-13',
]);

$validator->passes();
`
}
```

The field under validation must be a value after or equal to the given date. For more information, see the [after](#rule-after) rule.

<a name="rule-alpha"></a>
#### alpha

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'abcdefg'
];

$validator = Validator::make($data, [
    'field' => 'alpha',
]);

$validator->passes();
`
}
```

The field under validation must be entirely alphabetic characters.

<a name="rule-alpha-dash"></a>
#### alpha_dash

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'abc-defg'
];

$validator = Validator::make($data, [
    'field' => 'alpha_dash',
]);

$validator->passes();
`
}
```

The field under validation may have alpha-numeric characters, as well as dashes and underscores.

<a name="rule-alpha-num"></a>
#### alpha_num


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'abc0123'
];

$validator = Validator::make($data, [
    'field' => 'alpha_num',
]);

$validator->passes();
`
}
```
The field under validation must be entirely alpha-numeric characters.

<a name="rule-array"></a>
#### array


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => [1,2,3]
];

$validator = Validator::make($data, [
    'field' => 'array',
]);

$validator->passes();
`
}
```

The field under validation must be a PHP `array`.

<a name="rule-bail"></a>
#### bail

Stop running validation rules after the first validation failure.

<a name="rule-before"></a>
#### before:_date_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '2019-12-01'
];

$validator = Validator::make($data, [
    'field' => 'before:2019-12-13',
]);

$validator->passes();
`
}
```
The field under validation must be a value preceding the given date. The dates will be passed into the PHP `strtotime` function. In addition, like the [`after`](#rule-after) rule, the name of another field under validation may be supplied as the value of `date`.

<a name="rule-before-or-equal"></a>
#### before\_or\_equal:_date_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '2019-12-13'
];

$validator = Validator::make($data, [
    'field' => 'before_or_equal:2019-12-13',
]);

$validator->passes();
`
}
```

The field under validation must be a value preceding or equal to the given date. The dates will be passed into the PHP `strtotime` function. In addition, like the [`after`](#rule-after) rule, the name of another field under validation may be supplied as the value of `date`.

<a name="rule-between"></a>
#### between:_min_,_max_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 5
];

$validator = Validator::make($data, [
    'field' => 'between:1,10',
]);

$validator->passes();
`
}
```
The field under validation must have a size between the given _min_ and _max_. Strings, numerics, arrays, and files are evaluated in the same fashion as the [`size`](#rule-size) rule.

<a name="rule-boolean"></a>
#### boolean

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 1
];

$validator = Validator::make($data, [
    'field' => 'boolean',
]);

$validator->passes();
`
}
```
The field under validation must be able to be cast as a boolean. Accepted input are `true`, `false`, `1`, `0`, `"1"`, and `"0"`.

<a name="rule-confirmed"></a>
#### confirmed

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'test',
    'field_confirmation' => 'test',
];

$validator = Validator::make($data, [
    'field' => 'confirmed',
]);

$validator->passes();
`
}
```

The field under validation must have a matching field of `foo_confirmation`. For example, if the field under validation is `password`, a matching `password_confirmation` field must be present in the input.

<a name="rule-date"></a>
#### date

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '2019-01-01'
];

$validator = Validator::make($data, [
    'field' => 'date',
]);

$validator->passes();
`
}
```

The field under validation must be a valid, non-relative date according to the `strtotime` PHP function.

<a name="rule-date-equals"></a>
#### date_equals:_date_


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '2019-01-01'
];

$validator = Validator::make($data, [
    'field' => 'date_equals:2019-01-01',
]);

$validator->passes();
`
}
```
The field under validation must be equal to the given date. The dates will be passed into the PHP `strtotime` function.

<a name="rule-date-format"></a>
#### date_format:_format_

The field under validation must match the given _format_. You should use **either** `date` or `date_format` when validating a field, not both. This validation rule supports all formats supported by PHP's [DateTime](https://www.php.net/manual/en/class.datetime.php) class.

<a name="rule-different"></a>
#### different:_field_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'foo'
    'other_field' => 'bar'
];

$validator = Validator::make($data, [
    'field' => 'different:bar',
]);

$validator->passes();
`
}
```
The field under validation must have a different value than _field_.

<a name="rule-digits"></a>
#### digits:_value_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 100
];

$validator = Validator::make($data, [
    'field' => 'digits:3',
]);

$validator->passes();
`
}
```

The field under validation must be _numeric_ and must have an exact length of _value_.

<a name="rule-digits-between"></a>
#### digits_between:_min_,_max_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 1001
];

$validator = Validator::make($data, [
    'field' => 'digits_between:3,5',
]);

$validator->passes();
`
}
```

The field under validation must be _numeric_ and must have a length between the given _min_ and _max_.

<a name="rule-dimensions"></a>
#### dimensions

The file under validation must be an image meeting the dimension constraints as specified by the rule's parameters:

    'avatar' => 'dimensions:min_width=100,min_height=200'

Available constraints are: _min\_width_, _max\_width_, _min\_height_, _max\_height_, _width_, _height_, _ratio_.

A _ratio_ constraint should be represented as width divided by height. This can be specified either by a statement like `3/2` or a float like `1.5`:

    'avatar' => 'dimensions:ratio=3/2'

Since this rule requires several arguments, you may use the `Rule::dimensions` method to fluently construct the rule:

    use Illuminate\Validation\Rule;

    Validator::make($data, [
        'avatar' => [
            'required',
            Rule::dimensions()->maxWidth(1000)->maxHeight(500)->ratio(3 / 2),
        ],
    ]);

<a name="rule-distinct"></a>
#### distinct

When working with arrays, the field under validation must not have any duplicate values.

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => [
        ['id' => 1],
        ['id' => 2],
        ['id' => 3],
    ]
];

$validator = Validator::make($data, [
    'field.*.id' => 'distinct',
]);

$validator->passes();
`
}
```

    'foo.*.id' => 'distinct'

<a name="rule-email"></a>
#### email

The field under validation must be formatted as an e-mail address. Under the hood, this validation rule makes use of the [`egulias/email-validator`](https://github.com/egulias/EmailValidator) package for validating the email address. By default the `RFCValidation` validator is applied, but you can apply other validation styles as well:


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'marcel@beyondco.de'
];

$validator = Validator::make($data, [
    'field' => 'email',
]);

$validator->passes();
`
}
```

    'email' => 'email:rfc,dns'

The example above will apply the `RFCValidation` and `DNSCheckValidation` validations. Here's a full list of validation styles you can apply:

```
- `rfc`: `RFCValidation`
- `strict`: `NoRFCWarningsValidation`
- `dns`: `DNSCheckValidation`
- `spoof`: `SpoofCheckValidation`
- `filter`: `FilterEmailValidation`
```

The `filter` validator, which uses PHP's `filter_var` function under the hood, ships with Laravel and is Laravel's pre-5.8 behavior. The `dns` and `spoof` validators require the PHP `intl` extension.

<a name="rule-ends-with"></a>
#### ends_with:_foo_,_bar_,...

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'marcel@beyondco.de'
];

$validator = Validator::make($data, [
    'field' => 'ends_with:beyondco.de',
]);

$validator->passes();
`
}
```
The field under validation must end with one of the given values.

<a name="rule-exists"></a>
#### exists:_table_,_column_


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'marcel@beyondco.de'
];

User::create([
    'name' => 'Marcel',
    'email' => 'marcel@beyondco.de',
    'password' => 'test',
]);

$validator = Validator::make($data, [
    'field' => 'exists:users,email',
]);

$validator->passes();
`
}
```
The field under validation must exist on a given database table.

#### Basic Usage Of Exists Rule

    'state' => 'exists:states'

If the `column` option is not specified, the field name will be used.

#### Specifying A Custom Column Name

    'state' => 'exists:states,abbreviation'

Occasionally, you may need to specify a specific database connection to be used for the `exists` query. You can accomplish this by prepending the connection name to the table name using "dot" syntax:

    'email' => 'exists:connection.staff,email'

Instead of specifying the table name directly, you may specify the Eloquent model which should be used to determine the table name:

    'user_id' => 'exists:App\User,id'

If you would like to customize the query executed by the validation rule, you may use the `Rule` class to fluently define the rule. In this example, we'll also specify the validation rules as an array instead of using the `|` character to delimit them:

    use Illuminate\Validation\Rule;

    Validator::make($data, [
        'email' => [
            'required',
            Rule::exists('staff')->where(function ($query) {
                $query->where('account_id', 1);
            }),
        ],
    ]);

<a name="rule-file"></a>
#### file

The field under validation must be a successfully uploaded file.

<a name="rule-filled"></a>
#### filled


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'test'
];

$validator = Validator::make($data, [
    'field' => 'filled',
]);

$validator->passes();
`
}
```

The field under validation must not be empty when it is present.

<a name="rule-gt"></a>
#### gt:_field_


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 10,
    'other_field' => 1,
];

$validator = Validator::make($data, [
    'field' => 'gt:other_field',
]);

$validator->passes();
`
}
```

The field under validation must be greater than the given _field_. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the [`size`](#rule-size) rule.

<a name="rule-gte"></a>
#### gte:_field_


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 10,
    'other_field' => 1,
];

$validator = Validator::make($data, [
    'field' => 'gte:other_field',
]);

$validator->passes();
`
}
```

The field under validation must be greater than or equal to the given _field_. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the [`size`](#rule-size) rule.

<a name="rule-image"></a>
#### image

The file under validation must be an image (jpeg, png, bmp, gif, svg, or webp)

<a name="rule-in"></a>
#### in:_foo_,_bar_,...



```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'CLI',
];

$validator = Validator::make($data, [
    'field' => [
        Illuminate\Validation\Rule::in(['HTTP', 'CLI'])
    ]
]);

$validator->passes();
`
}
```
The field under validation must be included in the given list of values. Since this rule often requires you to `implode` an array, the `Rule::in` method may be used to fluently construct the rule:

    use Illuminate\Validation\Rule;

    Validator::make($data, [
        'zones' => [
            'required',
            Rule::in(['first-zone', 'second-zone']),
        ],
    ]);

<a name="rule-in-array"></a>
#### in_array:_anotherfield_.*


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'CLI',
    'other_field' => ['HTTP', 'CLI']
];

$validator = Validator::make($data, [
    'field' => 'in_array:other_field',
]);

$validator->passes();
`
}
```

The field under validation must exist in _anotherfield_'s values.

<a name="rule-integer"></a>
#### integer


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 123,
];

$validator = Validator::make($data, [
    'field' => 'integer',
]);

$validator->passes();
`
}
```

The field under validation must be an integer.


<a name="rule-ip"></a>
#### ip

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '127.0.0.1',
];

$validator = Validator::make($data, [
    'field' => 'ip',
]);

$validator->passes();
`
}
```
The field under validation must be an IP address.

#### ipv4


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '127.0.0.1',
];

$validator = Validator::make($data, [
    'field' => 'ipv4',
]);

$validator->passes();
`
}
```
The field under validation must be an IPv4 address.

#### ipv6


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '2001:db8::8a2e:370:7334',
];

$validator = Validator::make($data, [
    'field' => 'ipv6',
]);

$validator->passes();
`
}
```
The field under validation must be an IPv6 address.

<a name="rule-json"></a>
#### json

The field under validation must be a valid JSON string.

<a name="rule-lt"></a>
#### lt:_field_

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '10',
    'other_field' => '100',
];

$validator = Validator::make($data, [
    'field' => 'lt:other_field',
]);

$validator->passes();
`
}
```
The field under validation must be less than the given _field_. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the [`size`](#rule-size) rule.

<a name="rule-lte"></a>
#### lte:_field_


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '10',
    'other_field' => '100',
];

$validator = Validator::make($data, [
    'field' => 'lte:other_field',
]);

$validator->passes();
`
}
```
The field under validation must be less than or equal to the given _field_. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the [`size`](#rule-size) rule.

<a name="rule-max"></a>
#### max:_value_


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '10',
];

$validator = Validator::make($data, [
    'field' => 'max:10',
]);

$validator->passes();
`
}
```
The field under validation must be less than or equal to a maximum _value_. Strings, numerics, arrays, and files are evaluated in the same fashion as the [`size`](#rule-size) rule.

<a name="rule-mimetypes"></a>
#### mimetypes:_text/plain_,...

The file under validation must match one of the given MIME types:

    'video' => 'mimetypes:video/avi,video/mpeg,video/quicktime'

To determine the MIME type of the uploaded file, the file's contents will be read and the framework will attempt to guess the MIME type, which may be different from the client provided MIME type.

<a name="rule-mimes"></a>
#### mimes:_foo_,_bar_,...

The file under validation must have a MIME type corresponding to one of the listed extensions.

#### Basic Usage Of MIME Rule

    'photo' => 'mimes:jpeg,bmp,png'

Even though you only need to specify the extensions, this rule actually validates against the MIME type of the file by reading the file's contents and guessing its MIME type.

A full listing of MIME types and their corresponding extensions may be found at the following location: [https://svn.apache.org/repos/asf/httpd/httpd/trunk/docs/conf/mime.types](https://svn.apache.org/repos/asf/httpd/httpd/trunk/docs/conf/mime.types)

<a name="rule-min"></a>
#### min:_value_


```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '10',
];

$validator = Validator::make($data, [
    'field' => 'min:10',
]);

$validator->passes();
`
}
```
The field under validation must have a minimum _value_. Strings, numerics, arrays, and files are evaluated in the same fashion as the [`size`](#rule-size) rule.

<a name="rule-not-in"></a>
#### not_in:_foo_,_bar_,...

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => 'chocolate',
];

$validator = Validator::make($data, [
    'field' => [
        Illuminate\Validation\Rule::notIn(['sprinkles', 'cherries']),
    ],
]);

$validator->passes();
`
}
```
The field under validation must not be included in the given list of values. The `Rule::notIn` method may be used to fluently construct the rule:

    use Illuminate\Validation\Rule;

    Validator::make($data, [
        'toppings' => [
            'required',
            Rule::notIn(['sprinkles', 'cherries']),
        ],
    ]);

<a name="rule-not-regex"></a>
#### not_regex:_pattern_

The field under validation must not match the given regular expression.

Internally, this rule uses the PHP `preg_match` function. The pattern specified should obey the same formatting required by `preg_match` and thus also include valid delimiters. For example: `'email' => 'not_regex:/^.+$/i'`.

**Note:** When using the `regex` / `not_regex` patterns, it may be necessary to specify rules in an array instead of using pipe delimiters, especially if the regular expression contains a pipe character.

<a name="rule-nullable"></a>
#### nullable

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => null,
];

$validator = Validator::make($data, [
    'field' => 'nullable',
]);

$validator->passes();
`
}
```
The field under validation may be `null`. This is particularly useful when validating primitive such as strings and integers that can contain `null` values.

<a name="rule-numeric"></a>
#### numeric

```try-code
{
    mode: "cli",
    cliCode: `$data = [
    'field' => '10',
];

$validator = Validator::make($data, [
    'field' => 'numeric',
]);

$validator->passes();
`
}
```
The field under validation must be numeric.

<a name="rule-password"></a>
#### password

The field under validation must match the authenticated user's password. You may specify an authentication guard using the rule's first parameter:

    'password' => 'password:api'

<a name="rule-present"></a>
#### present

The field under validation must be present in the input data but can be empty.

<a name="rule-regex"></a>
#### regex:_pattern_

The field under validation must match the given regular expression.

Internally, this rule uses the PHP `preg_match` function. The pattern specified should obey the same formatting required by `preg_match` and thus also include valid delimiters. For example: `'email' => 'regex:/^.+@.+$/i'`.

**Note:** When using the `regex` / `not_regex` patterns, it may be necessary to specify rules in an array instead of using pipe delimiters, especially if the regular expression contains a pipe character.

<a name="rule-required"></a>
#### required

The field under validation must be present in the input data and not empty. A field is considered "empty" if one of the following conditions are true:

```
- The value is `null`.
- The value is an empty string.
- The value is an empty array or empty `Countable` object.
- The value is an uploaded file with no path.
```

<a name="rule-required-if"></a>
#### required_if:_anotherfield_,_value_,...

The field under validation must be present and not empty if the _anotherfield_ field is equal to any _value_.

If you would like to construct a more complex condition for the `required_if` rule, you may use the `Rule::requiredIf` method. This methods accepts a boolean or a Closure. When passed a Closure, the Closure should return `true` or `false` to indicate if the field under validation is required:

    use Illuminate\Validation\Rule;

    Validator::make($request->all(), [
        'role_id' => Rule::requiredIf($request->user()->is_admin),
    ]);

    Validator::make($request->all(), [
        'role_id' => Rule::requiredIf(function () use ($request) {
            return $request->user()->is_admin;
        }),
    ]);

<a name="rule-required-unless"></a>
#### required_unless:_anotherfield_,_value_,...

The field under validation must be present and not empty unless the _anotherfield_ field is equal to any _value_.

<a name="rule-required-with"></a>
#### required_with:_foo_,_bar_,...

The field under validation must be present and not empty _only if_ any of the other specified fields are present.

<a name="rule-required-with-all"></a>
#### required_with_all:_foo_,_bar_,...

The field under validation must be present and not empty _only if_ all of the other specified fields are present.

<a name="rule-required-without"></a>
#### required_without:_foo_,_bar_,...

The field under validation must be present and not empty _only when_ any of the other specified fields are not present.

<a name="rule-required-without-all"></a>
#### required_without_all:_foo_,_bar_,...

The field under validation must be present and not empty _only when_ all of the other specified fields are not present.

<a name="rule-same"></a>
#### same:_field_

The given _field_ must match the field under validation.

<a name="rule-size"></a>
#### size:_value_

The field under validation must have a size matching the given _value_. For string data, _value_ corresponds to the number of characters. For numeric data, _value_ corresponds to a given integer value. For an array, _size_ corresponds to the `count` of the array. For files, _size_ corresponds to the file size in kilobytes.

<a name="rule-starts-with"></a>
#### starts_with:_foo_,_bar_,...

The field under validation must start with one of the given values.

<a name="rule-string"></a>
#### string

The field under validation must be a string. If you would like to allow the field to also be `null`, you should assign the `nullable` rule to the field.

<a name="rule-timezone"></a>
#### timezone

The field under validation must be a valid timezone identifier according to the `timezone_identifiers_list` PHP function.

<a name="rule-unique"></a>
#### unique:_table_,_column_,_except_,_idColumn_

The field under validation must not exist within the given database table.

**Specifying A Custom Table / Column Name:**

Instead of specifying the table name directly, you may specify the Eloquent model which should be used to determine the table name:

    'email' => 'unique:App\User,email_address'

The `column` option may be used to specify the field's corresponding database column. If the `column` option is not specified, the field name will be used.

    'email' => 'unique:users,email_address'

**Custom Database Connection**

Occasionally, you may need to set a custom connection for database queries made by the Validator. As seen above, setting `unique:users` as a validation rule will use the default database connection to query the database. To override this, specify the connection and the table name using "dot" syntax:

    'email' => 'unique:connection.users,email_address'

**Forcing A Unique Rule To Ignore A Given ID:**

Sometimes, you may wish to ignore a given ID during the unique check. For example, consider an "update profile" screen that includes the user's name, e-mail address, and location. You will probably want to verify that the e-mail address is unique. However, if the user only changes the name field and not the e-mail field, you do not want a validation error to be thrown because the user is already the owner of the e-mail address.

To instruct the validator to ignore the user's ID, we'll use the `Rule` class to fluently define the rule. In this example, we'll also specify the validation rules as an array instead of using the `|` character to delimit the rules:

    use Illuminate\Validation\Rule;

    Validator::make($data, [
        'email' => [
            'required',
            Rule::unique('users')->ignore($user->id),
        ],
    ]);

> {note} You should never pass any user controlled request input into the `ignore` method. Instead, you should only pass a system generated unique ID such as an auto-incrementing ID or UUID from an Eloquent model instance. Otherwise, your application will be vulnerable to an SQL injection attack.

Instead of passing the model key's value to the `ignore` method, you may pass the entire model instance. Laravel will automatically extract the key from the model:

    Rule::unique('users')->ignore($user)

If your table uses a primary key column name other than `id`, you may specify the name of the column when calling the `ignore` method:

    Rule::unique('users')->ignore($user->id, 'user_id')

By default, the `unique` rule will check the uniqueness of the column matching the name of the attribute being validated. However, you may pass a different column name as the second argument to the `unique` method:

    Rule::unique('users', 'email_address')->ignore($user->id),

**Adding Additional Where Clauses:**

You may also specify additional query constraints by customizing the query using the `where` method. For example, let's add a constraint that verifies the `account_id` is `1`:

    'email' => Rule::unique('users')->where(function ($query) {
        return $query->where('account_id', 1);
    })

<a name="rule-url"></a>
#### url

The field under validation must be a valid URL.

<a name="rule-uuid"></a>
#### uuid

The field under validation must be a valid RFC 4122 (version 1, 3, 4, or 5) universally unique identifier (UUID).

<a name="conditionally-adding-rules"></a>
## Conditionally Adding Rules

#### Validating When Present

In some situations, you may wish to run validation checks against a field **only** if that field is present in the input array. To quickly accomplish this, add the `sometimes` rule to your rule list:

    $v = Validator::make($data, [
        'email' => 'sometimes|required|email',
    ]);

In the example above, the `email` field will only be validated if it is present in the `$data` array.

> {tip} If you are attempting to validate a field that should always be present but may be empty, check out [this note on optional fields](#a-note-on-optional-fields)

#### Complex Conditional Validation

Sometimes you may wish to add validation rules based on more complex conditional logic. For example, you may wish to require a given field only if another field has a greater value than 100. Or, you may need two fields to have a given value only when another field is present. Adding these validation rules doesn't have to be a pain. First, create a `Validator` instance with your _static rules_ that never change:

    $v = Validator::make($data, [
        'email' => 'required|email',
        'games' => 'required|numeric',
    ]);

Let's assume our web application is for game collectors. If a game collector registers with our application and they own more than 100 games, we want them to explain why they own so many games. For example, perhaps they run a game resale shop, or maybe they just enjoy collecting. To conditionally add this requirement, we can use the `sometimes` method on the `Validator` instance.

    $v->sometimes('reason', 'required|max:500', function ($input) {
        return $input->games >= 100;
    });

The first argument passed to the `sometimes` method is the name of the field we are conditionally validating. The second argument is the rules we want to add. If the `Closure` passed as the third argument returns `true`, the rules will be added. This method makes it a breeze to build complex conditional validations. You may even add conditional validations for several fields at once:

    $v->sometimes(['reason', 'cost'], 'required', function ($input) {
        return $input->games >= 100;
    });

> {tip} The `$input` parameter passed to your `Closure` will be an instance of `Illuminate\Support\Fluent` and may be used to access your input and files.

<a name="validating-arrays"></a>
## Validating Arrays

Validating array based form input fields doesn't have to be a pain. You may use "dot notation" to validate attributes within an array. For example, if the incoming HTTP request contains a `photos[profile]` field, you may validate it like so:

    $validator = Validator::make($request->all(), [
        'photos.profile' => 'required|image',
    ]);

You may also validate each element of an array. For example, to validate that each e-mail in a given array input field is unique, you may do the following:

    $validator = Validator::make($request->all(), [
        'person.*.email' => 'email|unique:users',
        'person.*.first_name' => 'required_with:person.*.last_name',
    ]);

Likewise, you may use the `*` character when specifying your validation messages in your language files, making it a breeze to use a single validation message for array based fields:

    'custom' => [
        'person.*.email' => [
            'unique' => 'Each person must have a unique e-mail address',
        ]
    ],

<a name="custom-validation-rules"></a>
## Custom Validation Rules

<a name="using-rule-objects"></a>
### Using Rule Objects

Laravel provides a variety of helpful validation rules; however, you may wish to specify some of your own. One method of registering custom validation rules is using rule objects. To generate a new rule object, you may use the `make:rule` Artisan command. Let's use this command to generate a rule that verifies a string is uppercase. Laravel will place the new rule in the `app/Rules` directory:

    php artisan make:rule Uppercase

Once the rule has been created, we are ready to define its behavior. A rule object contains two methods: `passes` and `message`. The `passes` method receives the attribute value and name, and should return `true` or `false` depending on whether the attribute value is valid or not. The `message` method should return the validation error message that should be used when validation fails:

    <?php

    namespace App\Rules;

    use Illuminate\Contracts\Validation\Rule;

    class Uppercase implements Rule
    {
        /**
         * Determine if the validation rule passes.
         *
         * @param  string  $attribute
         * @param  mixed  $value
         * @return bool
         */
        public function passes($attribute, $value)
        {
            return strtoupper($value) === $value;
        }

        /**
         * Get the validation error message.
         *
         * @return string
         */
        public function message()
        {
            return 'The :attribute must be uppercase.';
        }
    }

You may call the `trans` helper from your `message` method if you would like to return an error message from your translation files:

    /**
     * Get the validation error message.
     *
     * @return string
     */
    public function message()
    {
        return trans('validation.uppercase');
    }

Once the rule has been defined, you may attach it to a validator by passing an instance of the rule object with your other validation rules:

    use App\Rules\Uppercase;

    $request->validate([
        'name' => ['required', 'string', new Uppercase],
    ]);

<a name="using-closures"></a>
### Using Closures

If you only need the functionality of a custom rule once throughout your application, you may use a Closure instead of a rule object. The Closure receives the attribute's name, the attribute's value, and a `$fail` callback that should be called if validation fails:

    $validator = Validator::make($request->all(), [
        'title' => [
            'required',
            'max:255',
            function ($attribute, $value, $fail) {
                if ($value === 'foo') {
                    $fail($attribute.' is invalid.');
                }
            },
        ],
    ]);

<a name="using-extensions"></a>
### Using Extensions

Another method of registering custom validation rules is using the `extend` method on the `Validator` [facade](/docs/{{version}}/facades). Let's use this method within a [service provider](/docs/{{version}}/providers) to register a custom validation rule:

    <?php

    namespace App\Providers;

    use Illuminate\Support\ServiceProvider;
    use Illuminate\Support\Facades\Validator;

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
            Validator::extend('foo', function ($attribute, $value, $parameters, $validator) {
                return $value == 'foo';
            });
        }
    }

The custom validator Closure receives four arguments: the name of the `$attribute` being validated, the `$value` of the attribute, an array of `$parameters` passed to the rule, and the `Validator` instance.

You may also pass a class and method to the `extend` method instead of a Closure:

    Validator::extend('foo', 'FooValidator@validate');

#### Defining The Error Message

You will also need to define an error message for your custom rule. You can do so either using an inline custom message array or by adding an entry in the validation language file. This message should be placed in the first level of the array, not within the `custom` array, which is only for attribute-specific error messages:

    "foo" => "Your input was invalid!",

    "accepted" => "The :attribute must be accepted.",

    // The rest of the validation error messages...

When creating a custom validation rule, you may sometimes need to define custom placeholder replacements for error messages. You may do so by creating a custom Validator as described above then making a call to the `replacer` method on the `Validator` facade. You may do this within the `boot` method of a [service provider](/docs/{{version}}/providers):

    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        Validator::extend(...);

        Validator::replacer('foo', function ($message, $attribute, $rule, $parameters) {
            return str_replace(...);
        });
    }

<a name="implicit-extensions"></a>
### Implicit Extensions

By default, when an attribute being validated is not present or contains an empty string, normal validation rules, including custom extensions, are not run. For example, the [`unique`](#rule-unique) rule will not be run against an empty string:

    $rules = ['name' => 'unique:users,name'];

    $input = ['name' => ''];

    Validator::make($input, $rules)->passes(); // true

For a rule to run even when an attribute is empty, the rule must imply that the attribute is required. To create such an "implicit" extension, use the `Validator::extendImplicit()` method:

    Validator::extendImplicit('foo', function ($attribute, $value, $parameters, $validator) {
        return $value == 'foo';
    });

> {note} An "implicit" extension only _implies_ that the attribute is required. Whether it actually invalidates a missing or empty attribute is up to you.

#### Implicit Rule Objects

If you would like a rule object to run when an attribute is empty, you should implement the `Illuminate\Contracts\Validation\ImplicitRule` interface. This interface serves as a "marker interface" for the validator; therefore, it does not contain any methods you need to implement.
