+++
title = "我的 Sublime Text 2 設定"
slug = "wo-de-sublime-text-2-she-ding"
date = "2014-04-24T10:03:53.000Z"
url = "/2014/04/24/wo-de-sublime-text-2-she-ding"
+++

使用文字編輯器撰寫程式碼的時候，第一步就是要挑整適合於自己使用的編輯環境，在 Sublime Text 2 裡只要使用快捷鍵 <code>⌘,</code> 就可以開啟設定頁面，然後就可以依照個人使用情況來做調整啦～

以下是我目前的 Sublime Text 2 設定值，大家可以參考看看

	{
		"font_size": 18.0,
		"ignored_packages":
		[
			"Vintage"
		],
		"tab_size": 4,
		"translate_tabs_to_spaces": true,
    	"highlight_line": true,
    	"trim_trailing_white_space_on_save": true
	}
    
我將 font_size 設成 18，這樣對眼睛比較好，畢竟要長時間看程式碼，還是大一點的字型比較好。

另外，Sublime Text 可以透過 Vintage 這個內建的 package 提供 vi 模擬模式，讓使用者可以使用 vi 的指令模式來操作 Sublime Text，由於我個人不熟悉 vi，所以就在 ignored_packages 將這個 packeage ignore 掉，其實 Sublime Text 一開始預設就是 ignore 這個 package 的，畢竟都已經使用 Sublime Text 了，要使用 vi 就使用真正的 vi 吧。

tab_size 我是設成 4，其實之前我都是使用 3，但實在太多 open source 的 project 都是使用 4，只好改變我的習慣。

translate_tabs_to_spaces 設成 true 可以將 tab 都轉成空白，這樣使用別人的 code 比較不會造成排版亂掉（如果大家的 tab_size 不同的話）。

highlight_line 設成 true 可以讓游標所在的行高亮顯示，一樣是為了自己的眼睛好，當然要設成 true。

trim_trailing_white_space_on_save 設成 ture，可以在儲存檔案時自動將多餘的空白去除掉，有時行末多餘的空白可能會造成一些奇怪的問題，就讓 Sublime Text 來幫我們把關吧～