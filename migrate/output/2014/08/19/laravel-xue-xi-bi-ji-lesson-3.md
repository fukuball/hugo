+++
title = "Laravel 學習筆記 Lesson 3"
slug = "laravel-xue-xi-bi-ji-lesson-3"
date = "2014-08-19T11:43:47.000Z"
url = "/2014/08/19/laravel-xue-xi-bi-ji-lesson-3"
+++

### 如何新增資料表及 Model - 以 Users 為例

我們使用 Laravel 的遷移(migration)系統來建立資料表以保存我們的資料。遷移記錄著資料庫的改變歷程，這讓團隊成員間的資訊分享更為簡單。

接下來，我們來創建遷移檔，我們使用 Artisan CLI。在專案的根目錄下，在終端裡執行下列指令：

```language-bash
php artisan migrate:make create_users_table
```

然後，在 `app/database/migrations` 目錄下找到產生的遷移檔。檔案中有一個包含了兩個方法 `up` 和 `down` 的類別。在 `up` 方法中，你必須表明你要對你的資料表做哪些更動，而在 `down` 的方法裡，你只要回復這些更動。

我們定義一個遷移檔如下：

```language-php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateUsersTable extends Migration {

	/**
	 * Run the migrations.
	 *
	 * @return void
	 */
	public function up()
	{
		Schema::create('users', function($table)
	    {
	        $table->increments('id');
	        $table->string('email')->unique();
	        $table->string('name');
	        $table->string('password', 60);
	        $table->string('remember_token', 100);
	        $table->timestamps();
	    });
	}

	/**
	 * Reverse the migrations.
	 *
	 * @return void
	 */
	public function down()
	{
		Schema::drop('users');
	}

}
```

然後我們從終端裡透過 migrate 指令來執行遷移動作。在專案的根目錄裡執行下列指令：

```language-bash
php artisan migrate --force
```

這樣我們就可以建好 Users 資料表了，開始放些資料進去吧。

### 新增 User Model Class

當建立好資料表，我們需要在 `app/models` 底下新增一個資料表所對應的 Model Class，通常 users 資料表，我們會新增一個命名為 User 的 Model Class，檔名為 `app/models/User.php`，資料表用小寫複數命名，Model 用單數首字母駝峰式命名，Model 內容如下：

```language-php
<?php

use Illuminate\Auth\UserTrait;
use Illuminate\Auth\UserInterface;
use Illuminate\Auth\Reminders\RemindableTrait;
use Illuminate\Auth\Reminders\RemindableInterface;

class User extends Eloquent implements UserInterface, RemindableInterface {

	use UserTrait, RemindableTrait;

	/**
	 * The database table used by the model.
	 *
	 * @var string
	 */
	protected $table = 'users';

	/**
	 * The attributes excluded from the model's JSON form.
	 *
	 * @var array
	 */
	protected $hidden = array('password', 'remember_token');

}

```

### 製作表單

新增一個新的 Routing 規則：

```language-php
Route::get('/user/create-form', 'UserController@getCreateForm');
```

實作 `UserController` 中的 `getCreateForm` 方法：

```language-php
public function getCreateForm()
{

	return View::make('user.user-create-form');

};
```

然後新增 `app/views/user/user-create-form.blade.php`，內容如下：

```language-php
@extends('layouts.layout')

@section('content')
<?php

$old_name = '';
$old_email = '';
$old_password = '';

if (!empty(Input::old())) {
    $old_name = Input::old('input_name');
    $old_email = Input::old('input_email');
    $old_password = Input::old('input_password');
}

?>
<div class="starter-template">
    @if ($errors->has())
        <div class="alert alert-danger" role="alert">
        @foreach ($errors->all() as $error)
            {{ $error }}<br/>
        @endforeach
        </div>
    @endif
    <form class="form-horizontal" role="form" method="post" action="/user/create">
        {{ Form::token() }}
        <div class="form-group @if ($errors->has('name')) has-error @endif">
            <label for="input_name" class="col-sm-2 control-label">
                Name
            </label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="input_name" name="input_name" placeholder="Name" value="{{ $old_name }}">
                @if ($errors->has('name')) <p class="help-block">{{ $errors->first('name') }}</p> @endif
            </div>
        </div>
        <div class="form-group @if ($errors->has('email')) has-error @endif">
            <label for="input_email" class="col-sm-2 control-label">
                Email
            </label>
            <div class="col-sm-10">
                <input type="email" class="form-control" id="input_email" name="input_email" placeholder="Email" value="{{ $old_email }}">
                @if ($errors->has('email')) <p class="help-block">{{ $errors->first('email') }}</p> @endif
            </div>
        </div>
        <div class="form-group @if ($errors->has('password')) has-error @endif">
            <label for="input_password" class="col-sm-2 control-label">
                Password
            </label>
            <div class="col-sm-10">
                <input type="password" class="form-control" id="input_password" name="input_password" placeholder="Password" value="{{ $old_password }}">
                @if ($errors->has('password')) <p class="help-block">{{ $errors->first('password') }}</p> @endif
            </div>
        </div>
        <div class="form-group">
            <div class="col-sm-offset-2 col-sm-10">
                <button type="submit" class="btn btn-default">
                    Create
                </button>
            </div>
        </div>
    </form>
</div>
@stop
```

### 接收表單資料

由於在 `app/views/user/user-create-form.blade.php` 的表單所指定的 action url 是 post 到 `/user/create`，所以我們要新增 Routing 規則：

```language-php
Route::post('/user/create', array('before' => 'csrf', 'uses' => 'UserController@create'));
```

實作 `UserController` 中的 `create` 方法：

```language-php
public function create() {

    $input           = Input::all();
    $input_name      = $input['input_name'];
    $input_email     = $input['input_email'];
    $input_password  = $input['input_password'];
    $hashed_password = Hash::make($input_password);

    $validator = Validator::make(
        array(
            'name' => $input_name,
            'email' => $input_email,
            'password' => $input_password
        ),
        array(
            'name' => 'required',
            'email' => 'required|email|unique:users',
            'password' => 'required|min:8'
        )
    );

    if ($validator->fails()) {

        // get the error messages from the validator
        $messages = $validator->messages();

        // redirect our user back to the form with the errors from the validator
        return Redirect::to('/user/create-form')
                ->withInput()
                ->withErrors($validator);

    } else {

        $user           = new User;
        $user->name     = $input_name;
        $user->email    = $input_email;
        $user->password = $hashed_password;
        $user->save();

        return Redirect::to('/user/list');

    }

}
```

### csrf 驗證

CSRF/XSRF 全名 Cross Site Request Forgery 中文翻成「跨網站偽造請求」，而 CSRF 主要的攻擊行為就是利用當使用者合法取得網站使用認證後，透過某些方式偽造網站合法使用者的身份進行非法的存取動作，合法使用者即可能在不自覺的情況下被引導到駭客的攻擊網頁。

在現今的 Web Framework 幾乎都有很完善的 CSRF 驗證解決方案來解決 CSRF 的攻擊，Laravel 也不例外。

首先我們可以在 `app/routes.php` 中的 Routing Rules 中指定是否使用 CSRF 驗證，如：

```language-php
Route::post('/user/create', array('before' => 'csrf', 'uses' => 'UserController@create'));
```

當我們有指定要驗證 CSRF 時，Laravel 在進入 `UserController@create` 前就會先驗證 CSRF Token 是否合法，這個動作 Laravel 實作在 `app/filters.php`，內容如下：

```language-php
Route::filter('csrf', function()
{
	if (Session::token() != Input::get('_token'))
	{
		throw new Illuminate\Session\TokenMismatchException;
	}
});
```

我們可以在這邊修改 CSRF Token 驗證的動作。

由於 Laravel 在進入 `UserController@create` 前就會先驗證 CSRF Token 是否合法，我們需要在表單中傳入合法的 Token，產生合法 Token 的方法如下：

```language-php
{{ Form::token() }}
```

這樣 Laravel 就會自動在表單中插入含有合法 Token 的隱藏 input 標籤。

### 後端表單驗證

Laravel 有很方便且易讀的資料驗證方法，例如：

```language-php
$validator = Validator::make(
    array(
        'name' => $input_name,
        'email' => $input_email,
        'password' => $input_password
    ),
    array(
        'name' => 'required',
        'email' => 'required|email|unique:users',
        'password' => 'required|min:8'
    )
);
```

第一個 array 是放要驗證的資料值，有 name, email, password 需要驗證，第二個 array 則是 name, email, password 分別要符合哪些條件，比如 name 是 required，不能是空值，email 是 required 而且格式要符合 email 且在 users 表單中是唯一值，password 的條件則是 required 且最少要 8 個字元。

如此我們就可以很方便地驗證使用者輸入的資料，並且可讀性也非常好。

如果驗證失敗了，我們也可以將錯誤及提示回傳至頁面讓使用者知道：

```language-php
if ($validator->fails()) {

    // get the error messages from the validator
    $messages = $validator->messages();

    // redirect our user back to the form with the errors from the validator
    return Redirect::to('/user/create-form')
            ->withInput()
            ->withErrors($validator);

}
```

如此我們就可以在 `/user/create-form` 用以下的方式取得錯誤訊息及之前使用者輸入的值：

```language-php
if (!empty(Input::old())) {
    $old_name = Input::old('input_name');
    $old_email = Input::old('input_email');
    $old_password = Input::old('input_password');
}

@foreach ($errors->all() as $error)
    {{ $error }}<br/>
@endforeach
```


