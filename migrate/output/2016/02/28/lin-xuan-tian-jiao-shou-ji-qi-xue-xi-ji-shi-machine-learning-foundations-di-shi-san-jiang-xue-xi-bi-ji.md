+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第十三講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-san-jiang-xue-xi-bi-ji"
date = "2016-02-28T18:27:22.000Z"
url = "/2016/02/28/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-san-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第十二講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-er-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在上一講中，我們了解了如何使用非線性轉換來讓我們的機器學習演算法可以學習出非線性分類模型，也了解了這樣的方法可能會讓模型複雜度變高，造成 Overfitting 使未來 Eout 效果不佳的情況，所以要慎用此方法。在這一講中將更進一步說明什麼是 Overfitting，並講解如何避免 Overfitting。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-1.png">
</p>

### Bad Generalization 無法舉一反三

我們來看個例子，現在我們使用一個二次多項式加上一點 noise 產生資料點，由於有 noise，我們是無法學習出一個二次多項式讓 Ein 為 0。但如果我們使用了非線性轉換到四次多項式來進行學習，我們可以找到一個 w 讓 Ein 為 0，看起來可能會像是圖中的紅線。但可想而知紅線的 Eout 可能會非常高，如此我們的機器學習是失敗的，無法舉一反三。 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-2.png">
</p>

### Overfitting 過度優化

其實這就是一種過度優化，當我們發現 Eout - Ein 很大時，就是發生了 Bad Generalization。

我們觀察圖中的 dvc\*，當 dvc\* 越來越高時，Ein 會下降，但 Eout 會上升，這時就是產生了 Overfitting。

當 dvc\* 往左時，Ein 會上升，Eout 也會上升，這時就是產生了 Underfitting。

Underfitting 不會很常發生，因為我們會追求低的 Ein，因此可以避免 Underfitting，但 Overfitting 卻常常發生，因為追求低 Ein，會讓我們不小心進入陷阱。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-3.png">
</p>

### Case Study 1/2

我們再來看一個例子，我們現在有兩個 target function，一個是 10 次多項式加上一些 noise，一個是 50 次多項式然後沒有 noise，現在我們使用一個 2 次多項式及一個 10 次多項式來逼近學習這兩個 target function，以觀察 Overfitting 現象。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-4.png">
</p>

### Case Study 2/2

結果我們發現，當我們將學習模型由 2 次多項式轉換到 10 次多項式時，無論是在 10 次或 50 次多項式的資料點都會產生 Overfitting，Ein 變小了，但是 Eout 卻變得非常大！

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-5.png">
</p>

### Learning Curve

我們將 Ein 及 Eout 的變化畫成圖示，我們可以看出 10 次多項式的模型在資料點 N 趨近于無限大時，的確可以得到很低的 Eout，但在資料點不夠多的情況下，Eout 卻會比原來的 2 次多項式模型高很多，圖中灰色的區域會很容易產生 Overfitting。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-6.png">
</p>

### Noise 的影響

會產生 Overfitting 其實就是 Noise 的影響，尤其當資料點不夠多的情況下影響會很大，在有 Noise 的情況下，複雜的學習模型會去模擬 Noise，因此也就會造成未來在做預測時反而會不準確。所以在有 Noise 的情況下，有時簡單的模型反而會有好的效果。

Noise 除了我們一般所知的 stochastic noise 之外，還有另一種 Noise，當我們要學習的模型越複雜時，這其實對我們的學習演算法也是一種 Noise，這就是 deterministic noise。我們將這兩個 Noise 與 Data N 的數量畫成圖來觀察 Overfitting，我們可以得到四個結論：

1. 當 data 越少時，Overfitting 越容易發生
2. 當 stochastic noise 越大時，Overfitting 越容易發生
3. 當 deterministic noist 越大時，Overfitting 越容易發生
4. 當使用的學習模型越複雜時，因為他會模擬 Noist，Overfitting 越容易發生

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-8.png">
</p>

### 避免 Overfitting 的方法

我們有幾個方法來避免 Overfitting：

1. 先從簡單的模型開始學習，再慢慢使用複雜的模型，這在上一講有說過了。
2. 使用資料清洗（Data Cleaning/Pruning），將錯誤的 label 修正，或直接刪除錯誤的數據。
3. 製造資料（Data Hinting），使用合理的方法將原來手的的資料變得更多，比如在數字識別的這個問題將已有的數字透過平移、旋轉來製造出更多資料。
4. 正規化（Regularization），下 14 講的主題。
5. 驗證（Validation），第 15 講的主題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-9.png">
</p>

### 總結

在這一講中，我們更了解了什麼是 Overfitting，也觀察到 Overfitting 是很容易發生的，也介紹了一些避免 Overfitting 的方法。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-13-12.png">
</p>