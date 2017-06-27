+++
title = "如何找出占用 Port 的 Process 並將之關閉"
slug = "ru-he-zhao-chu-zhan-yong-port-de-process-bing-jiang-zhi-guan-bi"
date = "2014-11-25T11:13:25.000Z"
url = "/2014/11/25/ru-he-zhao-chu-zhan-yong-port-de-process-bing-jiang-zhi-guan-bi"
+++

開服務時有時難免會遇到 Port 被占用的情況，這時就需要找出哪些 Process 占用了這個 Port，並強制關閉 Process，如此才能夠再度使用這個 Port。

假設現在 1337 Port 被占用了，我們可以使用以下指令找出占用 Port 的 Process：

```
$ lsof -i tcp:1337

// 輸出結果
COMMAND   PID USER   FD   TYPE  DEVICE SIZE/OFF NODE NAME
php     26267 root    5u  IPv4 4542269      0t0  TCP *:1337 (LISTEN)
php     26267 root    7u  IPv4 4542295      0t0  TCP 
php     26267 root    8u  IPv4 4542296      0t0  TCP
```

然後我們就可以使用 PID 來關閉 Process：

```
$ kill -9 26267
```