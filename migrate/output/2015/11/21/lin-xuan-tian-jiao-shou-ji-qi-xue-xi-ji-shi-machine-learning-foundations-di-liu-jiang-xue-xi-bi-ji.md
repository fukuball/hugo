+++
title = "林軒田教授機器學習基石 MACHINE LEARNING FOUNDATIONS 第六講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-liu-jiang-xue-xi-bi-ji"
date = "2015-11-21T13:41:57.000Z"
url = "/2015/11/21/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-liu-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第五講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-wu-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

在第五講中我們了解了如何將 PLA 無限的假設集合透過 Dichotomy、Break Point 這樣的方式轉換成有限的集合，在第六講中我們將更進一步去推導其實這個假設集合的成長函數會是一個多項式，如此我們就可以完全相信PLA 機器學習方法的確在數學理論上是可行的了。

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

我們先來回顧一下上一講的內容，在上一講我們知道了成長函數似乎跟 break point 有些關係，這一講我們將慢慢導出這樣的關係其實是一個多項式。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-1.png">
</p>

### 從 break point 找其他線索

從上一講提到的 break point 我們知道了成長函數至少會小於 2 的 N 次方，且如果 break point 在k取到了，那 k+1, k+2,... 都會是 break point。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-2.png">
</p>

### 由例子觀察 break point

這邊林軒田教授用了一連串的例子說明了如果 H 有Break Point k，那當 N 大於 k 時，mH(N) 成長函數會大大縮減（以 binary classification 這個問題來說，所有的 H 為 2 的 N 次方個）。

既然知道 mH(N) 成長函數會大大縮減，那究竟能縮減到什麼程度？會不會是一個多項式的形式呢？

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-3.png">
</p>

### Bounding Function

接下来，引出了 Bounding Function 的概念，Bounding Function 的意義就是為了看在 N 個樣本點的情況下，如果 Break Point 為 K，那 mH(N) 會縮減到什麼程度的一個函式。

值得一提的是，這裡的 Bounding Function B(N, K) 只與 N 和 K 有關，與假設集合 H 無關，這樣在 Binary Classification 這個問題下，無論是 positive intervals 還是 1D perceptrons 他們的 Bounding Function 就都會是一樣的，如果我們能夠得到 Bounding Function 的結果，那就可以推廣到各個 Binary Classification 的問題。

所以我們新的目標就是找出 B(N, K) 是不是小於等於 poly(N) 了。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-4.png">
</p>

### 推導 Bounding Function 數學式

從以下投影片的 Dichotomies 例子可以導出 Bounding Function 的一個上界，所以 B(N, k) 會是小於等於 B(N-1, k)+B(N-1, k-1)。（詳細過程可以參考影片）

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-5.png">
</p>

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-6.png">
</p>

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-7.png">
</p>

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-8.png">
</p>

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-9.png">
</p>

### Bounding Function 定理

Bounding Function 的上界出現了我們想要的多項式形式，這裡得出了一個定理，只要 Break Point 存在，那 mH(N) 成長函數一定能夠被一個多項式包含住，我們可以用投影片中的式子來表示 B(N, k)。

事實上式子中的"小於等於"可以直接是"等於"，這已有證明，但不在這次課程範圍，有興趣可以去找其他資料來看。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-10.png">
</p>

### 找出 break point 就能算出成長函數

有了 Bounding Function 定理，我們就可以透過找出 break point 來算出假設集合的成長函數，比如上一講中我們說 PLA 2D perceptrons 的成長函數小於 2 的 N 次方，現在我們可以說PLA 2D perceptrons 的成長函數小於等於 B(N, 4)，因為 2D perceptrons 的 break point 出現在 4。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-11.png">
</p>

### 把 Bound Function 的定理引入 Hoeffding 不等式

有了上面的推導，我們知道 mH(N) 是可以在某種條件下（Break Point k）被 Bound 住。現在回到 Hoeffding 不等式的 union bound 形式，把 Bound Function 的定理概念引入這個 Hoeffding 不等式可以慢慢推導出投影片中下面的式子。

直觀的想法我們可以把 mH(N) 的上界直接代進 Hoeffding 不等式，但理論上我們不能這樣做，因為目前 Eout(h) 是無限個，因此我們需要做一些轉換才能購買 B(N, k) 引入這個 Hoeffding 不等式。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-12.png">
</p>

### 第一步把 Eout(h) 轉換成有限個

第一步我們需要把 Eout(h) 轉換成有限個，這裡沒有做嚴格的證明，只個了直觀的解釋，假設還有一筆資料 D‘（數量也是 N），得到的結果為 Ein‘，那 Ein 與 Eout 發生 BAD（差距很大），應該跟 Ein 與 Ein‘ 發生 BAD 的情況接近。

所以這個無限的 Eout(h) 就轉換成有限個的 Ein‘(h) 了。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-13.png">
</p>

### 第二步整理式子中的成長函數 mH(N)

利用第一步的结果，再直觀想像一下：為了產生 Ein‘ 我們多了 N 個樣本點，所以成長函數中的 N 就變成了 2N 了。

我們可以想像就樣的結果其實就是我們用了 Bound Function 這個定理，將原本無限的 Union Bound 限縮在一個 BAD overlap 的空間。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-14.png">
</p>

### 第三步代進 Hoeffding 不等式

接下來代進 Hoeffding 不等式就完成了。這樣的轉換就像是 2N 個樣本，現在抽了 N 的樣本出來，這 N 個樣本跟原來 2N 個樣本的真實情況相比發生 BAD 的機率會是多少。這樣還是一個 Hoeffding 不等式，只是就像罐子變小、誤差變小、不放回抽樣的 Hoeffding 不等式。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-15.png">
</p>

### Vapnik-Chervonenkis（VC）bound

這最終的式子就是 Vapnik-Chervonenkis（VC）bound，它將 Eout 用  Ein' 來代換，然後將假設集合專換成分類（使用 Bound Function 證明為一個多項式），然後再代進 Hoeffding 不等式。

在 2D perceptrons 中，break point k=4，mH(N) 是 O(N3)，由 VC bound 可知 2D perceptrons 是可以從數據中得到學習效果。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-17.png">
</p>

### 總結

從這一講中，我們可以知道 Break Point 的出現可以大大限縮假設集合成長函數，而這個成長函數的上界是 B(N, k)，且可推導出 B(N, k) 是一個多項式，經過一些轉換與推導我們可以把無限的假設集合代換成有限的假設集合，因此可以從數學理論中得知 2D perceptrons 是可以從數據中得到學習效果的。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-6-16.png">
</p>