---
description: TVSDK響應載入媒體項而調度媒體播放器項事件。
title: 載入程式事件
exl-id: 80a503f2-ad2e-44e5-93dc-2311df77f52e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 載入程式事件{#loader-events}

TVSDK響應載入媒體項而調度媒體播放器項事件。

這些事件提供了替代工作流。 建立MediaPlayer時不需要您實現此介面。 當您想要 `MediaPlayerItemLoader`。

要被通知有關載入媒體播放器資源的事件，註冊 `MediaPlayerItemLoader.LoaderListener` 包括以下事件。

| 事件 | 意義 |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([媒體播放器項](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | 媒體資源載入已成功完成。 |
| [上錯誤](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | 載入媒體資源時出現問題。 |

>[!NOTE]
>
>另請參閱 `onLoadInfo (loadInfo)` 在QoS事件下。
