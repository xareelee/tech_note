---
title: 使用 GitHub Pages 和 Jekyll 來建立 Blog
layout: post
category : Blog
tags : [GitHub Pages, Jekyll]
---


因為一直習慣使用 [markdown] 來寫筆記，寫久了之後發現資料還是需要放在雲端上，已防止哪天電腦上的資料遺失了，至少還有個異地備份。而後來希望能將一些 markdown 的筆記轉為自己 blog 文章，所以才會有這個 blog 和這篇文章。

我曾經有自己申請一個 domain 以及主機，來自己 host 一個 blog (試過 [wordpress] 和 [octopress])，不過後來懶得經營，加上主機一年後到期。這次我則決定使用 [GitHub Pages] 和 [Jekyll] 來建立 blog。

* 為何我選擇 GitHub Pages + Jekyll
* 不必寫程式碼，也可以架好免費的 blog
* 正統的建立方式
* 熟悉 markdown、HTML、git、GitHub、Jekyll
* 開始寫 Blog


## 為何我選擇 GitHub Pages + Jekyll

簡單的說，因為它滿足了我懶惰的需求：

1. **要可以使用 [markdown] 來撰寫 blog：**
    * Markdown 可以用簡單的文字，表達出文章的架構。
    * 讓文章內容、結構與文章呈現的相依性分離，可以專注在寫作上。
    * 可以套用不同 theme (.css) 讓文章排版變得好看。
    * 撰寫 Markdown 文件已經算是 21 世紀的基本能力。
2. **要可以使用 [git] 做管理和發佈：**
    * 分散式管理讓我可以在電腦上完成文章之後，再同步到 host 主機上。
    * 可以使用 git 做文章的 branch，需要發佈時，再 merge 回發佈的支線上。
    * 可以使用 git 查看文章的歷史修改記錄。即使刪除了文章，還是能夠找回。
    * 萬一哪天 host 服務終止了，電腦上依舊保有這些文章以及 blog 系統，可以快速佈署到新的主機上。
3. **能夠 host 在 [GitHub] 上 ([GitHub Pages]))：**
    * 一個免費 git hosting。
    * 有好用的 web 介面可以操作和設定。
    * 支援 blogger 系統，不需要自己管理主機、申請 URL domain。
    * 已習慣使用 GitHub 做異地的版本控制，不想再到處創帳號。
4. **能夠自訂頁面、擴充功能的 blogger 系統：**
    * 這個時代講求個性化，頁面上所有元件的安排都要能夠依照自己的喜好，可以自行修改。傳統的 blogger 平台服務無法滿足需求。
    * 有別人已經寫好的 theme，就不用自己重頭開始排版、加功能。
    * 要能容易擴充，有別人已經寫好的功能可以直接套用。
    * 社團活躍度高，文件充足，有問題都 google 的到，或是有人可以回答。
    * 選用 [Jekyll] 的原因是 GitHub Pages 推薦使用的 blogger 平台。


## 不必寫程式碼，也可以架好免費的 blog

如果你沒寫過程式、或是新手，完全不想碰程式碼、不在電腦上安裝東西、不想碰 git 版本控制、不想接觸 command line 指令，只想單純靠瀏覽器，就架好 GitHub Pages + Jykyll 的 blog，事實上也是有辦法的 (不過你還是得學 [markdown] 來寫文章)。

雖然本篇文章的目標不是教學簡易架設的方法，不過這邊可以稍微簡述如何進行。如果你是 programmer，我會建議跳到下一節的正統方法進行佈建。


### (1) 先申請 GitHub 的個人帳號

先到 [GitHub] 申請一個個人帳號，選擇免費方案就好，不過你的 source code repository 都會是公開的，但是對於建立 blog 來說，資訊本來就是公開的，所以沒關係。

### (2) 找到一個你喜歡的佈景主題樣式，找到 source code，然後複製他到你的 GitHub 帳號

這部份聽起來很難，其實很簡單。

先找到一個也是用 GitHub Pages + Jykyll 架設 blog 的 open source code，直接在 GitHub 上面點選 fork，來複製一份到自己的帳號下。Fork 完之後，GitHub 應該馬上就會幫忙產出你的 blog (URL 也會自動建立)。

你可以 google 查找 `Jykell themes`，或是以下的網站，來找到你想要的 theme 及 source code：

* https://mademistakes.com/work/jekyll-themes/
* https://github.com/jekyll/jekyll/wiki/Themes
* http://jekyllthemes.org
* http://www.zhanxin.info/themes.html (中文)

如果你完全沒有頭緒的話，

1. 可以先嘗試使用[這個網頁](https://mmistakes.github.io/skinny-bones-jekyll/)的主題樣式當做開始 (我有測試過，使用上沒問題)。
2. 在它的 [GitHub source code](https://github.com/mmistakes/skinny-bones-jekyll) (或是其他主題的 GitHub 頁)，點選右上角的 fork，複製一份到自己的帳號。
3. 基本上，這樣就完成了。GitHub 會開始幫你產生 HTML 的頁面 (請見下節)。


### (3) 參訪 GitHub 自動幫你產生的 blog 頁面

在你 fork 出來的專案，可以在右邊的工具列找到 **Settings (設定)**。設定頁內有個 **GitHub Pages** 的區域，會告訴你 blog 會被發佈到的 URL。基本上格式就是 `http://{username}.github.io/{project_name}`。

另外，通常剛 fork 完，你的 blog 網站還不會被建立好，建議可以等個 30-60 分鐘再回來 (通常只有第一次會比較久)。發佈完成的話，在 Settings 內 GitHub Pages 的發佈狀態會顯示綠色並打勾。

你可以在 Settings 頁修改 project name (Repository name)。另外也建議把 Default branch 直接設定為 `gh-pages`，因為 GitHub 是根據 `gh-pages` 這個分支的內容來產生 project page 的網頁，若是修改到其他分支的檔案，GitHub 是不會更新網頁的。

GitHub Pages 除了支援 project pages 外，還有支援 [user/organization page](https://help.github.com/articles/user-organization-and-project-pages/)，主要差別在於 URL 路徑。不過一般來說，使用 project pages 彈性較高，也足夠符合需求；而且，你還可以創造多個 project，來切分不同的目的的 blog 網站 (URL domain 一樣，只差在路徑)。

> 只要 project name 不取為是 `{username/organization}.github.io`，產生的就是 project page；GitHub 就會查找這個 project 的 `gh-pages` 分支，並嘗試建立起 HTML 頁面。


### (4) 修改原本的設定，刪除原本的文章

大多數正常的情況下，你 blog 頁面應該跟原本的長一樣；若不一樣，就要看網頁原始碼來找出原因，通常是相依性和網站設定沒有修改。

通常有以下項目可以修改：

* 網頁的設定是在 `_config.yml` 檔案內，通常會有一些資訊需要修改 (`url`、`title`、`description`、`username`、`email`)。
* markdown 文章 (.md) 都是存在 `_posts` 資料夾下，你可以直接把裡面的檔案都清空。
* 如果你想改網頁的元件內容，那就看你對 HTML、Ruby、Jekyll 等熟不熟悉了。 


### (5) 開始撰寫你的 Blog

新的文章只要放在 `_posts` 資料夾下，GitHub 就會自動開始幫你更新網頁內容。不過要注意以下幾點：

* markdown 的檔案命名必須為 `YYYY-MM-DD-{article_title}.md`。
* 通常支援並非是純 markdown，而是採用 kramdown，因此部分正統 markdown 的標記方式可能不適用。
* markdown 內容的開頭應該類似下方，標示一些文章屬性 (大多數為非必要)：

<pre lang="markdown">
---
layout: article
title: "Sample Post Style Guide"
categories: articles
modified: 2014-08-27T11:57:41-04:00
tags: [sample]
comments: true
ads: true
---

// 以下開始撰寫你的文章
</pre>


## 正統的建立方式

在 [GitHub Pages](https://pages.github.com) 上，有步驟教學。如果資訊不足的話，google `GitHub Pages + Jekyll` 也有很多建立 blog 的教學文。所以這裡就不再說明。

用正統方法建立起的 GitHub Pages + Jekyll 的差別在於：

* 有本機端的一份程式碼，所以你可以在離線的狀態下，使用 Mac 上好用的 markdown/HTML 編輯器。
* 可以方便 git 操作，包括開分支撰寫文章，文章完成後再 merge。
* 可以在送到 GitHub 之前，在本機端先跑 Jekyll 看結果，邊看邊修。完成後再 push 到 GitHub 上。



## 所需 markdown、HTML、git、GitHub、Jekyll 的能力

整個 blog 需要接觸到 markdown、HTML、git、GitHub、Jekyll。如果有不熟的也沒關係，很多東西都只需要入門的能力，甚至可以跳過。

### Markdown 技能：
* 初期學習門檻低、中期學習曲線平、後期精通容易。人人都可以上手。
* 越熟練越好，這是文字工作者必備的技能。
* 建議搭配[所見即所得](https://zh.wikipedia.org/zh-tw/所見即所得)的編輯軟體，在 Mac 上我使用 [MacDown] 這個由台灣開發者的優秀軟體。

### HTML/CSS/Javascript 技能：
* 初期學習門檻低、中期學習曲線略陡、後期精通需要花一些時間。
* 基本的難度不高，學多少就可以用多少，所以可以從入門開始就能夠改得動一些東西。
* 雖然不是一定要懂，但能懂一點點比較好，這樣客製化比較容易。
* 基本上專案內的檔案，大多為 HTML、CSS (SCSS)、js。
* 在 Mac 上的編輯器，我推薦使用 [Sublime Text](https://www.sublimetext.com) (Sublime Text 2 是免費的) 或是 [Atom](https://atom.io)。

### git 技能：
* 簡單的說，就是指令列的 [TimeMachine](https://support.apple.com/zh-tw/HT201250)。但 git 功能遠超過單純的歷史備份。
* 初期學習門檻高、中期學習曲線還算平、後期精通需要花一些時間。
* 通常只要學會提交備份 (add/commit)、遠端同步 (push/pull)、分支概念 (branch) 就夠了。
* 許多圖型介面軟體可以避免 command line。在 Mac 上我推薦使用 [SourceTree]。

### GitHub：
* GitHub 是一個 web service，只要學會它的網頁操作即可。
* 基本上簡單易用，學習成本很低。

### Jekyll：
* 基本上不必直接接觸 Jekyll 的程式碼，只要直接使用就好，官方文件算是充足。
* 如果你已經有程式開發的概念，那麼在 HTML 內使用程式碼插入內容，是件簡單的事。


# 架好了，就開始寫 Blog 吧！




[markdown]: http://markdown.tw
[GitHub Pages]: https://pages.github.com
[GitHub]: https://github.com
[Jekyll]: http://jekyllrb.com
[Emerald]: https://github.com/KingFelix/emerald
[git]: https://git-scm.com
[wordpress]: https://wordpress.org
[octopress]: http://octopress.org
[MacDown]: http://macdown.uranusjr.com
[SourceTree]: https://www.sourcetreeapp.com