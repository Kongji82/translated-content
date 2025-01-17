---
title: AbortController：AbortController() 构造函数
slug: Web/API/AbortController/AbortController
l10n:
  sourceCommit: 15f0b5552bc9c2ea1f32b0cd5ee840a7d43c887e
---

{{APIRef("DOM")}}{{AvailableInWorkers}}

**`AbortController()`** 构造函数创建了一个新的 `AbortController` 实例。

## 语法

```js-nolint
new AbortController()
```

### 参数

无。

## 示例

在下面的这段代码中，我们将通过 [Fetch API](/zh-CN/docs/Web/API/Fetch_API) 来下载一段视频。

首先通过 {{domxref("AbortController.AbortController","AbortController()")}} 构造函数来创建一个 controller 实例，然后通过 {{domxref("AbortController.signal")}} 属性获取到它的关联对象 {{domxref("AbortSignal")}} 的引用。

当 [fetch 请求](/zh-CN/docs/Web/API/Window/fetch)初始化时，我们将 `AbortSignal` 作为一个选项传递进入请求的选项对象中（下面的 `{signal}`）。这将 signal 和 controller 与 fetch 请求相关联，并且允许我们通过调用 {{domxref("AbortController.abort()")}} 去中止它，如下面的第二个事件监听器。

```js
const controller = new AbortController();
const signal = controller.signal;

const url = "video.mp4";
const downloadBtn = document.querySelector(".download");
const abortBtn = document.querySelector(".abort");

downloadBtn.addEventListener("click", fetchVideo);

abortBtn.addEventListener("click", () => {
  controller.abort();
  console.log("Download aborted");
});

function fetchVideo() {
  fetch(url, { signal })
    .then((response) => {
      console.log("Download complete", response);
    })
    .catch((err) => {
      console.error(`Download error: ${err.message}`);
    });
}
```

> [!NOTE]
> 当 `abort()` 被调用，`fetch()` promise 将会抛出 `AbortError`。

你可以在 GitHub 上找到一个完整的使用示例——参见 [abort-api](https://github.com/mdn/dom-examples/tree/main/abort-api)（[也可以看在线演示](https://mdn.github.io/dom-examples/abort-api/)）。

## 规范

{{Specifications}}

## 浏览器兼容性

{{Compat}}

## 参见

- [Fetch API](/zh-CN/docs/Web/API/Fetch_API)
