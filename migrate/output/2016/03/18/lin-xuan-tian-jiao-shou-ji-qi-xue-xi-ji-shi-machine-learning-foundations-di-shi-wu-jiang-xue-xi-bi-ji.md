+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第十五講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-wu-jiang-xue-xi-bi-ji"
date = "2016-03-18T18:30:53.000Z"
url = "/2016/03/18/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-wu-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第十四講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-si-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在上一講中，我們進一步了解了如何透過正規化（Regularization）來避免 Overfitting，但正規化這個方法會有一個參數 lambda，這個 lambda 我們又要如何選擇呢？在這一講將會學習到使用 Validation 這個方法來幫助我們選擇比較好的 lambda 值，同理，這個方法也可以幫助我們用於選擇各種不同的學習模型。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-1.png?1">
</p>

### 許多學習模型可以使用

經過了前面 14 講，我們已經學會了許多學習模型，在演算法上我們有 PLA、Pocket、Linear Regression、Logistic Regression 可以做選擇；然後在模型學習的過程中，我們可以指定演算法要經過幾次的學習，每次學習優化的過程要走多大步；我們也可以有很多種線性轉換的方式將模型轉換到更複雜的空間來進行學習；如果模型太過複雜了，我們也有很多種正規化的方法來讓模型退回叫簡單的模型，並可透過 lambda 這個參數來調整退回的程度。

我們可以任意組合，但組合完之後我們要怎麼判斷哪個組合未來在做預測時效果會比較好呢？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-2.png">
</p>

### 用 Ein 來做選擇

如果我們用 Ein 來做選擇，那就永遠會選擇到比較複雜的模型，這在上一講中我們已經知道這很可能會有 Overfitting 發生。所以用 Ein 來做選擇是很危險的。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-3.png">
</p>

### 用 Etest 來做選擇

使用 Etest 來做選擇，基本上理論上是可行的，但 Etest 實際在我們訓練的過程中是不能拿來用的，直接拿 Etest 來幫助我們選擇模型其實是一種作弊行為。所以用 Etest 來做選擇也是不可行的。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-4.png">
</p>

### 引進 Eval

既然用 Ein 或 Etest 來做選擇是不可行的，那如果我們把我們手中的資料 D 保留一份下來作為 Dval，然後在訓練的過程中都不使用 Dval，等訓練完之後，在挑選各種模型的時候再用 Dval 來做選擇，那這樣會是一個比較安全的做法。

這有點像是我們在練習時，會把一些練習題留下來，等考試之前再驗證看看自己的成果如何，機器學習也用上了這個概念。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-5.png">
</p>

### 進一步了解 Dval

所以有了 Dval 的概念之後，我們就會把拿到的資料先分成 Dtrain 及 Dval，Dtrain 用來做訓練得出 g-，Dval 用來做驗證。在霍夫丁不等式的理論中，我們可以保證 Eout(g-) 會跟 Eval(g-) 很接近。所以用 Eval 來選擇最好的模型是可行的。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-6.png">
</p>

### 選出 Eval 表現最好的模型

所以現在當我們有很多個模型需要做選擇時，每個會用訓練資料先得出各自最好的 g-，然後我們再用驗證資料計算 Eval，Eval 表現最好的模型就是我們要的。不過 g- 使用的訓練資料較少，也因此未來的表現也可能因為訓練資料少而受影響。所以我們選出了最好的模型之後，會再將所有的資料使用進去訓練出一個最好的 g。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-7.png">
</p>

### 驗證資料的影響

我們用一些實驗來看驗證資料的影響，用 Ein 來選的話，Eout 就會是上面那條黑實線，因為 Ein 永遠會選擇最複雜的模型。然後用 Etest 來選模型，當然會得到最好的 Eout 值，但這是作弊。紅色的線代表我們用 g- 直接來做預測，當驗證資料越多的時候，g- 的 Eout 值就變高了，有時甚至比 Ein 選出來的模型還差。藍色的線代表我們用驗證資料選出模型之後，再將全部的資料丟進去訓練出 g，如此得到的效果都會比用 Ein 來選好。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-8.png">
</p>

### 那要保留多少驗證資料

從上面的實驗，我們會知道驗證資料的多寡也會影響選出來的模型，所以我們應怎麼選擇保留多少驗證資料呢？實務上我們目前都是用 1/5 的資料作為驗證資料。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-9.png">
</p>

### 一個極端的例子

我們從 Eout(g) 及 Eout(g-) 及 Eval(g-) 的關係中觀察，如果我們的驗證資料 k 越小，那 Eout(g) 與 Eout(g-) 就會越接近；但驗證資料 k 越大，那 Eout(g-) 及 Eval(g-) 就會越接近；有沒有方法可以讓 Eout(g) 跟 Eout(g-) 很接近，卻又可以讓 Eval 可以正確地挑出最好的模型。

這個方法就是 leave-one-out cross validataion，每次只保留一個資料作為驗證資料，重複這個過程，直到所有的資料都做過驗證資料，並將所有的 Eval 做平均之後，Eval 最好的那個模型就會是我們想要的模型。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-10.png">
</p>

### 用一個簡單的例子來說明 Leave One Out

我們用一個簡單的例子來說明 Leave One Out Cross Validation 選擇模型的效果。假設現在我們有三個點，現在有兩個模型要做選擇，一個是線性模型，一個是常數模型。從下圖我們可以看出常數模型的 Eloocv 會比較小，所以我們就會用常數模型作為我們最後訓練完的結果。

這也告訴我們，當資料很少的時候，有時選擇簡單的模型效果反而會比較好。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-11.png">
</p>

### 理論上也有保證

我們剛才都是以實驗上的角度來說明 cross validation 是有效果的，這邊有一個理論推導也可以支持這個結果。推導 Eloovc 的期望值時，最後可以得到跟 Eout(N-1) 平均相等。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-12.png">
</p>

### Leave-One-Out Cross Validation 的缺點

雖然 Leave-One-Out Cross Validation 在理論上的確可以讓我們得到的結果很接近真實得到的 Eout，但這個方法也有缺點。如果我們有 1000 個資料，那我們就每個模型都要訓練一千次來計算出各自的 Eloocv，這樣計算量會非常大。

然後觀察下圖 Eloovc 的曲線，我們可以看出隨著 Feature 值的上升，Eloocv 值不會是一個穩定下降再上升的曲線，它會有跳動的情況發生（例如多個模型表現都很好的情況），所以有時會造成選擇的盲點。

因此實務上我們都不會使用 Leave-One-Out Cross Validation 這個方法來選擇模型。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-13.png">
</p>

### 分份數的概念

Leave-One-Out Cross Validation 很像是把 D 個資料分成 D 分來做 cross validation，那我們可以將份數變少，比如說分成 5 份或 10 份做 cross validation，這樣就可以大大減少計算量了。

目前實務上都是分 10 份，使用 10-fold cross validation。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-14.png">
</p>

### 一些提醒

Cross Validaton 是用來做模型的選擇，基本上也會是用風險，因此 validation 表現的結果很好，也不是百分之百未來做預測時效果都會很好。還是要記得觀察未來的預測情況。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-15.png">
</p>

### 總結

由於我們已經學會了很多機器學習的方法，有許多地方可以調整我們學習的模型，所以在眾多的學習模型中哪個是最好的，我們也需要有一個方法來幫助我們做選擇，這個方法就是 Cross Validation。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-15-16.png">
</p>