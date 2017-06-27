+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第八講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-ba-jiang-xue-xi-bi-ji"
date = "2015-12-23T12:02:57.000Z"
url = "/2015/12/23/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-ba-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第七講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-qi-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在第七講中我們定義了 VC Dimension，就是最大的 non-break point，當 d_vc 是有限的，且資料 N 夠大，Ein 很小的時候，理論上機器學習是可以達成目標的。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-1.png">
</p>

### 重溫機器學習流程圖

重溫機器學習流程圖，大致的理論我們都已經完備了，但這時又會想，如果資料來源有雜訊（noise）又會如何呢？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-2.png">
</p>

### 雜訊（Noise）是什麼

雜訊是什麼呢？以之前的銀行發卡的例子來說明，比如該發卡未發卡、不該發卡卻發了卡、或是一開始收集的基本資料就是錯的，這些就會是我們搜集到資料時的雜訊，在有雜訊的情況下 VC bond 還會正常運作嗎？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-3.png">
</p>

### 用彈珠顏色會改變來代表雜訊來看 VC bound

之前在推導 VC bound 時是用彈珠來說明，我們可以用不固定顏色的彈珠來代表雜訊推導 VC bound（以 pocket algorithm 可以想成是 o 和 x 在同一線上，所以無法確定 o 或 x，這就是雜訊），也就是資料來源會多了一個 y ~ P(y|x)這個條件，從之前的理論推導中，我們了解了訓練資料跟測試資料都來自同一個資料分佈的話，那 VC bound 就會成立。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-4.png">
</p>

### 新的機器學習流程圖

所以新的機器學習流程圖就可以容忍雜訊。也因此可以容忍雜訊的 pocket algorithm 就有理論基礎了。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-5.png">
</p>

### 錯誤衡量

接下來探討如何衡量 g 跟 f 是否很接近，我們使用 E_out(g) 來衡量，這個衡量方式有三個特點：1. 使用 out of sample 來衡量 2. 用 point-wise 的方式一個點一個點衡量 3. 如果是二元分類的問題就會使用 0/1 error 來衡量。但其實也不一定要遵照這三個特點，有很多不同的方法被提出來，只是我們同常還是會這樣來做錯誤衡量。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-6.png">
</p>

### 兩個重要的 Pointwise 錯誤衡量

有兩個重要的 Pointwise 錯誤衡量方式可以記起來，一個是 0/1 錯誤，這個可以用在分類上；一個是平方錯誤，這個通常用在迴歸問題上，不同的錯誤衡量方式會怎麼影響機器學習呢？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-8.png">
</p>

### Ideal Mini-Target

從下面可以例子，我們可以從資料來源 P(y|x) 及 error function 了解它們如何互相影響，在 0/1 錯誤的情況下，選擇 y=0.2 會得到最小的 error 0.3，但在平方錯誤的情況下，選擇 y=1.9 才會得到最小的 error 0.29，機器學習的過程也會在 P(y|x) 及 error function 的關係去找出 ideal mini-target f(x)。 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-9.png">
</p>

### 再次更新機器學習流程圖

所以選擇用什麼 error function 也會影響機器學習的結果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-10.png">
</p>

### 錯誤衡量的選擇

錯誤衡量的選擇也還會有其他考量，具體了解一下錯誤，在 0/1 error 這種 error function，會有 false reject 及 false accept 這兩種錯誤，我們會同等的看待這兩種錯誤，只要出錯，那 error 就是 1。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-11.png">
</p>

### 錯誤有權重：超級市場指紋辨識

但實際的世界可能會有這種情況，錯誤是有權重的，我們可以用超級市場指紋辨識給優惠這種例子來說明，如老顧客有優惠，新顧客沒有優惠，如果指紋辨識 false reject 老顧客沒優惠，那就會失去這位老顧客，影響較大，我們可以給這個錯誤較大的權重。但新顧客 false accept 就沒什麼大不了，虧點小錢而已，錯誤的權重應該比較小。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-12.png">
</p>

### 錯誤有權重：CIA 指紋辨識

但如果是在 CIA 機密文件的指紋辨識上，那就反過來了，有權限的人 false reject 沒有什麼大不了，但沒權限的人 false accept 那就會出大問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-13.png">
</p>

### 最後更新機器學習流程圖

將這樣的概念套用到機器學習流程圖上面，其實就是在演算法 A 這邊對權重的情況作一些調整。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-14.png">
</p>

### 將錯誤權重套用到演算法

如何將錯誤權重套用到演算法呢？我們用 CIA 指紋辨識這個例子來說明，我們可以直接將 false accept 的錯誤乘上 1000 倍，但這其實只做了一半。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-15.png">
</p>

### 更嚴謹一點

因為資料量沒有變，卻讓 error 直接乘上 1000 倍並不嚴謹，所以我們可以用下面這個方式來想，假設沒權限（false accept 錯誤）的資料複製了 1000 筆相同的資料下去訓練，這樣 false accept 乘上 1000 倍就合理，但實務上我們不會真的複製 1000 筆資料進去，而是在演算法上面多去使用沒權限（false accept 錯誤）的資料做運算的機率大了 1000 倍，這樣就很像虛擬的放大資料。用這樣的方式去調整演算法才比較嚴謹。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-17.png">
</p>

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-8-18.png">
</p>

### 結語

在這一講中，我們了解了有雜訊的情況下，機器學習理論上還是可以運作的，並且介紹了錯誤衡量（error measure）的方式也會影響演算法挑選的結果，如果 error measure 有權重的話，那調整演算法時也要嚴謹些，直接在 error function 乘上權重並不夠嚴謹。這一講完備之後，機器學習的基礎理論已經告一段落了，下一講將開始介紹其他機器學習演算法。（我們目前只會 PLA 及 Pocket PLA）
