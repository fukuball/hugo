+++
title = "如何做出網頁版 iTunes 11 的封面背景特效"
slug = "ru-he-shi-yong-html5-xiang-guan-ji-shu-zuo-chu-itunes-11-de-feng-mian-bei-jing-te-xiao"
date = "2014-06-25T10:21:33.000Z"
url = "/2014/06/25/ru-he-shi-yong-html5-xiang-guan-ji-shu-zuo-chu-itunes-11-de-feng-mian-bei-jing-te-xiao"
+++

### 前言

最近為了 training 新人，我在 iNDIEVOX 主持了每兩週會舉行一次的技術分享會，每位與會人員都需要準備一個分享講題，講題可以是任何開發技術相關的主題，甚至是相關產業新聞。

不過最近有些忙碌，加上世界杯熬夜的影響，我自己得準備的分享講題眼看就要開天窗了，只好拿出去年在 [HappyDesigner Mini 分享會 #3](http://happydesigner.kktix.cc/events/happydesigner-mini-3) 的講題來充充場面，剛好也可以逼自己整理成 blog！

那麼...... 究竟要如何做出網頁版 iTunes 11 的封面背景特效呢？在哪裡才能買得到呢？

<p style="text-align:center">
<img src="http://static.obeobe.com/image/subtitle-image/那麼在哪裡才能買得到呢？.jpg">
</p>

... ... 我們這邊會直接說明如何實作，所以是買不到的喔！

### 觀察分析

首先讓我們觀察分析一下 iTunes 11 的封面特效：

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11.png?1">
</p>

透過我們精準的觀察與分析之後，我們可以將 iTunes 11 的封面特效歸納成以下三點：

1. 專輯資訊字體顏色配色與專輯封面配色相似
2. 專輯資訊區塊背景色與專輯封面背景色相似
3. 專輯資訊區塊背景色形成一個模糊遮罩蓋在專輯封面上

也就是說我們只要做到以上三點，大概就可以做到類似 iTunes 11 的封面特效了！

### 實作

### Step 1：實作蓋在專輯封面上模糊遮罩

首先我們先不管顏色，看看是否能用 CSS 3 來實作蓋在專輯封面上模糊遮罩，研究一番之後發現並不難實作，CSS 3 的語法如下：

	.mask {
    	box-shadow: rgb(9, 8, 9) 14px 17px 25px inset,
                    rgb(9, 8, 9) -1px -1px 170px inset;
	}
    
我們使用 CSS 3 中的 <code>box-shadow</code> 這個 property 來實做陰影效果，將這個陰影蓋在封面上便可以形成一個模糊遮罩，其中 <code>rgb(9, 8, 8)</code> 表示陰影的顏色，<code>inset</code> 表示陰影是往區塊內部長，<code>14px 17px 25px</code> 分別表示陰影向水平方向長的長度、陰影向垂直方向長的長度、陰影模糊的長度，由於陰影是向區塊內長，分別就表示水平方向<strong>由左向內</strong>長 14px 的陰影、垂直方向<strong>由上向內</strong>長 17px、然後都長 25px 的模糊程度。

同理類推，底下的 <code>rgb(9, 8, 9) -1px -1px 170px inset</code> 就表示水平方向<strong>由右向內</strong>長 1px 的陰影、垂直方向<strong>由下向內</strong>長 1px、然後都長 170px 的模糊程度。

這個語法會形成像這樣的效果：

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11_2.png?1">
</p>

太棒了！小小的一段 CSS 3 語法居然帶給我們這麼大的成就感，聰明的我們把這個遮罩蓋在封面像就會形成這樣的效果：

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11_3.png?1">
</p>

如此我們就可以暫時使用黑色背景、白色字體、黑色遮罩來完成第一版的 iTunes 11 封面背景效果。

### <a href="http://www.fukuball.com/show-case/5tunes11-v1" target="_blank">第一版成品展示</a>

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11_4.png?1">
</p>

### Step 2：萃取出專輯封面主要顏色，讓背景色、字體顏色、模糊遮罩配色與專輯封面配色相似

實作完模糊遮罩之後，剛剛第一步我們先擱在一邊的顏色就是接下來的重點了，所謂「萃取出專輯封面主要顏色」究竟是怎麼一回事呢？感覺好像需要用到演算法？沒有錯！要取出專輯封面的<strong>主要顏色</strong>確實需要借助演算法這個高深的技巧！

我們可以以人類最直觀的想法來猜猜演算法應該會怎麼實作：首先每張圖片都是由若干像素組合而成，而每個像素都有一個顏色，我們可以用數數的方式找出最多相同顏色的像素取出成為一個代表色，若要找出多個代表色，那就可以用同的想法類推，讓顏色接近的像素聚集在一起，分成一堆一堆的，若要取十個顏色，就分成十堆，讓每一堆的像素數都相同，然後將這十個顏色堆的顏色取平均色，我們就可以萃取出圖片的十個代表色了！

類似想法的演算法其實已經有許多人想出來、也實作好程式了，其中一個最有名的演算法就叫做 [Color Quantization](http://en.wikipedia.org/wiki/Color_quantization)，它的核心精神就像我們上述的做法一樣把圖片的顏色像<strong>切豆腐</strong>一樣去分堆，去找出代表色，各種不同的演算法其實就只是在於<strong>切法</strong>的不同而已！

其實這樣的演算法最早是用來壓縮圖像使用的，我們希望儘量用較少的顏色來重畫原來的圖片，又不希望重畫的圖片與原來的圖片差太多，因此就要<strong>找出圖片的主要代表色來重畫原圖</strong>，這樣重畫的壓縮圖片就不會與原來的圖片差太多，又能達到壓縮效果！

詳細演算法可以寫成好幾篇部落格，因此我就不在這邊贅述，有興趣詳細了解的可以參考[這個網站](http://www.csie.ntnu.edu.tw/~u91029/Image.html)！

我們現在已經知道要取出圖片的主要代表色就要使用 Color Quantization 演算法，那接下來要自己實做演算法嗎？哈哈哈！當然不必啊！像這種有名的演算法一定有一大堆已經寫好的開源碼可以使用！

這邊我們使用 [Color Thief](https://github.com/lokesh/color-thief) 來取出圖片的主要代表色，首先引入函式庫到網頁中：

    <script type="text/javascript" src="/path/to/color-thief.min.js">
    </script>
    
然後用以下語法來得到圖片的主要代表色：

	myImage = $('#myImage');
    var colorThief = new ColorThief();
	colorThief.getPalette(myImage, 8);
    
其中的 <code>8</code> 就是表示要取出圖片八個主要代表色，同理你要取出十個主要代表色，就改成 <code>colorThief.getPalette(myImage, 10)</code> 就可以了！很簡單吧！！

如此我們就可以使用 Color Thief 取出的第一個主要顏色來畫背景及遮罩、第二個主要顏色畫字體完成第二版的 iTunes 11 封面背景效果，這樣的效果就已經很不錯了！

### <a href="http://www.fukuball.com/show-case/5tunes11-v2" target="_blank">第二版成品展示</a>

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11_5.png?2">
</p>

### Step 3：調整、調整、再調整

從第二版的 iTunes 11 封面背景效果展示中，其實我們已經得到了不錯的效果，但我們會發現有些地方會怪怪的，比如：

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11_6.png?2">
</p>

這個封面中，Color Thief 取出的第一個代表色是灰色，所以造成了我們不想要的結果，但其實又不能說是 Color Thief 或是 Color Quantization 演算法的錯，因為這張封面確實有蠻多像素是屬於灰色系列的。

我們認為較好的結果就是讓專輯資訊區塊的背景色及遮罩能和封面的背景色是類似的，在這個例子裡我們希望得到的是<strong>米分糸工色</strong>的！我們開怎麼辦呢？

我們可以做的就是去調整演算法，讓 Color Thief 取出代表色時只算封面中屬於背景部份的像素！感覺很直觀嘛！

問題在於...

### 請翻譯翻譯他媽的要怎麼告訴程式只算封面背景部份的像素啊啊啊啊！！！！

<p style="text-align:center">
<img src="http://static.obeobe.com/image/subtitle-image/我就想讓你翻譯翻譯，什麼叫驚喜.jpg">
</p>

其實找出圖片中屬於背景的部份這個問題我們並不是第一個遇到的，這個問題也已經探討很久了，目前也有許多方法被研發出來，有很多方法甚至牽涉到[機器學習](http://en.wikipedia.org/wiki/Machine_learning)領域的研究，我們這邊當然也可以用這些方法來解，但我就不引用這些方法了，我們可以利用一個更直觀的方法來完成！

我們可以再觀察一下 iTunes 11 的封面特效，我們可以發現背景色的遮罩效果會與封面的上半部及左半部溶在一起，那我們可不可以動一些手腳來讓 Color Thief 只計算封面上半部及左半部的像素呢？當然可以啊！

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11_7.png?2">
</p>

所以我們就以這樣的想法對 Color Thief 做了一點 Hack，修改的語法大致如下：

	for (var i = 0; i<image_data.length; i=i+4) {
		r = image_data[i + 0];
     	g = image_data[i + 1];
     	b = image_data[i + 2];
     	a = image_data[i + 3];

     	if ( i<(image_data.length*0.30) || (i%(image.width*4))<(image.width*0.30) ) {
        	bg_image_data_array.push([r, g, b]);
     	}

  	}

  	var bg_cmap = MMCQ.quantize(bg_image_data_array, 5);
  	var bg_palette = bg_cmap.palette();
    
其中 <code>i<(image_data.length*0.30)</code> 就代表圖片中上面 30% 部分的像素資料，<code>(i%(image.width*4))<(image.width*0.30)</code> 就代表圖片中左邊 30% 部分的像素資料，這樣就可以讓 Color Thief 只計算封面上半部及左半部的像素了！

像這樣的方法在學術上就稱為 Heuristic Algorithm，以最直觀的方式來設計演算法，雖然可能不會得到最佳解，但常常能得到一些不錯的效果！

如此我們就可以使用 Hack 調整過後的 Color Thief 取出的第一個主要顏色來畫背景及遮罩、第二個主要顏色畫字體來完成完全體的 iTunes 11 封面背景效果，感覺一切都對了啊！！！

### <a href="http://www.fukuball.com/show-case/5tunes11" target="_blank">完全體成品展示</a>

<p style="text-align:center">
<img src="http://static.obeobe.com/image/blog-image/itunes11_8.png?2">
</p>

### 結語

關於這個主題，我有製作 HappyDesigner Mini 分享會 #3 時使用的投影片，[投影片連結在此](http://www.fukuball.com/slide-show/5tunes11)，有興趣的人可以參考看看。

我們這邊完整說明了如何做出網頁版 iTunes 11 的封面背景特效，使用了許多第三方的函式庫來幫助實作，也可以在這樣的練習中學習如何一步一步的完成我們最終想完成的目標。

其中也發現了許多可以精進的地方，例如取得主要顏色的演算法、機器學習自動偵測圖片背景部份這樣的問題，若要取得更好的結果，就是要更深入去研究相關演算法來得到更令人滿意的結果，而演算法這個領域其實如同偉大航道的新世界一樣充滿驚奇啊！未來有機會更深入研究的話希望也能跟大家分享～
