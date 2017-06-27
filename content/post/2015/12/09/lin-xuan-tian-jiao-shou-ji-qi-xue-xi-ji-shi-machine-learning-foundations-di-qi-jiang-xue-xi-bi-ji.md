+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第七講學習筆記"
slug = "lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-qi-jiang-xue-xi-bi-ji"
date = "2015-12-09T18:10:38.000Z"
url = "/2015/12/09/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-qi-jiang-xue-xi-bi-ji"
+++

### 前言

本系列部落格文章將分享我在 Coursera 上台灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明。若還沒有閱讀過 [第六講](http://blog.fukuball.com/lin-xuan-tian-jiao-shou-ji-qi-xue-xi-ji-shi-machine-learning-foundations-di-liu-jiang-xue-xi-bi-ji/) 的碼農們，我建議可以先回頭去讀一下再回來喔！

在第六講我們可以知道 Break Point 的出現可以大大限縮假設集合成長函數，而這個成長函數的上界是 B(N, k)，且可推導出 B(N, k) 是一個多項式，經過一些轉換與推導我們可以把無限的假設集合代換成有限的假設集合，這個上界我們就稱之為 VC Bond。因此可以從數學理論中得知 2D perceptrons 是可以從數據中得到學習效果，而且也不會有 Ein 與 Eout 誤差過大的情況發生，而這一講將進一步說明 VC Bond。

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 熱身回顧一下

上一講，我們從 break point 的性質慢慢推導出成長函數是一個多項式，因此我們可以保證 Ein 與 Eout 的差距在 N 資料量夠大的情況下不會因為假設集合的無限累積而差距變得很大。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-1.png">
</p>

### 將成長函數寫得更簡潔一點

目前我們知道假設集合的成長函數是 B(N, k) 這個多項式，實際算出來的值如左圖，其實我們可以直接用 N 的 k-1 次方來表示，實際算出來的值如右圖，總之 B(N, k) 會小於 N 的 k-1 次方，所以我們可以直接用 N 的 k-1 次方來表示成長函數。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-2.png">
</p>

### VC Bond 告訴我們什麼

將 VC Bond 簡化的成長函數 N 的 k-1 次方帶進上一講的霍夫丁不等式裡，式子可以簡化成下圖。這個式子告訴我們：1. 當成長函數有 break point k，也就是說假設集合很好，2. N 的資料量夠大，也就是說有足夠的好資料集，3. 如果我們有一個演算法可以找出一個 g 讓 Ein 很小，也就是說我們有好的演算法，那麼我們大概就可以說我們讓機器可以學到技巧了。

（當然還是要有好運氣，因為有可能壞事情還是會發生，只是機率較低）

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-3.png">
</p>

### VC Dimension

我們將最大的非 break point 的維度稱之為 VC Dimension。所以 d＿vc 就是 k-1。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-4.png">
</p>

### 定義好 VC Dimension 之後

定義好 VC Dimension 之後，之前舉的 break point 例子就可以改寫成 vc dimension，其中 2D perceptrons 的 vc dimension 就是 3（break point 是 4）。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-5.png">
</p>

### VC Dimension 與機器學習

我們回到機器學習的概觀圖，vc dimension 的概念告訴我們，當我們有有限的 d＿vc 時，此時演算法所找出的 g 會讓 Eout 與 Ein 很接近。而且不用管用的演算法 A 是什麼、資料 D 是從哪種資料分佈產生的、也不用管 target f 到底是什麼。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-6.png">
</p>

### 對應到 2D PLA

我們把這樣的概念對應到 2D PLA，2D PLA 會從線性可分的資料集 D 中找出一個 g 讓 Ein 為 0。然後 VC Dimention 告訴我們 2D PLA 的 d＿vc 是 3，在資料集 N 夠大的情況下可以保證 Ein(g) - Eout(g) 的差距很小，因此我們就可以說 2D PLA 的 Eout(g) 也會接近 0，這也就是說我們讓機器學習到技巧了。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-7.png">
</p>

### VC Dimention 跟 Perceptrons 的關係

我們知道 1D perceptron 的 d＿vc 是 2，2D Perceptron 的 d＿vc 是 3，所以我們會猜，d-D 的 perceptrons 的 d＿vc 會不會是 d+1，理論上證明這樣的想法是對的，證明的方法有兩個步驟，第一步證明 d＿vc >= d+1，第二步證明 d＿vc <= d+1，這邊不詳述證明細節。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-8.png">
</p>

### 模型複雜度

我們將新的霍夫丁不等式做一些轉換，將右式表示成 δ（壞事情發生的機率），那 1-δ 就代表是好事情發生的機率，就就是 Ein(g) - Eout(g) <= ε，我們可以知道 d＿vc 會影響壞事情（Ein 與 Eout 差距大）發生的機率，d＿vc 越高，就代表假設集合模型複雜度越高，但也可能讓壞事情發生的機率變高。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-9.png">
</p>

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-10.png">
</p>

### 模型複雜度圖示

從式子中我們可以看出機器學習的模型複雜度關係如下圖，當 d＿vc 上升時，Ein 會下降，但 Ω 會上升，當 d＿vc 下降時，Ein 會上升，但 Ω 會下降，所以 Eout 要最小 d＿vc 一定是在中間，也就是我們的模型複雜度不能太高也不能太低。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-11.png">
</p>

### 樣本複雜度

從新的霍夫丁不等式我們也可以來算一下樣本複雜度，比如現在我們需要壞事情 Ein 與 Eout 的差距 > ε＝0.1 的機率 <= δ=0.1，且已知 d＿vc=3，這樣我們會需要多少個樣本呢？理論上我們會大概需要 10000 X d＿vc 個樣本點，也就是說 2D perceptrons 大概就需要 30000 個樣本點。但實務上發現只要大概 10 x d＿vc 個樣本點就足夠了。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-12.png">
</p>

### 總結

在第七講中我們定義了 VC Dimension，就是最大的 non-break point，然後在 perceptrons 這樣的模型中，d＿vc 剛好等於 d+1，物理意義上可以想成可以調整的自由度有幾個維度。引進 VC Dimension 的概念之後，我們可以了解到機器學習的模型複雜度及樣本複雜度關係。

<p style="text-align:center">
    <img src="http://static.obeobe.com/image/blog-image/Machine-Learning-Foundations-7-13.png">
</p>