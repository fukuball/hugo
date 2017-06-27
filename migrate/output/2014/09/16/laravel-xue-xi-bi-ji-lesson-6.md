+++
title = "Laravel 學習筆記 Lesson 6"
slug = "laravel-xue-xi-bi-ji-lesson-6"
date = "2014-09-16T07:09:07.000Z"
url = "/2014/09/16/laravel-xue-xi-bi-ji-lesson-6"
+++

### 設定 Table 之間 One to One 的關係

Laravel 中的 ORM 可以設定 model 之間的關係，這是關聯式資料庫非常重要的部分，在這邊將簡易說明如何設定 ORM 之間 One to One 的關係。

目前我們已經有 user 這個 table，之前也介紹過如何使用 facebook 登入，這邊我們想將 user id 與 facebook user id 之間的關係記到資料庫以方便未來使用。

首先我們使用 migration 新增一個 facebook_user_mappings 這個 table：

```language-bash
php artisan migrate:make create_facebook_user_mapping_table
```

遷移檔的內容如下：

```language-php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateFacebookUserMappingTable extends Migration {

	/**
	 * Run the migrations.
	 *
	 * @return void
	 */
	public function up()
	{
		Schema::create('facebook_user_mappings', function($table)
	    {
	        $table->increments('id');
	        $table->integer('facebook_user_id')->unique();
	        $table->integer('user_id');
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
		Schema::drop('facebook_user_mappings');
	}

}
```

然後執行 migration：

```language-bash
php artisan migrate --force
```

這樣就會建出 facebook_user_mappings 這個 table，接下來建立對應到 table 的 ORM Model：

```language-php
<?php

class FacebookUserMapping extends Eloquent {

    /**
     * The database table used by the model.
     *
     * @var string
     */
    protected $table = 'facebook_user_mappings';

}
```

這樣我們就可以在使用者使用 facebook 登入的時候將 user id 與 facebook user id 之間的對應關係記下來，範例程式碼如下：

```language-php
$facebook_user_mapping_obj = FacebookUserMapping::where('facebook_user_id', '=', $fb_user_id)->first();

if (!empty($user_id) &&  empty($facebook_user_mapping_obj)) {

    $facebook_user_mapping_obj = new FacebookUserMapping;
    $facebook_user_mapping_obj->facebook_user_id = $fb_user_id;
    $facebook_user_mapping_obj->user_id = $user_id;
    $facebook_user_mapping_obj->save();

}
```

由於一個使用者只能連結一個 facebook 帳號，所以 user table 與 facebook_user_mappings table 就是一種 One to One 的關係，如何在 Laravel 中的 ORM 設定 One to One 的關係呢？

首先我們在 User Model 增加一個 facebookUserMapping Method：

```language-php
public function facebookUserMapping() {
    return $this->hasOne('FacebookUserMapping', 'user_id', 'id');
    //return $this->hasOne('OtherModel', 'foreign_key', 'local_key');
}
```

裡面設定了 User Model 會 hasOne FacebookUserMapping，後面兩個參數分別代表 foreign_key 及 local_key，在這個例子中，foreign_key 就是 facebook_user_mappings 這個 table 中的 user_id 欄位，而 local_key 就是 user table 中的 id 這個欄位。

接下來在 FacebookUserMapping Model 增加 user 這個 Method：

public function user() {
    return $this->belongsTo('User', 'user_id', 'id');
    //$this->belongsTo('User', 'local_key', 'parent_key');
}

裡面設定了 FacebookUserMapping Model 會 belongsTo User Model，後面兩個參數分別代表 local_key 及 parent_key，在這個例子中，local_key 就是 facebook_user_mappings 這個 table 中的 user_id 欄位，而 parent_key 就是 user table 中的 id 這個欄位。

如此我們就設定好 User Model 與 FacebookUserMapping Model 之間的 One to One 對應關係了～

### 設定 Table 之間 One to One 的關係可以做什麼呢？

設定好 table 之間的 One to One 關係可以讓我們更方便地使用資料庫的資料，若果沒有設定 table 之間 One to One 的關係，我要取出 users 的 facebook_user_mappings 資料就要使用 Query Builder 來 Join 取出資料，比如：

```language-php
$results = DB::table('users')
			->join('facebook_user_mappings', 'users.id', '=', 'facebook_user_mappings.user_id')
            ->get();
print_r($results);
```

印出來的資料會像這樣：

```language-php
Array
(
    [0] => stdClass Object
        (
            [id] => 9
            [email] => fukuball@gmail.com
            [name] => Fukuball Lin
            [password] => $2y$10$rGCzZJVTuPM6kZmqj6XPIOGQu/1b1g1ewcxyQIcthtxotGUjWU25m
            [remember_token] => 4N7zVwiGp7QagMxwofyKGIx2VoxNcNtMYYTea19uUssAjn59q78uNIyOTQOP
            [created_at] => 2014-09-30 16:32:55
            [updated_at] => 2014-09-30 16:32:55
            [deleted_at] => 
            [facebook_user_id] => 1111111111
            [user_id] => 8
        )

)
```

只是單純地將資料從資料庫中取出來而已，如此就無法使用 ORM 的方式來操作資料。但如果建立了 One to One 關係，我們就可以使用 ORM 的方式來取出資料，比如：

```language-php
$users = User::all();
foreach($users as $user) {
    print_r($user->facebookUserMapping);
}
```

印出來的資料會像這樣：

```language-php
FacebookUserMapping Object
(
    [table:protected] => facebook_user_mappings
    [connection:protected] => 
    [primaryKey:protected] => id
    [perPage:protected] => 15
    [incrementing] => 1
    [timestamps] => 1
    [attributes:protected] => Array
        (
            [id] => 9
            [facebook_user_id] => 1111111111
            [user_id] => 8
            [created_at] => 2014-09-30 16:32:55
            [updated_at] => 2014-09-30 16:32:55
        )

    [original:protected] => Array
        (
            [id] => 9
            [facebook_user_id] => 1111111111
            [user_id] => 8
            [created_at] => 2014-09-30 16:32:55
            [updated_at] => 2014-09-30 16:32:55
        )

    [relations:protected] => Array
        (
        )

    [hidden:protected] => Array
        (
        )

    [visible:protected] => Array
        (
        )

    [appends:protected] => Array
        (
        )

    [fillable:protected] => Array
        (
        )

    [guarded:protected] => Array
        (
            [0] => *
        )

    [dates:protected] => Array
        (
        )

    [touches:protected] => Array
        (
        )

    [observables:protected] => Array
        (
        )

    [with:protected] => Array
        (
        )

    [morphClass:protected] => 
    [exists] => 1
)
```

如此取出來的資料會是一個完整的 FacebookUserMapping Model Object，而不只是單純的資料，這樣就可以直接使用寫在 FacebookUserMapping Model 裡的方便 method。

總結來說，如果可以設定 Model 之間的關係，未來在使用資料時會變得很方便，否則就會寫很多 Query 在程式碼中，程式會變得難以維護。但是如果是複雜的 Query 還是可以斟酌使用 Query Builder 來查詢資料。