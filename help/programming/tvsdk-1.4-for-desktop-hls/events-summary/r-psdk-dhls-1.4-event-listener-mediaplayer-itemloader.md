---
description: TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。
title: 載入器事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 載入器事件{#loader-events}

TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。

這些事件提供了另一種工作流程。 建立`MediaPlayer`時，不需要實施此介面。 當您想要擁有`MediaPlayerItemLoader`時，請使用此選項。

要獲知與載入媒體播放器資源相關的事件，請向`MediaPlayerItemLoader`對象註冊以下事件的偵聽器。

| 事件 | 意義 |
|---|---|
| MediaPlayerItemLoader。[已完成](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | 媒體資源載入成功完成。 |
| MediaPlayerItemLoader。[失敗](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | 載入介質資源時發生問題。 |