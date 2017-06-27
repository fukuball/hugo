+++
title = "Laravel 學習筆記 Lesson 14"
slug = "laravel-xue-xi-bi-ji-lesson-14"
date = "2014-11-04T08:11:01.000Z"
url = "/2014/11/04/laravel-xue-xi-bi-ji-lesson-14"
draft = true
+++

### 忘記密碼

use Illuminate\Auth\Reminders\RemindableTrait;
use Illuminate\Auth\Reminders\RemindableInterface;

class User extends Eloquent implements RemindableInterface {

    use RemindableTrait;

}

php artisan auth:reminders-table

php artisan migrate

php artisan auth:reminders-controller

Route::get('/remind', 'RemindersController@getRemind');

public function getRemind()
	{
		return View::make('password.remind');
	}
    
<form action="/remind" method="POST">
    <input type="email" name="email">
    <input type="submit" value="Send Reminder">
</form>

Route::post('/remind', 'RemindersController@postRemind');

Password::remind(Input::only('email'), function($message)
{
    $message->subject('Password Reminder');
});

Route::get('/password/reset/{token}', 'RemindersController@getReset');

<form class="form" role="form" action="/password/reset" method="POST">
    <input class="form-control" type="hidden" name="token" value="{{ $token }}">
    <label class="control-label">Email</label>
    <input class="form-control" type="email" name="email">
    <label class="control-label">新密碼</label>
    <input class="form-control" type="password" name="password">
    <label class="control-label">確認新密碼</label>
    <input class="form-control" type="password" name="password_confirmation">
    <button class="btn btn-primary" type="submit">Reset Password</button>
</form>

Route::post('/password/reset', 'RemindersController@postReset');