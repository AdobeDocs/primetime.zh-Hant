---
description: TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。
seo-description: TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。
seo-title: 載入器事件
title: 載入器事件
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 載入器事件{#loader-events}

TVSDK會回應載入媒體項目，而調度媒體播放器項目事件。

這些事件提供了另一種工作流程。 建立MediaPlayer時，您不需要實作此介面。 當您想要擁有`MediaPlayerItemLoader`時，請使用此選項。

若要收到有關載入媒體播放器資源之事件的通知，請註冊`MediaPlayerItemLoader.LoaderListener`的實作，包括下列事件。

| 事件 | 意義 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) mediaPlayerItemplayerItem) | 媒體資源載入成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 載入介質資源時發生問題。 |

>[!NOTE]
>
>另請參閱QoS事件下的`onLoadInfo (loadInfo)`。

