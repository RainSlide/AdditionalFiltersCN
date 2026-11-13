# Bilibili Scripts



## Libraries

### KvSDK
`"//s1.hdslb.com/bfs/seed/jinkela/kv-sdk/index.js",{lib:"KvSDK"}`

- export `window.KvSDK`

- load ReporterPb

### ReporterPb

`"//s1.hdslb.com/bfs/seed/jinkela/short/reporter-pb/index.js",{lib:"ReporterPb"}`

- [fingerprint.js](https://github.com/fingerprintjs/fingerprintjs) subscript `https://s1.hdslb.com/bfs/seed/jinkela/short/reporter-pb/fingerPrint.js`

- export `window.ReporterPb`
- export `window.__ReporterPbGlobalState`

- load SecureCollectSDK

- `POST https://data.bilibili.com/v2/log/web`
- `POST https://api.bilibili.com/x/web-frontend/data/report`

### SecureCollectSDK

WASM-based encrypting periodic data report, contains another copy of [fingerprint.js](https://github.com/fingerprintjs/fingerprintjs).

`"//s1.hdslb.com/bfs/seed/jinkela/short/minntaki-wasm-sdk/bili-sc-sdk.umd.js"`

- export `window.SecureCollectSDK`

### BPNC / BPP2PSDK

`https://s1.hdslb.com/bfs/static/nc/nc-loader-*.min.js`

- 2.14.0 `https://s1.hdslb.com/bfs/static/nc/nc-loader-2.14.0.min.js`


## End of `<head>`

### Core Script

`https://s1.hdslb.com/bfs/static/player/main/core.*.js`

- `4.10.8-82b0378d (2026-10-27T14:46:44+08:00)`:
  `https://s1.hdslb.com/bfs/static/player/main/core.9c6ca999.js`

- has keyword `spm_id_from`

- load KvSDK & ReporterPb
- load `https://s1.hdslb.com/bfs/seed/jinkela/risk-captcha-sdk/CaptchaLoader.js`
- load `https://s1.hdslb.com/bfs/static/jinkela/video/video.*.js`
  - as of `4.10.8-82b0378d (2026-10-27T14:46:44+08:00)`:
    `https://s1.hdslb.com/bfs/static/jinkela/video/video.8c3699a3aaf218112dadb300b3127b36bdacfe5c.js`
  - has keyword `spm_id`
  - has keyword `spm_id_from`
  - has keyword `spmId`
  - has keyword `reportBrowserEvent()`
  - xhr.send `POST https://api.bilibili.com/x/web-frontend/data/collector`
- load npd scripts `https://s1.hdslb.com/bfs/static/player/main/widgets/npd.*.*.js`
  - load BPNC / BPP2PSDK
  - load ReporterPb

- xhr.send `GET https://api.bilibili.com/x/click-interface/click/now`
- xhr.send `POST https://api.bilibili.com/x/click-interface/click/web/h5`
- 视频观看进度：
  xhr.send `POST https://api.bilibili.com/x/click-interface/web/heartbeat`

### `@bilibili/log-reporter`

`https://s1.hdslb.com/bfs/seed/log/report/log-reporter.js`

- export `window.reportObserver`
- export `window.webpackLogReporter`

- read `window.reportConfig`
- read `window.abtest`
- read `window.performance`
- read `window.doNotTrack`
- write `window.sessionStorage.setItem("b_timer", ...)`

### `@bilibili/bili-mirror`

`https://s1.hdslb.com/bfs/seed/jinkela/short/b-mirror/biliMirror.umd.mini.js`

包含数据上报（biliMirror）、白屏检测与白屏截图上报

- export `window.__biliMirror__`
- export `window.__biliMirrorPbInstance__`

- load KvSDK & ReporterPb

- fetch `POST https://api.bilibili.com/x/web-frontend/action-log/upload`
- fetch `POST https://api.bilibili.com/x/web-frontend/action-log/upload-image`

- read `window.performance`
- read `window._naToH5`

### `@bilibili/bmg-unpkg`

包含图像自动 fallback 功能与数据收集上报（BMG_TRACKER / biliMirror）

HTML 中的注释：`<!-- 图片降级 -->`

实测没有任何主流浏览器需要图像 fallback，也没有观察到图像主 CDN（`i0.hdslb.com`）长时间掉线。

为防万一，解除屏蔽的规则如下：
``` adblock
@@||hdslb.com/bfs/seed/jinkela/short/bmg/register/*
```

`https://s1.hdslb.com/bfs/seed/jinkela/short/bmg/register/cmpt.js`

- has keyword `BMG_TRACKER`

- export `window.imgAutoFallbackOnLoad`
- export `window.imgAutoFallbackOnError`
- export `window.bmgOnload`
- export `window.bmgCmptOnload`
- export `window.bmgCmptOnerror`

- read `navigator.userAgent`
- read `window.__BMG_AF__`
- read `__BMG_TRACKER__`

`https://s1.hdslb.com/bfs/seed/jinkela/short/bmg/register/fallback.js`

- has keyword `spm_prefix`
- has keyword `spmId`
- has keyword `Miss reporter args`

- export `window.imgAutoFallbackOnLoad`
- export `window.imgAutoFallbackOnError`

- load KvSDK & ReporterPb

- read `window.biliMirror`
- read `window.__BMG_AF__`



## End of `<body>`

### 必火推广

`cm` 可能是 **C**o**M**mercial 的缩写。

`https://s1.hdslb.com/bfs/cm/cm-sdk/static/js/bili-collect.js`

### Captcha

`https://s1.hdslb.com/bfs/seed/jinkela/risk-captcha-sdk/CaptchaLoader.js`

### polyfill

features 可能会按 UA 变化，但即使是最新浏览器，也都会莫名加载 `globalThis` 的 polyfill。

`https://www.bilibili.com/gentleman/polyfill.js?features=globalThis`


### SVG animation player library

[SVGA](https://svga.dev/) 2023 年就停更了…

`https://s1.hdslb.com/bfs/seed/fehub/loki/unpkg/svgaplayerweb/svga.min.js`

### @bilibili/bili-user-fingerprint

唯一混淆的 JS，可使用：
- https://github.com/relative/synchrony
- https://github.com/HumanSecurity/restringer

`https://s1.hdslb.com/bfs/seed/jinkela/short/user-fingerprint/bili-user-fingerprint.min.js`

- export `window.__biliUserFp__`

- read `window.__USER_FP_CONFIG__`
- read `window.__MIRROR_REPORT__ || window.biliMirror`
