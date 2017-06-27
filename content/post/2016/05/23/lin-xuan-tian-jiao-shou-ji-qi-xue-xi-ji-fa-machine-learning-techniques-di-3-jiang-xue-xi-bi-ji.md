+++
title = "林軒田教授機器學習技法 Machine Learning Techniques 第 3 講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-3-jiang-xue-xi-bi-ji"
date = "2016-05-23T17:39:46.000Z"
url = "/2016/05/23/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-3-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習技法（Machine Learning Techniques）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第 2 講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-fa-machine-learning-techniques-di-2-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

在上一講中，我們介紹了 Dual SVM，這是為了讓我們可以對資料點做高維度的特徵轉換，這樣就可以讓 SVM 學習更複雜的非線性模型，但我們又不想要跟高維度的計算牽扯上關係，Dual SVM 將問題作了一些轉換，能夠將演算法跟高維度的計算脫鉤，但上一講中的 Q 矩陣實際上還是計算了高維度特徵矩陣內積，所以並沒有真的解決問題。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-1.png">
</p>

### Dual SVM 仍與高維度 d 有依賴關係

目前推導出來的 Dual SVM 仍與高維度 d 有依賴關係，我們能不能簡化 Q 矩陣的高維度特徵矩陣內積計算呢？

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-2.png">
</p>

### 觀察矩陣內積的每一個運算

我們用二次轉換拆開來觀察，發現原本將矩陣進行特徵轉換之後在做矩陣內積，可以分成 0 次項、1 次項、 2 次項分開來計算，結果會是一樣的。而更高維度的轉換也會有相同的性質。如此我們就可以限制計算量只在原本的特徵維度 O(d)。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-3.png">
</p>

### Kernel 的概念

有了上述的性質，我們可以引進 Kernel 的概念，之前都是將矩陣進行特徵轉換之後再去計算內積，現在我們可以改成使用 kernel function 來做計算，znTzm 可以改成對應的 kernel function K(xn, xm)。

由於我們都不去 z 空間做計算了，因此也無法得到 z 空間的 w，所以 b 與 w 的式子都要改成使用 kernel function K(xn, xm) 來計算。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-4.png">
</p>

### 用 QP 解 Kernel SVM

導出 Kernel function 之後，我們一樣可以將 kernel function 計算出來的 Q 矩陣丟進去 QP Solver 來解 SVM。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-5.png">
</p>

### Polynomial Kernel

我們可以將 Kernel Function 整理成更一般化的形式，這樣就可以推導出各式各樣的 Polynomail Kernel。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-6.png">
</p>

### Poly-2 Kernel 圖示

我們使用一個例子來看一下 Poly-2 Kernel 的效果，我們可以調整 gamma 參數得出不一樣的分類曲線。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-7.png">
</p>

### Polynomial Kernel 一般化

由 Poly-2 Kernel，我們可以再做更多變化，常數項用 zeta 當參數、特徵空間轉換用 Q 當參數，加上原本的 gamma 參數，Polynomial SVM 可以很自由地調整 Kernel 參數來得到更好的分類效果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-8.png">
</p>

### 無限多維轉換的 Kernel

由於我們的演算法已經跟高維度的空間脫鉤了，所以我們有了這樣的想法，我們是不是可以使用無限多維轉換的 kernel 呢？

我們觀察一下指數函數 exp(-(x-x')^2)，結果發現就是一個對 X 的無限多維轉換，由此我們可以推導出下式的無限多維轉換 Kernel，也稱為 Gaussian kernel。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-9.png">
</p>

### Gaussian SVM

推導出 Gaussian Kernel 之後，使用 Gaussian Kernel 的 SVM 就是 Gaussian SVM。Gaussian SVM 演算法會與 Polynomial SVM 一樣，只是 Kernel 不一樣，由於是無限多維轉換，我們也不用再去煩腦要用幾次的轉換。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-10.png">
</p>

### 觀察 Gaussian SVM 的效果

Gaussian SVM 是無限多維的轉換，因此可以預期它有很強的 power 可以做好分類，同時又保證 mergin 最大可以避免 overfit。但下圖中實驗調整 Gaussian Kernel 的 gamma 參數，其實還是有可能會產生 overfit，所以 Gaussian SVM 也不是萬能的，還是要謹慎驗證計算出來的結果。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-12.png">
</p>

### 回顧 Linear Kernel 優缺點

我們來回顧一下目前學過的 Kernel。首先是 Linear Kernel，優點是模型較為簡單，也因此比較安全，不容易 overfit；可以算出確切的 W 及 Support Vectors，解釋性較好。缺點就是，限制會較多，如果資料點非線性可分就沒用。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-13.png">
</p>

### 回顧 Polynomial Kernel 優缺點

再來是 Polynomial Kernel，由於可以進行 Q 次轉換，分類能力會比 Linear Kernel 好。缺點就是高次轉換可能會有一些數字問題產生，造成計算結果怪異。然後太多參數要選，比較難使用。也因此 Polynomial Kernel 可能會用在比較低次轉換的 SVM 問題上，但這樣也許就可以用 Linear SVM 取代。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-14.png">
</p>

### 回顧 Gaussian Kernel 優缺點

最後是 Gaussian Kernel，優點就是無限多維的轉換，分類能力當然更好，而且需要選擇的參數的較少。但缺點就是無法計算出確切的 w 及 support vectors，預測時都要透過 kernel function 來計算，也因此比較沒有解釋性，而且也是會發生 overfit。比起 Polynomail SVM，Gaussian SVM 比較常用。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-15.png">
</p>

### 其他 Kernel

除了目前介紹的 Kernel 之外是否還有其他 Kernel 呢？當然有，你也可以自己定義自己的 Kernel，只要符合 Mercer's condition 就是一個合法的 Kernel。不過要定義自己的 Kernel 並不是件容易的事。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-16.png">
</p>

### 總結

在這一講中，我們終於脫離了高維度空間的計算依賴，使用 Kernel Funciton 來解 Dual SVM，因此引進了 Polynomial Kernel SVM 的概念，最後甚至推導出了無限多維轉換的 Gaussian Kernel SVM。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Techniques-3-17.png">
</p>