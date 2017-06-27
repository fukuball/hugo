+++
title = "Laravel 學習筆記 Lesson 15"
slug = "laravel-xue-xi-bi-ji-lesson-15"
date = "2014-11-17T12:48:34.000Z"
url = "/2014/11/17/laravel-xue-xi-bi-ji-lesson-15"
draft = true
+++

### 在地化

Laravel 的 Lang 類別提供方便的方法來取得多種語言的字串

語言字串儲存在 app/lang 資料夾的檔案裡

新增語言檔 message.php

切換

App::setLocale('en');

echo Lang::get('messages.welcome');

echo trans('messages.welcome');

使用變數

'hi' => '嗨， :name'

echo trans('messages.hi', array('name' => 'Fukuball'));

複數

'apples' => '{0} There are none|[1,19] There are some|[20,Inf] There are many',

echo Lang::choice('messages.apples', 10);

'dogs' => '{1} There is :num dog|[2,Inf] There are :num dogs',

echo Lang::choice('messages.dogs', 1, array('num' => 1));

