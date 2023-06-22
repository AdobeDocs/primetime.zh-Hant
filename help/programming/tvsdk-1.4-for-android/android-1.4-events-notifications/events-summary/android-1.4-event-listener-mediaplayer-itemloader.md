---
description: TVSDK會傳送媒體播放器專案事件來回應載入媒體專案。
title: 載入器事件
exl-id: 80a503f2-ad2e-44e5-93dc-2311df77f52e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 載入器事件{#loader-events}

TVSDK會傳送媒體播放器專案事件來回應載入媒體專案。

這些事件提供替代工作流程。 建立MediaPlayer時不需要實作此介面。 當您想要擁有 `MediaPlayerItemLoader`.

若要收到有關載入媒體播放器資源之事件的通知，請註冊實作 `MediaPlayerItemLoader.LoaderListener` 包括以下事件。

| 事件 | 含義 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 媒體資源載入已成功完成。 |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 媒體資源載入時發生問題。 |

>[!NOTE]
>
>另請參閱 `onLoadInfo (loadInfo)` 在QoS事件底下。
