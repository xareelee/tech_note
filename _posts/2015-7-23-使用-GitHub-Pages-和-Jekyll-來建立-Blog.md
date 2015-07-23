---
title: 使用 GitHub Pages 和 Jekyll 來建立 Blog
---

因為一直習慣使用 [markdown] 來寫筆記，寫久了之後發現資料還是需要放在雲端上，已防止哪天電腦上的資料遺失了，至少還有個異地備份。而後來希望這些 markdown 文件若能輕鬆成為 blog 文章，所以才會有這個 blog，和這篇文章。

我曾經有自己申請一個 domain 以及主機，來自己 host 一個 blog (試過 [wordpress] 和 [octopress])，不過後來懶得經營，加上主機一年後到期。這次我則決定使用 [GitHub Pages] 和 [Jekyll] 來建立的，並使用 [Emerald] 主題來改的。因為它滿足了我的需求：

1. **要可以使用 [markdown] 來撰寫 blog：**
    * Markdown 可以用簡單的文字，表達出文章的架構。
    * 撰寫 Markdown 文件已經算是 21 世紀的基本能力。
    * 可以套用不同 theme (.css) 讓文章排版變得好看。
    * 需要一個能夠把現有的 markdown 文件，輕鬆直接轉成 blog 文章的方法。
2. **要可以使用 [git] 做管理和發佈：**
    * 分散式管理讓我可以在電腦上完成文章之後，再同步到 host 主機上。
    * 可以使用 git 做文章的 branch，需要發佈時，再 merge 回發佈的支線上。
    * 可以使用 git 查看文章的歷史修改記錄。即使刪除了文章，還是能夠找回。
    * 萬一哪天 host 服務終止了，電腦上依舊保有這些文章以及 blog 系統，可以快速佈署到新的主機上。
3. **能夠 host 在 [GitHub] 上：**
    * 需要一個免費 git hosting。
    * 有好用的 web 介面可以操作和設定。
    * 支援 blogger 系統，不需要自己管理主機、申請 URL domain ([GitHub Pages])。
    * 自己也習慣使用 GitHub 做異地的版本控制，也不想再到處創帳號。
4. **能夠自訂頁面、擴充功能的 blogger 系統：**
    * 這個時代講求個性化，頁面上所有元件的安排都要能夠依照自己的喜好，可以自行修改。傳統的 blogger 平台服務無法滿足需求。
    * 有別人已經寫好的 theme，就不用自己重頭開始排版、加功能。
    * 要能容易擴充，有別人已經寫好的功能可以直接套用。
    * 社團活躍度高，文件充足，有問題都 google 的到，或是有人可以回答。
    * 選用 [Jekyll] 的原因是 GitHub Pages 推薦使用的 blogger 平台。




## 建立自己的 GitHub Pages

在 [GitHub Pages](https://pages.github.com) 上，有步驟教學




### GitHub Pages 提供兩種類型

GitHub Pages 提供[兩種類型](https://help.github.com/articles/user-organization-and-project-pages/)：

* User/Organization Pages：
* Project Pages


[markdown]: http://markdown.tw
[GitHub Pages]: https://pages.github.com
[GitHub]: https://github.com
[Jekyll]: http://jekyllrb.com
[Emerald]: https://github.com/KingFelix/emerald
[git]: https://git-scm.com
[wordpress]: https://wordpress.org
[octopress]: http://octopress.org
