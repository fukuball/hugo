+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第十一講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-jiang-xue-xi-bi-ji-2"
date = "2016-01-29T09:02:33.000Z"
url = "/2016/01/29/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-jiang-xue-xi-bi-ji-2"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第十講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-shi-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在上一講中我們了解了 Logistic Regression 演算法並了解了如何使用 Logistic Regrssion 來預測心臟病發病機率這樣的問題，這一講中將延伸之前學過的演算法，在理論上說明 Linear Regression 以及 Logistic Regression 都可以用來解 Binary Classification 的問題。學會了 Binary Classification 之後，我們也可以用這樣的技巧來解 Multi-Classification 的問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-1.png">
</p>

### 比較之前學過的演算法

比較之前學過的演算法，三個算法最後都會得到一個線性函數來輸出 scroe 值，但 PLA 做 Linear Classification 是一個 NP-hard 的問題，Linear Regression 及 Logistic Regression 則相對較容易求解，我們可以使用 Linear Regression 或是 Logistic Regression 演算法來解 Linear Classification 的問題嗎？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-2.png">
</p>

### 將三個演算法的 Error Function 整理一下

依據各個 Error Function 的算法，我們都可以整理成 ys 的形式，在物理意義上，我們可以說 y 代表正確性，s 代表正確或錯誤程度多少。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-3.png">
</p>

### 畫成圖來瞧瞧

我們以 ys 為橫坐標，error 為縱坐標，把這三個函數畫出來。 0/1 error 在 ys <= 0 時 error 是 1，squre error 在 ys << 1 或 ys >> 1 時會很大，cross-entropy error 在 ys 很小時， error 也會變得很大，但當 squre error 跟 cross-entropy error 很小時，他們 ys 區間所對應的 squre error 也會很小，因此我們可以從這樣的圖得知 squre error 跟 cross-entropy error 都是 0/1 error 的上界。 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-4.png">
</p>

### 套用至 VC Bound 理論

將這樣的 Error 上界關係套用 VC Bound 理論，只要 Logistic Regression 或 Linear Regression 的 E_in 小，那 Linear Classfication 的 E_out 就會小，因此理論上我們可以使用 Logistic Regression 及 Linear Regression 來代替 Linear Classfication。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-5.png">
</p>

### 使用 Regression 來做分類

依據以上的理論，我們可以用 Regression 來代替 PLA/Pocket 做分類，會比較有效率（PLA 是一個 NP-hard 的問題），比較一下三個演算法，(1) PLA 在線性可分的時候可以得到一個最佳解，但資料常常不會是線性可分，所以就會用 Pocker 來替代。（2）Linear Regression 可以很快的優化求解，但當 |ys| 很大的時候，positive direction 及 negative direction 的 bound 都太鬆，E_out 可能會效果不好。(3) Logistic Regression 可以用 gradient descent 求解，但在 negative direction 的 bound 會太鬆，E_out 可能會效果不好。

以據上述的特性，我們可以使用 Linear Regression 跑出一個 w 作為 (PLA/Pocket/Logistic Regression) 的 w0，然後再使用 w0 來跑其他模型，這樣可以加快其他模型的優化速度。然後實務上拿到的資料常常不是線性可分的，所以我們會比較常使用 Logistic Regression 而不是 PLA/Pocket。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-6.png">
</p>

### 優化 Logistic Regression

實務上我們會比較常使用 Logistic Regression，但 Logistic Regression 比起 PLA 比較沒有效率，因為 Logistic Regression 在決定優化方向時，會觀察所有的資料點再做決定，時間複雜度是 O(N)，但 PLA 每次只看一個點，時間複雜度是 O(1)，我們可以讓 Logistic Regression 優化到 O(1) 嗎？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-7.png">
</p>

### 隨機梯度下降

我們可以使用隨機梯度下降的方式讓 Logistic Regresiion 優化到 O(1)，這樣的方法就是每次只透過隨機選取一個資料點（xi, yi）來取梯度，然後再用這個梯度對 w 進行更新，這種優化方法就叫做隨機梯度下降。

原來的演算法是用所有的資料點在算梯度，然後取平均，再更新 W，隨機梯度下降是不用每次算所有的點，每次只算一個點來代替所有點的平均。可以這樣做的背後原理，我們可以想成隨機取一個點取很多次之後，大概就是跟所有的點做平均差不多，所以我們可以用隨機梯度下降取代原本的梯度下降。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-8.png">
</p>

### 隨機梯度下降與 PLA 的關係

將隨機梯度下降與 PLA 算式放在一起觀察，可以發現隨機梯度是一個軟性的 PLA，每次調整 0~1 ynxn，但 PLA 只有調與不調，比較硬。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-9.png">
</p>

### 多元分類

我們現在已經會 Binary Classification 了，那 Multi-Classification 的問題要怎麼解呢？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-10.png">
</p>

### 一次分一個類別出來

既然我們會二元分類，我們可以一次分一個類別出來，讓現在要分類出來的資料是 o，其他資料設成 x 來做分類。以這個例子就是先把正方形變成 o，其他變成 x。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-11.png">
</p>

### 結合所有的二元分類

結合所有的二元分類模型之後，我們就可以做多元分類了，不過會有一些區域有模糊地帶。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-12.png">
</p>

### 使用軟性二元分類來解模糊地帶的問題

在這邊我們可以使用軟性二元分類來解模糊地帶的問題，比如將所有的二元分類模型用 Logistic Regression 來訓練，就能讓每個分類器預測出資料是屬於哪一類的百分比，這樣我們就可以從所有的分類器裡面找出百分比最大的那個來預測這個資料點是屬於哪一類，而解決模糊地帶的問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-13.png">
</p>

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-14.png">
</p>

### One-Versus-ALL (OVA) Decomposition

這樣的方法就是 One-Versus-ALL (OVA) Decomposition，每次把一個類別和非這個類別的當成兩類，用 Logistic Regresion 分類，當分類器輸入某個點，就看這個點在哪一個類別的機率最大。不過這個方法的缺點是，當類別很多的時候，比如 k=100，那每次用 logistic Regression 分類時正樣本和負樣本的差別就會非常大，訓練出來的結果可能會不好。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-15.png">
</p>

### 一次只比較兩個類別

我們可以用一次只比較兩個類別這樣的方法來解決 OVA 樣本資料差距過大的問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-16.png">
</p>

### 投票預測分類

這樣的方法，每次只取兩個類別來做訓練，如果一共有 K 類的話，就要做  C(K, 2) 次的 Logistic Regression。當一個資料點輸入做預測時，就用這 C(K, 2) 個分類器給所有 K 個類別投票，取票數大的作為輸出結果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-17.png">
</p>

### One-Versus-One (OVO) Decomposition

這樣的方法就是 One-Versus-One (OVO) Decomposition，這種方法的好處是可以應用在任何 Binary Classification 方法，缺點是效率可能會低一些，因為要訓練 C(K,2) 個類別，不過如果類別很多且每個類別的樣本量都差不多的時候，OVO 的方法不一定會比 OVA 方法效率低。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-18.png">
</p>

### 總結

在第十一講中，我們比較了 PLA、Linear Regression 及 Logistic Regression，然後理論上這三個演算法都可以應用在 Linear Classifition 上，然後也學會了使用 Stochastic Greadient Descent 來讓 Logistic Regression 跟 PLA 演算法的計算時間複雜度一樣。學會了 Binary Classification 之後，我們也可以將這樣的方法運用 OVA 及 OVO 的方式來解 Multi-Classification 的問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-11-19.png">
</p>