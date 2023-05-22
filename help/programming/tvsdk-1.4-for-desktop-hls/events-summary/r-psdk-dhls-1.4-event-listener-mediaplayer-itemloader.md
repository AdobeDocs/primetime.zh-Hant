---
description: TVSDK響應載入媒體項而調度媒體播放器項事件。
title: 載入程式事件
exl-id: ee5be2d4-5c77-4af4-b8fe-8cef18d7c0d9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 載入程式事件{#loader-events}

TVSDK響應載入媒體項而調度媒體播放器項事件。

這些事件提供了替代工作流。 建立 `MediaPlayer`。 當您想要 `MediaPlayerItemLoader`。

要獲知與載入媒體播放器資源相關的事件，請向 `MediaPlayerItemLoader` 的雙曲餘切值。

| 事件 | 意義 |
|---|---|
| MediaPlayerItemLoader。[已完成](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 媒體資源載入已成功完成。 |
| MediaPlayerItemLoader。[失敗](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 載入媒體資源時出現問題。 |
