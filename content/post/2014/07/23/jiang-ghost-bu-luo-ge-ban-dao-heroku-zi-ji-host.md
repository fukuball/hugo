+++
title = "將 Ghost 部落格搬到 Heroku 自己 Host"
slug = "jiang-ghost-bu-luo-ge-ban-dao-heroku-zi-ji-host"
date = "2014-07-23T10:26:31.000Z"
url = "/2014/07/23/jiang-ghost-bu-luo-ge-ban-dao-heroku-zi-ji-host"
+++

之前心血來潮（詳見[開始使用 GHOST 寫部落格](http://blog.fukuball.com/kai-shi-shi-yong-ghost-xie-bu-luo-ge/)）使用了 [Ghost](https://ghost.org/) 寫部落格，沒想到竟也堅持了一陣子了，眼見之前因為在 [Kickstarter](https://www.kickstarter.com/) 參與了 Ghost 投資而得到的免費六個月使用權就要過了，之後就需要付每個月至少 5 美元的使用費，實在也不是筆小錢，但身為程式設計師自己 Host 一個網站其實也不是件難事，所以就在參加 COSCUP 的空檔時間將部落格搬到 [Heroku](https://dashboard.heroku.com/apps) 自己 Host 了～ 自己的部落格自己 Host！

原本想說搬移的過程也可以寫成一篇教學文，但是真的有點簡單，雖然有些細節需要注意，但基本上我實在是不知如何湊成一篇教學文啊！總之如果會使用 Heroku，基本上在 Heroku 上安裝 Ghost 是沒什麼問題的，這樣就可以在 Heroku 上免費 Host Ghost 部落格了！省下每個月 5 美元的感覺真爽啊！

<p style="text-align:center">
<img src="http://static.obeobe.com/2014/Jul/i__e88e__-1406113001957.jpg" alt="非常好">
</p>

如果大家還是想知道如何在 Heroku 上安裝 Ghost 部落格，可以到我 Github 上 [blog.fukuball.com](https://github.com/fukuball/blog.fukuball.com) 這個 Repo 參考一下安裝的指令，不過由於我自己有使用 AWS，這個 Repo 的後端資料庫是接 AWS RDS MySQL，圖片的 Storage 則是接 AWS S3，如果沒有使用 AWS 的話，就建議使用原本的設定就好，可以參考 [Deploy Ghost to heroku for free](http://www.therightcode.net/deploy-ghost-to-heroku-for-free/) 這篇文章來試試～

話說雖然我已經將 Ghost 上的部落格關掉了，但我個人的 Profile 仍然還在 Ghost 網站上，[funder badge](https://ghost.org/fukuball/) 還是好好地掛在網頁上面。現在真心覺得有 funder badge 的 backer 應該要可以永久免費使用 Ghost 部落格才對啊！不然以 Ghost 這種 backer 組成幾乎都是程式設計師的平台，只要一收費大家就是怒搬部落格到 Heroku 了！

![ghost funder badge](http://static.obeobe.com/2014/Jul/Screen_Shot_2014_07_23_at_7_00_18_PM-1406113694581.png)

<blockquote>
圖片取自於 Google 搜尋，絕無意侵犯智財權。若有侵犯請告知，我會馬上刪除，感謝！
</blockquote>