+++
title = "Laravel 學習筆記 Lesson 9-1"
slug = "laravel-xue-xi-bi-ji-lesson-9"
date = "2014-10-06T08:05:32.000Z"
url = "/2014/10/06/laravel-xue-xi-bi-ji-lesson-9"
+++

### 設定 Table 之間 One to Many 的關係

我們在 [Laravel 學習筆記 Lesson 6](http://blog.fukuball.com/laravel-xue-xi-bi-ji-lesson-6/) 曾經說明過如何設定 Laravel 中的 Model One to One 的關係，在這邊將簡易說明如何設定 ORM 之間 One to Many 的關係。

假設現在我們的資料有文章（Post）及文章評論（Comment），我們會先建立好文章的 Model 及 Comment 的 Model，通常一篇文章會有很多個評論，所以文章及評論就是一種一對多的關係。

要在 Laravel 中的 Model 建立一對多的關係非常簡易，首先我們在 Model Post Class 中設定好一對多的關係，範例程式碼如下：

```
class Post extends Eloquent {

    public function comments()
    {
        return $this->hasMany('Comment', 'post_id', 'id');
        //return $this->hasMany('model_name', 'foreign_key', 'local_key');
    }

}
```

裡面設定了 Post Model 會 hasMany Comment，後面兩個參數分別代表 foreign key 及 local key，在這個例子中，foreign key 就是 comment 這個 table 中的 post_id 欄位，而 local key 就是 post table 中的 id 這個欄位。

接下來在 Comment Model 增加 post 這個 Method：

```
class Comment extends Eloquent {

    public function post()
    {
        return $this->belongsTo('Post', 'post_id', 'id');
        //return $this->belongsTo('model_name', 'local_key', 'parent_key');
    }

}
```

裡面設定了 Comment Model 會 belongsTo Post Model，後面兩個參數分別代表 local key 及 parent key，在這個例子中，local key 就是 comment 這個 table 中的 post_id 欄位，而 parent key 就是 post 中的 id 這個欄位。

如此我們就設定好 Post Model 與 Comment Model 之間的 One to Many 對應關係了～

設定好 table 之間的 One to Many 關係可以讓我們更方便地使用資料庫的資料，若果沒有設定 table 之間 One to Many 的關係，我要取出 Post 的 comment 資料就要使用 Query Builder 來 Join 取出資料，但如果建立了 One to Many 關係，我們就可以使用 ORM 的方式來取出資料，比如：

```
$comments = Post::find(1)->comments;
```

總結來說，如果可以設定 Model 之間的關係，未來在使用資料時會變得很方便，否則就會寫很多 Query 在程式碼中，程式會變得難以維護。但是如果是複雜的 Query 還是可以斟酌使用 Query Builder 來查詢資料。