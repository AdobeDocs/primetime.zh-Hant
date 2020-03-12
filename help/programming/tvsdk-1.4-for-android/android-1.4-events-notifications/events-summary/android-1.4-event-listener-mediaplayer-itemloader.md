---
description: TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。
seo-description: TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。
seo-title: 載入器事件
title: 載入器事件
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 載入器事件{#loader-events}

TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。

這些事件提供了另一種工作流程。 建立MediaPlayer時，您不需要實作此介面。 當您想要擁有時，請使用這個 `MediaPlayerItemLoader`。

若要獲知與載入媒體播放器資源相關的事件，請註冊包含下 `MediaPlayerItemLoader.LoaderListener` 列事件的實作。

| 事件 | 意義 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 媒體資源載入成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 載入介質資源時發生問題。 |

>[!NOTE]
>
>另請參閱 `onLoadInfo (loadInfo)` QoS事件下。

