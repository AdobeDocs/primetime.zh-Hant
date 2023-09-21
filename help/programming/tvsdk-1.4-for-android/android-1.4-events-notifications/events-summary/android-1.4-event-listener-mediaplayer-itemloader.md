---
description: TVSDK會傳送媒體播放器專案事件來回應載入媒體專案。
title: 載入器事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 載入器事件{#loader-events}

TVSDK會傳送媒體播放器專案事件來回應載入媒體專案。

這些事件提供替代工作流程。 建立MediaPlayer時不需要實作此介面。 當您想要 `MediaPlayerItemLoader`.

若要收到有關載入媒體播放器資源之事件的通知，請註冊實作 `MediaPlayerItemLoader.LoaderListener` 包括以下事件。

| 事件 | 含義 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 媒體資源載入已成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 媒體資源載入時發生問題。 |

>[!NOTE]
>
>另請參閱 `onLoadInfo (loadInfo)` 在QoS事件底下。
