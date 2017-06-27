+++
title = "林軒田教授機器學習技法 Machine Learning Techniques 第 6 講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-6-jiang-xue-xi-bi-ji-2"
date = "2016-08-06T05:51:47.000Z"
url = "/2016/08/06/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-6-jiang-xue-xi-bi-ji-2"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習技法（Machine Learning Techniques）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第 5 講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-5-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在上一講中，我們了解了如何使用 SVM 來解 Logistic Regression 的問題，一個是使用 SVM 做轉換的 Probabilistic SVM，一個是使用 SVM  Kernel Trick 所啟發的 Kernel Logistic Rregression。這一講我們將繼續介紹如何延伸到解 Regression 的問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-1.png">
</p>

### 利用 Representer Theorem 延伸

從數學模型上，我們發現 L2-regularized 線性模型都可以轉換成 Kernel 形式，而 Linear/Ridge Regression 都有公式解，那麼 Kernel Ridge Regession 也可以推導出公式解嗎？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-2.png">
</p>

### Kernel Ridge Regression 數學式

我們使用 Representer Theorem 將 Kernel 應用至 Ridge Regression 的數學式上，得到以下 Kernel Ridge Regression 數學式。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-3.png">
</p>

### 解 Kernel Ridge Regression 最佳化

接下來我們利用偏微分來計算 Kernel Ridge Regreesion 數學式的最佳化，對 beta 進行偏微分為 0 時即可求得 beta 最佳解。我們可以很簡易的用這個式子做到非線性的 Regression。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-4.png">
</p>

### Linear 及 Kernel Ridge Regression 的比較

Linear 及 Kernel Ridge Regression 比較起來，當然 Linear 模型較簡易，因此計算效能較好，而 Kernel Ridge Regression 由於可以做非線性轉換，因此有更強的彈性。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-5.png">
</p>

### Soft-Margin SVM 與 Least-Squares SVM 的比較

當我們使用 Kernel Ridge Regression 做分類時，這就是 Least-Squares SVM，Least-Squares SVM 與 Soft-Margin SVM 比較起來，他們的邊界會很接近，但會有更多的 Support Vector，如此在做預測時會慢一些。Suppport Vector 的數量跟 beta 有關，我們可以讓 beta 變得跟標準的 SVM 一樣稀疏嗎？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-6.png">
</p>

### Tube Regression 模型

我們重新思考一個新模型 Tube Regression，讓錯誤在一定範圍內為 0，當錯誤超過界線時，我們再以錯誤的點與邊界的距離當作錯誤值。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-7.png">
</p>

### L2-Regularized Tube Regression

將 Tube Regression 的性質帶入 L2-Regularized，與 SVM 對照一下，目前的 L2-Regularized Tube Regression 並不能微分，雖然可以 Kernel 化，但卻不知有沒有跟 SVM 一樣有稀疏 Support Vector 的性質。

我們將 L2-Regularized Tube Regression 改成跟 SVM 幾乎一樣的形式來求解看看，這就是 Support Vector Regression。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-8.png">
</p>

### Support Vector Regression Primal 形式

首先我們來推導一下 Support Vector Regression 的 Primal 形式，由於目前的數學式有絕對值，所以我們使用上界的錯誤及下界的錯誤做展開，如下數學式。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-9.png">
</p>

### 帶入 Lagrange Multiplier

如同解 SVM 的對偶問題，我們使用了 Lagrange Multiplier 的技巧，這邊也是一樣，但由於有上界的錯誤及下界的錯誤，我們也需要有上界的 Lagrange Multiplier 及 下界的 Lagrange Multiplier。

如此就可以仿造解 Dual SVM 一樣，去解出最佳解時 SVR 的 KKT Conditions。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-11.png">
</p>

### 比較一下 SVM Dual 及 SVR Dual

SVM Dual 及 SVR Dual 數學式比較如下圖所示，因此如同之前使用 QP Solver 解 SVM Dual，我們可以將 SVR Dual 對應的變數帶入 QP Solver 來解 SVR Dual。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-12.png">
</p>

### SVR 的稀疏性質

從 SVR 最佳解的條件中，當錯誤值在 tube 範圍內時，我們會訂為 0，然後因為點在 Tube 裡面，所以 y 跟分數的差值是不等於 0 的，依照 complementary slackness，如此 alpha 上界跟 alpha 下界就都是 0，alpha 上界與 alpha 下界相減是 beta，這樣就代表 beta 也是 0。而 Support Vetor 是 beta 不等於 0 的點，所以這就代表 SVR 有稀疏 Support Vetor 的性質。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-13.png">
</p>

### 總結

在這一講中我介紹了 Kernel Ridge Regression 及 Support Vetor Regression，有關 SVM 的相關模型已經都介紹完畢了，之後的課程將介紹如何像雞尾酒那樣結合各種學習模型。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-6-16.png">
</p>