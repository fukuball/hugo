+++
title = "Laravel 學習筆記 Lesson 11"
slug = "laravel-xue-xi-bi-ji-lesson-11-2"
date = "2014-10-21T09:58:52.000Z"
url = "/2014/10/21/laravel-xue-xi-bi-ji-lesson-11-2"
draft = true
+++

### 使用 Cache

app/config/cache.php

Cache::put('key', 'value', $minutes);

if (Cache::has('key'))
{
    //
}

$value = Cache::get('key');

if (Cache::has('users-all')) {
            $users = Cache::get('users-all');
            echo "From Cache";
        } else {
            $users = User::all();
            Cache::put('users-all', $users, 3);
            echo "From Database";
        }

$value = Cache::remember('users', $minutes, function()
{
    return DB::table('users')->get();
});