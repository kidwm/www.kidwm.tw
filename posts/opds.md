---
title: 線上書庫格式 OPDS ─ Open Publication Distribution System
date: 2016-01-31
---
說到音訊檔案的訂閱，大家一定對 Podcast 不陌生，其實電子書籍也有一個發佈規格稱為 [OPDS](http://opds-spec.org/)，它以 [ATOM](https://tools.ietf.org/html/rfc4287) 為基底（後來有 2.0 版本草案則是採用 [JSON-LD](https://json-ld.org/)），揉合了 [OPML](http://www.opmlicons.com/) 的特性，提供線上書庫的瀏覽功能。

OPDS 在推廣網站上有將特色說明得很清楚，主要就是透過 [Catalog](http://discover-opds.org/catalog.html) 的功能，可以方便地讓讀者在陳列的書庫裡瀏覽、搜尋和購買書籍。

![Catalogs in Foliate](/images/Foliate_Catalogs.png)

由於 OPDS 發表以來似乎不甚為人熟知，僅能在此略舉一二有在使用 OPDS 發佈書庫內容的站點，英文的有 [Feedbooks](http://www.feedbooks.com/catalog) 與 [Standard Ebooks](https://standardebooks.org/opds/) 等些許來源，但目前中文的只看到[中華電子佛典協會](http://www.cbeta.org/opds)，至於其它私人收藏分享大概是礙於取得來源問題，幾乎是沒有見到（後來我在[寶島書庫](http://epub.tw/opds.xml)也有提供）。

其實除了書庫用途以外，OPDS 也很適合雜誌期刊、機關會報的發表，只是撇開內容來源的建置作業不談，電子書閱覽軟體也少有完善的 Aggregator 功能支援，缺乏相關通知機制以方便透過 OPDS 訂閱出版品，更何況目前主流的電子出版品流通平台仍是在各家 App 的封閉系統中。

希望在 Podcast 風行於世之後，不久的將來也能看到 OPDS 流行起來。
