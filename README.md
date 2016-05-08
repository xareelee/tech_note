# Development Notes

本庫用來發表部落格，請參考這個[連結 (http://xareelee.github.io/tech_note)](http://xareelee.github.io/tech_note)。

該頁面使用 [Jekyll](http://jekyllrb.com) 驅動，並使用 [Hyde](https://github.com/poole/hyde) 主題。

## 發佈新文章

使用 markdown 寫一篇文章，即可藉由 Jekyll 產生靜態 .html：

1. 檔名必須使用 `:year-:month-:day-:title.md`，並放在 `_posts` 資料夾下
2. 內文開頭應該包含以下標頭：

```html
---
layout      : post <!--使用 post.html 排版-->
title       : 使用 GitHub Pages 和 Jekyll 來建立 Blog
subtitle    : 快速建立 Blog 的方法 <!--不一定要有，顯示在主頁面-->
tags        : [GitHub Pages, Jekyll]
---
```