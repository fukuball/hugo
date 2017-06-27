+++
title = "林軒田教授機器學習技法 Machine Learning Techniques 第 11 講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-11-jiang-xue-xi-bi-ji"
date = "2017-04-25T08:46:15.000Z"
url = "/2017/04/25/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-11-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習技法（Machine Learning Techniques）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第 10 講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-10-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

上一講的 Random Forest 演算核心主要就是利用 bootstrap data 的方式訓練出許多不同的 Decision Trees 再 uniform 結合起來。


<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-01.png">
</p>

### AdaBoost Decision Tree

這一講接下來要介紹的 AdaBoost Decision Tree 其實乍看有些類似，但它的訓練資料集並不是透過 bootstrap 來打亂，而是使用之前 AdaBoost 的方式再每一輪資料計算加權 u(t) 去訓練出許多不同的 Decision Tree，最後再以 alpha(t) 的權重將所有的 Decision Tree 結合起來。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-02.png">
</p>

### 權重會影響演算法

由於 AdaBoost Decision Tree 會考慮到權重，因此應該要像之前介紹過的 AdaBoost 會將權重傳進 Decision Stump 一樣，AdaBoost Decision Tree 應該也要將權重傳進 Decision Tree 裡做訓練，但這樣就需要調整 Decision Tree 原本的演算法，我們不喜歡這樣。

轉換一個方式，也許我們可以一樣使用抽樣的方式來將訓練資料依造 u(t) 的權重做抽樣，這樣就可以直接將用權重抽樣玩的訓練資料集傳進 Decision Tree 做訓練，達到相同的效果，如此就不用改原本 Decision Tree 的演算法了。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-03.png">
</p>

### 要使用 Weak Decision Tree

另外要注意的是，如果 AdaBoost Decision Tree 使用了 fully grown 的 Decision Tree，這樣 alpha(t) 就會變得無限大，如此訓練完的 AdaBoost Decision Tree 做預測時就只會參考這個權重無限大的 Decision Tree，這樣就沒有 Aggregation Model 的效果了，我們應該要避免這個問題，所以要使用弱一點的 Decision Tree，比如透過 pruned 來避免 Decision Tree fully grown。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-04.png">
</p>

### 特例：使用 Extremely Pruned Tree

如果 AdaBoost Decision Tree 使用了 Extremely Pruned Tree，比如限制樹的高度只有 1，那這樣其實就是之前學過的 AdaBoost，這是 AdaBoost Decision Tree 中的一個特例。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-05.png">
</p>

### Gradien Boost

這邊的數學演算太過複雜，大家可以直接觀看影片學習，我這邊直接說數學推導最後得出來的結論。

AdaBoost 透過一些數學特性的推導之後，可得出圖中的式子，代表要最佳化 binary-output Error，這個式子可以換成是要算 real-output Error，這樣就是所謂的 Gradien Boost。

由於 real-output Error 的最佳化是一個連續函數，我們可以使用跟之前的 logistic regression 一樣的方式使用 gradient decent 找出最佳的 ita 及 h(x)。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-06.png">
</p>

### Gradien Boost 演算法

Gradien Boost 演算法的數學推導這邊也請大家去看影片，我直接講數學推導完之後得到的結論，整個演算法看起來很簡單，第一步先使用 xn 與餘數 (yn - sn) 做訓練，得出 gt，第二步再使用 gt 對 xn 做資料轉換，再使用 gt(xn) 與餘數 (yn - sn) 做 linear regression 算出 alphat，最後使用 sn + alphat * gt(xn) 得出新的 sn，重複這個過程，將各個 Decision Tree 結合起來就是 Gradien Boost Decision Tree 了！


<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-07.png">
</p>

### Blending Models

課程到這邊已經介紹完了 Blending Models 的各種形式，有 uniform、non-uniform、conditional 的形式，uniform 可以帶來穩定性，non-uniform 及 conditional 可以帶來模型複雜度，但要小心 overfiting。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-08.png">
</p>

### Aggregation Learning Model

從上述的 blending 方式，我們可以發展出不同的 Aggregation Model，如 Badding 使用 uniform vote、AdaBoost 使用 linear vote by reweighting、Decision Tree 使用 conditional vote、GradientBoost 使用 linear vote by residual（餘數） fitting。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-09.png">
</p>

### Aggregation Model 的好處

Aggregation Model 可以避免 underfitting，讓 weak learner 結合起來也可以做複雜的預測，其實跟 feature transform 的效果很類似。Aggregation Model 也可以避免 overfitting，因為 Aggregation 會選出比較中庸的結果，這其實跟 regularization 的效果類似。所以使用了 Aggregation 也就是 Ensemble 方法通常也就代表了更好的效果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-11.png">
</p>

### 總結

在這一講，我們從 Random Forest 延伸到了 AdaBoost Decision Tree，再從 AdaBoost Decision Tree 延伸到 Gradient Boosting，基本上對大部分的 Aggregation Model 都有一些認識了。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-11-12.png">
</p>