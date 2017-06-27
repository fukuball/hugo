+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第九講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-jiu-jiang-xue-xi-bi-ji"
date = "2016-01-06T11:52:22.000Z"
url = "/2016/01/06/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-jiu-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第八講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-ba-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在第八講中我們機器學習流程圖裡加入了 error function 及 noise 的概念，並了解在這樣的情況下機器學習還是可行的。前面花了很大的篇幅在說機器為何可以學習，接下來是要說明機器是怎麼學習的。本篇以眾所皆知的線性迴歸為例，從方程式的形式、誤差的衡量方式、如何最小化 Ein，讓我們對線性迴歸在機器學習上的應用有些理解。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-1.png">
</p>

### 信用卡額度問題

回到信用卡這個例子，假設我們現在需要的是判定要發多少信用額度給申請者，這種問題的答案就從發不發卡變成了一個實數，這就是線性迴歸的問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-2.png">
</p>

### 線性迴歸

將上述問題寫成線性迴歸式就如下圖，其實與 perceptron 很像，但不用再取正負號。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-3.png">
</p>

### 圖解線性迴歸

圖解線性迴歸問題就會如下圖所示，找一條線或超平面來讓所有的資料點與之的差距最小。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-4.png">
</p>

### 線性迴歸的錯誤衡量

線性迴歸的錯誤衡量一般是使用平方錯誤，所以在計算 Ein 的過程是算出平均平方錯誤最小的值，而 Eout 的差距就可以用平方錯誤來計算效果。最小的 Ein 如何計算呢？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-5.png">
</p>

### 整理成矩陣的形式

我們將 Ein 的式子整理成矩陣的形式，推導過程如下。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-6.png">
</p>

### 最小的 Ein

整理成這種式子的 Ein 理論上已知是個連續、處處可微的凸函數，所以計算最小的 Ein 就是去解每一個維度進行偏微分為 0 所得到的值。他的物理意義就是在這個凸函數中這個點在各個維度都無法再下滑。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-7.png">
</p>

### 最小的 Ein 就是計算 Ein 的梯度

這就是在計算 Ein 的梯度，我們將原本的式子展開後，並對這個式子做偏微分。對矩陣的偏微分的理解我們可以從 1 個維度慢慢推廣，如此就可知 XTXw - XTy = 0 時可以得到最佳解。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-8.png">
</p>

### 線性迴歸最佳解

有上所得到的結果，如果 X^TX 是有反矩陣的話，那就可以很容易的算出 (X^TX)-X^Ty 是我們得到的最佳解，其中 (X^TX)-X^T 又稱為 pseudo-inverse，但如果 X^TX 是 singular，那就無法這樣算出一個最佳的 pseudo-inverse，但還是有辦法得出一個 pseudo-inverse，記為 X+，通常我們會用內建的數學方法得出 pseudo-inverse。 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-9.png">
</p>

### 線性迴歸機器學習演算法

如此線性迴歸機器學習演算法就會是這樣，第一步，特徵資料組成一個矩陣 X，答案組成一個向量 y，第二步，計算 X 的 pseudo-inverse，第三步，將 X pseudo-inverse 與 y 做內積，如此就可以得到最佳解 W。 

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-10.png">
</p>

### 線性迴歸到底是不是機器學習演算法

由於好像是用一個式子就算出答案，所以有人會懷疑線性迴歸到底是不是機器學習演算法，線性迴歸在本質上的確跟遵循機器學習流程，在計算 psedo-inverse 的過程其實就有學習調整的過程，只是我們直接用別人寫好的函式沒辦法看出來，另外，機器學習其實就是想要做到 Eout 好，如果 Eout 好那就是一個機器學習演算法。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-11.png">
</p>

### 分析線性迴歸的 Ein 與 Eout

用一些理論來分析線性迴歸的 Ein 與 Eout，Ein 平均可以推導到 noise level x (1-(d+1)/N)，第一步推導如下圖，我們又稱 XX+ 為 hat matrix H，因為它讓真實的答案 y 變成了預測的答案 y hat，所以就叫 hat matrix H。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-12.png">
</p>

### Hat Matrix H 的物理意義

y hat 物理意義就是 X 的線性組合，原本有很多個 y hat，可以組成一個線性組合空間，迴歸分析就是在算 y - yhat 最小的，Hat Matrix H 就是把 y 投影到 yhat，然後 I-H 可以將 y 線性轉換到 y - yhat，代表真實答案與預測答案的差距。其中數學上有個性質 trace(I-H) = N-(d+1)，這個沒有證明，只有用自由度來說明。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-13.png">
</p>

### 用這樣的物理意義來證明 noise level x (1-(d+1)/N)

我們用這樣的物理意義來證明 noise level x (1-(d+1)/N)，我們可以想成 y 是從 f(x) 加上一些 noise 得出來的，這個 noise 被 I-H 線性轉換到 y-yhat，如就可以計算出 Ein 平均會是 noise level x (1-(d+1)/N)。

有趣的是 Eout 會是 noise level x (1＋(d+1)/N)，但證明很複雜。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-14.png">
</p>

### 學習曲線

Ein 跟 Eout 都會隨著 N 越大而收斂，而且 Ein 及 Eout 的差距會被 bound 住，所以也有 VC bound 的性質，因此迴歸分析的確可以達成機器學習效果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-15.png">
</p>

### 線性分類跟線性迴歸

分類 y 是 +1 或 -1，迴歸是實數；分類的假設集合要取 sign，迴歸不用；分類是 0/1 錯誤，迴歸是平方錯誤；分類是個 NP-hard 的問題，不容易算出最佳解，但迴歸可以容易算出最佳解，我們可以把分類問題轉成用迴歸來解嗎？

直覺來想，我們可以算出迴歸解之後，再取 sign，那就變成分類模型了，理論上可以嗎？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-16.png">
</p>

### 觀察分類與迴歸的錯誤衡量

觀察分類與迴歸的錯誤衡量我們可以發現迴歸的平方錯誤曲線是壓在分類的0/1錯誤曲線上的，也就是說平方錯誤一定會比較大。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-17.png">
</p>

### 使用 VC bound 理論將迴歸套用到二元分類

使用 VC bound 理論將迴歸套用到二元分類，可以知道迴歸錯誤會是上界，如果迴歸可以得到 Ein 小，那 Eout 就會小，因此可以將迴歸套用在二元分類上，這樣會比算 PLA 有效率，雖然效果不一定比較好。

我們也可以將迴歸用在先期計算，先計算出最好的 PLA 初始線，然後再進行 PLA 演算法，如此就可以增加 PLA 的效能。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-18.png">
</p>

### 總結

當我們要機器回答實數解的時候，那就是線性迴歸問題。而線性迴歸演算法可以用 pseudo-inverse 很快地算出來，Ein 與 Eout 的差距會隨著 N 越大而收斂，而且在理論上我們可以用線性迴歸來解分類問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-9-19.png">
</p>
