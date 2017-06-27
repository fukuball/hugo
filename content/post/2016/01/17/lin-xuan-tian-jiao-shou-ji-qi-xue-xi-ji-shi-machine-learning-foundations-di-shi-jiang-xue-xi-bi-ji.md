+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第十講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-jiang-xue-xi-bi-ji"
date = "2016-01-17T06:03:36.000Z"
url = "/2016/01/17/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第九講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-jiu-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在上一講中我們了解了如何使用線性迴歸的方法來讓機器學習回答實數解的問題，第十講我們將介紹使用 Logistic Regression 來讓機器學習回答可能機率的問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-1.png">
</p>

### 可能性問題

我們用心臟病發生的機率這樣的問題來做為例子，假設我們有一組病患的數據，我們需要預測他們在一段時間之後患上心臟病的「可能性」為何。我們拿到的歷史數據跟之前的二元分類問題是一樣的，我們只知道病患之後有或者沒有發生心臟病，從這樣的數據我們用之前學過的二元分類學習方法可以讓機器學習到如何預測病患會不會發病，但現在我們想讓機器回答的是可能性，不像二元分類那麼硬，所以又稱軟性二元分類，即 f(x) = P(+1|x)，取值的範圍區間在 [0, 1]。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-2.png">
</p>

### 軟性二元分類

我們的訓練數據跟二元分類是完全一樣的，x 是病人的特徵值，y 是 +1（患心臟病）或 -1（沒有患心臟病），沒有告訴我們有關「患病機率」的訊息。回想在二元分類中，我們使用 w\*x 得到一個「分數」之後，再利用取號運算 sign 來預測 y 是 +1 或是 -1。對於目前這個問題，如果我們能夠將這個「分數」映射到 [0, 1] 區間，似乎就可以解這個問題了～

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-3.png">
</p>

### Logistic 假設

我們把上面的想法寫成式子，就是 h(x) = theta(wx)，映射分數到 [0, 1] 的 function 就叫做 logistic function，用 theta 來表示

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-4.png">
</p>

### Logistic 函式

Logistic regression 選擇使用了 sigmoid 來將值域映射到 [0, 1]，sigmoid 是 f(s) = 1 / (1 + exp(-s))，f(x) 單調遞增，0 <= f(x) <= 1。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-5.png">
</p>

### 如何定義 Logistic Regression 的 Error Function

那麼對於 Logistic 假設，我們要如何定義 Logistic Regression 的 Error Function E_in(h)？回顧一下之前學過的方法，Linear Classificaiton 是使用 0/1 Error，Linear Regression 是使用 Squared Error。

Logistic Regression 的目標是找到 h(x) 接近 f(x)＝P(+1|x)，也就是說當 y=+1 時，P(y|x) = f(x)，當 y=-1 時，P(y|x) = 1-f(x)。我們要讓 Error 小，就是要讓 h(x) 與 f(x) 接近。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-6.png">
</p>

### 使用 Likelihood 的概念

我們知道資料集 D 是由 f(x) 產生的，我們可以用這樣的思路去想，f(x) 跟 h(x) 生成目前看到的資料集 D 的機率是多少，用這種 Likelihood 的概念，我們只要在訓練過程讓 h(x) 跟 f(x) 產生資料集 D 的機率接近就可以。

不過我們並不知道 f(x)，但我們可以知道 f(x) 產生資料集 D 的機率很高，因為確實就是由 f(x) 產生的。

簡而言之就是產生目前所看到的資料集是一個我們不知道的 f(x)，f(x) 可能會產生出很多種資料集，我們看到的只是其中之一，但 f(x) 是我們無法知道的，我們可以去算 g(x)，從眾多的 g(x) 去算出那一個最可能產生我們目前看到的資料集，這就是去算 max likelihood，之後我們就可以說 g(x) 跟 f(x) 很像～

所以我們只要計算讓 h(x) Likelihood 越高越好。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-7.png">
</p>

### 將 Likelihood 套用到 Logistic Regression

所以現在問題轉換成了計算 h(x) 越高越好了，得到最高 likelihood 機率值的就是我們所要的 g(x)。

式子就是 g = argmax likelihood(h)

likelihood(h) 的式子可以描述成 P(x1)h(x1) x P(x2)(1-h(x2)) ... P(xn)h(1-h(xn))

又因為 sigmoid 性質 1-h(x) = h(-x)，所以 likelihood(h) 的式子可以描述成 P(x1)h(+x1) x P(x2)(-h(x2)) ... P(xn)h(-h(xn))

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-8.png">
</p>

### 將式子做一些轉換

likelihood(h)＝P(x1)h(+x1) x P(x2)(-h(x2)) ... P(xn)h(-h(xn))，我們要計算的是 max likelihood，所以 	max likelihood(h) 正比於 h(score) 連乘，正比於 theta(yn)theta(wxn) 連乘。

我們取上 ln，不會影響計算結果，所以取 ln 做後續的推導。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-10.png">
</p>

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-11.png">
</p>

### Cross-Entropy Error

如果 max Likelihood 轉換成 Error，作為 Logistic Regression 的 Error Function，就會是求 min 的 -ln theta(ynwxn) 連加，代進 sigmoid theta，就會得到 ln(1+exp(-ywx))，這又稱為 Cross-Entropy Error 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-12.png">
</p>

### 最小化 E_in(W)

機器學習的訓練過程就是最小化 E_in(W)，推導出 Cross-Entropy Error 之後，就可以將 E_in(W) 寫成如下圖所示，該函數是連續、可微，並且是凸函數。所以求解最小值就是用偏微分找到谷底梯度為 0 的地方。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-13.png">
</p>

### 微分過程

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-14.png">
</p>

### E_in(W) 梯度為 0 無法容易求出解

和之前的 Linear Regression 不同，這個 ▿Ein(w) 不是一個線性的式子，要求解 ▿Ein(w)=0 是很困難的。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-15.png">
</p>

### 使用 PLA 優化的方式最佳化

這種情況可以使用類似 PLA 利用迭代的方式來求解，這樣的方法又稱為梯度下降法（Gradient Descent）

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-16.png">
</p>

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-17.png">
</p>

### 逐步優化

要尋找目標函數曲線的波谷，可以想像成一個人站在半山腰，每次都選擇往某個方向走一小步，讓他可以距離谷底更近，哪個方向可以更近谷底(greedy)，就選擇往這個方向前進。

所以優化方式就是 wt+1 = wt + ita(v)，v 代表方向（單位長度），ita 代表步伐大小。

找出 min Ein(wt+ita(v)) 就可以完成機器的訓練了。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-18.png">
</p>

### 轉換成線性

min Ein(wt+ita(v)) 還是非線性的，很難求解，但在細微的觀點上決定怎麼走下一步，原本的 min Ein(wt+ita(v)) 可以使用泰勒展開式轉換成線性的 min Ein(Wt) + ita(V)▿Ein(w)。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-19.png">
</p>

### Gradient Descent 梯度下降

所以我們真正要求解的是 v 乘上梯度如何才能越小越好，也就是 v 與梯度是完全相反的方向。想像一下：如果一條直線的斜率 k>0，說明向右是上升的方向，應該要向左走，反之，斜率 k<0，向右走才是對的。如此才能逐步降低 E_in，求得 min Ein。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-20.png">
</p>

### ita 參數的選擇

解決的方向的問題，代表步伐大小的 ita 也很重要，如果步伐太小，到達山谷的速度會太慢，如果步伐太大，則會很不穩定，E_in 會一下太高一下太低，有可能也會無法到達山谷。理想上在距離谷底較遠時，步伐要大一些，接近谷底時，步伐要小一些，所以我們可以讓步伐與梯度數值成正相關，來做到我們想要的效果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-21.png">
</p>

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-22.png">
</p>

### 完整的 Logistic Regression Learning Algorithm

先初始化 w0，第一步計算 Logistic Regression 的 Ein 梯度，然後更新 w，wt+1 = wt - ita(V)▿Ein(wt)，直到 ▿Ein(wt+1) = 0 或是足夠多的回合之後回傳最後的 wt+1。（每回合計算的時間複雜度與 Pocket PLA 一樣）

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-23.png">
</p>

### 總結

第十講中我們了解了當要用 Logistic Regression 解可能性這樣的問題的時候，我們使用的 sigmoid 來將函數做轉換，因此導出了 cross-enropy error function，最佳化無法直接用偏微分的方式求出解，所以使用了 Gradient Descent 這樣的方式來逐步優化來求出解。 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-10-24.png">
</p>