+++
title = "林軒田教授機器學習技法 Machine Learning Techniques 第 12 講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-12-jiang-xue-xi-bi-ji"
date = "2017-05-22T09:38:06.000Z"
url = "/2017/05/22/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-12-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習技法（Machine Learning Techniques）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第 11 講](https://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-11-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

上一講我們從 Random Forest 延伸到了 AdaBoost Decision Tree，再從 AdaBoost Decision Tree 延伸到 Gradient Boosting，大家不一定要記住所有演算法的細節，但大致上對 Aggregation 的方式有些概念就可以啦！

如果要記，就要記住這個核心概念：Aggregation Model 可以避免 underfitting，讓 weak learner 結合起來也可以做複雜的預測，其實跟 feature transform 的效果很類似。Aggregation Model 也可以避免 overfitting，因為 Aggregation 會選出比較中庸的結果，這其實跟 regularization 的效果類似。所以使用了 Aggregation 也就是 Ensemble 方法通常也就代表了更好的效果。

這一講我們將開始介紹現在很紅的類神經網路機器學習演算法。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-01.png">
</p>

### Perceptron 的線性組合

我們先看一下最簡單的類神經網路，其實可以看成是多個 Perceptron 的線性組合，如果之前學過的 Aggregation，這樣組合多個 Perceptron 就能帶來更複雜的學習效果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-02.png">
</p>

### 單層類神經網路的限制

單層類神經網路可以透過組合越多的神經元來模擬曲線的邊界，用以解決更複雜的問題，但還是有其限制，比如 XOR 及雙曲線這樣的邊界，無論如何都無法透過單層的線性組合來做到，因此我們需要想辦法再延伸單層類神經網路。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-04.png">
</p>

### 多層類神經網路

所以就延伸出了多層類神經網路，就跟邏輯閘設計一樣，多層的架構就可以做出 XOR 這樣的邏輯，多層類神經網路就可以模擬各種各樣的邊界了，一般人家在說的類神經網路其實也就是說多層類神經網路。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-05.png">
</p>

### 在生物上的關係

類神經網路與生物上的神經網路有什麼關係呢？其實類神經網路的架構就是有想要模擬生物上的神經網路，但不完全就跟生物上的神經網路一樣，就跟飛機是模擬鳥類，但跟鳥類飛行實際如何運作並不完全一致。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-06.png">
</p>

### 類神經網路的 output

我們從這個圖探討類神經網路的 output，在 output 之前我們可以把它看成是一個對 x 資料的轉換，x 資料經過各個神經元結合轉換之後，再透過 output 層的線性組合做 voting，如果要做分類就對最後的 output 加上 sign 函數，要做迴歸就直接輸出 output 結果，如果要輸出機率值，就對最後的 output 加上 theta 函數，如此就可以用來解各種常見的 Machine Learning 問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-07.png">
</p>

### 特徵轉換

我們再往前看一下 x 在 output 前經過的特徵轉換層，這些轉換層是由許多神經元組成，用來計算複雜的特徵轉換，每個神經元也會做組合與輸出，這邊的組合如果是用線性組合，那在數學意義上，所有的神經網路就是單純的在做線性組合，所以並無法做到複雜的特徵轉換。

所以這邊的組合要跟邏輯閘一樣使用類似 sign 函數來組合，才能組合出複雜的邊界，但 sign 函數組合並不是一個連續函數，因此比較難優化，所以我們會永 tanh 函數來逼近 sign 函數，如此就不僅可以模擬複雜邊界，然後計算也比較容易優化。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-08.png">
</p>

### 類神經網路假設

如上述去界定類神經網路的架構後，我們可以把類神經網路畫成如下圖，我們會有 x 作為輸入，然後經過各層的 weight 計算後，再透過神經元的 tanh 組合，最後再輸出結果，如此我們只剩下如何去計算出各層的 weight 就可以訓練出類神經網路了。 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-09.png">
</p>

### 神經元的物理意義解釋

這邊我們可以探討一下神經元的物理意義，我們可以看到前一層的輸出會作為後一層的輸入，如果達到一定程度神經元就會輸出結果，所以其實他就是在做兩層之間的匹配程度，越匹配就越能輸出結果，也就是每個神經元都是在學習某一種 pattern。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-10.png">
</p>

### 如何學習各層之間的 weight？

之前學過的 Gradient Boosting 可以用來解單層的類神經網路，但多層的類神經網路不容易用 Gradient Boosting 來解，這邊需要用 Stochastic Gradient Decent 來解會比較簡單一些。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-11.png">
</p>

### Backpropagation 演算法

計算類神經網路的 Gradient Decent 需要使用到 Backpropagation 演算法，這邊我跳過了數學推導過程，想要詳細了解我另外推薦[李宏毅老師的講解](https://www.youtube.com/watch?v=ibJpTrp5mcE)，演算法概觀如下：首先，需要先設定整個類神經網路的 weight value，然後 1. 隨機選取一個資料點 x，2. 計算 forward pass，3 計算 backward pass，4 調整 weight。

（forward 跟 backward pass 分別怎麼計算請看[李宏毅老師的講解](https://www.youtube.com/watch?v=ibJpTrp5mcE)）

通常實務上我們會重複 1 - 3 很多次之後做一個平均再去 update weight，這樣的做法叫做 mini batch。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-14.png">
</p>

### NN 最佳化的問題

由於類神經網路非常複雜，有很多個凸點，所以很容易在學習過程中得到一個 local minimum 的結果。因此不同的起始 weight 可能會得到不同的最佳化結果，在訓練類神經網路時可以挑不同的起始 weight 來做訓練。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-15.png">
</p>

### VC Dimension 

類神將網路的 VC Dimension 為 V\*D，V 是神經元數量，D 是權重的數量，所以如果神經網路的層數跟神經元多起來那 VC Dimension 就會很高，所以可能就會有 overfitting 的現象，這樣就需要做 regularization 來防止 overfitting。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-16.png">
</p>

### Early Stopping

除了使用一般的逞罰項來做 regularization 之外，類神經網路還是用了另一個方式來做到 regularization，這個方法叫 Early Stopping，至於哪時要 stop 呢？那就要做 validation。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-18.png">
</p>

### 總結

這一講說明了什麼是類神經網路，以及類神經網路的核心演算法 Backpropagation，下一講將介紹類神經網路的延伸 - 深度學習。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-12-19.png">
</p>