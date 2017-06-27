+++
title = "Laravel 學習筆記 Lesson 8"
slug = "laravel-xue-xi-bi-ji-lesson-8"
date = "2014-09-30T10:06:02.000Z"
url = "/2014/09/30/laravel-xue-xi-bi-ji-lesson-8"
+++

### 上傳檔案到本機端

網站應用程式經常需要有上傳檔案的功能，在這邊介紹如何在 Laravel Framework 中上傳檔案到本機端。

其實現在大部份的網站應用程式都不會單純將上傳的檔案存到本機端，而是直接存到雲端的硬碟裡，例如存到 AWS，以避免應用程式的伺服器硬碟爆滿而造成整台網頁伺服器掛掉，不過如何上傳檔案到雲端硬碟和上傳檔案到本機端其實大同小異，日後我們會再介紹如何上傳至雲端硬碟。

### 上傳檔案表單

首先我們需要先製作一個上傳檔案的表單，上傳檔案表單與一般表單不同的地方在於上傳檔案表單需要多一個 property `enctype="multipart/form-data"`，如此才能夠順利上傳檔案，範例表單如下：

```
<form class="form-horizontal" method="post" action="/user/icon-upload" accept-charset="UTF-8" enctype="multipart/form-data">
	<input type="file" class="form-control" id="user_icon_file" name="user_icon_file" placeholder="上傳圖片" value="">
</form>
```

### 處理上傳檔案

首先我們新增一個表單所對應的請求 Routing Rule：

```
Route::post('/user/icon-upload','UserController@iconUpload');
```

然後在 Routing Rule 指定的 Controller 裡新增對應的方法，在這邊的例子為 iconUpload，範例如下：

```
public function iconUpload()
{
	$file = Input::file('user_icon_file');
	$extension = $file->getClientOriginalExtension();
    $file_name = strval(time()).str_random(5).'.'.$extension;
	
    $destination_path = public_path().'/user-upload/';

    if (Input::hasFile('user_icon_file')) {
    	$upload_success = $file->move($destination_path, $file_name);
        echo "img upload success!";
    } else {
        echo "img upload failed!";
    }
            
    $user_obj = Auth::user();
    $user_obj->user_icon = $file_name;
    $user_obj->save();
    
}
```

首先我們用 `$file = Input::file('user_icon_file')` 取得上傳檔案的相關資料，如果檔案相關的資料都會存在 `$file` 這個變數裡面，然後使用 `$file->getClientOriginalExtension()` 我們可以取得檔案的副檔名，為了避免上傳的檔案因為檔名相同而造成上傳檔案相互覆蓋，我們通常會重新產生新的檔案名稱，如 `$file_name = strval(time()).str_random(5).'.'.$extension`，記得副檔名也要附加在檔案名稱中。

接下來我們需要告訴 Laravel 我們要將上傳的檔案存在伺服器的哪的資料夾，這個例子是使用 `$destination_path = public_path().'/user-upload/'`，所以必須先在 app 中下這兩個指令新增放上傳檔案的資料夾：

```
$ mkdir public/user-upload
$ chmod -R 777 public/user-upload
```

使用 `Input::hasFile('user_icon_file')` 這個方法檢查檔案是否確實上傳後，`$upload_success = $file->move($destination_path, $file_name)` 這個方法就可以將檔案上傳至 `$destination_path` 並將檔案以 `$file_name` 重新命名。

記得最後要將 `$file_name` 這個資訊存下來，這樣未來才能將上傳的檔案顯示在網頁，如此就完成上傳檔案的功能了。


### 在網頁顯示上傳的圖片

由於我們已將上傳的圖片檔案上傳至 `public/user-upload` 這個資料夾，而資料庫裡又有記下圖片檔名的資訊，如此我們可以很容易地得到圖片的公開網址，讓網頁可以順利顯示圖片。

範例如下：

```
<img src="/user-upload/{{ $user_obj->user_icon }}" >
```

由於大部份的網頁伺服器都會將 Laravel 的根目錄指向 public 這個資料夾，所以圖片網址就不需要再有 public 了。

如果之前有寫過 PHP，會發現 Laravel 的上傳檔案跟 PHP 的寫法很不一樣，主要是 Laravel 將上傳檔案的相關功能另外再包裝了起來，如此才不會發生一些非預期的意外，不過基本上概念是很累似的。


