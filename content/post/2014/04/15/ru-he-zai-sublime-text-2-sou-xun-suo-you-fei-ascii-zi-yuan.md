+++
title = "如何在 Sublime Text 2 搜尋所有非 ASCII 字元"
slug = "ru-he-zai-sublime-text-2-sou-xun-suo-you-fei-ascii-zi-yuan"
date = "2014-04-15T08:11:24.000Z"
url = "/2014/04/15/ru-he-zai-sublime-text-2-sou-xun-suo-you-fei-ascii-zi-yuan"
+++

寫程式有時會需要找出原始碼裡所有非 ASCII 字元，拜訪了一下 Google 大神得到了這個答案，筆記一下！

Regular Expression:

    [^\x00-\x7F]