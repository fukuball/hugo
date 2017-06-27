+++
title = "林軒田教授機器學習基石 MACHINE LEARNING FOUNDATIONS 第五講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-wu-jiang-xue-xi-bi-ji"
date = "2015-10-15T06:33:18.000Z"
url = "/2015/10/15/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-wu-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第四講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-si-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

在第四講中我們了解了在有限假設集合的情況下機器學習是可能的，而第五講就是想要將有限假設集合可以推廣出去，讓我們在無限的假設集合裡也可以透過一些理論慢慢收斂到一個多項式集合，如此我們就可以放心的利用機器學習來解決我們所面對的一些問題。

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

我們先來回顧一下上一講的內容，在上一講我們知道了機器學習在足夠的資料及有限的假設集合這種情況下是可行的。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-1.png">
</p>

### 更新機器學習流程圖

如果假設集合 H 是有限 M 個，然後資料量夠多 N，不管我們的演算法 A 是什麼，我們由定理可以知道 Eout 跟 Ein 是很接近的。所以如果 A 找到了一個假設 g 讓 Ein 近似於 0，那我們就可以說 Eout 大概就會是 0，因此機器學習在這樣的情況下是可行的。

有了這樣的概念，我們擴充了我們的機器學習流程圖。從輸入資料中去訓練機器學習，然後得到 Ein 近似於 0，之後再從同一個資料分佈中去測試機器學習的結果，如此可以證明機器有學習到技能。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-2.png">
</p>

### 機器學習的兩個核心問題

機器學習有兩個核心問題，我們希望 Eout 跟 Ein 是很接近的，這個意思就是說，我們希望後來測試學習的結果，會跟訓練時得到的結果很接近，這樣我們才能說機器有學習到技能。

另一個就是，我們希望 Ein 可以很小，也就是訓練的過程中，我們希望機器就可以得到很好的效果，也就是誤差很小。

那之前我們所說的有限集合 M 在這邊扮演什麼角色呢？

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-3.png">
</p>

### Ｍ 的兩難

如果假設集合 M 很小，我們可以保證 Eout 可以接近 Ein，但是因為假設集合小，可以挑選的選擇就少，也因此 Ein 可能會是一個不小的值，也就是誤差會大。

如果假設集合 M 很大，我們可以會得到一個比較好的 Ein，也就是誤差比較小，但是 M 太大我們就無法保證 Eout 會跟 Ein 接近，也就是我們無法保證學習的結果，那機器就白學了。

所以 M 是在哪個值剛好能同時解決這個兩個問題就是一個重點。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-4.png">
</p>

### Ｍ 從哪裡來？

從上一講的定理證明中，我們知道 M 是從當較大的誤差發生的情況累積出來的，所以如果假設集合越大，那累積出來的就一個越大的數字，如果是無限集合，那就沒有上限，但如果是有限集合的話，那就會有個上限。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-6.png">
</p>

### 大誤差發生的情況有很多時候是重疊的

但其實那個上限值我們是高估的，因為許多種大誤差發生的情況都可能是很相似的情況，所以其實這些大誤差發生的情況有很大一部份是重疊的。

那我們可以轉一個想法，我們可以把無限的假設集合依照它們的類型來分類嗎？這樣就可以轉換成一個有限的集合。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-7.png">
</p>

### 一個點的時候有幾種線

之前的 PLA 演算法其實有無限多的假設集合 H，所以在平面上分類一個點的線有無限多條，但是如果說有幾種線，那就只有兩種，一種線是將 x1 分成 o 的，一種線是將 x1 分成 x 的。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-8.png">
</p>

### 兩個點的時候有幾種線

以此類推，兩個點的時候，平面上會多多少種分類這兩個點的線呢？答案是四種線。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-9.png">
</p>

### 四個點的時候有幾種線

再以此類推，四個點的時候，平面上會多多少種分類這四個點的線呢？我們會發現下圖中有兩個組合已經無法找到直線可以做好分類，我們最多只能找到 14 條可以分類四個點的線。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-10.png">
</p>

### Effective Number of Lines

這個故事告訴我們，隨著輸入變多，線的種類會慢慢變成不是指數型成長。依這樣的概念，我們將原本無限多的線轉變為有限多的不同種類的線，我們就可以用這個有限多的不同種類的線的數字來取代 M，這個數字會小於 2 的 N 次方。

這樣我們就可以再套到霍夫丁的定理，知道這樣的過程機器學習的解決會是有效可行的。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-11.png">
</p>

### Dichotomies

這樣的過程就是將原本無限多的線，轉換成分種類的線 Dichotomies，一個 Dichotomy 就是一種分類組合，在二元分類裡這樣組合的上界就是 2 的 N 次方，我們可以用這個數字來取代無限大的 M。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-12.png">
</p>

### 找出問題的成長函數

了解這樣的特性之後，我們只要找出我們要解的問題的成長函數，而這個成長函數不會無限增加，那機器學習就可以證明是可行的。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-13.png">
</p>

### 四種成長函數

我們這邊列出了四種成長函數，分屬不同的問題，PLA 是屬於 2D perceptrons，mH 會小於 2 的 N 次方，代進霍夫丁不等式，由於是指數型成長，並無法保証式子會成立。所以我們希望能證明 PLA 的 mH 會是一個多項式，這樣才能保證霍夫丁不等式成立。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-14.png">
</p>

### Break Point 的概念

Break Point 指的是，當下一個輸入出現時，Dichotomies 組合不再是指數型成長的的那個點，在 2D perceptrons 這邊從我們剛剛的例子可以知道 break point 出現在 4 個輸入時。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-15.png">
</p>

### 四種成長函數的 Break Points

我們知道 positive rays 的 break point 出現在 2，他的成長函數是 big O N，positive intervals 的 break point 出現在 3，他的成長函數是 big O N 平方，那麼在 2D perceptrons 時，我們知道 break point 出現在 4，那他的成長函數是 big O N 三次方嗎？我們可以推廣成一個通式嗎？這就是下次課程的內容了。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-16.png">
</p>

### 總結

機器學習可能的兩個核心問題是 Ein 近似於 0，且 Eout 跟 Ein 要接近。PLA 無限多的線我們可以轉換成 Effective Number of Lines 也就是轉換成 Effective Numbers of Hypotheses，M 無限集合也就轉為 mH 的有限集合，然後觀察 break point 的出現，讓我們可以知道假設集合不會是一個指數型成長的情況，如此依照霍夫丁不等式所說的，我們就可以讓機器學習的理論有充分的證明為可行了。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-5-17.png">
</p>


