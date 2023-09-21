---
description: TVSDK會傳送媒體播放器專案事件來回應載入媒體專案。
title: 載入器事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 載入器事件{#loader-events}

TVSDK會傳送媒體播放器專案事件來回應載入媒體專案。

這些事件提供替代工作流程。 建立「 」時，不需要實作此介面 `MediaPlayer`. 當您想要 `MediaPlayerItemLoader`.

若要收到有關載入媒體播放器資源之事件的通知，請使用 `MediaPlayerItemLoader` 物件。

| 事件 | 含義 |
|---|---|
| MediaPlayerItemLoader。[已完成](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 媒體資源載入已成功完成。 |
| MediaPlayerItemLoader。[失敗](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 媒體資源載入時發生問題。 |
