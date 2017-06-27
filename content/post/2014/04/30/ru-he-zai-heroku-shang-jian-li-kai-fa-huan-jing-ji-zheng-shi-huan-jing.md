+++
title = "如何在 Heroku 上建立開發環境及正式環境"
slug = "ru-he-zai-heroku-shang-jian-li-kai-fa-huan-jing-ji-zheng-shi-huan-jing"
date = "2014-04-30T12:41:15.000Z"
url = "/2014/04/30/ru-he-zai-heroku-shang-jian-li-kai-fa-huan-jing-ji-zheng-shi-huan-jing"
+++

在開發網站的時候，我們至少會有一個正在開發中的開發環境，即真正上線開放給使用者使用的正式環境，通常我們會使用類似 git 的版本控制系統開一個 dev branch 及 ㄧ個 master branch，分別對應到開發環境及正式環境。

所以在 Heroku 上，我們也會希望開一個給使用者使用的 Heroku app（正式環境），另一個就是線上開發版的 Heroku app（開發環境），開發者可能在自己的 local 端開發完之後，將自己的開發的成果 merge 到 dev branch，我們就可以看在線上開發版的運作情況，沒問題了我們才會發佈到正式環境。

首先我們需要先 create 兩個 Heroku App，這邊我們以 Laravel 專案為例：

Step 1：新增 Heroku App

    $ heroku create my-laravel-project --buildpack 
    // 新增正式環境 Heroku Laravel App
    $ heroku create dev-my-laravel-project --buildpack 
    // 新增開發環境 Heroku Laravel App
    
Step 2：將 dev branch 專案發佈到開發環境
	
    $ git config remote.heroku.url "git@heroku.com:dev-my-laravel-project.git"
    $ git push -f heroku dev:master
    
Step 3：將 merge 好的 master branch 專案發佈到正式環境

    $ git config remote.heroku.url "git@heroku.com:my-laravel-project.git"
    $ git push heroku master
    
如此就可以視情況將 dev branch 發佈到 Heroku 開發環境、master branch 發佈到 Heroku 正式環境，這樣就不會讓正在開發的功能影響到獻上的使用者了。