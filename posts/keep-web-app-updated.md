---
title: 讓 Web App 持續跟進最新版
date: 2022-01-26
---
要讓網頁一直跟進最新版，直接了當的作法就是讓瀏覽器不要存下任何快取備份，每次都向伺服器拿取當前版本就行。

有對 Assets 做 Cache Busting 的話，透過針對 HTML 輸出設定 HTTP Header 的 [`Cache-Control`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) 為 `no-store` 就能達成。

但在不讓我們設定網頁伺服器的狀況下，我們也能透過 [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers) 來指示瀏覽器每次載入頁面時都略過快取來下載：

```js
self.addEventListener('fetch', function (event) {
  // we do not use cache at all, just for fetching latest html shell
  if (event.request.mode === 'navigate') {
    event.respondWith(fetch(event.request.url, {
      // make the response not involved with any cache
      cache: 'reload',
      // https://bugs.chromium.org/p/chromium/issues/detail?id=669363
      // do not follow the redirect in service worker
      redirect: 'manual'
    }).catch(() => new Response(
      '<p style="text-align: center">Network Offline</p>',
      {status: 200, headers: {'Content-Type': 'text/html; charset=UTF-8'}}
    )));
  }
});
```

藉由以上這些手法，至少達成了只要讓瀏覽器重新整理網頁就一定能呈現最新版的目標。

另外在發行新版本 Web App 後，如果不會保留前一版的檔案，再加上採用 [Code Splitting](https://developer.mozilla.org/en-US/docs/Glossary/Code_splitting) 拆分，在路徑改變時才會載入下一個頁面所需的檔案這樣的行為，會造成還在使用前一版的使用者切換到未載入過的頁面時因為抓取不到而出錯，使用 [webpack](https://webpack.js.org/) 打包時可以這樣處理這個狀況：

```js
window.addEventListener('error', e => {
  // when webpack loading chunk failed, usually it means there is a newer version deployed
  if (
    /Loading(\sCSS)? chunk [\d]+ failed/.test(e.message) &&
    sessionStorage.getItem('webpackChunkError') !== e.message
  ) {
    // record to prevent an infinite loop when still fail to load chunk after reloading
    sessionStorage.setItem('webpackChunkError', e.message);
    window.location.reload();
  }
});
```

在捕捉到這個錯誤的同時，讓使用者在切換頁面的過程中更新上去。
