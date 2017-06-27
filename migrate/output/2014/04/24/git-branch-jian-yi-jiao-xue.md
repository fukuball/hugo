+++
title = "Git Branch 簡易教學"
slug = "git-branch-jian-yi-jiao-xue"
date = "2014-04-24T14:27:16.000Z"
url = "/2014/04/24/git-branch-jian-yi-jiao-xue"
+++

### 前言

多人共同開發的專案，有時我們需要開發新功能，同時又要修 Bug，可能主程式也要不斷維護開發，我們需要同步進行以加速開發，這時我們通常會從主 branch（通常預設為 master）開出一個新的 branch 來開發，當完成所要開發的新功能或完成 bug 的修正時，就可以將這個 branch merge 回主 branch，因此使用 git branch 在軟體開發上是非常重要的技能。

### git branch

使用 git branch 可以列出所有的 branch 並告訴你目前正在哪個 branch：

	$ git branch
      dev
    * master
    
假設要再開一個 bug-fix 的 branch，就可以使用以下指令來開 branch：

	$ git branch bug-fix
    
若要刪除 branch 則使用 git branch -d 來刪除，-D 則為強制刪除

	$ git branch -d bug-fix
    
### git checkout

目前我們已有多個 branch，我們可以使用 git checkout 來切換 branch：

	$ git checkout dev
    
### git merge

當我們在 branch 完成工作之後，就要將更新的程式碼 merge 回主 branch，這時請先回到主 branch：
	
    $ git checkout master
    
然後再使用 git merge 來將要 merge 的 branch merge 進去主 branch，比如將 dev merge 進 master：

	$ git merge dev
    
### conflict 的處理

有時我們 merge 時會產生 conflict，其實如果兩個人同時在相同的 branch 修改相同一行程式碼也會產生 conflict，總之使用版本控制系統應該幾乎都會碰到 conflict，所以處理 conflict 也是相當重要的。

產生 conflict 的時候 <<<<<<<<<< HEAD 到 ========== 的區域是目前你所要 commit 內容，而從 =========== 到 >>>>>>>>>>> dev 則是你要合併的 dev branch 的內容，總之就是將這一段 conflict 修正成你要的結果，然後再將這個修正 commit 上去就可以了。

發生 confict 時的處理步驟大概就是這樣：

1. 找到 confict 的檔案，修改成你要的結果。
2. 使用 git add . 將處理好的檔案加入 stage。
3. git commit 提交合併訊息。

###結語

以上是一些 Git Branch 的簡易使用教學，但我平常用還是用 GUI 比較多，個人推薦 Github 出品的 GUI 工具，用 Github 的 Client Merge 超簡單的！工具只要簡單易用就好了，不太需要什麼複雜的功能啊。

Github GUI Client 下載：

* [GitHub for Windows](https://windows.github.com/)
* [GitHub for Mac](https://mac.github.com/)


 