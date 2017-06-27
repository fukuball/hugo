+++
title = "如何列出正在執行的 PHP Script Process"
slug = "ru-he-lie-chu-zheng-zai-zhi-xing-de-php-script-process"
date = "2014-03-10T16:58:22.000Z"
url = "/2014/03/10/ru-he-lie-chu-zheng-zai-zhi-xing-de-php-script-process"
+++

在實務上我們通常會使用 crontab job 來背景執行一些程式，有時我們會有需要砍掉這些 process 的情況發生，這時我們就需要列出 process 的 process id，並手動將這些 process 砍掉～

以要查閱 apns-task.php 這支 php script 在機器上執行的 process id 為例，指令可以這樣下：

    $ ps auxwww|grep apns-task.php|grep -v grep

如此就可以列出正在執行 apns-task.php 這支程式的所有 process：

    user 15211 0.0 0.0 4108 604 ? Ss 15:10 0:00 /bin/sh -c php /path-to-your-script/apns-task.php
    user 15213 50.0 0.0 211584 28124 ? R 15:10 0:00 php /path-to-your-script/apns-task.php


如輸出結果所見，現在有兩個 process 15211 及 15213 正在執行 apns-task.php 這支程式，如果要刪除 process 15211，指令就可以這樣下：

    $ kill 15211


以上就是如何列出正在執行的 PHP script process 的簡易筆記～
