+++
title = "如何開啓 Apache2 的 mod_rewrite"
slug = "ru-he-kai-qi-apache2-de-mod_rewrite"
date = "2014-03-10T17:08:05.000Z"
url = "/2014/03/10/ru-he-kai-qi-apache2-de-mod_rewrite"
+++

使用 Apache2 作為網頁伺服器時，尤其是 PHP Web Application，通常會使用 rewrite rule 來改寫網址，最近開 AWS 上的 Ubuntu 12.04 機器，安裝 Apache2 時 mod_rewrite 預設並非開啓的，所以我們就要自行開啓 mod_rewrite。

指令如下：

    $ sudo a2enmod rewrite
    Enabling module rewrite.
    To activate the new configuration, you need to run:
    service apache2 restart 

開啓後，重開 apache2 即可啓用 mod_rewrite。