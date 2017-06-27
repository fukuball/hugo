+++
title = "Laravel 學習筆記 Lesson 5"
slug = "laravel-xue-xi-bi-ji-lesson-5"
date = "2014-09-09T12:58:07.000Z"
url = "/2014/09/09/laravel-xue-xi-bi-ji-lesson-5"
+++

## 在 Laravel 中使用 Oauth

目前網站使用其他社群網站帳號授權登入的功能非常常見，其實這樣的登入機制是使用 <a href="http://zh.wikipedia.org/wiki/OAuth" target="_blank">Oauth</a> 這種開放授權標準，只要實作 Oauth 這個標準，我們就可以很方便又相對安全地分享使用者的資料。

在 Laravel 中也可以透過 <a href="https://github.com/artdarek/oauth-4-laravel" target="_blank">artdarek/oauth-4-laravel</a> 這個套件來使用 Oauth。

### 安裝 artdarek/oauth-4-laravel

我們可以使用 composer 的方式來安裝 artdarek/oauth-4-laravel，請在 `composer.josn` 中的 `require` 加入以下內容：

```language-json
"require": {
  "artdarek/oauth-4-laravel": "dev-master"
}
```

然後執行以下指令使用 composer 將套件安裝好：

```language-bash
$ composer update
```

### 註冊使用 artdarek/oauth-4-laravel 套件

安裝完後還需要做一些設定，請打開 `app/config/app.php` 檔案，分別在 `providers` 及 `aliases` 中註冊要使用 `artdarek/oauth-4-laravel` 套件：

```language-php
'providers' => array(
    // ...

    'Artdarek\OAuth\OAuthServiceProvider'
)
```

```language-php
'aliases' => array(
    // ...

    'OAuth' => 'Artdarek\OAuth\Facade\OAuth',
)
```

### 產生並修改設定檔

Oauth 的機制中需要先向資料提供網站註冊並取得 API Key 及 Token，所以勢必要有一個地方記錄這些 API Key 及 Token。

首先我們先使用以下指令告訴 `artdarek/oauth-4-laravel` 產生設定檔：

```language-bash
$ php artisan config:publish artdarek/oauth-4-laravel
```

設定檔產生的位置在 `app/config/packages/artdarek/oauth-4-laravel/config.php`，打開它，將 facebook 給的 `app id` 及 `app secret` 填入：

```language-php
<?php
return array( 

    /**
     * Storage
     */
    'storage' => 'Session', 

    /**
     * Consumers
     */
    'consumers' => array(

        /**
         * Facebook
         */
        'Facebook' => array(
            'client_id'     => '',
            'client_secret' => '',
            'scope'         => array(),
        ),      

    )

);
```

### 以 Facebook 登入為例

接下來我們就可以試作看看 Facebook 登入的功能，首先增加一條 Route 規則：

```language-php
Route::get('/fb-login', 'AuthController@fbLogin');
```

然後在對應的 Controller 增加對應的 method 處理功能邏輯，範例程式碼如下：

```language-php
    public function fbLogin() {

        // get data from input
        $code = Input::get('code');
        // get fb service
        $fb = OAuth::consumer('Facebook');

        // check if code is valid

        // if code is provided get user data and sign in
        if (!empty($code)) {

            // This was a callback request from facebook, get the token
            $token = $fb->requestAccessToken($code);

            // Send a request with it
            $result = json_decode($fb->request('/me'), true);

            $facebook_user_id   = $result['id'];
            $user_name          = $result['name'];
            $user_email         = $result['email'];
            $user_avatar_url    = "http://graph.facebook.com/".$facebook_user_id."/picture?type=large";

            $user_obj = User::where('email', '=', $user_email)->first();

            if (empty($user_obj)) {

                // create user
                $user_obj = new User;
                $user_obj->name = $user_name;
                $user_obj->email = $user_email;
                $user_obj->password = Hash::make(str_random(8));
                $user_obj->save();

                $user_id = $user_obj->id;

            }

            Auth::login($user_obj);

            return Redirect::to('/');


        } else {

            // get fb authorization
            $url = $fb->getAuthorizationUri();

            // return to facebook login url
            return Redirect::to((string)$url);

        }

    }
```

就這樣就可以完成 Laravel 上使用 Facebook Oauth 登入的功能了！真簡單！
