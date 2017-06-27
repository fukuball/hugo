+++
title = "在 Linux 系統背後執行一個程序"
slug = "zai-linux-xi-tong-bei-hou-zhi-xing-ge-cheng-xu"
date = "2014-11-25T11:24:52.000Z"
url = "/2014/11/25/zai-linux-xi-tong-bei-hou-zhi-xing-ge-cheng-xu"
+++

當有一個程序需要不斷的偵測請求，我們通常需要背景執行一個程序，且不能讓程序關閉，比較正規的做法當然就是直接開一個伺服器服務來執行這個程序，但有時我們會不希望為了一個小程序而去開服務，這時可以用以下這個指令來讓系統背後執行一個程序：

```
$ nohup node server.js &
```

以上例子就會讓系統背後執行 node.js 的預設 server，即使關閉 terminal 也會持續執行，若想關閉，就需要用 kill 的方式來將程序關閉。