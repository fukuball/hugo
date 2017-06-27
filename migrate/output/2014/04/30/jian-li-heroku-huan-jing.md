+++
title = "如何建立 Heroku 環境"
slug = "jian-li-heroku-huan-jing"
date = "2014-04-30T11:50:14.000Z"
url = "/2014/04/30/jian-li-heroku-huan-jing"
+++

Heroku 是一個 PaaS 雲端服務，可以讓開發者快速在雲端上放上自己開發的服務，使用 PaaS 服務可以在開發初期省下不少資源，若目前的開發專案沒有使用到 Heroku 沒有支援的功能，使用 Heroku 是一個很好的選擇。

使用 Heroku 所需要建立的環境步驟如下：

Step 1：[註冊 Heroku 帳號](https://id.heroku.com/signup/dc)

Step 2：[安裝 Heroku toolbelt](https://toolbelt.heroku.com/)

Step 3：測試使用 Heroku CLI 登入

	$ heroku login
    Enter your Heroku credentials.
	Email: adam@example.com
	Password:
	Could not find an existing public key.
	Would you like to generate one? [Yn]
	Generating new SSH public key.
	Uploading ssh public key /Users/adam/.ssh/id_rsa.pub
    
如果可以成功，就代表安裝已經完成

Step 4：新增 SSH Key

要 push project 到 Heroku 需要使用 SSH key，如果沒有 SSH key 的話，可以用以下指令新增一個 SSH key

    $ ssh-keygen -t rsa
    Generating public/private rsa key pair.
	Enter file in which to save the key (/Users/adam/.ssh/id_rsa):
	Enter passphrase (empty for no passphrase):
	Enter same passphrase again:
	Your identification has been saved in 	/Users/adam/.ssh/id_rsa.
	Your public key has been saved in /Users/adam/.ssh/id_rsa.pub.
	The key fingerprint is:

Step 5：將 SSH Key 新增到 Heroku 帳戸

	$ heroku keys:add
    Found existing public key: /Users/adam/.ssh/id_rsa.pub
	Uploading SSH public key /Users/adam/.ssh/id_rsa.pub... done

Step 6：將現有專案 deploy 到 Heroku

	$ cd my-project
	$ heroku create my-project
    $ git push heroku master
    
如此就可以建立好 Heroku 環境，並且將自己的專案發佈到 Heroku 的雲端環境，對於機器不熟的人，用 Heroku 其實還蠻方便的。


