+++
title = "如何使用 CSS3 Transition"
slug = "css3-transition"
date = "2015-07-06T06:47:25.000Z"
url = "/2015/07/06/css3-transition"
+++

### 前言

我們之前曾經介紹過 [如何使用 CSS3 Animation](http://blog.fukuball.com/rru-he-shi-yong-css3-animation/)，也不小心在該篇文章中說要另文跟大家介紹如何使用 CSS3 Transition，拖稿了近一年，今天終於要來實現諾言了～雖然大家可能根本就不在意，但哥就是真性情的人他媽的當真了啊！

在這個浮誇的時代，如果網頁上沒有酷炫的功能或特效，似乎就遜掉了（幹！開場跟如何使用 CSS3 Animation 這篇文章一模一樣，可以再混一點啊），好啦，不說廢話，總之就是網頁有使用到 CSS3 Transition 馬上就會讓你的網站帥十倍啦！很爽吧！（請注意：本人並不會因此帥十倍）

就讓我們一起來看看 CSS3 Transition 大法怎麼練吧！

### CSS3 Transition 第一級

第一級讓我們先由簡單的範例從做中學，現在讓我們想像一個情境，我們希望滑鼠 hover 至某個 div 元素時，讓這個 div 元素改變背景色，若沒有用轉場（Transition）效果，我們就會看到 div 元素硬生生的改變顏色，一點都不溫柔，這樣橫衝直撞會讓 TA 很不舒服，所以我們才會需要 CSS3 Transition 來讓 TA 舒服一點。

```css
div.example-no-transition {
	width: 580px;
    padding: 9px 15px;
    background-color: #FF5050;
    color: white;
    margin-bottom: 20px;
    margin-top: 20px;
    border-radius: 5px;
}
div.example-no-transition:hover {
	background-color: #6666FF;
}
```
這段 CSS 語法就是代表當滑鼠 hover 至 div.example-no-transition 元素時，背景顏色會變成 <code>#6666FF</code>，但就是很生硬的變過去，但當我們加入 transition 那就不一樣了。

```css
div.example-with-transition {
	width: 580px;
    padding: 9px 15px;
    background-color: #FF5050;
    color: white;
    border-radius: 5px;
    -webkit-transition: background-color 1s;
    -moz-transition: background-color 1s;
    -o-transition: background-color 1s;
    -ms-transition: background-color 1s;
    transition: background-color 1s;
}
div.example-with-transition:hover {
	background-color: #6666FF;
}
```

這段 CSS 語法 transition 的部分就是說 div 元素要如何轉場，<code>background-color 1s</code> 的意思就是說 background-color 會在 1 秒的時間變化成 hover 所指定的背景色。

就是這麼簡單！

特別注意有 <code>-webkit-</code> 這個前綴的 CSS 語法是為了支援 webkit 核心的瀏覽器，例如：Chrome、Safari、Opera 等等。

#### <a href="http://codepen.io/fukuball/pen/domeOo" target="_blank">CSS3 Transition 第一級展示</a>

### CSS3 Transition 第二級

CSS3 Transition 第一級使用的只是預設的轉場效果，總感覺缺少了點什麼，通常龜毛的人不會滿足於預設的效果，所以在 CSS3 Transition 第二級我們會學到如何調整 CSS3 Transition 的轉場效果。

```html
<div id="example-transition">
  <div class="ease">ease</div>
  <div class="linear">linear</div>
  <div class="easein">ease-in</div>
  <div class="easeout">ease-out</div>
  <div class="easeinout">ease-in-out</div>
</div>
```

```css
#example-transition {
  width: 520px;
}
#example-transition div {
  width: 100px;
  margin: 5px 0;
  padding: 5px;
  color: white;
  background-color: #FF5050;
  text-align: right;
  border-radius: 5px;
}
#example-transition:hover div {
  width: 500px;
}
#example-transition div.ease {
  -webkit-transition: 3s ease;
  -moz-transition: 3s ease;
  -o-transition: 3s ease;
  -ms-transition: 3s ease;
  transition: 3s ease;
}
#example-transition div.linear {
  -webkit-transition: 3s linear;
  -moz-transition: 3s linear;
  -o-transition: 3s linear;
  -ms-transition: 3s linear;
  transition: 3s linear;
}
#example-transition div.easein {
  -webkit-transition: 3s ease-in;
  -moz-transition: 3s ease-in;
  -o-transition: 3s ease-in;
  -ms-transition: 3s ease-in;
  transition: 3s ease-in;
}
#example-transition div.easeout {
  -webkit-transition: 3s ease-out;
  -moz-transition: 3s ease-out;
  -o-transition: 3s ease-out;
  -ms-transition: 3s ease-out;
  transition: 3s ease-out;
}
#example-transition div.easeinout {
  -webkit-transition: 3s ease-in-out;
  -moz-transition: 3s ease-in-out;
  -o-transition: 3s ease-in-out;
  -ms-transition: 3s ease-in-out;
  transition: 3s ease-in-out;
}
```

CSS3 Transition 讓我們可以使用 timing function 這個參數來調整轉場效果，我們在例子中將所以的 timing function <code>ease</code>、<code>linear</code>、<code>ease-in</code>、<code>ease-out</code>、<code>ease-in-out</code> 一字排開，讓大家可以看清楚各種 timing function 有何異同，至於要使用哪個 timing function 就要看各位施主的 sense 了～

其中請特別注意，我們在這個例子中並沒有在 transition 裡說明哪個 CSS property 要做轉場效果，所以會使用預設模式來做轉場效果，預設模式其實就是 all，也就是說所有可以做轉場效果的 property 都會一起做變化，很方便吧！

#### <a href="http://codepen.io/fukuball/pen/OVvdrq" target="_blank">CSS3 Transition 第二級展示</a>

### CSS3 Transition 第三級

CSS3 Transition 還有一個 delay 的參數可以調整，第三級裡面我們將介紹如何使用 CSS3 Transition 的 delay，這樣可以讓我們的轉場效果有更多的變化。

```html
<div id="example-transition">
  <div class="ease">ease</div>
  <div class="linear">linear</div>
  <div class="easein">ease-in</div>
  <div class="easeout">ease-out</div>
  <div class="easeinout">ease-in-out</div>
</div>
```

```css
#example-transition {
  width: 520px;
}
#example-transition div {
  width: 100px;
  margin: 5px 0;
  padding: 5px;
  color: white;
  background-color: #FF5050;
  text-align: right;
  border-radius: 5px;
}
#example-transition:hover div {
  width: 500px;
}
#example-transition div.ease {
  -webkit-transition: 1s ease;
  -moz-transition: 1s ease;
  -o-transition: 1s ease;
  -ms-transition: 1s ease;
  transition: 1s ease;
}
#example-transition div.linear {
  -webkit-transition: 1s linear 1s;
  -moz-transition: 1s linear 1s;
  -o-transition: 1s linear 1s;
  -ms-transition: 1s linear 1s;
  transition: 1s linear 1s;
}
#example-transition div.easein {
  -webkit-transition: 1s ease-in 2s;
  -moz-transition: 1s ease-in 2s;
  -o-transition: 1s ease-in 2s;
  -ms-transition: 1s ease-in 2s;
  transition: 1s ease-in 2s;
}
#example-transition div.easeout {
  -webkit-transition: 1s ease-out 3s;
  -moz-transition: 1s ease-out 3s;
  -o-transition: 1s ease-out 3s;
  -ms-transition: 1s ease-out 3s;
  transition: 1s ease-out 3s;
}
#example-transition div.easeinout {
  -webkit-transition: 1s ease-in-out 4s;
  -moz-transition: 1s ease-in-out 4s;
  -o-transition: 1s ease-in-out 4s;
  -ms-transition: 1s ease-in-out 4s;
  transition: 1s ease-in-out 4s;
}
```

其實我們就只是在 timing function 後面加了一個 delay 秒數而已，就可以做到一層一層的轉場變化效果，學會 CSS3 Transition 第三級之後我們就可以隱約看出 CSS3 Transition 的語法：

```css
transition: property duration timing-function delay;
```

第一個值是指定哪個 property 要變化，可以使用 all，第二個值 duration 是說轉場效果會多久完成，第三個值 timing-function 是說要使用什麼轉場效果有 <code>ease</code>、<code>linear</code>、<code>ease-in</code>、<code>ease-out</code>、<code>ease-in-out</code> 五種，第四個值 delay 是說明要延遲多久才開始轉場效果。 

#### <a href="http://codepen.io/fukuball/pen/aOYXgL" target="_blank">CSS3 Transition 第三級展示</a>

### CSS3 Transition 第四級

剛剛有說到 CSS3 Transition 可以指定 all property 進行轉場變化，其實並不是所有的 property 都可以進行轉場變化，可以進行轉場變化的 property 我們列成下表供大家參考。

<table class="table table-striped table-bordered">
    <tbody>
      <tr>
        <th>Property Name</th>
        <th>Type</th>
      </tr>
      <tr>
        <td><code>background-color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>background-image</code></td>
        <td>only gradients</td>
      </tr>
      <tr>
        <td><code>background-position</code></td>
        <td>percentage, length</td>
      </tr>
      <tr>
        <td><code>border-bottom-color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>border-bottom-width</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>border-color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>border-left-color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>border-left-width</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>border-right-color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>border-right-width</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>border-spacing</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>border-top-color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>border-top-width</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>border-width</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>bottom</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>crop</code></td>
        <td>rectangle</td>
      </tr>
      <tr>
        <td><code>font-size</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>font-weight</code></td>
        <td>number</td>
      </tr>
      <tr>
        <td><code>grid-*</code></td>
        <td>various</td>
      </tr>
      <tr>
        <td><code>height</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>left</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>letter-spacing</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>line-height</code></td>
        <td>number, length, percentage</td>
      </tr>
      <tr>
        <td><code>margin-bottom</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>margin-left</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>margin-right</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>margin-top</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>max-height</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>max-width</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>min-height</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>min-width</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>opacity</code></td>
        <td>number</td>
      </tr>
      <tr>
        <td><code>outline-color</code></td>
        <td>color</td>
      </tr>
      <tr>
        <td><code>outline-offset</code></td>
        <td>integer</td>
      </tr>
      <tr>
        <td><code>outline-width</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>padding-bottom</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>padding-left</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>padding-right</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>padding-top</code></td>
        <td>length</td>
      </tr>
      <tr>
        <td><code>right</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>text-indent</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>text-shadow</code></td>
        <td>shadow</td>
      </tr>
      <tr>
        <td><code>top</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>vertical-align</code></td>
        <td>keywords, length, percentage</td>
      </tr>
      <tr>
        <td><code>visibility</code></td>
        <td>visibility</td>
      </tr>
      <tr>
        <td><code>width</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>word-spacing</code></td>
        <td>length, percentage</td>
      </tr>
      <tr>
        <td><code>z-index</code></td>
        <td>integer</td>
      </tr>
      <tr>
        <td><code>zoom</code></td>
        <td>number</td>
      </tr>
    </tbody>
  </table>
  
比如我們現在希望 width 跟 backgournd-color 都可以進行轉場變化，就可以這樣寫：

```html
<div id="example-transition">
  <div class="ease">ease</div>
  <div class="linear">linear</div>
  <div class="easein">ease-in</div>
  <div class="easeout">ease-out</div>
  <div class="easeinout">ease-in-out</div>
</div>
```

```css
#example-transition {
  width: 520px;
}
#example-transition div {
  width: 100px;
  margin: 5px 0;
  padding: 5px;
  color: white;
  background-color: #FF5050;
  text-align: right;
  border-radius: 5px;
}
#example-transition:hover div {
  width: 500px;
  background-color: #000000;
}
#example-transition div.ease {
  -webkit-transition: 3s ease;
  -moz-transition: 3s ease;
  -o-transition: 3s ease;
  -ms-transition: 3s ease;
  transition: 3s ease;
}
#example-transition div.linear {
  -webkit-transition: 3s linear;
  -moz-transition: 3s linear;
  -o-transition: 3s linear;
  -ms-transition: 3s linear;
  transition: 3s linear;
}
#example-transition div.easein {
  -webkit-transition: 3s ease-in;
  -moz-transition: 3s ease-in;
  -o-transition: 3s ease-in;
  -ms-transition: 3s ease-in;
  transition: 3s ease-in;
}
#example-transition div.easeout {
  -webkit-transition: 3s ease-out;
  -moz-transition: 3s ease-out;
  -o-transition: 3s ease-out;
  -ms-transition: 3s ease-out;
  transition: 3s ease-out;
}
#example-transition div.easeinout {
  -webkit-transition: 3s ease-in-out;
  -moz-transition: 3s ease-in-out;
  -o-transition: 3s ease-in-out;
  -ms-transition: 3s ease-in-out;
  transition: 3s ease-in-out;
}
```

我們在 hover 時有兩個 property 不一樣，一個是 <code>width: 500px;</code>、一個是 <code>background-color: #000000;</code>，這兩個 property 都是屬於可以進行轉場效果的，因此這樣寫就會一起變化，很簡單吧！

#### <a href="http://codepen.io/fukuball/pen/vORPYQ" target="_blank">CSS3 Transition 第四級展示</a>

### 結語

我們已經練完了 CSS3 Transition 大法的前四級，其實只要學會這些技巧，大概就能做出不錯的特效，只是動畫如何安排才會吸引人就要看個人的 Sense 了，像我就沒有什麼 Sense～

或許可以去請教對動畫最有 Sense 的 <a href="http://ricetseng.com/" target="_blank">Rice Tseng</a> 公主！

結果跟 CSS3 Animation 那篇文章完全一模一樣！真的好混啊！哈哈哈！！！