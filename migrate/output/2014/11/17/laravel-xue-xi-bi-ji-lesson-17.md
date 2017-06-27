+++
title = "Laravel 學習筆記 Lesson 17"
slug = "laravel-xue-xi-bi-ji-lesson-17"
date = "2014-11-17T13:42:33.000Z"
url = "/2014/11/17/laravel-xue-xi-bi-ji-lesson-17"
draft = true
+++

### 單元測試

"phpunit/phpunit": "4.0.*",

composer update

vendor/bin/phpunit 

<?php

class ControllerTest extends TestCase {

    /**
     * A basic functional test example.
     *
     * @return void
     */
    public function testHomeControllerGetIndex()
    {

        $this->call('GET', '/');
        $this->assertResponseOk();

    }

}

登入狀態如何測試

public function testHomeControllerGetIndex()
    {

        $crawler = $this->client->request('GET', '/index.html');
        $this->assertTrue($this->client->getResponse()->isOk());
        $this->assertCount(0, $crawler->filter('a:contains("Fukuball Lin")'));

        $user = User::find(8);
        $this->be($user);
        $crawler = $this->client->request('GET', '/index.html');
        $this->assertTrue($this->client->getResponse()->isOk());
        $this->assertCount(1, $crawler->filter('a:contains("Fukuball Lin")'));

    }