+++
title = "如何使用 CSS3 Animation"
slug = "rru-he-shi-yong-css3-animation"
date = "2014-07-08T12:45:38.000Z"
url = "/2014/07/08/rru-he-shi-yong-css3-animation"
+++

### 前言

在這個浮誇的時代，如果網頁上沒有酷炫的功能或特效，似乎就遜掉了；如何讓網頁變得酷炫呢？其中一個方法就是使用 CSS3 Animation！只要使用了 CSS3 Animation 就可以讓網頁中的元素動起來，立馬讓你的網頁酷炫度超越世界上 80% 的網頁！

而我個人身為一個全端工程師，稍微研究一下 CSS3 Animation 也是合理的，而且只要會一點點就可以拿來唬唬人，何樂而不為？很可惜這個技能就是唬不了正妹，哎，誰叫正妹只喜歡魔術呢～

不過請特別注意 CSS3 的 Animation 與 Transition 並不相同喔！雖然都可以做到相似的效果，有時看起來也真的很像，但實際上 Animation 與 Transition 依操作的程度不同所以適合使用的地方也會有所不同，或許我之後會再寫一篇文章介紹 Transition。（吧？）

就讓我們一起來看看 CSS3 Animation 大法怎麼練吧！

### CSS3 Animation 第一級

假設我們要在一個 div 元素上加上動畫特效：

#### Step 1：定義要使用哪個關鍵影格(keyframe)來執行動畫

	div {
        width: 100px;
        height: 100px;
        background: red;
        position: relative;
    	-webkit-animation: animation-keyframe-name 5s; /* Chrome, Safari, Opera */
        -webkit-animation-iteration-count: infinite;
        animation: animation-keyframe-name 5s;
        animation-iteration-count: infinite;
    }
    
這段 CSS 語法就是代表 div 元素要用哪個關鍵影格來執行動畫，詳細的動畫動作都會寫在關鍵影格裡面，在這邊的意思就是要使用一個名稱叫 <code>animation-keyframe-name</code> 的關鍵影格來進行動畫，後面的 <code>5s</code> 就代表這個動畫執行的時間會是 5 秒鐘。而 <code>animation-iteration-count: infinite</code> 則代表這個關鍵影格動畫會不斷重複執行。

特別注意有 <code>-webkit-</code> 這個前綴的 CSS 語法是為了支援 webkit 核心的瀏覽器，例如：Chrome、Safari、Opera 等等。

所以這段語法翻譯成白話文就是：div 這個元素要使用一個叫做 <code>animation-keyframe-name</code> 的關鍵影格來進行動畫，動畫執行的時間長度為 5 秒鐘，且動畫會不斷重複執行。

keyframe 的名稱如果不想要叫 <code>animation-keyframe-name</code>，也可以改成其他的，比如：<code>fadein-keyframe</code>、<code>fadeout-keyframe</code> 等等。

#### Step 2：定義關鍵影格(keyframe)中動畫如何變化

	/* Chrome, Safari, Opera */
  	@-webkit-keyframes animation-keyframe-name {
    	from {background: red;}
        to {background: yellow;}
    }
    
    /* Standard syntax */
    @keyframes animation-keyframe-name {
    	from {background: red;}
        to {background: yellow;}
    }
    
這段 CSS 語法就定義了 <code>animation-keyframe-name</code> 這個關鍵影格的動畫變化，它會在 5 秒之內從原本背景色紅色（<code>from {background: red;}</code>）變為背景色黃色（<code>to {background: yellow;}</code>），就這樣我們就可以寫好 CSS3 動畫了，超簡單 der！

#### <a href="http://codepen.io/fukuball/pen/hzHAE" target="_blank">CSS3 Animation 第一級展示</a>

### CSS3 Animation 第二級

CSS3 Animation 第一級只有 from to 這兩種狀態可以指定動畫的變化，總感覺缺少了點什麼，如果好死不死動畫想要指定三種狀態變化怎麼辦？這時就要使用 CSS3 Animation 第二級了！在 CSS3 Animation 第二級我們可以使用動畫執行時間百分比來指定動畫變化的狀態。

    /* Chrome, Safari, Opera */
    @-webkit-keyframes animation-keyframe-name {
        0%   {background: red; left:0px; top:0px;}
        25%  {background: yellow; left:200px; top:0px;}
        50%  {background: blue; left:200px; top:200px;}
        75%  {background: green; left:0px; top:200px;}
        100% {background: red; left:0px; top:0px;}
    }

    /* Standard syntax */
    @keyframes animation-keyframe-name {
        0%   {background: red; left:0px; top:0px;}
        25%  {background: yellow; left:200px; top:0px;}
        50%  {background: blue; left:200px; top:200px;}
        75%  {background: green; left:0px; top:200px;}
        100% {background: red; left:0px; top:0px;}
    }
    
這段 CSS 語法將動畫的變化分成五個狀態，在動畫執行時間 0% 的時候是背景紅色的狀態（<code>0% {background: red;}</code>），在動畫執行時間 25% 的時候是背景黃色的狀態（<code>25% {background: yellow;}</code>），在動畫執行時間 50% 的時候是背景藍色的狀態（<code>50% {background: blue;}</code>），在動畫執行時間 75% 的時候是背景綠色的狀態（<code>75% {background: green;}</code>），在動畫執行時間 100% 的時候是背景變回紅色的狀態（<code>100% {background: red;}</code>），在我們這個例子裡動畫執行時間 100% 也就是動畫執行時間在第五秒的時候。如此我們就可以做更多細緻的動畫了。

#### <a href="http://codepen.io/fukuball/pen/lGwnx" target="_blank">CSS3 Animation 第二級展示</a>

### CSS3 Animation 第三級

在 CSS3 Animation 第三級我們可以使用更多屬性（property）來讓動畫有更多調整的空間，這些 animation 相關的 property 列表如下：

<table>
	<thead>
    	<tr>
          	<td>
              	CSS 屬性
          	</td>
          	<td>
              	說明
          	</td>
    	</tr>
    </thead>
    <tbody>
    	<tr>
        	<td>
              	animation-delay
          	</td>
          	<td>
              	設定元素在被載入之後到開始執行動畫之間的延遲時間
          	</td>
        </tr>
        <tr>
        	<td>
              	animation-direction
          	</td>
          	<td>
              	設定元素在動畫執行完之後，是否要以相反方向的方式播放，或是從頭開始以原來的方向重複播放。
          	</td>
        </tr>
        <tr>
        	<td>
              	animation-duration
          	</td>
          	<td>
              	設定整個動畫執行一次的時間長度
          	</td>
        </tr>
        <tr>
        	<td>
              	animation-iteration-count
          	</td>
          	<td>
              	設定動畫執行的次數，若要不斷重複執行，則可設為 infinite
          	</td>
        </tr>
        <tr>
        	<td>
              	animation-play-state
          	</td>
          	<td>
              	可用來暫停或繼續動畫播放
          	</td>
        </tr>
        <tr>
        	<td>
              	animation-fill-mode
          	</td>
          	<td>
              	設定元素在動畫執行前後如何套用 CSS 的樣式
          	</td>
        </tr>
        <tr>
        	<td>
              	animation-timing-function
          	</td>
          	<td>
              	設定動畫執行的時間函數
          	</td>
        </tr>
    </tbody>
</table>
<br>

我們將所有動畫相關的屬性都使用看看：

	div {
        width: 100px;
        height: 100px;
        background: red;
        position: relative;
    	/* Chrome, Safari, Opera */
        -webkit-animation-name: animation-keyframe-name;
        -webkit-animation-duration: 5s;
        -webkit-animation-timing-function: linear;
        -webkit-animation-delay: 2s;
        -webkit-animation-iteration-count: infinite;
        -webkit-animation-direction: alternate;
        -webkit-animation-play-state: running;
        /* Standard syntax */
        animation-name: animation-keyframe-name;
        animation-duration: 5s;
        animation-timing-function: linear;
        animation-delay: 2s;
        animation-iteration-count: infinite;
        animation-direction: alternate;
        animation-play-state: running;
    }
    
    
#### <a href="http://codepen.io/fukuball/pen/dGKfo" target="_blank">CSS3 Animation 第三級展示</a>

感覺越來越強了！

### CSS3 Animation 第四級

在 CSS3 Animation 第三級我們學會使用更多動畫相關屬性了，但 CSS 的語法卻變得很冗長，這時就要使出 CSS3 Animation 第四級，這樣就可以寫出更精簡的 CSS3 Animation 語法了！

上面例子的：
	
    animation-name: animation-keyframe-name;
    animation-duration: 5s;
    animation-timing-function: linear;
    animation-delay: 2s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
    animation-play-state: running;

可以改寫成：

	animation: animation-keyframe-name 5s linear 2s infinite alternate;
    
所以就會變成：

	div {
        -webkit-animation: animation-keyframe-name 5s linear 2s infinite alternate; /* Chrome, Safari, Opera */
        animation: animation-keyframe-name 5s linear 2s infinite alternate; /* Standard syntax */
    }
    
CSS3 Animation 大法大功告成！
    
#### <a href="http://codepen.io/fukuball/pen/ADFco" target="_blank">CSS3 Animation 第四級展示</a>

### 結語

我們已經練完了 CSS3 Animation 大法的前四級，其實只要學會這些技巧，大概就能做出不錯的特效，只是動畫如何安排才會吸引人就要看個人的 Sense 了，像我就沒有什麼 Sense～

或許可以去請教對動畫最有 Sense 的 <a href="http://ricetseng.com/" target="_blank">Rice Tseng</a> 公主！