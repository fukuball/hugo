+++
title = "Laravel 學習筆記 Lesson 4"
slug = "laravel-xue-xi-bi-ji-lesson-4"
date = "2014-08-26T19:17:55.000Z"
url = "/2014/08/26/laravel-xue-xi-bi-ji-lesson-4"
+++

### 如何登入

要讓使用者登入，你可以使用 `Auth::attempt` 方法：

```language-php
if (Auth::attempt(array('email' => $email, 'password' => $password)))
{
    return Redirect::intended('dashboard');
}
```

不過要使用這種登入使用者的語法需要讓 User Model 實作一些 Auth 介面，所以 User Model 看起來像這樣：

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

### 判斷使用者是否已登入

```language-php
if (Auth::check())
{
    // The user is logged in...
}
```

### 如何登出

```language-php
Auth::logout();
```

### 另外一種登入方法

有時我們不是透過帳號密碼讓使用者登入，比如使用 facebook 得到 token 之後，應該透過程式讓使用者自動登入，方法如下：

```language-php
$user = User::find(1);
Auth::login($user);
```