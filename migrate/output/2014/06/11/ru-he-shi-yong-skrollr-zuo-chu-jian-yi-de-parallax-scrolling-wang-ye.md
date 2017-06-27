+++
title = "如何使用 skrollr 做出簡易的 Parallax Scrolling 網頁"
slug = "ru-he-shi-yong-skrollr-zuo-chu-jian-yi-de-parallax-scrolling-wang-ye"
date = "2014-06-11T13:19:43.000Z"
url = "/2014/06/11/ru-he-shi-yong-skrollr-zuo-chu-jian-yi-de-parallax-scrolling-wang-ye"
+++

前一陣子大家非常瘋 Parallax Scrolling 網頁，主要是利用人們瀏覽網頁時最習慣的動作「滾動」來做一些特效，讓使用者透過簡易的滾動就能瀏覽完整個網頁。

Parallax Scrolling 中文翻成視差滾動，wiki 上的定義上說明這是電腦圖學中一種特別的滑動特效技巧，原理是把背景圖片的移動速度放慢，讓前景圖片移動較快，因而在2D畫面上產生多層次的佈景深度。

但說了這麼多，不如還是透過實際的例子來感受一下什麼是 Parallax Scrolling，<a href="http://www.awwwards.com/20-best-websites-with-parallax-scrolling-of-2013.html" target="_blank" >20 Best Websites with Parallax Scrolling of 2013</a> 中就有許多有趣的例子！

如果仔細去研究這些例子的原始碼就會發現，要做這樣的網頁實在很費工，如果可以的話當然想找找有什麼方法可以快速的做好一個 Parallax Scrolling 網頁，於是就在 <a href="https://github.com/" target="_blank" >github</a> 上找到了 <a href="https://github.com/Prinzhorn/skrollr" target="_blank" >skrollr</a>。

skrollr 的使用方法真的非常簡單，步驟如下：

Step1：引入函式庫到網頁中：

    <script type="text/javascript" src="/path/to/skrollr.min.js">
    </script>
    
Step2：在網頁底端初始化 skrollr

	<script type="text/javascript">
    	var skrollr_obj = skrollr.init();
    </script>
    
Step3：利用以下語法來安排網頁中元素的轉場

	<div data-0="background-color:rgb(0,0,255);" data-500="background-color:rgb(255,0,0);">
    	WOOOT
    </div>
    
上面語法的意義就是使用者滾動位置從 0 滾動到 500 時 div 的 CSS 樣式變化，也就是說使用者滾動位置到 500 時，div 的背景色會從原來的藍色慢慢變為紅色。

如果要做淡出功能可以這樣寫：

	<div data-2100="opacity: 1;" data-2400="opacity: 0;">
    	<img src="/public/image/show-case/skrollr-demo/cell.png">
    </div>

如果要做漸漸模糊功能可以這樣寫：

	<div data-2100="-webkit-filter: blur(0px);" data-2400="-webkit-filter: blur(5px);">
    	<img src="/public/image/show-case/skrollr-demo/cell.png">
    </div>

以此類推，當然我們也可以寫 data-100 至 data-1000 的 CSS 樣式變化，因此我們可以很方便的安排網頁中元素的轉場，做出簡易的 Parallax Scrolling 網頁。

這麼簡易好用，應該所有剛接觸網頁設計的人都會用吧！所以我就現學現賣做了一個 <a href="http://www.fukuball.com/show-case/skrollr-demo" target="_blank" >天下第一武道大會</a> 網頁！小時候的回憶湧上心頭啊！

### 會踩雷的地方請特別注意

撰寫 CSS 轉場變化時要特別注意，每一個階段的 CSS 樣式一定要一致，舉個例子來說，當某個階段的 CSS 樣式有 <code>opacity: 0;</code> 及 <code>-webkit-filter: blur(0px);</code>，其他階段的 CSS 樣式也一定要有 <code>opacity: *;</code> 及 <code>-webkit-filter: blur(*px);</code>，否則會得到非預期的結果。

例如這樣是錯的寫法（在 data-2400 少寫了 opacity 的樣式）：

	<div data-2100="opacity: 1;-webkit-filter: blur(0px);" data-2400="-webkit-filter: blur(5px);">
    	<img src="/public/image/show-case/skrollr-demo/cell.png">
    </div>
    
這樣才是正確的寫法（data-2100 有寫到 opacity, -webkit-filter，data-2400 就要寫到 opacity, -webkit-filter）：

	<div data-2100="opacity: 1;-webkit-filter: blur(0px);" data-2400="opacity: 0;-webkit-filter: blur(5px);">
    	<img src="/public/image/show-case/skrollr-demo/cell.png">
    </div>



