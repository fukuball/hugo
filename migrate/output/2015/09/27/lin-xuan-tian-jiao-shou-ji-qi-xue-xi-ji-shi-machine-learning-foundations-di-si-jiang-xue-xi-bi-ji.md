+++
title = "林軒田教授機器學習基石 MACHINE LEARNING FOUNDATIONS 第四講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-si-jiang-xue-xi-bi-ji"
date = "2015-09-27T09:35:33.000Z"
url = "/2015/09/27/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-si-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第三講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-san-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

第四講的內容主要是讓我們知道機器學習是否真的可能，並利用數學上的定理來說明機器學習在某些情境之下是可能的，有數學上定理的支持，我們就可以放心的利用機器學習來解決我們所面對的一些問題。

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

我們先來回顧一下上一講的內容，在上一講我們知道了各式各樣的機器學習方法及名詞，而我們未來會專注於二元分類及迴歸這樣的問題，然後使用大量監督式標示好的資料且定義明確的特徵來進行機器學習。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-1.png">
</p>

### 看看這個問題，想想如何使用學習

有人會問，說了這麼多，如何知道機器學習是不是真的可能？說不定根本無法做到。比如這個問題，g(x)可以回答 +1 還是 -1。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-2.png">
</p>

### 見仁見智的問題無法解

像這樣的問題，你可以回答 +1，因為 +1 的圖都是對稱的，而這個圖是對稱的，所以是 +1。你可以回答 -1，因為 -1 的圖都是左上方黑色的，而這個圖是左上方黑色的，所以是 -1。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-3.png">
</p>

### 套到二元分類的問題

現在我們套到二元分類的問題，給了 Xn 及 Yn，然後機器學習出了 g，我們可以說 g 近似於 f 嗎？

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-4.png">
</p>

### 天下沒有白吃的午餐

在驗證 g 的時候，如果是用原本的 D，那我們很容易的說明 g 近似於 f，但是如果資料是用 D 以外的資料來驗證，那我們無法很明確的說明 g 近似於 f，但我們要的其實就是希望 g 在 D 以外的資料也近似於 f，這有可能嗎？

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-5.png">
</p>

### 利用罐子取彈珠的例子來說明是否可能

現在想像我們有一個裡面有很多橘色和綠色彈珠的罐子，我們可能無法知道橘色彈珠的真實比例，但我們可以推估出橘色彈珠出現的機率嗎？

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-6.png">
</p>

### 取樣看看

我們取樣看看，比如從罐子中取出十顆彈珠，假設現在取出的是三顆橘色七顆綠色，那我們可以說罐子中的比例是 30% 橘色 70% 綠色嗎？可能不能這樣說，有可能不是這樣比例，但很可能 30% 橘色 70% 綠色是一個很接近的比例數字。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-7.png">
</p>

### Hoeffding 不等式 1

我們可以說取樣出來的結果會很接近真實情況，是因為 Hoeffding's Inequality 這個定理。這個定理的數字如下圖，這說明了當 N 很大，也就是我們取樣的數字很大，那們 v - u 就會是一個很小的數字，也就是我們預估的 g 跟真實的 f 的差距很小。而當 ε 很大，也就是我們可以容忍的誤差很大的話，那當然我們就可以很容易地說 g 跟真實的 f 的差距很小。只要符合了這個不等式，那就叫做 probably approximately correct（PAC）。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-8.png">
</p>

### Hoeffding 不等式 2

通常我們不會希望容忍誤差很大，所以通常我們會取 N 很大來推估 g 是否接近 f 的真實情況。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-9.png">
</p>

### 把 Hoeffding 不等式連結到機器學習

當我們現在有一個固定的 h(x)（假設集合 H 的其中一個，他有可能是 g），我們想要知道是否接近 f(x)，x 從 X 中取出，如果 h(x)  ̸= f(x)，就是 h 答錯，就像是罐子中的橘色彈珠，如果 h(x) = f(x)，就是 h 答對，就像是罐子中的綠色彈珠，如果取樣的數字很大的話，那我們就可以用部分的已知資料來大概推估 h(x) 在未知資料的表現情況。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-10.png">
</p>

### 把這個誤差推估的概念加進我們的機器學習圖表

把這個誤差推估的概念加進我們的機器學習圖表，任何一個 h 都可以用已知的 Ein 來推估未知的 Eout，如果 N 夠大。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-11.png">
</p>

### 套進 Hoeffding 不等式

我們套進 Hoeffding 不等式，Ein 代表在已知取樣的中 h(x) 跟 f(x) 的誤差，Eout 代表其他未知的資料中 h(x) 跟 f(x) 的誤差，這在 Hoeffding 不等式的定理下，我們知道 N 很大時，Ein 與 Eout 的誤差很接近，所以我們可以說 Ein 與 Eout 是 PAC。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-12.png">
</p>

### 驗證 h(x) 好不好

所以這常常會被機器學習用在驗證得出來的 h(x) 好不好，可以用這個圖來簡單表示，只要 N 夠大，取樣的分佈一致，那他的表現結果好與不好，是可以很明確地用部分已知資料來推估它在其他未知資料表現得好不好。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-13.png">
</p>

### 好死不死取到壞資料的情況

我們還是會有好死不死取到壞資料的情況，但一樣可以用 Hoeffding 不等式說明這個機率很小，但是還是會發生。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-14.png">
</p>

### 如果有很多個 h

我們剛剛都是用一個 h 來推估是否機器學習是可能的，的確單一個 h 的時候，我們可以用取樣的資料來說明 h(x) 是否跟 f(x) 接近。那如果有很多個 h 呢？

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-15.png">
</p>

### 一樣套進 Hoeffding 不等式

如果是有限個 h，如 M 個 h，那一樣我們可以用取樣的資料來說明 h(x) 是否跟 f(x) 接近。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-16.png">
</p>

### 將這樣的概念加進去機器學習圖表

如果 H 這個集合只有 M 個，然後取樣的 N 夠大，利用 A 取出 g，如果 Ein(g) 接近 0，那麼 g 就是一個 PAC 的答案了，我可由此可知機器學習是可能的。那如果 M 是無限大呢？這個就要下一講來解答了。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-17.png">
</p>

### 總結

這一張說明了，我們無法直觀地說明得到的 h 是否能就是 f，因為天下沒有白吃的午餐。但我們用定理說明的 h 可以在未知的資料中 probably approximate correct。我們將定理連結到機器學習，就可以驗證 h。然後學習的過程也可以套進這樣的概念，當 H 中的 h 數量非無限的時候，機器學習是可能的。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Learning is Impossible-4-18.png">
</p>