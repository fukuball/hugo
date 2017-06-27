+++
title = "Laravel 學習筆記 Lesson 2"
slug = "laravel-xue-xi-bi-ji-lesson-2"
date = "2014-08-13T20:17:32.000Z"
url = "/2014/08/13/laravel-xue-xi-bi-ji-lesson-2"
+++

### 設定 Laravel App

剛裝好 Laravel，其實 Laravel 就可以正常運作了，但有一些基本設定還是先設定好，這樣可以避免後來遇到一些問題。

首先修改 `app/config/app.php` 檔案：

```language-php
'timezone' => 'UTC'
```

改為：
	
```language-php
'timezone' => 'Asia/Taipei'
```

另外在開發中如果希望可以看到完整的 Debug 內容，可以將 Debug 打開：

```language-php
'debug' => false
```

改為：

```language-php
'debug' => true
```

### 設定 Laravel 資料庫

我們需要設定好資料庫的連線資訊，Laravel 預設使用 MySQL 資料庫，所以我們先修改 `app/config/database.php` 檔案中 MySQL 的連線資訊部分：

```language-php
'mysql' => array(
	'driver'    => 'mysql',
	'host'      => 'localhost',
	'database'  => 'database_name',
	'username'  => 'database_username',
	'password'  => 'database_password',
	'charset'   => 'utf8',
	'collation' => 'utf8_unicode_ci',
	'prefix'    => '',
)
```
    
將 `host、database、username、password` 改成所使用的資料庫相關資訊。


### 設定 Laravel Routing 初探

使用者如何進入 Laravel App 的設定都定義在 `app/routes.php` 中，一安裝好 Laravel 時，`app/routes.php` 就已經有定義一條規則：

```language-php
Route::get('/', function()
{
	return View::make('hello');
});
```

這個意思是，當使用者輸入 `/` 這個網址時，Laravel 就會回應 hello 這個 View 給使用者。

通常我們都會希望除了 `/` 這個網址可以進入首頁之外，`/index.html` 也會希望可以正常進入首頁，所以我們就要自己加入這個規則：

```language-php
Route::get('/', function()
{
	return View::make('hello');
});
    
Route::get('/index.html', function()
{
	return View::make('hello');
});
```
    
### 使用 Laravel Controller

目前我們並沒有使用到 Controller，而是直接將程式內容塞在每個 Routing Rule 裡面，將來網站功能變多，`routes.php` 的內容就會變得很龐大，這樣並不是一個好的架構。

所以我們需要將功能邏輯的部分改寫在 Controller 裡，例如：

```language-php
Route::get('/', 'HomeController@getIndex');
```

如此， `/` 這個網址的程式功能及邏輯就可以分離至 `HomeController` 中的 static method `getIndex` 了。

然後我們在 `app/controller/HomeController.php` 裡加上 `getIndex` 的內容，如下：

```language-php
class HomeController extends BaseController {

	public function getIndex()
	{
		return View::make('index');
	}

}
```

### 範例網頁使用 bootstrap、fontawesome

Controller 中寫的 `View::make('index')` 意思就是會去將 `app/views/index.blade.php` 這個網頁內容包含進來，所以我們需要新增 `app/views/index.blade.php` 這個網頁，我們會使用 bootstrap 及 fontawesome 來製作我們的範例網頁：

```language-markup	
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <meta name="description" content="">
        <meta name="author" content="">
        <link rel="icon" href="/image/favicon.ico">
        <title>Titel</title>
        <!-- Bootstrap core CSS -->
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link href="//maxcdn.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css" rel="stylesheet">
        <!-- Custom styles for this template -->
        <link href="/stylesheet/pinhere.css" rel="stylesheet">
        <!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
        <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
        <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
        <![endif]-->
    </head>
    <body>
    	<div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
        	<div class="container">
            	<div class="navbar-header">
                	<button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                    	<span class="sr-only">Toggle navigation</span>
                    	<span class="icon-bar"></span>
                    	<span class="icon-bar"></span>
                    	<span class="icon-bar"></span>
                	</button>
                	<a class="navbar-brand" href="#">Project name</a>
            	</div>
            	<div class="collapse navbar-collapse">
                	<ul class="nav navbar-nav">
                    	<li class="active"><a href="#">Home</a></li>
                    	<li><a href="#about">About</a></li>
                    	<li><a href="#contact">Contact</a></li>
                	</ul>
            	</div><!--/.nav-collapse -->
        	</div>
    	</div>
    	<div class="container">
        	<div class="starter-template">
        		<h1>Bootstrap starter template</h1>
        		<p class="lead">Use this document as a way to quickly start any new project.<br> All you get is this text and a mostly barebones HTML document.</p>
    		</div>
    	</div><!-- /.container -->
    	<!-- Bootstrap core JavaScript
    ================================================== -->
    	<!-- Placed at the end of the document so the pages load faster -->
    	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
    	<!-- Latest compiled and minified JavaScript -->
    	<script src="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
    </body>
</html>
```

### 將 layout 及頁面內容分開來

由於許多頁面我們都會用到相同的排版佈局，比如可能上面都有 header，所以我們可以將這樣的佈局抽離開來，讓每個網頁都可以繼承同樣的排版佈局。首先我們新增 `app/views/layouts/layout.blade.php` 這個檔案，內容如下：

```language-markup
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <meta name="description" content="">
        <meta name="author" content="">
        <link rel="icon" href="/image/favicon.ico">
        <title>Title</title>
        <!-- Bootstrap core CSS -->
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link href="//maxcdn.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css" rel="stylesheet">
        <!-- Custom styles for this template -->
        <link href="/stylesheet/pinhere.css" rel="stylesheet">
        <!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
        <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
        <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
        <![endif]-->
    </head>
    <body>
    <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
        <div class="container">
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
                <a class="navbar-brand" href="#">Project name</a>
            </div>
            <div class="collapse navbar-collapse">
                <ul class="nav navbar-nav">
                    <li class="active"><a href="#">Home</a></li>
                    <li><a href="#about">About</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </div><!--/.nav-collapse -->
        </div>
    </div>
    <div class="container">
        @yield('content')
    </div><!-- /.container -->
    <!-- Bootstrap core JavaScript
    ================================================== -->
    <!-- Placed at the end of the document so the pages load faster -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
    <!-- Latest compiled and minified JavaScript -->
    <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
    </body>
</html>
```

我們將每個網頁會改變的部分改成 `@yield('content')`，如此原來的 `app/views/index.blade.php` 內容就可以改成如下：

```language-php
@extends('layouts.layout')

@section('content')
    <div class="starter-template">
        <h1>Bootstrap starter template</h1>
        <p class="lead">Use this document as a way to quickly start any new project.<br> All you get is this text and a mostly barebones HTML document.</p>
    </div>
@stop
```

我們可以直接繼承 `app/views/layouts/layout.blade.php` 的佈局架構，並把 `@yield('content')` 換成 `@section('content')` 中間的內容，將 layout 及頁面內容分開來我們可以更方便地修改 View 的內容。