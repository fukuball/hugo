+++
title = "Auth and Test"
slug = "auth-and-test"
date = "2016-02-03T18:27:22.000Z"
url = "/2016/02/03/auth-and-test"
draft = true
+++

```
php artisan migrate
```

```
php artisan make:auth
```

- welcome.blade.php - the public welcome page
- home.blade.php - the dashboard for logged-in users
- auth/login.blade.php - the login page
- auth/register.blade.php - the register/signup page
- auth/passwords/email.blade.php - the password reset confirmation page
- auth/passwords/reset.blade.php - the password reset prompt page
- auth/emails/password.blade.php - the password reset email

```
Route::group(['middleware' => 'web'], function () {
    Route::auth();

    Route::get('/home', 'HomeController@index');
});
```

```
// Authentication Routes...
$this->get('login', 'Auth\AuthController@showLoginForm');
$this->post('login', 'Auth\AuthController@login');
$this->get('logout', 'Auth\AuthController@logout');

// Registration Routes...
$this->get('register', 'Auth\AuthController@showRegistrationForm');
$this->post('register', 'Auth\AuthController@register');

// Password Reset Routes...
$this->get('password/reset/{token?}', 'Auth\PasswordController@showResetForm');
$this->post('password/email', 'Auth\PasswordController@sendResetLinkEmail');
$this->post('password/reset', 'Auth\PasswordController@reset');
```

```
composer require laravel/socialite
```

```
	public function testLoginPage()
    {
        $this->visit('/')
             ->click('Login')
             ->seePageIs('/login');
    }

    public function testNewUserRegistration()
    {

        $user = factory(App\User::class)->make();

        $this->visit('/register')
             ->type($user->name, 'name')
             ->type($user->email, 'email')
             ->type($user->password, 'password')
             ->type($user->password, 'password_confirmation')
             ->press('Register')
             ->seePageIs('/home');


        $this->seeInDatabase('users', ['email' => $user->email]);

    }

    public function testLoginHeader()
    {

        $user = factory(App\User::class)->make();

        $this->actingAs($user)
             ->visit('/')
             ->see($user->name);

    }
```

