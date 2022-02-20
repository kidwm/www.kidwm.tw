---
title: 外接內覆，絕緣開發
date: 2022-02-22
---

對於 [Wrap Third-Party Libraries](https://markus.oberlehner.net/blog/wrap-third-party-libraries/) 這個觀念的了解，最知名的應該是來自下面這一段話：

> In fact, **wrapping third-party APIs is a best practice.** When you wrap a third-party API, you minimize your dependencies upon it: You can choose to **move to a different library in the future without much penalty.** Wrapping also makes it easier to **mock out third-party calls when you are testing your own code.**
>
> One ﬁnal advantage of wrapping is that you aren’t tied to a particular vendor’s API design choices. **You can deﬁne an API that you feel comfortable with.**
>
> [Robert C. Martin](http://cleancoder.com/), Chapter 7, Error Handling, *Clean Code*

提到了三項主要的好處：

* 方便將來抽換至不同的 Library
* 單元測試可以容易 Mock
* 可以使用自己的風格來設計 API

> We can solve any problem by **introducing an extra level of indirection**, except for the problem of too many levels of indirection.
>
> *[Fundamental theorem of software engineering](https://en.wikipedia.org/wiki/Fundamental_theorem_of_software_engineering)*

還有些其它好處，比如當被包覆的工具在改版後有 Breaking Change 時，透過這個中間層(Indirection)就能集中處理掉，而不必到處去修改有使用到的檔案。

也能在 wrapper 這裡共享設定簡化呼叫介面，限制可用的功能，或是提供額外的功能。

> Every solution of a problem raises new unsolved problems
>
> Karl Popper, *Conjectures and Refutations*

當然還是有一些地方要注意，引入這個抽象層除了帶來額外的整合測試需求外，還得撰寫更多文件說明來緩解 [The Law of Leaky Abstractions](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)，但這些都是軟體開發本來就該做好的，我認為相較於好處來說壞處不大。

更多詳細的解說內容可以參考 [Why You Should (Often) Wrap Your Dependencies](https://levelup.gitconnected.com/why-you-should-often-wrap-your-dependencies-5fced2999616) 這篇文章。