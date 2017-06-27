+++
title = "Laravel 學習筆記 Lesson 9-2"
slug = "laravel-xue-xi-bi-ji-lesson-9-2"
date = "2015-04-01T14:16:39.000Z"
url = "/2015/04/01/laravel-xue-xi-bi-ji-lesson-9-2"
+++

### 設定 Table 之間 Many to Many 的關係

我們在 [Laravel 學習筆記 Lesson 6](http://blog.fukuball.com/laravel-xue-xi-bi-ji-lesson-6/) 曾經說明過如何設定 Laravel 中的 Model One to One 的關係，也在 [Laravel 學習筆記 Lesson 9-1](http://blog.fukuball.com/laravel-xue-xi-bi-ji-lesson-9/) 說明過如何設定 Laravel 中的 Model One to Many 的關係，在這邊我們繼續說明如何設定 ORM 之間 Many to Many 的關係。

假設現在我們的資料有使用者（User）及文章（Post），我們會先建立好 User 的 Model 及 Post 的 Model，通常一個使用者會有很多篇文章，而文章如果可以由多位使用者共同編輯，使用者及文章就是一種多對多的關係。

要在 Laravel 中的 Model 建立多對多的關係需要有一個中介的 table，這樣的資料庫結構設計也才會符合正規化，所有的多對多關係都可以拆解成一對多的關係，所以在這邊我們還會有一個中介 table，user_post_mappings，這個 tabel 至少會有兩個欄位 user_id 及 post_id，記錄 user 與 post 多對多的資料，如此我們就可以在 User Model 及 Post Model 建立多對多的關係。

在 User Model 建立與 Post 的多對多關係的範例程式碼如下：

```php
class User extends Eloquent {

    public function posts()
    {
        return $this->belongsToMany('Post', 'user_post_mappings', 'user_id', 'post_id');
        //return $this->belongsToMany('model_name', 'mapping_table_name', 'foreign_key', 'other_foreign_key');
    }

}
```

使用 belongsToMany 來設定，這個意思就是 User Model 屬於多個 Post，且透過 user_post_mappings 來找到對應關係，後面兩個參數一個是 user_id，一個是 post_id，皆是 user_post_mappings 的 foreign_key，分別對應到 User Model 及 Post Model 的 id。

同樣的，在 Post Model 建立與 User 的多對多關係的範例程式碼如下：

```php
class Post extends Eloquent {

    public function users()
    {
        return $this->belongsToMany('User', 'user_post_mappings', 'post_id', 'user_id');
        //return $this->belongsToMany('model_name', 'mapping_table_name', 'foreign_key', 'other_foreign_key');
    }

}
```

使用 belongsToMany 來設定，這個意思就是 Post Model 屬於多個 User，且透過 user_post_mappings 來找到對應關係，後面兩個參數與 User Model 中的設定反過來，一個是 post_id，一個是 user_id，皆是 user_post_mappings 的 foreign_key，分別對應到 Post Model 及 User Model 的 id。

如此我們就設定好 User Model 與 Post Model 之間的 Many to Many 對應關係了～

設定好 table 之間的 Many to Many 關係可以讓我們更方便地使用資料庫的資料，若果沒有設定 table 之間 Many to Many 的關係，我要取出 User 的 post 資料或 Post 的 User 資料就要使用 Query Builder 來 Join 取出資料，但如果建立了 Many to Many 關係，我們就可以使用 ORM 的方式來取出資料，比如：

```
$posts = User::find(1)->posts;
$users = Post::find(10)->users;
```

總結來說，如果可以設定 Model 之間的關係，未來在使用資料時會變得很方便，否則就會寫很多 Query 在程式碼中，程式會變得難以維護。但是如果是複雜的 Query 還是可以斟酌使用 Query Builder 來查詢資料。