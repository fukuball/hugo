+++
title = "Laravel 學習筆記 Lesson 1"
slug = "laravel-xue-xi-bi-ji-lesson-1"
date = "2014-08-05T08:37:49.000Z"
url = "/2014/08/05/laravel-xue-xi-bi-ji-lesson-1"
+++

### 前言

近來 Web Programming 相關技術及工具已經越來越成熟，許多功能可能都不再需要自己動手從頭刻，需要的反而是學習如何去使用這些工具，Laravel 是目前最熱門的 PHP Framework，它就是一個為了 Web Programming 而生的開發工具。

學習工具看似是一個方便且輕鬆的路，但其實也有它的難處，比如會常常忘記如何使用、使用的的語法也可能會是這個 Framework 所特有的、對於實際上程式怎麼運作會一知半解，這對初學者來說還是有學習進入門檻。

我編寫了這系列部落格僅是為了記錄我個人的學習記錄，並非為了教學，所以可能會有不夠詳盡的地方，但多少希望能夠回饋一下社群，當然有問題也歡迎各位跟我討論，大家一起互相學習！

### 建立開發環境

1. Linux 作業系統，例如 Ubuntu 或 Debian
2. 安裝 Git
3. 安裝 PHP 5.4 以上版本（需要有 MCrypt PHP 套件）
4. 安裝 Composer（PHP 套件管理工具）
5. 安裝 Nginx
6. 安裝 HHVM
7. 安裝 Laravel

其實 Laravel 也又內建 web server，但使用 Nginx 及 HHVM 作為 PHP 網頁伺服器是為了建立大型網站，這可以帶來比較好的穩定度及效能。

建立開發環境的詳細細節可以參考這篇教學文章： http://fideloper.com/hhvm-nginx-laravel

### 設定 Git 的 SSH Key

設定好 Git 的 SSH Key 之後，伺服器就可以透過 SSH 的方式存取 Git Server 的 Repo，我個人是 Github 及 Bitbucket 都有使用，因此兩個 Git Server 都會設定好 SSH Key。

設定方法如下：

1. [Set up SSH for Git On Github](https://help.github.com/articles/generating-ssh-keys#platform-linux)
2. [Set up SSH for Git On Bitbucket](https://confluence.atlassian.com/display/BITBUCKET/Set+up+SSH+for+Git)

若是初學者不了解 Git 如何使用，可以參考一下我這篇部落格 [GIT 簡易使用教學](http://blog.fukuball.com/git-jian-yi-shi-yong-jiao-xue/)，至少了解一下基本使用方法。

### 建立 Laravel Project

開發環境建立好之後，我們就可以開始新建一個 Laravel Project，建立 Laravel Project 的指令如下：

	composer create-project laravel/laravel your-project-name --prefer-dist
    
your-project-name 請填入想要的 Project 名稱，比如我想做一個叫 car 的網站，那我的指令就會是：

	composer create-project laravel/laravel car --prefer-dist
    
就這麼簡單的一個指令就可以安裝好 Laravel 的 Project 了！

### 將 Laravel 加入 Git Repo

接下來我們要將 Laravel Project 加入 Git Repo 做版本控制，指令如下：

#### Step 0：在 Git Server 開好 Git Repo

首先需要在 Git Server 上開好 Project 的 Git Repo，Git Server 可以是 Github 或是 bitbucket 等服務，如此我們就可以得到 Git Server 的 Git Repo 網址。

#### Step 1：進入 Laravel Project 資料夾

	cd /path/to/your/project 
    
比如我的 Project 的實體位置在 /var/www/car，那指令就會是：
    
    cd /var/www/car
    
#### Step 2：初始化一個 Git Repo

	git init 
    
#### Step 3：將 Local Git Repo 連結 Remote Git Repo

在 Step 0 可以取得 Git Server 上的 Project Git Repo 網址，接下來我們要將 local 的 git repo 與 server 上的 git repo 連結起來，以 bitbucket 為例：

	git remote add origin git@bitbucket.org/username/bbreponame.git
    
指令中的 username 指的是在 git server 上的使用者名稱，bbreponame 指的是 step 0 時在 git server 上開好的 repo 名稱，所以 car 這個 prject 的 server git repo 網址可能會像這樣：

	git remote add origin ssh://git@bitbucket.org/fukuball/car.git
    
#### Step 4：將目前的 Laravel Project 所有檔案加入 Git Repo

	git add .
    
#### Step 5：將目前的 Laravel Project Commit 進 Git Repo

	git commit -a -m "Init laravel project"
    
#### Step 6：將所有的 Commit Push 至 Git Server

	git push origin master
    
完成以上步驟就完成了 Laravel Project 的建立，並且將 Laravel Project 加入了 Git 版本控制，這是所有 Web 專案開發的起手式～

### 設定 Laravel Project 使用 Nginx Virtual Host

若是大型網站開發，我們通常會使用 Nginx 等網頁伺服器，而同一台機器上可能不只有一個 Project，可能會同時有 <code>car.fukuball.com</code> 及 <code>bike.fukuball.com</code> 在指向同一台機器，這使我們就要使用 Nginx 的 Virtual Host 設定將 <code>car.fukuball.com</code> 指向 car 這個 project 的實體位置，這邊的例子是 <code>/var/www/car</code>，而 
<code>bike.fukuball.com</code> 指向 bike 這個 project 的實體位置，如： <code>/var/www/bike</code>。

Virtual Host 設定檔位置通常會是在 <code>/etc/nginx/sites-available</code> 或是 <code>/etc/nginx/conf.d</code>，現在我們就在這個位置下新增一個設定檔：

	vim /etc/nginx/conf.d/car.fukuball.com.conf
    
設定檔的範例內容如下：

	server {
    	listen 80;
        root /var/www/car/public/;
        index index.php index.html index.htm;
        server_name car.fukuball.com;
        location / {
			try_files $uri $uri/ /index.php?$args;
		}
        location ~* ^.+\.(ogg|ogv|svg|svgz|eot|otf|woff|mp4|ttf|rss|atom|jpg|jpeg|gif|png|ico|zip|tgz|gz|rar|bz2|doc|xls|exe|ppt|tar|mid|midi|wav|bmp|rtf)$ {
			access_log off; log_not_found off; expires max;
		}
		location ~* \.(css|js)$ {
			expires 365d;
		}
        error_page 500 502 503 504 /50x.html;
		location = /50x.html {
			root /usr/share/nginx/html;
		}
        location ~ \.(hh|php)$ {
			fastcgi_split_path_info ^(.+\.php)(/.+)$;
			fastcgi_keep_conn on;
			fastcgi_pass 127.0.0.1:9000;
			fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param REDIRECT_QUERY_STRING "$query_string";
            include fastcgi_params;
		}
		location ~ /\. {
			deny all;
		}
    }
    
設定好之後，將 nginx 重開就完成了。
    
	service nginx restart
        
### 結語

以上完成之後，終於可以開始開發專案，我們也終於可以進入如何使用及開發 Laravel PHP Framework，Laravel 學習筆記 Lesson 1 主要就是記錄如何從無到有建立一個可以使用 Laravel 的開發環境，接下來就是打開編輯器，開始寫 Code 囉！

ps. 建議初學者可以使用 Sublime Text 等 IDE 作為開發的編輯器，這篇部落格有介紹 [我在 SUBLIME TEXT 2 常用的快捷鍵](http://blog.fukuball.com/wo-zai-sublime-text-2-chang-yong-de-kuai-jie-jian/)，在開發上會有很多幫助。
    

