+++
title = "Laravel 4.2 to Laravel 5.2"
slug = "laravel-4-2-to-laravel-5-2"
date = "2016-01-19T17:01:29.000Z"
url = "/2016/01/19/laravel-4-2-to-laravel-5-2"
draft = true
+++

# Laravel 4.2 to Laravel 5.0

## Directory Structure

```
    app/commandd    => app/Console
    app/controllers => app/HTTP/Controllers

    app/models      => app/User.php
    app/start       => X

    app/lang        => resources/lang
    app/views       => resources/views

    config, database, tests, storage => root
```

## Form & HTML 

```
{!!
	Form::text('username');
!!}
```

--<n>--

## It's Gone

![](https://github.com/fukuball/laravel5-slide/raw/master/assets/gif/gone.gif)

--<n>--

## Form & HTML 

"laravelcollective/html": "~5.0"

config/app.php 

```
'providers' => [
	...

	Collective\Html\HtmlServiceProvider::class,
]

'aliases' => [
	...

    'Form'      => Collective\Html\FormFacade::class,
    'Html'      => Collective\Html\HtmlFacade::class,
]
```

--<n>--

## Blade Raw Tags

```
{{
}}
```

```
{!!
!!}
```

## FileSystem - Flysystem 
### config/filesystems.php

```

	'default' => 'local',

```

```
	'cloud' => 's3',

```


```php
$disk = Storage::disk('s3');

$contents = Storage::disk('local')->get('file.jpg')
```

--<n>--

### Cloud

```
use Illuminate\Contracts\Cloud;

class HomeController extends BaseController {
	public function index(Cloud $cloud) {

        $cloud->get('hello.text');
	}
}
``` 

--<n>--

## Socilate

--<n>--

# Laravel 5.0 to Laravel 5.1

## Namespace
### PSR-2

PSR-2 程式碼風格指南已經被 Laravel 框架採用為預設的風格指南。
![](https://github.com/fukuball/laravel5-slide/raw/master/assets/img/controller.png)

https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md

## Event Broadcasting

Laravel 讓你可以簡單的經由 websocket 連線來「廣播」你的事件。

## Middleware

## 測試翻修

```
public function testNewUserRegistration()
{
    $this->visit('/register')
         ->type('Taylor', 'name')
         ->check('terms')
         ->press('Register')
         ->seePageIs('/dashboard');
}
```

## 模型工廠

模型工廠讓你簡單的為 Eloquent 模型定義一組「預設」的屬性，並為你的測試或資料填充產生測試模型實例。模型工廠也使用進階的 Faker PHP 函式庫來產生隨機屬性的資料

```
$factory->define(App\User::class, function ($faker) {
    return [
        'name' => $faker->name,
        'email' => $faker->email,
        'password' => str_random(10),
        'remember_token' => str_random(10),
    ];
});
```

## 資料夾結構

app/Commands => app/Jobs
app/Handler => app/Listeners

# Laravel 5.1 to Laravel 5.1.11

登入授權機制改善

# Laravel 5.1.11 to 5.2

## Authentication Scaffolding

```
php artisan make:auth
```

## Middleware Groups

```
/**
 * The application's route middleware groups.
 *
 * @var array
 */
protected $middlewareGroups = [
    'web' => [
        \App\Http\Middleware\EncryptCookies::class,
    ],

    'api' => [
        'throttle:60,1',
    ],
];
```

```
Route::group(['middleware' => ['web']], function () {
    //
});
```

## Rate Limiting

```
Route::get('/api/users', ['middleware' => 'throttle:60,1', function () {
    //
}]);
```

## Array Validation

```
$validator = Validator::make($request->all(), [
    'person.*.email' => 'email|unique:users'
]);
```

```
'custom' => [
    'person.*.email' => [
        'unique' => 'Each person must have a unique e-mail address',
    ]
],
```

### CronJob

http://www.sitepoint.com/managing-cronjobs-with-laravel/
