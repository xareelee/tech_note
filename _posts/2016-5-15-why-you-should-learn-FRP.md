---
layout      : post
title       : 為何你應該要學 FRP
tags        : [FRP, Swift, Haskell]
---


[Function reactive programming (FRP)](https://en.wikipedia.org/wiki/Functional_reactive_programming) 算是近年最火紅的話題之一，幾乎所有開發平台，都開始引入 FRP 了。而 FRP 帶來最大的好處，就是**提昇生產力**！

自己寫了 FRP 兩年多 (iOS/ReactiveCocoa)，從一開始自學、摸索，不斷地遇到撞牆期，然後不斷地突破、成長後，現在寫 FRP 應該算是駕輕就熟了。

一個人學習 FRP 是不容易的，尤其是缺少有經驗的人帶領、沒有進階教學資源；而要求一個團隊都用 FRP 開發，更算是難上加難。但是它帶來的好處，遠比撞牆期的痛苦還要來得大。也因此當已經習慣 FRP 開發之後，基本上就[回不去](https://www.google.co.jp/search?biw=1440&bih=801&tbm=isch&sa=1&q=%E5%8F%AF%E6%98%AF%E7%91%9E%E5%87%A1+%E5%9B%9E%E4%B8%8D%E5%8E%BB%E4%BA%86&oq=%E5%8F%AF%E6%98%AF%E7%91%9E%E5%87%A1+%E5%9B%9E%E4%B8%8D%E5%8E%BB%E4%BA%86)了。

所以我希望能夠推動大家改用 FRP 開發，這樣將來在共同開發、維護上，可以大幅降低成本，工作也會比較開心。


# 目錄

* [OOP 已死，FRP 萬歲](#OOP-is-dead-long-live-FRP)
* [OOP 遇到的問題：Mutable State × Time = Complexity](#OOP-issues)
* [為何要學習 FRP](#why-learn-FRP)
* [用 FRP 解決問題](#FRP-comes-to-the-rescue)
* [FRP 簡單的例子](#FRP-example)
* [FRP 的世界就像是生物學的 Signal transduction](#signal-transduction)
* [學習成本與開發效率](#learning-curve-and-cost)
* [總結](#conclusion)


<a name="OOP-is-dead-long-live-FRP"/>

## [OOP 已死，FRP 萬歲](#OOP-is-dead-long-live-FRP)


OOP (object-oriented programming) 已經算是近 20 多年的主流編程範型 (programming paradigm)。然而，最近 FRP 火紅的程度，已經慢慢開始出現了典範轉移 (paradigm shift)。[「OOP is dead」](https://www.google.com/search?q=OOP+is+dead)這個話題的討論在最近已經開始慢慢增加。

從 Rx.NET 開始，ReactiveX 已經慢慢開始將 RP 擴展到[各個語言、開發平台](http://reactivex.io/languages.html)。即便是 Apple 最新的 Swift 語言，也充滿了大量 Haskell 的語言特性。可以說整個世界幾乎都在往 FP/RP 方向靠攏。

> 註：而另一個在移動開發 (mobile development) 可能會發生典範轉移的是 React Native。看來 JavaScript 快要統一世界了！


<a name="OOP-issues"/>

## [OOP 遇到的問題：Mutable State × Time = Complexity](#OOP-issues)

### OOP 的發展：著重需求改變的複雜度

OOP 的四大特性的目的是:

* 利用**封裝**，提高**內聚力**：*將高度相關的 data structure 和 function 之間的封裝成物件的 property 和 method。*
* 利用**繼承**、**多型**、**抽象**，來降低**耦合度**：*當需求改變時，減少需要**更改代碼的範圍**。*

至今 OOP 的發展，都著重在分析並解決**「需求變化時，帶來代碼變化的複雜度」**。這些發展包括[設計模式](https://en.wikipedia.org/wiki/Software_design_pattern)，或是引入 [closure](https://en.wikipedia.org/wiki/Closure_(computer_programming))、[AOP (aspect-oriented programming)](https://en.wikipedia.org/wiki/Aspect-oriented_programming) 等，來設法封裝變化、降低代碼耦合度，進而可以減少維護時擴展功能的麻煩。

此外 OOP 在實踐上，往往在**「開發維護直覺」**、**「擴展彈性」**、**「良好代碼封裝」**之間，無法兼顧。<u>依靠直覺</u>寫出的 OOP 代碼，往往容易造成高耦合度，使得維護、變更需求變得更困難，且容易出錯。而<u>為了降低耦合度、提高修改彈性</u>，往往會封裝代碼到不同的類別，反而會降低開發、維護的直覺，並且需要額外的準備功夫 (重構、模組化、寫文件、理解等)，雖然會降低後續維護成本 (技術債)，但交出第一版代碼的時間會較久。


### OOP 的問題：無法有效解決執行期狀態的複雜度

但 OOP 並不是著重在解決**「執行期狀態變化、資料同步的複雜度」**。這意味著一件事：「當執行期的複雜度提高 (邏輯、多線程、非同步等)，OOP 的開發維護成本很容易會以**等比級數**上升；尤其是當沒有良好的開發習慣、累積技術債的時候。」

追根究柢，OOP 存在著一個根本性的問題：*無法有效解決 mutable state 隨著時間的變化，所帶來的複雜度*

1. **資料–時間依賴**：
    * 大多數的程式是會有非常多的**執行狀態**，會隨著時間改變。
    * 一旦**資料依賴於時間**，問題就會變得十分複雜。無法回溯某個時間點的狀態，就較難解決問題。
    * 尤其在非同步 (async) 處理時，有多種來源會影響同一組資料，一旦沒處理好，會是一場災難。
2. **複雜的狀態同步**：
    * 當狀態改變牽扯到複雜的資料同步時，需要寫大量的同步資料的代碼，是非常大的問題。
    * 尤其當改變一個狀態時，影響範圍**廣** (會觸發多個的事件和資料同步)，範圍又**深** (會更進一步觸發另一連串的事件和資料同步)，代碼量和複雜度就會提昇很多。尤其下游的處理又交互影響。
    * 雖然各開發平台可能有 [data binding](https://en.wikipedia.org/wiki/Data_binding) 的解決方案，但還是不比 FRP 來的強大、簡潔。
3. **狀態依賴和副作用**：
    * 由於程式語言和編程範型的許可，使得大部分的開發者容易將**純函式 (pure function)** 的部份與**「狀態依賴」**和**[「副作用 (side effect)」](https://en.wikipedia.org/wiki/Side_effect_(computer_science))**封裝在一起，成為 impure function。
    * 這些**隱性**的狀態依賴，導致在不同時間的相同輸入，會有不同的結果。
    * 而將副作用與函式混雜在一起，也會增加除錯難度 (尤其是**隱性**地改變另一組資料時)。


<a name="why-learn-FRP"/>

## [為何要學習 FRP](#why-learn-FRP)

學習 FRP 並不是為了趕上流行，而是要解決目前 OOP 開發時遇到的問題。因為 FRP：

* 同時兼顧開發直覺、良好封裝、擴展彈性
* 降低代碼的複雜度
* 解決複雜的資料對時間的依賴
* 解決複雜的資料處理、同步
* 對依賴和副作用重新封裝



<a name="FRP-comes-to-the-rescue"/>

## [用 FRP 解決問題](#FRP-comes-to-the-rescue)

FRP 著重的是「封裝**執行期**資料的處理和變化」，也就是**邏輯組裝**和**資料同步**。

我們可以理解一件事：「所有程式執行狀態的變化，都是來自於一個事件 (event) 的發生。」

若先不考慮其他的副作用，我們可以把 event 看成是一種 input，藉由**純函式**轉換成一個 output 後，又當成另外一個函式的 input，進行連鎖反應：

```
input (event) -[func 1]-> output 
                          input -[func 2]-> output 
                                            input -[func 3]-> output                 
```

我們把這些**純函式**串連起來，並把中間的函式 I/O 當做是處理的中間狀態 (intermediate)，而最終產生出結果：

```
input (event) -> intermediate ->  ... -> intermediate -> output
```

這些 input、intermediate、output，都是一組暫時的資料，還不會影響程式的任何狀態。我們將他們用 **`Stream`** 包裝，並藉由純函式串接起來，形成[**資料流 (dataflow)**](https://en.wikipedia.org/wiki/Dataflow_programming)：

```
Stream (input) -> Stream (intermediate) ->  ... -> Stream (output)
```

另外，`Stream` 也是一個 `Observable`，可以被**訂閱 (subscription)**、引入**副作用**：

```
Stream (input) -> Stream (intermediate) ->  ... -> Stream (output)
    \                   \                               \
     -> side effect      -> side effect                  -> side effect
```

我們可以在 side effect 中，進行許多非純函數的**輸出**操作：

1. 輸出到記憶體：把資料同步到一個屬性、變數進行保存 (data binding)
2. 輸出到硬碟：包括 database 的處理，或是寫入檔案等
3. 輸出到螢幕：包括 print、或是 UI 改變、動畫等等
4. 其他 output 等等

而 input 的部份 (依賴)，我們都會包裝成 `Stream` 來處理。包括：

1. 使用者點擊螢幕 (touch event)
2. 設置一個時間觸發器 (timer)
3. 狀態追蹤 (observation)
4. 系統通知 (notification)
5. callback 
6. HTTP response
7. 硬碟資料讀取
8. 其他 input 等等


FRP 把事件包裝成 `Stream`，形成 dataflow，帶來了許多好處：

* 意味著不再有 delegate、key-value observation、block、target-action、notification 等自己的處理方式。所有的事件都統一轉換成 `Stream` 來處理，並提供了統一的處理介面。
* `Stream` 串起來的 **dataflow** 可以「分流」和「合併」，用簡單的語法組織起複雜的邏輯架構。
* 提供「依賴」和「副作用」封裝的方式，而可以著重在**純函式**的 dataflow 處理。

> 註1: 大多數 FRP 並不是真正的 FP，你可以在 `Stream` 形成的 dataflow 中，加入依賴或副作用，而變成 impure function，這是因為程式語言的許可。
>
> 註2: 事實上，`Stream` 就是 FP 中的 **`Monad`** 的實現，不過我們在這邊不會解釋它。


<a name="FRP-example"/>

## [FRP 簡單的例子](#FRP-example)

一個簡單的例子，使用者在輸入框輸入文字時，即時搜索結果並印出 (詳細請見 [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa#example-online-search))：

```swift
// 從 text field 中獲得使用者輸入字串的 stream
let searchStrings = textField.rac_textSignal()
    .toSignalProducer()
    .map { text in text as! String }

// 將字串 stream 轉成 HTTP 請求，而得到結果，並轉回到主線程
let searchResults = searchStrings
    .flatMap(.Latest) { (query: String) -> SignalProducer<(NSData, NSURLResponse), NSError> in
        let URLRequest = self.searchRequestWithEscapedQuery(query)
        return NSURLSession.sharedSession().rac_dataWithRequest(URLRequest)
    }
    .map { (data, URLResponse) -> String in
        let string = String(data: data, encoding: NSUTF8StringEncoding)!
        return self.parseJSONResultsFromString(string)
    }
    .observeOn(UIScheduler())

// 使用訂閱來引入 side effect，而將結果列印出來
searchResults.startWithNext { results in
    print("Search results: \(results)")
}
```

我們可以清楚的看到 dataflow 是如何處理事件，並且用很少的代碼在一個地方完成實作，而不必再把這些實作分散在不同的類別、方法中了！



<a name="signal-transduction"/>

## [FRP 的世界就像是細胞的 Signal transduction](#signal-transduction)

如果你無法想像一個充滿 `Stream` 的 FRP 真實世界是什麼樣，你可以參考生物學中的**[訊息傳遞 (Signal transduction)](https://en.wikipedia.org/wiki/Signal_transduction)**。

![11](https://upload.wikimedia.org/wikipedia/commons/2/29/Signal_transduction_v1.png)

簡單的解釋 signal transduction：

1. **環境監聽**：生物細胞藉由細胞膜表面的接受器 (receptor) 來偵測環境分子；*例如 `RKT 穿膜蛋白`*。
2. **觸發訊號**：一旦一個細胞外的特定環境因子觸發了接受器，接受器便會觸發一個細胞內的化學反應 (reaction)，將其轉換成分子訊號；*例如 `RKT` 偵測到了細胞外的生長因子 (growth factor)*。
3. **連鎖反應**：一個化學反應會將受質 (substrate) 轉換成產物 (product)，這個產物就是一種分子訊號。而該分子訊號將會影響細胞內的另一個生化反應，而引起連鎖反應，形成**訊號流**。*例如： `Grb2/SOS -> Ras -> Raf -> MEK...`*。
4. **調控**：這些影響分為**「促進 (`->`)」**和**「抑制 (`-|`)」**，在複雜的訊息網路中產生出狀態。
5. **訊號拆分**：一個訊號可以影響**多個下游**，稱為 **signaling cascades** (就像一個瀑布撞擊一個石頭後，會拆分成多個小瀑布)；因此即便是只偵測到一個外部的環境因子，也可以引發細胞全面性的改變，而不是只有單一的變化。*例如 `G-Protein` 影響了下游的 `Ras` `PLC` 和 `PI3K` 等*。
6. **訊號集結**：一個訊號可以被**多個上游**共同影響，決定出一個狀態。*例如：`Ras` 會被 `G-Protein` `Grb2/SOS` `Fyn/Shc` 等影響*。
7. **表現**：這些訊號分子，最終會影響著基因調控 (gene regulation)，甚至是細胞增生 (proliferation)、死亡 (apoptosis) 等。這些表現就是細胞面對外部刺激時，所表現出的應對反應。


細胞建立利用多種生化反應，以及中間物質 (intermediate substrate)，來形成複雜的細胞狀態及反應網絡；面對外界環境的刺激時，可以有效的快速調整細胞內的分子狀態，進而影響細胞的生命表現，來適應環境：

```
stimulation -> signal transduction -> express
```

程式就像是細胞一樣，充滿著複雜的狀態和事件處理。在**事件**和**反應**之間，需要個**訊息傳遞**網絡架構。而 FRP 就是組織這個訊息傳遞架構 (reactive dataflow network)：

```
events -> reactive dataflow network -> side effects
```

> 如果你想多了解 FRP/RP，可以參考這篇 [The introduction to Reactive Programming you've been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)。



<a name="learning-curve-and-cost"/>

## [學習成本與開發效率](#learning-curve-and-cost)

如果說從 OOP 改用 FRP 的「轉換」成本很低，那一定是騙人的。因為開發效率雖然提昇了，但是學習門檻卻也很高：

* 大多數的教學只教入門的特定情結使用方式
* 書籍只教「概念」、或是如何使用 FRP 的 API，沒有真實開發狀況的講解
* 缺乏進階內容，自己實作很容易遇到問題，踩到地雷。

當你只是用少量 FRP 來完成一些事情，那還可能容易實踐。但一旦決心要全面採用 FRP 開發，那剛開始的產能一定是很差的。因為會開始遇到許多高級的問題，而這些問題都是需要知識和經驗去排除的。若沒有人帶，而自己從錯誤中學習，是非常花時間的。

根據我的預估：

* 剛使用 FRP，開發維護的**效率**大概只有原本 OOP 的 50-80% (多出 25-100% 的成本)
* 熟悉 FRP 後，開發維護的**成本**大概只有原本 OOP 的 50-80% (增加了 25-100% 的效率)

也就是說，在熟悉 FRP 開發後，你的產能最高可以提昇至 2 倍左右。這是因為許多複雜的問題、資料的串接，在 FRP 下是十分直覺、可以輕鬆實踐的，在維護和開發上，可以省下可觀的成本。

那需要多久時間，才能讓 FRP 的開發效率超過原本 OOP 呢？我的預估是 1-3 個月，端看開發者的資質和努力，以及學習的途徑。

全面採用 FRP 開發後，大致的學習曲線和效率如下 (100% 為原本的 OOP 開發效率)：

* 第一個月：約 50 % 的開發效率。因為你會不斷遇到很多問題，需要學習的東西比想像多很多。
* 第三個月：約 100% 上下的開發效率。端看學習效率，突破了多少瓶頸。
* 半年：約 120% 的開發效率。你會慢慢看到 FRP 帶來的好處。對於整體的開發框架會有些想法。
* 一年：約 150-200+% 的開發效率，對大部分 FRP 框架的 API 已經算是十分了解，並知道如何避開麻煩。



<a name="conclusion"/>

## [總結](#conclusion)

FRP 帶來的好處，遠遠超過學習時帶來的挫折。以長期來看，學習並開始使用 FRP，可以算是很好的投資。而且，目前各平台都在推動 FRP 開發方式，將來要轉換開發平台，也可以說是事半功倍。

另外，有些人會把 FRP 當做是比較 "fency" 的 KVO、notification...等，而沒有深入到 FRP 的核心精神和帶來的好處，那會是十分可惜的。

我會在之後寫另外一篇來講解如何學習 FRP，要注意的問題，以及 FRP 在 iOS 的 best practice (包含架構)。


