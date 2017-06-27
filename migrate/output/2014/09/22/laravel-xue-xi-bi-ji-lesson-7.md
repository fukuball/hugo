+++
title = "Laravel 學習筆記 Lesson 7"
slug = "laravel-xue-xi-bi-ji-lesson-7"
date = "2014-09-22T18:53:42.000Z"
url = "/2014/09/22/laravel-xue-xi-bi-ji-lesson-7"
+++

### 刪除及軟刪除

寫網頁應用程式免不了需要做到一些刪除資料的功能，由於 Laravel 使用 ORM，要刪除資料非常容易，不用再特地寫 SQL Query，程式可讀性也非常好，例如：

```language-php
$user_obj = User::find(1);
$user_obj->delete();
```

如此就可以從資料庫中刪除編號 1 這筆 user 的資料。 

但有時我們會有這樣的需求，我們想要刪除資料，但不想要真的將資料從資料庫中刪除掉，這樣要怎麼做呢？

直覺的做法就是，自己新增一個欄位來標示資料是否被刪除，這樣基本上就可以做到這樣的功能，只是取資料時總是要多寫一個條件來篩選出沒有被標示成已刪除的資料，自己在程式中處理久了，會覺得有些麻煩，Laravel 有沒有一個比較好的解決方案呢？

這樣的功能在 Laravel 就叫做軟刪除，而且透過軟刪除後的資料在取資料時不會出現，不必再特地去 Query 中增加條件，Laravel 都幫你處理好了！

要怎麼在 Laravel 中使用軟刪除呢？

首先，我們先增加一個 migration 檔案：

```language-bash
php artisan migrate:make update_user_soft_delete
```

然後在 migration 檔案中使用 `softDeletes()` 幫 user table 增加軟刪除所需要的資料欄位，而實際上這個資料欄位的名稱是 `deleted_at`，請參考底下遷移檔內容：

```language-php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class UpdateUserSoftDelete extends Migration {

	/**
	 * Run the migrations.
	 *
	 * @return void
	 */
	public function up()
	{
		Schema::table('users', function($table)
		{

			$table->softDeletes();

		});
	}

	/**
	 * Reverse the migrations.
	 *
	 * @return void
	 */
	public function down()
	{
		Schema::table('users', function($table)
		{
		    $table->dropColumn('deleted_at');
		});
	}

}
```
然後我們執行 migration：

```language-bash
php artisan migrate --force
```

如此我們就準備好軟刪除所需要的資料欄位了。

接下來我們要將 User Model 增加軟刪除的功能，我們需要在 User Model 上方增加這一行 `use Illuminate\Database\Eloquent\SoftDeletingTrait;`，告訴 Laravel 我們要在這個 Model 使用軟刪除。

然後在 User Model 的內容中增加這兩行：`use SoftDeletingTrait;` 及 `protected $dates = ['deleted_at'];`，如此 User Model 的刪除方法就會變成軟刪除，範例如下：

```language-php
use Illuminate\Database\Eloquent\SoftDeletingTrait;

class User extends Eloquent {

    use SoftDeletingTrait;

    protected $dates = ['deleted_at'];

}
```

我們還是像以前一樣刪除資料：

```language-php
$user = User::find(1);
$user->delete();
```

資料會呈現刪除狀態，但卻不會從資料庫中消失，取資料時也不會取出這些被軟刪除的資料：

```language-php
$users = User::all();
// 軟刪除的資料不會出現
```

若真的想要一併取回列出軟刪除的資料也可以做到：

```language-php
$users = User::withTrashed()->get();
// 軟刪除的資料會出現
```

由於軟刪除的資料其實還存在資料庫中，我們可以將資料回復回來：

```language-php
$user = User::find(1);
$user->restore();
```

Laravel 的軟刪除功能真的很好用！





