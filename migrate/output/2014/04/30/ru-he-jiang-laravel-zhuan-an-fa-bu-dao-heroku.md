+++
title = "如何將 Laravel 專案發佈到 Heroku"
slug = "ru-he-jiang-laravel-zhuan-an-fa-bu-dao-heroku"
date = "2014-04-30T12:28:21.000Z"
url = "/2014/04/30/ru-he-jiang-laravel-zhuan-an-fa-bu-dao-heroku"
+++

目前最火紅的 PHP Framework 就是 [Laravel](http://laravel.com/) 了，以往 PHP Framework 的缺點就是沒有一個熱絡的社群，Laravel 的出現漸漸改變了這樣的現象，Laravel 社群比起其他 PHP Framework 的社群熱絡多了，雖然比起 Rails、Django 及 Node.js 確實還是差了一大截，但總是好現象。

由於看好它的發展性，目前有一些 Side Project 是用 Laravel 來實作，這些 Side Project 如果沒有必要實在是不太想碰機器或者安裝環境，所以發佈到 Heroku 是最好的選擇，只要發佈到 Heroku，Heroku 就會幫忙安裝好所有需要的環境。

步驟如下：

Step 1：使用 CLI 在 Heroku 上開啟一個可以 Build Laravel 的專案

    $ heroku create my-laravel-project --buildpack https://github.com/winglian/heroku-buildpack-php
    
Step 2：在 Laravel 的 Project 資料夾內發佈專案到 Heroku

    $ git push heroku master
    
有時 Heroku 發佈專案會失敗，基本上發佈失敗只要再下一次指令就可能會成功，我也不知道為何有時會這樣，或許是因為是用 Laravel 的關係吧！總之，一次不成功，那就試第二次就對了！

其實還蠻簡單的，還不用管機器，真的很方便～