+++
title = "林軒田教授機器學習基石 Machine Learning Foundations 第一講學習筆記"
slug = "machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji"
date = "2015-08-17T07:17:34.000Z"
url = "/2015/08/17/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji"
+++

### 前言

機器學習（Machine Learning）是一門很深的課程，要直接跳進來學習其實並不容易，因此系統性由淺而深的學習過程還是必須的。這一系列部落格文章我將分享我在 Coursera 上臺灣大學林軒田教授所教授的機器學習基石（Machine Learning Foundations）課程整理成的心得，並對照林教授的投影片作說明，希望對有心學習 Machine Learning 的碼農們有些幫助。

### 範例原始碼：[FukuML - 簡單易用的機器學習套件](https://github.com/fukuball/fuku-ml)

我在分享機器學習基石課程時，也跟著把每個介紹過的機器學習演算法都實作了一遍，原始碼都放在 [GitHub](https://github.com/fukuball/fuku-ml) 上了，所以大家可以去參考看看每個演算法的實作細節，看完原始碼會對課程中的數學式更容易理解。

如果大家對實作沒有興趣，只想知道怎麼使用機器學習演算法，那 [FukuML](https://github.com/fukuball/fuku-ml) 絕對會比起其他機器學習套件簡單易用，且方法及變數都會跟林軒田教授的課程類似，有看過課程的話，說不定連文件都不用看就會使用 [FukuML](https://github.com/fukuball/fuku-ml) 了。不過我還是有寫 [Tutorial](https://github.com/fukuball/FukuML-Tutorial) 啦，之後會不定期更新，讓大家可以容易上手比較重要！

### 如何有效學習機器學習

從基礎來由淺入深，包含理論及實作技術用說故事的方式包裝，比如何時可以使用機器學習、為何機器可以學習、機器怎麼學習、如何讓機器學得更好，讓我們可以記得並加以應用。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-1.png?1">
</p>

### 從人的學習轉換到機器學習

人學習是為了習得一種技能，比如學習辨認男生或女生，而我們可以從觀察中累積經驗而學會辨認男生或女生，這就是人學習的過程，觀察 -> 累積經驗、學習 -> 習得技能；而機器怎麼學習呢？其實有點相似，機器為了學習一種技能，比如一樣是學習辨認男生或女生，電腦可以從**觀察資料**及**計算**累積**模型**而學會**辨認**男生或女生，這就是機器學習的過程，資料 -> 計算、學習出模型 -> 習得技能。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-2.png">
</p>

### 再定義一下什麼是技能

「師爺，翻譯翻譯什麼是他媽的技能」「技能不就是技能嗎」在機器學習上，技能就是透過計算所搜集到的資料來提升一些可量測的性能，比如預測得更準確，實例上像是我們可以搜集股票的交易資料，然後透過機器學習的計算及預測後，是否可以得到更多的投資報酬。如果可以增加預測的準確度，那麼我們就可以說電腦透過機器學習得到了預測股票買賣的技能了。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-3.png">
</p>

### 舉個例子

各位勞苦功高的碼農們，現在老闆心血來潮要你寫一個可以辨識樹的圖片的程式，你會怎麼寫呢？你可能寫一個程式檢查圖片中有沒有綠綠的或是有沒有像葉子的形狀的部份等等，然後寫了幾百條規則來完成辨識樹的圖片的功能，現在功能上線了，好死不死現在來了一張樹的圖片上面剛好都沒有葉子，你寫的幾百條規則都沒用了，辨識樹的圖片的功能只能以失敗收場。機器學習可以解決這樣的問題，透過觀察資料的方式來讓電腦自己辨識樹的圖片，可能會比寫幾百條判斷規則更有效。這有點像是教電腦學會釣魚（透過觀察資料學習），而不是直接給電腦魚吃（直接寫規則給電腦）。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-4.png">
</p>

### 那麼什麼時候可以使用機器學習呢

從上個例子我們可以大概了解使用機器學習的使用時機，大致上如果觀察到現在你想要解決的問題有以下三個現象，應該就是機器學習上場的時刻了：

1. 存在某種潛在規則
2. 但沒有很辦法很簡單地用程式直接定義來作邏輯判斷（if else 就可以做到，就不用機器學習）
3. 這些潛在規則有很多資料可以作為觀察、學習的來源
    
<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-5.png">
</p>

### 舉個實際的機器學習例子 1

Netflix 現在出了一個問題，如果你能讓使用者對電影喜好程度星級預測準確率提升 10%，那就可以獲得 100 萬美金，馬上讓你從碼農無產階級晉升到天龍人資產階級，而這個問題是這樣的：他們給了你大量使用者對一些電影的星級評分資料，你必須要讓電腦學到一個技能，這個技能可以預測到使用者對他還沒看過的電影評分會是多少星級，如果電腦能準確預測的話，那某種程度它就有了可以知道使用者會不會喜歡這些電影的技能，進而可以推薦使用者他們會喜歡的電影，讓他們從口袋裡拿錢過來～

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-6.png">
</p>

### 舉個實際的機器學習例子 2

這邊偷偷告訴大家一個很常見的機器學習方法的模型，我們再來整理一下，其實這個問題可以轉化成這樣，使用者有很多個會喜歡這部電影的因素，比如電影中有沒有爆破場景、有沒有養眼畫面、有沒有外星人等等，這個我們就稱之為使用者的特徵值（feature），而電影本身也有很多因素，比如電影中有出現炸彈、是很有魅力的史嘉蕾·喬韓森所主演、片名是 ET 第二集等等，這個我們就稱之為電影的特徵值，我們把這兩個特徵值表示成向量（vector），如此如果使用者與電影特徵值有對應的特徵越多，那就代表使用者很有可能喜歡這部電影，而這可以很快地用向量內積的方式計算出來。也就是說，機器學習在這個問題上，只要能學習出這些會影響使用者喜好的**因素**也就是機器學習所說的**特徵值**會是什麼，那這樣當一部新的電影出來，我們只要叫電腦對一下這部新電影與使用者的特徵值的對應起來的向量內積值高不高就可以知道使用者會不會喜歡這部電影了～

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-7.png">
</p>

### 將剛剛的問題用數學式來描述

我們在用銀行核發信用卡的例子來描述機器學習，我們可以把信用卡申請者的資料想成是 x，而 y 是銀行是否核發信用卡。所以這就是一個函式，它有一個潛在規則，可以讓 x 對應到 y，機器學習就是要算出這個 f 函式是什麼。現在我們有大量的信用卡對申請者核發信用卡的資料，就是 D，我們可以從資料觀察中得到一些假設，然後讓電腦去學習這些假設是對的還是錯的，慢慢習得技能，最後電腦可能會算出一個 g 函式，雖然不是完全跟 f 一樣，但跟 f 很像，所以能夠做出還蠻精確的預測。
    
<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-8.png">
</p>

### 機器學習流程

所以機器學習銀行是否核發信用卡的流程就像這樣，我們想要找到 target function，可以完整預測銀行對申請者是否要核發信用卡才會賺錢，這時我們會餵給電腦大量的資料，然後透過學習演算法找出重要的特徵值，這些重要的特徵值就可以組成函式 g，雖然跟 f 不一樣，但很接近。

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-9.png">
</p>

### 機器學習的 Model

從上面的學習流程，我們可以知道最後電腦會學習出 g 可以辨認資料中較重要的特徵值，這些特徵值可能是我們一開始觀察資料所整理出來的假設，所以我們餵資料給電腦做學習演算法做計算時，也會餵一些假設進去，以銀行核發信用卡的例子就是這個申請者年薪是否有 80 萬、負債是否有 10 萬、工作是否小於兩年等等假設，這些假設就是 H，學習演算法再去計算實際資料與假設是否吻合，這個演算法就是 A，最後演算法會挑出最好的假設集合是哪些。 H 與 A 我們就稱為是機器學習 Model

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-10.png">
</p>

### 機器學習的基本定義

機器學習的基本定義可以用這個圖來概括，用一句話來說的話就是「use data to compute hypothesis g that approximates target f」，你如果問我為何要用英文寫下這句話，其實只是因為這樣看起來比較像是一個偉人大學者寫的啊！拿來唬人用的！

<p style="text-align:center">
	<img src="http://static.obeobe.com/image/blog-image/machine-learning-foundations-by-lin-xuan-tian-di-jiang-xue-xi-bi-ji-11.png">
</p>