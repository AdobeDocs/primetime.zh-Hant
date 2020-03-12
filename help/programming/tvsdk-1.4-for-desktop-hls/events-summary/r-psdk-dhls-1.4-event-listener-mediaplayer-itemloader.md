---
description: TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。
seo-description: TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。
seo-title: 載入器事件
title: 載入器事件
uuid: 0ad37715-14b1-457c-892f-0db0d6220f0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 載入器事件{#loader-events}

TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。

這些事件提供了另一種工作流程。 建立時，不需要實施此介面 `MediaPlayer`。 當您想要擁有時，請使用這個 `MediaPlayerItemLoader`。

要獲知與載入媒體播放器資源相關的事件，請向對象註冊以下事件的監 `MediaPlayerItemLoader` 聽器。

| 事件 | 意義 |
|---|---|
| MediaPlayerItemLoader。[已完成](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 媒體資源載入成功完成。 |
| MediaPlayerItemLoader。[失敗](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 載入介質資源時發生問題。 |