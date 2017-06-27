+++
title = "Laravel 學習筆記 Lesson 12"
slug = "laravel-xue-xi-bi-ji-lesson-12"
date = "2014-10-28T10:59:45.000Z"
url = "/2014/10/28/laravel-xue-xi-bi-ji-lesson-12"
draft = true
+++

Crawler

"repositories": [
    {
      "url": "https://github.com/everlaat/laravel4-goutte.git",
      "type": "git"
    }
  ],
  
  {
  "require": {
    "laravel/framework": "4.0.*",
    ...
    "elvedia/goutte": "1.0.*"
  }
  ...
}

composer update

'providers' => array(
    ...
    'Elvedia\Goutte\Providers\GoutteServiceProvider',
),

'aliases' => array(
    ...
  'Goutte' => 'Elvedia\Goutte\Facades\Laravel\GoutteFacade',
),


use Symfony\Component\DomCrawler\Crawler;


$crawler = new Crawler();
			$crawler->addContent('<html><body><p>Hello World!</p></body></html>');
			echo $crawler->filter('body > p')->text();
            
https://github.com/everlaat/laravel4-goutte
https://github.com/fabpot/goutte
https://github.com/symfony/DomCrawler
http://symfony.com/doc/current/components/dom_crawler.html

use Goutte\Client;

$client = new Client();
			$crawler = $client->request('GET', 'http://zh.wikipedia.org/wiki/%E4%B9%94%E7%BA%B3%E6%96%AF%C2%B7%E7%B4%A2%E5%B0%94%E5%85%8B');
			$crawler->filter('a')->each(function ($node) {
				echo $node->text()."<br/>";
				echo $node->attr('href')."<br/>";
			});
            
            
$client = new Client();
			$crawler = $client->request('GET', 'http://www.indievox.com/song/1');

			$title_node = $crawler->filter('title');
			echo "title<br/>";
			echo $title_node->text()."<br/>";

			$crawler->filter('meta[property="og:title"]')->each(function ($node) {
				echo "og:title<br/>";
				echo $node->attr('content')."<br/>";
			});

			$crawler->filter('meta[property="og:url"]')->each(function ($node) {
				echo "og:url<br/>";
				echo $node->attr('content')."<br/>";
			});

			$crawler->filter('meta[property="og:image"]')->each(function ($node) {
				echo "og:image<br/>";
				echo $node->attr('content')."<br/>";
			});

			$crawler->filter('meta[property="og:description"]')->each(function ($node) {
				echo "og:description<br/>";
				echo $node->attr('content')."<br/>";
			});